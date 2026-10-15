
一个 IPP 请求的剖析

图 8.5 Get-Jobs 响应

## 总结

IPP 请求和响应使用常见的二进制格式。多字节整数值采用网络字节序（大端）。每个属性组必须通过 HTTP POST 方法发送，内容类型为 `application/ipp`。每个请求还带有额外数据（如打印文件）。每个响应都有状态码和其他可能的属性，以完整描述任何错误状况。

166

本页留白

167

# 9 章

## 打印机对象

本章介绍了为 IPP 打印机对象提供的属性操作。

### 什么是打印机对象？

打印机对象代表接受并打印任务对象的单个打印机。打印机对象还可以关联订阅对象。

每个打印机对象始终处于三种状态之一：空闲（idle）、处理中（processing）或停止（stopped）。空闲打印机对象是因为没有打印任务。当新对象可用时，打印机对象开始打印。

处于处理状态的打印机对象正在打印一个任务对象。能够同时打印多个对象的打印机通常是大幅打印机或可以沿介质宽度输出以提高速度的打印机。大多数 IP 实现一次只打印一个任务。

最后，停止打印机对象在发生物理错误（例如缺墨水或纸张）且管理员决定在处理期间将其离线时停止。

### 必要属性

打印机对象有多个关联属性。这些属性在 IPP 服务器上始终可用，但如果未定义或实现不支持，其值可能为空。表 9.1 列出了打印机对象的必要属性。

表 9.1 打印机对象的必要属性

| 属性 | 类型 | 描述 |
|---|---|---|
| `charset-configured` | charset | 文本属性的默认字符集 |
| `charset-supported` | 1setOf charset | 支持的字符集 |
| `compression-supported` | 1setOf type3 keyword | 服务器支持的压缩类型 |
| `copies-default` | integer (1:MAX) | 默认生成的副本数 |
| `copies-supported` | rangeOfInteger (1:MAX) | 支持的副本数数范围 |
| `document-format-default` | mimeMediaType | 打印任务的默认文档格式 |
| `document-format-supported` | 1setOf mimeMediaType | 支持的文档格式 |

# 表 9.1 续

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `finishes-default` | 1setof type2 enum | 应用于文档页的默认结束状态 |
| `finishes-supported` | 1setof type2 enum | 文档页可用的结束状态 |
| `generated-natural-language-supported` | 1setof nullLanguage | 支持的语言 |
| `ipp-versions-supported` | 1setof type2 keyword | 打印机对象支持的版本号 |
| `job-hold-until-default` | type3 keyword | name | 新任务的默认保持时间 |
| `job-hold-until-supported` | 1setof (type3 keyword | name) | 新任务支持的保持时间 |
| `job-priority-default` | integer (1:100) | 默认打印优先级 |
| `job-priority-supported` | integer (1:100) | 支持的最大任务优先级值 |
| `job-sheets-default` | type3 keyword | name | 打印任务时默认的作业页设置 |
| `job-sheets-supported` | 1setof (type3 keyword | name) | 支持的作业页设置 |
| `media-default` | type3 keyword | name | 打印任务时使用的默认介质 |
| `media-ready` | 1setof type3 keyword | name | 哪些介质已准备好打印 |
| `media-supported` | 1setof type3 keyword | name | 支持的介质类型 |
| `multiple-document-handling-default` | type2 keyword | 打印复份时的默认文档处理方式 |
| `multiple-document-handling-supported` | 1setof type2 keyword | 支持的文档处理类型 |
| `natural-language-configured` | naturalLanguage | 返回属性的配置语言 |
| `number-up-default` | integer (1:MAX) | 每个输出上打印的文档页数 |
| `number-up-supported` | 1setof integer(1:MAX) | rangeOfInteger(1:MAX) | 支持的份打（number-up）值 |
| `operations-supported` | 1setof type2 enum | 打印机对象支持的操作 |
| `orientation-requested-default` | type2 enum | 文档页的默认方向 |
| `orientation-requested-supported` | 1setof type2 enum | 支持的方向 |

