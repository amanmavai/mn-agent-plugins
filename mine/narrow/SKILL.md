---
name: narrow
description: Simplify by supporting less. Find unused flexibility (options, env vars, fallbacks, modes), propose constraints that remove it, and apply the ones the user approves. Use when asked to simplify a design, script, API, config or process by adding constraints or cutting options. For behavior-preserving cleanup, use essence.
---

# Narrow

Every option, fallback and supported case is a path that has to stay correct. Paths nobody takes are paths nobody tests, so that's where the bugs sit. Narrow what the thing supports to how it's actually used, and the code, the docs and the bugs shrink together.

This changes behavior on purpose. `essence` keeps behavior identical; `narrow` removes support for cases. Removing support is the user's decision, so propose first and apply only what they approve.

## The test

An assumption is **safe** when breaking it either can't happen in this setup, or makes the thing stop with a clear error. A wrong guess then costs one retry.

An assumption is **unsafe** when breaking it silently produces wrong state: bad data, lost work, a wrong commit, wrong output that looks right. Keep the guard for these, however rare the case.

Every constraint you add needs one of three things: a check that enforces it, an existing error that already covers it, or a reason it can't break here.

## Workflow

1. **Find the real usage.** Name the thing and who uses it, how. Get evidence, not guesses: call sites, config files that exist, scripts that invoke it, docs that describe it. Say it in one or two lines.
2. **List the flexibility.** Every option, flag, env var, fallback, mode, alternate path, and general case. For each one ask: who uses this today, and when did this path last run?
3. **Propose constraints.** One row each:

   | Constraint | Removes | If broken | Enforced by |
   |---|---|---|---|
   | Run from the main checkout only | self-check, ambiguous branch base | error on start | existing check at line 40 |

   "If broken" says loud or silent. Drop any row that would fail silently.
4. **Ask.** Show the table and let the user pick. Note any rows that reverse an earlier deliberate decision.
5. **Apply.** For each approved constraint, add its check, delete the code it makes dead, and write the constraint down where the next reader will look: the file header, the docs, the usage text. Run the project's checks.
6. **Report.** What went, roughly how much smaller it got, and which constraints now hold.

## Where flexibility hides

- Options, flags and env vars nobody sets
- Support for many when there is one: remotes, backends, platforms, editors, config locations
- Fallbacks for environments that don't exist here
- Two ways to run or call the same thing: sourced and executed, sync and async, CLI and library
- Two config sources doing one job
- "Works from anywhere" when it's always run from one place
- Glob or regex matching where the inputs are a fixed short list
- Resume, reattach and retry paths that nobody uses
- In a process: steps, approvals or handoffs that exist for people who aren't involved

Bugs found in rarely-run paths are evidence. Mention them in the proposal.

## Keep it when

- It guards against silent damage
- Real users exist outside what you can see: a public API, another team, other machines
- Loosening it again later would be expensive. Narrowing pays off when undoing it takes minutes.

## Done when

- Each remaining constraint is enforced, already covered by an error, or can't break here
- Each constraint is written down
- No failure mode went from loud to silent
- There is less to read than before
