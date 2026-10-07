
| job-detailed-status-messages | 1setof text(MAX) | 可读状态消息日志 |

| job-document-access-errors | 1setof text(MAX) | 可读文档访问错误消息日志 |

| job-until | type3 keyword | 名称 | 任务的挂起条件（如果有） |

| job-impressions | integer (@:MAX) | 打印任务中的打印面数 |

| job-impressions-completed | integer (@:MAX) | 已打印的面数 |

| job-k-octets | integer (@:MAX) | 文档文件中的字节数 |

| job-k-octets-processed | integer (@:MAX) | 已处理的字节数 |

| job-media-sheets | integer (@:MAX) | 打印任务中的介质页数 |

| job-media-sheets-completed | integer (@:MAX) | 已打印的介质页数 |

| job-message-from-operator | text (127) | 来自打印员的可读文本消息 |

#### 表 10.4 续

| 名称 | 类型 | 描述 |

|---|---|---|

| job-more-info | uri | 通过 浏览器获取更多信息的 URL |

| job-priority | integer (1:100) | 打印任务的优先级 |

| job-sheets | type3 keyword | 名称 | 任务页 |

| job-state-message | text (MAX) | 可读状态消息 |

| media | type3 keyword | 名称 | 介质尺寸、类型或来源 |

| multiple-document-handling | type2 keyword | 如何处理文档副本 |

| number-of-documents | integer (:MAX) | 任务中的文档文件数量 |

| number-of-intervening-jobs | integer (:MAX) | 在此任务之前调度打印的任务数 |

| number-up | integer (1:MAX) | 每个输出页放置的文档页数 |

| orientation-requested | type2 enum | 输出的方向 |

| output-device-assigned | name(127) | 分配任务的输出设备名称 |

| page-ranges | setOf rangeOfInteger | 打印任务中的哪些页面 |

| print-quality | type2 enum | 输出质量 |

| printer-resolution | resolution | 输出分辨率 |

| sides | type2 keyword | 打印单面还是双面 |

## copies 属性

`copies` 属性指定了任务将生成的副本数。`copies` 仅适用于文档文件，而不适用于与任务关联的任务页（job sheets）。`copies` 属性的值必须在打印机 `copies-supported` 属性定义的范围内。

## date-time-at-completed 属性

`date-time-at-completed` 属性提供了任务完成、取消或中止的日期和时间。

CUPS 不提供此属性。

## date-time-at-creation 属性

`date-time-at-creation` 属性提供了任务创建的日期和时间。

CUPS 不提供此属性。

## date-time-at-processing 属性

`date-time-at-processing` 属性提供了任务处理的日期和时间。

CUPS 不提供此属性。

## finishings 属性

`finishings` 属性指定了此任务的后续动作。可用关键字由打印机的 `finishings-supported` 属性定义。

## job-detailed-status-messages 属性

`job-detailed-status-messages` 属性提供了有关任务状态的可读文本列表。

CUPS 不提供此属性。

## job-document-access-errors 属性

`job-document-access-errors` 属性提供了检索文档时遇到的任何错误的可读文本消息。

CUPS 1.1 不提供此属性。

CUPS 1.2 提供 HTTP 和 FTP 错误。

## job-until 属性

`job-until` 属性指定了任务的挂起条件。

## job-impressions 属性

`job-impressions` 属性提供了打印任务中的打印面数。与 `job-media-sheets` 属性不同，因为 `job-media-sheets` 统计的是打印页数。

CUPS 不提供此属性。

## job-impressions-completed 属性

`job-impressions-completed` 属性提供了已打印的面数。与 `job-media-sheets-completed` 属性不同，因为 `job-media-sheets-completed` 统计的是已打印的页数。

CUPS 不提供此属性。

## job-k-octets 属性

`job-k-octets` 属性提供了文档文件中的字节数。CUPS 在向任务中添加额外文档时更新此值。

## job-k-octets-processed 属性

`job-k-octets-processed` 属性提供了已处理的字节数。CUPS 不提供此属性。

## job-media-sheets 属性

`job-media-sheets` 属性提供了打印任务中的介质页数。与 `job-impressions` 属性不同，因为 `job-impressions` 统计的是打印的面数。例如，一个包含 20 页的典型双面打印任务的 `job-media-sheets` 值为 10，`job-impressions` 值为 20。

CUPS 不提供此属性。

## job-media-sheets-completed 属性

`job-media-sheets-completed` 属性提供了已打印的介质页数。与 `job-impressions-completed` 属性不同，因为 `job-impressions-completed` 统计的是已打印的面数。

CUPS 不提供此属性。

## job-message-from-operator 属性

`job-message-from-operator` 属性提供了来自打印员的可读文本消息。这可能包含类似“任务正挂起，直到我们需要一卷新的光纸”的消息。

