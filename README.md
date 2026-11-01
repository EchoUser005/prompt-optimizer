# Prompt Optimizer

**把需求写清楚，把提示词改明白。**

用 ICTIO 理清判断逻辑、提炼准确指令，让人和 AI 都容易理解，也方便后续维护。

Prompt engineering & optimization skill for coding agents, including Codex and Claude Code.

[安装](#安装) · [使用](#使用) · [优化技巧](#优化技巧) · [Skill 正文](skills/prompt-optimizer/SKILL.md)

## 安装

需要 Node.js / npx：

```bash
npx skills add EchoUser005/prompt-optimizer --skill prompt-optimizer -g
```

按提示选择 Codex、Claude Code 等工具。`-g` 安装到用户目录；去掉它则安装到当前项目。也可以指定工具：

```bash
npx skills add EchoUser005/prompt-optimizer --skill prompt-optimizer -g -a codex
```

安装方式见 [Skills CLI](https://github.com/vercel-labs/skills/blob/main/docs/commands.md)。本仓库包含纯文本指令与评测参考，无需配置 API Key 或额外服务。

## 使用

提供任务需求或现有提示词，获得可审阅、复制使用的候选稿和关键改动说明。系统接入与发布由使用者按项目安排，效果评测按需开展。

安装后，直接让助手使用 `prompt-optimizer` skill。Codex 可通过 `$prompt-optimizer` 显式调用；各工具的入口以其技能选择器为准。[Codex 使用说明](https://learn.chatgpt.com/docs/build-skills)

**从零开始**

```text
使用 prompt-optimizer skill，帮我写一个从客服对话提取待办的提示词。
只提取用户明确承诺、尚未完成的事项，输出任务、负责人和期限。
先给满足核心需求的初版。
```

**优化表达**

```text
使用 prompt-optimizer skill，优化下面这段提示词，让判断顺序和条件更清楚，表达简洁准确。
保留业务含义和已认可的示例，先在对话里给我看候选全文。
[附现有提示词]
```

**验证效果**

```text
使用 prompt-optimizer skill，对比下面两个版本。
固定案例、模型和参数，分别检查目标改善、遗留错误和新增错误。
[附两个版本、测试输入与实际输出]
```

## 优化技巧

| 技巧 | 解决什么问题 |
| --- | --- |
| 突出功能重点 | 根据人格对话、功能任务或知识问答的目标，确定指令主次。 |
| 理清判断逻辑 | 按依赖组织判断，在分流处明确条件与动作。 |
| 提炼准确表达 | 用准确的动词、对象和条件替换拖沓、含混的要求。 |
| 按职责重排结构 | 用 ICTIO 区分指令、资料、工具、当前输入与输出，安排层级和位置。 |
| 按场景组织示例 | 用无序列表写场景，用引用块展示判断、文风或工具交互。 |

ICTIO 对应 **Instruction、Context、Tools、Input、Output**。按功能需要裁剪；一句能说清任务时保留一句，有先后判断或分流时再展开。

示例采用共同的外层结构，内部按任务保留必要信息：

```markdown
## examples

以下只示范简短、自然的回应语气。

- 对方已经决定结束对话
  > 好，回头聊。
```

few-shot 给出输入和符合任务约束的完整输出，生成任务直接示范成品文案；工具示例区分调用与返回。处理说明归入指令。完整示范见[改写案例](skills/prompt-optimizer/references/rewrite-examples.md)。实际效果需要验证时，沿用[评测方法](skills/prompt-optimizer/references/evaluation.md)。

## 仓库内容

```text
skills/prompt-optimizer/
├── SKILL.md                 功能重点、逻辑、表达、结构与场景示例
└── references/
    ├── rewrite-examples.md  完整改写、场景示例与局部迭代
    └── evaluation.md        案例、评分、对照与归因方法
```

[Skill 正文](skills/prompt-optimizer/SKILL.md) · [完整改写案例](skills/prompt-optimizer/references/rewrite-examples.md) · [评测方法](skills/prompt-optimizer/references/evaluation.md)

## 参与改进

欢迎提交失败案例或改进建议。请附任务目标、脱敏后的输入、现有提示词、实际输出与期望行为；若比较模型效果，再注明模型和关键参数。

修改应针对具体问题，说明改善了什么、仍有什么不足。新增技巧的归属与核对方式见[贡献指南](CONTRIBUTING.md)，优先修正对应位置，保留简单任务的简洁写法。

## 来源与许可

ICTIO 方法来自 [Echo 的原文](https://echouser005.github.io/posts/how-the-ictio-framework-improves-the-maintainability-of-engineered-prompts/)。通用示例与延伸阅读见[完整改写案例](skills/prompt-optimizer/references/rewrite-examples.md)。

[MIT License](LICENSE) · Copyright © 2026 [EchoUser005](https://github.com/EchoUser005)
