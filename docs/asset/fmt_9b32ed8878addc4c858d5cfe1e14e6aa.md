
- Hard Disk Images—硬盘在此处映射。

- Serial Ports—串口在此处映射。

Dosemu 是为 root 用户设置的。如果你想让 Linux 上的其他用户使用 DOS，请编辑 `/etc/doseemu.conf` 以包含以下内容：

```
root all
c all
```

关于 doseemu 的信息，请访问 http://www.doseemu.org。

## 运行 Windows 和 Macintosh 应用程序

虽然 Red Hat Linux 系统本身没有提供运行 Microsoft Windows 或 Macintosh 操作系统的软件，但你可以为了这些目的添加几个仿真包。WINE 和 Bochs 可运行 Windows 95 应用程序。ARDI 可以运行 Macintosh 程序。

### WINE

WINE 项目 (http://www.wine) 似乎是运行针对 Windows 应用程序中最有支持的项目。WINE 并不是模拟器，它并没有模拟整个 Windows 操作系统。相反，通过实现 Win32 应用程序接口 (API) 和 Windows 3.x 接口，WINE 项目更多是一个兼容层。

除了开发软件，WINE 项目还维护了一个在 Windows 下运行的应用程序数据库。列出了超过 1000 个应用程序，尽管许多只能部分运行。重点是，应用程序列表正在不断增长，并且特别关注运行重要的 Windows 3.1、95 和 98 应用程序。

### Bochs

Bochs 是一种 PC 仿真软件，可以运行 DOS、Minix 2.0 和 Windows 95 应用程序。尽管以前需要支付少量费用，但在 2000 年 3 月，Bochs 被 MandrakeSoft (http://www.linux-mandrake.com) 收购，该公司将其开源。Bochs 开发者声称以下 Windows 操作系统应用程序可以在 Bochs 中运行：

- Access 97

- CorelDRAW 7

- Excel 97

- Lotus 1-2-3 97

- Word 97

- PowerPoint 97

## 188 第二部分 + 使用红帽 Linux 

- ✦ Quattro Pro 7

- ✦ WordPerfect 7

你可以从 TUCOWS 网站（http://www.tucows.com- 等，不，应该是 (http://www.tucows.com)）下载 Bochs。

### ARDI Executor

除了能让你在 PC 上运行许多流行的 Macintosh 应用程序之外，由 ARDI 公司开发的 ARDI Executor (http://www.ardi.com) 还允许你能够使用 Mac 格式的软盘和各种 Mac 驱动器工作。该软件是收费的（Linux 版本 75 美元，学生仅需 35 美元）。你可以从 http://www.ardi.com/download.html 下载免费试用版。

ARDI 还维护了一份兼容的 Mac 软件列表。列出了多数百种 Mac 应用程序。每个应用程序都用颜色标记（绿色、黄色、橙色、红色或黑色），以指示该软件在 ARDI 下的运行情况。绿色和黄色分别表示完全可用和基本可用。橙色表示大部分不可用。红色意味着无法运行，因为需要 ARDI 中尚未实现的功能。简单来说，列出的应用程序有三分之二是绿色或黄色。

## 总结

在直接为 Linux 和其他 UNIX 系统编写的应用程序、移植到 Linux 的应用程序以及可以在仿真中运行的应用程序之间，有数百个可以使用红帽 Linux。互联网上有许多地方可以下载 Linux，还有更多可以通过 CD 购买。

为了简化安装和管理 Linux 应用程序，红帽开发了红帽包管理器 (RPM)。使用为 RPM 开发的工具（如 `rpm` 命令），你可以轻松地安装、删除和查询各种 格式的 Linux 软件包。

在可以在 Linux 中运行的应用程序类型中，为 X Window 系统创建程序提供了最大的兼容性和灵活性。然而，使用仿真软件，可以运行适用于 DOS、Windows 95/98 以及 Macintosh 操作系统的应用程序。

# 第6 章

使用红帽 Linux 发布

## 本章

- 选择红帽 Linux 作为你的发布平台

- 使用 Groff 创建文档

- 使用商业文字处理器

- 使用红帽 Linux 打印文档

- 使用 ghostscript 和 Acrobat 显示

- 进行图形处理

- 使用 SANE 驱动的扫描仪

作为一个桌面系统，操作系统必须能够很好地完成至少一项任务：生成文档。并不是意外的是，在 Windows 上，Word（现已集成到 Office 中）是微软桌面成功的基。许多人购买第一台电脑是为了编写和格式化文档。

开箱即用，红帽 Linux 包含了生成文档的工具，这些工具大多是旧的基于文本的。许多技术人员使用这些工具（如 Groff 和 LaTeX）感到相当满意。对于那些想要更友好的文字处理的人来说，这里也有提供图形化、GUI 界面的文字处理应用程序。

在本章中，我将介绍使用红帽 Linux 作为发布平台的优缺点。我包含了基于文本和 GUI 的文档准备软件描述，它们要么自带，要么作为插件可用（通常价格合理）。我还描述了用于打印和显示文档的工具、用于处理各种格式图像的软件以及使用扫描仪。

### 选择红帽 Linux 作为你的发布平台

免费发布平台的吸引力对你可能和免费操作系统一样诱人。想象一下，每次微软推出新版本的 Office 都要花费数百美元。那么，你打算尝试吗？

![](img/176fafece2d30daee750bc078e898ee4_220_0.png)

## 190 部分 + 使用红帽 Linux

答案是肯定的……也许吧。成千上万的人使用 Linux 和其他 UNIX 系统作为生成文档的唯一手段。特别是软件开发者、大学生和其他技术人员对使用 Linux 提供的某些工具创建和发布文档感到相当满意。

在你跳入红帽 Linux 的“水池”之前，你可能想确保里面有水。红帽 Linux 并不是所有人的发布平台——至少目前不是。

（注：原文中存在大量重复的 OCR 错误，已根据文档工程师逻辑进行去重和清理）

#192 第二部分 使用红帽系统 Linux

你可以在《StarOffice 战争》中读到某人将小型办公室的 Windows 95/98 系统替换为 Linux 和 StarOffice 的经历。该文档位于：http://users.smileys.net/~leonb/StarOffice-wars.html。

交叉引用

## 5. 你是否习惯于调整事物以使其正常工作？

在使用 Groff 或 LaTeX 时，为了获得正确的格式，你通常需要重新格式化几次。这涉及到使用如 Ghostview 等工具（运行可能很慢），或者反复在打印机处往返。你可能还想编写脚本来运行你的格式化和打印命令。这需要一些调整。如果你，或者需要使用你所建立的文档系统的人不擅长调整，你可能更倾向于使用商业文字处理器。并排运行 LaTeX（编辑器）和 Ghostview（查看器）等工具可以让你更接近所见即所得（WYSIWYG）的体验。

## 6. 你是否需要特殊功能，例如色彩分色？

大多数高级出版功能在 Red Hat Linux 中尚无法实现。例如，一些专业出版人员已经指出，目前没有 Linux 工具可以进行色彩分色或某些高级照片处理操作。

### Linux 出版的属性

传统出版工具的某些属性使得它们特别适用于某些类型的文档出版。如前所述，Groff 和 LaTeX（基于 Tex）随 Red Hat Linux 一起提供，并在技术人员中非常流行。人们之所以青睐传统的 UNIX/Linux 文档工具有以下几个原因：

- 操作纯文本文件非常容易。使用 `perl`、`sed` 和 `grep` 等工具，你可以通过一个命令或脚本扫描并更改一份或数百份文档。

- 支持科学和数学符号法。通过 `geqn`，你可以创建可以由 Groff 输出的复杂方程。LaTeX 和 Tex 特别适用于技术符号。某些数学包需要 LaTeX。

- 编辑速度可以更快，因为传统的 Linux 文档是用文本编辑器创建的。通常情况下，从文本编辑器获得的体验比文字处理器更好。一些学习了 `vi` 或 `emacs` 文本编辑器的人完全不需要依赖鼠标。此外，现在还有基于 X 的文本处理器集成了许多文字处理功能（如拼写检查和编辑功能菜单）。

布局简单的文档非常适合 Linux 文档工具。例如，一本带有少量流程图和图片的技术书籍可以使用 Red Hat Linux 文档工具轻松地制作和维护。信函和备忘录使用这些工具也十分简单。当然，红帽 Linux 页面（为 Linux 中的每个命令、文件和设备提供单独说明）以及其他 Linux 文档也是用这些工具创建。
