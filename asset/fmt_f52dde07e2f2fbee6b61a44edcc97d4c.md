
```c
if (response != NULL) {
    for (attr = ippFindAttribute(response, "printer-name", IPP_TAG_NAME);
         attr != NULL) {
        attr = ippFindNextAttribute(response, "printer-name", IPP_TAG_NAME))
        puts(attr->values[0].string.text);
    }
    ippDelete(response);
} else {
    printf("无法获取打印机列表: %s\n",
           ippErrorString(cupsLastError(0)));
}
```

```c
/* 关闭与服务器的连接。 */
httpClose(http);
return (0);
```

# 优化你的请求

许多 IPP 操作都支持 `requested-attributes` 属性，该属性列出了客户端感兴趣的属性。IPP 服务器随后可以从响应中消除这些属性。这种消除可以提供更快、更及时的响应，并减轻服务器、客户端和网络的负载。

例如，通过 `requested-attributes` 可以使 `showprinter` 示例变得高效得多：

```
ippAddString(request, IPP_TAG_OPERATION, IPP_TAG_KEYWORD,
    "requested-attributes", NULL, "printer-name");
```

IPP 服务器随后将尝试限制响应，仅包含名为 `"printer-name"` 的属性。

> 注意：IPP 规范允许使用 `requested-attributes` 属性来限制响应。这种消除可以提供更快、更及时的响应，并减轻服务器，客户端和网络的负载。

## 总结

许多 IPP 操作都支持 `requested-attributes` 属性，该属性列出了客户端感兴趣的属性。IPP 服务器随后可以从响应中消除这些属性。这种消除可以提供更快、更及时的响应，并减轻服务器、客户端和网络的负载。

CUPS 提供了丰富的函数来管理 HTTP 响应。IPP 响应由 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1

CUPS 提供了丰富的函数来管理 HTTP 响应。IPP 响应由 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1

CUPS 提供了丰富的函数来管理 HTTP 响应。IPP 响应由 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1

# 第16章：为 CUPS 编写过滤器

## 什么是过滤器？

过滤器是用于一种格式转换为另一种格式的程序。本章描述了如何为 CUPS 编写过滤器，它是打印的核心。

CUPS 提供了许多转换格式的过滤器。图 16.1 显示了过滤器、打印驱动程序和后端之间的关系。

### 什么是过滤器？

HP-GL 和 HP-GL/2 是所谓的矢量格式。每个文件由一系列初始化命令和绘图命令组成。关于 HP-GL 的完整手册可以在开发者的网站找到：

```
http://www.developer-solutions.com/
```

大多数 CAD 应用生成用于打印的 HP-GL/2 文件和 PostScript 文件。

### hltops 过滤器

`hltops` 过滤器将 HP-GL 和 HP-GL/2 的图文件转换为 PostScript。当图文件包含 PS 命令时，可以使用 `fitplot` 选项进行匹配。如果使用了 `blackplot` 选项，过滤器将只输出黑白。

`hltops` 过滤器使用打印机的 PDF 文件来确定可用页面大小、打印区域和页边距，无论打印机支持颜色。

`hltops` 过滤器的输出通常通过到 `ppstops` 过滤器。

### imagagetops 过滤器

`imagagetops` 过滤器将图像文件转换为 PostScript。它可以按原始大小（默认），在使用 `scaling` 选项时按页面百分比缩放，或者在使用 `ppi` 选项时按分辨率缩放。可以使用 `page-label` 选项或通过 `cupsd.conf` 文件中的 `Classification` 指令添加标签。

该过滤器使用打印机的 PDF 文件来确定可用页面大小、语言级别以及是否为打印机产生 RGB 或灰度数据。图像数据对于 Level 1 PostScript 打印机是十六进制字符串，对于 Level 2 和 3 PostScript 打印机是 base85 编码字符串。

