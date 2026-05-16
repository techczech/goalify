# PRD Document Template

Use this when Goalify needs to create or revise the PRD document before drafting a `/goal`. Keep it concrete enough that a future Codex run can decide what to build, what not to build, and how to know when it is done.

```text
# <Project Name> PRD

Status:
- Draft | User-confirmed | Ready for /goal

Last updated:
- <date or conversation marker>

Purpose:
- <why this project should exist, in user-facing terms>

Primary user:
- <person or role>

Workflow:
- Before: <what the user does now>
- During: <what the product should let them do>
- After: <what changes because the product worked>

Pain removed:
- <specific friction, risk, or cost>

Product principles:
- <principle that rules work in or out>
- <principle that protects quality or scope>
- <principle that reflects the user's taste or constraints>

Feature inventory:
- Core now: <current features that define the product>
- Incomplete: <features that exist but fail the desired standard>
- Missing: <features needed for the next useful version>
- Deferred: <valuable later, not now>
- Not a feature: <tempting but explicitly out of scope>

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
- <criterion that confirms documentation or product understanding is updated>

Evidence:
- Source: <docs, instructions, issues, plans>
- History: <commits, releases, tags, direction of travel>
- Code: <implemented modules, tests, scripts, UI>
- User confirmed: <interview decisions>

Open decisions:
- <question that must be answered before implementation>

Recommended goal:
- <one bounded product outcome ready for `/goal`, or "not ready yet">
```

## Rules

- Prefer observable product states over generic improvements.
- Keep definitions and principles short enough to use during implementation.
- Record feature boundaries explicitly; the no-s are as useful as the yes-s.
- Separate evidence from inference.
- If the PRD is not ready for `/goal`, say exactly which decision is missing.
