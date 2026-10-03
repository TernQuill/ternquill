# What's new in TernQuill

Written for people using the app: what changed and what it means for you.
`scripts/release.sh` takes the section for the version it releases (and
refuses to release without one) and ships the recent sections with the
update, so the update window shows everything since your version.

Format: `## <version>`, then `### New`, `### Improved` or `### Fixed`, then
bullets that start with a **bold name**.

## 0.8.9

### New
- **A faster terminal engine** — the terminal is now drawn by xterm.js on the graphics card (WebGL), from a set of ready-made letters instead of one by one. Big output scrolls past faster (up to a quarter quicker on a Mac), animations around the terminal stay smooth, and it keeps 10,000 lines of history. Same font, letter spacing and colours as before; lines sit a little further apart, as in Ghostty.

### Improved
- **One font size for the terminal and the input bar** — Settings → Terminal → Font size now sets both, and the terminal's text is drawn as light as the input bar's, so they read as one.
- **The scrollbar keeps out of the way** — thin and quiet, shown while you scroll and when you point at it.

### Fixed
- **The input bar with prompt themes** — with powerlevel10k (and similar themes) the input bar didn't come up; it does now.

## 0.8.8

### Improved
- **The server's name while you're in ssh** — a pane's header and its tab show the server you're on (from its prompt, e.g. pxmx02, or the address you connected to) instead of your Mac, with a server icon.

## 0.8.7

### Improved
- **A log for when something goes missing** — TernQuill now notes what it saves before an update and what it takes back after (which shells and AI chats, nothing of what you type or see) in ~/Library/Logs/TernQuill/app.log, so a lost tab or chat can be traced.

## 0.8.6

### Improved
- **The menu bar no longer covers your tabs in full screen** — when it slides in, the tab bar slides down with it and everything under it makes room; the input bar stays put. Or put the tabs at the bottom in full screen: Settings → Terminal → Tabs at the bottom in full screen.
- **No scrollbar flash when a terminal changes size** — resizing the window, splitting or the full-screen tab bar no longer blinks the terminal's scrollbar.

### Fixed
- **Full screen without the thick bar** — in full screen the window kept a tall empty strip above the tabs (and showed it again whenever the menu bar slid in). It's gone; the tabs start at the left edge there, since full screen has no window buttons.

## 0.8.5

### Improved
- **Lighter with many tabs** — a new title, folder or name in one tab no longer redraws the terminals in every other tab.

### Fixed
- **Updating keeps your shells and AI chats again** — in 0.8.4 the new version couldn't reconnect to the terminals and agents the old one left running, so after the update your tabs, their history and open AI chats were gone (the conversations themselves stayed saved — /resume finds them). The terminal helper now runs from its own copy of the app, which an update doesn't replace. Updating from 0.8.4 itself still starts fresh shells once; AI chats come back and continue.
- **Honest system requirements** — TernQuill needs macOS 13 Ventura or later on Apple silicon; it claimed to run on 10.13.
- **A slow start no longer breaks restoring your tabs** — if TernQuill took a moment to start, restoring could stall for good and nothing was saved after that.

## 0.8.4

### Improved
- **Closing asks when something still runs** — ⌘W, closing a tab, "Close other tabs" and "Close group" ask first if a command, an ssh session or an agent is still at work there, and name it. Don't want that? Settings → Terminal → Ask before closing.
- **⌘K finds more** — the AI panel, find, next/previous pane and command, leaving a pane out of broadcast, note folders, closing, checking for updates and switching the theme.
- **"AI" instead of "Claude"** where it means any agent: the rail, the View menu (AI Panel), "Ask AI about this", and AI tabs named after their agent (Gemini CLI, Codex…).
- **Removing a notes folder or an agent asks first** (Settings saves on its own).
- **"Write a runbook" from a note** always uses a Claude Code chat — reading the terminal is Claude Code's.
- **Notes folders set to Off are really off** — AI agents now run in a macOS sandbox that can't read or change those folders, whatever path or command they try (before, only Claude Code's own file tools were stopped). Works for every agent except Codex, which runs its own sandbox — its chat tells you so.