`imagagetops` 过滤器的输出通常直接发送到后端，因此生成的 PostScript 包含所有命令。在使用开启页标签或分类标记的光栅打印机时，`imagagetops` 的输出被管道到 `pstoraster` 以进行系列图像的转换。

> 注意：
> PostScript 打印机支持三种语言级别之一。1 级打印机代表了原始的 PostScript 打印机，例如 Apple LaserWriter。2 级打印机是目前最常用的 PostScript 打印机。3 级打印机于 2000 年底上市，并将在几年后主导 PostScript 打印机市场。
> 
> 每个语言级别都支持许多不同的功能，以及一种通用的核心语言。任何想要编写生成 PostScript 过滤器的程序都需要《Adobe PostScript 语言参考手册》，因为该手册是 Adobe 文档结构规范 (DSC) 规范。您可以在网上找到这些内容：
> 
> ```
> http://partners.adobe.com/asn/developer/technotes/main.html
> ```

### imagetoraster 过滤器

`imagetoraster` 将图像文件转换为一系列栅格图像。它可以将图像缩放为原始尺寸（默认值），或者在使用缩放选项时将其缩放为页面大小的百分比，或者根据您通过 `ppi` 选项指定的解析进行缩放。可以使用 `page-label` 选项创建标签，或者通过 `cupsd.conf` 文件中的 `Classification` 指令创建标签。

过滤器使用 PPD 文件来确定可用页面尺寸、打印区域以及发送到打印机驱动程序的栅格数据类型。PPD 文件中的颜色配置文件信息也会被使用；对于 CUPS 1.1，过滤器支持带有查找表的 CMY 变换矩阵，用于控制栅格数据的整体伽马和密度校正。在 CUPS 1.2 中，PPD 文件可以为每个分辨率、颜色模型和媒体类型指定 ICC 配置文件；这些配置决定了发送到打印机驱动程序的栅格数据的色彩空间。

`imagetoraster` 过滤器的输出被传递到打印机驱动程序，由驱动程序将栅格图像转换为打印页面。

> 注意：
> `imagetops` 和 `imagetoraster` 过滤器使用 `cupsimage` 库来读取和转换图像文件。该库支持对 BMP、GIF、JPEG、PhotoCD、便携 anymap（PBM, PGM, PNM, PPM）、SGI RGB、Sun Raster 和 TIFF 图像文件的读取。

### pdftops 过滤器

`pdftops` 过滤器基于 Derek B. Noonburg 的 Xpdf 软件，将 Adobe 便携文档格式 (PDF) 文件转换为 PostScript。它将 PDF 文档中的页面缩放到请求的页面尺寸。

过滤器使用打印机的 PPD 文件来确定可用页面尺寸、打印区域和打印机的语言级别。

`pdftops` 过滤器的输出被传递到 `pstops` 过滤器。

> 注意：
> PDF 格式可能是电子共享复杂文档最流行的格式，并正迅速成为印前和其他打印应用的标准。其流行的主要原因是其可移植性和开放性格式——PDF 可在任何地方用于任何用途。Apple 的 MacOS 使用 PDF 文件作为其打印架构的基础，GNOME 项目可能在桌面环境的最终版本中使用它。甚至此书的终稿校样也是通过 PDF 文件完成的！
> 
> Adobe 在线维护着 PDF 格式的公开规范：
> 
> ```
> http://partners.adobe.com/asn/developer/technotes/main.html
> ```
> 
> PDFZone 网站也是寻找 PDF 软件和信息的绝佳之地：
> 
> ```
> http://PDFZone.com
> ```

### pstops 过滤器

大多数打印文件都会通过 `pstops` 过滤器。它接收 PostScript 打印文件，将其拆分为页面，并使用必要的打印机命令、选项和胶接代码（glue）重新组合页面，以产生所需的打印作业。

