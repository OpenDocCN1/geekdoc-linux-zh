
| `-e command` | 在 xterm 窗口中运行指定命令。 |
| `-fb font` | 使用指定的字体。 |
| `-fg color` | 指定前景色。 |
| `-fl fontname` | 设置活动图标的字体。 |
| `-fn font` | 指定用于普通文本的字体。 |
| `-hc color` | 设置用于前景色的颜色。 |
| `+|-le` | 启用检测 `stty` `erase` 值。 |
| `+|-im` | 启用插入模式。 |
| `+|-j` | 启用跳跃滚动。 |
| `-leftbar` | 强制将滚动条置于窗口左侧。 |
| `+|-ls` | 将 shell 启动为登录 shell。 |
| `+|-mb` | 当用户在右侧边框附近输入时，发出边框提示音。 |
| `-mc time` | 指定多击选择之间的最大时间（以毫秒为单位）。 |
| `-ms color` | 指定 `默认` 指针颜色。 |
| `-nb n` | 指定从右侧边框向左的 n 个字符 (`n`)，如果启用提示音，则在此处发出边框提示音。 |
| `+|-nul` | 启用下划线显示。 |
| `+|-pc` | 启用粗体颜色。 |
| `-rightbar` | 强制将滚动条置于窗口右侧边框。 |
| `-rv` | 通过交换前景色和背景色来模拟反色视频。 |
| `+|-rv` | 启用反向换行。 |
| `+|-s` | 启用异步滚动。 |
| `+|-sb` | 保存从顶部滚出的所有行并显示滚动条。 |
| `+|-sf` | 启用 Sun 功能键。 |
| `+|-si` | 在窗口底部结束输出。 |
| `+|-sk` | 启用滚动时自动重新定位窗口。 |
| `-sl n` | 指定要从屏幕顶部滚出并保存的行数 (`n`)。 |
| `+|sp` | 启用 Sun 键盘映射。 |
| `+|t` | 以 Tektronix 模式而非 VT102 模式启动。 |
| `-title string` | 使用指定字符串作为窗口标题。 |
| `-tm keyword` | 指示应使用的终端设置，由关键字指定。选项包括 `intr`, `quit`, `erase`, `kill`, `eof`, `eol`, `swtch`, `start`, `stop`, `brk`, `sup`, `dsup`, `rprnt`, `flush`, `weras` 和 `inext`。 |
| `-tn name` | 指定要使用的终端类型名称。 |
| `+|-ulc` | 禁用带颜色的下划线显示。 |
| `+|-ut` | 跳过在系统日志中创建条目。 |
| `+|-vb` | 启用视觉而非听觉提示音。 |
| `+|-wf` | 等待窗口映射完成后再启用子进程。 |
| `-ziconbeep percentage` | 以指定百分比的音量发出提示音。 |

# 第 2 章

## 获取帮助和定位

![](img/e85417bb52fc523c6fc7b3b77b124ecb_62_0.png)

在本章中，您将学习用于在 Linux 上获取帮助的命令。您还将学习可以帮助您定位的命令。后一类包括提醒您在 Linux 文件系统中位置的命令，您所属的用户组，以及更多内容——包括一个可以显示或打印当前月份或年份（或任何月份或任何年份）的美观日历的命令。

### 概览

| 我怎么做 | 查看此条目 | 示例 |
| :--- | :--- | :--- |
| 找出哪个 man 页面有我想要的信息？ | `apropos`, `man` | `apropos fonts` |
| 显示或打印日历？ | `cal` | `cal -y 2003 \| 1pr` |
| 查看当前系统日期和时间？ | `date`, `rdate` | `date` |
| 找出网络上谁还在使用计算机？ | `finger`, `rwho` | `finger suzanne` |
| 找出各种 bash shell 命令的作用？ | `help` | `help cd` |
| 显示此系统的 IP 地址？ | `hostname` | `hostname -i` |
| 更改系统日期和时间？ | `hwclock` | `hwclock --set --date='05/21/03 12:56'` |
| 找出我的用户和组名称及 ID？ | `id`, `groups`, `whoami` | `id` |
| 获取关于 GNU 实用工具的信息？ | `info` | `info emacs` |
| 获取关于命令的详细信息？ | `man` | `man cdrecord` |
| 查看当前目录的完整路径名称？ | `pwd` | `pwd` |
| 正确设置时区？ | `tzselect` | `tzselect` |
| 找出我运行的是哪个版本的 Linux 内核？ | `uname` | `uname` |
| 找出我在这次会话中使用 Linux 的时间有多长？ | `uptime` | `uptime` |
| 找出谁还在使用此系统？ | `w`, `who` | `w` |

