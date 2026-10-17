
Python 是面向对象的、现代、简洁、可移植的并且特别易于维护。如果你是一个寻找能够随你一起成长的脚本语言的全职系统管理员，请考虑 Python。Python 的官方首页是 `http://www.python.org`。

# Ruby

Ruby 是编程界的新秀。尽管它仍处于走向成名和认可的过程中，但那些了解并使用它的系统管理员表示，它的受喜爱程度与 Perl 不相上下。和 Python 一样，Ruby 是面向对象、高级级且灵活的。Ruby 的官方首页是 `http://www.rubycentral.com`。

# 计划和周期进程

## at: 以后事件的一次性调度

假设你正在写一份关于世界金融周期的电子周专栏，并通过电子邮件发送。为了简化涉及金融市场的法律影响，你特意选择在周五下午 5:00 发送。

```
at 5:00 Friday << EOF
echo "Financial Cycles Report" | mail@example.com
EOF
```

## cron: 周期性调度

`cron` 守护在启动时启动。它每分钟检查一次 `crontab` 文件，以查找按小时、每天、每周、每月运行的任务：

```cron
* * * * /path/to/script.sh
0 * * * * /path/to/script.sh
0 0 * * * /path/to/script.sh
0 0 0 * * /path/to/script.sh
0 0 0 0 * /path/to/script.sh
0 0 0 0 0 /path/to/script.sh
```

`cron` 目录结构在不同的系统版本中可能不同。无论在哪里，都不要直接编辑文件；请使用相应的 `crontab` 命令：

```
/etc/cron.hourly
/etc/cron.daily
/etc/cron.weekly
/etc/cron.monthly
```

有三个修改 `crontab` 的选项：

- `crontab -l`：出当前用户的 `crontab` 到标准输出。
- `crontab -e`：调用默认编辑器编辑 `crontab`。
- `crontab -r`：删除当前用户的所有 `crontab`。

现代 `crontab` 还可以接受文件名作为参数。

```
crontab filename
```

如果引的文件包含正确的 `crontab` 条目，该文件将成为新的 `crontab`。

在 Red Hat 下，`crontab` 命令需要参数或选项。在 Solaris 下，没有参数或选项的 `crontab` 命令将从标准输入读取新的 `crontab` 文件。

先读手册！在使用 `crontab` 之前，请阅读你系统上的 `cron` 和 `crontab` 页面。语法和元数据可能是系统特定的，如果你使用了错误的语法可能会造成损坏。

`crontab` 和 `at` 的区别在于，`crontab` 应用于调度和运行周期性的、重复的任务，而 `at` 任务通常是为了在未来的某个时间运行一次。

> 注意 `/etc/cron.allow` 和 `/etc/cron.deny` 文件控制谁可以在你的系统可以使用 `crontab` 命令。详情请参阅 `crontab` 手页。你也可以通过 `/etc/at.allow` 和 `/etc/at.deny` 文件控制谁可以在你的系统可以使用 `at` 命令。默认情况下，Red Hat Linux 允许任何人使用 `at` 和 `crontab` 命令。

## anacron: 可中断的周期性调度

`cron` 的缺点在于它假设系统会一直运行。但对于 Linux 笔记本系统而言，这并非事实。因此，默认情况下，安装了 `anacron` 并设置为在启动时运行，同时附加恢复操作（具体方法请查看 `/etc/sysconfig/apm-scripts/resume`）。`anacron` 由 `/etc/anacontab` 文件控制，其安装后会查找从 `/etc/cron.daily`、`/etc/cron.weekly` 和 `/etc/cron.monthly` 目录运行的任务。它的结构如下所示：

```
# /etc/anacontab: configuration for anacron
```

# 详情请参见 anacron(8) 和 anacontab(5)。

```
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/usr/bin:/usr/bin
```

# 这些项对于 Red Hat Linux 系统非常有用。

| | | |
| :--- | :--- | :--- |
| 1 5 | cron.daily run-parts /etc/cron.daily | |
| 7 10 | cron.weekly run-parts /etc/cron.weekly | |
| 30 15 | cron.monthly run-parts /etc/cron.monthly | |

