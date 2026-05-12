# AI Agent 阅读入口

用于告诉小助手“本次必须读什么”，避免每次全量读取文档。

完整目录含义、快速导航表见 [`README.md`](./README.md)。若仓库内另有产品经理专用 `ai-agent-pm/`，可与之配合使用（本仓库未包含时可忽略）。

## 必读（每次任务开始前）

1. `rules/must-follow.md`
2. `goals/now.md`

## 按需读取

- 需要总览或查文件含义：`README.md`
- 需要新开任务：`templates/new-task.md`
- 需要记录执行：`templates/task-log.md`
- 需要确认命名：`README.md` 中「命名规范」
- 需要前端开发注意事项：`rules/frontend-rules.md`
- 需要复盘经验：`logs/` 下最近 3 份记录
- 需要 Cursor Skill 对话示例：[`SKILL.md`](./SKILL.md)
- 需要按条保存对话指令、少打字：`queued-tasks.md`

## 执行策略

- 默认最小改动，不跨目录重构。
- 先列“本次改动范围（1-3 条）”再动代码。
- 完成后按 `templates/task-log.md` 组织回复：**必填**已完成项、未完成项、风险点、验证建议；**有待办时**补充「接下来要做的事」，无则写「无」或省略该小节。

## 快速决策（选哪个 Skill）

在对话开头写明使用的 Skill id，便于 Cursor 加载对应入口（详见 [`SKILL.md`](./SKILL.md)）。

- 涉及 Vue 组件、样式、表单、接口联调、交互优化：使用 **`ai-agent-frontend-task`**
- 文档整理、规则维护、通用实现、分析任务：使用 **`ai-agent-generic-task`**

## 维护本文件时

在 `rules/` 下新增专题规则文件（如 `xxx-rules.md`）时，将对应项加入上文「按需读取」，并控制条目数量；专题过多时可在 `README.md` 用表格汇总，INDEX 只保留高频入口。
