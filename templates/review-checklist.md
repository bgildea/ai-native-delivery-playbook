# Review checklist for AI-assisted changes

## Does it do the right thing?
- [ ] Matches the acceptance criteria, nothing extra
- [ ] Out-of-scope areas untouched

## Is it real?
- [ ] Every API, function and config option used actually exists
- [ ] New dependencies are real, maintained and needed

## Is it tested?
- [ ] Tests exercise behaviour, not mocks
- [ ] At least one failure path is tested
- [ ] CI is green

## Is it safe?
- [ ] No secrets, tokens or personal data in code, tests or fixtures
- [ ] Input validated, output escaped
- [ ] Payments, auth and migrations reviewed by a person who understands them

## Is it maintainable?
- [ ] No duplicated logic
- [ ] Naming matches the codebase
- [ ] I could explain this change to a colleague without the model
