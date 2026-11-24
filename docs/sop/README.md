# 亚马逊全框架 SOP

本目录存放跨境电商亚马逊全框架 SOP 的构筑正文。它是前期构筑文档，不是已上线产品，也不是已跑通的验证流。已拍板的分层、红线与仍开放事项见 [蓝图](../blueprint.md)。

形成 90% 自动化仍是目标，不是现状。「经测试，性能优于 Windmill、Airflow、Prefect、Temporal 和 mindflow.io」仍是产品定位主张，本仓库未附测试方法或数据。Windmill Flow 词汇与退款店铺 playbook 只作参照，不在本目录里当成已选定的验证流。

## 目录规范

| 路径 | 是什么 |
| --- | --- |
| `docs/sop/NN-<slug>.md` | 一篇构筑。`NN` 是两位序号，从 `01` 起，按写入仓库的顺序递增，缺号不回填。`<slug>` 是短横线连接的短名。从 [_template.md](_template.md) 复制后填写 |
| `docs/bots/<bot>.md` | 该构筑对应 Bot 的身份与职责。从 [bots/_template.md](../bots/_template.md) 复制。一个 Bot 可以被多篇 SOP 引用；一篇 SOP 指向它的主责 Bot |
| `docs/sop/README.md`、`docs/sop/_template.md`、`docs/bots/_template.md` | 说明和模板，不是构筑正文，不占序号 |

slug 一旦被公开引用就不再改名。需要改名时新开一篇，并在旧篇写明替代关系。已写入的编号构筑见下方清单。

## 构筑清单

| 篇 | 名称 | 状态 | X.com |
| --- | --- | --- | --- |
| [01-amazon-ops-framework-overview.md](01-amazon-ops-framework-overview.md) | 亚马逊运营框架 SOP 架构总览 | 草稿 | 未发布 |

## GitHub 与 X.com 双端同步

1 个构筑 = 1 篇 `docs/sop/NN-<slug>.md` + 关联的 `docs/bots/<bot>.md` + 1 篇结构一致的 X.com 长文。

GitHub 上的稿是事实底稿。X.com 长文使用同一骨架，不另写一套没进仓库的步骤、字段或数字。骨架参照 Andrew（`@s4yonnara`）的 [Grok Bot 社媒团队长文](https://x.com/s4yonnara/status/2119777956423700863）：The skill / app / system at a glance、带人工审批闸门的原理图、分步判据（该文里的栏目标题是 “The system at a glance”，每步末尾是 “You're ready to move on when”）。Mindwill 在这个骨架上追加 `Memories` / `Skills` / `Routines` / `Integrations` 四栏和 Bot 职责卡。该文里的社媒团队步骤、工具和价格不是 Mindwill 的事实，不抄进构筑。

同步顺序：

1. 先把草稿写入本仓库。状态写「草稿」。X.com 链接栏写「未发布」。
2. 草稿经过所有者本人同意之后，才可以公开发布。
3. 发布后把帖子 URL 回写到对应 SOP 的基本信息里，状态改为「已在 X.com 发布」。

公开发布属于不可逆操作。未得到所有者本人同意时，不发帖、不转发、不把稿子贴到其他公开渠道。

## 事实分级

每一篇里的步骤和数据来源都要标明等级。三个等级不能混写成「已实现」：

| 等级 | 含义 | 当前怎么用 |
| --- | --- | --- |
| 已核实实现 | 本仓库或已运行环境里能够指到的行为 | 本仓库目前没有可运行产品代码。没有可核验的实现记录时，不要使用这一级 |
| 附件 / 实践陈述 | 所有者或业务材料里已经写出的做法 | 写明材料名称。材料没写的数字、字段和步骤不要补 |
| 待从飞书 SOP 补齐的节点 | 飞书 SOP 里应有、本篇还没抄入的步骤或字段 | 留下空位和待补说明。不根据常识填步骤，本说明也不链接一份未经指定的飞书文档 |

查不到的信息保持空缺，或标成待补。禁止编造字段、店铺数据、业绩数字或性能数字。

## 后续预留的目录

下面两个目录后续再配。本提交不创建它们，也不放入可运行代码，不预设字段 schema。

| 目录 | 以后放什么 |
| --- | --- |
| `flows/` | Mindwill 自研 JSON / YAML 配置。格式取向已定，具体字段尚未设计 |
| `graphs/` | LangGraph 状态图，Python 或 TypeScript（`@langchain/langgraph`）都可以。配置层在上；`StateGraph`、`Subgraphs`、Checkpointer（如 `PostgresSaver`）和 `interrupt()` 在下 |

每篇 SOP 的「编码编排」只说明这篇构筑打算怎样映射，字段名等 schema 拍板后再填。私有云默认取向是开源库自管加 Postgres。LangSmith Agent Server 自托管 / standalone 当前不绑定；若以后评估，须另行确认其商业许可。

## 写作时不要放开的口子

统一不可逆操作红线，以及跨境运营补充闸门，以蓝图中的原文为准。复制到单篇时原文保留，不可删减：

> 凡是对外发送消息或文件、公开发布内容、动用资金、承诺价格或交付时间、删除数据，以及其他任何不可逆操作，都必须先停下来征得所有者本人同意。
>
> 跨境运营补充闸门：店铺登录只在本地紫鸟、绝不上云；ERP 等外部系统的写操作与付款一律人工确认。

自动 routine 默认关闭。人工跑通一轮，并且确认闸门能拦住写操作之后，才可以开启。
