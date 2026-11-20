# 对照与参照笔记

本文是对整理材料的表达整理，供前期构筑对照使用。它不是 Mindwill 已实现能力的说明书，也不是 Mindwill 已获得的认证声明。

Flow 概念与退款示例提炼自 Windmill 公开介绍；竞品目录以 [docs/blueprint.md](blueprint.md) 中已核对的 31 条为准；Temporal 与信任中心的事实分别核对自 [temporal.io](https://temporal.io/) 与 [trust.windmill.dev](https://trust.windmill.dev/)（2026-11-20，Asia/Shanghai）。文中的对照判断来自整理笔记，未经 Mindwill 实测。

## 如何阅读那 31 条对照目录

[Windmill alternatives and comparisons](https://www.windmill.dev/compare) 是对照索引页。官方目录按六类组织，已完整写入蓝图，此处不再用「代表性几条」代替全部 31 条。整理稿里曾写「无法直接列出全部 31 个名称」，这一缺口已补上。

官方六类是：

- 工作流编排与数据引擎
- 工作流自动化与 iPaaS
- 内部工具与应用构建
- 安全自动化
- 基础设施与 IT 自动化
- 更多对照

整理笔记的理解是：这张索引要划清边界，而不是宣称在所有维度上胜过所有对象。代码优先的工程团队，可能更看重可测试的多语言脚本、Git 版本控制，以及可视化编排与审批；纯 SaaS 连接、零代码或完全托管的场景，整理笔记认为 Zapier、Make 或 n8n 往往更直接。这是阅读方向，不是 Mindwill 的选型结论。

Dify、FastGPT、mindflow.io 出现在 Mindwill 关于文案中，但不在上述 31 条里，对照时需单独记下。

## 整理笔记中的对照要点

下表保留整理稿里的代表性差异，便于快速阅读。条目分组与官方六类不完全相同（例如整理稿把 Kestra 放在「数据与基础设施编排」，把 PowerShell Universal 放在「安全与 IT 自动化」；官方目录中 Kestra 属于「工作流编排与数据引擎」，PowerShell Universal 属于「基础设施与 IT 自动化」）。具体对比以各来源页为准。

| 阅读分组 | 对象 | 整理笔记中的要点 | 来源页 |
| --- | --- | --- | --- |
| 工作流编排与数据引擎 | Apache Airflow | 纯 Python DAG 的常见选择，人才库大；Windmill 强调多语言，且步骤可单独测试，短任务调度开销更小 | https://www.windmill.dev/compare/airflow |
| 工作流编排与数据引擎 | Prefect / Dagster | Prefect 偏用装饰器编排已有函数，Dagster 偏按数据资产思考；Windmill 更常被放到混合语言管道，或需要在管道旁加 UI 与审批的场景 | https://www.windmill.dev/compare/prefect 、 https://www.windmill.dev/compare/dagster |
| 工作流编排与数据引擎 | Temporal | 代码优先的 SDK，把持久化工作流写进产品代码，由工程师精细控制；Windmill 更偏向可视化编排 | https://www.windmill.dev/compare/temporal 、 https://temporal.io/ |
| 工作流编排与数据引擎 | Kestra | 整理稿写：YAML 声明管道、插件丰富；审批等表单 UI 在其企业版；Windmill 的审批步骤在社区版可用。此条未经本仓库复核，以官方对照页为准 | https://www.windmill.dev/compare/kestra |
| 工作流自动化与 iPaaS | n8n | 偏预构建节点与画布；整理稿写 n8n Cloud 的 Code 节点无法导入外部包，Windmill 以可独立运行、带依赖的脚本为中心。Cloud 限制一条未经本仓库复核 | https://www.windmill.dev/compare/n8n |
| 工作流自动化与 iPaaS | Zapier / Make | 非开发者主导、SaaS 之间搬数据、接受托管时更常见；Windmill 更常被放到开发者主导、逻辑要进 Git，或必须跑在自有网络内的自动化 | https://www.windmill.dev/compare/zapier 、 https://www.windmill.dev/compare/make |
| 内部工具与应用构建 | Retool | 模板与组件库强，适合较简单的 CRUD 界面；整理稿写 Retool 闭源，自托管需企业版，Windmill 开源可自托管。许可与版本边界以各方当前说明为准 | https://www.windmill.dev/compare/retool |
| 基础设施与 IT 自动化 | PowerShell Universal | 自动化资产围绕 PowerShell、希望单机跑脚本 / API / 门户时更贴；Windmill 被整理为可与其他语言共存，并带更完整的工作流编辑与审批 | https://www.windmill.dev/compare/powershell-universal |

## Flow 概念精炼

蓝图里的 Flow 构建元素、退款原理图和验证 Playbook，已经按 Windmill 官方演示整理过。这里只保留公开介绍里最要紧的几句，不再按截图逐张展开。

Windmill 产品卡上的定义是：Flow 用来把脚本组成工作流；可视化构建器支持把脚本串起来，并处理分支、循环、错误处理、审批和重试；每个步骤可从工作区或 Hub 复用。要点包括：拖拽步骤；分支、循环与错误处理；暂停 / 审批步骤。配套演示是约两分钟的 [What is a flow](https://www.windmill.dev/docs/getting_started/flows_quickstart)。

公开演示里还有一句更短的本质描述：Flow 是由步骤组成的图，并以 JSON（或 YAML）存储。也就是说，人看到的是可编排的图，机器执行和版本控制用的是文本定义。步骤可以是动作、审批 / 提示、嵌套 Flow、循环、分支（走一条或走全部）、AI Agent / AI Decision；后续步骤通过 `results.<step_id>` 引用前面的结果，通过 `flow_input` 引用流程入参。触发方式与脚本相同，演示中出现过 Webhooks、定时、HTTP 路由、邮件、Kafka、Postgres 变更等。

这些是参照对象的能力描述，不是 Mindwill 已实现清单。

## Temporal 对照

[Temporal](https://temporal.io/) 把自己定位为持久化执行（Durable Execution）平台：用已有语言的 SDK 编写业务逻辑，由平台保证流程在失败后能从中断处继续，而不是另写一套对账和断点恢复。公开首页（2026-11-20 查阅）强调两点分工：

- **Workflow**：用代码书写的业务流程，状态会被持久化；失败后可从停下的位置恢复。
- **Activity**：与外部世界交互的单元（调用 API、等待输入等），由平台处理重试与恢复。

部署上可以自托管开源服务（首页写明 MIT 许可），也可以使用 Temporal Cloud。首页写：「Either way, we never see your code」。也就是业务代码跑在使用者自己的环境里。公开用例包括 Agents / MCP / AI 管道、人工介入（Humans-in-the-Loop）、长时流程、Saga 补偿等。

整理笔记与公开对照页把两者的差别概括为：Temporal 是代码优先、交给后端或平台工程师做工业级容错与状态管理；Windmill Flow 以可视化编排为主，脚本作为节点，审批和 AI 步骤更开箱即用。二者都出现在 Mindwill 的性能对照名单里，但「经测试，性能优于……」仍是定位主张，本仓库未附测试数据。

整理稿中还提到若干 Temporal 客户与框架集成名称。除首页明确出现的公开表述外，此处不另行转写，避免把未核对的名单写进仓库。

## 企业安全与合规参照（Windmill Trust Center）

[Windmill Trust Center](https://trust.windmill.dev/) 回答的是企业客户会问的问题：把业务逻辑和敏感数据放到这个平台上，安全与合规如何证明。这是 Windmill 的信任中心，不是 Mindwill 的认证。记下它，是为了看清后期若面向企业客户，大约要回答哪些问题。

2026-11-20 对照整理稿截图与该页面时，可见：

- 合规概况中，SOC 2 Type 2、HIPAA 均显示为已合规。
- 特色文档包括 Windmill Pentest 2026 认证函，以及 Windmill SOC 2 II 型认证 2025。
- 控制措施按类别列出，截图中可见并已在该站核对到的类别包括：访问控制与授权、数据管理与保护、灾难恢复、电子邮件安全、端点安全。站点上还有漏洞管理等更完整的控制目录。

整理笔记把这些措施与 Flow 能力对应起来看：托管模式下要用加密、访问控制和审计来证明安全；若流程里会把敏感数据交给大模型，SOC 2 与 HIPAA 是常见的合规依据；备份、恢复测试和业务连续性，则关系到长周期审批和流程状态会不会因故障丢失。这些对应关系是阅读理解，不能写成 Mindwill 已经具备同等认证或控制。

Mindwill 材料中的取向是本地或私有化部署、密码库与最小必要调用。具体认证、控制清单和部署形态都还没有定，这里只作为后续安全设计的参照清单。
