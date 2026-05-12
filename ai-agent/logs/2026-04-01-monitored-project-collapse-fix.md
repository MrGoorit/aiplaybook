# 任务记录：修复 monitored-project 详情弹窗 el-collapse-item 默认展开问题

> 按 `task-log.md` 模板记录。

## 任务信息

- 任务标题：产品反馈，打开 monitored-project 的项目详情弹窗，并且点击了除项目信息以外的 el-tab，之后再打开其他的，本来默认展开的所有 el-collapse-item 都不会默认展开了，帮我修复成自动展开所有 el-collapse-item
- 执行人（小助手）：GitHub Copilot
- 执行日期：2026-04-01

## 已完成项

- 分析问题：`ProjectInfoTabItem.vue` 中缺少 `showAllCollapse` 方法，导致 `DetailModal.vue` 中调用时无法展开 collapse。
- 添加 `showAllCollapse` 方法：设置 `collapseNameList.value = Object.keys(pCollapseNameInfo);` 以展开所有 collapse-item。
- 运行 ESLint 检查，无语法错误（有 TypeScript 版本警告，不影响功能）。

## 未完成项

- 无

## 风险点

- 如果 `pCollapseNameInfo` 键值变化，需要同步更新方法。
- 确保在弹窗打开时正确调用该方法。

## 验证建议

- 打开项目详情弹窗，检查 base tab 的 collapse 是否默认展开。
- 切换到其他 tab，再打开新弹窗，验证 base tab collapse 仍默认展开。