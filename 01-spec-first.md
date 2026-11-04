# 1. Spec first

When a model can write a working first draft in minutes, the bottleneck moves upstream. A vague ticket used to cost a day of an engineer's questions. Now it costs a confident, plausible implementation of the wrong thing.

## What a good spec contains

- **The problem in one paragraph**, including who has it
- **Acceptance criteria** a tester (or a test) can check without asking anyone
- **Constraints**: the stack, files not to touch, performance or security limits
- **Out of scope**, stated explicitly. Models fill gaps generously
- **Examples**: an input and the output you expect, or a similar existing feature to copy

## Write acceptance criteria as tests you could run

```gherkin
Given a member with an active annual subscription
When they buy a conference ticket
Then the member price is applied
And the Stripe charge carries product metadata "conference-ticket"
```

Criteria in this shape translate straight into automated tests, which is exactly what you want the model to write next.

## The product owner's job changes

The spec is read by two audiences now: engineers and models. Both do better with fewer adjectives and more examples. A good habit is to ask the model to restate the spec and list its questions before any code is written. Its questions are usually the gaps a junior engineer would have hit two days in.

## Checklist

- [ ] Could someone build this without talking to me?
- [ ] Is every acceptance criterion testable?
- [ ] Have I said what *not* to change?
- [ ] Is there at least one concrete example?
