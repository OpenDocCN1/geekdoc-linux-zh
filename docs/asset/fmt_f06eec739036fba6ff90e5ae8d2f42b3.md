
**图 2-6.** 使用逻辑运算符的高级搜索

### 注册文档以进行在线搜索

在文档服务器上的文档可以被搜索或查看之前，必须发生两件事：每个文档和文档索引必须创建或安装在 `DocSearch` 服务器上，并且文档和文档索引必须注册到库服务。有两种方法可以将文档注册到服务器。大多数 `AIX` 应用程序具有为文档服务器预建的索引，并随应用程序自动安装。或者，您可以以手动方式让服务器了解文档，即在服务器上手动创建文档索引，然后手动注册索引。索引会创建压缩版本的文档，或一组文档。这个新创建的索引文件（而非原始 `HTML` 文件）才是 `DocSearch` 将进行搜索和显示的对象。

本节将概述注册文档以及创建文档库服务所需索引的步骤。

1. 以 `HTML` 格式创建文档。
2. 创建文档的索引。
3. 在文档服务器上注册新的索引。

索引注册完成后，它们将在 Web 浏览器中显示，准备进行搜索和查看。您可以在在线文档库服务章节 `AIX 5L Version 5.1 General Programming Concepts: Writing and Debugging Programs`（`AIX 5L` 版本 `5.1` 通用编程概念：编写和调试程序）中找到这些操作各步骤的详细指南。编写文档的应用程序开发人员会发现该章节对于在编写 `installp` 软件包时创建自动安装索引特别有价值。您还可以将公司的文档注册到在线文档库中。这种灵活性使 `DocSearch` 成为一个宝贵的全企业文档搜索引擎。

## 常见的 `DocSearch` 和 `man` 页面问题

在使用 `DocSearch` 时，您可能会遇到一个或多个错误。这是最常见的五大问题列表。

**问题 1** 最常见的问题之一是域名解析。您可能需要编辑 `/etc/hosts` 文件，并在短主机名后直接添加一个句点 (.)。例如，

`10.10.10.2 booboo.`

**问题 2** 在 `5.1` 迁移安装后，您输入 `man ls`，发现没有错误提示或数据输出。您遇到了 `DocSearch` 显示的某种怪癖。首先确保该命令的文件已安装。以下命令将产生这些文件的目录列表：

```
# lsipp -f bos.man.en_US.cmbs
```

这应该显示已安装的 `bos.man.en_US.cmbs` 软件组中的文件。

如果您随后进入 `/usr/share/man/info/en_US` 目录并运行递归长列表 (`ls -Rl * | more`) 查看目录内容，发现大多数文件为空，则存在问题。您需要安装/重新安装以下文件以纠正此问题：

- `bos.html.en_US.topnav.navigate` - 顶级导航
- `bos.html.en_US.nav` - 在线导航
- `bos.html.en_US.cmbs.cmdbal` - `AIX` 命令参考 1
- `bos.html_en_US.cmds.cmda2` - `AIX` 命令参考 2
- `bos.html_en_US.cmds.cmda3` - `AIX` 命令参考 3
- `bos.html_en_US.cmds.cmda4` - `AIX` 命令参考 4
- `bos.html_en_US.cmds.cmda5` - `AIX` 命令参考 5
- `bos.html_en_US.cmds.cmda6` - `AIX` 命令参考 6

**问题 3**

您收到以下错误消息：“`Error: Can’t open display: XYZ.`”（错误：无法打开显示：`XYZ`。）。这意味着您试图打开由 `DISPLAY` 变量定义的窗口，但该变量定义错误，未设置变量，或者您没有权限使用此显示设备。请依次执行以下命令：

```
# xhost -<remote_hostname_or_IP_address>
# export DISPLAY=<local_hostname_or_IP_address>:0.0
# docsearch &
```

**问题 4**

`CDE` 帮助子面板上没有 `DocSearch` 图标。您已安装 `DocSearch`，但 `CDE` 尚未发现新图标。您需要重启工作区管理器以发现新图标。在屏幕的空白处右击。这将弹出工作区菜单。在菜单中，左击“重启工作区管理器”，然后在弹出的对话框中单击“确定”。或者，您可以注销并重新登录到系统。

**问题 5**

