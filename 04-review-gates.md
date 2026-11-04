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
