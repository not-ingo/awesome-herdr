---
name: awesome-source-audit
description: Weekly audit of the awesome-herdr link list — verify every listed link still exists and still qualifies, capture updates to existing ones, search GitHub, GitLab, Codeberg, Reddit, social media, and articles for new candidates with a real track record, and refresh the dated Trending section with releases, company news, and notable use. Enforces a stability protocol so the curated list changes slowly while Trending stays current. Use for the scheduled weekly audit, or when asked to refresh, re-verify, or expand the awesome-herdr sources.
---

# Awesome source audit

This repository is a **list of links**, nothing else. It does not host
tutorials, recipes, or reference pages, and it must not grow any. `README.md`
is the product; `data/sources.json` is its state. If a task tempts you to write
a new page, the answer is a better one-line entry instead.

The list's value is that a reader can trust it without checking. Two failure
modes destroy that, and they pull in opposite directions:

- **Rot** — links that died, moved, got archived, or quietly turned into
  something else, still listed as if fine.
- **Churn** — entries appearing and disappearing week to week because a link
  had a bad day or something trended briefly.

This audit fixes the first without causing the second. **A week where nothing
changes is a successful audit.** Do not manufacture activity.

All paths below are relative to the project root
(`projects/awesome-herdr/`).

## State

| File | Role |
| --- | --- |
| `data/sources.json` | The ledger: `sources` (status, evidence, strikes, probation), `trending` (dated news items), and `audits` (this history). Authoritative. |
| `README.md` | The list itself, rendered *from* the ledger — `listed` sources plus unexpired `trending` items. |

If the two disagree, the ledger is right and the README is stale.

**The list runs at two speeds.** Everything under `sources` is deliberately
slow and governed by the probation and strike rules below. The `trending`
array is the opposite: news, dated and expiring. Never let one contaminate the
other — a trending item does not become a listed source just because it was
newsworthy, and a listed source is not removed because its news went stale.

## The bar

An entry qualifies only if **all** of these hold:

- **Track record**: ≥25 stars on GitHub, or **≥10 on GitLab or Codeberg** —
  those hosts have far smaller populations, so the same count represents more
  adoption. Comparable public traction also counts (a front-page Hacker News
  thread, a widely shared post, a known publication) — or it is an official
  Herdr resource.
- **Canonical home**: link where development happens, never a mirror. GitLab
  and Codeberg copies of GitHub projects are the same entry.
- **Alive**: pushed or published within the last 60 days, not archived.
- **Licensed**, for anything installable.
- **Herdr-specific**: a general terminal tool that merely mentions Herdr does
  not qualify.
- **You opened it.** A search-result snippet is not evidence.

Articles additionally must be substantive first-hand accounts — configs,
measurements, named limitations. Reject SEO filler, and reject listicles that
merely restate the README.

Official Herdr resources (herdr.dev and its documentation, the marketplace, the
main repository) are exempt from the probation rule below, not from
verification.

## Ledger shape

A `sources` entry:

```json
{
  "id": "github-com-owner-repo",
  "url": "https://github.com/owner/repo",
  "title": "repo",
  "section": "Navigation and layout",
  "status": "listed | probation | candidate | retired | rejected",
  "first_seen": "2026-08-12",
  "listed_since": "2026-08-12",
  "last_verified": "2026-08-12",
  "last_ok": "2026-08-12",
  "strikes": 0,
  "sightings": 1,
  "evidence": {
    "stars": 74, "license": "MIT", "last_push": "2026-08-11",
    "kind": "github | gitlab | codeberg | web | hn",
    "method": "GitHub API 2026-08-12; herdr-plugin.toml presence verified"
  },
  "exempt_from_probation": false,
  "last_change": null,
  "notes": "Why it qualifies, or why it was rejected."
}
```

A `trending` item:

```json
{
  "date": "2026-08-03", "kind": "release | breaking | company | engineering | growth | adoption | gap",
  "expires": "2026-10-01", "text": "One sentence.", "sources": ["https://…"]
}
```

`status` is the field that decides everything: only `listed` appears in the
README, `rejected` means evaluated and refused (keep the reason), `retired`
means it was listed once and failed out.

## Budget and rate limits

The GitHub API is the backbone of this audit and it will run out mid-run if you
are careless. Unauthenticated: **60 core requests per hour** and **10 search
requests per minute**. A full audit needs roughly one core call per listed
GitHub entry plus the sweep, which does not fit.

Before starting, check what you have, and prefer an authenticated token when
one exists (`gh auth status`; a token raises the core limit to 5000/hour):

