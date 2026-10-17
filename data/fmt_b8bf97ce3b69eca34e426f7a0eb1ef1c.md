
- C. 预约优先级
- D. 预约提醒

- 7. 默认情况下，所有人都可以查看你的日历，除非你限制了访问权限（是/否）。
    - A. 是
    - B. 否

- 8. 使用地址簿管理器（`Address Manager`），你可以对电子卡执行以下所有操作，但：
    - A. 安排预约
    - B. 发送电子邮件
    - C. 拨打电话
    - D. 将某人挂起

- 9. 计算器和时钟有什么共同特征？
    - A. 它们只能作为命令行工具运行。
    - B. 它们作为可选组件安装。
    - C. 它们是 CDE 的部分图形化工具。
    - D. 它们仅是显示工具，无法接受输入。

- 10. 关于终端（`Terminal`）窗口，以下哪项是？
    - A. 每个终端窗口都在新的 shell 中启动。
    - B. 终端窗口是从 CDE 内部启动的。
    - C. 终端窗口让你能够访问命令行。
    - D. 以上皆是。

## UNIX 命令摘要

`mailx` 交互式消息处理系统。示例：

```
$ mailx user2@cisco.com < dante.doc
```

`uuencode` 用于将二进制文件转换为 ASCII 编码表示，可以使用电子邮件发送。编码后的文件是一个普通的 ASCII 文本文件。

## 关键术语

**Calendar Manager** **日历管理器** 一个功能强大的图形化日程和预约管理程序。它是 Solaris CDE 的标准组件。

**Domain name** **域名** 电子邮件地址中的公司和类型部分，例如 `jiml@company.com`，其中 `company.com` 是域名。

**Mail Tool** **邮件工具** 一个功能强大的图形化电子邮件管理程序。它是 Solaris CDE 的标准组件，一个电子邮件客户端。

**mailx** `mailx` 程序（以及早期的更基础的 `mail` 程序）随每个版本的 UNIX 一提供，是读取和发送邮件的可接受程序。`mailx` 程序的基础知识位于附录 E，对于那些需要邮件程序但无法访问 CDE 的时候来说，这些是值得学习的。

**Pine** `Pine` 邮件程序是基于菜单的，比 `mailx` 程序更容易使用。`Pine` 是在华盛顿大学开发的，可以在命令提示符处输入 `pine` 即可访问。

**Username** **用户名** UNIX 用户的登录名，是用户电子邮件地址的一个部分，例如 `jiml@company.com`，其中 `jiml` 是用户名。

## 目标

读完本章后，你将能够：

- 使用 CDE 帮助
- 参考 AnswerBook2
- 使用命令行帮助
- 执行基础 UNIX 工作站故障排除
- 比较 DOS 和 UNIX 命令

# 第 4 章

# 获取帮助

## 简介

本章介绍了 Solaris 环境提供的各种形式的帮助。它涵盖了使用通用桌面环境（CDE）时提供的图形化帮助。CDE 帮助包含许多选项，例如帮助管理器（`Help Manager`）和面板（`Front Panel`）帮助。AnswerBook2 是 Solaris 手册的在线版本，也可以通过 CDE 访问。本章还涉及名为 *manual* 或 *man* 的页的命令行帮助，它们为 UNIX 命令和工具提供基于字符的帮助。本章还回顾了一些基础的故障排除技术，并为具有 DOS 背景的人提供了 DOS 到 UNIX 的交叉引用表。

## 使用 CDE

CDE 内置了许多图形化帮助功能。本节识别了这些功能的位置，并描述了它们可以提供的帮助类型。

## 使用帮助查看器（Help Viewer）

帮助图标位于面板的右侧。用左鼠标键点击该图标将打开帮助子面板（如图 4-1 所示），其中有帮助选项。这里列出了这些选项，并对每个提供的帮助类型进行了简要描述。

