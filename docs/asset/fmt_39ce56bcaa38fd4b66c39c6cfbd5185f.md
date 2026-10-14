
| Enter | 引用。 |
| n | 移动到同级的下一个 info 页。 |
| p | 移动到同级的上一个 info 页。 |
| u | 向上移动一级。 |
| l | 返回上次显示的帮助。 |
| s | 在 info 页中搜索。 |
| h | 显示帮助。 |
| ? | 列出命令摘要。 |
| q | 结束 info 显示。 |

### 练习 4-2

#### 访问和使用 info 页

在本次练习中，你将学习如何使用 `info` 命令，以及如何在 info 文本中导航。

你将在练习集中找到此练习。

（练习结束）

## 目标 3 访问发布说明和白皮书

发布说明、白皮书和其他有用信息存储在 `/usr/share/doc/` 目录。该目录包含：

- 发布说明 (Release Notes)
- 手册 (Manuals)
- 安装软件包帮助
- 教程 (Howtos)

### 发布说明

当你完成 SUSE Linux Enterprise Server 安装时，发布说明会在窗口中出现。

![](img/428e877abd09b1c1114d179d3458f12_127_0.png)

如果你以后访问这些发布说明，可以在目录下查找：

`/usr/share/doc/release-notes/SUSE_Linux_Enterprise_Server_10/`

有两个发布说明可用：

- `RELEASE-NOTES.en.html`
- `RELEASE-NOTES.en.rtf`

这些文件的内容相同。仅文件格式不同。

### 教程 (Howtos)

你可以在教程中找到更多信息（包括背景材料）。Linux 中几乎每个可以想象的主题都有相应的教程。

在 SUSE Linux Enterprise Server 10 中，默认不安装教程，但你稍后可以手动安装。

教程还以多种格式提供，例如 ASCII、PostScript 和 HTML。此外，许多教程已翻译成各种语言。

SUSE Linux Enterprise Server 的安装媒体包含大量的教程。HTML 格式的 Linux 文档项目 (TLDP) 教程安装在 `/usr/share/doc/howto/en/html/` 目录下。

你也可以安装 ASCII 格式的教程（软件包 `howto`, ASCII format）。安装后，你可以在 `/usr/share/doc/howto/en/txt/` 目录下找到它们。

你可以在 http://www.tldp.org 找到所有当前教程的列表（以及可用翻译）。

## 练习 4-3 访问发布说明和白皮书页面

在此练习中，你将访问发布说明和白皮书页面。

你将在练习本中找到此练习。

（练习结束）

## 目标 4 使用基于 GUI 的帮助

SUSE Linux Enterprise Server 10 的图形应用程序还提供在线帮助工具。

要启动在线帮助，请选择主菜单系统区域的“帮助 (Help)”。

图 4-2

![](img/428e877abd09b1c11149d179d3458f12_131_0.png)

使用链接在内容之间导航。

你还可以使用搜索功能快速查找帮助。在工具栏的搜索框中输入主题并按回车键。

在线帮助在大多数 GNOME 中均可用，可以通过按 F1 启动。

### 目标 5

#### 在网络上查找帮助

你可以在互联网上找到关于 Linux 的广泛信息集合，涵盖了普通问题和特殊问题。以下是一些较常用的 Linux 网站：

- http://www.novell.com/linux/
- http://www.tldp.org
- http://www.cert.org（特别是针对安全问题）
- http://www.securityfocus.com（特别是针对安全问题）
- http://www.kernel.org（特别是针对与 Linux 内核相关的问题）

要查找其他信息源，可以使用如 Google 这样的搜索网站。Google 在 www.google.com/linux 提供了专门针对 Linux 问题的搜索网站。

> 小心你在个人主页上找到的信息。这些信息可能是过时的或错误的。

![](img/428e877abd09b1c11149d179d3458f12_132_0.png)

### 练习 4-4

#### 在网络上查找帮助

在此练习中，你将学习如何在网络上查找帮助。你在 Novell 支持网站上查找 SUSE Linux Enterprise Server 10 的更新。你还将使用 Google Linux 搜索引擎在互联网上查找关于 GNOME 和 SLES10 的信息。

