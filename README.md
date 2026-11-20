# Mindwill

面向 IPaaS（集成平台即服务）的代码优先生态整合平台。用于快速搭建工作流、SOP、AI 工作台与 AI 监督学习，覆盖工作流、AI 应用、AI 决策和 AI 代理。

业务团队利用 AI 进行构建（业务流、工作流、各类 Flow：信息与资产）；工程师掌控最终发布版本。

> 这是一个面向 IPaaS 的平台（集成平台即服务），面向工作流、AI 应用、AI 决策和 AI 代理，用于快速搭建工作流、SOP、AI 工作台、AI 监督学习，是代码优先的生态整合平台，基于速度最快的自托管编排器（经测试，性能优于 Windmill、Airflow、Prefect 和 Temporal、mindflow.io）。业务团队利用 AI 进行构建，业务流、工作流、各种 Flow（信息、资产），工程师则掌控最终发布版本。它是 Lovable、Retool、Dify、FastGPT 和 n8n 的开源替代方案。

**说明：** 「经测试，性能优于 Windmill、Airflow、Prefect、Temporal 和 mindflow.io」是产品定位主张，本仓库尚未附测试方法或数据，不作为已验证结论。形成 90% 自动化是目标，不是现状。本仓库当前是前期构筑文档，不是已上线产品说明书。

- 品牌：天机跨境旗下的 Mindwill
- 拟用站点： [mindwill.dev](https://mindwill.dev)（About 与标签按此书写；Mindwill.io、Mindwill.ai、Mindwillai.com 仍为候选，尚未宣布取舍）
- 仓库： [yangyayun2016/mindwill](https://github.com/yangyayun2016/mindwill)

## 拟用标签

`ai-agents` · `airflow-alternative` · `internal-tools` · `open-source` · `orchestration` · `postgresql` · `python` · `rust` · `self-hostable` · `self-hosted` · `typescript` · `vibe-coding` · `workflow-engine`

技术取向（标签，不是已实现清单）：Rust、Python、TypeScript、PostgreSQL；自托管 / 可自托管；工作流引擎与 AI agents。

## 文档

完整前期构筑蓝图见 [docs/blueprint.md](docs/blueprint.md)，包括：

- 定位与目标、关于文案
- 五层架构
- Flow 构建元素（步骤、数据与触发、编辑与容错）
- 退款审批原理图与验证 Playbook
- 资产、AI 学习、AI 监督与黑匣子
- 竞品与对照范围（Windmill 官方对比目录 31 条，加 Mindwill 自身对照对象）
- 前期构筑顺序

## 来源

- [Flows quickstart](https://www.windmill.dev/docs/getting_started/flows_quickstart)
- [Workflows as code](https://www.windmill.dev/docs/core_concepts/workflows_as_code)
- [Windmill alternatives and comparisons](https://www.windmill.dev/compare)