- 帮助管理器（`Help Manager`）——大多数情况的主要帮助工具
- SunSolve Online——来自 Sun Microsystems 的基于 Web 的在线帮助
- Solaris Support——基于 Web 的 Sun Microsystems 支持联系方式
- 信息（`Information`）——访问管理器信息的 readme 文件
- 桌面简介（`Desktop Introduction`）——使用桌面的基本教程
- 面板帮助（`Front Panel Help`）——面板图标和功能的帮助
- 项目帮助（`Item Help`）——关于特定项目的屏幕特定信息，通过选择该项目获取
- AnswerBook2——在线格式的 Solaris 参考手册

**图 4-1**

帮助管理器子面板。

![](img/a603cad51ef73bb7213e266f707c6758_135_0.png)

超链接（显示为下划线文本或框框图形）可以快速带你进入相关的帮助页面。只需点击帮助窗口中适当的文本区域即可。

返回（`Backtrack`）按钮允许你回溯在帮助屏幕间遵循的路径。

打印（`Print`）按钮可用于打印特定帮助主题的副本。

## 搜索帮助索引

索引搜索允许你查看所有帮助卷。要访问帮助索引搜索，在帮助查看器窗口点击索引（`Index`）按钮即可显示如图 4-2 所示的屏幕。这些卷以超链接的形式显示，可引用任何帮助页面。你还可以根据关键词搜索特定的帮助项目。帮助索引项目左侧的数字是可用子主题的数量。

**图 4-2**

帮助索引。

![](img/a603cad51ef73bb7213e266f707c6758_136_0.png)

## 使用项目帮助（Item Help）

关于特定项目的屏幕特定信息，通过选择该项目获取。

AnswerBook2——在线格式的 Solaris 参考手册。

**图 4-3**

项目内功能。

![](img/a603cad51ef73bb7213e266f707c6758_136_1.png)

## 访问帮助的其他方法

在桌面的任何空白处点击右键会显示工作空间（`Workspace`）菜单。从工作空间菜单中，你可以从程序（`Programs`）子菜单选择帮助选项。点击终端上的帮助图标会激活下拉菜单。大多数窗口也有特定于应用程序的帮助选项，如图 4-4 所示。

**图 4-4**

应用程序特定帮助。

![](img/a603cad51ef73bb7213e266f70c6758_137_0.png)

## 技能构建（Skill Builder）

### 实验活动 4.1

### 使用 CDE

在实验中，你将使用 CDE 内置的若干帮助功能来协助完成 CDE 相关任务。你使用主帮助查看器并搜索帮助索引。你还可以使用项目帮助来发现桌面图标。参考 Cisco Networking Academy Program: Fundamentals of UNIX Lab Companion。

### AnswerBook2

如果 AnswerBook2 安装在系统或网络服务器上，可以在帮助子面板上看到如图 4-5 所示的图标，并访问它。AnswerBook2 系统允许你查看 Solaris 手册的在线版本（包括图形）。几个在线书籍集合包含大量信息，包括：

- Solaris 8 系统管理员集合
- Solaris 8 用户集合
- Solaris 8 软件开发者集合

**图 4-5**

帮助子面板菜单。

![](img/a603cad51ef73bb7213e266f707c6758_138_0.png)

由于 AnswerBook2 页面占用的磁盘空间，你的系统管理员可能没有将 AnswerBook2 安装在计算机硬盘上。但是，也可以从连接到网络远程主机作为服务器的 CD-ROM 或硬盘上访问 AnswerBook2 文件。

**图 4-6**

初始的 AnswerBook2 界面。

![](img/a603cad51ef73bb7213e266f707c6758_139_0.png)

## 技能训练 (Skill Builder)

## 实验活动 4.2.1

## 参考 AnswerBook2 帮助

在本实验中，你将使用 Solaris AnswerBook2 并熟悉各种可用的在线手册。AnswerBook2 系统允许你使用 Web 浏览器查看许多打印版 Solaris 手册的在线版本，包括图形内容。请参阅《思科网络学院课程：UNIX 基础实验伴侣》。

## 命令行帮助

除了图形化的 CDE 帮助外，你还可以通过名为 man pages（帮助页）的命令行帮助获取有关 UNIX 命令、系统调用、文件格式和系统维护的帮助。