这确保了 `cron.daily` 脚本每天运行一次（并且在 `anacron` 运行 5 分钟后执行）。如果每周脚本在超过一周后没有运行，它们会在 `anacron` 启动 10 分钟后运行；如果在 30 天内没有运行，则每周脚本会在 `anacron` 启动 15 分钟后运行。得益于每个 `cron` 目录中的 `@anacron` 脚本，`anacron` 可以帮助确定脚本上一次运行的时间。如果你是一个笔记本电脑用户，并且一直必须手动更新 `slocate` 数据库，你就会注意到这一点。

## cron 示例

系统管理的一个现实问题是磁盘空间不足。接下来的章节提供了一些建议的权宜方法，帮助你掌握系统的运行状况。

### 跟踪系统核心文件

`cron` 总是需要一些设置。我们将仔细通过一个示例来帮助追踪 `cron` 产生的垃圾文件。

使用 `cron` 功能至少需要一个外部文件。请先执行此命令来练习 `cron` 概念：

```
# echo "0,5,10,15,20,25,30,35,40,45,50,55 * * * * date" >/tmp/experiment
```

### 应用与工具

然后按照如下方式调用 `crontab`：

```
# crontab /tmp/experiment
```

最后，输入命令：

```
# crontab -l
```

最后一个命令将带给你一个类似下面的结果：

```
0,5,10,15,20,25,30,35,40,45,50,55 * * * date > /dev/tty
```

当前时间将在你启动实验的窗口中每 5 分钟出现一次。

为了更有用的示例，创建一个名为 `/tmp/entry` 的文件，内容只有以下这一行：

```
@ 2 * * * -name "core*" -exec ls -1 \
```

接下来，使用此命令：

```
# crontab /tmp/entry
```

结果是，每天早上 2:00，`cron` 都会启动搜索 `core` 的任务并将结果通过发送给你。这非常有用，因为 UNIX 系统在某些错误条件下会创建名为 `core` 的文件。这些 `core` 镜像通常很大，很容易填满磁盘上大量令人头疼的空间。通过前面的序列，你每天早上都能在电子邮箱箱中收到一份报告，列出系列可能对你毫无用处的文件的具体位置和大小。

### 监控用户空间

假设你做了一些实验，并积累了一份 `cron` 任务清单来监控系统健康。除了其他任务外，你希望系统在每周一的 2:10 告诉你哪 10 个用户的主目录树（`/home/`）最大。首先进入捕获你调度的所有任务：

```bash
# crontab -l /tmp/entries
```

将此行附加到 `/tmp/entries` 的末尾：

```
10 2 * * 1 du -s /home/* | sort -nr | head -10
```

执行此请求，`cron` 将向你发送你所需要的报告：

```
# crontab /tmp/entries
```

## 自动化 第 19 章

> 注意：`crontab` 文件中的注释可以救你的任务。无疑，它们会让它变得更容易。如果没有出现问题，你可能几个月或几年都不看你的 `crontabs`。要记住为什么你（或他人）创建某个特定项目可能是困难的。简短的描述性注释意味着你不需要查找并检查每个项目调用的脚本。如果你急于弄清楚为什么会出错，反向工程 `cron` 任务可能会特别令人沮丧。

## 使用 cfengine 进行自动化配置管理

管理员执行的大多数常规任务涉及系统配置的某些方面。当你只有一个站点时，可以手动管理新安装和更新，使用检查清单来确保一致性和完整。但一旦你的领域内机器超过十台，自动化就变成了一种必需，而不仅仅是便利——特别是如果你必须支持多个操作系统时。

Mark Burgess 在设计 `cfengine` 时考虑到了这种需求。它以高级、平台无关脚本语言的形式存在，允许管理员用非常少的词汇说明他们希望如何配置系统。你在系统上执行的许多常见任务实际上是内置命令。以下是 `cfengine` 的工作原理：

1. 你构建一个中心配置文件，定义给定系统应该是什么样的。注意，这可能跨越多个文件。
2. 你编写一个本地配置文件，告诉 `cfengine` 如何找到并处理你创建的那个中心配置文件。
