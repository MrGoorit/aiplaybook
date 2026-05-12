## Skill: ai-agent-frontend-task

本 Skill 用于本仓库的前端开发任务，默认面向 `web/yes-one-api`（Vue3 + Vite + Element Plus + UnoCSS）等前端子项目。

### 会自动读取的文件

- `ai-agent/INDEX.md`
- `ai-agent/rules/must-follow.md`
- `ai-agent/goals/now.md`
- `ai-agent/rules/frontend-rules.md`

### 执行流程（简要）

1. 根据本次对话描述，先列出「本次改动范围（1–3 条）」。
2. 在确认范围内，按最小改动原则实现前端改动：
   - 优先复用已有组件、样式、工具方法
   - 接口调用统一通过对应子项目下的 `src/api/**`，在 `web/yes-one-api` 中使用 `src/api/request.ts` 封装的 `request`
3. 修改完成后，给出需要执行的校验命令：在 `web/yes-one-api/` 下运行 **`pnpm lint`**，必要时补充 **`pnpm type-check`**，说明预期无误后再宣称完成。
4. 按 `ai-agent/templates/task-log.md` 的结构收尾说明：
   - 已完成项
   - 未完成项
   - 风险点
   - 验证建议
   - 若有需后续跟进的内容，加上「接下来要做的事」，否则写「无」或省略该小节。

### 触发示例

> 使用 `ai-agent-frontend-task`。  
> 需求：在 `web/yes-one-api/src/views/User/index.vue` 中增加邮箱搜索能力，接口沿用 `web/yes-one-api/src/api/user.ts`，不改动分页逻辑。

