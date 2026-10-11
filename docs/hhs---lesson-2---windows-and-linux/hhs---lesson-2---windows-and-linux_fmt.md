
# HHS - 第 2课 - Windows 与 Linux

![](img/c27935123f59a22046d0a5f43d6d0b88_0_0.png)

# 第 2 课

## LINUX 和 WINDOWS 基础命令

## “使用许可”信息

以下课程和工作手册根据 ISECOM 的以下条款和条件开放并供可用。

黑客高中项目中的所有作品均为小学生、初中生和高中生提供非商业用途，无论他们是在公立机构、私立机构还是在家自学的一部分。这些材料不得以任何形式复制并出售。严禁在没有许可的情况下提供任何收费的课程、课程、培训或营地，包括大学课程、学院课程、职业学校课程及类似。要购买许可，请访问 LICENSE 课程、夏季或计算机营地以及 www.hackerhighschool.org/license。

HHS 项目是一个学习工具，和任何其他学习工具一样，教学取决于教师的影响而非工具本身。ISECOM 对本文中任何信息的应用或滥用不承担责任。

HHS 项目是一个开放的社区努力，如果你发现该项目的价值，我们请求你通过购买许可、捐赠或赞助来支持我们。

## 贡献者

Daniel Fernández Bleda, 安全审计员

Jairo Hernández, La Salle URL Barcelona

Jaume Abella, La Salle URL Barcelona - ISECOM

Kim Truett, ISECOM

Pete Herzog, ISECOM

Marta Barceló, ISECOM

![](img/c27935123f59a22046d0a5f43d6d0b88_3_0.png)

![](img/c27935123f59a22046d0a5f43d6d0b88_3_1.png)

![](img/c27935123f59a22046d0a5f43d6d0b88_3_2.png)

## 2.1. 引言与目标

本课介绍了 Windows 和 Linux 操作系统的命令和基础工具，以便你熟悉它们。这些命令将用于完成后续课程中的练习。

在本课结束时，你应该掌握以下命令：

- 通用 Windows 和 Linux 命令
- 基础网络命令和工具
- `ping`
- `tracert`
- `netstat`
- `ipconfig`
- `route`

## 2.2. 要求与设置

### 2.2.1 要求

本课程需要以下设备：

- 一台运行 Windows 98/Me/2000/NT/XP/2003 的 PC
- 一台运行 Linux Suse/Debian/Knoppix 的 PC
- 访问互联网。

### 2.2.2 设置

![](img/c27935123f59a22046d0a5f43d6d0b88_5_0.png)

这是你将要工作的环境。它由你的接入互联网的 PC 以及 ISECOM 黑客高中网络组成，你将通过互联网访问该网络。这是你进行大多数测试的网络。

请注意，对 ISECOM 测试网络的访问是受限制的。为了获得访问权限，你的导师必须联系系统管理员。

## 2.3. 系统操作：WINDOWS

大多数用于 Windows 的命令都是内部命令。

### 2.3.1 如何打开 MS-DOS 窗口

要发布命令，需要：

1. 点击“开始”按钮
2. 选择“运行”选项
3. 如果你使用的是 Windows，输入 "`cmd`" 并按回车。将类似下面的窗口：

![](img/c27935123f59a22046d0a5f43d6d0b88_6_0.png)

### 2.3.2 命令和工具 (Windows)

可以输入以下命令：

| `date` | 显示或设置系统日期 |
| `time` | 显示或设置系统时间 |
| `ver` | 显示正在使用的 MS-DOS 版本 |
| `dir` | 显示目录的子目录和文件 |
| `cls` | 清屏 |
| `mkdir` | 创建名为 "`directory`" 的目录 |
| `chdir`, `cd` | 显示或切换目录到 "`directory`" |
| `rmdir` | 删除名为 "`directory`" 的目录 |

## 2.4. 系统操作：Linux

## LINUX 和 WINDOWS 基础命令

| `free` | 以文本格式显示结构 |
| `chkdsk` | 检查磁盘 |
| `mem` | 显示系统使用的和剩余内存 |
| `rename` | 重命名文件 |
| `ren` | 重命名文件 |
| `copy` | 将一个或文件复制到另一个位置 |
| `move` | 移动文件并重命名文件和目录 |
| `type` | 输出文本文件的内容 |
| `more` | 分页显示信息 |
| `delete`, `del` | 删除一个文件 |

注意：斜体文字不是命令，必须替换为所需的值。例如，“`delete`”和“`del`”是同一个命令。

## 工具

| `ping host` | 验证与机器 "`host`" 的连接 |
| `ping` 命令通过 ICMP（互联网控制消息协议）向另一台计算机发送“数据包”，以学习是否可以通过网络访问。此外，它还会显示关于未响应数据包百分比和响应的统计摘要。可以直接使用机器名称或其 IP 地址。 |

示例：`ping www.google.com`

`ping 193.145.85.2`

某些选项：

- `n`：发送 `n` 个数据包
- `t`：持续 ping 指定主机直到停止（按 CTRL+C 结束）

要查看更多选项：`ping /h`

## 2.4 系统操作：Linux

正如在 Windows 中一样，如果你在使用 Linux，我们需要打开终端窗口。因此，我们将学习如何打开终端窗口。

![](img/c27935123f5922046d0a5f436d088_0)

### 2.4.1 如何打开终端

要使用以下命令，需要打开终端：

1. 点击“开始”按钮
2. 选择“运行”
3. 输入“`konsole`”
4. 将出现一个类似下面的窗口：

![](img/c27935123f5922046d0a5f436d088_1)

5. 现在可以输入列出的命令。

### 2.4.2 命令和工具（Linux）

| 命令 | 说明 |
| :--- | :--- |
| `pwd` | 显示当前目录名称。 |
| `hostname` | 显示本地主机名（你当前使用的计算机）。 |
| `finger user` | 显示用户“`user`”的信息。例如：`finger root` |
| `ls` | 列出目录的内容。例如：`ls` |
| `cd directory` | 从当前目录切换到“`directory`”。如果没有指定目录名，它将切换到主目录。例如：对于登录名“`mylogin`”，命令 `$cd` 会切换到 `/home/mylogin`。例如：`$cd` 会切换到上一个目录。例如：`$cd /tmp` |
| `cp source dest` | 将文件“`source`”复制到文件“`dest`”。复制文件例如：`cp /etc/passwd /tmp` |
| `rm file` | 只有文件的所有者（或 root）可以删除它。例如：`rm myfile` |
| `mv source dest` | 移动或重命名文件目录。例如：`mv oldname` |
| `mkdir directory` | 创建名为“`directory`”的目录。 |
| `rmdir directory` | 删除名为“`directory`”的目录。 |
| `find name` | 查找名为“`name`”的文件。 |
| `echo string` | 将字符串写入文件。 |
| `command >> file` | 将字符串追加到文件末尾。 |

## 延伸阅读

如需查看详细的术语表，请访问以下 URL：

- http://www.matise.net/files/glossary.html
- http://www.uic.edu/depts/accc/inform/v106.html
- http://www.catb.org/~esr/jargon/

Windows – 有关命令和工具的更多信息，请在 MS-DOS 窗口输入 "`command /h`" 或 "`command /?`"。

Linux – 有关命令和工具的更多信息，请在 shell 中输入 "`command --help`" 或 "`man command`"。