`DocSearch` 正在启动，您收到一条消息称找不到文档服务器。在 `AIX 5L` 版本 `5.1` 中，必须手动编辑 `httpd.conf` 文件以定义文档服务器。

```
# vi /usr/HTTPServer/conf/httpd.conf
```

在文件中搜索 `ServerName` 变量。取消该行的注释，并输入文档服务器的完全限定主机名：

`ServerName yogi.mydomain.com`

## `man` 页面

`man` 页面提供关于 `AIX` 命令、文件、库子例程和系统调用的参考文档。`man` 命令不会执行 `DocSearch` 提供的同种类模式搜索，因此您需要确切知道正在查找信息的命令或文件名。`man` 命令的语法如下。

```
# man { command | file | subroutine | system call }
```

例如，

```
# man man
```

将显示 `man` 命令的在线文档。`man` 命令按以下顺序搜索并显示文档：

- 在 `/usr/share/man` 目录结构中的任何 `nroff` 目录 (`man?`)。
- 在 `/usr/share/man` 目录结构中的格式化版本目录 (`cat?`)。
- 如果上述两项搜索失败，则搜索超文本 (`DocSearch`) 数据库。
- 超文本文档位于 `/usr/share/man/info` 目录结构中。

## 在 `AIX 4.3.3` 和 `5L` 版本 `5.1` 上安装 `man` 页面

如果系统只需要 `man` 页面，那么 `DocSearch` 可能对来说功能过剩。要在 `4.3.3` 和 `5L` 上安装 `man` 页面，必须安装以下所有软件组：

- `bos.html.en_US.topnav.navigate` - 顶级导航
- `bos.html.en_US.nav` - 在线导航
- `bos.html.en_US.cmds.cmddal` - `AIX` 命令参考 1
- `bos.html.en_US.cmds.cmsd2` - `AIX` 命令参考 2
- `bos.html.en_US.cmds.cmsd3` - `AIX` 命令参考 3
- `bos.html.en_US.cmds.cmsd4` - `AIX` 命令参考 4
- `bos.html.en_US.cmds.cmsd5` - `AIX` 命令参考 5
- `bos.html.en_US.cmds.cmsd6` - `AIX` 命令参考 6

## 使用 `man` 页面

`man` 命令可以访问存储在 `DocSearch` 中的信息。调用时，`man` 将首先搜索 `/usr/man/cat?` 目录，然后搜索 `/usr/man/man?`，最后，如果已安装 `DocSearch` 数据，则搜索 `DocSearch` 数据。命令 `man` 和 `catman` 将 `man` 页面第 1、2 和 8 节映射到 `DocSearch` 命令文档，将第 2 和 3 节映射到 `DocSearch` 子例程文档，将第 4、5 和 7 节映射到 `DocSearch` 文件文档。您需要定期执行 `catman -w` 以保持 `arprofs` 和 `whatis` 命令的数据库为最新状态。

```
# catman -w
```

不时地，您可能需要添加自己的自定义 `man` 页面信息。这可能是一个解释计费策略、备份支持、本地开发软件等的帮助文件。将本地 `man` 页面与供应商提供的帮助分开存放是个好主意。这样可以防止它们在安装、维护和升级活动中被覆盖。本地 `man` 页面常用的位置路径是 `/usr/man/man1` 和 `/usr/local/man/man7`。环境变量 `MANPATH` 可以在 `/etc/environment` 中设置以包含您的本地 `man` 页面路径。用户也可以使用 `MANPATH` 来支持他们自己的 `man` 目录。

以下是一些本地 `man` 页面存储库：

- `/usr/man/man1`
- `/usr/local/man/man?`
- `/usr/local/cat/cat?`

在创建新的 `man` 页面时，您可以使用现有的 `man` 页面作为模板。尽量保持一种通用风格，以便您的用户知道预期看到什么。每个 `man` 页面应包括：一个标识主题或命令的名称部分，一个描述命令及参数选项和格式的综合描述部分，一个描述主题的描述部分，一个详述参数和值信息的选项部分，以及一个关于已知错误的部分。在 `man` 页面末尾，可以考虑包含一个“另请参阅”部分以指示相关信息，以及一个可选的作者部分以标识作者姓名和地址。

以下是 `man` 页面风格的示例：

