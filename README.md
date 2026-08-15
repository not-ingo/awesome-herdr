# Awesome Herdr [![Awesome](https://awesome.re/badge-flat.svg)](https://awesome.re)

> Curated links for [Herdr](https://herdr.dev) — the terminal workspace manager for AI coding agents.

Herdr's plugin marketplace is unmoderated: any repository tagged `herdr-plugin` appears in it, and there were **605** of them when this list was last audited. This list is the opposite — a short set of things with a track record.

**Inclusion bar:** a license, a push within the last 60 days, no archive notice, and a track record — **25+ stars on GitHub, or 10+ on GitLab or Codeberg**, where the same number means considerably more. Official Herdr resources are exempt from the star rule. Articles need to be substantive first-hand accounts, not SEO filler. Entries link to a project's canonical home, never to a mirror.

**Host coverage:** GitHub, GitLab, and Codeberg were all searched. Nothing on GitLab or Codeberg clears the bar today — the closest are two 0-star Codeberg plugins, tracked in [`data/sources.json`](data/sources.json) for re-checking. Worth knowing if you host there: `herdr plugin install` takes a GitHub `owner/repo` only, so a plugin hosted elsewhere is installed by cloning it and running `herdr plugin link <path>`.

**How the plugin entries were picked:** every repository in Herdr's [marketplace](https://herdr.dev/plugins/) with 25+ stars — 34 of the 605 — ranked and checked one by one. What is missing is missing on purpose: personal dotfiles repositories, and three otherwise-qualifying projects that ship no license (`pi-extensible-workflows` ⭐ 175, `herdr-tab-smart-rename` ⭐ 32, `herdr-board` ⭐ 26). They are recorded in [`data/sources.json`](data/sources.json) and will be listed the moment a license appears.

**Signals collected:** 2026-08-12, via the GitHub, GitLab, and Codeberg APIs and by reading each linked page. Star counts move; treat them as an order of magnitude.

## Contents

- [Trending](#trending)
- [Official](#official)
- [Reviewing and reading code](#reviewing-and-reading-code)
- [Navigation and layout](#navigation-and-layout)
- [Sandboxes and isolation](#sandboxes-and-isolation)
- [Browsers and viewers](#browsers-and-viewers)
- [Git and worktrees](#git-and-worktrees)
- [Remote and mobile](#remote-and-mobile)
- [Editor integration](#editor-integration)
- [Extras](#extras)
- [Articles](#articles)
- [Discussion](#discussion)
- [Related lists](#related-lists)
- [Contributing](#contributing)

## Trending

Everything else in this list is deliberately slow. This section is the opposite: news, releases, and notable use, refreshed weekly. Items are dated, carry a source, and are dropped once they are ~8 weeks old or superseded — so an empty-ish Trending section means a quiet month, not a neglected list.

**Refreshed:** 2026-08-12.

- **2026-08-06 · Company** — Herdr joined **Y Combinator (Fall 2026)**, with the runtime staying Apache-2.0 and open. Still a one-person team; the YC page cites 25k stars and 340k downloads within four months of launch. [Announcement](https://herdr.dev/blog/) · [YC profile](https://www.ycombinator.com/companies/herdr)
- **2026-08-03 · Release v0.8.0** — Adds `herdr --skill` (prints the agent instruction file bundled with the binary), `ui.tab_bar_position = "bottom"`, live filtering in the keybind help, and session reporting plus native resume for Grok CLI and Antigravity CLI. [Release notes](https://github.com/herdrdev/herdr/releases/tag/v0.8.0)
- **2026-08-03 · Engineering** — "Ten agents, three clients, 95% less CPU": the rendering and status-indicator work behind running a real fleet without melting a laptop. The closest thing to a published scale account. [Post](https://herdr.dev/blog/)
- **2026-07-21 · Breaking change in v0.7.5** — Installed and linked plugins, including their enabled state, are now **global to the user** rather than isolated per Herdr session. Plugins installed only in a named session on 0.7.3 must be installed or linked again. [Release notes](https://github.com/herdrdev/herdr/releases/tag/v0.7.5)
- **2026-06-30 · Growth** — Hit #1 on GitHub Trending; roughly 15k stars in early July and **28.2k** by 2026-08-12. The plugin marketplace held **605** repositories on the same date, up from 582 nine days earlier. [Repository](https://github.com/herdrdev/herdr) · [Marketplace](https://herdr.dev/plugins/)

## Official

- [Blog](https://herdr.dev/blog/) — Release notes, engineering write-ups, and company news. The primary source for everything in Trending above.
- [herdrdev/herdr](https://github.com/herdrdev/herdr) — The tool itself: a single Rust binary giving workspaces, tiled panes, and agent state detection inside your existing terminal. ⭐ 28.2k · Apache-2.0
- [Documentation](https://herdr.dev/docs/) — Install, concepts, session state, configuration, agents, plugins, and the socket API.
- [Socket API](https://herdr.dev/docs/socket-api/) — The local Unix socket that lets scripts and agents create panes, read other panes, and subscribe to state changes. The reason Herdr is programmable rather than just usable.
- [Plugin marketplace](https://herdr.dev/plugins/) — Auto-generated index of every repository tagged `herdr-plugin`. No review queue, so bring judgement; this list is one filter over it.
- [Writing plugins](https://herdr.dev/docs/plugins/) — A plugin is a directory with a `herdr-plugin.toml` manifest and commands Herdr can launch, in any language your machine can run.

## Reviewing and reading code

- [herdr-reviewr](https://github.com/persiyanov/herdr-reviewr) — Code-review and file-viewer sidebar: comment on an agent's diff and send the comments back to it. ⭐ 398 · MIT
- [herdr-file-viewer](https://github.com/smarzban/herdr-file-viewer) — Git-aware read-only file viewer: tree plus content pane with diffs, rendered markdown, and syntax highlighting. Safe to point at untrusted repositories. ⭐ 391 · MIT
- [herdr-sidebar](https://github.com/alexarthurs/herdr-sidebar) — VS Code-style sidebar combining a file explorer and git source control in one pane. ⭐ 49 · MIT

## Navigation and layout

- [herdr-navigator](https://github.com/thanhdat77/herdr-navigator) — Jump to any workspace, agent, project, session, remote, or directory from a single prompt. ⭐ 74 · MIT
- [herdr-spreader](https://github.com/yuk1ty/herdr-spreader) — Spin up a whole workspace layout — tabs, panes, commands — from one declarative file. ⭐ 68 · MIT
- [herdr-sessionizer](https://github.com/andrewchng/herdr-sessionizer) — Fuzzy-open projects and worktrees, then bootstrap workspaces from declarative TOML. For the tmux-sessionizer crowd. ⭐ 30 · MIT
- [herdr-command-palette](https://github.com/JanTvrdik/herdr-command-palette) — fzf command palette: fuzzy-pick and run any plugin action. ⭐ 26 · MIT
- [herdr-plugin-workspace-manager](https://github.com/razajamil/herdr-plugin-workspace-manager) — Declarative tab and pane layouts with per-workspace defaults, applied automatically. ⭐ 28 · MIT
- [herdr-plugin-sesh](https://github.com/fullerzz/herdr-plugin-sesh) — Sesh-style workspace picker TUI, integrated with zoxide so frequently used directories surface first. ⭐ 25 · MIT

## Sandboxes and isolation

- [crabbox](https://github.com/openclaw/crabbox) — Warm a box, sync the diff, run the suite: ephemeral environments so agents execute somewhere other than your machine. The most-starred thing in the marketplace; install the plugin subdirectory, `openclaw/crabbox/plugins/herdr`. ⭐ 1.3k · MIT
- [agentbox-herdr-plugin](https://github.com/madarco/agentbox-herdr-plugin) — Herdr front end for [agentbox](https://github.com/madarco/agentbox) (⭐ 346), which runs multiple agents in parallel sandboxed VMs locally or in the cloud. ⭐ 26 · MIT

## Browsers and viewers

- [terminal-browser](https://github.com/zenbu-labs/terminal-browser) — A real browser rendered inside your terminal, with a Herdr plugin in `zenbu-labs/terminal-browser/herdr-plugin`. ⭐ 954 · MIT
- [herdr-browser](https://github.com/ogulcancelik/herdr-browser) — Render a Chromium view inside a pane and drive it over CDP, so an agent can look at what it built. ⭐ 297 · MIT
- [ghzinga](https://github.com/osolmaz/ghzinga) — Clickable Rust TUI for a single GitHub issue or PR, for triaging without a browser. Plugin lives in `osolmaz/ghzinga/plugins/herdr`. ⭐ 72 · MIT
- [termscope](https://github.com/iurysza/termscope) — Open files and links already visible on your terminal screen in a split. ⭐ 43 · MIT

## Git and worktrees

- [herdr-worktrunk](https://github.com/devashish2203/herdr-worktrunk) — Switch, create, and remove git worktrees through worktrunk without leaving Herdr. ⭐ 85 · MIT
- [herdr-plugin-jj-workspace](https://github.com/NathanFlurry/herdr-plugin-jj-workspace) — Create and remove Jujutsu workspaces as Herdr workspaces, for jj users running parallel agents. ⭐ 41 · MIT

## Remote and mobile

- [collie](https://github.com/AltanS/collie) — PWA for managing Herdr from your phone over a tailnet: see which agents are blocked, read panes, reply, and get push notifications. ⭐ 368 · MIT
- [herdr-remote](https://github.com/dcolinmorgan/herdr-remote) — Monitor and drive agents from the macOS menu bar, a phone, or Telegram, with zero config locally. ⭐ 227
- [herdr-mirror](https://github.com/nikok6/herdr-mirror) — Mirror remote Herdr servers into your local window so local and remote sessions live in one place. ⭐ 130 · MIT
- [herdr-mobile-relay](https://github.com/0cv/herdr-mobile-relay) — Mobile web app for approving and monitoring agents remotely — the approvals half of the problem. ⭐ 38

## Editor integration

- [vim-herdr-navigation](https://github.com/paulbkim-dev/vim-herdr-navigation) — Seamless `Ctrl+h/j/k/l` across Herdr panes and Vim/Neovim splits, in the spirit of vim-tmux-navigator. ⭐ 80 · MIT
- [herdr-splits.nvim](https://github.com/lmilojevicc/herdr-splits.nvim) — Smart split navigation and resizing between Herdr and Neovim. ⭐ 44 · MIT

## Extras

- [herdr-plus](https://github.com/cloudmanic/herdr-plus) — A grab-bag first-class plugin adding Projects and Quick Actions. ⭐ 228 · MIT
- [memex](https://github.com/nicosuave/memex) — Search transcripts across Claude Code, Codex, Pi, OpenCode, Copilot, and Cursor, and resume a session from a hit. ⭐ 107 · MIT
- [llmtrim-herdr](https://github.com/fkiene/llmtrim-herdr) — Compresses every agent pane's requests to cut token spend; the author reports around −31%. ⭐ 31 · MPL-2.0
- [herdr-window-title-sync](https://github.com/rjyo/herdr-window-title-sync) — Syncs terminal window titles from workspaces, tabs, and agent sessions. ⭐ 31 · MIT
- [herdr-auto-title](https://github.com/sh1ma/herdr-auto-title) — Generates tab titles from Claude Code and Codex conversations. A script rather than a manifest plugin. ⭐ 30 · MIT

## Articles

- [I Gave Up tmux and Zellij for Herdr](https://www.joshfinnie.com/blog/switching-to-herdr/) — Josh Finnie's hands-on switch, with his actual `config.toml`, plugin picks, and an honest list of tradeoffs. 2026-08-06.
- [Herdr: a tmux for agents](https://en.thedavestack.com/herdr-a-tmux-for-agents/) — Architectural take on the control surface and plugin model from someone building orchestration on top of it. Start here if you want to script Herdr.
- [Herdr Review: The Agent Multiplexer Your Terminal Needed](https://andrew.ooo/posts/herdr-agent-multiplexer-terminal-review/) — A day of real use with Claude Code and Codex, with a comparison table against tmux and Zellij, and named limitations. Written against v0.4.0, so check version-specific claims. 2026-07-08.

## Discussion

- [Herdr: Agent multiplexer that lives in your terminal](https://news.ycombinator.com/item?id=48714802) — The Hacker News thread that introduced most people to it. 166 points, 110 comments, and a useful argument about whether running many parallel agents is actually a good idea.

## Related lists

- [yigitkonur/awesome-herdr](https://github.com/yigitkonur/awesome-herdr) — The established curated index of the Herdr ecosystem: tools, workflows, configs, clients, skills, and integrations. Broader than this list; check it before concluding something does not exist. ⭐ 123 · MIT

## Contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md). Short version: open the thing, run it on the current Herdr release, describe it in one sentence, and never list what you have not used.

Entries are tracked in [`data/sources.json`](data/sources.json) and re-verified weekly. Additions serve a three-week probation before they appear here, and removals need three consecutive failures — this list is meant to be boring and trustworthy rather than fresh.

## License

[CC0 1.0](LICENSE) — to the extent possible under law, the contributors have waived all copyright and related rights to the curation in this repository. Linked works keep their own licenses.
