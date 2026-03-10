# x-cmd Super Skill Architecture

> 如何组织 x-cmd-skill/x-cmd 这个超级 Skill —— 集中所有 x-cmd 适用于 AI 的功能，并支持派生独立可用的 Skills

---

## 核心理念

**一个入口，无限扩展**

- **SKILL.md** 作为统一入口，提供 x-cmd 的核心能力概述
- **extensions/** 目录存放各种垂直场景的子 Skills
- 每个子 Skill 可独立发布，也可通过主 Skill 统一访问

---

## 目录结构

```
x-cmd/
├── SKILL.md                              # 超级 Skill 主入口
├── ARCHITECTURE.md                       # 本文档 - 架构说明
├── extensions/                           # 子 Skills 目录
│   ├── install-x-cmd.SKILL.md           # 安装指南（基础）
│   ├── china-acceleration.SKILL.md      # 中国区加速（场景）
│   ├── module-advise.SKILL.md           # 模块开发 - Advise 配置（未来）
│   ├── module-tldr.SKILL.md             # 模块开发 - TLDR（未来）
│   ├── module-websrc.SKILL.md           # websrc 模块详解（未来）
│   ├── module-mirror.SKILL.md           # mirror 模块详解（未来）
│   ├── module-env.SKILL.md              # env 模块详解（未来）
│   ├── scenario-docker.SKILL.md         # Docker 使用场景（未来）
│   ├── scenario-git.SKILL.md            # Git 使用场景（未来）
│   └── ...                              # 更多场景化 Skills
├── README.md
├── README.cn.md
└── LICENSE.txt
```

---

## 命名规范

### 文件命名

```
{主题}-{子主题}.SKILL.md
```

| 类型 | 示例 | 说明 |
|------|------|------|
| 基础功能 | `install-x-cmd.SKILL.md` | 安装指南 |
| 区域/网络 | `china-acceleration.SKILL.md` | 中国区加速 |
| 模块详解 | `module-{name}.SKILL.md` | 具体模块使用指南 |
| 场景化 | `scenario-{name}.SKILL.md` | 特定使用场景 |
| 开发指南 | `dev-{topic}.SKILL.md` | 模块开发相关 |

### 文件后缀

**必须使用 `.SKILL.md`** —— 标识这是 Skill 文档，区别于普通 Markdown

---

## 内容组织原则

### 1. 主 SKILL.md 负责

- **核心定位**：x-cmd 是什么，能做什么
- **快速入口**：最常用的 5-10 个命令
- **导航引导**：链接到 extensions/ 中的子 Skills
- **不重复**：不在主文档详述具体模块用法

### 2. extensions/ 子 Skill 负责

- **垂直深入**：单个模块或场景的完整指南
- **独立可用**：可单独拿出来作为独立 Skill 使用
- **场景化**：解决具体问题的端到端方案

---

## 演进路径

### Phase 1: 核心基础（当前）

```
extensions/
├── install-x-cmd.SKILL.md           ✅ 安装指南
└── china-acceleration.SKILL.md      ✅ 中国区加速
```

### Phase 2: 模块详解（未来）

```
extensions/
├── module-websrc.SKILL.md           # websrc 模块 - 区域与渠道管理
├── module-mirror.SKILL.md           # mirror 模块 - 包管理器镜像
├── module-env.SKILL.md              # env 模块 - 软件包管理
├── module-advise.SKILL.md           # advise 模块 - 命令补全
├── module-tldr.SKILL.md             # tldr 模块 - 命令速查
└── module-pkg.SKILL.md              # pkg 模块 - 高级包管理
```

### Phase 3: 场景化 Skills（未来）

```
extensions/
├── scenario-docker.SKILL.md         # Docker 工作流
├── scenario-git.SKILL.md            # Git 工作流
├── scenario-data-processing.SKILL.md # 数据处理场景
├── scenario-devops.SKILL.md         # DevOps 场景
└── scenario-ai-development.SKILL.md  # AI 开发场景
```

### Phase 4: 开发指南（未来）

```
extensions/
├── dev-module-creation.SKILL.md     # 如何开发 x-cmd 模块
├── dev-advise-authoring.SKILL.md    # 编写 Advise 配置
├── dev-testing.SKILL.md             # 模块测试指南
└── dev-contribution.SKILL.md        # 贡献指南
```

---

## 独立发布策略

每个 extensions/ 中的 `.SKILL.md` 文件都可以独立发布为单独的 Skill：

### 示例：china-acceleration 独立发布

```bash
# 创建独立仓库
git clone git@github.com:x-cmd-skill/x-cmd-china-acceleration.git

# 复制内容
cp extensions/china-acceleration.SKILL.md x-cmd-china-acceleration/SKILL.md

# 添加必要的元数据
cat > x-cmd-china-acceleration/SKILL.md << 'EOF'
---
name: x-cmd-china-acceleration
description: China region network acceleration for x-cmd
parent: x-cmd
---

# 原内容...
EOF
```

### 元数据规范

独立发布的 Skill 需要添加前置元数据：

```yaml
---
name: x-cmd-{topic}                    # Skill 名称
description: |                         # 简短描述
  一句话说明这个 Skill 是做什么的

parent: x-cmd                          # 父 Skill 标识
source: extensions/{file}.SKILL.md     # 来源文件

license: Apache-2.0
compatibility: POSIX Shell

metadata:
  author: Li Junhao
  version: "0.0.1"
  category: x-cmd-extension
  tags: [x-cmd, {topic}]
---
```

---

## 维护指南

### 添加新 Skill 的流程

1. **创建文件**
   ```bash
   touch extensions/{topic}-{subtopic}.SKILL.md
   ```

2. **编写内容**
   - 遵循现有格式（参考 china-acceleration.SKILL.md）
   - 包含：概述、快速开始、详细说明、示例、FAQ

3. **更新主 SKILL.md**
   - 在适当位置添加链接
   - 保持导航清晰

4. **提交更改**
   ```bash
   git add extensions/{topic}-{subtopic}.SKILL.md SKILL.md
   git commit -m "skill: add {topic}-{subtopic} extension"
   ```

### 更新现有 Skill

- 直接编辑 extensions/ 中的文件
- 如影响主入口，同步更新 SKILL.md
- 保持向后兼容（不要删除已有链接）

---

## 设计哲学

### 1. 渐进式披露

```
SKILL.md (概览)
    ↓
extensions/install-x-cmd.SKILL.md (入门)
    ↓
extensions/module-*.SKILL.md (深入)
    ↓
extensions/scenario-*.SKILL.md (实践)
```

用户按需深入，不被信息淹没。

### 2. 单一职责

每个 `.SKILL.md` 文件只解决**一类问题**：
- ✅ `china-acceleration.SKILL.md` —— 只解决中国区加速
- ✅ `module-advise.SKILL.md` —— 只讲 advise 模块
- ❌ 不要混合多个主题

### 3. 独立与统一的平衡

- **统一**：通过主 SKILL.md 入口统一管理
- **独立**：每个子 Skill 可单独使用、独立发布
- **链接**：通过相对路径链接，保持关联

---

## 示例：完整的 Skill 结构

### china-acceleration.SKILL.md 剖析

```markdown
---
# 可选：独立发布时的元数据
name: x-cmd-china-acceleration
parent: x-cmd
---

# 标题（清晰明了）
# China Region Network Acceleration Guide

> 一句话描述：How to configure x-cmd for optimal network access in China region

---

## Quick Detection & Configuration

> 快速开始 - 3 行命令解决问题

```bash
x websrc testcn
x websrc set cn
x apt mirror set tuna
```

---

## Detailed Instructions

> 详细说明 - 分模块、分场景讲解

### System Package Managers

#### APT (Debian/Ubuntu)

```bash
x apt mirror set tuna
```

Available mirrors: `ali`, `tuna`, `bfsu`, `ustc`, `tencent`

---

## Complete Configuration Example

> 完整示例 - 复制即用

```bash
if x websrc testcn; then
    x websrc set cn
    x apt mirror set tuna 2>/dev/null || true
    x npm mirror set ali 2>/dev/null || true
fi
```

---

## Related Links

> 相关链接 - 保持导航

- [x-cmd Official Website](https://www.x-cmd.com)
- [Back to x-cmd Skill](../SKILL.md)
```

---

## 总结

| 层级 | 文件 | 职责 |
|------|------|------|
| 入口 | `SKILL.md` | 核心概述 + 导航 |
| 基础 | `extensions/install-x-cmd.SKILL.md` | 入门必看 |
| 场景 | `extensions/china-acceleration.SKILL.md` | 特定场景 |
| 模块 | `extensions/module-*.SKILL.md` | 模块详解 |
| 开发 | `extensions/dev-*.SKILL.md` | 开发指南 |

**核心原则**：
1. 使用 `extensions/` 目录组织子 Skills
2. 文件后缀统一为 `.SKILL.md`
3. 命名采用 `{topic}-{subtopic}` 长描述格式
4. 每个子 Skill 可独立发布
5. 主 SKILL.md 提供统一入口和导航

---

> 本文档本身也是示例 —— 描述如何组织，同时展示组织方式。
