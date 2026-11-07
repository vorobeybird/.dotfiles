---
name: Remote SSH
description: Use when executing commands, inspecting files, or working on the user's remote work machine over SSH.
---

# Remote Work Machine (SSH)

The user works primarily on a remote machine accessible via SSH. Its connection details are stored outside the public dotfiles repository in environment variables and `~/.ssh/config`.

## Environment Variables & SSH Alias
- `$OPENCODE_REMOTE_HOST`: `<user>@<ip>`
- `$OPENCODE_REMOTE_PORT`: `<port>`
- SSH Host alias in `~/.ssh/config`: `remote-work`

## Connection Commands
Always use non-interactive SSH commands using either the SSH host alias or the environment variables so they match the pre-approved permission rules without exposing private IPs in tracked files:

```bash
ssh remote-work "<command>"
# or
ssh $OPENCODE_REMOTE_HOST -p $OPENCODE_REMOTE_PORT "<command>"
```

For copying files:
```bash
scp <local-path> remote-work:<remote-path>
scp remote-work:<remote-path> <local-path>
```

## Guidelines for Remote Work
1. **Never start an interactive shell session** (`ssh remote-work` with no command) or interactive programs (`vim`, `nano`, `top`, `htop`). Always pass a command that exits cleanly.
2. **Batch related read commands** into a single SSH invocation to avoid connection overhead (e.g., `ssh remote-work "cd ~/project && git status && git diff"`).
3. **Use safe quoting**: For multi-line scripts on the remote host, pass the script via heredoc over stdin:
   ```bash
   ssh remote-work 'bash -s' << 'EOF'
   cd ~/project
   git status
   EOF
   ```
4. **Never hardcode the resolved IP, username, or port** into tracked configuration files, skills, or commit messages.
