# Week 9 gate demonstrations

The project uses `week9-lab-reference.zip`; `is212-week9-demos.zip` contains separate lecture examples. This lab has no submission requirement.

- [Baseline CI](https://github.com/0xjunwei/is212-week9-lab/actions/runs/38105091360): lint, test, audit, package, smoke, and e2e all passed. Deployment ZIP and SPDX SBOM were generated.
- [Checkbox regression PR #2](https://github.com/0xjunwei/is212-week9-lab/pull/2): removing `value="1"` left source/API checks green, but e2e received $1.50 instead of $3.00. Closed without merging.
- [AWS workflow PR #3](https://github.com/0xjunwei/is212-week9-lab/pull/3): both deployment jobs download the same artifact and print AWS CodeSha256.
- [Packaging exercise PR #4](https://github.com/0xjunwei/is212-week9-lab/pull/4), [failing run](https://github.com/0xjunwei/is212-week9-lab/actions/runs/38105867002): omitting `duckfine.py` left lint, test, audit, and package green; smoke and e2e failed with `No module named 'duckfine'`. GitHub disabled merging. The package copy line is restored in this PR.

`main` requires a pull request, an up-to-date branch, and passing `test`, `smoke`, and `e2e` checks; administrators must follow the rule. The production environment requires reviewer `0xjunwei`. Temporary AWS credentials are saved only as GitHub environment secrets and must be refreshed for a new Learner Lab session.
