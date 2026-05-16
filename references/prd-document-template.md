# PRD Document Template

Use this when Goalify needs to create or revise the PRD/spec document before drafting a `/goal`. This document is the implementation target, not the working log.

The PRD/spec must be tight. Do not include interview history, evidence dumps, AGENTS.md notes, repo-history notes, process commentary, or agent reasoning. Put those in `discovery-notes-template.md`.

```text
# <Project Name> PRD

Status:
- Draft | User-confirmed | Ready for /goal

Purpose:
- <why this project should exist, in user-facing terms>

Primary user:
- <person or role>

Key terms:
- <canonical term>: <tight product/domain definition>
- Avoid: <ambiguous synonym or rejected term>

Workflow:
- Before: <what the user does now>
- During: <what the product should let them do>
- After: <what changes because the product worked>

Product principles:
- <principle that rules work in or out>
- <principle that protects quality or scope>
- <principle that reflects the user's taste or constraints>

Feature specification:
- Core: <features that define the product>
- Missing or changed: <features required for the next useful version>
- Deferred: <valuable later, not now>
- Out of scope: <tempting but explicitly rejected features>

Quality criteria:
- UX: <observable interaction standard>
- Correctness: <expected output/data behaviour>
- Reliability/performance: <if relevant>
- Accessibility: <if relevant>
- Privacy/security/permissions: <if relevant>
- Maintainability/docs: <if relevant>

Acceptance criteria:
- <criterion that can be verified by a user-visible workflow>
- <criterion that can be verified by a command, test, artifact, screenshot, or demo>
- <criterion that confirms documentation or product understanding is updated, if relevant>

Constraints:
- <product, technical, privacy, release, or compatibility constraint that changes what can be built>

Open product decisions:
- <decision that must be resolved before implementation, or "None">
```

## Rules

- Keep this document normative: what the product must become.
- Keep it cheap for a future implementation agent to read.
- Include only constraints that affect the product or implementation target.
- Translate repo instructions into concise constraints only when they affect the target. Do not write "AGENTS.md says..." notes here.
- Do not include evidence, interview history, clarification history, assumptions trail, discarded options, or process notes.
- If the PRD is not ready for `/goal`, list only the product decision that is missing.
