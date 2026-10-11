# IS212 Week 9: QuackLoan

Week 9 lab project based on the professor's `week9-lab-reference.zip`.
The separate `is212-week9-demos.zip` contains lecture examples.

## Run locally

Use Python 3.13, matching the GitHub Actions workflow and AWS Lambda runtime.

```sh
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m unittest discover -v
python -m flask --app app run --port 5001
```

Open `http://localhost:5001/` to check a fine. Five days late costs $1.50,
or $3.00 for a Deluxe duck. `/health` reports service health, and
`/fine?days=5&deluxe=1` returns the fee as JSON.

## Pipeline

The workflow runs lint, unit and integration tests, and a dependency audit.
It builds one deployment ZIP and an SBOM, then runs smoke and browser tests
against that ZIP. Staging and production use GitHub environments; production
requires approval by the configured reviewer.

The workflow deploys the tested ZIP to AWS Lambda in staging, runs the smoke
tests against its Function URL, and waits for production environment approval.
Production receives the same ZIP and runs the same smoke tests. The supplied
`pipeline-with-aws-deploy.yml.txt` remains available as the professor's reference.

For AWS deployment, use `us-east-1` and Python 3.13 Lambda functions named
`quackloan-staging` and `quackloan-prod`. Configure each GitHub environment
with `FUNCTION_NAME` and `FUNCTION_URL` variables and these temporary secrets:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_SESSION_TOKEN`

Enter credentials only in GitHub Actions secrets. Refresh them when the AWS
Learner Lab session changes.

## Browser and smoke tests

The GitHub workflow installs Playwright and tests the packaged app.
To run browser tests locally, start the app above and use another terminal:

```sh
python -m pip install playwright
python -m playwright install chromium
BASE_URL=http://localhost:5001/ python -m unittest discover -s e2e -v
bash smoke.sh http://localhost:5001
```

The production gate and checks should be configured before promoting a
release. Required branch checks are `test`, `smoke`, and `e2e`.
