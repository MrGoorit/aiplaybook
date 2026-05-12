# Cursor Skill 使用说明

本文件说明本项目如何通过 Cursor Skill 触发 AI 协作；与 `ai-agent/` 内规则配合使用。

- 总目录说明见 [`README.md`](./README.md)；执行任务前读哪些文件见 [`INDEX.md`](./INDEX.md)。
- Cursor 实际加载的是项目根目录 **`.cursor/skills/*/SKILL.md`**；本文件内容与入口保持一致，便于在仓库内检索与评审。

## Skill 位置（项目级）

- 所有与本项目相关的 Skill 入口统一放在：`.cursor/skills/`
- Skill 的具体执行规则和流程统一维护在：`ai-agent/` 目录（`rules/`、`goals/`、`templates/`、`logs/` 等）
- 新增或调整 Skill 时：
  - 在 `.cursor/skills/` 下新增或修改对应 `SKILL.md`
  - 同步更新本文件 `ai-agent/SKILL.md`（与入口内容一致，便于检索与评审）
  - 在 `ai-agent/` 中更新相应的规则或模板（如有需要）

## 本项目提供的两个 Skill

- `ai-agent-frontend-task`：前端相关开发任务
- `ai-agent-generic-task`：通用任务（文档、规则、脚本、分析等）

## 前端开发场景示例（以 `web/yes-one-api` 为例）

**需求**：在 `web/yes-one-api/src/api/` 下新增一个接口模块，并在页面中对接调用。

在对话中推荐这样使用：

> 使用 `ai-agent-frontend-task`。  
> 需求：在 `web/yes-one-api/src/api/` 目录新增一个 `channel` 模块，对接以下接口：
> - GET /xxx/yyy：……（描述用途、参数、返回结构）
> - POST /xxx/zzz：……  
> 要求：
> - 风格对齐现有 `web/yes-one-api/src/api/channel.ts` 模块
> - 不修改现有 API 模块，只新增本模块和必要的类型定义

Skill 会自动：

1. 读取 `ai-agent/INDEX.md`、`ai-agent/rules/must-follow.md`、`ai-agent/goals/now.md` 和 `ai-agent/rules/frontend-rules.md`。
2. 先列出“本次改动范围 1-3 条”。
3. 再按最小改动原则实现，并按 `templates/task-log.md` 收尾：**必填**已完成项、未完成项、风险点、验证建议；**有待办时**写「接下来要做的事」，无则写「无」或省略。完成后在 `web/yes-one-api/` 下执行 **`pnpm lint`**，必要时补充 **`pnpm type-check`**。

## 文档/规则维护场景示例

**需求**：补充前端规则文档中的“接口超时时间”约定。

在对话中推荐这样使用：

> 使用 `ai-agent-generic-task`。  
> 需求：在 `ai-agent/rules/frontend-rules.md` 中增加一条关于“接口超时时间与重试策略”的规则：
> - 默认超时时间多少秒
> - 允许/不允许的重试次数
> - 和接口文档不一致时的处理方式  
> 要求：
> - 语气和现有规则保持一致
> - 不修改已有规则，只新增一小节

Skill 会自动：

1. 读取 `ai-agent/INDEX.md`、`ai-agent/rules/must-follow.md`、`ai-agent/goals/now.md`。
2. 先写出改动范围，再给出具体修改方案。
3. 用 `templates/task-log.md` 的结构说明修改了哪些规则、风险点和验证建议；有待办时补充「接下来要做的事」。若本次改动包含 `web/yes-one-api/src/` 等可运行代码，完成后在对应目录执行 **`pnpm [lint|type-check]`** 等项目已有脚本。

## 只需记住的两件事

- 前端相关任务：开头加一句  
  > 使用 `ai-agent-frontend-task` …
- 其它通用任务：开头加一句  
  > 使用 `ai-agent-generic-task` …

其余的“读哪些文件、按什么结构输出结果”，都由 Skill 与 `ai-agent/` 内规则自动约束。
