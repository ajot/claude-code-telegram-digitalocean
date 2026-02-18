# Claude Code Telegram on DigitalOcean

Automated setup script for running [Claude Code Telegram](https://github.com/RichardAtCT/claude-code-telegram) on a DigitalOcean Droplet.

Send messages to Claude Code from Telegram. It reads your repo, makes changes, and responds — all running on your Droplet.

<table><tr>
<td><img width="300" alt="Telegram bot conversation" src="https://github.com/user-attachments/assets/ca2c91d9-473b-44c5-8996-ff8bf04237c1" /></td>
<td><img width="300" alt="Telegram bot conversation" src="https://github.com/user-attachments/assets/8b8ac8e9-5dd4-4dc9-b032-3527c9e31a4e" /></td>
</tr></table>

## Quick Start

SSH into a fresh Ubuntu Droplet and run:

```bash
curl -fsSL https://raw.githubusercontent.com/ajot/claude-code-telegram-digitalocean/main/setup-droplet.sh | bash
```

The script will walk you through everything interactively.

## What It Sets Up

1. **System packages** — zsh, git, gh, python3, build tools
2. **Oh My Zsh** — installed and set as default shell
3. **SSH deploy key** — generated and configured for GitHub
4. **GitHub CLI** — authenticated with your personal access token
5. **Poetry** — Python package manager
6. **Claude Code CLI** — installed and configured with your Anthropic API key
7. **Terminal compatibility** — sets `TERM=xterm-256color` for SSH
8. **Bot repo** — cloned, dependencies installed, known [`tool_name` bug](https://github.com/RichardAtCT/claude-code-telegram/issues/37) fix applied
9. **`.env` configured** — Telegram bot token, username, and allowed user IDs
10. **Systemd service** *(optional)* — run the bot in the background, auto-start on reboot

## Prerequisites

Before running the script, have these ready:

- A [DigitalOcean Droplet](https://docs.digitalocean.com/products/droplets/how-to/create/) running Ubuntu
- A [GitHub personal access token](https://github.com/settings/tokens) (scopes: `repo`, `read:org`)
- An [Anthropic API key](https://console.anthropic.com/)
- A Telegram bot token from [@BotFather](https://t.me/BotFather)
- Your Telegram user ID from [@userinfobot](https://t.me/userinfobot)

## Useful Commands

Once the bot is running as a systemd service:

```bash
systemctl status claude-telegram-bot     # check if it's running
journalctl -u claude-telegram-bot -f     # follow logs
systemctl restart claude-telegram-bot    # restart
systemctl stop claude-telegram-bot       # stop
```

Or run manually:

```bash
cd ~/claude-code-telegram
make run-debug    # with logs
make run          # production mode
```

## Detailed Walkthrough

See [blog-droplet-setup.md](blog-droplet-setup.md) for a step-by-step explanation of every command the script runs.
