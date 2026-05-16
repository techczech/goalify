---
name: goalify
description: Turn a coding or development project into a clear PRD and effective Codex `/goal` task. Use when the user asks to inspect a repo, project, codebase, backlog, issue, roadmap, PRD, product goals, interview them about goals, review repo history, construct a proper product document, or create a long-running goal prompt with clear scope, checkpoints, validation commands, progress reporting, pause conditions, and a verifiable stopping condition.
---

# Goalify

## Overview

Convert a project into a durable product understanding and, when appropriate, a Codex `/goal` contract. The output should help Codex keep working across turns on one verifiable objective, not merely restate a normal coding prompt.

Goalify is an interview skill before it is a drafting skill. Its job is to clarify concepts, sharpen terminology, and test the user's assumptions until the project language is clear enough for an agent to work safely.

Use official Codex guidance as the baseline: `/goal` is for long-running work with one objective, a validation loop, and a clear end state. It is experimental and requires `features.goals` to be enabled, either through `/experimental` or `[features] goals = true` in `config.toml`.

Goalify has two products:

- A PRD document that captures the project's purpose, users, principles, features, missing pieces, quality criteria, non-goals, and open decisions.
- A `/goal` prompt generated from that PRD once the product outcome is clear enough to execute.

## Non-Negotiable Interview Contract

When Goalify is used for a PRD, roadmap, product goal, feature goal, or Codex `/goal`, you must ask clarification questions before declaring the work ready.

- Ask at least one real clarification question and wait for the user's answer before producing a final PRD, final goal prompt, or "ready" conclusion.
- Default to one question at a time. Do not dump a questionnaire unless the user explicitly asks for a batch.
- For each question, provide your recommended answer and the evidence or assumption behind it. The user should react to a concrete proposal.
- A long user suggestion is not a substitute for the interview. Treat it as evidence, identify the most load-bearing ambiguous term or decision, and ask about that first.
- If you can answer a question by reading docs, code, tests, issues, or history, inspect those first. Then ask only the unresolved conceptual question.
- Do not say "I have enough" until the user has answered at least one clarification question in this Goalify session and the PRD readiness check passes.
- If the user asks you to "just draft it", still ask one concept-clarifying question first unless they explicitly say "do not ask questions".

## Workflow

1. Resolve the target project path and read its local instructions first:
   - `AGENTS.md`, `CLAUDE.md`, `README.md`, package manifests, architecture docs, release docs, roadmap files, tests, CI config, and obvious issue/backlog files.
   - Use `rg --files`, `rg`, and targeted file reads. Avoid broad generated/build directories such as `node_modules`, `dist`, `build`, `target`, `.next`, and `.venv`.
2. Inspect project state without changing it unless the user explicitly asked for edits:
   - Check `git status --short --branch`.
   - Note dirty, ahead/behind, or untracked state in the goal report because a long-running goal may otherwise trample user work.
   - If the goal would create or edit files, include a first checkpoint to pull/rebase safely and preserve local changes.
3. Build a concept map before drafting:
   - Identify key terms the user used, terms from docs, and terms implied by the code.
   - Flag overloaded words, synonyms, unresolved concepts, and conflicting definitions.
   - Use concrete scenarios to expose whether the terms actually mean what everyone thinks they mean.
4. Decide whether the next output should be a PRD, a `/goal`, or both:
   - Use `/goal` for migrations, large refactors, release hardening, multi-step test repair, benchmark/eval improvement, prototype completion, documentation refreshes tied to validation, and deployment retry loops.
   - Use PRD-first mode when the user asks to be interviewed, says the goal is unclear, asks for a proper document, asks for product principles, or wants to decide what the project should become before starting a long-running goal.
   - Do not force `/goal` onto a loose backlog, a vague aspiration, a one-file edit, or unrelated chores. In those cases, say that a normal prompt or a split set of goals is better.
5. Choose the goal frame:
   - Use an engineering contract when the user wants implementation, validation, migration, tests, release hardening, or code quality work.
   - Use a PRD contract when the user wants the goal tied to product intent, stated goals, user workflow, non-goals, acceptance criteria, or roadmap shape.
   - Use a constructed PRD contract when the user asks to build the PRD by interviewing them and reviewing code or repo history. In this mode, do not rush to the `/goal`; build the PRD first.
6. Choose one objective:
   - Make it bigger than one turn but smaller than "improve this whole repo".
   - Anchor it in repo evidence: current scripts, docs, missing validation, stated non-goals, failing checks, release routine, or product goals.
7. Draft the goal using the relevant contract:
   - Use `references/goal-contract-template.md` for engineering-contract goals.
   - Use `references/prd-goal-contract-template.md` for product/PRD-shaped goals.
   - Use `references/prd-interview-history-template.md` when the PRD must be constructed from user interview plus repo evidence.
   - Use `references/prd-document-template.md` when writing or revising the PRD document itself.
8. Include the exact command or first message the user can paste into Codex:
   - Start with `/goal`.
   - Name the objective and the stopping condition in the first sentence.
   - Keep the rest as structured instructions inside the same prompt.

## Output Shape

For direct goal-generation mode, return:

