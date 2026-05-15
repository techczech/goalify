# Goal Contract Template

Use this template to draft a Codex `/goal` prompt after inspecting the target project.

```text
/goal Complete <objective> without stopping until <verifiable end state>.

Project: <absolute path or clear repo name>

Read first:
- <project instruction file>
- <architecture/readme/plan/issue/log>

Objective:
- <one durable outcome>

Scope:
- Change: <allowed files, modules, behaviours, docs>
- Preserve: <public APIs, UX, data model, privacy/security rules>
- Do not touch: <generated files, unrelated work, secrets, lockfiles unless needed>

Checkpoints:
1. <first evidence-gathering or safety checkpoint>
2. <implementation or repair checkpoint>
3. <validation and documentation checkpoint>
4. <handoff checkpoint>

Validation loop:
- Run <command>.
- Run <command>.
- If validation fails, inspect the failure, make the smallest relevant change, and rerun the failing check before continuing.

Progress log:
- After each checkpoint, record current checkpoint, files changed, checks run, evidence, remaining work, and blockers.

Pause if:
- A destructive command, secret, credential, external production system, schema migration, publishing step, or product decision is required.
- The working tree contains unrelated changes that would be overwritten.

Stop when:
- <same verifiable end state, expressed as concrete passing checks or artifacts>

Final handoff:
- Summarise changed files, validation commands and results, known risks, and any manual follow-up.
```

## Review Checklist

- Does the first line start with `/goal` and name both the outcome and stop condition?
- Can Codex verify progress without asking the user after every step?
- Are the validation commands real for this repo?
- Is the scope small enough that one long-running agent can finish it?
- Does the goal say when to pause instead of pushing through ambiguity?
- Does the final handoff make review easy?
