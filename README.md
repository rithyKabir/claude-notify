# claude-notify

macOS desktop notifications for [Claude Code](https://claude.com/claude-code):

| Event | Notification | Sound |
|-------|-------------|-------|
| Claude finishes a task | **Claude Code** / *\<project folder\>* — "Claude task is done" | Glass |
| Claude needs permission | **Claude Code — needs permission** — "Waiting for your approval: \<tool\>" | Ping |
| Claude is waiting for input | **Claude Code — waiting** — the actual message | Ping |

Clicking a notification focuses the app Claude Code is running in (Terminal, iTerm2, PyCharm, VS Code, …) — detected automatically at runtime.

## Requirements

macOS with [Homebrew](https://brew.sh). Works on Apple Silicon and Intel.
Installed terminal-notifier.
Allow permission for teminal-notifier from settings to send notification.

## Install

1. Install the notifier binary:

   ```bash
   brew install terminal-notifier
   ```

2. Install the plugin (inside Claude Code):

   ```
   /plugin marketplace add rithyKabir/claude-notify
   /plugin install claude-notify@claude-notify
   ```

3. Allow notifications — send one test:

   ```bash
   terminal-notifier -title 'Claude Code' -message 'test'
   ```

   then open **System Settings → Notifications → terminal-notifier** and enable **Allow notifications**. Style: *Banners* auto-hide after a few seconds; *Alerts* stay until dismissed. **Notifications are silently invisible until you do this step.**

4. Restart Claude Code (or open `/hooks` once) to load the hooks.

## Troubleshooting

- **No notifications at all** → step 3 above; also verify `terminal-notifier -message test` shows one from a plain terminal.
- **Click opens the wrong app** → the target comes from `__CFBundleIdentifier` of the process that launched Claude Code; it falls back to Terminal.app when unset.
- **Uninstall** → `/plugin uninstall claude-notify@claude-notify`, then `brew uninstall terminal-notifier` if nothing else uses it.