
常用开关：

| 开关 | 功能 |
| --- | --- |
| `-d` | 显示进程数据重定位 |
| `-r` | 显示进程数据和函数重定位 |
| `-u` | 显示未使用的直接依赖项 |
| `-v` | 详细模式；打印所有信息 |

**名称：** ELF Library查看器
**页面引用：** 283
**作者/发布者：** Michael Pyne
**获取途径：** http://www.purinchu.net/software/elfviewer.php
**描述：** 用于显示目标 ELF 文件库依赖关系的图形化工具。库根据文件路径按层级显示，并位于单独的字段中。内置搜索工具允许数字取证人员快速查询并定位特定标识的文件，这些文件以红色文本显示。

![](img/aa19fd7b1fc75dc422144821b9c6657c_420_0.png)

# 396 Linux 系统恶意软件取证领域指南

名称：视觉化依赖遍历器 (Visual Dependency Walker)
页面引用：283-284
作者/发布者：Filippos Papadopoulos 和 David Sansome
获取途径：http://freecode.com/projects/visual.ldd
描述：用于显示目标 ELF 文件库依赖关系的图形化工具。库根据文件路径按层级显示，并在单独字段中显著显示。实用的右键菜单允许数字取证人员快速展开或折叠依赖树，或将树形保存到文本文件中。

![](img/aa19fd7b1fc75dc422144821b9c6657c_421_0.png)

名称：DepSpec
页面引用：284
作者/发布者：Kyle McFarland
获取途径：https://launchpad.net/depspec
描述：一种用于文件依赖分析的双窗格 GUI，可揭示导入的库、导出库以及相关的符号引用。DepSpec 可以处理 ELF 和 PE 文件。

![](img/aa19fd7b1fc75dc422144821b9c6657c_421_1.png)

# 第 5 章 文件识别与特征分析

名称：ELF 依赖遍历器 (ELF Dependency Walker)
页面引用：283-284
作者发布者：Peter Cheung
获取途径：http://code.google.com/p/elf-dependency-walker/
描述：一个功能丰富的 ELF 依赖分析工具，通过展开树形提供可选的视图。在树形模式下，可疑文件以层级树（或文件依赖关系）的形式显示，依赖项显示在右侧查看面板中。或者，图形模式允许数字取证人员将目标标本的文件依赖关系渲染为八种不同的图形布局，以提供对比视角。保存为便携网络图形 (.png) 图像。

![](img/aa19fd7b1fc75dc422144821b9c6657c_422_0.png)

## 提取符号和调试引用

| 名称：NM |
| --- |
| 页面引用：285 |
| 作者/发布者：GNU |
| 获取途径：GNU Binary Utilities (binutils)；Linux 发行版原生 |
| 描述：列出目标文件中符号的命令行工具。 |
| 开关 | 功能 |
| --- | --- |
| `-a` | 显示仅调试器的符号 |
| `-A` | 在每个符号之前显示输入文件的名称。在将低级符号解码为用户级符号的“反混(Demangle)”模式下 |
| `-c` | 显示动态符号而非标准符号 |
| `-g` | 仅显示外部符号 |
| `-1` | 使用调试信息定位文件名 |
| `-n` | 按地址对符号进行数值排序 |

| 名称：Gedit 符号浏览器插件 |
| --- |
| 页面引用：291 |
| 作者/发布者：Micah Carrick |
| 获取途径：http://www.micahcarrick.com/gedit-symbol-browser-plugin.html |
| 描述：一种通过 gedit 利用的图形化符号提取和分析工具。 |

![](img/aa19fd7b1fc75dc422144821b9c6657c_423_0.png)

## 文件元数据

| 名称：Exiftool |
|------|
| 页面引用：294 |
| 作者/发布者：Phil Harvey |
| 获取途径：http://www.sno.phy.queensu.ca |
| 描述：一个强大的命令行元数据工具，可以从 PDF、MS Office 等其他类型获取信息。常用开关： |

| 开关 | 功能 |
| --- | --- |
| `-q` | 静默输出 |
| `-r` | 递归处理 |
| `-s` | 简短输出 |
| `-S` | 非常简短输出 |
| `-w` | 输出到文件 |

## ELF 分析

| 名称：Binutils |
|------|
| 页面引用：276 |
| 作者/发布者：GNU |
| 获取途径：www.gnu.org/binutils |
| 描述：一组处理 ELF 文件的工具，包括 `nm` 等。 |

| 名称：Elfutils |
|------|
| 页面引用：276 |
| 作者/发布者：Ulrich Drepper |
| 获取途径：http://www.fedor.org/elfutils |
| 描述：一组用于处理 ELF 文件的工具： |

| 工具 | 功能 |
| --- | --- |
| `-a` | 所有 |
| `-h` | 显示文件头 |
| `-l` | 显示程序头 |
| `-s` | 显示节头 |
| `-t` | 显示节详情 |
| `-e` | 显示头部详情 |
| `-s` | 显示符号 |
| `--dyn-syms` | 显示动态符号 |
| `--notes` | 显示注释 |
| `-V` | 显示文件版本信息 |

