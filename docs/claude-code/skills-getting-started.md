# Claude Code 社区技能（Skills）上手指南

## Skills 是什么？

Skills 本质上是带 `SKILL.md` 规则文件的文件夹，告诉 AI **在什么场景下、按什么流程做事**。比如 `brainstorming` 技能会强制 AI 在动手写代码前先问清楚需求、提出方案供用户选择。

截至 2026 年 2 月，Claude Code 插件生态已有超过 **1300 个技能** 嵌入在 **313 个插件** 中。

### Skills vs Plugins

| 类型 | 说明 |
|---|---|
| **Skill** | 一个带 `SKILL.md` 规则说明的文件夹，相对轻量 |
| **Plugin** | 功能更完整，可包含命令、子代理（Agents）、钩子（Hooks）等 |

---

## 必装技能 Top 4

### 1. Superpowers（开发方法论全家桶）

- **作者**：Jesse Vincent (`obra`)
- **GitHub**：https://github.com/obra/superpowers （22700+ Star）
- **包含子技能**：`brainstorming`、`writing-plans`、`executing-plans`、`test-driven-development`、`systematic-debugging`、`verification-before-completion`、`subagent-driven-development` 等 20+ 个
- **安装命令**：

```bash
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace
```

### 2. skill-creator（Anthropic 官方——自创技能）

- **GitHub**：https://github.com/anthropics/skills
- **用途**：分析工作流、沉淀个人经验为可复用技能
- **安装命令**：

```bash
npx skills add anthropics/skills@skill-creator -g -y
```

### 3. find-skills（Vercel 出品——技能搜索引擎）

- **用途**：搜索社区技能，找合适的直接安装
- **安装命令**：

```bash
claude install-skill https://github.com/vercel-labs/skills
```

### 4. everything-claude-code（一站式全能插件）

- **用途**：单插件替换 20+ 独立技能，包含 `/plan`、`/tdd`、代码审查、安全审查、构建错误修复等
- **安装命令**：

```bash
claude plugin add everything-claude-code
```

---

## brainstorming 技能详解

这是 Superpowers 中最受推崇的技能，**强制 AI 在动手前先思考**：

| 步骤 | 说明 |
|---|---|
| 1. 探索项目上下文 | 检查文件、文档、最近提交 |
| 2. 逐个提问 | 一次一个问题，了解目的 / 约束 / 成功标准 |
| 3. 提出 2-3 种方案 | 附权衡分析和推荐 |
| 4. 展示设计 | 按模块逐步确认 |
| 5. 输出设计文档 | 存入 `docs/superpowers/specs/` |
| 6. 过渡到实施计划 | 自动调用 `writing-plans` |

> **铁律**：哪怕需求再简单，也必须走完流程 —— 越简单的需求越容易因跳过设计而踩坑。

---

## 四种安装方式对比

| 场景 | 推荐方式 | 命令示例 |
|---|---|---|
| 安装 Superpowers 全套 | 插件市场 | `/plugin install superpowers@superpowers-marketplace` |
| 只装单个技能 | `npx skills add` | `npx skills add <url> --skill <name> -g -y` |
| 同事给的 .zip 包 | `npx skills add` | `npx skills add ~/Downloads/xxx.zip -g -y` |
| 团队共享定制技能 | 手动复制到项目 | 放入 `.claude/skills/` 并提交 Git |

---

## 推荐渐进上手路线

| 阶段 | 做什么 | 目的 |
|---|---|---|
| **今天** | 先装 Superpowers，体验 `brainstorming` | 感受"AI 先问再动手"的工作流 |
| **一周后** | 装 skill-creator，把你最重复的一个工作流写成技能 | 形成个人工具积累 |
| **按需** | 用 find-skills 搜特定场景的技能 | 补足特定需求 |

---

## 不想装全套 Superpowers？只装一个技能也可以

```bash
npx skills add <技能地址> --skill <技能名> -g -y
```

---

## 使用心法

1. **循序渐进**：不要一次性安装所有技能，按"基础执行 → 常用自动化 → 体验优化"分批来
2. **描述即触发器**：`SKILL.md` 的 `description` 字段是给 AI 看的"触发信号"，必须明确使用场景
3. **skill-creator 设计原则**：渐进式披露、自由度匹配、最小化冗余、可验证性
4. **常见坑**：注意 Token 消耗、避免功能重叠导致技能冲突、务必先调查根因再修复（systematic-debugging 铁律）

---

> 整理日期：2026-05-27
