# Output template

---

## Branch summary: `<branch-name>` → `<base-branch>`

**<brief description of what this branch does>**

**Type**: {change_type, inferred from commits/diffs; omit if unclear}
**Why**: {reason, inferred from commits/diffs; omit if unclear}

### Visual overview

<!-- ASCII diagram: architecture, data flow, or component relationships. Omit for trivial changes.-->

### [Theme heading chosen from the actual change intent.]

- One concrete evidence-backed change per bullet.
- Keep bullets specific and reviewer relevant.

### [Another theme heading.]

### Notes

- Include only when needed
- Use for risk, validation caveats, follow-ups, migration warnings, or uncertainty.

**Visual overview**: Include when changes touch architecture, data flow, or component relationships. Useful patterns: before and after transformations, component trees, data flow pipelines. Skip it entirely for config tweaks, copy updates, or renames.

## Principles

- **Grounded, not speculative.** Every claim traces to the diff. If unclear, flag it.
- **Visual first.** Lead with a diagram when structure changes, skip it when structure doesn't.
- **Why over what.** The diff shows what changed. Your job is to explain why.
- **2-4 thematic headings.** Group by concern, not by file.
- **Name headings well.** "API refactoring", not "Changes". Use sentence case.
- **Skip noise.** Formatting-only changes, lock files, and incidental edits don't earn a bullet.