| `objdump` | 显示 ELF 信息 |
| `size` | 显示节大小 |

恶意软件取证领域指南

| 名称：Greadelf |
|------|
| 页面引用：276 |
| 作者/发布者：Ashok Das |
| 获取途径：https://code.google.com/p/greadelf |
| 描述：用于 `readelf` 的图形化工具，提供 ELF 视图。 |

| 名称：nm | 列出文件中的符号。 |

![](img/aa19fd7b1fc75dc422144821b9c6657c_425_0.png)

| 名称：ERESI 逆向工程界面 |
|------|
| 页面引用：308 |
| 作者/发布者：Julien Vanague 和 ERESI 团队 |
| 获取途径：http://www.eresi.org |
| 描述：一个面向逆向工程的多架构二进制分析框架。该框架包含以下工具：`elf`, `kdbg`, `etrace`, `evista`, `kersch`。 |

| 名称：Readelf |
|------|
| 页面引用：277, 305, 308 |
| 作者/发布者：GNU |
| 获取途径：www.gnu.org/binutils |
| 描述：显示 ELF 文件结构和内容的命令行工具。 |

| 开关 | 功能 |
| --- | --- |
| `-d` | 显示进程数据重定位 |
| `-r` | 显示进程数据和函数重定位 |
| `-u` | 显示未使用的直接依赖 |
| `-v` | 详细模式；打印所有信息 |

## 恶意文档分析

## 恶意文档分析：PDF 文件

| 名称：Origami |
|------|
| 页面引用：341-344 |
| 作者/发布者：Guillaume Delugré, Frédéric Raynal (贡献者) |
| 获取途径：http://esec-lab.sogei.com/doctypeindex.php?pages=Origami; http://google.com/origami-pdf |
| 描述：Origami 是一个用 Ruby 编写的框架，用于解析和分析恶意 PDF 文档，并为了研究目的生成恶意 PDF。Origami 包含一系列 Ruby 解析器——核心脚本（如下所示）、脚本和 Walker（用于检查可疑 PDF 文件的 GTK GUI 界面，如图）。 |

| 脚本 | 功能 |
| pdfscan.rb | 解析目标 PDF 文件标本的内容和结构 |
| extractjs.rb | 从目标 PDF 文件标本提取 JavaScript |
| detectsig.rb | 检测目标 PDF 文件标本中的恶意签名 |
| pdfclean.rb | 从目标 PDF 文件标本提取元数据 |
| printmetadata.rb | 从目标 PDF 文件标本提取文件元数据 |

![](img/aa19fd7b1fc75dc422144821b9c6657c_426_0.png)

# Linux 系统恶意软件取证野外指南

名称：Jsunpack-n
页码：344
作者/分发者：Blake Harstein
获取地址：https://google.com/p/jsunpack-n; Jsunpack: http://jsunpack.jeek.org/dec/go
描述：Jsunpack 是“通用 JavaScript 解包器”，是一套用 Python 编写的工具集，用于模拟浏览器行为并向 URL 通知。虽然它是研究人员调查漏洞的强大工具，但 Jsunpack 也是数字调查员喜爱的工具，用于识别客户端浏览器漏洞、检查 PDF 文件并提取 JavaScript。在图所示，`*pdf.py*` 脚本用于从可疑 PDF 文件中提取 JavaScript 并将其写入单独的文件中以便进一步分析。

```
malwarelab/malwarelab/jsunpack-n.py

/home/malwarelab/Desktop/merry_christmas_UNZIPPED.pdf

processing /home/malwarelab/Desktop/merry_christmas_UNZIPPED.pdf!!!

parsing /home/malwarelab object(t 26 0

failed to decompress

Found JavaScript in 31 0 (3106 bytes)

children [

  tags ['Filter', ''], ['FlatDecode', ''], ['Length', '1213']\]

indata = <<Filter/[FlatDecode]/Length

1213>>streamVmG8YJ) [pB8jIO=vYtp?>=5ba==9<s'gt]-gghlIwwhY

Wrote JavaScript (9085 bytes -- 5979 headers / 3106 code) to file

/home/malwarelab/Desktop/merry_christmas_UNZIPPED.pdf.out
```

名称：PDFMiner
页码：347
作者/分发者：Yusuke Shinyama
获取地址：http://www.unixuser.org/~euke/python/pdfminer/index.html
描述：Python PDF 解析器和分析器。PDF Miner 包含许多 Python 脚本用于提取 PDF 文件内部的文本数据：`pdf2txt.py`（从 PDF 文件提取文本内容）和 `dumppdf.py`（以伪 XML 格式显示 PDF 文件的内部内容）。

## 第 5 章 文件识别与分析

