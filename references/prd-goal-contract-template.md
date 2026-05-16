# PRD Goal Contract Template

Use this template when a `/goal` prompt should be tied to product intent rather than only code elements. First reconstruct or read a tight PRD/spec, then turn that PRD/spec into a durable Codex goal. If the PRD/spec is too generic or has not been clarified through at least one answered question, switch to `prd-interview-history-template.md` before drafting the goal.

The `/goal` prompt is a chat artifact. Do not save it inside the PRD/spec. Do not paste a full PRD or discovery notes into the `/goal`; reference the PRD/spec path.

```text
/goal Complete the product outcome specified in <PRD/spec path> without stopping until <verifiable product acceptance state>.

Project: <absolute path or clear repo name>

Read first:
- <PRD/spec path>
- The repo's local agent instructions and developer docs needed to work safely.

Do not treat discovery notes, interview history, repo-history notes, or AGENTS.md commentary as the implementation specification. If the PRD/spec has an ambiguity, pause for clarification instead of mining discovery notes for hidden requirements.

Objective:
- Implement the recommended product outcome in the PRD/spec.

Scope:
- Change: <allowed UX, docs, tests, parser logic, product copy, release artefacts from the PRD/spec>
- Preserve: <privacy, permissions, local-only behaviour, workflows, APIs, existing release rules from the PRD/spec>
- Do not touch: <unrelated features, generated files, secrets, publishing steps, broad redesigns>

Checkpoints:
1. Read the PRD/spec and identify the acceptance criteria, constraints, and non-goals.
2. Map PRD/spec acceptance criteria to code/docs/tests and identify the smallest product gap.
3. Implement the smallest coherent change set that closes that gap.
4. Validate with the repo's real checks and any manual/product evidence the PRD/spec requires.
5. Update docs only where behaviour or acceptance criteria changed.

Validation loop:
- Run <repo command>.
- Run <repo command>.
- If product behaviour is UI-visible, run or describe the concrete browser/app verification path.
- If validation fails, inspect the failure, make the smallest relevant change, and rerun the failing check before continuing.

Progress log:
- After each checkpoint, record current checkpoint, PRD/spec criterion addressed, files changed, checks run, evidence, remaining work, and blockers.

Pause if:
- The PRD source is ambiguous or conflicts with code behaviour.
- The work requires a new product decision, privacy change, broad redesign, external service, secret, destructive command, release/publish step, or overwriting unrelated work.
- The goal would still boil down to "improve", "finish", "clean up", or "make better" without verifiable product evidence.

Stop when:
- <product acceptance state> is demonstrated by passing checks plus concrete product evidence.

Final handoff:
- Summarise changed files, PRD/spec criteria satisfied, validation commands and results, remaining risks, and follow-up product decisions.
```

## Review Checklist

- Does the goal name the product outcome, not just a code chore?
- Are the success criteria traceable to stated project goals?
- Are non-goals and privacy/security constraints preserved?
- Is there a clear bridge from PRD criteria to files, tests, docs, or app verification?
- Can Codex stop on evidence rather than a feeling that the project is "better"?
- Was the Goalify interview/question gate completed before this prompt was drafted?
