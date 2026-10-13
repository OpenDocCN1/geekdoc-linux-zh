
让我们看看在信息立方中启用的原生属性。在第一张插图中，没有启用原生属性，但在第二个图中你可以看到 `0OLD_TO_COUNTRY` 有标记。从查询侧的技术角度来看，在数据选择期间，数据管理器连接信息提供者和主表（“连接”）来填充查询。

![](img/f703ab958723c29086b17397273fad3b_207_0.png)

| 版本比较 | | | | | | | |
|---|---|---|---|---|---|---|---|
| 信息立方 | 技术名称 | O | Data | L | Key Fi |
| 客户立方 `T_SDDMEM02` | | | | | | | |
| 对象信息 | | | | | | | |
| 设置 | | | | | | | |
| 维度 | | | | | | | |
| 导航属性 | | | | | | | |
| 竞争对手 | `OMATERIAL_COMPETITOR` | | | CHAR 19 |
| 物料 | `OMATERIAL_PRM_VIBON` | | | CHAR 22 |
| 部门 | `OMATERIAL_DIVBION` | | | CHAR 02 |
| 外部物料组 | `OMATERIAL_GETMATGRP` | | | CHAR 18 |
| 激活属性 1 (主激活属性) | `OMATERIAL_HC_AGENT1` | | | CHAR 20 |
| 激活属性 2 | `OMATERIAL_HC_AGENT2` | | | CHAR 20 |
| 激活属性 3 | `OMATERIAL_HC_AGENT3` | | | CHAR 20 |
| 锚点指示器 | `OMATERIAL_HC_AIBIND` | | | | | |
| 审批类型 | `OMATERIAL_HC_APPRTY` | | | CHAR 02 |
| ATC 代码 | `OMATERIAL_ATC_CODE` | | | CHAR 02 |
| ATC 代码的医学类别 | `OMATERIAL_HC_ATMTYP` | | | CHAR 03 |
| 目录 1 | `OMATERIAL_HC_CATIN01` | | | | | | |
| 目录 2 | `OMATERIAL_HC_CATIN02` | | | | | | |
| 目录 3 | `OMATERIAL_HC_CATIN03` | | | | | | 01 |

## 第 6 章：在 BEx Query Designer 191 中增强特性的使用

### 显示 InfoCube

| 版本比较 | | | 业务内容 | | 日期 | L | 关键 F. |
|---|---|---|---|---|---|---|---|
| InfoCube | | | 性名称: Value | | | | |
| 预定义源 | | | `MATERIAL_QRT_RULE` | CHAR 01 | | | |
| | 季节 | | | `MATERIAL_QRT_SEASON` | CHAR 04 | | | |
| | 季节年份 | | | `MATERIAL_QRT_SEAVR` | CHAR 04 | | | |
| | 尺寸 | | | `MATERIAL_QRT_SIZE` | CHAR 18 | | | |
| | 供源 | | | `MATERIAL_QRT_RIFF` | CHAR 01 | | | |
| | 行业标准描述 | | | `MATERIAL_OSDO_DESCR` | CHAR 02 | | | |
| | 特性类型 | | | `MATERIAL_BUCCERITTY` | CHAR 06 | | | |
| | 结构类 | | | `MATERIAL_ARTICLA` | CHAR 08 | | | |
| | 功能类 | | | `MATERIAL_GFUNCLASS` | CHAR 08 | | | |
| | 客户账户 | | | `MATERIAL_VENDOR` | CHAR 10 | | | |
| | 售方部分的业务伙伴名称 | | | `ISOLDO_TO_PARTNER` | CHAR 10 | | | |
| | 售方行业 | | | `ISOLDO_TO_INDU` | CHAR 03 | | | |
| | 对方国家 | | | `ISOLDO_TO_COUNTRY` | CHAR 03 | | | |
| | 客户分类 | | | `ISOLDO_CUST_CLASS` | CHAR 02 | | | |
| | 客户主数据 | | | `ISOLDO_TO_MASTER` | CHAR 05 | | | |
| | D&B > D-U-S 名称 | | | `ISOLDO_DOBNS_NUM` | NUMC 09 | | | |
| | `ISOLDO_TO_DOBEMPT` | | | `ISOLDO_TO_DOBEMPT` | NUMC 07 | | | |
| | 行业 | | | `ISOLDO_TO_INDU` | CHAR 04 | | | |
| | 关键客户 | | | `ISOLDO_KEYACCOUNT` | CHAR 01 | | | |
| | 项目 ID | | | `ISOLDO_TO_ITEM_ID` | CHAR 02 | | | |
| | 品牌变体 | | | `ISOLDO_TO_TYPE` | CHAR 04 | | | |
| | 邮政编码 | | | `ISOLDO_TO_POSTAL_CD` | CHAR 04 | | | |
| | 州（国家） | | | `ISOLDO_TO_REGION` | CHAR 03 | | | |
| | `ISOLDO_TO_GISESEMPRTY` | | | `ISOLDO_TO_GISESEMPRTY` | NUMC 08 | | | |
| | 预定义类别 | | | `ISOLDO_TO_INVST_RTY` | | | | |

