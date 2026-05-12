# 执行记录：QLY 回放交互加固

## 任务信息

- 任务标题：视频回放防抖与禁点反馈优化
- 执行人（小助手）：AI Assistant
- 执行日期：2026-03-31

## 接下来要做的事

- 在 `QlyPlaybackButton.vue` 中将 `videoLoading` 下发给 `VideoProgressBar.vue`，统一控制时间轴可点击状态。
- 在 `VideoProgressBar.vue` 中增加加载中禁点逻辑，并在禁点阶段提供清晰交互反馈。
- 串行化回放请求流程，确保 `stop -> start -> 冷却 3 秒 -> 解锁`。

## 已完成项

- 已完成父子组件联动：`QlyPlaybackButton.vue` 向 `VideoProgressBar.vue` 传入 `videoLoading`。
- 已完成时间轴禁点控制：`videoLoading=true` 时点击拦截并提示“回放资源加载中，请稍后再试”。
- 已完成请求顺序加固：在回放切换中执行 `await stopRecord()` 后再 `await getBackVideoUrl()`。
- 已完成冷却窗口：`start` 请求完成后继续等待 3 秒，再解除交互锁。
- 已完成并发保护：通过请求序列号仅允许最后一次请求解除 `videoLoading`。
- 已完成视觉反馈优化：禁点期间时间轴与录像片段光标显示 `cursor-not-allowed`，恢复后显示 `cursor-pointer`。
- 已执行校验命令：`pnpm run lint:eslint`，结果通过。

## 未完成项

- 无。

## 风险点

- 3 秒冷却会降低连续点选响应速度，属于策略性取舍，需业务确认体验预期。

## 验证建议

- 打开回放后快速连续点击 10 次以上，确认加载期间不重复触发请求。
- 观察请求顺序，确保先 `stop` 再 `start`，且完成后至少 3 秒才允许下一次有效点击。
- 在无录像区域点击，确认仅提示“此处无录像数据”，不触发回放请求。
- 在禁点阶段悬停时间轴与录像片段，确认光标为 `cursor-not-allowed`。

## 备注（可选）

- 建议后续将同类“交互节流 + 请求串行 + UI 状态锁”的模式沉淀到 `patterns/` 目录，形成可复用方案。