```bash
curl -sS https://api.github.com/rate_limit | jq '.resources.core, .resources.search'
```

Then spend it deliberately:

- The **search** endpoint returns full repository objects — stars, license,
  `pushed_at`, `archived` — for up to 100 repositories in **one** call. Use the
  `topic:herdr-plugin stars:>=25` sweep to verify most listed GitHub entries at
  the same time, instead of calling `/repos/{owner}/{repo}` for each.
- Reserve per-repository calls for entries the sweep does not cover: anything
  not carrying the topic, and manifest-path checks for genuinely new plugins.
- Non-GitHub sources (GitLab, Codeberg, blogs, articles) have their own,
  looser limits — do those while GitHub is cooling down.

**A rate-limited response is not a dead link.** HTTP 403 or 429 with a
`rate limit` message, and any network error, means *unknown*: leave
`last_verified` alone, do **not** increment `strikes`, and record the entry as
unverified in the audit. Striking healthy entries because the API said "slow
down" is the fastest way to corrupt the list, and three such runs would retire
everything. If a run cannot verify everything, verify what you can, log which
entries were skipped, and finish the rest next week — a partial audit honestly
reported beats a complete one built on guesses.

Re-running on the same day is safe: skip anything whose `last_verified` is
already today.

## Procedure

Work the phases in order and record as you go.

### Phase 1 — Verify what is listed

For every entry with `status` of `listed` or `probation`:

1. Fetch the URL; follow redirects and note the final one. For GitHub entries,
   pull fresh metadata:

   ```bash
   curl -sS "https://api.github.com/repos/<owner>/<repo>" \
     -H "Accept: application/vnd.github+json"
   ```

   Read `stargazers_count`, `pushed_at`, `archived`, `license.spdx_id`, and any
   `full_name` change (a rename returns HTTP 301 with the new location).

2. Classify the outcome:
   - **OK** — reachable, unchanged in substance. Update `last_verified`,
     `last_ok`, and `evidence`; reset `strikes` to 0.
   - **MOVED** — permanent redirect or rename. Update `url` and `evidence`,
     record it in `last_change`. **Not** a strike.
   - **CHANGED** — alive but materially different: new major version, changed
     scope, new maintainer, license change, or it fell below the bar (archived,
     or no push in 60 days). Update `description`/`evidence` and `last_change`.
     Falling below the bar starts probation, not removal.
   - **FAIL** — 404/410, repository gone, or the content no longer matches the
     entry.
   - **UNKNOWN** — rate limited (403/429), timeout, DNS failure, or any 5xx.
     Not a strike, not a verification. Leave the entry untouched and list it as
     unverified in the audit record.
3. On FAIL, increment `strikes` and leave the entry listed unless the
   retirement rule fires.

Rewrite an entry's one-line description **only** when it would now be written
differently. Cosmetic rewording is churn in prose form.

### Phase 2 — Search for candidates

Cover every channel each week. A channel returning nothing is a normal result
worth recording.

1. **The marketplace, ranked** — the highest-yield channel, because Herdr's own
   index is unmoderated and sorted by nothing:

   ```bash
   curl -sS "https://api.github.com/search/repositories?q=topic:herdr-plugin+stars:%3E%3D25&sort=stars&order=desc&per_page=60" \
     -H "Accept: application/vnd.github+json"
   ```

   That query returns exactly the population that clears the star bar — review
   **every** result, not just the top few, and skip what the ledger already
   holds. Also check `topic:herdr`.

   Before listing a plugin, confirm it really is one, and find its install
   path: `herdr-plugin.toml` is often in a subdirectory rather than the root
   (`openclaw/crabbox/plugins/herdr`,
   `zenbu-labs/terminal-browser/herdr-plugin`). Check the root first, then the
   likely directories:

   ```bash
   curl -sS -o /dev/null -w "%{http_code}\n" \
     "https://api.github.com/repos/<owner>/<repo>/contents/herdr-plugin.toml"
   ```

   A repository can still qualify without a manifest if it is Herdr-specific
   in another way (a script, a companion app) — say so in the entry.

2. **GitLab and Codeberg** — smaller yield, but the bar is lower there (10
   stars) and nothing else covers them:

   ```bash
   curl -sS "https://gitlab.com/api/v4/projects?topic=herdr-plugin&order_by=star_count&sort=desc&per_page=50"
   curl -sS "https://gitlab.com/api/v4/projects?search=herdr&order_by=star_count&sort=desc&per_page=50"
   curl -sS "https://codeberg.org/api/v1/repos/search?q=herdr&limit=50&sort=stars&order=desc"
   ```

   Expect noise: GitLab's substring search matches things like `washerdryer`,
   and several hits are mirrors or forks of the GitHub repository. As of
   2026-08-12 neither host carried a qualifying project. Note that
   `herdr plugin install` accepts a GitHub `owner/repo` only, so anything
   hosted elsewhere installs by cloning plus `herdr plugin link <path>` —
   mention that in any entry from those hosts.