关于使用导航属性需要一点注意：大量使用导航属性会导致在选择过程中“连接”中出现大量表，并可能阻碍导航属性的删除和创建（属性 SID 表的构建）。这也会影响导航属性的时间依赖性、主数据的加载（属性 SID 表的调整），导航属性的输入调用以及查询的执行。从技术上讲，有时手动为主数据表创建额外的索引，以提高带有导航属性查询的系统性能。一个典型的场景是，假设你在选择特性值时遇到问题——例如，在包含导航属性的 BEx 查询中，相应的主数据表很大（超过 20,000 条目）。在这种情况下，通常对导航属性施了限制。我们在前一节中讨论过从导航属性使用传递属性，因此我想说明这是你可能调查的特性使用的另一种选项，可以根据你所开发的系统架构进行深入研究。

如果一个特性作为导航属性包含在 `InfoCube` 中，则它可以用于导航查询。该特性本身具有进一步的导航属性，称为传递属性。这些属性在查询中不会自动可用于导航。正如第 2 章所述，它们必须被开启。

## SAP 业务信息仓库报告

### 特性属性

在本节中，我们将从 `BEx Query Designer` 的视角而非 BEx Analyzer 来看特性属性，因为许多不同的选项是相似的，我们只对 `BEx Query Designer` 特有的选项进行详细介绍。

在特定特性的“特性属性”对话框中，你可以设置一系列功能。这些设置会影响查询下钻中该特性的所有键值（key figures）。尽管这些可以在这里都设为默认设置，但在查询的执行状态下仍然可以更改。下面的插图显示了此主题可用不同选项页的初始视图。在“常规”（General）选项卡中，特性的名称会自动出现。你可以覆盖此文本。新文本与 `InfoObject` 维护中提供的文本不同，并用于查询显示。“使用标准文本”（Use Standard Text）复选框允许你指示始终使用默认值。在这种情况下，标准文本是来自 `InfoObject` 维护中确定的特性的文本。特性的技术名称也显示在此选项卡中。

![](img/f703ab958723c29086b17397273fad3b_209_0.png)

“显示”（Display）选项卡提供了选项。在显示部分，你可以选择想要呈现的格式。选项有：

- 不显示
- 键值
- 文本

## 第 6 章：在 BEx Query Designer 193 中增强特性的使用

如果你设置了文本的显示类型，你可以选择所需的文本。选项有：

- 标准
- 短文本
- 长文本
- 中文本

在“排序”（Sorting）选项卡中，你可以根据键值按升序对特性进行排序。如果特性具有属性，你可以按属性排序。在“按...排序”下，选择键值或文本。选择升序或降序。

假设你想根据特定标准进行排序。为此，你可以为文章创建一个属性。然后你可以根据该属性排序。

在“特性设置”（Characteristic Setting）对话框中，你可以指定始终使用默认值。在这种情况下，标准文本是 `InfoObject` 维护中确定的特性。在“结果行”（Results rows）中，你可以选择始终显示、始终提供或显示多个单值。显示多个单值意味着当存在至少两个单值时显示结果，且任何结果仅显示一个值。在这种情况下，值和结果是相同的，行重复相同的值。结果行的决策可能比你想象的更有争议。
