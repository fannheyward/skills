# GPT-6 Astra skills 审查与优化

日期：2026-09-14。范围：本仓库的 5 个 skills、目录说明及相关计划。基线：`183761bf95855c7719485ccb1a6c87014433beed`，初始工作区干净。

## 问题与依据

GPT-6 Astra 对 skill 中的限制和冲突更敏感，可能在任务尚未完成时请求确认，也可能扩大测试范围。优化应明确完成条件、澄清边界和验证范围。[官方模型指导](https://developers.openai.com/api/docs/guides/latest-model#prompting-best-practices)

官方建议缩短触发描述，按实际任务读取资料，并重新评估旧模型需要的固定流程。多分支内容适合按需加载；简单 skill 无须增加路由层。[官方 skills 优化文章](https://developers.openai.com/blog/rethinking-skills-and-prompts-for-gpt-6-astra)

Codex 的 `policy.allow_implicit_invocation: false` 禁止隐式调用，保留显式调用。本仓库已有该配置，本次保留全部 `agents/openai.yaml` 和 `disable-model-invocation: true`。[官方 skills 文档](https://learn.chatgpt.com/docs/build-skills#optional-metadata)

以下问题来自静态审查，不代表已测得模型成功率或速度变化。

| Skill | 发现 | 修改决策 |
| --- | --- | --- |
| `optimize-agents-md` | 按动词区分模式，未明示计划确认；所有实质冲突均要求提问 | 明确混合请求与计划确认的处理；先应用优先级，仅将未解决的政策选择交给用户 |
| `ui-find-icon` | 复用已有图标与强制搜索两站存在冲突；小改动也必须构建或测试 | 已有图标满足需求时完成本地核验；新图标搜索保持 Remix 优先与两站比较；按风险选择检查 |
| `de-review` | 引用的 review skill 可能要求额外 setup 或提问；末尾强制重复已通过检查 | 固定审查范围和来源优先级；说明缺失能力；复用同一最终内容的检查结果 |
| `git-push-lease` | 强制语法归一化未说明保留指定 lease 条件；成功的 dry-run 可能被误报为推送完成 | 保留显式 lease 约束；区分预览成功与远端更新成功 |
| `squash-commits` | 初始干净状态被当作稍后 `reset --hard` 的充分依据 | 变更前复核状态；恢复时保留新出现或来源不明的改动 |

## 设计决策与边界

- 保持每个 skill 的单一用途和英文正文。仅修正有证据的冲突、完成条件及操作边界，不复制通用 AGENTS 规则。
- 保留 5 个 skills 的手动调用政策、Git 目标和备份校验、审查范围区分、消融证据要求、Remix 优先和依赖变更限制。
- 采用工作流指令优化，不添加模型选择、reasoning effort 或 API 参数。异步工具和执行中用户指令的处理依赖宿主能力，Markdown 不会启用这些功能。
- 仅修改仓库源文件。不更新全局安装，不提交、不推送，不在本仓库执行被审查的历史重写或推送流程。
- 验证采用 YAML、链接、完整 diff 和有限场景检查。Git 行为示例限于临时仓库；结束后进行独立只读审查。

## 实施与验收

- [x] 获取官方文档并审查 5 个入口、UI 元数据、依赖和既有计划。
- [x] 修改有证据的指令问题，并同步受影响的计划和目录说明。
- [x] 检查 YAML、名称、调用政策、链接和完整差异；对 Git 恢复与 dry-run 做隔离检查。
- [x] 完成独立审查所需的文件、来源与验证证据；独立验收结论见最终交付，若发现问题则修正后再次送审。

完成条件：5 个 skills 的用途与调用限制保持一致；澄清只阻塞依赖答案的工作；只读要求优先；通过的检查不因固定流程重复；Git 恢复不丢弃来源不明的改动；最终报告区分静态检查、隔离 Git 检查与模型行为评估。

## 风险与回退

减少流程约束可能丢失安全条件，因此保留 Git 备份、目标解析、tree 校验和非快进拒绝边界。新增保护可能导致恢复暂停，此时应报告状态和备份位置，保留用户改动。任何回退只撤销本次修改，保留后续用户工作。

## 验证结果

- 5 个 skills 的 YAML、目录与名称、默认调用提示和两处手动调用限制均通过检查。全部 `agents/openai.yaml` 与基线逐字节一致。
- 官方 `quick_validate.py` 对原文件报告不识别 `disable-model-invocation`。保留该字段并单独解析断言，在临时副本中仅移除该字段后，5 个 skills 均通过官方校验。
- 14 个本地 Markdown 链接可解析；`git diff --check` 通过；Git index 保持不变。
- 临时 Git 仓库的 7 个场景通过：rebase 后 squash 的提交数量、父提交和 tree 保持；无新改动的提交失败后恢复；hook 写入后检测并保留改动与备份；工作区干净但 HEAD 出现新提交时保留该提交；dry-run 返回成功但不更新本地裸仓库；过期的显式 lease 拒绝更新；匹配的显式 lease 允许指定强制更新。
- Git 场景由主代理按文档执行，用于确认命令语义及状态边界，不是模型端到端调用评估。独立 reviewer 的结果在最终交付中报告。
- 未运行付费模型 A/B、真实远端推送、全局 skill 安装或项目构建。本次没有 API 应用或编译代码变更，不能据此声称模型成功率或耗时改善。

## 相关文件

- [de-review](../../skills/de-review/SKILL.md)
- [git-push-lease](../../skills/git-push-lease/SKILL.md)
- [optimize-agents-md](../../skills/optimize-agents-md/SKILL.md)
- [squash-commits](../../skills/squash-commits/SKILL.md)
- [ui-find-icon](../../skills/ui-find-icon/SKILL.md)
- [目录](../../README.md)