你将在练习本中找到此练习。

（练习结束）

## 总结

| 目标 | 总结 |
| :--- | :--- |
| 1. [访问和使用 man 页](#) | 在线帮助最重要的命令是 `man`。手册页始终分为若干部分，并根据不同的章节安排。使用命令 `less` 查看手册页。 |
| 2. [使用 info 页](#) | 许多程序不再提供手册页。取而代之的是 info 文件，可以使用命令 `info` 读取。以下是 info 格式的优点：<br>* 可结构化文档设置。<br>* 可以从目录直接跳转到特定章节。<br>* 特定章节之间可以链接。 |
| 3. 访问发布说明和白皮书 | 发布说明可以在以下目录找到：`/usr/share/doc/release-notes/`。在 `/usr/share/doc/manual/sles-admin_en/` 中，提供了管理员手册的 PDF 和 HTML 版本。安装 SUSE Enterprise Server 10 后不提供教程。如果你手动安装，可以在以下目录找到它们：`/usr/share/doc/howto/en/`。对于大多数已安装的软件包，以下目录下有帮助文件：`/usr/share/doc/packages/package-name` |
| 4. 使用基于 GUI 的帮助 | SUSE Enterprise Server 10 为图形应用程序提供了帮助系统。要启动在线帮助，请从主菜单选择“帮助”。帮助程序在大多数 GNOME 应用程序中均可用，可以通过按 F1 启动。 |

## 目标总结

### 5. 在网络上查找帮助

互联网是关于 Linux 普通问题和特殊问题的非常丰富的专家知识源。

以下是几个常用的常用的网站：

- http://www.novell.com/linux/suse
- http://www.tldp.org
- http://www.cert.org
- http://www.securityfocus.com
- http://www.kernel.org
- http://www.google.com/linux

## 第 5 部分 管理目录和文件

在本节中，你将学习 Linux 的结构以及最重要的命令。

## 目标

- 1. 理解文件系统 (FHS)
- 2. 识别 Linux 中的文件类型
- 3. 切换目录并列出内容
- 4. 创建和查看文件
- 5. 操作文件和目录
- 6. 在 Linux 中查找文件
- 7. 内容

### 目标 1 理解文件系统 (FHS)

Linux 文件系统概念（泛而言）与其他系统有很大不同。

Linux 中的文件名长度最多可达 255 个字符。它可以包含任何字符。某些字符（例如美元符号 `$`、分号 `:`）具有特定含义。如果你想使用这些字符而不产生特殊含义，必须在前面加上反斜杠 `\`。

你还可以使用变音符号、带有变音标记的字母或其他特定字符。Linux 区分大写和小写字母。例如，Invoice 和 invoice 标识为不同的文件。

要理解 Linux 文件系统概念，你需要了解以下内容：

- 系统的分层结构
- FHS（文件层次结构标准）
- 根目录 `/`
- 基本二进制文件 `/bin`
- 启动目录 `/boot`
- 其他分区 `/data`
- 设备文件
- 配置文件 `/etc`
- 用户目录 `/home`
- 库 `/lib`
- 可移动介质 `/media`
- 应用程序目录 `/opt`
- 管理员目录 `/root`
- 系统二进制文件 `/sbin`
- 服务数据目录 `/srv`
- 子目录 `/subdomain`
- 临时区域 `/tmp`
- 下方的 `/usr`
- 变量文件 `/var`
- Windows 分区 `/windows`
- 进程文件 `/proc`
- 系统信息目录 `/sys`
- 临时挂载文件系统的挂载点 `/mnt`
- 其他挂载文件系统

#### 系统的分层结构

Linux 文件系统概念涉及以树的形式表示的分层文件系统。

这棵树并不限于本地分区。它可以跨越分区，这些分区位于网络中不同的计算机上。它从根目录开始，管理员的名字由此产生，并延伸出树的分支。

以下是典型文件系统的摘录：

图 5-1

（等待，源中缺少图像链接，但文本继续）

此目录树中的文件由其路径唯一定义。路径指的是指向该文件的目录名。
