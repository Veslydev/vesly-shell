# Vesly Shell

A purple **Zsh + Starship** SSH shell matching [Vesly MOTD](https://github.com/Veslydev/vesly-motd), with autosuggestions and syntax highlighting. Designed for Termius mobile, Warp SSH and normal SSH clients.

## One-line installer — Debian / Ubuntu / Proxmox

```bash
sudo apt-get update && sudo apt-get install -y git && D=$(mktemp -d) && git clone --depth 1 https://github.com/Veslydev/vesly-shell.git "$D/vesly-shell" && sudo bash "$D/vesly-shell/install.sh"
```

The installer installs `zsh`, `zsh-autosuggestions` and `zsh-syntax-highlighting` using apt. Starship v1.26.0 is downloaded from the official GitHub release and checked against a pinned SHA-256 for x86_64 or aarch64. No plugin managers, random `curl | bash`, or Nerd Fonts.

### What changes?

The login shell stored in `/etc/passwd` **does not change**. Only interactive SSH Bash with a TTY is switched to Zsh; remote commands, automation, rsync, SCP/SFTP, and non-interactive sessions retain their behavior. Already-Zsh SSH logins load the theme after `~/.zshrc`, so existing Oh My Zsh configuration remains intact. All users are supported via system-wide hooks.

- Desktop (90+ columns): two-line prompt showing user, hostname, path, Git branch/status and command duration.
- Mobile: one-line minimal purple prompt, chosen automatically from terminal width.
- `vesly-shell` launches a themed Zsh for quick testing.
- To roll back: `sudo bash /etc/vesly-shell/uninstall.sh`.
- The installer can be rerun without duplicate hooks. Packages are deliberately *not* purged on rollback.

## Limitations

The bundled installer targets Debian/Ubuntu/Proxmox. For NixOS use a declarative shell configuration; this repository does not edit generated NixOS `/etc`. Warpify may override a remote prompt using Warp's own integration. Plain Warp SSH and Termius render the Starship prompt directly. If Warpify and the Bash → Zsh redirect conflict, select the remote Zsh explicitly or disable the redirect for that session.

## Security

Existing `sshd_config`, PAM, SSH keys, root login shell, user dotfiles and MOTD settings are untouched. `/etc/zsh/zlogin`, `/etc/bash.bashrc` and `/etc/profile.d/vesly-shell.sh` receive only managed hooks. Backups are retained at `/var/lib/vesly-shell/backups`. Existing Zsh packages and local terminal history are not removed. Shell themes are updated *manually* by rerunning the reviewed GitHub installer; there is no root-level automatic code updater.

MIT License — 2026 Vesly Cloud Labs.
