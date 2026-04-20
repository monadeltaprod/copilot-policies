# copilot-policies

Manages GitHub Copilot organisation policies for **monadeltaprod**, including enabling premium models in Copilot CLI.

## Fixing "Blocked / Disabled" models in Copilot CLI

If you see the error below when running `/model` in Copilot CLI:

```
Available  [Blocked / Disabled]
These models are not currently available. They may be disabled by
your organization's policy or not included in your plan.

  gpt-5.4 / gpt-5.1 / claude-sonnet-4.x / claude-opus-4.x
```

there are two ways to fix it:

### Option 1 — Run the GitHub Actions workflow (recommended)

1. Add a repository secret called **`COPILOT_ADMIN_TOKEN`** — a PAT with `manage_billing:copilot` scope, owned by an organisation owner.
2. Navigate to **Actions → Enable Premium Copilot Models → Run workflow**.
3. Accept the default org (`monadeltaprod`) and click **Run workflow**.

The workflow will attempt to enable the Copilot CLI policy and each premium model via the GitHub REST API and print a summary of what was changed. Any settings that can only be changed through the UI will be listed with direct links.

### Option 2 — Manual UI steps (org owner required)

1. Go to **https://github.com/organizations/monadeltaprod/settings/copilot/policies**
   → Set **Copilot in the CLI** to **Enabled**.
2. Go to **https://github.com/organizations/monadeltaprod/settings/copilot/models**
   → Enable each premium model: GPT-5.4, GPT-5.1, Claude Sonnet 4.6, Claude Sonnet 4.5, Claude Opus 4.7, Claude Opus 4.6, Claude Opus 4.6-fast, Claude Opus 4.5.

## Copilot CLI custom agent

This repository also ships a **`copilot-policy-helper`** custom agent (`.github/agents/my-agent.agent.md`). Once this branch is merged into the default branch, you can invoke it from Copilot CLI:

```
/agent copilot-policy-helper
```

The agent will check your org's current policy state and guide you through the fix.