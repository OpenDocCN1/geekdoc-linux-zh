
| 数据类型 Data Type | CHAR CHAR- | | | |
| 长度 Length | 3 | | | |
| 小写字母 Lowercase letters | | | | |
| 转换例程 Convers. Rout | | | | |
| 输出格式 Output format | ALPHA | | | |
| SID 表 SID table | ICE/BICE/DTRY | | | |
| 特性是否为文档属性 Characteristic is document attr | 常数 Constant | | | |
| 传输路由 Transfer Routing | 最后更改 Last change | | | |
| 属性 By | SCHNEIDER | | | |
| 时间 On | 03.04.2002 11:41:03 | | | |

对利润中心完成相同的过程，如下所示。现在我们已经完成了特性的设置。

| 合作伙伴 Partner | | 业务中心 Business Center | | | |
|---|---|---|---|---|---|
| 特性 Characteristics | ICE_PCTR | | | | |
| 长描述 Long description | 合作伙伴中心 Partner Center | | | | |
| 参考特性 Reference char | ICE_PCTR | | | | |
| 版本 Version | 激活 Active | 已保存 Saved | | | |
| 对象状态 Object Status | 激活 Active, 可执行 exercable | | | | |
| | 业务解释器 Business Explainer | 主数据字段 Master datafields | 层级结构 Hierarchy | 复合 Compounding |
| 字典 Dictionary | 其他 Other | | | | |
| 数据元素 Data element | ICE/BICE/PCTR | | | | |
| 数据类型 Data Type | CHAR CHAR- | | | | |
| 长度 Length | | | | | |
| 小写字母 Lowercase letters | | | | | |
| 转换例程 Convers. Rout | ALPHA | | | | |
| 输出格式 Output format | | | | | |
| SID 表 SID table | ICE/BICE/DCTR | | | | |
| 特性是否为文档属性 Characteristic is document attr | 常数 Constant | | | | |
| 传输路由 Transfer Routing | 最后更改 Last change | | | | |
| 属性 By | SCHNEIDER | | | | |
| 时间 On | 03.04.2002 11:41:46 | | | | |

# 第 13 章：高级报告过程与功能 575

接下来，我们需要设置键值（key figures）。初始键值（key figure）将是一个没有引用活动的标准键值，如下所示。该键值的技术名称为 `ICE_REV`。

| 版本比较 Version Comparison | | 业务内容 Business Content | | |
|---|---|---|---|---|---|
| 键值 Key Figure | `ICE_REV` | | | | |
| 长描述 Long description | 收入 Revenue | | | | |
| 短描述 Short description | | | | | |
| 版本 Version | | 激活 Active | 已保存 Saved | | | |
| 对象状态 Object status | | 激活 Active, 可执行 executable | | | | |
| 类型布局 Typelayout | 聚合 Aggregation | 附加属性 Additional Properties | | | |
| 类型控制 TypeCtrl | | | | | |
| + 金额 + Amount | 数字 Number | 日期 Date | | | |

# 578 SAP 业务信息仓库报告

数据浏览器：表 `RSDICE` 选条目 12

| KEYNM | OBJECT | POGET | IDNM1 | IDNM2 | SCOLEOP1 | SCOLEOP2 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `ICE_REV1 A` | 0001 | `ICE_PTRC` | `ICE_PPTR` | | | |
| `ICE_REV1 A` | 0001 | `ICE_CTRY` | `ICE_PTRY` | | | |
| `ICE_REV2 A` | 0001 | `ICE_PTRC` | `ICE_PPTR` | | | |
| `ICE_REV2 M` | 0001 | `ICE_PTRC` | `ICE_PPTR` | OR | | |
| `ICE_REV3 A` | 0001 | `ICE_PTRC` | `ICE_PPTR` | OR | | |
| `ICE_REV3 M` | 0001 | `ICE_CTRY` | `ICE_PPTR` | OR | | |
| `ICE_REV4 A` | 0001 | `ICE_PTRC` | `ICE_PPTR` | AND | | |
| `ICE_REV4 M` | 0001 | `ICE_PTRC` | `ICE_PPTR` | AND | | |
| `ICE_REV4` | 0001 | `ICE_CTRY` | | | | |

版权所有 SAP AG

在此过程中填充的另一个表是 `RSDIOBJCMP`。此表存储了所有复合信息对象（InfoObjects）的信息。在这种情况下，键值（key figures）是复合的，请注意如下所示，`REV1` 到 `REV4` 复合到了 `REV`：

## 层级结构“国家显示”：“活动版本”

| 层级结构 | 级别 | 属性 | 内部 | 节点名称 | L |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 测试节点 | 特性说明 | 国家 | 信息对象 | | |
| | 欧洲 | | `SHEER_NODE_EUROPE` | | |
| | AT | | `ICE_CODE_AT` | | |
| | DE | | `ICE_CODE_DE` | | |
| | UK | | `ICE_CODE_UK` | | |
| | | | `SHEER_NODE_USA` | | |
| | CTRY | | `ICE_CODE_CTRY` | | |
| 美洲 | | | `SHEER_NODE_AMERICAS` | | |
| | CDN | | `ICE_CODE_CDN` | | |
| | US | | `ICE_CODE_US` | | |

版权所有 SAP AG

接下来，我们需要使用在查询中将使用的层级结构来识别组合并为报告赋值。在这种情况下，将配置两个层级结构：一个用于利润中心组合，另一个用于国家组合。这里显示了这两个层级结构。注意特定节点中利润中心的组合，以及它们如何汇总到文本以进行分区摘要。这将是执行收入组合的最终驱动因素。

数据浏览器：表 `RSDIOBJCMP` 选条目 8

| KEYNM | OBJECT | POGET | RSDIOBJCMP | CMPTY |
| :--- | :--- | :--- | :--- | :--- |
| `ICE_REV1` | 0001 | `ICE_REV` | 4 | |
| `ICE_REV1 M` | 0001 | `ICE_REV` | 4 | |
| `ICE_REV2` | 0001 | `ICE_REV` | 4 | |
| `ICE_REV2 M` | 0001 | `ICE_REV` | 4 | |
| `ICE_REV3` | 0001 | `ICE_REV` | 4 | |
| `ICE_REV3 M` | 0001 | `ICE_REV` | 4 | |
| `ICE_REV4` | 0001 | `ICE_REV` | 4 | |
| `ICE_REV4 M` | 0001 | `ICE_REV` | 4 | |

* 注意 *

# 第 13 章：高级报告过程与功能 579

层级结构“利润中心”显示：“活动版本”

| | 维护级别 | 层级结构属性 | 利润中心 | | 信息对象 | 节点 | L |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 利润中心 | | 利润中心 | | | `BHER_NODE` | ROOT | |
| | 利润中心 | | | | `BHER_NODE` | | |
| | | `PC102` | | | `ICE_PTRC` | `PC0..` | | |
