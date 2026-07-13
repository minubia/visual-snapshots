# CI/CD Pipeline Setup Prompt

You are helping me set up a CI/CD pipeline for this project using GitHub Actions.

The project is in the current working directory. Before asking me anything, explore the repo to discover:
- Package manager (check package.json `packageManager` field or lock files)
- Framework / build system (vite, next, etc.)
- Whether Supabase is used (look for `supabase/` dir, edge functions, migrations)
- Whether Firebase is used (look for `firebase.json`, `.firebaserc`)
- Test scripts available (check `package.json` scripts)

Then set up the following pipeline:

## Branch strategy
- `dev` → no automated action
- `test` branch (push/merge) → run all tests, then deploy to **staging** (environment: `test`)
- `main` branch (push/merge) → run tests only, no deploy
- **Production deploy** → manual trigger only (`workflow_dispatch`)

## Workflow files to create
1. `.github/workflows/deploy-staging.yml` — triggers on push to `test`
   - Jobs: test → build → deploy-hosting + deploy-functions (if applicable)
   - Status check name: `test-before-merging`
   - Notify on failure (email) — only if SMTP secrets are configured

2. `.github/workflows/test-main.yml` — triggers on push to `main`
   - Job name: `test-before-merging`
   - Run tests only, no deploy
   - Notify on failure (email) — only if SMTP secrets are configured

3. `.github/workflows/deploy-production.yml` — manual trigger only
   - Input: confirm (must type "deploy")
   - Check for `DEPLOY_HOLD` file in repo root — abort if present
   - Jobs: guard → test → build → deploy-hosting + deploy-functions (if applicable)
   - Uses environment: `main`

## Rules
- Use `pnpm` if `packageManager` field in package.json specifies it; otherwise detect from lock file
- Only include Supabase function deploy steps if a `supabase/functions/` directory exists
- Only include Firebase deploy steps if `firebase.json` exists
- Firebase authentication uses a service account (not a token):
  ```yaml
  - uses: google-github-actions/auth@v2
    with:
      credentials_json: ${{ secrets.FIREBASE_SERVICE_ACCOUNT }}
  - run: firebase deploy --only hosting:...
  ```
- SMTP email notifications are **optional** — use env var + step output pattern to skip gracefully if secrets not set:
  ```yaml
  - name: Check SMTP configured
    id: smtp
    env:
      SMTP_SERVER: ${{ secrets.SMTP_SERVER }}
    run: |
      if [ -n "$SMTP_SERVER" ]; then
        echo "configured=true" >> $GITHUB_OUTPUT
      else
        echo "configured=false" >> $GITHUB_OUTPUT
      fi
  - name: Email on failure
    if: ${{ steps.smtp.outputs.configured == 'true' && contains(needs.*.result, 'failure') }}
  ```
- Add `env: FORCE_JAVASCRIPT_ACTIONS_TO_NODE24: true` at workflow level
- Environments are named `test` and `main` (not staging/production)

## After creating the workflows, tell me:
- What GitHub repository secrets to add (per environment: `test` and `main`)
- What GitHub environments to create
- How to test the pipeline
