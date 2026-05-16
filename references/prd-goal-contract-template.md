# PRD Goal Contract Template

Use this template when a `/goal` prompt should be tied to product intent rather than only code elements. First reconstruct or read a PRD from the repository's own stated goals, then turn that PRD into a durable Codex goal. If the PRD is too generic or has not been clarified through at least one answered question, switch to `prd-interview-history-template.md` before drafting the goal.

```text
/goal Complete <product outcome> without stopping until <verifiable product acceptance state>.

Project: <absolute path or clear repo name>

Read first:
- <product-goal source: README, AGENTS, PRD, roadmap, issue, transcript, docs>
- <architecture/source files needed to connect product intent to implementation>

PRD trace:
- Product purpose: <why the project exists, in the project's own terms>
- Key terms: <canonical concepts and resolved ambiguities>
- Target users/workflow: <who uses it and what they are trying to do>
- Current stated goals: <features, behaviours, release goals, reliability goals>
- Product principles: <rules that distinguish the right product from a generic improvement>
- Feature inventory: <core now, incomplete, missing, deferred, out of scope>
- Quality criteria: <observable standards for UX, correctness, reliability, privacy, accessibility, maintainability, or docs>
- Non-goals/constraints: <what must remain out of scope>
- Success criteria: <observable user-facing and technical acceptance criteria>

Objective:
- <one durable product outcome that serves the stated goals>

Scope:
- Change: <allowed UX, docs, tests, parser logic, product copy, release artefacts>
- Preserve: <privacy, permissions, local-only behaviour, workflows, APIs, existing release rules>
- Do not touch: <unrelated features, generated files, secrets, publishing steps, broad redesigns>

Checkpoints:
1. Reconstruct or read the PRD from the stated-goal sources and save or report it before implementation.
2. Verify that at least one clarification question has been asked and answered in this Goalify session. If not, ask one before drafting or executing the goal.
3. Verify the PRD is not a generic "improve this" brief: it must name product principles, key terms, feature boundaries, quality criteria, acceptance evidence, and non-goals.
4. Map PRD acceptance criteria to code/docs/tests and identify the smallest product gap.
5. Implement the smallest coherent change set that closes that gap.
6. Validate with the repo's real checks and any manual/product evidence the PRD requires.
7. Update docs only where behaviour or acceptance criteria changed.

Validation loop:
- Run <repo command>.
- Run <repo command>.
- If product behaviour is UI-visible, run or describe the concrete browser/app verification path.
- If validation fails, inspect the failure, make the smallest relevant change, and rerun the failing check before continuing.

Progress log:
- After each checkpoint, record current checkpoint, PRD criterion addressed, files changed, checks run, evidence, remaining work, and blockers.

Pause if:
- The PRD source is ambiguous or conflicts with code behaviour.
- The work requires a new product decision, privacy change, broad redesign, external service, secret, destructive command, release/publish step, or overwriting unrelated work.
- The goal would still boil down to "improve", "finish", "clean up", or "make better" without verifiable product evidence.
- No clarification question has been answered in the current Goalify session.

Stop when:
- <product acceptance state> is demonstrated by passing checks plus concrete product evidence.

Final handoff:
- Summarise the reconstructed PRD, changed files, product criteria satisfied, validation commands and results, remaining risks, and follow-up decisions.
```

## Review Checklist

- Does the goal name the product outcome, not just a code chore?
- Are the success criteria traceable to stated project goals?
- Are non-goals and privacy/security constraints preserved?
- Is there a clear bridge from PRD criteria to files, tests, docs, or app verification?
- Can Codex stop on evidence rather than a feeling that the project is "better"?
