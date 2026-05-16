# PRD Interview And History Template

Use this template when the PRD does not already exist clearly enough and must be constructed from user interview plus repo evidence. The first deliverable is shared product understanding. Draft the `/goal` only after the PRD is specific enough to execute.

The interview is mandatory. Do not treat a long user suggestion as enough context. It is raw material for the first clarification question.

## Evidence Pass

Before interviewing, inspect:

- Local instructions: `AGENTS.md`, `CLAUDE.md`, `README.md`.
- Product docs: PRDs, roadmaps, release notes, design notes, architecture docs, backlog files, issue exports.
- Repo history: `git log --oneline --decorate -20`, recent tags, version bumps, release commits, and large feature commits.
- Code shape: package manifests, routes/views, core modules, tests, CI/workflows, scripts, and config.
- Current state: `git status --short --branch`.

Capture evidence as short bullets. Label each bullet as `source`, `history`, or `code`. Also capture:

- Product principles already implied by docs or architecture.
- Features already present.
- Missing or half-present features.
- Quality signals: tests, validation, UX checks, performance, accessibility, privacy, reliability, release process.
- Contradictions between docs, code, and user statements.
- Domain terms and product terms that need canonical definitions.
- Words the user used that could mean more than one thing.

## Concept Clarification

Before drafting a PRD, create a small concept map:

- `Canonical terms`: terms already defined by docs, UI, code, issues, or the user's stable language.
- `Ambiguous terms`: words that could mean several things.
- `Conflicting terms`: words where docs, code, and user intent appear to disagree.
- `Missing terms`: concepts the product needs but has not named yet.

When a term is ambiguous, ask. Do not silently choose a meaning unless the answer is obvious from repo evidence. A good clarification question names the competing meanings:

```text
You keep saying "session". I see the code using that word for a saved browser run, but your description sounds like a training workshop. I recommend reserving "session" for the workshop and calling the saved run a "capture". Is that the distinction you want?
```

Keep concept definitions out of implementation detail. Define what the concept is in the product or domain, not how the code stores it.

## Interview Questions

Ask only what the evidence pass cannot answer. Ask one question at a time by default, waiting for feedback before continuing. The first Goalify response after evidence gathering should end with a question, not with a completed PRD or `/goal`.

For each question:

- Say what repo evidence triggered it.
- Provide the recommended answer based on that evidence.
- Say what downstream decision it unlocks.
- If the user uses vague or overloaded language, propose a precise term or product state.
- If code and user intent conflict, ask which should win.
- Wait for the user's answer before moving to the next branch or declaring readiness.

Walk down the design tree in dependency order:

1. Who is the primary user for this project right now?
2. What workflow or pain should this project make easier?
3. What would make the next version feel genuinely useful rather than merely more complete?
4. Which existing features are core, incomplete, accidental, or deprecated?
5. What missing features would change the product's usefulness the most?
6. What quality criteria matter: correctness, UX, speed, privacy, accessibility, reliability, maintainability, deployment, or documentation?
7. What must stay out of scope?
8. What evidence would convince you the goal is done?
9. If the code and your preference disagree, which should Codex optimise for?

Do not ask all questions mechanically. Stop only when the PRD can name a product outcome, principles, key terms, features, missing pieces, quality criteria, acceptance evidence, and non-goals. If the user has already provided strong product context, state the assumptions and ask for confirmation of the riskiest one. Do not skip that confirmation.

## Question Gate

Before saying the PRD or `/goal` is ready, verify:

- At least one clarification question has been asked in this Goalify session.
- The user has answered it.
- The answer changed, confirmed, or rejected a concept, boundary, quality criterion, feature priority, non-goal, or acceptance criterion.
- Any remaining unanswered questions are listed as open decisions or pause conditions.

If this gate fails, ask the next clarification question instead of drafting the final artifact.

## Stress Tests

Use concrete scenarios to prevent generic goals:

- "A first-time user opens this. What should they understand or accomplish in the first two minutes?"
- "What is a realistic failure case this version must handle gracefully?"
- "Which tempting feature would make the product worse or blur its purpose?"
- "What would count as done in a screenshot, command output, test report, or short demo?"
- "What would a future maintainer misunderstand if we do not write it down?"

Surface contradictions directly:

