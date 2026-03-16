# session-handoff

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill for seamless session handoff between AI conversations.

一个 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 技能，用于在 AI 对话之间无缝交接工作上下文。

## Why / 为什么需要

When using Codex / Claude Code / Gemini CLI for complex tasks, long conversations lead to increasing hallucinations and degraded problem-solving. The fix is starting a fresh session — but context is lost.

使用 Codex / Claude Code / Gemini CLI 处理复杂任务时，对话越长，AI 的幻觉越多，解决问题的能力越差。解决办法是开新会话——但上下文会丢失。

This skill generates a structured handoff document so the next AI agent can pick up exactly where the last one left off.

这个技能会生成一份结构化的交接文档，让下一个 AI 能从断点处精确接续工作。

## Install / 安装

### Option A: Plugin install (recommended) / 插件安装（推荐）

In Claude Code, run:

在 Claude Code 中执行：

```
/plugin marketplace add james20141606/session-handoff
/plugin install session-handoff@session-handoff-marketplace
```

Then use with:

安装后使用：

```
/session-handoff:session-handoff
```

### Option B: One-liner from GitHub / 一行命令安装

```bash
# Global install (all projects) / 全局安装（所有项目生效）
git clone https://github.com/james20141606/session-handoff.git /tmp/session-handoff && mkdir -p ~/.claude/skills/session-handoff && cp /tmp/session-handoff/SKILL.md ~/.claude/skills/session-handoff/ && rm -rf /tmp/session-handoff

# Or project-level install / 或项目级安装（仅当前项目生效）
git clone https://github.com/james20141606/session-handoff.git /tmp/session-handoff && mkdir -p .claude/skills/session-handoff && cp /tmp/session-handoff/SKILL.md .claude/skills/session-handoff/ && rm -rf /tmp/session-handoff
```

### Option C: Manual / 手动安装

```bash
git clone https://github.com/james20141606/session-handoff.git
mkdir -p ~/.claude/skills/session-handoff
cp session-handoff/SKILL.md ~/.claude/skills/session-handoff/
```

### Option D: Just copy the file / 直接复制文件

You only need one file: [`SKILL.md`](./SKILL.md). Download or copy it to:

你只需要一个文件：[`SKILL.md`](./SKILL.md)。下载或复制到：

```
~/.claude/skills/session-handoff/SKILL.md    # global / 全局
.claude/skills/session-handoff/SKILL.md      # project / 项目级
```

No restart needed — Claude Code picks up new skills automatically.

无需重启，Claude Code 会自动发现新技能。

## Usage / 使用方法

### Step 1: End the old session / 结束旧会话

Say any of these in your current conversation:

在当前对话中说以下任意关键词：

| Trigger / 触发词 | Type / 类型 |
|---|---|
| `/session-handoff` | slash command |
| `handoff` / `session handoff` | English keyword |
| `交接` / `工作交接` / `写交接文档` | 中文关键词 |
| `开新会话` / `new session` / `context too long` | 场景描述 |

The AI generates `./YYMMDD-handoff.md` with 7 sections:

AI 会生成 `./YYMMDD-handoff.md`，包含 7 个章节：

1. **Current Task Objective / 当前任务目标**
2. **Current Progress / 当前进展**
3. **Key Context / 关键上下文** — background, constraints, decisions / 背景、约束、已做决定
4. **Key Findings / 关键发现**
5. **Unfinished Items / 未完成事项** — prioritized / 按优先级排序
6. **Recommended Handoff Path / 建议接手路径** — what to check, what to verify / 该看什么、该验证什么
7. **Risks and Caveats / 风险与注意事项** — dead ends and pitfalls / 已验证的死路和容易踩的坑
8. **First Step for the Next Agent / 下一步建议** — one concrete action / 一个具体可执行的动作

### Step 2: Start the new session / 开始新会话

The skill outputs a ready-to-paste prompt. Copy it into your new session:

技能会输出一段可以直接复制的 prompt，粘贴到新会话即可：

```
Read ./260316-handoff.md — this is a handoff document from a previous session.
Follow the "First Step for the Next Agent" section and continue the work described in it.
```

The new AI reads the file and continues from where you left off.

新的 AI 会读取文件并从你上次离开的地方继续工作。

## How it works / 工作原理

```
Old session / 旧会话                New session / 新会话
┌──────────────┐                   ┌──────────────┐
│ Long context  │──"handoff"──►   │ Fresh start   │
│ + hallucinate │  generates      │               │
│               │  handoff.md     │  reads file   │
│               │  ──────────►    │  continues    │
└──────────────┘                   └──────────────┘
```

## Compatibility / 兼容性

Works with any AI coding assistant that supports skill/prompt loading:

适用于任何支持技能/提示加载的 AI 编程助手：

- **Claude Code** — native skill/plugin support / 原生技能和插件支持
- **Gemini CLI** — copy the prompt template from SKILL.md / 复制 SKILL.md 中的提示模板
- **Codex CLI** — copy the prompt template from SKILL.md / 复制 SKILL.md 中的提示模板
- **Cursor / Windsurf / other** — add as a custom prompt or rule / 作为自定义提示或规则添加

## License

MIT
