# Contributing

This repository is a list of links and nothing else. There are no tutorials,
recipes, or reference pages here, and additions of that kind are out of scope —
if you have written one, the contribution is a link to it.

## The bar

An entry belongs here if all of these hold:

1. **It has a track record.** At least 25 stars on GitHub, or 10 on GitLab or
   Codeberg — those hosts have far smaller populations, so the same count
   represents more adoption. Comparable public traction also counts: a
   front-page Hacker News thread, a widely shared post, a known publication.
   Official Herdr resources are exempt.
   Link the canonical home. A GitLab or Codeberg mirror of a GitHub project is
   the same entry, and it belongs under wherever development actually happens.
2. **It is alive.** Pushed or published within the last 60 days, not archived,
   and licensed if it is installable.
3. **It is Herdr-specific.** A general terminal tool that merely mentions Herdr
   does not qualify.
4. **You used it.** Not "it looks good" — you installed the plugin, or read the
   article end to end, on the current Herdr release.
5. **It is not redundant.** If it is better than something already listed, say
   so and propose the replacement. Two entries doing the same job means one
   should go.

Articles are held to one more rule: substantive first-hand accounts only —
configs, measurements, named limitations. Not SEO filler, and not a listicle
restating Herdr's README.

## Entry format

```markdown
- [name](https://github.com/owner/repo) — What it does, in one sentence,
  ending with who it is for. ⭐ 398 · MIT
```

- One line per entry, however long — the README is not hard-wrapped. Leave
  re-wrapping to whatever you read it in.
- Em dash (`—`) between name and description, not a hyphen.
- The star count and license are the evidence; take them from the GitHub API on
  the day you add the entry, not from memory.
- No superlatives, no "blazingly fast", no emoji in descriptions.
- Version-specific behavior gets an explicit note: "(0.8.0+)".

Sections are ordered by usefulness to a newcomer. A section needs two entries
to exist, and holds at most eight — at the cap, adding means retiring the
weakest incumbent. A single entry with no company goes in Extras.

Many plugins keep `herdr-plugin.toml` in a subdirectory, and
`herdr plugin install` needs the full path. If yours does, put it in the entry:
`openclaw/crabbox/plugins/herdr`, not `openclaw/crabbox`.

## Trending entries

The [Trending](README.md#trending) section plays by opposite rules: it is
supposed to move. An item needs a **date**, a **source link**, and to be an
actual event — a release, a breaking change, company news, a named production
user, or a measured milestone. Items expire after roughly eight weeks or when
superseded, and there is no probation, because news that waits three weeks is
not news.

What never belongs there: undated claims, unlinkable figures, reviews that are
not news, and old items kept alive to make the section look busy.

## How entries age

Entries are tracked in [`data/sources.json`](data/sources.json) and re-verified
weekly by the `awesome-source-audit` skill. Two rules shape what to expect:

- **New entries serve a probation.** Something qualifying must be seen in three
  consecutive weekly audits before it appears in the README. Official Herdr
  resources are the only exception.
- **Removals need three consecutive failures.** One dead fetch is not a
  removal. The exceptions are immediate: archived with a pointer elsewhere,
  malicious or spam, paywalled, license removed, or the link now points
  somewhere unrelated.

This is deliberate. A list that reshuffles weekly is not a list you can trust
without checking, which defeats the point of a list.

## Removing entries

Removal is a contribution. If a link is dead, a plugin broke on a new release,
or a project was abandoned without a note, open a change that removes or
relabels it and say what you observed — a URL, a date, a status code.