通过 `pstops` 过滤器，您可以使用 `page-ranges` 选项打印页面范围，使用 `page-set` 选项打印奇偶数页，使用 `page-label` 选项和 `Classification` 指令生成页标签和分类标记，以及使用 `number-up` 选项将多个页面放在单个输出页面上。

过滤器使用打印机的 PPD 文件来确定可用页面尺寸以及打印区域和边距。PPD 文件还提供了打印机在作业和每个页面之前所需的命令和其他数据。

`pstops` 过滤器在输出到 PostScript 打印机时会计数信息（"PAGE:" 消息）。

`pstops` 过滤器的输出传递给 PostScript 打印机的后端，或者传递给非 PostScript 打印机的 `pstoraster` 过滤器。

## 第三部分 使用 CUPS 编程

> 注意：
> `pstops` 过滤器解码 PostScript 文件中的注释，以确定文档中每页的开始和结束。这些注释遵循 Adobe 文档结构规范 (DSC) 规范描述的格式，可以在网上获取：
> 
> ```
> http://partners.adobe.com/asn/developer/technotes/main.html
> ```
> 
> 如果您尝试打印没有这些注释的 PostScript 文件，`pstops` 过滤器会将该文件视为单页文件。它不支持页面过滤选项或页面计数。

### pstoraster 过滤器

`pstoraster` 过滤器将 PostScript 文件转换为用于打印机驱动程序的栅格图像。根据嵌入的 PostScript 和命令，过滤器可以为较小尺寸的喷墨打印机和 50 英寸宽绘图仪生成栅格数据。当前的过滤器 `pstoraster` 支持语言级别 1 到 3。

过滤器使用打印机的 PPD 文件来确定可用页面尺寸、打印区域以及发送到打印机驱动程序的栅格数据类型。PPD 文件中的颜色配置文件会被使用；对于 CUPS 1.1，过滤器支持带有查找表的 CMY 变换矩阵，用于控制栅格数据的整体伽马和密度校正。在 CUPS 1.2 中，PPD 文件可以为每个分辨率、颜色模型和媒体类型指定 ICC 配置文件；这些配置决定了发送到打印机驱动程序的栅格数据的色彩空间。

`pstoraster` 过滤器的输出被传递到打印机驱动程序，由驱动程序将栅格图像转换为打印页面。

> 注意：
> `pstoraster` 过滤器基于 Ghostscript 解释器和图形库。在前端，过滤器支持 CUPS 接口而非 Ghostscript 命令行选项。
> 
> 在后端，打印机驱动程序被单一栅格驱动程序取代。该栅格驱动程序生成适用于 CUPS 的栅格数据。`praster` 过滤器还包含了针对标准 GhostScript 发行版的修复。该项目可以在网上找到：
> 
> ```
> http://partners.adobe.com
> ```
> 
> 为 CUPS 文件过滤器
> 
> 该 GhostScript 发行版被多个 Linux 发行版使用，并包含了它们的补丁和修复。该发行版还包含一个适用于 CUPS 的 `praster` 版本，有助于减少磁盘空间需求。

过滤器将文本转换为 PostScript。通过它，您可以使用 `columns` 选项打印多列文本，使用 `prettyprint` 选项突出显示关键字和漂亮标题，以及使用 `wrap` 选项换行。`epi` 和 `lpi` 选项决定文本的大小。

过滤器使用打印机的 PPD 文件来确定可用页面尺寸以及打印区域和边距。PPD 文件还提供了可用字体列表。如果文本需要打印机上不可用的字体，则字体将嵌入文档中。

过滤器处理通常通过回车或退格字符实现的下划线和加粗覆盖方法。分页符换出当前页面。

当您对文本文件使用 `prettyprint` 选项时，过滤器使用 `CONTENT_TYPE` 环境变量来决定如何突出文件中的语法。这些规则目前硬编码在过滤器中。

`textops` 过滤器的输出传递给 `pstops` 过滤器，在发送打印机之前进行进一步处理。

