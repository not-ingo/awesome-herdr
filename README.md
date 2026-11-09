# Awesome Herdr [![Awesome](https://awesome.re/badge-flat.svg)](https://awesome.re)

> Curated links for [Herdr](https://herdr.dev) — the terminal workspace manager for AI coding agents.

Herdr's plugin marketplace is unmoderated: any repository tagged `herdr-plugin` appears in it, and there were **2,073** of them when this list was last audited. This list is the opposite — a short set of things with a track record.

**Inclusion bar:** a license, a push within the last 60 days, no archive notice, and a track record — **25+ stars on GitHub, or 10+ on GitLab or Codeberg**, where the same number means considerably more. Official Herdr resources are exempt from the star rule. Articles need to be substantive first-hand accounts, not SEO filler. Entries link to a project's canonical home, never to a mirror.

**Host coverage:** GitHub, GitLab, and Codeberg were all searched. Nothing on GitLab or Codeberg clears the bar today — the closest is a 1-star Codeberg todo tool of uncertain Herdr relevance; the genuine Herdr plugins found there all sit at 0 stars, tracked in [`data/sources.json`](data/sources.json) for re-checking. Worth knowing if you host there: `herdr plugin install` takes a GitHub `owner/repo` only, so a plugin hosted elsewhere is installed by cloning it and running `herdr plugin link <path>`.

**How the plugin entries were picked:** every repository in Herdr's [marketplace](https://herdr.dev/tui/plugins/) with 25+ stars — 98 of the 2,073 — ranked and checked one by one. What is missing is missing on purpose: personal dotfiles repositories, tools where Herdr is one interchangeable backend among several rather than the point, and otherwise-qualifying projects that ship no license, including `pi-extensible-workflows` (⭐ 248), `herdr-board` (⭐ 183), and `herdr-tab-smart-rename` (⭐ 78). They are recorded in [`data/sources.json`](data/sources.json) and go back under review the moment a license appears. `herdrm` (⭐ 793), a native macOS agent console, adopted one on 2026-09-10, but it is the noncommercial PolyForm license, so it is tracked rather than headed here until noncommercial terms are confirmed to clear the bar.

**Signals collected:** 2026-11-09, via the GitHub, GitLab, and Codeberg APIs and by reading each linked page. Star counts move; treat them as an order of magnitude.

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
- [Orchestration and agent status](#orchestration-and-agent-status)
- [Extras](#extras)
- [Articles](#articles)
- [Discussion](#discussion)
- [Related lists](#related-lists)
- [Contributing](#contributing)

## Trending

Everything else in this list is deliberately slow. This section is the opposite: news, releases, and notable use, refreshed weekly. Items are dated, carry a source, and are dropped once they are ~8 weeks old or superseded — so an empty-ish Trending section means a quiet month, not a neglected list.

**Refreshed:** 2026-11-09.

- **2026-10-30 · Release** — Herdr released a **native desktop app** ([herdrdev/herdr-app](https://github.com/herdrdev/herdr-app), Apache-2.0): macOS, Linux, and Windows, bundling herdr-core for standalone use while still supporting an existing Herdr 1 daemon. [HN thread (367 upvotes)](https://news.ycombinator.com/item?id=50298436) · [Install](https://github.com/herdrdev/herdr-app#install)
- **2026-11-09 · Growth** — **49,549** stars on 2026-11-09, up from 45,899 on 2026-10-26 and roughly 15k in early July, when it hit #1 on GitHub Trending. The plugin marketplace holds **2,073** repositories on the same date, up from 1,924; 98 of them clear this list's 25-star bar, up from 94. [Repository](https://github.com/herdrdev/herdr) · [Marketplace](https://herdr.dev/tui/plugins/) · [Downloads](https://herdr.dev/blog/connecting-the-machines/)
- **2026-10-13 · Release v0.9.4 / v0.9.5** — v0.9.4 adds `herdr plugin update` (one command to update all GitHub-installed plugins without config reload, while running panes keep working on their old files), persistent Windows sessions across machine restart, and improved idle detection for Antigravity and Grok. v0.9.5 (2026-10-14 hotfix) restores prefix shortcuts for Chinese, Japanese, and Korean input methods on macOS (Tern and `text:` keybinds), fixes Codex session tracking and Claude Code blocked-question display. [v0.9.4](https://github.com/herdrdev/herdr/releases/tag/v0.9.4) · [v0.9.5](https://github.com/herdrdev/herdr/releases/tag/v0.9.5)
- **2026-09-29 · Breaking changes in v0.9.2** — The Herdr-specific pane graphics API is **removed**: `pane.graphics.info`, `set`, `clear`, and `stream` now return `unknown_method`. Plugins that display images must switch to standard **Kitty graphics protocol**, which Herdr now renders natively. [Release notes](https://github.com/herdrdev/herdr/releases/tag/v0.9.2)
- **2026-09-24 · Adoption** — **GENDA Inc.**, a Japanese entertainment company, published a retrospective by one of its development engineers: a custom plugin that placed Claude Code and Codex in role-based Herdr panes, why they stopped using it as models improved, and that they still work in Herdr panes. The first named company found documenting its engineers' use of Herdr. It is a retrospective, with no scale or cost figures. [Post (Japanese)](https://zenn.dev/genda_jp/articles/baton-retrospective-model-evolution)
- **2026-09-07 · Breaking changes in v0.9.0** — The single-process `--no-session` mode is **removed**: every terminal UI launch now attaches to a background server, detaching leaves panes running, and `server stop` is what ends a session. Closing a primary workspace that has open worktree workspaces now requires explicit group intent (`workspace close --group`, or `close_group: true`), otherwise the whole group stays open. And new lifecycle event subscriptions start with **live events instead of replaying retained history** — API and plugin clients must subscribe before taking their initial snapshot or they will miss changes. [Release notes](https://github.com/herdrdev/herdr/releases/tag/v0.9.0)

## Official

- [Blog](https://herdr.dev/blog/) — Release notes, engineering write-ups, and company news. The primary source for everything in Trending above.
- [herdrdev/herdr](https://github.com/herdrdev/herdr) — The tool itself: a single Rust binary giving workspaces, tiled panes, and agent state detection inside your existing terminal. ⭐ 49.5k · Apache-2.0
- [Herdr desktop app](https://github.com/herdrdev/herdr-app) — Native desktop app for macOS, Linux, and Windows: workspaces, terminals, and agent monitoring in a notarized Rust/GPUI app. Bundles herdr-core; a separate Herdr 1 install is optional. ⭐ 2.5k · Apache-2.0
- [herdr-core](https://github.com/herdrdev/herdr-core) — The headless terminal runtime: an SSH endpoint and no native UI; what the desktop app bundles and what server-side installs run. ⭐ 529 · Apache-2.0
- [Documentation](https://herdr.dev/tui/docs/) — Install, concepts, session state, configuration, agents, plugins, and the socket API.
- [Socket API](https://herdr.dev/tui/docs/socket-api/) — The local Unix socket that lets scripts and agents create panes, read other panes, and subscribe to state changes. The reason Herdr is programmable rather than just usable.
- [Plugin marketplace](https://herdr.dev/tui/plugins/) — Auto-generated index of every repository tagged `herdr-plugin`. No review queue, so bring judgement; this list is one filter over it.
- [Writing plugins](https://herdr.dev/tui/docs/plugins/) — A plugin is a directory with a `herdr-plugin.toml` manifest and commands Herdr can launch, in any language your machine can run.

## Reviewing and reading code

- [herdr-reviewr](https://github.com/persiyanov/herdr-reviewr) — Code-review and file-viewer sidebar: comment on an agent's diff and send the comments back to it. ⭐ 977 · MIT
- [herdr-file-viewer](https://github.com/smarzban/herdr-file-viewer) — Git-aware read-only file viewer: tree plus content pane with diffs, rendered markdown, and syntax highlighting. Safe to point at untrusted repositories. ⭐ 702 · MIT
- [herdr-annotate](https://github.com/plannotator/herdr-annotate) — Comment on any terminal text, review whole Markdown documents and agent replies, and send the feedback straight back to the agent. Prebuilt binary, Herdr 0.8.0+. ⭐ 737 · MIT
- [herdr-sidebar](https://github.com/alexarthurs/herdr-sidebar) — VS Code-style sidebar combining a file explorer and git source control in one pane. ⭐ 539 · MIT
- [herdr-hunk-diff](https://github.com/jhochenbaum/herdr-hunk-diff) — Review an agent's diff hunk by hunk and send inline comments back to the agent that wrote it. Finer-grained than herdr-reviewr's sidebar; needs Herdr 0.8.0+ and Node 22.12+, macOS and Linux only. ⭐ 150 · MIT
- [herdr-file-annotator](https://github.com/JonasBaeumer/herdr-file-annotator) — Opens a review pane in your workspace: select lines, tag a note as fix, verify, question, or nit, and it goes back to the agent instead of being dictated into the prompt. ⭐ 65 · MIT

## Navigation and layout

- [herdr-navigator](https://github.com/thanhdat77/herdr-navigator) — Jump to any workspace, agent, project, session, remote, or directory from a single prompt. ⭐ 188 · MIT
- [herdr-bar](https://github.com/jeffarese/herdr-bar) — Cmd+K quick switcher for any tab, pane, agent, repo, or branch, plus agent icons and automatic tab titles from Claude and Codex tasks. ⭐ 213 · MIT
- [herdr-plugin-manager](https://github.com/speardragon/herdr-plugin-manager) — Plugin manager inside Herdr: see installed plugins, check for updates, install or remove, with per-plugin status badges. ⭐ 86 · MIT
- [omarchy-herdr](https://github.com/jankeesvw/omarchy-herdr) — Omarchy bar widget that shows the count and contents of running Herdr servers; one click opens the session in Herdr. Built for Omarchy (DHH's Arch-based Linux distribution) but works in any bar that supports it. ⭐ 58 · MIT
- [herdr-sessionizer](https://github.com/andrewchng/herdr-sessionizer) — Fuzzy-open projects and worktrees, then bootstrap workspaces from declarative TOML. For the tmux-sessionizer crowd. ⭐ 53 · MIT
- [herdr-plugin-sesh](https://github.com/fullerzz/herdr-plugin-sesh) — Sesh-style workspace picker TUI, integrated with zoxide so frequently used directories surface first. ⭐ 52 · MIT
- [herdr-workflows](https://github.com/aorumbayev/herdr-workflows) — Record a repeated sequence in a Herdr pane as a short YAML workflow file and replay it from a hotkey; steps can run shell commands, start coding agents and wait for them, call Herdr API methods, or chain other workflows. ⭐ 40 · MIT

## Browsers and viewers

- [terminal-browser](https://github.com/zenbu-labs/terminal-browser) — A real browser rendered inside your terminal, with a Herdr plugin in `zenbu-labs/terminal-browser/herdr-plugin`. ⭐ 4.5k · MIT
- [terminal-code](https://github.com/zenbu-labs/terminal-code) — VS Code inside your terminal, from the terminal-browser team, with the same split-pane Herdr plugin in `zenbu-labs/terminal-code/herdr-plugin`. ⭐ 2.2k · MIT
- [termscope](https://github.com/iurysza/termscope) — Open files and links already visible on your terminal screen in a split. ⭐ 71 · MIT

## Git and worktrees

- [herdr-worktrunk](https://github.com/devashish2203/herdr-worktrunk) — Switch, create, and remove git worktrees through worktrunk without leaving Herdr. ⭐ 197 · MIT
- [herdr-lazygit](https://github.com/Crokily/herdr-lazygit) — lazygit in a narrow sidebar pane that expands to the full layout on one key, with AI-generated commit messages. ⭐ 45 · MIT

## Remote access

- [sheprd](https://github.com/sheprd-labs/sheprd) — Native workspace for terminals and AI agents (Rust/GPUI): workspaces, tabs, splits, agent monitoring, files, diffs, and phone remote; supports both a Herdr daemon and the bundled herdr-core. macOS, Linux, Windows. Formerly herdr-gpui. ⭐ 2.2k · Apache-2.0
- [ovis](https://github.com/devswha/ovis) — Browser and phone client for Herdr: chat view, live terminal, pane approvals, push alerts, worktree creation, and file viewer. Requires Herdr 0.9+. ⭐ 2.0k · MIT
- [herdr-remote](https://github.com/dcolinmorgan/herdr-remote) — Monitor and drive agents from the macOS menu bar, a phone, or Telegram, with zero config locally. ⭐ 448
- [roamgate](https://github.com/powerfooI/roamgate) — Browser client for a running Herdr server: terminals, agent sessions, and file and diff review, on desktop or phone. Formerly herdr-studio. ⭐ 324 · MIT
- [herdr-web](https://github.com/kcosr/herdr-web) — Browser client for a running session, over a Rust HTTP/WebSocket bridge that works around Herdr allowing only one terminal attach owner. A companion app, not a plugin; needs Herdr 0.8.0+. ⭐ 165 · MIT
- [herdr-hud](https://github.com/finna/herdr-hud) — Floating desktop HUD for macOS and Windows: a draggable button that opens Herdr agents, recent output, and a prompt composer above fullscreen apps, locally or over SSH/Tailscale. ⭐ 119 · MIT
- [herdrx](https://github.com/riba2534/herdrx) — Self-hosted, multi-user remote Herdr terminal workbench: access and share Herdr sessions from a web browser, with per-user auth. ⭐ 40 · MIT

## Phone and mobile

- [collie](https://github.com/AltanS/collie) — PWA for managing Herdr from your phone over a tailnet: see which agents are blocked, read panes, reply, and get push notifications. ⭐ 1.6k · MIT
- [Heeler](https://github.com/ZingerLittleBee/Heeler) — Native iOS agent console: every agent on your machines sorted by who needs you, a live terminal to steer, and a full-keyboard composer. ⭐ 835 · Apache-2.0
- [herdr-mobile-relay](https://github.com/0cv/herdr-mobile-relay) — Mobile web app for approving and monitoring agents remotely — the approvals half of the problem. ⭐ 371
- [pairfob](https://github.com/arronKler/pairfob) — Your Herdr agents on your phone over an end-to-end encrypted peer-to-peer channel; the computer dials out so no inbound ports or VPN are required. Read, reply, approve, and get push alerts. ⭐ 183 · Apache-2.0
- [whip](https://github.com/kosumic/whip) — Android app for supervising Herdr over SSH or Tailscale, falling back to a plain SSH shell when Herdr is not there. Note the AGPL-3.0 copyleft. ⭐ 132 · AGPL-3.0
- [herdr-telegram-agents](https://github.com/permgps/herdr-telegram-agents) — Telegram bot bridge for Herdr agents: receive agent status, answer prompts, and send commands from any Telegram client. ⭐ 87 · MIT

## Editor integration

- [herdr-nvim](https://github.com/ChmaraX/herdr-nvim) — A persistent, full-height Neovim sidebar one key away, with quick access to the files your agent is working on. ⭐ 342 · MIT
- [vim-herdr-navigation](https://github.com/paulbkim-dev/vim-herdr-navigation) — Seamless `Ctrl+h/j/k/l` across Herdr panes and Vim/Neovim splits, in the spirit of vim-tmux-navigator. ⭐ 115 · MIT
- [zed-herdr](https://github.com/ImArtisann/zed-herdr) — Keeps the active Herdr workspace open in Zed without either app owning the other. macOS and Linux, Herdr 0.7.3+. ⭐ 36 · MIT

## Orchestration and agent status

- [shepherdr](https://github.com/eliasstravik/shepherdr) — Herdr layout providing mission control for herdr-core agents: a space's Assistant coordinates tasks, each in its own git worktree, with review and merge gates. Formerly herdr-projects. ⭐ 1.1k · MIT
- [pi-herdsman](https://github.com/boadij/pi-herdsman) — Pi extension for asynchronous subagents and agent-fleet orchestration: delegated tasks run as background Pi sessions that Herdr places and owns. Requires Herdr ≥ 0.9.1 and `herdr integration install pi`. ⭐ 220 · Apache-2.0
- [herdr-radar](https://github.com/hhdebb/herdr-radar) — Sidebar plugin that regroups Herdr's Agents list by project, shows each agent with its vendor logo and colour, and distinguishes working, waiting on you, and parked states. ⭐ 204 · MIT
- [herdr-agent-usage](https://github.com/levi-qiao/herdr-agent-usage) — Model, context, and subscription quota for each agent in Herdr's sidebar, grouped by Space, for Claude, Codex, Grok, OpenCode, Pi, Cursor, and more. Formerly herdr-agent-quota. ⭐ 159 · MIT
- [agent-router](https://github.com/nidhi-singh02/agent-router) — CLI that filters your subscriptions by fixed rules, asks TypeSafe to rank the rest and pick model and effort level, then launches Cursor, Claude Code, Codex, or OpenCode in a Herdr pane. ⭐ 124 · MIT
- [omo-herdr-dag](https://github.com/jc01rho/omo-herdr-dag) — DAG visualization and orchestration for Omo workflows running in Herdr, with per-node status, retry controls, and a live timing view. ⭐ 124 · MIT
- [pi-bellwether](https://github.com/joelhooks/pi-bellwether) — Pi package for controlling a Herdr runtime from Pi over the socket API, with typed errors, timeouts, and watch lifecycles. ⭐ 89 · MIT
- [herdr-lantern](https://github.com/aigorahub/herdr-lantern) — Shows which agent in the herd needs you and what each is working toward, then jumps you to its pane or starts a new one. ⭐ 74 · MIT

## Extras

- [crabbox](https://github.com/openclaw/crabbox) — Warm a box, sync the diff, run the suite: ephemeral environments so agents execute somewhere other than your machine. Install the plugin subdirectory, `openclaw/crabbox/plugins/herdr`. ⭐ 1.5k · MIT
- [herdr-auto-title](https://github.com/kryptamine/herdr-auto-title) — Generates tab titles from Claude Code, Codex, and Pi conversations — the content, where herdr-automatic-rename uses the process name. ⭐ 279 · MIT
- [memex](https://github.com/nicosuave/memex) — Search transcripts across Claude Code, Codex, Pi, OpenCode, Copilot, and Cursor, and resume a session from a hit. ⭐ 308 · MIT
- [tsk](https://github.com/smarzban/tsk) — Terminal task board shared by you (TUI) and your agents (CLI); `tsk setup herdr` binds prefix+t to the workspace's board and prefix+a to quick-capture a task from any pane. ⭐ 264 · MIT
- [herdr-automatic-rename](https://github.com/qu8n/herdr-automatic-rename) — Renames tabs from each pane's foreground process, tmux `automatic-rename` style, and adds 1-9 jump keys. Needs Herdr 0.7.1+. ⭐ 229 · MIT
- [herdr-ts-sdk](https://github.com/dmmulroy/herdr-ts-sdk) — Effect-native TypeScript SDK for Herdr's local Unix socket API: every operation as a typed `Effect`, socket responses decoded with Effect Schema, live events as `Stream`. ⭐ 56 · MIT
- [herdr-beads](https://github.com/miiraheart/herdr-beads) — `bd` task board for Herdr: List, Table, and Kanban views over your bd issues, docked as a sidebar or floating popup; edits go straight to `bd`. ⭐ 42 · MIT
- [herdr-floax](https://github.com/Tyru5/herdr-floax) — Toggleable floating scratch shell per workspace, in the style of tmux-floax. ⭐ 28 · MIT

## Articles

- [A deep dive into Herdr](https://flaviocopes.com/herdr/) — Flavio Copes on the repositories he actually runs it against, his agents/dev/checks/deploy tab layout, a deliberately minimal config, and limits he hit in use — including parallel pushes jamming a Cloudflare Pages build queue. 2026-08-10.
- [I Gave Up tmux and Zellij for Herdr](https://www.joshfinnie.com/blog/switching-to-herdr/) — Josh Finnie's hands-on switch, with his actual `config.toml`, plugin picks, and an honest list of tradeoffs. 2026-08-06.
- [herdr and cmux: two shapes of the same agent multiplexer](https://blog.debedb.com/2026/07/26/herdr-and-cmux-two-shapes-of-the-same-agent-multiplexer/) — A structural comparison of the two designs with named Herdr limitations. The author says outright he has not run Herdr in anger, so it is stronger on cmux; read it for the framing. 2026-07-26.
- [Herdr: a tmux for agents](https://en.thedavestack.com/herdr-a-tmux-for-agents/) — Architectural take on the control surface and plugin model from someone building orchestration on top of it. Start here if you want to script Herdr.
- [Herdr Review: The Agent Multiplexer Your Terminal Needed](https://andrew.ooo/posts/herdr-agent-multiplexer-terminal-review/) — A day of real use with Claude Code and Codex, with a comparison table against tmux and Zellij, and named limitations. Written against v0.4.0, so check version-specific claims. 2026-07-08.
- [Terminals That Outlive the Laptop](https://intertwingly.net/blog/2026/09/14/Terminals-That-Outlive-the-Laptop.html) — Sam Ruby, 2026-09-14: forwarding a Mac's Herdr socket over SSH to a Linux laptop and building an Omarchy plugin that mirrors the session on the remote display. Herdr 0.9.0, Omarchy 4.0.3.
- [herdr vs cmux, after two months on each](https://coles.codes/posts/herdr-vs-cmux/) — Matt Coles, 2026-08-02: a two-month comparison on Linux and Mac with versions stated (herdr 0.7.4, cmux 0.64.x) and concrete differences in keybinding model, plugin discovery, and SSH handling. 2026-08-02.
- [Herding parallel agents on a remote box with herdr](https://coles.codes/posts/herding-agents-with-herdr/) — Matt Coles: running parallel agents on a remote Ubuntu box with Herdr 0.7.3, with setup commands, keybindings including a suspend-and-detach shortcut, and SSH config for one-command attach. 2026-06-10.

## Discussion

- [Herdr: One terminal to rule them all](https://news.ycombinator.com/item?id=48756578) — The largest Herdr thread on Hacker News. 404 points, 178 comments. 2026-07-02.
- [Herdr is joining Y Combinator. The runtime stays open](https://news.ycombinator.com/item?id=49201003) — The funding thread, and the recurring question of what stays open when a terminal tool takes money. 281 points, 189 comments. 2026-08-06.
- [Herdr: Agent multiplexer that lives in your terminal](https://news.ycombinator.com/item?id=48714802) — The thread that introduced most people to it, with a useful argument about whether running many parallel agents is actually a good idea. 166 points, 110 comments. 2026-06-29.
- [Connecting the machines](https://news.ycombinator.com/item?id=49612818) — The HN thread on the 0.9 multi-machine announcement: the argument over Herdr Cloud versus self-hosted SSH discovery, and what the funding means for the open runtime. 2026-09-08.

## Related lists

- [yigitkonur/awesome-herdr](https://github.com/yigitkonur/awesome-herdr) — The established curated index of the Herdr ecosystem: tools, workflows, configs, clients, skills, and integrations. Broader than this list; check it before concluding something does not exist. ⭐ 289 · MIT

## Contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md). Short version: open the thing, run it on the current Herdr release, describe it in one sentence, and never list what you have not used.

Entries are tracked in [`data/sources.json`](data/sources.json) and re-verified weekly. Additions serve a three-week probation before they appear here, and removals need three consecutive failures — this list is meant to be boring and trustworthy rather than fresh.

## License

[CC0 1.0](LICENSE) — to the extent possible under law, the contributors have waived all copyright and related rights to the curation in this repository. Linked works keep their own licenses.
