# Awesome Herdr [![Awesome](https://awesome.re/badge-flat.svg)](https://awesome.re)

> Curated links for [Herdr](https://herdr.dev) — the terminal workspace manager for AI coding agents.

Herdr's plugin marketplace is unmoderated: any repository tagged `herdr-plugin` appears in it, and there were **1,130** of them when this list was last audited. This list is the opposite — a short set of things with a track record.

**Inclusion bar:** a license, a push within the last 60 days, no archive notice, and a track record — **25+ stars on GitHub, or 10+ on GitLab or Codeberg**, where the same number means considerably more. Official Herdr resources are exempt from the star rule. Articles need to be substantive first-hand accounts, not SEO filler. Entries link to a project's canonical home, never to a mirror.

**Host coverage:** GitHub, GitLab, and Codeberg were all searched. Nothing on GitLab or Codeberg clears the bar today — the closest is a 1-star Codeberg todo tool of uncertain Herdr relevance; the genuine Herdr plugins found there all sit at 0 stars, tracked in [`data/sources.json`](data/sources.json) for re-checking. Worth knowing if you host there: `herdr plugin install` takes a GitHub `owner/repo` only, so a plugin hosted elsewhere is installed by cloning it and running `herdr plugin link <path>`.

**How the plugin entries were picked:** every repository in Herdr's [marketplace](https://herdr.dev/plugins/) with 25+ stars — 65 of the 1,130 — ranked and checked one by one. What is missing is missing on purpose: personal dotfiles repositories, tools where Herdr is one interchangeable backend among several rather than the point, and otherwise-qualifying projects that ship no license, including `pi-extensible-workflows` (⭐ 214), `herdr-board` (⭐ 123), and `herdr-tab-smart-rename` (⭐ 75). They are recorded in [`data/sources.json`](data/sources.json) and go back under review the moment a license appears. `herdrm` (⭐ 682), a native macOS agent console, adopted one on 2026-09-10, but it is the noncommercial PolyForm license, so it is tracked rather than headed here until noncommercial terms are confirmed to clear the bar.

**Signals collected:** 2026-09-12, via the GitHub, GitLab, and Codeberg APIs and by reading each linked page. Star counts move; treat them as an order of magnitude.

## Contents

- [Trending](#trending)
- [Official](#official)
- [Reviewing and reading code](#reviewing-and-reading-code)
- [Navigation and layout](#navigation-and-layout)
- [Browsers and viewers](#browsers-and-viewers)
- [Git and worktrees](#git-and-worktrees)
- [Remote access](#remote-access)
- [Phone and mobile](#phone-and-mobile)
- [Editor integration](#editor-integration)
- [Extras](#extras)
- [Articles](#articles)
- [Discussion](#discussion)
- [Related lists](#related-lists)
- [Contributing](#contributing)

## Trending

Everything else in this list is deliberately slow. This section is the opposite: news, releases, and notable use, refreshed weekly. Items are dated, carry a source, and are dropped once they are ~8 weeks old or superseded — so an empty-ish Trending section means a quiet month, not a neglected list.

**Refreshed:** 2026-09-12.

- **2026-09-08 · Company** — Herdr raised a **$6M seed** led by Bessemer Venture Partners, with Y Combinator, e2vc, and angels including Tobi Lütke (Shopify), Dane Knecht (Cloudflare), and Görkem Yurtseven (fal). The runtime stays open, the money goes to hiring, and applications go through an SSH endpoint rather than a web form. [Announcement](https://herdr.dev/blog/herdr-raised-a-seed/)
- **2026-09-07 · Breaking changes in v0.9.0** — The single-process `--no-session` mode is **removed**: every terminal UI launch now attaches to a background server, detaching leaves panes running, and `server stop` is what ends a session. Closing a primary workspace that has open worktree workspaces now requires explicit group intent (`workspace close --group`, or `close_group: true`), otherwise the whole group stays open. And new lifecycle event subscriptions start with **live events instead of replaying retained history** — API and plugin clients must subscribe before taking their initial snapshot or they will miss changes. [Release notes](https://github.com/herdrdev/herdr/releases/tag/v0.9.0)
- **2026-09-07 · Release v0.9.0** — Local and saved SSH machines now live in one window with a combined agent list, machine-scoped navigation, and automatic reconnects, managed through `herdr machine`; a disconnected machine no longer interrupts the others. Multiple clients can view different workspaces and tabs independently, the terminal UI moved into each client to cut redraw work in busy multi-client sessions, and Kitty graphics are on by default in compatible terminals. [Release notes](https://github.com/herdrdev/herdr/releases/tag/v0.9.0)
- **2026-09-07 · Company** — "Connecting the machines": the blog post behind the 0.9 multi-machine client, why it took longer than expected, and **Herdr Cloud** named as what comes next. [Post](https://herdr.dev/blog/connecting-the-machines/)
- **2026-08-19 · Release v0.8.2** — Windows support is now generally available on the stable channel (previously preview-only); the plugin marketplace now discovers manifests at repository roots and subdirectories and groups multiple plugins under one repository; Qwen Code state detection and native session restore. [Release notes](https://github.com/herdrdev/herdr/releases/tag/v0.8.2)
- **2026-08-03 · Engineering** — "Ten agents, three clients, 95% less CPU": the rendering and status-indicator work behind running a real fleet without melting a laptop. The closest thing to a published scale account. [Post](https://herdr.dev/blog/ten-agents-three-clients-95-percent-less-cpu/)
- **2026-06-30 · Growth** — **37,992** stars on 2026-09-12, up from 36,426 four days earlier and roughly 15k in early July, when it hit #1 on GitHub Trending; the 0.9 announcement put downloads above **700,000**. The plugin marketplace held **1,130** repositories on the same date, up from 1,033; 65 of them clear this list's 25-star bar, up from 60. [Repository](https://github.com/herdrdev/herdr) · [Marketplace](https://herdr.dev/plugins/) · [Downloads](https://herdr.dev/blog/connecting-the-machines/)
- **Standing gap** — No company has been found publicly documenting Herdr in production use. Still a search target every week; a first one would be the headline item here.

## Official

- [Blog](https://herdr.dev/blog/) — Release notes, engineering write-ups, and company news. The primary source for everything in Trending above.
- [herdrdev/herdr](https://github.com/herdrdev/herdr) — The tool itself: a single Rust binary giving workspaces, tiled panes, and agent state detection inside your existing terminal. ⭐ 38k · Apache-2.0
- [Documentation](https://herdr.dev/docs/) — Install, concepts, session state, configuration, agents, plugins, and the socket API.
- [Socket API](https://herdr.dev/docs/socket-api/) — The local Unix socket that lets scripts and agents create panes, read other panes, and subscribe to state changes. The reason Herdr is programmable rather than just usable.
- [Plugin marketplace](https://herdr.dev/plugins/) — Auto-generated index of every repository tagged `herdr-plugin`. No review queue, so bring judgement; this list is one filter over it.
- [Writing plugins](https://herdr.dev/docs/plugins/) — A plugin is a directory with a `herdr-plugin.toml` manifest and commands Herdr can launch, in any language your machine can run.

## Reviewing and reading code

- [herdr-reviewr](https://github.com/persiyanov/herdr-reviewr) — Code-review and file-viewer sidebar: comment on an agent's diff and send the comments back to it. ⭐ 686 · MIT
- [herdr-file-viewer](https://github.com/smarzban/herdr-file-viewer) — Git-aware read-only file viewer: tree plus content pane with diffs, rendered markdown, and syntax highlighting. Safe to point at untrusted repositories. ⭐ 569 · MIT
- [herdr-sidebar](https://github.com/alexarthurs/herdr-sidebar) — VS Code-style sidebar combining a file explorer and git source control in one pane. ⭐ 329 · MIT
- [herdr-hunk-diff](https://github.com/jhochenbaum/herdr-hunk-diff) — Review an agent's diff hunk by hunk and send inline comments back to the agent that wrote it. Finer-grained than herdr-reviewr's sidebar; needs Herdr 0.8.0+ and Node 22.12+, macOS and Linux only. ⭐ 118 · MIT

## Navigation and layout

- [herdr-navigator](https://github.com/thanhdat77/herdr-navigator) — Jump to any workspace, agent, project, session, remote, or directory from a single prompt. ⭐ 144 · MIT
- [herdr-spreader](https://github.com/yuk1ty/herdr-spreader) — Spin up a whole workspace layout — tabs, panes, commands — from one declarative file. ⭐ 110 · MIT
- [herdr-sessionizer](https://github.com/andrewchng/herdr-sessionizer) — Fuzzy-open projects and worktrees, then bootstrap workspaces from declarative TOML. For the tmux-sessionizer crowd. ⭐ 46 · MIT
- [herdr-plugin-workspace-manager](https://github.com/razajamil/herdr-plugin-workspace-manager) — Declarative tab and pane layouts with per-workspace defaults, applied automatically. ⭐ 40 · MIT
- [herdr-plugin-sesh](https://github.com/fullerzz/herdr-plugin-sesh) — Sesh-style workspace picker TUI, integrated with zoxide so frequently used directories surface first. ⭐ 39 · MIT

## Browsers and viewers

- [terminal-browser](https://github.com/zenbu-labs/terminal-browser) — A real browser rendered inside your terminal, with a Herdr plugin in `zenbu-labs/terminal-browser/herdr-plugin`. ⭐ 2.9k · MIT
- [herdr-browser](https://github.com/ogulcancelik/herdr-browser) — Render a Chromium view inside a pane and drive it over CDP, so an agent can look at what it built. ⭐ 348 · MIT
- [ghzinga](https://github.com/osolmaz/ghzinga) — Clickable Rust TUI for a single GitHub issue or PR, for triaging without a browser. Plugin lives in `osolmaz/ghzinga/plugins/herdr`. ⭐ 85 · MIT
- [termscope](https://github.com/iurysza/termscope) — Open files and links already visible on your terminal screen in a split. ⭐ 53 · MIT

## Git and worktrees

- [herdr-worktrunk](https://github.com/devashish2203/herdr-worktrunk) — Switch, create, and remove git worktrees through worktrunk without leaving Herdr. ⭐ 143 · MIT
- [herdr-plugin-jj-workspace](https://github.com/NathanFlurry/herdr-plugin-jj-workspace) — Create and remove Jujutsu workspaces as Herdr workspaces, for jj users running parallel agents. ⭐ 47 · MIT

## Remote access

- [herdr-remote](https://github.com/dcolinmorgan/herdr-remote) — Monitor and drive agents from the macOS menu bar, a phone, or Telegram, with zero config locally. ⭐ 354
- [herdr-mirror](https://github.com/nikok6/herdr-mirror) — Mirror remote Herdr servers into your local window so local and remote sessions live in one place. Note that Herdr 0.9 now does multi-machine natively via `herdr machine`. ⭐ 228 · MIT
- [herdr-web](https://github.com/kcosr/herdr-web) — Browser client for a running session, over a Rust HTTP/WebSocket bridge that works around Herdr allowing only one terminal attach owner. A companion app, not a plugin; needs Herdr 0.8.0+. ⭐ 121 · MIT

## Phone and mobile

- [collie](https://github.com/AltanS/collie) — PWA for managing Herdr from your phone over a tailnet: see which agents are blocked, read panes, reply, and get push notifications. ⭐ 942 · MIT
- [herdr-mobile-relay](https://github.com/0cv/herdr-mobile-relay) — Mobile web app for approving and monitoring agents remotely — the approvals half of the problem. ⭐ 205
- [whip](https://github.com/kosumic/whip) — Android app for supervising Herdr over SSH or Tailscale, falling back to a plain SSH shell when Herdr is not there. Note the AGPL-3.0 copyleft. ⭐ 66 · AGPL-3.0
- [herdr-mobile](https://github.com/benkraus/herdr-mobile) — Native iOS and Android client, talking to the separately deployed `benkraus/herdr-plugin-mobile-relay`. ⭐ 54 · MIT
- [agentslate](https://github.com/DanielOu1208/agentslate) — iPhone remote keypad for supervising agents over Tailscale, with an offline demo mode. Mac side installs via Homebrew; live control needs Herdr 0.8.0+. ⭐ 30 · MIT

## Editor integration

- [vim-herdr-navigation](https://github.com/paulbkim-dev/vim-herdr-navigation) — Seamless `Ctrl+h/j/k/l` across Herdr panes and Vim/Neovim splits, in the spirit of vim-tmux-navigator. ⭐ 105 · MIT
- [herdr-splits.nvim](https://github.com/lmilojevicc/herdr-splits.nvim) — Smart split navigation and resizing between Herdr and Neovim. ⭐ 60 · MIT

## Extras

- [crabbox](https://github.com/openclaw/crabbox) — Warm a box, sync the diff, run the suite: ephemeral environments so agents execute somewhere other than your machine. Install the plugin subdirectory, `openclaw/crabbox/plugins/herdr`. ⭐ 1.4k · MIT
- [herdr-plus](https://github.com/cloudmanic/herdr-plus) — A grab-bag first-class plugin adding Projects and Quick Actions. ⭐ 305 · MIT
- [memex](https://github.com/nicosuave/memex) — Search transcripts across Claude Code, Codex, Pi, OpenCode, Copilot, and Cursor, and resume a session from a hit. ⭐ 209 · MIT
- [herdr-automatic-rename](https://github.com/qu8n/herdr-automatic-rename) — Renames tabs from each pane's foreground process, tmux `automatic-rename` style, and adds 1-9 jump keys. Needs Herdr 0.7.1+. ⭐ 81 · MIT
- [herdr-auto-title](https://github.com/sh1ma/herdr-auto-title) — Generates tab titles from Claude Code and Codex conversations — the content, where herdr-automatic-rename uses the process. A script rather than a manifest plugin. ⭐ 52 · MIT
- [pi-herdr-squad](https://github.com/jillesme/pi-herdr-squad) — Runs read-only investigation squads across your panes; `pi install npm:pi-herdr-squad`, and needs a Pi session inside a Herdr-managed pane. ⭐ 26 · MIT

## Articles

- [A deep dive into Herdr](https://flaviocopes.com/herdr/) — Flavio Copes on the repositories he actually runs it against, his agents/dev/checks/deploy tab layout, a deliberately minimal config, and limits he hit in use — including parallel pushes jamming a Cloudflare Pages build queue. 2026-08-10.
- [I Gave Up tmux and Zellij for Herdr](https://www.joshfinnie.com/blog/switching-to-herdr/) — Josh Finnie's hands-on switch, with his actual `config.toml`, plugin picks, and an honest list of tradeoffs. 2026-08-06.
- [herdr and cmux: two shapes of the same agent multiplexer](https://blog.debedb.com/2026/07/26/herdr-and-cmux-two-shapes-of-the-same-agent-multiplexer/) — A structural comparison of the two designs with named Herdr limitations. The author says outright he has not run Herdr in anger, so it is stronger on cmux; read it for the framing. 2026-07-26.
- [Herdr: a tmux for agents](https://en.thedavestack.com/herdr-a-tmux-for-agents/) — Architectural take on the control surface and plugin model from someone building orchestration on top of it. Start here if you want to script Herdr.
- [Herdr Review: The Agent Multiplexer Your Terminal Needed](https://andrew.ooo/posts/herdr-agent-multiplexer-terminal-review/) — A day of real use with Claude Code and Codex, with a comparison table against tmux and Zellij, and named limitations. Written against v0.4.0, so check version-specific claims. 2026-07-08.

## Discussion

- [Herdr: One terminal to rule them all](https://news.ycombinator.com/item?id=48756578) — The largest Herdr thread on Hacker News. 404 points, 178 comments. 2026-07-02.
- [Herdr is joining Y Combinator. The runtime stays open](https://news.ycombinator.com/item?id=49201003) — The funding thread, and the recurring question of what stays open when a terminal tool takes money. 281 points, 189 comments. 2026-08-06.
- [Herdr: Agent multiplexer that lives in your terminal](https://news.ycombinator.com/item?id=48714802) — The thread that introduced most people to it, with a useful argument about whether running many parallel agents is actually a good idea. 166 points, 110 comments. 2026-06-29.

## Related lists

- [yigitkonur/awesome-herdr](https://github.com/yigitkonur/awesome-herdr) — The established curated index of the Herdr ecosystem: tools, workflows, configs, clients, skills, and integrations. Broader than this list; check it before concluding something does not exist. ⭐ 207 · MIT

## Contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md). Short version: open the thing, run it on the current Herdr release, describe it in one sentence, and never list what you have not used.

Entries are tracked in [`data/sources.json`](data/sources.json) and re-verified weekly. Additions serve a three-week probation before they appear here, and removals need three consecutive failures — this list is meant to be boring and trustworthy rather than fresh.

## License

[CC0 1.0](LICENSE) — to the extent possible under law, the contributors have waived all copyright and related rights to the curation in this repository. Linked works keep their own licenses.