- `textops` 过滤器设计用于支持一个通用的文本引擎和一个生成输出的语言模块。`textops` 过滤器提供了 PostScript 语言模块。在随后的第 17 章中，您将看到使用文本引擎构建用于惠普激光打印机的 PCL 语言模块。

## CUPS 过滤器架构

CUPS 过滤器构打印系统支持任何类型打印能力的核心。调度器选择过滤器将打印文件转换为可打印的形式。除了过滤器程序本身，调度器还会读取 MIME 类型和转换文件，这些文件描述了系统支持的文件类型和过滤器。

前节描述的过滤器列在 `mime.types` 和 `mime.conv` 文件中。这些文件使调度器能够确定打印文件的最低成本过滤方案。

每个过滤器通过管道传递给下一个过滤器，其他消息则写入标准错误文件。链中的第一个过滤器读取命令行上指定的文件。后续的过滤器必须从标准输入文件读取内容。

### 命令行参数

每个过滤器都使用继承自系统打印系统的命令行接口。每个过滤器恰好提供六或七个命令行参数：

```
printer job user copies options filename
printer job user title copies options
```

第一个过滤器带有七个参数运行，而链中第一个之后的每个过滤器只获得六个参数。这使得第一个过滤器可以直接读取打印文件，而每个额外的过滤器则从标准输入读取上一个过滤器的结果。

- `printer` 参数 (`argv[0]`) 是打印机队列的名称，即 `printer-name` 属性的值。

> 注意：
> Shell 解释器会将 `printer` 参数 (S0) 替换为 shell 脚本的名称。如果你在 shell 脚本中需要打印机名称，请使用下一节列出的相应环境变量。

- `job` 参数 (`argv[1]`) 提供正在打印任务的数字 ID。它是 `job-job-id` 属性的值。

- `user` 参数 (`argv[2]`) 提供与任务相关的用户名。它是 `job-job-originating-user-name` 属性的值。

- `title` 参数 (`argv[3]`) 提供与任务相关的名称或标题。它是 `job-job-name` 属性的值。

- `copies` 参数 (`argv[4]`) 提供打印的份数。它是 `job-number-copies` 属性的值。

- `options` 参数 (`argv[5]`) 是由空格分隔的任务模板属性的字符串表示。布尔属性在真值时提供为 "name"，假值时提供为 "!name"。其他属性对于单值属性以 "name=value" 形式提供，集合属性以 "name=value1,value2,...,valueN" 形式提供。可以使用 `cupsParseOptions()` 函数将此字符串转换为 CUPS 选项数组，

```c
int num_options;
cups_option_t *options;
...
num_options = 0;
options = NULL;
num_options = cupsParseOptions(argv[5], num_options, &num_options);
```

- `filename` 参数 (`argv[6]`) 仅提供给第一个过滤器。它指定要转换的打印文件。

> 注意：
> 所有过滤器都必须准备从标准输入读取打印文件。如果过滤器需要对文件进行随机访问，它必须将标准输入上的打印文件复制到临时文件。

### 环境变量

每个过滤器都会接收一组可以使用的固定环境变量。表 16.2 列出了这些环境变量。

#### 表 16.2 传递给 CUPS 过滤器的环境变量

| 名称 | 描述 |
| --- | --- |
| `CHARSET` | 客户端为此打印文件使用的字符集。 |
| `CLASSIFICATION` | 当前系统高分类级别，例如“unclassified（未分类）”。仅在使用时提供。 |
| `CONTENT_TYPE` | 原始文档格式，例如“application/postscript”。 |
| `CUPS_DATADIR` | CUPS 数据文件的位置。 |
| `CUPS_FONTPATH` | CUPS 字体文件的位置。 |
| `CUPS_SERVERROOT` | CUPS 配置文件的位置。 |
| `DEVICE_URI` | 输出设备 URI。 |
| `LANG` | 客户端为此打印文件使用的语言。 |
