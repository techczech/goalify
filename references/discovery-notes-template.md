# Discovery Notes Template

Use this when Goalify needs to preserve the evidence, interview trail, and process material that should not live in the PRD/spec.

```text
# <Project Name> Discovery Notes

Purpose:
- Support the PRD/spec at <prd path or title> without becoming the implementation target.

Repo evidence:
- Source docs: <README, roadmap, issues, PRDs, release notes, design docs>
- Local instructions: <AGENTS.md or CLAUDE.md constraints that affected the work>
- Code shape: <modules, tests, scripts, UI, config>
- History: <commit/tag/release direction, if useful>

Concept map:
- Canonical terms: <terms and definitions>
- Ambiguous terms: <terms needing clarification>
- Conflicting terms: <docs/code/user language conflicts>
- Missing terms: <concepts that need names>

Interview trail:
- Question: <question asked>
- Recommended answer: <agent proposal>
- User answer: <answer>
- Decision: <concept, boundary, quality criterion, non-goal, feature priority, or acceptance criterion clarified>

Assumptions and open questions:
- Product assumptions: <assumptions not yet confirmed>
- Process assumptions: <notes for future discovery, not implementation spec>

Rejected or deferred ideas:
- <idea>: <why rejected or deferred>

Links:
- PRD/spec: <path>
- Related docs: <paths>
```

## Rules

- This is allowed to be messy and historical. The PRD/spec is not.
- Keep AGENTS.md observations, repo-history notes, interview history, and agent reasoning here.
- When a note becomes a product requirement, rewrite it into the PRD/spec as a concise constraint or acceptance criterion.
- Do not ask the later `/goal` agent to read this file unless the user explicitly wants broader background.