```
mycommand(1)
NAME
    mycommand - Does just what I want to do.
SYNOPSIS
    mycommand [will|wont] work
    mycommand is always used as a last resort. It can
    be expected either to work or to fail. mycommand
    contains no surprises at all.
OPTIONS
    will     Completes the work at hand.
    wont     Take a vacation.
BUGS
    mycommand is always error free!
SEE ALSO
    myprogram(1), myshell(1)
AUTHOR
    Me. Who did you think it was?
```

您可以在 `man` 页面中包含 `nroff` 标签以控制显示格式。包含这些标签后，可以使用 `nroff` 对其进行测试（见表 2-1）。

```
# nroff -man mycommand.1 | more
Here is a sample man page with tags inserted:
.TH mycommand 1
```

`.SH NAME`

`mycommand \- 执行我想要做的操作。`

`.SH SYNOPSIS`

`mycommand [will|wont] work`

`.SH DESCRIPTION`

`.B mycommand`

通常作为最后的手段使用。它可能成功，也可能失败。

`.B mycommand`

完全没有任何意外情况。

`.SH OPTIONS`

`.TP 3`

`Will`

完成手头的任务。

`.TP 3`

`wont`

去度假。

`.SH BUGS`

`.B mycommand`

永远没有错误！

`.SH SEE ALSO`

`myprogram(1), myshell(1)`

`.SH AUTHOR`

`.B 我。`

你以为是谁？

| 标签 | 用途 |
| --- | --- |
| `.TH <name> <num>` | 手册页名称和章节号 |
| `.SH <section>` | 标识一个子章节 |
| `.B <text>` | 粗体或高亮文本 |
| `.I <text>` | 斜体文本 |
| `.PP` | 段落块 |
| `.TP <num>` | 段落缩进 `<num>` 个空格，除了第一行 |
| 表 2-1。 | `nroff` 标签示例 |

记得定期运行 `catman -w` 命令，以保持 `apropos` 和 `whatis` 数据最新。在运行 `catman -w` 命令前后都运行 `man -k print` 命令，以查看其效果。您可能希望将其添加到根用户的 `cron` 表中。

```
## catman -w
```

## `DocSearch`

以下列表是对一些 `DocSearch` 文件和命令的参考。

| `DocSearch` 文件/命令 | 定义 |
| --- | --- |
| `/usr/bin/docsearch` | `docsearch` 命令 |
| `/usr/lib/nls/msg/$LANG/docsearch.cat` | `docsearch` 消息目录 |
| `/usr/bin/defaultbrowser` | `defaultbrowser` 命令 |
| `/usr/share/man/info` | 超文本文档 |
| `/usr/share/man/info/$LANG` | 已安装的 `docsearch` 文件集 |
| `mount -v cdrfs -r /dev/cd0 /infod` | 挂载到 CD-ROM |

## `man` 页

以下是一些 `man` 页文件和命令的定义。

| `man` 页文件/命令 | 定义 |
| --- | --- |
| `/usr/man/cat?` | 格式化文本；优先搜索 |
| `/usr/man/man?` | `nroff` 格式；次要搜索 |
| `catman -w` | 更新 `whatis` 数据库以供 `apropos` 命令使用 |

## 检查清单

以下是文档库服务和联机 `man` 页关键要点的检查清单。

- 要启动文档库服务（`DocSearch`），请在命令行中输入 `docsearch`，或者在通用桌面环境（`CDE`）中，点击帮助图标，然后从图标列表中选择“文档库”。
- 本地或远程用户也可以使用 Web 浏览器通过以下 `URL` 访问文档库服务：

  ```
  http://<Server-Hostname>/cgi-bin/ds_form
  ```

- 其中 `<Server-Hostname>` 是文档 Web 服务器的主机名或 IP 地址。
- 您可以从挂载的 CD-ROM 运行 `DocSearch` 和 `man` 页，但不推荐此方法，因为响应时间可能无法接受，并且必须始终挂载 CD-ROM 才能使文档服务正常工作。
- 为了获得最佳性能，应将整个文档搜索服务库安装在文档服务器本地的固定磁盘上。
- 要在 `AIX 4.3.3` 上安装 `DocSearch`，如果它们尚不存在，您需要定义 `innadm` 用户和组，并确保语言环境变量设置为正确的值。
- 默认情况下，`DocSearch` 库搜索服务作为 `AIX 5L` 中 `BOS` 的一部分进行安装。然而，如果您从以前的 `AIX` 版本或发行版进行了*迁移升级*，您可能在重新启用文档搜索服务时会遇到一些问题，并且可能希望卸载并重新安装 `DocSearch` 系统。
- 在主要的 `DocSearch` 浏览器窗口中，要执行搜索，请在“Search For”字段中输入感兴趣的主题，然后按 ENTER 键。您的搜索可以是简单的单词或短语匹配，或者您可以使用 `AND`、`OR` 和 `NOT` 逻辑搜索运算符创建复杂的逻辑搜索。
- 您可能会遇到 `DocSearch` 域名注册问题。如果是这样，请编辑 `/etc/hosts` 文件，并在短主机名后面直接添加一个句点 (.)。
- 要显示关于 `AIX` 命令、文件、库子例程和系统调用的参考文档，请使用 `man` 命令。