## man 帮助页 (Man Pages)

《UNIX 程序员手册》（也称为 man pages）描述了你所关于系统在线命令、系统调用、文件格式和系统维护需要了解的知识。在线 man帮助页是 Solaris 计算环境（以及所有 UNIX 版本）的一部分，并默认安装。man帮助页以基于基于字符屏幕显示形式存在，不是图形化的。

要访问 帮助页，你必须处于命令提示符下。你可以登录命令行，或在 CDE 中打开终端 窗口并从 Korn shell (`$`) 等命令提示符开始。当你想要使用某个命令或工具但忘记了语法，或者需要某些如何使用它的信息时，man帮助页非常有帮助。man帮助页提供了有关如何输入命令、其目的的描述以及可用选项或参数的信息。某些命令在所有三个 shell 中均无法工作；man帮助页会告知你哪些命令可以在哪些 shell 中运行。我们将 Bourne shell 称为 (`sh`)，Korn shell 称为 (`ksh`)，C shell 称为 (`csh`)。

## man 命令

`man` 命令用于显示可用的数百个 UNIX 命令中任何一个命令的在线 man 帮助页。你可以通过在命令行输入 `man intro` 来获取所有 UNIX 命令的列表及其功能的简要描述。你可以通过输入 `man man` 来显示 `man` 命令本身的帮助页。

你可以通过多种方式使用该命令。基本形式是 `man name`，其中 `name` 是你想获取信息的命令名称。`man` 命令有几个实用的选项，用于执行关键词搜索和显示程序员手册的特定章节。这里列出了使用该命令的几种不同方法，并对每种进行了简要解释：

- `$ man name`——提供特定命令的帮助，其中 `name` 是你想要获取帮助的命令，例如 `ls`、`cat` 或 `mkdir`。
- `$ man -k keyword`——在 man 帮助页的目录中搜索指定的关键词，并显示每个条目的单行摘要。图 4-7 显示了命令输出的一个示例。

**图 4-7**

`man -k keyword`。

```
Window Edit Options               Terminal
man -a calendar             cdcm (1) - 日历管理器
cdcm_archive cdcm_archive (1) - 日历存档文件的格式
cdcm_delete cdcm_delete (1) - 从日历数据库中删除预约
cdcm_diff cdcm_diff (1) - 比较日历-预约条目
cdcm_insert cdcm_insert (1) - 将预约插入日历数据库
cdcm_dump cdcm_dump (1) - 从日历数据库中删除预约
sdcm_admin sdcm_admin (1) - 日历管理工具
sdcm_convert sdcm_convert (1) - 日历转换工具
cal (1) - 显示日历
diffime (1) - 比较两个日历之间的差异
diff (1) - 显示日历主题的变化
calendar manager, appointment and resource sc task (1)
cm_delete (1) - 从日历管理器数据中删除预约
cm_insert (1) - 向日历管理器数据中插入预约
cm_lookup (1) - 从日历管理器数据中查找预约
```

## 使用 man 帮助页

- `$ man -s section name`——显示 man 帮助页的特定章节，该章节可以包含多个命令。图 4-8 显示了输出示例。

**图 4-8**

`man -s section name`。

![](img/a603cad51ef73bb7213e266f707c6758_139_0.png)

## 帮助标题 (Headings)

在命令提示符下，man 帮助页的输出对你是有帮助的。

## man 帮助页的标题

man 帮助页被分为不同的章节。常见的标题包括：

- **name**（名称）——列出与主题相关的命令。
- **synopsis**（摘要）——显示关于该命令的用法。
- **description**（描述）——提供有关命令功能的详细说明。
- **OPTIONS**（选项）——列出可用的选项或参数。
- **EXAMPLES**（示例）——提供如何使用命令的示例。
- **SEE ALSO**（另参见）——列出相关的命令或主题。
- **INDEX**（索引）——按关键字查找命令。

## 在 man 帮助页中滚动

man 帮助页的输出可能多达 20 个屏幕。在找到特定的命令页面后，某些按键对于滚动非常有用。图 4-10 显示了滚动功能。

