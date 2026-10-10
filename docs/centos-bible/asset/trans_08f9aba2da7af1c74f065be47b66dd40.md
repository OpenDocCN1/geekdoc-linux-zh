
# 第三部分 管理

该文件会自动在您定义的 `EDITOR` 或 `VISUAL` 环境变量中指定的文本编辑器中打开，默认编辑器为 `vi`。完成后，只需退出编辑器即可。假设没有语法错误，您的 crontab 文件将会被安装。例如，如果您的用户名是 `jsmith`，您刚刚创建的文件就是 `/var/spool/cron/jsmith`。如果您添加了一行带描述性注释的行，或者当然也可以从源代码目录中删除任何旧的 core 文件，该文件可能类似于以下内容：

```
#  Find and remove core files from /home/jsmith/src
5 1 * * Sun,Wed find /home/jsmith/src -name core.[0-9]* \
-exec rm {} \; > /dev/null 2>&1
```

由于 CentOS 中的 core 文件由单词 `core` 组成，后跟一个点 (.) 和进程 ID，因此本示例将匹配所有以 `core.` 开头后跟数字的文件。root 用户可以通过使用 `crontab` 命令的 `-u username` 选项来访问任何用户的个人 crontab 文件。

> **注意** cron 任务是在一个非常基本的环境中启动的，该环境仅包含有限的 `PATH`。任务中的程序要么以完整路径输入，要么在 crontab 文件开头应有一个 `PATH` 定义。

## 理解 cron 文件

设置了独立的 cron 目录，用于存放每小时、每天、每周和每月运行的 cron 任务。这些 cron 任务均设置为从 `/etc/crontab` 文件中运行。默认的 `/etc/crontab` 文件看起来像这样：

```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

前四行初始化所有后续作业的运行时环境（每个作业运行的子 shell、可执行程序搜索路径、输出和错误消息的接收者以及该用户的主目录）。接下来的五行以用户 `root` 身份执行 `run-parts` 程序，该程序控制您可能希望定期运行的程序。

`run-parts` 是一个将目录作为命令行参数的 shell 脚本。然后它会顺序执行该目录内的每个程序（shell 脚本最为常见，但也评估二进制可执行文件和链接）。默认配置在每天每小时的第 1 分钟执行 `/etc/cron.hourly` 中的程序；每天凌晨 4:02 执行 `/etc/cron.daily`；每周日凌晨 4:22 执行 `/etc/cron.weekly`；以及每月 1 日凌晨 4:42 执行 `/etc/cron.monthly`。

以下是安装在不同软件包 cron 目录中的文件示例：

- `/etc/cron.daily/logrotate.cron` — 自动轮转、压缩和处理系统日志文件。
- `/etc/cron.daily/makewhatis.cron` — 更新 whatis 数据库（包含 man 页面的描述），该数据库由 man -k、apropos 和 whatis 命令使用以查找与特定单词相关的 man 页面。
- `/etc/cron.daily/slocate.cron` — 使用 updatedb 命令更新 /var/lib/slocate/slocate.db 数据库，其中包含机器上文件的可搜索列表。
- `/etc/cron.daily/tmpwatch` — 删除 /tmp、/var/tmp 和 /var/catman 中 10 天内未访问的文件。

安装在 /etc/cron.weekly 中的 makewhatis.cron 脚本与 /etc/cron.daily 中的类似，但它完全重建 whatis 数据库，而不仅仅是更新现有数据库。

最后，/etc/cron.d 目录中的文件具有与 /etc/crontab 文件相同的格式。

> **注意** 如果您不习惯从命令行使用 cron，kdeadmin 软件包中提供了一个 KControl 任务调度器窗口，用于管理 cron 任务。要启动 KControl，请在终端窗口中输入 kcontrol。

## 摘要

Shell 脚本是 CentOS 系统配置、启动、管理和定制的组成部分。它们用于消除重复命令的输入。它们通常从 CentOS 中的调度设施执行，从而在确定进程何时运行以及运行频率方面提供了很大的灵活性。它们还控制启动时大多数守护进程和服务器进程启动。

init 守护进程及其配置文件 /etc/initab（注：此处原文可能意指 /etc/inittab）在 CentOS 系统的初始启动中起着重要作用。它们实现了由 /etc/rc.d/init.d 中的 shell 脚本执行的运行级别概念，并提供了以有序方式关闭或重新启动机器的机制。

要使 shell 脚本配置为持续运行，您可以使用 cron 设施。可以通过直接编辑 cron 文件来添加 cron 作业，或者通过运行 at 和 batch 等命令来输入要运行的命令。

# 第 12 章

# 创建备份和恢复数据

如果您曾遭受硬盘崩溃之苦，您就知道那有多令人沮丧。您可能会丢失不可替代的数据。您很可能花费了无数小时重新安装操作系统和应用程序。这并不是一段愉快的经历。只需经历一次，您就能认识到定期备份关键数据的重要性。

如今，更大、更快的备份介质简化了数据备份过程。CentOS 支持许多不同类型的介质——例如可写光盘（CD-R 和 CD-RW）、DVD（DVD-R、DVD+R、DVD+RW 和 DVD-RW）以及磁带——用于创建备份。使用 *cron* 等工具，您可以配置备份在计划时间无人值守地运行。

本章描述了如何创建备份策略以及如何为 CentOS 系统上的数据备份选择介质。它告诉您如何执行自动备份和网络备份。它还描述了如何使用 *restore* 命令等工具恢复单个文件或整个文件系统。

# 制作简单的备份归档

GNOME 桌面在处理可移动介质（CD、DVD、USB 闪存盘等）方面的改进可以帮助您快速备份个人数据。在 CentOS 系统上运行 GNOME 桌面时，使用以下程序备份主目录中的所有数据。

- **本章内容**
- 执行简单备份
- 选择备份策略
- 选择备份介质
- 备份到硬盘
- 使用 dump 备份文件
- 使用 *cron* 自动执行备份
- 恢复备份文件
- 使用 Amanda 进行网络备份
- 使用多台计算机执行网络备份
- 使用 *pax* 归档实用程序

1. 将一张空白 CD 或 DVD 插入计算机的光驱。桌面上会出现一个图标，表示空白磁盘已准备好使用。
2. 双击“Blank Disc”图标以查看 CD/DVD Creator 窗口。或者，从弹出的窗口中选择 CD/DVD Creator。
3. 打开桌面上代表您主目录的文件夹图标（例如 mike 的 Home），并浏览到 /home 文件夹。
4. 将您的主目录从 /home 文件夹拖放到 CD/DVD Creator 窗口中。
5. 以相同方式将您要备份的其他文件和文件夹添加到 CD/DVD Creator 窗口中。
6. 当您要将备份的所有文件和文件夹都复制到 CD/DVD Creator 窗口时，单击“Write to Disc”，将出现“Write to Disc”弹出窗口。
7. 为备份介质输入磁盘名称，并可选择 Write speed。如果之后在 GNOME 桌面上打开 CD/DVD，该磁盘名称将用作挂载点的名称。图 12-1 显示了“Write to Disc”弹出窗口和 CD/DVD Creator 窗口（其中用户 mike 的主文件夹已拖入该文件夹）。

### 图 12-1

在 CD/DVD Creator 窗口上拖放文件和文件夹以进行简单备份。单击 Write 将文件和文件夹写入磁盘。

![](img/2f265415ceec72538dd3c78ffca75c10_501_0.png)

此程序会导致标准 ISO9660 映像带有 Rock Ridge 扩展烧录到 CD 或 DVD 上。该磁盘可以从 Linux、Windows 或其他支持该格式的系统读取