# 表 9.1 续

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `pages-ranges-supported` | boolean | 打印文档时是否支持页码过滤 |
| `pdl-override-supported` | type2 keyword | IPP 属性是否覆盖打印文件中的命令 |
| `printer-accepting-jobs` | boolean | 打印机对象是否接受新任务 |
| `printer-name` | name(127) | 打印机对象的标识名称，例如 Laserjet |
| `printer-state` | type1 enum | 当前打印机状态 |
| `printer-state-reasons` | set1Of type2 keyword | 当前打印机状态的原因 |
| `printer-up-time` | integer (1:MAX) | 打印机运行的秒数 |
| `printer-uri-supported` | set1Of uri | 可用于访问打印机对象的 URI |
| `queued-job-count` | integer (0:MAX) | 该打印机队列中的任务数 |
| `sides-default` | type2 keyword | name | 任务的默认双面设置 |
| `sides-supported` | set1Of type2 keyword | 可用的双面设置 |
| `uri-authentication-supported` | set1Of type2 keyword | 相应 URI 支持的认证类型 |
| `uri-security-supported` | set1Of type2 keyword | 相应 URI 支持的安全类型 |

## `charset-configured` 属性

`charset-configured` 属性包含服务器文本属性的默认字符集。对于 CUPS 来说，通常是 `iso-8859-1`。

## `charset-supported` 属性

`charset-supported` 属性列出了支持的字符集。对于 CUPS，这将包含以下内容：

- `iso-8859-1`
- `iso-8859-2`
- `iso-8859-3`
- `iso-8859-4`
- `iso-8859-5`

```
iso-8859-6
iso-8859-7
iso-8859-8
iso-8859-9
iso-8859-10
iso-8859-13
iso-8859-14
iso-8859-15
us-ascii
utf-8
windows-874
windows-1250
windows-1251
windows-1252
windows-1253
windows-1254
windows-1255
windows-1256
windows-1257
windows-1258
```

## `compression-supported` 属性

`compression-supported` 属性列出了支持的文档压缩方法。对于 CUPS 1.1.x，此属性将包含单个关键字字符串 `none`。对于 CUPS，此属性将包含以下字符串：

```
none
deflate
gzip
```

## `copies-default` 属性

`copies-default` 属性指定了每个任务生成的默认份数。对于 CUPS 来说，此值始终为 1。

## `copies-supported` 属性

`copies-supported` 属性指定了打印机可以生成的最小和最大份数。对于 CUPS，最小始终为 1，最大值始终为 65。

## `document-format-default` 属性

`document-format-default` 属性指定了默认的文档格式。对于 CUPS 来说，该值始终是 `application/octet-stream`。

## `document-format-supported` 属性

`document-format-supported` 属性列出了支持的文档格式。对于 CUPS，此属性将包含以下：

- `application/pdf`
- `application/postscript`
- `application/gif`
- `application/jpeg`
- `application/png`
- `application/tiff`

## `finishings-default` 属性

`finishings-default` 属性指定了默认的结束状态。对于 CUPS 来说，该值见表 9.2。

## `finishings-supported` 属性

`finishings-supported` 属性列出了支持的结束状态。对于 CUPS 来说，该属性源自 Location。

# 表 9.2 结束状态

| 值 | 描述 |
|---|---|
| no-hold | 不保持任务——尽快处理。 |
| indefinite | 保持任务直到手动释放。 |
| day-time | 在每天早上 6 点到下午 6 点之间打印。 |
| evening | 在每天晚上 6 点到第二天早上 6 点之间打印。 |
| night | 在每天晚上 6 点到第二天早上 6 点之间打印。 |
| weekend | 在周末打印。 |
| second-shift | 在每天下午 6 点到午夜 12 点之间打印。 |
| third-shift | 在每天凌晨 12 点到早上 8 点之间打印。 |

## `job-sheets-default` 属性

`job-sheets-default` 属性指定了打印作业时默认的作业单（job sheets）。对于 CUPS，作业单被视为页眉（banner）和页脚（trailer），并被视为一组数组名称。默认值通常为“none”，但可以由管理员覆盖。表 9.4 列出了 CUPS 随附的标准作业单。

表 9.4 作单

| 名称 | 描述 |
| --- | --- |
| none | 不打印任何作业单。 |
| classified | 在顶部和底部打印带有粗体“**Classified**”字样的作业单。 |
| confidential | 在顶部和底部带有粗体“**Confidential**”字样的作业单。 |
| secret | 在顶部和底部带有粗体“**Secret**”字样的作业单。 |
| standard | 打印不带特殊标记的作业单。 |
| topsecret | 在顶部和底部带有粗体“**Top Secret**”字样的作业单。 |
| unclassified | 在顶部和底部带有粗体“**Unclassified**”字样的作业单。 |

## `job-sheets-supported` 属性

`job-sheets-supported` 属性列出了可用的作业单。对于 CUPS，此值派自 `/usr/share/cups/banners` 目录下的文件。

## `media-default` 属性

