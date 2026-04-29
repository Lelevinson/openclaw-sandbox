### first-time devcontainer setup
copy `.env.example` to `.env` manually before opening or rebuilding the devcontainer

### check project context7 mcp
do `codex mcp list` from the repo root; `context7` should show as enabled

### shutdown timed out error
do `pkill -9 -f openclaw`

### open openclaw workspace dir in vscode
do `code /home/node/.openclaw/workspace`

### reset openclaw (full)
do `openclaw reset` then `rm -rf /home/node/.openclaw/* /home/node/.openclaw/.[!.]*`

### openclaw gateway service
select **NO**