### Fixed
- **Keys arrive in the order you type them** — a large paste could be overtaken by the Enter or Ctrl+C you pressed right after it; now everything typed into a terminal (and every message to an AI agent) goes out strictly in order.
- **Very large pastes** (several MB) no longer cut the connection to your shells.
- **Ten times more scrollback** — terminals kept only about 600 lines of history; now about 5,600 full-width lines (the same as Ghostty).
- **Command blocks after a long session** — once the history was full, a block's hover, "Copy output" and "Ask AI" could point at another command's output. They stay on their own command now.
- **✦ on a note in a folder set to Off** is gone — it would have sent the note to the AI.
- **Rename and Delete** appear only for notes in your folders, not on a project's own README and docs.
- **"Close other tabs" and "Close group"** now also stop the AI chats in those tabs.
- **⌥⌘I with broadcast off** now says why nothing happened.
- **Switching the theme switches macOS's parts too** — menus, dialogs and the window frame change at once, not after a restart.
- **A custom theme with a mistake** shows in Settings → Appearance with what's wrong and on which line, instead of silently missing. Theme previews understand any CSS colour (rgb(), oklch()…).
- **Notes search** shows "Searching…", says when nothing matched, and when a folder couldn't be searched.
- **Completion doesn't re-ask on every letter** — with a menu open, kubectl, gh, helm, terraform and spec generators are asked once and the list narrows as you type (no call to your cluster for each key).
- **Menus by keyboard** — right-click menus move with ↑/↓ and pick with ↵; dialogs take the focus and give it back.
- **Accessibility** — icon buttons have names for VoiceOver, settings switches are announced with their label, and the model/agent pickers close with Esc or a click outside.
- **Docs** — the shortcut list gained ⌥⇥ and the AI panel's keys; a few wrong or doubled bits fixed.
- **Less work in the background** — the AI setup screen checks the agent every 10 s instead of 4 (and only while you're in the window); a running command's timer in a hidden tab no longer redraws.
- **Your saved tabs are safer** — a session file that can't be read is kept aside (session.json.bad) instead of being overwritten with a fresh start, one broken tab no longer loses the others, and a failed save tells you and tries again.
- **Settings that can't be read** (a typo from editing by hand) are kept aside and TernQuill starts with defaults and tells you — instead of not starting at all.
- **An agent that never answers** no longer leaves its chat "starting" forever: after a while it stops with a message.
- **"Session ended" comes after the last output**, not before it.
- **Renaming a note only by letter case** (Note → note) works.
- **Notes: an edit is never written over a change a sync tool made in the same moment.**
- **Notes: switching notes right after typing** could mark the next note "changed on disk" and lose what you then typed there (more likely on a slow disk or a synced folder). Each open note now saves on its own.

## 0.8.3

### New
- **Updates don't close your shells** — ssh sessions, builds and anything else running in TernQuill keep going while it updates, and every terminal comes back showing what it showed before. Quitting TernQuill (⌘Q) still closes them. If TernQuill crashes, its shells wait 10 minutes for it to come back. This starts with the update *from* 0.8.3 to the next version.
- **Approvals sealed in your Keychain** — what you approved in Settings (agents, notes folders) is sealed with a key only TernQuill can read from your Keychain. Another program can no longer approve its own change to your settings, or delete the approvals to start over: either way, everything waits for you again.
- **…and neither does Claude** — a Claude Code chat keeps working through an update: an answer half-written goes on, a question waiting for your Allow is still there afterwards. So updating no longer waits for Claude to finish. Other agents (Gemini, Codex…) still restart and pick up their chat.

### Fixed
- **Security review** (three independent passes) — among the fixes:
  - The background helper only talks to TernQuill itself (its code signature is checked on both ends), so no other program can use it to run commands or take over a shell or chat.
  - Pressing Tab in a folder no longer runs that folder's code (`make`, `rake`, `bundle`, `npx`, `bin/…` completions are off).
  - Broadcast no longer copies a password you type into the other panes.
  - AI answers' Run button now puts the command in your input bar — you see all of it and press Enter.
  - Permission cards show everything a tool would get, and every rule "Always allow" would save.
  - Deleting a note can't be redirected outside the vault; pasted images never overwrite anything.
  - Agent settings can't smuggle an approval with a duplicate id, and a no-prompt mode set from outside waits for approval.
  - The updater and helper ignore whatever environment they were started with.
- **Terminals fit their pane again** after some resizes where they stayed a few rows too tall and the last lines hid behind the input bar.

## 0.8.2

### New
- **Settings changed elsewhere wait for you** — if something other than TernQuill edits an AI agent's command or environment, the agent doesn't start until you approve it in Settings → AI agents, which shows exactly what it would run. A notes folder set to Allow from outside counts as Ask first until you approve it.

### Improved
- **Tighter data folder** — TernQuill's folder and files must belong to you; if others could change them, the permissions are tightened. Themes now live in a private folder too.

## 0.8.1

### Improved
- **Settings in a tab** — ⌘, opens Settings like Docs: sections on the left (Appearance, Terminal, AI agents, Notes, Updates), all on one page, with search. Changes save on their own — no Save button.
- **Theme previews** — Appearance shows each theme as a small picture of the app, your own themes included. New theme files show up when you come back to TernQuill.

### Fixed
- **Safer custom themes** — a theme file can only change colours: only known colour names are read, each value must be a real colour, and anything else is ignored. TernQuill reads only plain JSON files up to 64 KB in the themes folder (no links to other files), and a theme's name is kept to one short line.

## 0.8.0

### New
- **Light theme** — Settings → Appearance: Dark, Light, or Match macOS. The whole app switches at once, terminals included — even what's already on screen.
- **Your own themes** — a theme is a small JSON file with the colours you want to change. "Open the themes folder…" in Settings puts an example there to start from; save the file and pick it in the list. See Docs → Appearance & themes.

## 0.7.2

### Improved
- **Smooth resizing** — dragging a divider between panes, the edge of the AI or Notes panel, or the Notes folder list follows the pointer exactly; terminals resize as you drag instead of after you let go, and a PDF no longer catches the pointer half-way.
- **Dividers light up** in the accent colour when you can grab them and while you drag.

## 0.7.1

### New
- **Leave a pane out of broadcast** — click a pane's label in its header (or right-click → Exclude from broadcast, ⌥⌘I). It shows "paused" and gets nothing; typing in it goes only there, so you can do one thing on one server without turning broadcast off. Click again to bring it back. The title bar shows how many panes take part ("2 of 3 panes").

## 0.7.0

### New
- **Notes next to your terminal** — Notes is now a panel on the left (⌘⇧N or the rail button), so a runbook and the terminal you're running it in are side by side. The ▢ button in a note's header opens it as a tab of its own.
- **PDFs in Notes** — PDFs in your vault show up in the folder list and open right in Notes.

### Improved
- **Folder list width** — drag its edge; TernQuill remembers it.

## 0.6.1

### Improved
- **Properties like Obsidian** — a note's properties (frontmatter) show as a list with icons: tags as pills, dates as dates, checkboxes, links. Click to edit the text.

## 0.6.0

### New
- **AI and your notes** — ✦ in a note's header: ask about the note, improve it, or write a runbook of what you just did in the terminal. The prompt waits in the AI panel; you press Enter. Edits arrive as a card showing the change — nothing is written until you allow it.
- **AI access per vault** (Settings → Notes): Ask first (default) — the agent asks before it reads or changes notes there; Allow — it reads freely, edits still ask; Off — it can't see the vault at all. Claude Code for now; other agents follow.

### Improved
- **AI from Notes or Docs** works in the folder of the terminal you were last in, not your home folder.

## 0.5.2

### Improved
- **Hide the folders** — the button next to a note's path (or ⌘\\) shows or hides the folder list in Notes, also for a note opened to the side.

## 0.5.1

### Improved
- **Tables** in notes show as a real table; click one to edit its text.
- **Foldable callouts** — `> [!note]-` starts folded, `+` open; the arrow toggles.
- **Links to headings** — `[[Note#Heading]]` shows as "Note › Heading" and jumps to the heading.
- **Undo after outside changes** — when a note reloads because another app changed it, ⌘Z can still undo.
- **Tags** — suggestions appear as soon as you type `#`.

### Fixed
- **Line endings** stay exactly as they were in the file (Windows-style, mixed or not).
- **Images inside a callout** stay inside its box.
- **`[[#Heading]]`** (a heading in the same note) jumps there instead of making an empty note.

## 0.5.0

### New
- **Notes** — write and read markdown notes in TernQuill: connect your Obsidian vault (Settings → Notes, or the button in Notes), and the README and docs of the project you're in show up on their own. ⌘⇧N opens Notes, ⌘P finds a note.
- **Writes like Obsidian** — formatting shows as you type; `[[links]]`, `#tags`, callouts, checklists, tables and pasted images work, and your files stay exactly as Obsidian writes them. Saves by itself; if a note changes in another app meanwhile, you choose which version stays.
- **Runbooks** — shell code blocks in a note have Run: the command lands in your terminal's input bar, ready for Enter.
- **Next to the terminal** — right-click a note → Open to the side.

## 0.4.15

### Fixed
- **The AI panel stays put** — clicking into the terminal no longer folds it. It folds only when you ask: ⌘L, the ✦ on the left, its × or moving the chat to a tab.

## 0.4.14

### Fixed
- **Chats stay on the strip** — back to how 0.4.12 worked: folding the AI panel keeps every chat on the strip, empty ones too. The strip goes away when you close the last chat.

## 0.4.13

### Improved
- **A tidier right edge** — when the AI panel folds, chats you never wrote in are dropped; with no chats left, the strip on the right disappears too.

## 0.4.12

### New
- **Several AI chats** — a strip on the right edge of the AI panel lists its chats: **+** starts a fresh one (any agent, any model), a click switches. Each keeps working while you look at another; a spinning ring means working, an accent dot waiting for you, a small dot a new reply.
- **The panel folds away** — click into your terminal and the AI panel tucks in; its chats stay on the strip. Click one (or ⌘L) to bring it back.

### Improved
- **Colours** — the chat header's dot follows the app's colours (green ready, accent working) instead of the agent's brand colour.
- **All chats come back** — after a restart or an update, every chat in the panel is restored, not just the one you were looking at.

## 0.4.11

### New
- **Switch to Auto when you keep saying yes** — after you've allowed two steps in a chat, the next question offers to allow it and let the agent continue on its own (Claude's Auto, with its safety check). "Not now" keeps asking.

