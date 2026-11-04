# 5. Evaluating AI features

When the feature itself is powered by an LLM (a chat assistant, a summariser, an agent with tools), unit tests aren't enough. Output varies, and "looks fine" in a demo is not evidence.

## Build an eval set early

- Start with 20 to 50 realistic inputs, including the awkward ones: ambiguous requests, rude users, off-topic questions, attempts to make it do something it shouldn't
- Write down what a good answer looks like for each, as a rubric, not an exact string
- Grow the set every time a real failure is reported

## Score it automatically where you can

| Check | How |
| --- | --- |
| Did it call the right tool with valid arguments? | Deterministic assertions |
| Did it refuse what it should refuse? | Deterministic assertions on a labelled set |
| Is the answer correct and grounded? | Rubric scoring by a person, or a model grader you've checked against people |
| Did it leak data it shouldn't? | Pattern checks plus red-team cases |

## Make it a release gate

Run the eval set on every prompt change, model upgrade or tool change. A change that improves one case and quietly breaks five others is common. The eval set is how you see it.

## Track it in production

- Thumbs up and down, plus the conversation for review
- Handoff or escalation rate
- Cost and latency per conversation

The [telegram-claude-agent](https://github.com/bgildea/telegram-claude-agent) repo has a small working example of an eval suite.