```text
The README frames this as <X>, but the code currently optimises for <Y>. I recommend treating <X> as the product principle and <Y> as implementation drift unless you tell me otherwise. Is that right?
```

## Constructed PRD Shape

```text
# <Project Name> PRD

Status:
- Draft | User-confirmed | Ready for /goal

Product purpose:
- <one-paragraph purpose grounded in user answers and repo evidence>

Key terms:
- <canonical term>: <tight definition>
- Avoid: <ambiguous or rejected term>

Primary user and workflow:
- User: <who>
- Workflow: <before -> during -> after>
- Pain removed: <specific friction>

Current evidence:
- Source evidence: <docs/instructions>
- History evidence: <commit/tag/release direction>
- Code evidence: <implemented shape>

Product principles:
- <principle 1 with evidence or user confirmation>
- <principle 2 with evidence or user confirmation>
- <principle 3 with evidence or user confirmation>

Feature inventory:
- Core now: <features that already define the product>
- Incomplete: <features present but not good enough>
- Missing: <features the user wants or evidence implies>
- Not a feature: <tempting but rejected features>

Quality criteria:
- UX: <observable interaction standard>
- Correctness: <data/output behaviour>
- Reliability/performance: <if relevant>
- Privacy/security/permissions: <if relevant>
- Maintainability/docs: <if relevant>

Non-goals and constraints:
- <non-goal>
- <privacy/security/permission/performance/release constraint>

Acceptance criteria:
- <user-facing criterion with evidence>
- <technical criterion with validation command or artifact>
- <documentation/PRD criterion if needed>

Open assumptions:
- <assumption, labelled as user-confirmed, repo-inferred, or unresolved>

Clarification history:
- Asked: <question>
- Answered: <user answer>
- Decision: <concept, boundary, criterion, or priority clarified>

Goal candidates:
- Recommended: <one bounded product outcome>
- Later: <deferred goal>
```

## PRD Readiness Check

A PRD is ready for `/goal` only when:

- The primary user and workflow are named.
- Key product concepts are named and ambiguous terms are resolved or listed as open decisions.
- The product principles are specific enough to reject plausible but wrong work.
- The feature inventory distinguishes present, missing, incomplete, and out-of-scope features.
- Quality criteria are observable.
- Acceptance criteria can be verified by commands, artifacts, screenshots, demos, or manual checks.
- At least one clarification question has been answered in this Goalify session.
- Open assumptions are either low-risk or explicitly called out in the `/goal` pause conditions.

If this check fails, keep interviewing or inspect more repo evidence. Do not paper over gaps with generic language.

## Goal Prompt Template

```text
/goal Complete <constructed-PRD outcome> without stopping until <acceptance criteria and validation evidence> are satisfied.

Project: <absolute path or repo name>

Read first:
- <constructed PRD if saved, otherwise the interview answers in this prompt>
- <repo source files/docs/history evidence>

Constructed PRD:
- Product purpose: <purpose>
- Key terms: <canonical concepts and resolved ambiguities>
- Primary user/workflow: <user/workflow>
- Product principles: <principles>
- Feature inventory: <core/incomplete/missing/out-of-scope>
- Quality criteria: <observable standards>
- Non-goals/constraints: <constraints>
- Acceptance criteria: <criteria>
- Clarification history: <questions answered and decisions made>
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
3. Identify the smallest coherent product gap that satisfies the recommended goal.
4. Implement the change set that closes that gap without drifting into later goals.
5. Validate with repo commands and product evidence.
6. Update the PRD or docs if implementation clarifies the product contract.

Validation loop:
- Run <repo command>.
- Run <repo command>.
- If UI-visible, verify the relevant workflow in browser/app and record evidence.

Progress log:
- After each checkpoint, record PRD criterion, files changed, checks run, product evidence, remaining work, and blockers.

Pause if:
- An assumption needs product confirmation.
- The requested work conflicts with repo instructions, privacy constraints, release rules, or unrelated local changes.
- The implementation would satisfy a vague improvement but not the PRD acceptance criteria.

Stop when:
- <acceptance criteria> pass and the final handoff connects changes back to the constructed PRD.

Final handoff:
- Include the PRD summary, interview assumptions, repo-history evidence, changes, validation results, and remaining decisions.
```