|  way | Peepdf |
| :--- | :--- |
| 页码 | 347 |
| 作者/分发者 | Jose Miguel Esparza |
| 获取地址 | http://google.com/invoked/peepdf |
| 描述 | 命令行 PDF 解析器和分析器。Peepdf 可以调用并指向目标文件（如图所示），或使用“-i”选项创建一个“PPDF shell”，在其中可以直接查询。 |

```
labMalwareLab=~/peepdf.py -f Beneficial-medical-programs.pdf

File: Beneficial-medical-programs.pdf

MD5: 3d2d3b618c0878bd332ee29bbc4c0

SHA1: a447a8bc7f12e5178be3e3bl8f54af4af51

Size: 32860 bytes

Version: 1

Binary: True

Linearized: False

Encrypted: False

Updates: 0

Objects: 14

Streams: 4

Comments: 0

Errors: 0

Version: 0

Info: No

Objects: [14]; [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 13, 14, 64]

Streams: (4); [8, 64, 10, 14]

Encoded: (2); [64, 10]

Decoding error: (1); [64]

Suspicious Elements:

/AcroForm: [1]

/OpenAction: [1]

/JS: [11]

/Javascript: [11]
```

| 选项 | 功能 |
| :--- | :--- |
| metadata | 显示目标 PDF 元数据，包括创建日期、修改日期、生产者、创建者、关键词、作者或其他项目。 |
| object | 显示目标对象在解码和解密后的内容 |
| offsets | 显示目标文件的物理结构 |
| open | 打开并解析目标文件 |
| rawobject | 在不进行解码和解密的情况下显示目标对象的内容 |
| rawstream | 显示目标文件中的对象引用或对象 |
| references | 在目标文件中搜索指定的字符串或十六进制字符串 |
| stream | 显示目标流在解码和解密后的内容 |

# Linux 系统恶意软件取证野外指南

名称：Malzilla
页码：351
作者/分发者：Boban Spasic aka chubby
获取地址：http://malzilla.sourceforge.net/downloads.html
描述：Malzilla 由恶意软件猎寻工具的开发者开发，通常用于恶意软件研究人员导航潜在的恶意 URL，以探测恶意及相关产物的内容。然而，Malzilla 具有多种解码和 shellcode 分析功能，使其成为数字调查员工具箱中探索恶意 PDF 文件的必备工具。截至本文编写时，该工具尚未在 Linux 上安装和运行；必须先在分析系统中安装 WINE 或 CrossOver。

![](img/aa19fd7b1fc75dc422144821b9c6657c_429_0.png)

名称：Hachoir-utid
页码：357
作者/分发者：Victor Wiener
获取地址：https://bitbucket.org/hachoir/parser/hachoir-utid
描述：基于 hachoir-parser，hachoir-utid 是一种二进制文件探索工具，可以解析许多类型的文件，包括 OLE 文件。

## 第 5 章 文件识别与分析

名称：Hachoir-wx
页码：271, 357
作者/分发者：Victor Steiner
获取地址：https://bitbucket.org/hachoir/wiki/hachoir-wx
描述：基于 wx 的 hachoir GUI，使数字调查员能够解析包括 OLE 文件在内的二进制文件。

```
https://bitbucket.org/hachoir/blob/docs/hachoir.md
```

```
d0 cf 11 e0 e8 b1 0a 01 00 00 00 00 03 ff ff
00 00 00 00 00 00 00 ff ff ff ff ff
23 00 00 00 00 00 00 00 ff ff ff ff ff
00 00 00 00 00 00 00 00 ff ff ff ff ff
ff ff ff ff ff ff ff ff ff ff ff ff
ff ff ff ff ff ff ff ff ff ff ff ff
ff ff ff ff ff ff ff ff ff ff ff ff
ff ff ff ff ff ff ff ff ff ff ff ff
```

```
| 地址 | 名称 | 类型 | 大小 |
| :--- | :--- | :--- | :--- |
| 0000008.0 | header/ | header | 00000068.0 |
| 0000004.0 | difat/ | Difat | 0000420.0 |
| 0000438.0 | property/ | Property | 00000510.0 |
| 0000448.0 | sfat/ | Sectfat | 00000510.0 |
| 0000448.0 | property(1)/ | Property | 00000120.0 |
| 0000458.0 | property(2)/ | Property | 00000120.0 |
| 0000458.0 | property(3)/ | Property | 00000120.0 |
| 0000468.0 | property(4)/ | Property | 00000120.0 |
| 0000468.0 | property(5)/ | Property | 00000120.0 |
```

# Linux 系统恶意软件取证野外指南

名称：pyOLEscanner

页码：357

作者/分发者：Giuseppe 'Evilcrly' Bonfa

获取地址：https://github.com/Evilcrly/PythonScripts

描述：用于筛选 OLE 文件恶意性的 Python 脚本，包括嵌入的可执行文件、API 引用、shellcode 和其他产物。

```
malwareLab|~$pyOLEscanner$ python pyOLEscanner.py Discussions.doc
```
