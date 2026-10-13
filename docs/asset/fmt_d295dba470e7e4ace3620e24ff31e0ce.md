
除了详细导航外，导航面板还包含用于动态导航和相关链接的 `iViews`，这些也可以包含 BI 内容。详细导航会自动出现，就像 Portal 角色的第二层包含带有 `iViews` 和 Portal 页面的文件夹，从而包含更多内容。当显示 Portal 页面或 `iViews` 时，动态导航和相关链接的 `iViews` 在导航面板中显示相应的 `iView` 链接。您可以在 Portal 页面以及每个单独 `iView` 上设置 `iViews`。所有 Portal 页面和 `iViews` 都包含在导航面板中，并显示为“动态导航”和“相关链接”。在动态导航中，`iViews` 本身显示在导航面板中。在相关链接中，会显示链接列表。除了之前列出的 `iViews` 外，导航门户中还会显示 Portal 收藏夹（Portal Favorites）`iView`。

## 业务智能门户角色

在门户中，Portal 角色是您处理 BI 内容的主要入口点。它包括分析、报告以及规划。Portal 角色的技术名称为 `com.sap.ip.bi_showcase`。

业务智能门户包含来自两个 Portal 角色的内容：资源管理器（Explorer）和业务规划（Business Planning）。前文描述的业务规划提供了用户如何在门户中使用 BI 内容来分析业务数据并分发这些数据，同时使用知识管理和协作功能的示例。另一方面，业务规划 Portal 角色允许业务专家使用模型规划应用程序。

## 企业门户管理员与企业门户

本节提供了有关将 BI 内容集成到门户中的不同场景的描述。解释包含了技术信息，将有助于管理员理解并进行必要的设置。在“自定义”（Customizing）下列出的详细前提指的是当前场景。更多信息请参阅 SAP Reference IMG_SAP Customizing Implementation Guide_SAP NetWeaver_Business Intelligence_Settings for Reporting and Analysis_BEx Web_Integration into the Portal。这些信息大多是技术性的，可能是 IT 组或 Portal 组的职责，但对每个这些不同门户可以显示的内容有一个基本的理解。

BI 内容可以以不同的方式显示。BEx 应用可以作为 `iViews`、预计算文档或门户中的链接包含在门户中。此外，您可以在门户中显示 BI 分析器工作（Analyzerbooks）和 BI 文档。可以使用 BI Portal 角色或门户中的 KM 文件夹调用这些内容。各种工具支持您在门户中生成 BI 内容并将其整合。将 BI 内容集成到门户需要来自 SAP NetWeaver BI 和 SAP NetWeaver Portal 的经验。为了进行必要的设置，BI 系统管理员与 Portal 管理员之间的密切合作。同样，负责 BI 内容和 Portal 内容的作者必须密切工作，将 BI 内容集成到门户中。

您可以使用各种工具将 BI 内容集成到门户中。根据集成类型，您会在门户中创建具有不同显示方式的对象。您在门户中显示 BI 对象有多种选项。各种显示类型总结在表 16-3 中。

