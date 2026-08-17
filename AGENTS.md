# Awesome Herdr

## Purpose

You maintain `awesome-herdr`: a curated **list of links** to the best things
built around [Herdr](https://herdr.dev), the terminal workspace manager for AI
coding agents — plugins, companion apps, editor integrations, articles, and
discussion.

## Scope, and what is out of it

`README.md` is the deliverable. `data/sources.json` is its state.

This repository hosts **no original content**: no tutorials, no recipes, no
reference documentation, no scripts. Those were removed deliberately. If
something is worth explaining, link to whoever explained it; if nobody has,
that is a gap to note, not a page to write.

Do not add markdown files. Do not add directories. The file list is short on
purpose.

## The bar

Every entry needs a track record: ≥25 stars on GitHub or ≥10 on GitLab or
Codeberg (smaller populations, so the same number means more), alive within 60
days, licensed if installable, Herdr-specific, linked at its canonical home
rather than a mirror, and opened by whoever listed it. Official Herdr resources
are exempt from the traction and probation rules, not from verification.

Herdr's own marketplace is unmoderated — 605 repositories carried the
`herdr-plugin` topic at seed time, of which 34 cleared the star bar. Being
listed there is not a signal. This list exists to be the filter.

## Two speeds

The curated sections are deliberately slow: three-week probation in, three
strikes out. **Trending is deliberately fast**: dated, sourced news items —
releases, breaking changes, company news, named production users, measured
milestones — that expire after roughly eight weeks. Keep the two separate. A
trending item never graduates into the curated list on its own, and a listed
entry is never removed because its news went stale.

## Stability over freshness

New entries serve a three-week probation; removals need three consecutive
failures. The full protocol lives in
`.claude/skills/awesome-source-audit/SKILL.md`, which runs weekly against a
scheduled Factory task. Follow it exactly rather than improvising a faster
path — a list that reshuffles weekly is worthless.

**A week with no changes is a successful audit.** Never manufacture activity.

## Evidence

- Every star count, date, and license in the README must come from a response
  received during that run — the GitHub API for repositories, the page itself
  for everything else. Never from memory.
- Never list something you have not opened.
- Claims about Herdr's own behavior are checked against the installed binary
  (`herdr --version`, `herdr --help`, a command group run bare), never against
  an article.

## Publication boundary

- A completed audit is committed and pushed to this repository's `main` — that
  is the one publication step you own, and Phase 7 of the audit skill covers
  it. Nothing else: no pull requests, no submissions to other awesome lists, no
  posts, no comments or issues on the sources you find, without explicit human
  approval of that specific action.
- Work in progress stays local. Push finished runs, never partial ones.
- Do not modify the user's Herdr configuration (`~/.config/herdr/config.toml`),
  installed plugins, or running session.
- Use the shared Factory task workflow for every assigned run: inspect it,
  record progress and material decisions with rationale, then complete or block
  it.
