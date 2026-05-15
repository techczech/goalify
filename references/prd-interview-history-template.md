# PRD Interview And History Template

Use this template when the PRD does not already exist clearly enough and must be constructed from user interview plus repo evidence.

## Evidence Pass

Before interviewing, inspect:

- Local instructions: `AGENTS.md`, `CLAUDE.md`, `README.md`.
- Product docs: PRDs, roadmaps, release notes, design notes, architecture docs, backlog files, issue exports.
- Repo history: `git log --oneline --decorate -20`, recent tags, version bumps, release commits, and large feature commits.
- Code shape: package manifests, routes/views, core modules, tests, CI/workflows, scripts, and config.
- Current state: `git status --short --branch`.

Capture evidence as short bullets. Label each bullet as `source`, `history`, or `code`.

## Interview Questions

Ask only what the evidence pass cannot answer. Prefer one short batch.

Good default questions:

1. Who is the primary user for this project right now?
2. What workflow or pain should this project make easier?
3. What would make the next version feel genuinely useful rather than merely more complete?
4. What must stay out of scope?
5. What evidence would convince you the goal is done?
6. If the code and your preference disagree, which should Codex optimise for?

For smaller requests, ask only the top 2-3 questions. If the user has already provided strong product context, skip the interview and state the assumptions.

## Constructed PRD Shape

```text
Constructed PRD

Product purpose:
- <one-paragraph purpose grounded in user answer and repo evidence>

Primary user and workflow:
- User: <who>
- Workflow: <before -> during -> after>
- Pain removed: <specific friction>

Current evidence:
- Source evidence: <docs/instructions>
- History evidence: <commit/tag/release direction>
- Code evidence: <implemented shape>

Product principles:
- <principle 1>
- <principle 2>
- <principle 3>

Non-goals and constraints:
- <non-goal>
- <privacy/security/permission/performance/release constraint>

Acceptance criteria:
- <user-facing criterion>
- <technical criterion>
- <validation evidence>

Open assumptions:
- <assumption, labelled as user-confirmed or inferred>
```

## Goal Prompt Template

```text
/goal Complete <constructed-PRD outcome> without stopping until <acceptance criteria and validation evidence> are satisfied.

Project: <absolute path or repo name>

Read first:
- <constructed PRD if saved, otherwise the interview answers in this prompt>
- <repo source files/docs/history evidence>

Constructed PRD:
- Product purpose: <purpose>
- Primary user/workflow: <user/workflow>
- Product principles: <principles>
- Non-goals/constraints: <constraints>
- Acceptance criteria: <criteria>
- Open assumptions: <assumptions>

Objective:
- <one product outcome based on the constructed PRD>

Scope:
- Change: <allowed docs/code/tests/UI>
- Preserve: <constraints and product principles>
- Do not touch: <unrelated/generated/secret/release areas>

Checkpoints:
1. Re-read the constructed PRD and repo instructions; note any conflicts before editing.
2. Map acceptance criteria to code, docs, tests, and manual verification.
3. Implement the smallest coherent change set that satisfies the criteria.
4. Validate with repo commands and product evidence.
5. Update the PRD or docs if implementation clarifies the product contract.

Validation loop:
- Run <repo command>.
- Run <repo command>.
- If UI-visible, verify the relevant workflow in browser/app and record evidence.

Progress log:
- After each checkpoint, record PRD criterion, files changed, checks run, product evidence, remaining work, and blockers.

Pause if:
- An assumption needs product confirmation.
- The requested work conflicts with repo instructions, privacy constraints, release rules, or unrelated local changes.

Stop when:
- <acceptance criteria> pass and the final handoff connects changes back to the constructed PRD.

Final handoff:
- Include the PRD summary, interview assumptions, repo-history evidence, changes, validation results, and remaining decisions.
```