CUPS 不提供此属性。

## job-priority 属性

`job-priority` 属性指定打印任务的优先级。任务优先级用于控制队列中打印任务的顺序；优先级越高越打印。

CUPS 使用任务优先级来确定任务在队列中的位置，但不会停止已经在已经在队列中的低优先级任务。

## job-sheets 属性

`job-sheets` 属性指定打印任务时使用的横幅页（banner pages）。

CUPS 支持 1 或 2 张作业单。第一张单在任务中的文档之前打印，第二张单在任务中的文档之后打印。由于 CUPS 中作业单的实现方式，在任务创建后无法更改 `jobsheets` 属性。

## job-state-message 属性

`job-state-message` 属性为任务提供一种人类可读的状态消息。

CUPS 目前不支持此属性。

## media 属性

`media` 属性指定任务的介质尺寸、类型或来源。

CUPS 允许每个任务接受 1 个或多个属性值，以便指定所有三个介质值。

## multiple-document-handling 属性

`multiple-document-handling` 属性指定如何处理文档副本。本质上，此属性控制副本是否进行装订。

CUPS 支持 `multiple-documents-collated-copies` 和 `multiple-documents-uncollated-copies` 值。

## number-of-documents 属性

`number-of-documents` 属性提供任务中文档文件的总数。

CUPS 将作业单包含在计数中。

## number-of-intervening-jobs 属性

`number-of-intervening-jobs` 属性提供在此任务之前安排打印的任务数。

CUPS 不支持此属性。

## number-up 属性

`number-up` 属性指定每个输出页面放置的文档页数。

CUPS 支持每面或每张纸打印 1、2 或 4 页。

## orientation-requested 属性

`orientation-requested` 属性指定输出的方向。该值必须必须是打印机 `orientation-supported` 属性中的值之一。

## output-device-assigned 属性

`output-device-assigned` 属性提供分配给任务的输出设备名称。

CUPS 不提供此属性。

## page-ranges 属性

`page-ranges` 属性指定打印任务中的哪些页面。集合中的页范围必须是唯一的，并适用于任务中的所有文档。例如，如果指定的 `page-ranges` 属性值为 1–4，则将在每个文档中打印第 1–4 页，或者只打印第一个文档的前 4 页。

CUPS 按升序打印页范围，指定值为 7–8 的 `page-ranges` 属性将打印第 1、2、7 和 8 页。

## print-quality 属性

`print-quality` 属性指定输出质量。该值必须必须是打印机 `print-quality-supported` 属性中的值之一。

CUPS 不支持此属性。

## printer-resolution 属性

`printer-resolution` 属性指定打印任务的输出分辨率。该值必须是打印机 `printer-resolution-supported` 属性中的值之一。

## sides 属性

`sides` 属性指定是单面还是双面输出。该值必须是打印机 `sides-supported` 属性中的值之一。

## CUPS 属性

CUPS 定义了若干由 CUPS 文件过滤器使用的新模板属性。表 10.5 定义了 CUPS 属性。

| 名称 | 类型 | 描述 |

|---|---|---|

| blackplot | boolean | 是否仅用黑色墨水打印 HP-GL/2 绘文件 |

| brightness | integer (0:200) | 打印任务的整体亮度 |

| columns | integer (1:4) | 文件的列数 |

| cpi | type2 enum | 打印文本文件时每英寸字符数 |

| fitplot | boolean | 是否将 HP-GL/2 绘文件缩放到介质尺寸 |

| gamma | integer (1:10000) | 打印任务的整体  校正 |

| hue | integer (-180:180) | 应用于图片的色彩旋转 |

| job-billing | text(MAX) | 任务计费信息 |

| job-originating-host-name | name(MAX) | 创建任务的主机名或 IP 地址 |

| lpi | type2 enum | 打印文件时每英寸行数 |

| page-bottom | integer (0:MAX) | 打印文本文件时的页边距（磅） |

| page-label | text(MAX) | 显示在每个打印页顶部底部的标签 |

| page-left | integer (0:MAX) | 打印文本文件时的左边距（磅） |

| page-right | integer (0:MAX) | 打印文本文件时的右边距（磅） |

| page-set | type2 keyword | 每个文档中要打印的页面 |

## 表 10.5 继续

| 名称 | 类型 | 描述 |

|---|---|---|

| page-top | integer (0:MAX) | 打印文本文件时的顶边距（磅） |

| penwidth | integer (0:MAX) | HP-GL/2 绘文件中的默认笔宽 |

| position | type2 keyword | 图片在页面上的位置 |

| ppi | integer (1:MAX) | 图片每英寸像素分辨率 |

| prettyprint | boolean | 是否对文本文件应用格式化 |

| saturation | integer (0:200) | 文件的饱和度 |

