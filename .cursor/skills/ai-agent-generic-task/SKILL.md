## Skill: ai-agent-generic-task

本 Skill 用于通用任务（文档、规则、脚本、分析等），不限定具体技术栈。

### 会自动读取的文件

- `ai-agent/INDEX.md`
- `ai-agent/rules/must-follow.md`
- `ai-agent/goals/now.md`

### 执行流程（简要）

1. 先根据本次对话内容，写出「本次改动范围（1–3 条）」。
2. 在确认范围内，按最小改动原则修改或补充文档 / 规则 / 脚本：
   - 严格遵守 `ai-agent/rules/must-follow.md`
   - 不随意扩散改动到无关目录
3. 若涉及可运行代码（如脚本、前端实现），给出需要执行的校验命令说明；对 `web/yes-one-api/` 默认 **`pnpm lint`**，必要时 **`pnpm type-check`**。
4. 按 `ai-agent/templates/task-log.md` 的结构收尾说明：
   - 已完成项
   - 未完成项
   - 风险点
   - 验证建议
   - 若有需后续跟进的内容，加上「接下来要做的事」，否则写「无」或省略该小节。

### 触发示例

> 使用 `ai-agent-generic-task`。  
> 需求：在 `ai-agent/rules/frontend-rules.md` 中增加一条说明「本仓库 Vue 前端统一通过 `web/yes-one-api/src/api/request.ts` 调用接口」的规则，语气与现有规则保持一致。

