# ICTIO Prompt Skill

用 ICTIO 组织提示词，按当前阶段完成初始化、定向优化和效果评测。

[安装](#安装) · [使用](#使用) · [工作方式](#工作方式) · [Skill 正文](skills/prompt/SKILL.md)

## 安装

需要 Node.js / npx：

```bash
npx skills add EchoUser005/ictio-prompt-skill --skill prompt -g
```

按提示选择 Codex、Claude Code 等工具。`-g` 安装到用户目录；去掉它则安装到当前项目。也可以指定工具：

```bash
npx skills add EchoUser005/ictio-prompt-skill --skill prompt -g -a codex
```

安装方式见 [Skills CLI](https://github.com/vercel-labs/skills/blob/main/docs/commands.md)。本仓库包含纯文本指令与评测参考，无需配置 API Key 或额外服务。

## 使用

安装后，直接让助手使用 `prompt` skill，并提供任务需求或现有提示词。Codex 可通过 `$prompt` 显式调用；各工具的入口以其技能选择器为准。[Codex 使用说明](https://learn.chatgpt.com/docs/build-skills)

**从零开始**

```text
使用 prompt skill，帮我写一个从客服对话提取待办的提示词。
只提取用户明确承诺、尚未完成的事项，输出任务、负责人和期限。
先给满足核心需求的初版。
```

**优化表达**

```text
使用 prompt skill，整理下面这段提示词。
保留业务判断顺序和已认可的示例，把拖沓的要求提炼成明确指令。
[附现有提示词]
```

**验证效果**

```text
使用 prompt skill，对比下面两个版本。
固定案例、模型和参数，分别检查目标改善、遗留错误和新增错误。
[附两个版本、测试输入与实际输出]
```

## 工作方式

| 当前阶段 | Skill 做什么 |
| --- | --- |
| 初始化 | 明确任务类型和核心规则，选择必要的 ICTIO 要素，写最小可用初稿。 |
| 定向优化 | 定位表达、逻辑、上下文或模型表现的问题，修改相关部分。 |
| 验证与沉淀 | 核对实际输入与评分口径，通过受控对照验证变化，保留下一轮基线。 |

ICTIO 对应 **Instruction、Context、Tools、Input、Output**。按任务需要组合；一句 goal 能说清，就保留一句，需要先后判断或条件分流时再展开 workflow。

例如，业务已经明确“唯一订单直接查询，多笔订单需要区分”：

| 原表述 | 提炼后 |
| --- | --- |
| 充分理解用户需求，结合上下文灵活处理，必要时追问，确保查询准确。 | 根据当前请求与已有信息定位订单：唯一匹配时查询；匹配多个时，只追问用于区分订单的信息。 |

提炼保留判断依据与分支，删除不改变行为的铺垫。实际效果是否改善，再用对应案例验证。

## 仓库内容

```text
skills/prompt/
├── SKILL.md                 阶段判断、ICTIO 选用与指令提炼
└── references/
    └── evaluation.md        案例、评分、对照与归因方法
```

[Skill 正文](skills/prompt/SKILL.md) · [评测方法](skills/prompt/references/evaluation.md)

## 参与改进

欢迎提交失败案例或改进建议。请附任务目标、脱敏后的输入、现有提示词、实际输出与期望行为；若比较模型效果，再注明模型和关键参数。

修改应针对可复现的问题，说明改善了什么、仍有什么不足。优先保留简单任务的简洁写法。

## 来源与许可

ICTIO 方法来自 [Echo 的原文](https://echouser005.github.io/posts/how-the-ictio-framework-improves-the-maintainability-of-engineered-prompts/)。提示词与评测参考见 [SKILL.md](skills/prompt/SKILL.md#参照)。

[MIT License](LICENSE) · Copyright © 2026 [EchoUser005](https://github.com/EchoUser005)
