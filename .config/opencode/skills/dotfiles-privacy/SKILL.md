---
name: Dotfiles & Config Privacy
description: Use whenever creating, editing, or staging dotfiles, OpenCode configs, skills, or any file tracked by the `config` (.cfg) repository.
---

# Dotfiles & Config Privacy Rules

The user tracks their dotfiles in a public Git repository (`~/.cfg`) managed via the `config` alias.

## Strict Privacy Rules
1. **Never hardcode private or sensitive data** in any file under `~/.config/` or any file tracked by `config`:
   - No private or public IP addresses, hostnames, or custom ports
   - No SSH usernames or machine-specific credentials
   - No API keys, tokens, passwords, or private URLs
2. **Use Environment Variables or Untracked Local Files**:
   - In `opencode.json(c)`, use `{env:VAR_NAME}` or `{file:~/.secrets/...}`.
   - In shell scripts or skills, reference `$VAR_NAME` or aliases defined in untracked files (such as `~/.ssh/config`, which is not tracked in `.cfg`).
3. **Verify Before Staging**:
   - Before running `config add <filepath>`, inspect the file content to ensure no IP addresses, ports, usernames, or secrets are present.
