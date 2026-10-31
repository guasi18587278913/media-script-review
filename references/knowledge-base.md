# 知识库接入与选法

## 同一知识库，两端入口

- Codex：发现当前可用工具中属于 `gbrain_sc_media` 的 `get_page`。
- Claude Code：发现当前可用工具中属于 `sc-media-kb` 的 `get_page`。
- 这是同一用户知识库的只读入口。不同客户端的工具前缀可能变化，按工具能力和说明识别，不硬编码某个运行时包装器，不修改 MCP 配置或权限。

调用采用 `get_page` 的 `slug` 参数。工具未加载或调用失败时，回到 SKILL.md 的内置标准降级流程。未成功读取的页面不能算依据；需要用户明确指定的原文而缺失时，只标该部分待核。

## 当前任务怎样读

开始审稿或改稿时先读：

1. `workflows/creation_teacher`
2. `workflows/work_diagnosis`

当前会话已读且未变时不重复读取。库的最新细则用于补充内置标准，用户当前要求和锁定内容优先。仍然按“审现稿”的任务推进，不自动重走从零创作。

先根据现稿确定具体问题，再只读相关入口：

| 当前要解决的问题 | 对应入口 |
| --- | --- |
| 受众价值、选题角度确有问题 | `workflows/topic_planning`、`methods/playbook/playbook-topic-divergence` |
| 主线与结构 | `concepts/structure_quick` |
| 开头 | `concepts/opening_hook_quick` |
| 正文表达 | `concepts/body_expression_quick` |
| 结尾 | `concepts/ending_quick` |
| 标题或封面 | `workflows/title_packaging`、`concepts/title_cover_quick` |

选中写法后，使用页面支持的章节读取方式，如 `get_page(slug="concepts/structure#14")`，只读选中写法的完整说明；按速查页提示读取禁忌与“不照搬”小节，确认适用条件后再给替换句。不要假定每页都有相同编号或小节名称。

只审一个环节时，保留其他内容，仅核必要的承诺兑现关系。纯选题讨论停在角度，不能因为读了写稿方法就输出整篇稿。默认不重新做账号定位。

## 读取和使用边界

- 完整清单只在用户要求方法穷举、逐项验收，或速查页不足以判断时通读。普通全稿审查不等于穷尽所有方法。
- 不派助手扫全库，不批量读原文；核对具体例子时才沿出处读对应原文。用 `get_page` 读取，不直接读取 wiki-v2 文件。
- 已知页名直接读。查关联用 `get_backlinks`、`traverse_graph`；`search`、`query` 可能调用模型，不能假定免费或擅自发起可能付费的检索。
- 事实来自当前用户材料；知识库提供方法。原作者经验、历史范例、当前事实和本次判断分别表述，不把历史流量当可复现保证。
- 不使用已停用的 `workflows/draft_writing` 或旧观点、教程、纠错打法作为当前写稿流程。
- 只列确实采用的方法，并解释它改变了当前哪句或哪段；无法读到时使用内置检查法并如实说明，不事后贴知识库方法名。
- 本任务不写回、同步或维护知识库。只有用户要求保存作品或修改反馈时才读取 `workflows/creation_archive`，按该稿具体版本处理。
