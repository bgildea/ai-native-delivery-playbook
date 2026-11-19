# 4. Review gates

AI-written code goes through the same gates as anyone's, plus a few extra checks for the mistakes models tend to make.

## Automated gates (every change)

- Lint and formatting
- Type checks
- Unit and integration tests in CI
- Secret scanning
- Dependency audit

## Human gates (always)

| Area | Why a person must review |
| --- | --- |
| Payments (Stripe, Omise, refunds, webhooks) | Money moves; mistakes are expensive and public |
| Authentication and permissions | Easy to get subtly wrong, hard to notice |
| Data migrations | Often irreversible |
| Anything touching personal or health data | Legal and trust exposure |
| New dependencies | Supply-chain risk; models sometimes suggest packages that don't exist |

## What to look for in AI-written code

- Invented APIs, functions or config options that look right but don't exist
- Error handling that swallows failures quietly
- Tests that assert on mocks rather than behaviour
- Duplicated logic that already exists elsewhere in the codebase
- Security basics: input validation, escaping output, nonces and capability checks in WordPress

Use the [review checklist](templates/review-checklist.md) on any change you didn't write by hand.

## Worked example: reviewing an AI-written payment change

This is an illustrative example, not taken from a real codebase. It uses the conference ticket spec from [chapter 1](01-spec-first.md):

> Given a member with an active annual subscription, when they buy a conference ticket, then the member price is applied and the Stripe charge carries product metadata "conference-ticket".

The model came back with this function and test. Both look fine at a glance, CI is green, and the summary says "all acceptance criteria met".

```js
export async function chargeTicket(member, ticket) {
  const price = member.plan === 'annual' ? ticket.memberPrice : ticket.price;
  try {
    return await stripe.paymentIntents.create({
      amount: price,
      currency: 'eur',
      metadata: { product: 'conference-ticket' },
    });
  } catch (err) {
    console.log(err);
    return null;
  }
}
```

```js
test('applies member price', async () => {
  stripe.paymentIntents.create = vi.fn().mockResolvedValue({ id: 'pi_1' });
  await chargeTicket({ plan: 'annual' }, ticket);
  expect(stripe.paymentIntents.create).toHaveBeenCalled();
});
```

Payments sit in the human gates table above, so a person reviews it. These are the comments that reviewer would leave.

**Blocking: the criterion says "active".** This checks the plan type but not whether the subscription is still active, so a member whose annual plan lapsed last year still gets the member price. Please check status as well, and add a test for an expired annual member that expects the full price.

**Blocking: the failure is swallowed.** If Stripe declines the card or the call times out, this logs and returns `null`, and the caller has no way to tell that apart from a bug. Let the error propagate (or return an explicit failure the caller must handle), and add a test where `paymentIntents.create` rejects.

**Blocking: the test checks the mock was called, not what it was called with.** It would still pass if the code charged the full price or dropped the metadata. Assert on the arguments: `amount` equals `ticket.memberPrice` and `metadata.product` is `'conference-ticket'`. That turns the acceptance criterion into the test.

**Question: units.** Stripe expects `amount` in the smallest currency unit (cents for EUR). Is `ticket.memberPrice` stored in cents? If not, this charges a hundredth of the price. Either way, a test with a known price would make it obvious.

### What makes these comments useful

- Each one points at the spec or the checklist, not at taste. "The criterion says active" is hard to argue with
- Each says what goes wrong for a real user, not just what the code does
- Each ends with a concrete fix and the test that would prove it
- Blocking and non-blocking are labelled, so the next round is focused

Notice that every problem here passed CI. The automated gates checked that the code ran; only the review checked that it did the right thing. That is why payments, auth and migrations always get a person.
