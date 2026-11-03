# Prompt Optimizer

**把业务需求写清楚，让每一句提示词都对结果有用。**

一个面向工程化提示词的开源 Agent Skill。把需求或已有 Prompt 交给 Codex、Claude Code 等 coding agent，它会帮你理清判断逻辑、精炼指令、整理完整示例，交付可以直接试用、方便持续修改的提示词。你不需要先学提示词工程。

Prompt engineering & optimization for AI products: concise instructions, clear business logic, and maintainable prompts.

[谁适合用](#谁适合用) · [解决什么问题](#解决什么问题) · [快速开始](#快速开始) · [优化方法](#优化方法) · [反馈与迭代](#反馈与迭代)

## 谁适合用

- **开发或维护 AI 功能的开发者、创业者**：产品里已有对话角色、知识问答、内容生成或信息提取，需要提示词反复调用、持续迭代。
- **懂业务、正在接入 AI 的产品与行业团队**：知道想要什么结果，却总在和 Agent 来回改稿，规则越补越多，效果仍不稳定。
- **做垂直领域模型、端侧 AI 或设备应用的人**：关心算力、响应时间和调用成本，需要把领域要求表达准确，减少无效指令。

这个 Skill 装在帮你写提示词的 Agent 里；产出的提示词，再放到你自己的 AI 功能和目标模型中测试、使用。

## 解决什么问题

提示词会被反复调用。多余的文字会占用上下文，含混的规则会让模型自行猜测，层层追加的要求也会让下一次修改更困难。

| 你关心的问题 | Prompt Optimizer 怎么处理 |
| --- | --- |
| **调用成本与响应速度** | 删去重复、空泛和不改变行为的指令，减少每次请求的无效 token；保留必要的依据、条件和示例，让提示词的长度服务于任务。 |
| **输出稳定性** | 理清先判断什么、依据什么、不同情况如何处理；用符合任务要求的完整输入输出示例对齐标准，减少让模型猜业务规则的空间。 |
| **迭代与维护** | 把目标、资料、判断和输出约定放到清楚的位置，保留已有变量与接口要求。需求变化时能找到该改的地方，局部修改也能保留已经有效的内容。 |

它追求的是精炼、准确、能执行的表达。一句话能交代清楚的任务，就保留一句；需要流程和示例时，再把它们写完整。

## 快速开始

### 1. 安装到你的 Agent

使用 [Skills CLI](https://github.com/vercel-labs/skills/blob/main/docs/commands.md)，需要 [Node.js 22.20 或更新版本](https://github.com/vercel-labs/skills#install-a-skill)：

```bash
npx skills add EchoUser005/prompt-optimizer --skill prompt-optimizer -g
```

按提示选择 Codex、Claude Code 等工具。`-g` 安装到用户目录，跨项目使用；去掉它则安装到当前项目。只安装到 Codex 可以在命令后加 `-a codex`。

Skill 本身是纯文本指令和参考材料，无需额外配置 API Key 或服务，沿用你已有的 Agent 和模型环境。也可以通过 [Agensi 上架页](https://www.agensi.io/skills/prompt-optimizer-ictio-prompt-engineering)按平台说明使用，目前免费。

### 2. 复制这段话给 Agent

```text
用 prompt-optimizer 帮我优化下面这段提示词。
保留我的业务要求，有会影响结果的歧义再问我。
给我一版可以直接试用的完整提示词，并简短说明改了什么。

[粘贴你的提示词]
```

还没有提示词，就直接提供需求，让 Agent 用这个 Skill 写满足核心需求的初版。已有具体问题时，一起附上脱敏的输入、实际输出和期望结果；只想改某一处，也可以直接说明范围。

**你会拿到完整候选稿和关键改动说明。** 如果某项业务规则尚未明确，Agent 会指出需要确认的地方。系统接入与发布按你的项目安排。

### 3. 放回自己的任务里试

用相同的输入分别试原稿和改稿，看业务结果是否更符合预期；关心性能时，再对照实际 token 用量、调用成本和响应时间。

开始使用不需要先搭建自动评测系统。需要进一步验证时，再让 Agent 按[评测方法](skills/prompt-optimizer/references/evaluation.md)固定案例、模型和参数做对照，检查目标改善、遗留错误和新增错误。字数减少、排版整齐都不能单独证明效果改善。

## 优化方法

这套 Skill 整理自实际项目中的提示词调优经验，重点是把用户已经掌握的业务要求转成模型能执行的指令。

- **先确定功能重点。** 对话人格、功能任务和知识问答的重点不同，按当前需求决定主次，不强行套同一份长模板。
- **先理清逻辑，再精炼表达。** 写清依据、条件、动作与边界，删除同义重复和空泛铺垫，保留原有例外与适用范围。
- **按职责组织内容。** 用 ICTIO 区分 Instruction、Context、Tools、Input、Output，按任务裁剪章节，把关键要求放在容易找到的位置。
- **用完整示例对齐标准。** few-shot 给实际输入和符合要求的完整输出；示例里的“处理思路”不能替代模型最终要交付的结果。

具体写法见 [Skill 正文](skills/prompt-optimizer/SKILL.md)；需要前后对照时，查看[完整改写案例](skills/prompt-optimizer/references/rewrite-examples.md)。

## 反馈与迭代

目前是初版，会根据实际使用中的问题持续改进。不同模型、行业和设备条件下，仍会有需要补充的场景，欢迎通过 [Issue](https://github.com/EchoUser005/prompt-optimizer/issues)反馈。

请去掉敏感信息，附上任务目标、现有提示词、测试输入、实际输出与期望行为。若涉及成本、速度或稳定性，再注明模型、关键参数和可复现的对照结果。

新增技巧会放到对应的逻辑、表达、结构或示例位置，评测方法单独维护，避免每次发现问题就给 Skill 追加一层规则。参与修改请看[贡献指南](CONTRIBUTING.md)。

## 仓库内容

```text
skills/prompt-optimizer/
├── SKILL.md                 功能重点、逻辑、表达、结构与场景示例
└── references/
    ├── rewrite-examples.md  完整改写、场景示例与局部迭代
    └── evaluation.md        案例、评分、对照与归因方法
```

## 来源与许可

ICTIO 方法来自 [Echo 的原文](https://echouser005.github.io/posts/how-the-ictio-framework-improves-the-maintainability-of-engineered-prompts/)。

[MIT License](LICENSE) · Copyright © 2026 [EchoUser005](https://github.com/EchoUser005)
