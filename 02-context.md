# 2. Context is the product

The difference between useful and useless AI output is mostly context. Claude Code reads a `CLAUDE.md` file at the root of the repo, which makes it the natural place to keep what a new team member would need on day one.

## What goes in CLAUDE.md

- How to run, test and lint the project (exact commands)
- Architecture in a few lines: main folders and what lives where
- Conventions: naming, error handling, how we write tests
- Hard rules: never edit generated files, never commit `.env`, migrations go through review
- Domain words the code uses, so the model doesn't invent synonyms

Keep it short. A long file gets skimmed by people and diluted for models. See the [starter template](templates/CLAUDE.md.example).

## Point at examples, not descriptions

"Follow our plugin structure" is weak. "Model it on `includes/class-ticket-totals.php`" is strong. One good existing file is worth a page of style guide.

## Give it the boundaries

State what's off limits for the task: files, services, data. For payments, authentication and anything touching customer data, say explicitly that changes need human review before merge.

## Keep context fresh

When a review finds the same mistake twice, the fix usually belongs in `CLAUDE.md`, not in another review comment.
