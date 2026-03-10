# China Region Network Acceleration Guide

> How to configure x-cmd for optimal network access in China region

---

## Quick Detection & Configuration

```bash
# 1. Detect if in China region
x websrc testcn

# 2. Set x-cmd China channel (recommended)
x websrc set cn

# 3. Configure package manager mirrors
x apt mirror set tuna      # Debian/Ubuntu
x dnf mirror set tuna      # Fedora/RHEL
x npm mirror set ali       # Node.js/NPM
```

---

## Detailed Instructions

### Detect Current Network Region

```bash
x websrc testcn
```

- Returns `0` (true): Located in China region
- Returns `1` (false): Located overseas

### Switch Channels

| Command | Description |
|---------|-------------|
| `x websrc set cn` | Switch to China channel, use domestic CDN |
| `x websrc set inet` | Switch to international channel, use overseas sources |
| `x websrc set internet` | Same as `inet` |
| `x websrc set net` | Same as `inet` |
| `x websrc get` | View current configuration |

### Package Manager Mirror Configuration

**APT (Debian/Ubuntu)**
```bash
x apt mirror set tuna
```

Available mirrors: `ali`, `tuna`, `bfsu`, `ustc`, `tencent`

**DNF (Fedora/RHEL)**
```bash
x dnf mirror set tuna
```

Available mirrors: `ali`, `huawei`, `tuna`, `ustc`, `bfsu`

**NPM**
```bash
x npm mirror set ali
```

Available mirrors: `npmmirror` (default), `tencent`, `huawei`, `official`

### Docker Image Acceleration

Pull base images from AWS ECR (supports ubuntu, debian, alpine, etc.):

```bash
x docker ecpull ubuntu:22.04
x docker ecpull debian:12
x docker ecpull alpine:latest
```

Use cases:
- China users: Bypass Docker Hub access restrictions
- Overseas users: Bypass Docker Hub rate limits

---

## Complete Configuration Example

```bash
# Detect and configure China acceleration
if x websrc testcn; then
    x websrc set cn
    x apt mirror set tuna 2>/dev/null || true
    x dnf mirror set tuna 2>/dev/null || true
    x npm mirror set ali 2>/dev/null || true
    echo "China region acceleration configured"
fi
```

---

## Related Links

- [x-cmd Official Website](https://www.x-cmd.com)
- [x-cmd Documentation](https://x-cmd.com/llms.txt)