**图 4-10**

滚动 帮助页。

| 按键 | 描述 |
| :--- | :--- |
| 空格 | 滚动一页 |
| 回车 | 滚动一行 |
| b | 向后滚动一页 |
| f | 向前滚动一页 |
| q | 退出 `man` 命令 |
| /string | 向前搜索字符串 |
| n | 查找下一个出现项 |
| h | 显示所有快捷键描述 |

## 按章节搜索 man 帮助页

如前，man 帮助页底部的 SEE ALSO 部分列出了相关的引用。当这些引用后面跟着一个非 1 的数字时，表示可以使用 `-s` 选项访问该章节。例如，执行 `man passwd`（如图 4-11 所示）会显示 `passwd` 命令的信息，并提供如何更改密码的说明。该页面的 SEE ALSO 部分显示如下：

**图 4-11**

按章节搜索 man 帮助页。

```
$ man passwd
...
（输出省略）
SEE ALSO
finger(1), login(1), nispasswd(1),
crypt(3C), passwd(4)

$ man -s 4 passwd
$ man -s 3C crypt
```

显示 `man -s 4 passwd` 显示 `/etc/passwd` 文件的信息，而 `man -s 3C crypt` 显示密码加密的信息。列出的其他 SEE ALSO 项目是相关的，但没有独立的章节可以搜索。

## 按关键词搜索 man 帮助页

`man` 命令的 `-k` 选项同样有用。例如，如果你知道要寻找与日历相关的命令，但不确定有哪些可用命令，可以使用 `-k` 选项指定一个主题。图 4-12 显示了在查找与日历相关的命令时，使用 `-k` 选项的结果。

**图 4-12**

通过关键字搜索帮助页（man pages）。

```
Window Edit Options               Terminal
man -a calendar             cdcm (1) - 日历管理器
cdcm_archive cdcm_archive (1) - 日历存档文件的格式
cdcm_delete cdcm_delete (1) - 从日历数据库中删除预约
cdcm_diff cdcm_diff (1) - 比较日历-预约条目
cdcm_insert cdcm_insert (1) - 将预约插入日历数据库
cdcm_dump cdcm_dump (1) - 从日历数据库中删除预约
sdcm_admin sdcm_admin (1) - 日历管理工具
sdcm_convert sdcm_convert (1) - 日历转换工具
cal (1) - 显示日历
diffime (1) - 比较两个日历之间的差异
diff (1) - 显示日历主题的变化
calendar manager, appointment and resource sc task (1)
cm_delete (1) - 从日历管理器数据中删除预约
cm_insert (1) - 向日历管理器数据中插入预约
cm_lookup (1) - 从日历管理器数据中查找预约
```

## 使用 whatis 显示 man 帮助页头部

使用 `whatis` 命令可以显示手册章节的头部，如图 4-13 所示。然后可以使用 `man` 命令显示帮助页本身。如果你记得命令名称但不记得它的具体功能，`whatis` 命令非常有帮助。你可以使用 `whatis` 获取命令的简要定义。图中的示例显示了使用 `whatis` 查找 `grep` 命令的功能（`grep` 将在课程后部分介绍）。

**图 4-13**

`whatis` 命令。

```
Window Edit Options               Help
$ whatis cd
cd (1) - 更改目录
$ whatis grep
grep (1) - 在文件中搜索模式
```

## 提示

你可以使用命令 `man command_name | lpr`（或 `ipr`）打印页面。行打印命令（`lp` 和 `lpr`）将在第 11 章“UNIX打印”中介绍。

## 保存页面供以后使用

你可以将页面保存为文本文件以便编辑或发送电子邮件。使用命令 `man_name | col -b > filename`——例如 `man intro | col -b >~/unixcmds`。`intro` 命令包含所有 UNIX 命令的列表；竖线管道（`|`）将在第 7 章“高级目录和文件管理”中介绍；`col -b` 格式化帮助页输出；大于号（`>`）表示将 `man` 命令的输出发送到文件；`~/unixcmds` 是在你的主目录中创建的文件（`~` 代表主目录）。