### 在 Linux 上获取帮助

本节介绍以下内容：

- 在 Linux 上获取帮助
- 在线获取帮助

对于 Linux 命令的帮助，主角是 `man` 命令，它在屏幕上显示命令文档。几乎所有 Linux 命令和实用工具都有手册页，称为 `man pages`。这些文档以标准格式提供关于命令的信息。不太有用的是 `info` 命令，它提供了一个基于文本且相当令人困惑的超文本环境，用于有关 GNU 实用工具的信息；以及 `help` 命令，它提供对 bash shell 内置命令的简短一两句描述。通常，info 中可用的信息也可以在 man 页面中找到。同样，您将在 bash man 页面中找到关于内置 bash 命令的信息——比 `help` 命令提供的信息要多得多。您还可以尝试浏览 `/usr/doc` 目录，其中包含已安装应用程序的额外文档。

**提示** 如果您忘记了命令可以使用哪些选项，请在命令名后输入空格和 `-help`，如下例所示：`cal -help`。并非所有命令都支持此选项，但大多数命令都支持。

除了在使用 Linux 期间可用的命令外，你还可以获取在线帮助。“在线获取帮助的途径”表格为基于 Internet 的 Linux 帮助提供了一些极好的资源。请参阅“主要的 Linux 网站”表格，以获取最新的 Linux 新闻、信息和技巧。

### 在线获取帮助的途径

| 网站 | URL | 描述 |
| :--- | :--- | :--- |
| CNET Linux 帮助 | http://searchlinux.com/ | 提供一个搜索界面，用于搜索成千上万条关于 Linux 的 Usenet 消息。 |
| Linux 常见问题解答 | http://metalab.unc.edu/mdw/FAQ/Linux-FAQ.html | 面向初学 Linux 用户的入门级 FAQ（常见问题解答）。 |
| Linux Gazette 搜索页 | http://www.linuxgazette.com/wg/index.html | 提供一个搜索界面，用于搜索数百篇在线的 Linux Gazette 文章。 |
| Linux 硬件数据库 | http://lhd.datapower.com/start.html | 提供有关硬件和外围设备与 Linux 兼容性的信息。 |
| Linux HOWTO 索引 | http://metalab.unc.edu/mdw/HOWTO/HOWTO-INDEX.html | 在线 HOWTO 文档的索引。 |
| Linux 信息表 | http://metalab.unc.edu/mdw/HOWTO/INFO-SHEET.html | 有关 Linux 操作系统的事实和信息。 |
| Linux Online! | http://www.linux.org/help/irc.html | 列出几十个与 Linux 相关的 Internet 中继聊天（IRC）频道。 |
| Linux 知识库 | http://linuxkb.cheek.com | 提供一个搜索界面，用于搜索关于 Linux 的经审核的讨论。 |
| Linux Online! 邮件列表 | http://www.linux.org/help/lists.html | 列出几十个与 Linux 相关的邮件列表。 |
| Linux Online! 项目指南 | http://www.linux.org/help/projectguide.html | 提供有关 Linux 的全文书籍在线版本的访问权限。 |
| Linux 软件地图 | http://www.execpc.com/~ls/ | 提供一个搜索界面，用于搜索 Linux 软件数据库。 |

### 主要的 Linux 相关网站

| 网站 | URL | 描述 |
| :--- | :--- | :--- |
| Linux Today | http://www.linuxtoday.com | 有关 Linux 的最新新闻，包括指向 Linux 相关新闻文章的链接。 |