### Improved
- **Lighter on memory** — closing tabs now gives their memory back; before, every closed tab kept its terminal around.
- **Smoother AI answers** — long answers stream without slowing the window down.
- **Background tabs rest** — tabs you're not looking at no longer redraw 60 times a second.
- **Fewer background processes** — completion for tools like kubectl waits until you stop typing instead of running on every key.
- **Fair output** — a pane flooding output no longer holds up the others.
- **Ask AI about this** — sends the command you right-clicked, not just the last one.

### Fixed
- **Closing a tab always ends its programs** — programs that ignore the hang-up signal are stopped after two seconds instead of running on.
- **Agents stop cleanly** — no leftover helper processes after a chat ends; a restarted chat is no longer marked stopped by the old one.
- **Security: launch settings** — the installed app ignores environment settings another program passes when starting it (only the basics like your home folder and language are kept).
- **Security: updates** — an update is only offered when its signature checks out, and downloads can't be redirected to another server.
- **Security: broadcast** — passwords you type are never shown in the other panes.
- **Folder names with backslashes** are reported correctly.

## 0.4.10

### Improved
- **Updates just work** — TernQuill knows where its updates come from; the release-server field is gone from Settings.

## 0.4.9

### New
- **Ask AI from the right-click menu** — select text in the terminal (a stack trace, a log line), right-click and choose *Ask AI about this*. With nothing selected it sends the last command and its output.