| scaling | integer (1:1000) | 应用于图片的缩放 |

| wrap | boolean | 在文本文件中换行 |

## blackplot 属性

`blackplot` 属性指定 HP-GL/2 绘文件是完全用黑色渲染（`blackplot=true`）还是使用文件中指定的颜色。此属性不支持其他类型的文件。默认值为 false。

## brightness 属性

`brightness` 属性以百分比指定输出的整体亮度。亮度为 100 为正常，200 为亮度倍，50 为亮度减半。默认值为 100。

亮度通过以下函数等应用于青色、红色和黄色：

```
f(x) = brightness / 100 * x
```

## columns 属性

`columns` 属性指定打印文本文件时生成的列数。此属性不支持其他类型的文件。默认值为 1。

## cpi 属性

`cpi` 属性指定打印文本文件时每英寸字符数。此属性不支持其他类型的文件。支持的值为 10、12 和 17。默认值为 10。

## fitplot 属性

`fitplot` 属性指定 HP-GL/2 绘文件缩放到所选介质（`fitplot=true`），还是使用文件中指定的物理比例（`fitplot=false`）。此属性不支持其他类型的文件。默认值为 false。

只有当 HP-GL/2 文件包含 PS（Plot Size）命令时，缩放才有效。

## gamma 属性

`gamma` 属性指定输出的亮度校正。值 1000 表示不校正，2000 和 500 分别生成更亮和更暗的输出。默认值为 1000。

Gamma 通过以下函数应用于红色、绿色和蓝色值（或灰度输出的亮度）：

```
f(x) = x^(1000/gamma)
```

## hue 属性

`hue` 属性在打印图像文件时指定色彩旋转。此属性不支持其他类型的文件。默认值为 0。表 10.6 显示了不同色值对主色的影响。

| 表 10.6 色相对色彩的影响 |

| 颜色 | hue=-45 | hue=45 |

|---|---|---|

| 红色 | 紫色 | 黄橙色 |

| 绿色 | 黄绿色 | 蓝绿色 |

| 黄色 | 橙色 | 绿黄色 |

| 蓝色 | 天蓝色 | 紫色 |

| 品红色 | 靛蓝 | 绯红色 |

| 青色 | 蓝绿色 | 浅蓝 |

是否启用主机名解析。localhost 地址 (127.0.0.1) 始终解析为名称“localhost”。

此属性是只读的。

## 1pi 属性

`1pi` 属性指定打印文本文件时每英寸的行数。此属性对所有其他类型的文件均忽略。目前仅支持值 6 和 8。默认值为 6。

## page-bottom 属性

`page-bottom` 属性指定以点（points）为单位的底边距（72 点等于 1 英寸）。默认值是打印机 PPD 文件定义的设备物理边距。

## page-label 属性

`page-label` 属性提供一个文本值，放置在每页的页眉和页脚中。如果服务器设置了分类，则该分类将在页标签之前打印，页标签用于保存与作业分类相关的注意事项。默认情况下没有页标签。

## page-left 属性

`page-left` 属性指定以点（points）为单位的左边距（72 点等于 1 英寸）。默认值是打印机 PPD 文件定义的设备物理边距。

## page-right 属性

`page-right` 属性指定以点（points）为单位的右边距（72 点等于 1 英寸）。默认值是打印机 PPD 文件定义的设备物理边距。

## page-set 属性

`page-set` 属性指定打印哪些页面。支持的关键字见表 10.7。默认值为 all（所有）。

### 10.7 Page设置关键字

| 关键字 | 描述 |

| :--- | :--- |

| all | 打印所有页面 |

| even | 仅打印偶数页 |

| odd | 仅打印奇数页 |

## page-top 属性

`page-top` 属性指定以点（points）为单位的上边界（72 点等于 1 英寸）。默认值是打印机 PPD 文件定义的设备物理边距。

## penwidth 属性

`penwidth` 属性指定打印 HP-GL 文件时以微米（micrometers）为单位的默认笔宽（1000 微米 = 1 毫米）。此属性忽略所有其他类型的文件，并在使用 PW（笔宽）命令的 HP-GL 文件中会被覆盖。默认值为 1000 微米。

## position 属性

`position` 属性指定图像文件在介质上的位置。此属性对所有其他类型的文件均忽略。表 10.8 列出了支持的关键字。默认值为 center（中心）。

### 10.8 Position关键字

| 关键字 | 描述 |

| :--- | :--- |

| center | 图像在页面居中 |

| top | 在页面顶部居中打印图像 |

| left | 在页面左侧居中打印图像 |

| right | 在页面右侧居中打印图像 |

| top-left | 在页面左上角打印图像 |

| top-right | 在页面右上角打印图像 |

| bottom | 在页面底部居中打印图像 |

| bottom-left | 在页面左下角打印图像 |
