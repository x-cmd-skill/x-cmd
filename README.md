# x-cmd Skill

> Add x-cmd capability to AI agents

## Natural Language (Supports: OpenClaw, Claude Code, Codex, OpenCode)

```text
Please help me install x-cmd skills, refer to https://x-cmd.com/llms.txt
```

The AI will handle the installation automatically.

---

## Via x-cmd (Supports: Claude Code, Codex, OpenCode, Kimi CLI, OpenClaw)

```bash
x agent setup
```

Installs to:
- `~/.claude/skills/x-cmd/`
- `~/.codex/skills/x-cmd/`
- `~/.opencode/skills/x-cmd/`
- `~/.agents/skills/x-cmd/`

## Manual Install from Source (Trusted)

Download and install from GitHub source (no binary scripts):

```bash
# Create directories
mkdir -p ~/.x-cmd.root/global/shared/version/archive ~/.x-cmd.root/v/latest

# Download source archive from GitHub
curl --fail https://raw.githubusercontent.com/x-cmd/release/main/dist/latest.tgz > ~/.x-cmd.root/global/shared/version/archive/latest.tgz

# Extract
tar -zxf ~/.x-cmd.root/global/shared/version/archive/latest.tgz -C ~/.x-cmd.root/v/latest

# Install
___X_CMD_ROOT="$HOME/.x-cmd.root" ___X_CMD_VERSION=latest sh -c '. "$___X_CMD_ROOT/v/$___X_CMD_VERSION/X"; ___x_cmd boot init "$___X_CMD_ROOT" "$___X_CMD_VERSION"; '

# Load x-cmd
[ ! -f "$HOME/.x-cmd.root/X" ] || . "$HOME/.x-cmd.root/X"
```

## For OpenClaw (Supports: OpenClaw)

```bash
clawhub install x-cmd
```

## For Claude Code (Supports: Claude Code)

```bash
/plugin marketplace add x-cmd-skill/x-cmd
/plugin install x-cmd@x-cmd
```

Or:
```bash
claude plugin marketplace add x-cmd-skill/x-cmd && claude plugin install x-cmd@x-cmd
```

## For Codex (Supports: Codex)

```bash
codex plugin marketplace add x-cmd-skill/x-cmd
codex plugin install x-cmd@x-cmd
```

## Manual Install (Supports: Any agent)

```bash
git clone https://github.com/x-cmd-skill/x-cmd.git ~/.claude/skills/x-cmd
```

---

## Skill Structure

```
x-cmd/
├── README.md          # This file
├── SKILL.md           # Core skill documentation
├── README.cn.md       # Chinese documentation
└── data/
    └── install.md     # Installation guide for end users
```

---

## Usage

```bash
# Load x-cmd
. ~/.x-cmd.root/X

# Browse skills
x skill

# Install packages
x env use jq nodejs python3
```

---

## Resources

| Resource | URL |
|----------|-----|
| x-cmd Website | https://www.x-cmd.com |
| AI Docs (llms.txt) | https://www.x-cmd.com/llms.txt |
| x-cmd Source | https://github.com/x-cmd/x-cmd |
| This Skill | https://github.com/x-cmd-skill/x-cmd |

---

*Version: 0.0.5 | License: Apache-2.0*