| 显示类型 | 描述 |
| :--- | :--- |
| 作为 iView 的 BEx Web Application | 在门户中作为 iView 显示的基于 Web 的 BI 应用。BEx Web Applications 是使用 BEx Web Application Designer 创建的在 Web 上执行的模板。 |
| 作为知识管理中文档的 BEx Web Application | 存储在 KM 文件夹中带有历史数据的基于 Web 的 BI 应用。 |
| 作为知识管理中在线链接的 BEx Web Application | 存储在 KM 文件夹中带有当前数据的基于 Web 的 BI 应用的链接。 |
| 作为 iView 的 BEx Workbook | 带有带有或多个嵌入查询的 Microsoft Excel 工作簿，在单独的浏览器窗口中作为 iView 显示。（这是一个非常重要的点，因为使用 BI Portal 代替了 BEx 浏览器，Portal 可以成为您报告策略的中心。因此，您可以在门户中同时访问 Web 报告和 BEx Analyzer 工作簿。） |
| 作为 KM 文档的 Analyzer Workbook | 带有一个或多个嵌入查询的 Microsoft Excel 工作簿，以带有历史数据的文档形式存储。 |
| 作为 iView 的 BEx Query | 在门户中作为 iView 显示的带有一个或多个嵌入查询的 Microsoft Excel 工作簿。 |
| 作为 KM 中在线链接的 BEx Query | KM 文件夹中带有当前数据的基于 Web 的 BI 应用的链接。 |
| 作为 KM 文档的 BEx Query | 存储为带有历史数据的文档的 Microsoft Excel 工作簿。 |
| 作为 iView 的单个 BI Document | 在门户中作为 iView 显示的带有一个或多个嵌入查询的 Microsoft Excel 工作簿。 |
| 作为 iView 的多个 BI Document | KM 文件夹中带有当前数据的基于 Web 的 BI 应用。 |
| 作为 iView 的 Web 接口 | 在门户中作为 iView 显示的 Web 应用程序。 |
| BI 组件 | 来自 BI 系统的各种。 |

表 16-3 在门户中显示 BI 对象的选项

# 第 16 章：组织您的报告——企业门户

## 作为 iView 的 BEx Web Application 或 Query

在门户中作为 iView 显示的基于 Web 的 BI 应用或查询。BEx Web Applications 或查询直接访问 BI 系统。当使用 Portal 缓存时，数据更新会有延迟。可以使用 BEx Application Designer 或 BEx Query Designer 生成 BEx 应用或查询。两个最重要的属性 `System` 和 `BEx Application String` 会为 BEx Application Designer 和 BEx Query Designer 自动设置。您需要在 Portal 中手动输入这些属性。

`System` 属性包含 BI 系统上的别名（在门户中创建 BI 系统）。表 16-4 显示了可能用于 SAP BI 的 BEx Application String 值。

`<...>` 是替换为对象名称的占位符。您可以在 `BEx Application String` 属性上添加更多 URL 参数（例如设置过滤值）。URL 参数用连符号 (`&`) 隔开。可以使用 `Application Parameters` 传输额外的 BI 参数。

## 作为 KM 文档或链接的 Bex Web Application 或 Query

您可以将在 Web 上显示的 BEx 应用或查询作为预计算文档或链接，以 iView 的形式在知识管理中。带有历史数据的预计算文档存储在知识管理中（不在 BI 系统中）。BEx 应用或查询的链接通过 BI 元数据的存储管理器间接访问 BI 系统。可以使用 BEx Broadcaster 生成文档，并使用 BEx Application Designer 或 BEx Query Designer 生成链接。文档和链接仅位于知识管理中（不在 BI 系统中）。您可以使用

| BI 对象 | 值 |
| --- | --- |
| Web Template | `<TEMPLATE>` |
| Query | `<QUERY>` |
| Query View | `initial_state=VIEW&initial_state-view=<VIEW>` |
| InfoProvider | `initial_state=INFROPROVIDER&initial_state-infopvider=<INFROPROVIDER>` |
| Report | `<REPORT>` |

表 16-4 门户的 BEx Application String 属性

## SAP 业务信息仓库报告

使用 Portal Content Studio 创建包含文档和链接的 `iViews`。这些 `iViews` 的类型为 KM Document iView，代码链接为 `com.sap.km.cm.docs`。最重要的属性是文档的路径。以下是一些需要注意的点：

- 如果使用预计算的 BEx Web 应用程序或查询作为文档，路径独立于知识管理（Knowledge Management）中选择的文件夹。你需要在 BEx Broadcaster 的 `Target`（目标）选项页中指定文件夹。
- 如果使用 BEx Web 应用程序或查询作为链接，文档的路径独立于 BI 元数据仓库管理器（BI Metadata Repository Manager）所选的前缀以及 BEx Web 应用程序的模板 ID。你必须输入以下值作为文档路径（括号中的标识是技术名称的占位符）：