![](img/82f851021955589d82b22750fb3b1646_51_0.png)

# 第二部分

系统与系统架构

- `3 POWER` 处理器和系统
- `4 AIX 5L` 内核

此页故意留空。

![](img/82f851021955589d82b22750fb3b1646_53_0.png)

# 第 3 章

# POWER 处理器和系统

![](img/82f851021955589d82b22750fb3b1646_53_1.png)

版权所有 2002 麦格劳-希尔公司。点击此处查看使用条款。

随着世界各地的 `IBM` 开发团队努力工作以超越所有竞争对手，你可以肯定这些新芯片具备了新的功能。新的处理器技术有四个主要进展：

- 铜技术
- 绝缘体上的硅
- 低 $k$ 介电质
- `0.18` 微米及更小线宽的技术

所有这些进展都很重要，我将逐一介绍。

## 铜技术

铜技术允许处理器运行得更快、更冷。基本思想是使用铜线/迹线代替电路板上这类迹线的铝。使用铜线/迹线时，电流流动时的电阻更小。电阻越高，热量越多，因为电流流动受到限制。电阻较低时，电流流动受到的限制较少，因此部件运行温度较低。结果是能够在更小的空间内集成更多组件，这反过来减少了信号延迟，结果是时钟速度更快，某些处理器运行频率达到 `1.3 GHz`。（等你读到这篇文章时，速度还会更快！）

## 绝缘体上的硅

“绝缘体上的硅”这句话听起来很奇怪，违背了正常的思维。如何让脆弱的硅晶圆在绝缘体上工作？好吧，`IBM` 已经想出了一种在绝缘体上制造芯片的工艺。结果是非常凉爽的芯片，这意味着你需要更少的冷却风扇，而且可以把冰箱留在家。当设备运行得更冷时，你可以将更多、更冷的芯片更紧密地放置在一起。通过这种组合，你实现了更高的晶体管密度和更高的 `CPU` 时钟速度。

## 低 `K` 介电质

`Low~k` 介电质指的是芯片内迹线之间的电容。如果你不知道什么是电容器，它们是电视内部那些大的圆形组件。电容器由两个极板和一种介电质（绝缘体）组成。当电流通过极板时，电荷会在介电质中的极板之间积聚。当你将两根导线/迹线靠近在一起并使电流通过导线时，你就具备了制作电容器的组件，导线之间的空气间隙就是介电质。介电质保持电荷能力的度量称为 $dielectric~constant~(k)$（介电常数）。介电常数较高的材料储存的电荷较高。因此，我们需要集成电路中的极低 `low~k` 介电质。

当线宽缩小到 `0.18` 微米及更小时，集成电路内的迹线尽可能紧密地放置，以便在芯片内集成更多内容。当迹线靠得太近时，会出现电容耦合的可能性，这是由于介电质（在这种情况下是空气，一种绝缘体）中积聚的电荷导致的迹线（极板）之间的“泄漏”现象。其效果是原本应该保留在一根迹线上的信号会泄漏到其他迹线上，导致信号混合在一起。这种效果在集成电路中是行不通的。因此，`IBM` 提出了一种利用低 `k` 介电质芯片技术保护迹线免受这种泄漏效应影响的方法。实际上，这种新的芯片技术类似于在迹线之间放置屏蔽层。你可以将其类比为有线电视接线中的编织线屏蔽层，其中中心导体是迹线，编织线是屏蔽层。再次，结果是更快的时钟速度。当然，我极大地简化了这个概念。

## 小（`0.18` 微米及更小）迹线