`media-default` 属性指定打印时使用的介质。它是介质尺寸、类型和源字段的汇总。在 CUPS 中，它镜像了打印机 PPD 文件中 `DefaultPageSize` 的值。

## `media-ready` 属性

`media-ready` 属性列出了哪些介质尺寸、类型和源已准备好打印。CUPS 不使用此属性。

## `media-supported` 属性

`media-supported` 属性列出了打印机支持的介质尺寸、类型和源。在 CUPS 中，此属性包含来自打印机 PPD 文件的 `InputSlot`、`MediaType` 和 `PageSize` 属性列表。

## `multiple-document-handling-default` 属性

`multiple-document-handling-default` 属性指定了打印多份副本时的默认多文档处理方式。表 9.5 列出了可以使用的关键字值。在 CUPS 中，默认值为 `separate-documents-uncollated-copies`。

表 9.5 多文档处理关键字

| 关键字值 | 描述 |
|---|---|
| `single-document` | 生成排序的副本（例如 1, 2, 1, 2, 2）。每个文档和副本都被视为单个输出流，第二个文档和/或副本将从上一个的地方继续。 |
| `separate-documents-uncollated-copies` | 生成未排序的副本（例如 1, 1, 1, 2, 2）。 |
| `separate-documents-collated-copies` | 生成排序的副本（例如 1, 2, 1, 2, 1）。作业中的所有文档都从新的一页开始。 |
| `single-document-new-sheet` | 生成排序的副本，但每个副本都从新的一页开始。这与 `single-document` 关键字类似，但结果是完整的文档可以单独处理，而不是将 N 份副本装在一起。 |

## `multiple-document-handling-supported` 属性

`multiple-document-handling-supported` 属性列出了支持的文档处理类型。对于 CUPS，这包括关键字 `separate-documents-uncollated-copies` 和 `separate-documents-collated-copies`。

## `natural-language-configured` 属性

`natural-language-configured` 属性包含服务器用于文本消息的默认语言。对于 CUPS，此属性通常设置为字符串 `en`，尽管这在 `cups.conf` 文件中可以进行更改。

## `number-up-default` 属性

`number-up-default` 属性指定了每个输出页面上打印的文档页数。对于 CUPS，此值始终为 1。

## `number-up-supported` 属性

`number-up-supported` 属性指定了支持的 number-up 值。对于 CUPS，这始终是数字 1、2 和 4。

## `operations-supported` 属性

`operations-supported` 属性列出了支持的操作代码。CUPS 1.1.x 列出了所有标准的 IPP 操作代码，但 `Print-URI` 和 `Send-URI` 除外。CUPS 1.2.x 列出了所有的 IPP 操作代码。

## `orientation-requested-default` 属性

`orientation-requested-default` 属性指定了文档中页面的默认方向。表 9.6 列出了支持的值。对于 CUPS，此属性的值始终为 3（纵向）。

表 9.6 方向值

| 值 | 描述 |
|---|---|
| 3 | 以纵向方向打印（不旋转）。 |
| 4 | 以横向方向打印（逆时针旋转 90 度）。 |
| 5 | 以反横向方向打印（顺时针旋转 90 度）。 |
| 6 | 以反纵向方向打印（旋转 180 度）。 |

## `orientation-requested-supported` 属性

`orientation-requested-supported` 属性列出了可用的方向。对于 CUPS，这所有 4 个方向值（3, 4, 5 和 6）。

## `pages-ranges-supported` 属性

`pages-ranges-supported` 属性指定了打印文档时是否支持页码过滤。对于 CUPS，此属性始终为 `true`。

## `pdl-override-supported` 属性

`pdl-override-supported` 属性指定服务器是否可以覆盖文档数据中的选项。对于 CUPS，此值始终为 `false`。

## `printer-is-accepting-jobs` 属性

`printer-is-accepting-jobs` 属性指定打印机是否正在接受作业。

## `printer-name` 属性

`printer-name` 属性提供了打印机的标识名称。

## `printer-state` 属性

`printer-state` 属性指定了打印机状态。CUPS 的状态值见表 9.7。

表 9.7 状态值

| 值 | 描述 |
| --- | --- |
| 3 | 空闲。 |
| 4 | 正在处理作业。 |
| 5 | 已停止。 |

## `printer-state-reasons` 属性

`printer-state-reasons` 属性包含了描述打印机状态的原因字符串。对于 CUPS，除了 `none` 之外，所有状态都包含信息、警告或错误。表 9.8 列出了状态字符串。
