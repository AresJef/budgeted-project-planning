# budgeted-project-planning

把代码开发、重构、优化或续接项目拆成可验收步骤，在用户确定的总时间预算内规划和推进。每步设置预算，首次超时在安全边界自查；可调整阶段软目标，保留原预算、真实用时和有效证据。

正文使用“用户 / 规划 Agent / 执行 Agent”，不依赖特定模型、宿主、连接器或自动计时工具。两种 Agent 职责可由同一 Agent 承担。完整执行规则以 [SKILL.md](SKILL.md) 和相应 references 为准。

## 适用范围与授权

- 适用：制定项目计划、预算分步交付、在已授权实施中处理超时、验收和恢复，或根据已有记录续接项目。
- 完整项目采用固定验收权重和唯一台账；单文件小修复可使用短记录，仍保留步骤、每步预算、验收和超时自查。
- 用户控制总预算和核心取舍。总预算、必要验收、阶段硬上限及实施授权不能因安装或调用 Skill 自动增加。
- 仅阅读、评估、修改或制作模板不会启动开发项目。只有规划授权时交付计划；已有实施授权和明确预算时沿用授权推进。

## 包结构

```text
budgeted-project-planning/
├── SKILL.md
├── README.md
├── LICENSE
├── agents/
│   └── openai.yaml
└── references/
    ├── planning-and-decisions.md
    ├── budget-and-overrun.md
    ├── validation-and-evidence.md
    └── records-and-delivery.md
```

四份引用分别提供 [步骤和核心决策](references/planning-and-decisions.md)、[预算与超时处理](references/budget-and-overrun.md)、[验证与证据](references/validation-and-evidence.md)、[台账、恢复与交付](references/records-and-delivery.md)。按任务阶段读取，保留文件层次和相对链接。

[agents/openai.yaml](agents/openai.yaml) 是可选的 OpenAI UI 元数据，只提供名称、简介和调用提示。其他宿主可忽略或不安装该文件；正文和 references 不依赖它。安装核心须完整包含 SKILL.md 与四份 references，分发时保留 README 和 LICENSE。

## 本地安装

先核对目标宿主实际支持的用户级或项目级 Skill 目录及发现方式，再复制整个包到其中的独立 `budgeted-project-planning/` 目录。不要只复制 SKILL.md，也不要把本目录或某个示例路径直接视为所有宿主的安装位置。

可将以下请求交给支持本地 Skill 的 Agent：

```text
请从我提供的 budgeted-project-planning 完整包安装此 Skill。
先核实当前宿主支持的 Skill 安装位置和我指定的用户级或项目级范围。
完整复制 SKILL.md、references/、README.md 和 LICENSE，保留目录层次。
OpenAI 宿主可同时保留可选的 agents/openai.yaml；其他宿主按其支持情况处理。
若存在同名目录或 Skill，先只读比较来源和差异，不覆盖我的修改。
安装后检查格式、相对引用、发现结果，并做一次仅文本的显式调用验证。
安装和验证不授予项目实施权限。
```

安装后确认 frontmatter 中的 `name: budgeted-project-planning`、四份 references 和全部相对引用有效，并确认宿主发现了实际安装的文件。宿主未发现时按其真实刷新或加载方式处理；文件复制成功不等于已经加载。

## 使用示例

在支持 `$skill-name` 的宿主中可以显式调用；其他宿主使用其实际调用方式或明确指定已安装的 SKILL.md。

仅规划：

```text
使用 $budgeted-project-planning，为这个重构项目制定可执行的分步计划。
总预算 90 分钟，本次只授权规划；已有资料和冻结参考见项目目录。
请列出各步交付、原定预算、验收证据、依赖和下一动作，并集中提出必要核心问题。
```

沿用既有授权和记录：

```text
使用 $budgeted-project-planning，依据现有计划和唯一台账续接项目。
已有实施授权不变，保留原 T0、计时口径、暂停区间、累计用时和原步骤预算。
核实当前成果与证据后，按剩余总预算推进；未决核心问题只阻塞受影响步骤。
```

示例中的 90 分钟仅是示例输入，不是默认总预算。用户未给出完整总预算时，Skill 会先询问，不把截止时刻或新会话当作预算重置。

## 更新与冲突

记录来源、所选版本和实际安装目录。更新前比较用户修改和新包，保留需要保存的内容，在有覆盖授权后替换完整包，避免新入口混用旧 references。更新后重新核验引用和宿主发现。同名副本不自动合并，不静默覆盖或删除其他位置的 Skill。

## 手动发布到 GitHub

本目录可直接作为独立仓库根目录，SKILL.md 与 README.md、LICENSE 同级。建议仓库名为 `budgeted-project-planning`；用户可自行选择账号、可见性和版本标记。本包的制作不代表远程仓库已创建或发布。

1. 自行在 GitHub 创建仓库，避免额外生成冲突的 README 或许可证。
2. 将本目录全部八个文件上传到仓库根，保留 `references/` 和 `agents/` 子目录，不额外套一层同名目录。
3. 发布后用实际仓库 URL 和所选版本交给目标宿主安装器，明确根路径为 `.`、安装名称为 `budgeted-project-planning`，安装完整包并完成发现与文本调用验证。

可使用以下请求，替换占位信息后再发送：

```text
请用当前宿主支持的 Skill 安装方式，从 <实际 GitHub 仓库 URL>
安装仓库根目录的 budgeted-project-planning，根路径为 .。
使用 <选定提交或标签>，先核实实际安装位置，完整获取核心文件和 references。
保留 README、LICENSE；agents/openai.yaml 是可选的 OpenAI 元数据。
同名冲突先只读比较，不覆盖用户内容。验证加载，不启动项目实施。
```

## 来源、许可与验证边界

唯一内容基线：用户定稿《项目开发规划3-修订稿.md》版本 3，34,256 字节。
基线 SHA-256：`8ed08faa94a5a87fdd13c02b40b6de708e99a128b07b76536e4446fb22c5dd4b`。

采用 [MIT License](LICENSE)，版权为 `Copyright (c) 2026 AresJef`。

本包的格式、引用、原文覆盖和隔离文本情境检查不能证明远程仓库可访问、目标宿主已经安装或自动计时及后台续接可用。实际远程获取与发现、各宿主加载和真实项目效果须在对应环境验证。内部覆盖映射和检查报告保留于制作任务工作区，不属于发布包。