1. `Recommended /goal prompt` with one copyable prompt block.
2. `Why this is goal-shaped` in 2-4 bullets.
3. `PRD trace` when product goals are part of the request: product goal, users/workflow, acceptance criteria, non-goals, and evidence.
4. `Evidence used` with the project files or commands that informed the goal.
5. `Before running` with any setup or safety notes, including how to enable goals if needed.

If the user asks for several options, provide at most three goal candidates and mark one as recommended.

For interview-led PRD mode, return work in stages:

1. `Evidence pass`: what the repo already says, what history suggests, what the code contradicts, and what remains unknown.
2. `Concepts to clarify`: key terms, overloaded words, conflicting definitions, and assumptions that would change the goal.
3. `Interview`: ask one question at a time unless the user explicitly asks for a batch. For each question, provide a recommended answer based on the evidence and explain what decision it unlocks. End the message on the question and wait.
4. `Working PRD`: update the PRD draft as decisions crystallise. If the user asked for a file, create or update it in the requested path; otherwise present it in chat.
5. `Goal readiness`: say whether the PRD is ready for a `/goal`, and list the remaining decisions if it is not.
6. `Recommended /goal prompt`: generate this only after the PRD has a concrete product outcome, acceptance criteria, non-goals, validation evidence, and at least one answered clarification question.

## Constructing a PRD

When the user wants the PRD constructed through interview plus repo review:

1. Do a fast evidence pass before asking questions:
   - Read existing goal/product sources.
   - Inspect `git log --oneline --decorate -20`, recent tags, release notes, issue/backlog files, and major source modules.
   - Identify what the repo history suggests the project has been optimising for.
2. Ask only what cannot be answered from the repo:
   - If a question can be answered by exploring docs, code, tests, issues, or history, explore first instead of asking.
   - Ask one question at a time by default. Walk the design tree in dependency order so early answers constrain later questions.
   - For each question, provide your recommended answer. The user should be reacting to a concrete proposal, not a blank form.
   - Ask about the intended user, painful workflow, desired product state, feature boundaries, missing features, quality criteria, non-goals, success evidence, and priority trade-offs.
   - Do not ask questions already answered clearly by repo docs or history.
   - Never move straight from a long user suggestion to a completed PRD or `/goal`. Ask the first load-bearing clarification question first.
3. Challenge fuzzy or contradictory language:
   - Call out vague outcomes such as "improve", "make better", "clean up", or "finish the app" and replace them with observable product states.
   - If the user uses a term that conflicts with repo docs or code behaviour, surface the conflict immediately and ask which meaning should win.
   - Use concrete scenarios and edge cases to force precision around users, workflows, data, permissions, and quality bars.
4. Produce a proper PRD document:
   - Separate evidence from inference.
   - Mark assumptions that came from repo history rather than direct user confirmation.
   - Include product principles, feature inventory, missing features, quality criteria, acceptance criteria, non-goals, constraints, and open decisions.
   - Keep implementation detail out unless it changes product scope, validation, or constraints.
5. Generate a `/goal` from the PRD only after the product outcome is clear.

## Goal Contract Requirements

Every generated goal must include:

- One objective.
- One verifiable stopping condition.
- A stated-goal trace when the project has product goals, PRD language, user workflows, non-goals, or acceptance criteria.
- Files, docs, logs, issues, or plans to read first.
- Scope boundaries and explicit non-goals.
- Checkpoints that Codex can complete independently.
- Validation commands or artifacts, using commands found in the repo whenever possible.
- A progress-log instruction: current checkpoint, verified evidence, remaining work, blockers.
- Pause conditions for ambiguity, risky changes, secrets, destructive operations, permissions, or product decisions.
- Final handoff requirements: changed files, commands run, evidence, remaining risks.

When using a constructed PRD, also include the interview questions, the user's answers, the repo-history evidence, and unresolved assumptions.

Reject generic goals. A goal is not ready if it can be summarised as "improve the project", "make the docs better", "clean up the UI", or "finish the app" without naming the user-visible state, acceptance criteria, and validation evidence.

Reject ungrilled goals. A goal is not ready if no clarification question has been answered in the current Goalify session.

## Prompting Rules

- Prefer concrete repo commands over generic phrases like "run tests".
- Preserve the project's own AGENTS instructions and release rules.
- Mention dirty worktrees and generated directories so the goal can avoid them.
- Keep the prompt ambitious but bounded. A goal should not ask Codex to own product strategy, rewrite everything, or keep iterating forever.
- Follow the spelling, terminology, and tone already used by the target project.
- Never invent tests, scripts, CI, pricing, APIs, or release steps. If validation is missing, make "add minimal validation" an explicit checkpoint.
- Do not hide unresolved product decisions inside implementation tasks. Ask, decide, or mark the assumption before drafting the `/goal`.
- Prefer ending an early Goalify response with the next question rather than a completed artifact. The interview is the work.

## Reference

Read:

- `references/goal-contract-template.md` when drafting or reviewing an engineering-contract goal prompt.
- `references/prd-goal-contract-template.md` when drafting or reviewing a PRD/product-goal prompt.
- `references/prd-interview-history-template.md` when constructing a PRD by interviewing the user and reviewing code/history.
- `references/prd-document-template.md` when writing the PRD document before drafting the `/goal`.