3. **Reddit** — r/commandline, r/terminal, r/tmux, r/rust, r/ClaudeAI, and any
   Herdr-specific subreddit. Queries: `herdr`, `herdr plugin`, `herdr
   workspace`.
4. **Social and forums** — Hacker News, X, Lobsters, Mastodon, Bluesky,
   YouTube. Weigh by discussion, not by post count.
5. **Articles** — blogs, newsletters, and known outlets. Open every one you
   would list and judge it against the article bar.
6. **Other lists** — including `yigitkonur/awesome-herdr`. Anything it carries
   that this list does not is a candidate, subject to the same bar; never copy
   an entry across without opening it.

Record every hit as a `candidate` in the ledger with its evidence, **even when
you will not list it**. That record is what stops the same rejected thing from
being re-evaluated from scratch every week.

### Phase 3 — Admit, with probation

**Promotion rule — the stability mechanism:**

1. First qualifying audit → `status: "candidate"`, `sightings: 1`. Not in the
   README.
2. Still qualifying next audit → `status: "probation"`, `sightings: 2`. Still
   not in the README.
3. Still qualifying the audit after → `status: "listed"`, `listed_since` set to
   today. Now it goes in the README.

Nothing reaches the list in under three weeks. That filters hype cycles,
weekend projects, and briefly popular links. Official resources are the only
exception.

A candidate that stops qualifying resets to `candidate` with the reason in
`notes` — never silently dropped.

### Phase 4 — Retire, with hysteresis

- **3 consecutive strikes** → `status: "retired"`, removed from the README,
  kept in the ledger with the reason.
- **Immediate retirement**, no strike count, for exactly four cases: archived
  or deprecated by its maintainer with a pointer elsewhere; became malicious,
  spam, or paywalled; license removed or made incompatible; the link now points
  at unrelated content.
- A retired entry that returns re-enters through Phase 3 from `candidate`.

Never retire an entry in the audit that first flagged it, outside those four
cases. If you are tempted to, you are being churned.

### Phase 5 — Keep it the *most* awesome

- Soft cap of **8 entries per section**. At the cap, adding means explicitly
  retiring the weakest incumbent — both decisions logged. A section that wants
  more probably wants to be split.
- Once per audit, take the **single weakest listed entry** and ask whether it
  would be admitted today. If clearly not, mark it `probation` with a reason.
  One per audit: a slow trim, not a purge.
- A section needs two entries to exist. Do not create one for a single link;
  put it in Extras until it has company.
- Prefer replacing over accumulating: two plugins doing the same job means one
  of them should go.

### Phase 6 — Refresh Trending

Different rules apply here, on purpose. Trending carries releases, company
news, notable use, and anything a returning reader would want to know since
last week.

**What qualifies:** a dated, verifiable event with a source link — a release, a
breaking change, a funding or company announcement, a named production user, a
published scale or cost account, a notable third-party integration, or a
milestone that is actually a number (stars, downloads, marketplace size).

**What does not:** anything undated, any claim you cannot link, a review that
is not news, or a growth figure you did not read from an API or a page this
run.

Work it in this order:

1. **Check the primary sources every time**:

   ```bash
   curl -sS "https://api.github.com/repos/herdrdev/herdr/releases?per_page=8" \
     -H "Accept: application/vnd.github+json"
   ```

   plus the official blog (`https://herdr.dev/blog/`). Read release bodies, not
   just tags: **breaking changes are the single most valuable trending item**
   and they live in the notes.
2. **Search for adoption and use**: named companies or teams running Herdr,
   conference talks, published workflows, incident or scale write-ups. As of
   2026-08-12 no company had publicly documented production use — that gap is a
   standing search target, and finding one is a headline item.
3. **Re-measure the numbers you publish**: repository stars, marketplace size
   (`total_count` from the `topic:herdr-plugin` search). Only publish figures
   from this run.
4. **Expire aggressively.** Drop any item past its `expires` date, or
   superseded by a newer one (v0.8.1 supersedes the v0.8.0 release item; a
   breaking-change notice can outlive its release, so give those a longer
   window). Set `expires` roughly 8 weeks out when adding.
5. **Cap at 8 items.** If more qualify, keep the ones a reader would act on:
   breaking changes first, then releases, then company news, then milestones.