### Improved
- **Calmer broadcast** — no more spinning frame around the tab. Each pane says whether you're typing there or it mirrors, only the bar you type in is lit, and the other panes show what you type (dimmed) before Enter sends it to all of them.

## 0.4.8

### Fixed
- **$SHELL in terminals** — 0.4.7 left it empty in new tabs; it's your account's shell again.

## 0.4.7

### Improved
- **Safer multi-line pastes** — pasting several lines into a program that would run each one immediately (plain ssh, older tools) now asks first and shows what will run.
- **Security: locked-down window** — the app's window only runs TernQuill's own code, as an extra safety net.

### Fixed
- **Security: completion** — names that come from programs (git branches, npm scripts, kubectl…) are quoted when inserted, so a booby-trapped name can't run code when you press Enter; pressing Tab never runs code from what you typed.
- **Security: folder reports** — only TernQuill's own shell integration can tell the app which folder you're in.
- **Security: updates** — TernQuill only ever installs a newer version, shows only update notes signed by us, and refuses oversized downloads.
- **Security: sharing your terminal** — the agent gets exactly the tab shown on the card, even if you switch tabs before answering.
- **Security: installed app** — ignores settings that another program could pass when launching it, and is signed with macOS's hardened runtime.

## 0.4.6

### Fixed
- **Security: fake shell reports** — text shown in the terminal (a file you `cat`, output from a server) could pretend to be TernQuill's shell integration and change which programs completion runs. The app now only trusts reports signed with a secret per terminal.
- **Security: pasting** — hidden control characters in pasted text (or in a command from an AI answer) are removed, so a paste can't sneak in a command that runs by itself.
- **Security: links** — ⌘-click and links in AI answers open only web and mail addresses; other kinds (files, app links) could launch programs.
- **Security: updates** — each release's version is now signed too, so an old release can't be passed off as a new one.
- **Security: AI answers** — images from the internet in answers aren't loaded (they could carry data out); you can open them yourself.
- **Security: test hooks** — hooks for automated testing only work in development builds, not in the installed app.

