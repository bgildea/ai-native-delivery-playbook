# 6. Cost, risk and team adoption

Notes for leads and managers bringing AI-native delivery into a team.

## Start with one workflow, not the whole team

Pick a team and a type of work with good test coverage, like a plugin or an internal tool. Agree the review gates first. Measure before and after.

## What to measure

- Lead time from ticket to merge
- Review time per change, and change size
- Escaped defects (bugs found after release)
- Spend on AI tools per engineer

If lead time drops but escaped defects rise, the review gates aren't working.

## Risks and controls

| Risk | Control |
| --- | --- |
| Secrets or customer data pasted into prompts | Clear policy, secret scanning, redacted fixtures |
| Licensing of generated code | Company policy on AI tool use; review new dependencies |
| Skills atrophy in junior engineers | Pairing, and juniors explain AI-written code in review |
| Over-trusting confident output | Tests as the contract; human gates on risky areas |
| Cost creep | Per-team budgets, track spend alongside delivery metrics |

## Changing the role of the product owner

Specs get read literally and acted on in minutes. That rewards product owners who write clear acceptance criteria and examples, and it punishes vague tickets faster than before. Expect backlog refinement to become more important, not less.

## Writing it down

Keep a short failure log: what went wrong, why, and what changed (often a line in `CLAUDE.md` or a new test). Over a few months it becomes the team's real playbook.
