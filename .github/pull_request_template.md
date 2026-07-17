<!--
Retaintive organization-wide PR contract

目标：让 reviewer 快速判断改动范围、动机、正确性、风险以及上线和回滚方式。

写作规则：
- PR description 是 reviewer briefing，不是逐文件 diff。
- 内容长度和结构服从改动复杂度；写到 reviewer 能做出判断为止。
- Core sections 必须完成；不适用时说明原因。
- Conditional modules 只在相关时启用，不要保留空 section。
- Review 导致实现发生实质变化后，更新 PR body，不只依赖 commit history。
-->

## 摘要

<!--
先给 reviewer 结论，并根据改动复杂度充分说明：
- 最终结果
- 影响的用户、系统或 repository surface
- 是否改变 production behavior
- 重要的 scope、non-goals 和明确不做的事情

复杂 PR 可以使用多段文字、列表或表格；不要为了追求简短而丢失 reviewer 判断所需的信息。
避免逐文件复述 diff，具体设计和实现细节放在后续 sections。
-->

## 背景 / 为什么

<!--
说明问题、需求或设计背景：
- 之前哪里坏了、缺了什么
- 为什么现在需要修改
- 关联 Issue、incident、spec 或上游 PR
-->

## 改了什么

<!--
按 behavior、component 或 invariant 分组说明，不要逐文件复述 diff。

复杂改动重点写：
- contract / data flow 的变化
- 保持不变的 invariant
- compatibility boundary
- 明确不在本 PR 处理的内容
-->

## Validation

<!--
列出实际执行的命令、测试场景和结果，不要只写 “CI passes”。
如果某项未运行，说明原因和 residual risk。根据实际验证增删表格行。
-->

| 验证 | 结果 |
| --- | --- |
| `<command or scenario>` | `<pass / expected result / test count>` |

## Risk / Rollout / Rollback

<!--
根据实际改动覆盖：
- Risk level 和主要 failure mode
- deployment / migration order
- feature flag、backfill 或 manual step
- merge/deploy 后需要观察的 metrics、logs、alarms
- rollback、revert 顺序或 data recovery
- 无 runtime 影响时明确写明
-->

- **风险（Risk）：**
- **部署与发布顺序（Rollout / Deployment order）：**
- **监控与观察（Monitoring）：**
- **回滚方案（Rollback）：**

## Reviewer guide

<!--
告诉 reviewer：
- 最需要重点检查的 contract、文件或 decision
- 哪些内容已经由 tests/CI 证明
- 哪些判断仍需要人工确认
- 关联 Issue、spec、design doc 或 stacked PR
-->

<!--
CONDITIONAL MODULE — Bug / regression / incident
遇到 bug、Sentry issue、regression 或 production incident 时启用。

## Root Cause

说明：
- 触发条件
- 失败路径
- 为什么旧实现允许问题发生
- 为什么本次修改能防止回归
-->

<!--
CONDITIONAL MODULE — Observable behavior change
存在明显行为、流程、输出或 contract 变化时启用。

## 改前 vs 改后

| 设计面 / 行为 | 改前 | 改后 |
| --- | --- | --- |
| `<surface>` | `<old behavior>` | `<new behavior>` |
-->

<!--
CONDITIONAL MODULE — Architecture / cross-component flow
跨 service、API、queue、database 或系统边界时启用。

## Architecture / Data flow

使用足以说明改动的 ASCII 或 Mermaid 图，覆盖相关的 upstream input、authority / validation boundary、processing flow、persistence / side effects、downstream consumers 和 failure path。
-->

<!--
CONDITIONAL MODULE — UI
有用户可见的 frontend 变化时启用。

## Screenshots

覆盖被改动且影响 reviewer 判断的状态，例如 Before / After、相关 responsive viewport，以及被修改的 loading / empty / error state。说明截图对应的 commit、environment 和验证方式。
-->

<!--
CONDITIONAL MODULE — Database / schema / data migration
涉及 schema、migration、backfill 或 data contract 时启用。

## Migration / Data safety

说明：
- 迁移顺序（expand / backfill / cutover / contract）
- 兼容性窗口（compatibility window）
- 存量数据验证（existing data validation）
- 锁表与停机时间（locking / downtime）
- 迁移演练（migration dry-run）
- 回滚风险与不可逆边界（rollback risk / irreversible boundary）
-->

<!--
CONDITIONAL MODULE — Infrastructure / CDK / Lambda / deployment
涉及 infrastructure、CDK、Lambda、workflow 或 runtime config 时启用。

## Deployment / Infrastructure

说明：
- 影响范围（affected stacks / functions / workflows / environments）
- 实际验证（validation）与部署顺序（deployment order）
- 配置、密钥、IAM 和资源替换（config / secret / IAM / resource replacement）
- 可观测性（observability）与回滚路径（rollback path）
-->

<!--
CONDITIONAL MODULE — Security / authorization / sensitive data
涉及 auth、permissions、tenant data 或 external credentials 时启用。

## Security / Tenant isolation

说明：
- 认证与授权边界（authentication / authorization boundary）
- 租户、店铺与账户隔离（tenant / store / account isolation）
- 敏感数据处理（sensitive data handling）与最小特权原则（least privilege）
- 故障处理边界（fail-open / fail-closed behavior）
- 安全回归测试（security regression tests）
-->

<!--
CONDITIONAL MODULE — Observability
新增或修改 production behavior、background processing 或 integration 时启用。

## Observability

说明：
- 日志、指标、追踪与告警（logs / metrics / traces / alarms）
- 成功与失败信号（success / failure signal）
- 发布后的观测与判断方式
- 告警负责人（alert owner）与排障入口（troubleshooting entry point）
-->

<!--
CONDITIONAL MODULE — Review changed implementation
Review comments 导致实质修改时启用。

## Review updates

说明：
- 修复了什么 review finding
- 具体实现如何变化
- 新增或重跑了哪些 validation
- 遗留或推迟项目的 follow-up 与风险边界
-->