### Improved
- **Libraries** — Go dependencies updated; no known vulnerabilities in any library TernQuill uses.

## 0.4.5

### Improved
- **Update window** — shows what's new in every version since yours, laid out like the docs.
- **Under the hood** — the app's biggest parts are split into smaller pieces, so fixes and new features land faster and break less.

## 0.4.4

### Improved
- **Under the hood** — the main window's code is split into smaller parts. Nothing should look different.

## 0.4.3

### Improved
- **One accent colour** — buttons, switches and selections use the logo's violet-to-blue instead of white.

## 0.4.2

### Fixed
- **Picking up where you left off** — after an update the AI panel and your last tab open again.

## 0.4.1

### New
- **Clickable links** — ⌘-click a link in the terminal to open it in your browser, even one that wraps over several lines.

## 0.4.0

### New
- **More AI agents** — besides Claude Code, add pi, Gemini CLI, Codex, OpenCode, Goose or any agent that speaks ACP in Settings → AI. Chats with different agents can run side by side.
- **Several accounts** — add a second account of the same agent; each keeps its own sign-in.
- **Cost of a chat** — shown in the panel header when the agent reports it.

## 0.3.0

### Improved
- **Much faster terminal** — big output (logs, builds) renders up to 8× faster and the window no longer freezes while it scrolls by. Memory use during floods dropped to a quarter.

## 0.2.9

### New
- **Run from answers** — code blocks in AI answers have Copy and Run; Run sends the command to your terminal tab.

## 0.2.8

### New
- **Now playing** — what Apple Music or Spotify is playing shows in the title bar; hover it to pause or skip.

### Improved
- **Permissions stick** — macOS remembers what you allowed TernQuill (screen recording, controlling Music) across updates.

## 0.2.7

### Improved
- **Pure black input fields** — easier on OLED screens; the running-command light stays on the edge.
- **Messages while the agent works** — type and send; the message waits for its turn.

## 0.2.6

### New
- **The agent can read your terminal** — when you allow it, and only as much as you choose: the last N lines or everything.

## 0.2.5

### New
- **/resume** — continue an earlier Claude Code conversation, even one started in another terminal.

### Improved
- **Updates wait for the agent** — an update starts once the agent has finished what it's doing, and the chat picks up after the restart.

## 0.2.0

### New
- **AI panel (⌘L)** — Claude Code next to your terminal: asks before changing things, shows plans, edits and commands, understands images and your command output (✦ on a command).

## 0.1

### New
- **The input bar** — suggestions, history, completion for hundreds of tools, split panes, broadcast, tabs and groups, command blocks, and updates from your own server.