6. Rewrite the README's Trending block from the array, newest first, and update
   its **Refreshed** date.

A short Trending section is a truthful signal that the month was quiet. Never
pad it with restated old news, and never move a stale item into the curated
sections to keep it alive.

### Phase 7 — Reconcile and report

1. Rewrite the affected README sections from the ledger. Format:
   `- [Name](url) — one sentence. ⭐ 398 · MIT`. Keep the table of contents in
   sync, and refresh the star counts and the "Signals collected" date in the
   header.

   **Do not hard-wrap the README.** One line per paragraph and one per list
   item, however long. The file is deliberately unwrapped; re-wrapping it to 80
   columns is a regression, not tidying.
2. Check every link you touched resolves, including the relative ones.
3. Append one entry to the ledger's `audits` array:

   ```json
   {
     "date": "2026-08-19",
     "verified": 39,
     "unverified": [],
     "searched": "marketplace (34 ≥25 stars), GitLab (0), Codeberg (0), Reddit (3 hits), HN (0), articles (1)",
     "changes": "none",
     "trending": "1 added (v0.8.1), 1 expired (#1 on GitHub Trending)",
     "probation": ["herdr-sidebar — strike 1, 404, retry next week"],
     "candidates": ["owner/herdr-thing — sighting 1 of 3, 61 stars"]
   }
   ```

   Also re-check the `rejected` entries held back only for a missing license —
   `pi-extensible-workflows`, `herdr-tab-smart-rename`, `herdr-board`. A
   license appearing promotes them straight into Phase 3.

   `"changes": "none"` is the product, not an admission of a wasted run.
4. **Commit the run locally.** The audit is not finished while it sits in the
   working tree — the ledger's value is its history, and an uncommitted run is
   a run that can be lost or silently overwritten by the next one.

   ```bash
   git add README.md data/sources.json
   git commit -m "Weekly audit YYYY-MM-DD: <one-line summary>"
   ```

   Rules for the commit:
   - **Only `README.md` and `data/sources.json`.** Never `git add -A`; never
     commit scratch files, and stop to ask if anything else is modified.
   - **Commit even when nothing changed.** A run that verifies 39 entries and
     changes no listing still updates `last_verified`, `last_ok`, and the
     `audits` array. `Weekly audit 2026-08-17: changes none, 39 verified, 12
     candidates at sighting 1` is exactly the commit this list wants in its
     history.
   - **Summarize honestly in the subject line** — the counts, and `changes
     none` when that is the result. The body is the place for admissions,
     retirements, and anything left unverified.
5. **Push the run to `main`.**

   ```bash
   git push origin main
   ```

   The audit's whole point is that a reader can trust the published list, so
   the run is not finished until what they read matches what you verified.
   Push on every run, including `changes: none` runs — the refreshed
   `last_verified` dates are the evidence that the list is being maintained.

   The boundary is narrow and stops here:
   - **This repository's `main`, and nothing else.** No pull requests, no
     force-push, no other branches, no other remotes.
   - **Nothing outward-facing.** Submitting to other awesome lists, posting
     about the list, or commenting on the sources you find still needs
     explicit human approval per the root `AGENTS.md`.
   - **Never push a dirty or partial run.** Commit first, confirm
     `git status` is clean, and if the audit was cut short — rate limits,
     entries left unverified — push what you honestly recorded, with the
     gaps written into the `audits` entry.
   - If the push is rejected, someone else moved `main`. Pull, rebase, and
     re-check the reconciliation before pushing again; never force.
6. Record the run against the Factory task run per the root `AGENTS.md`:
   `run_progress` while working, `run_decision` for every admission,
   retirement, and replacement (with rationale and rejected alternative), then
   `run_complete`.

## Rules that override the urge to be helpful

- **Never list something you did not open.** Not from a snippet, not from
  another list, not from memory. This is the one unforgivable error.
- **Never invent a URL or a star count.** Every number in the README must come
  from a response you actually received this run.
- **Do not add pages.** No new markdown files, no docs directory, no tutorials.
  Links only.
- **Publish the list, and nothing else.** Committing and pushing this
  repository's `main` is part of the run (Phase 7). Everything else is off
  limits without explicit human approval per the root `AGENTS.md`: no pull
  requests, no submissions to other awesome lists, no posts about the list, no
  comments or issues on the sources you find.
- **Do not touch anything outside this project directory**, and do not modify
  the user's Herdr configuration or running session.
- **Report honestly.** "Nothing changed, 39 verified, 1 candidate at sighting 2
  of 3, Trending unchanged" is a complete and successful audit.
