
你可以在 `root` 命令行上使用 `date` 命令为系统设置日期和时间。作为 `date` 的参数，你可以列出（无分隔符）月、日、时间和年。在下一年，日期设置为 2008 年 4 月 6 日下午 2:59（04 代表 4 月，06 代表日，1459 代表时间，08 代表 2008 年）：

```
sudo date 0406145908
Sun Apr 6 02:59:22 PST 2008
```

### 使用 cron 调度任务

使用 cron 调度任务允许你在特定间隔自动执行命令。`cron` 守护进程是在特定时间执行调度命令的后台进程。这些命令定义在称为 crontabs 的文件中。你可以使用 `crontab -e` 命令创建或编辑 crontab。

一个 crontab 条目由五个字段组成，每个字段代表时间的一部分，随后是要执行的命令：

`* * * * * command`

- 分 `0-59`
- 小 `0-23`
- 日 `1-31`
- 月 `1-12`
- 星期 `0-6`，其中 `0` 是星期日

你可以使用通配符 `*` 匹配字段中的任何值。例如，`* * * * *` 将每分钟运行一次命令。你还可以使用范围 `-` 和列表 `,` 来指定多个时间。例如，`0 9-17 * * *` 将在每天上午 9 点到下午 5 点每小时运行一次命令，而 `0 0 1 * 1-5` 将每月 1 号周一至周五午夜运行一次命令。

- `MAILTO` 指定任务结果发送到的对象。默认情况下，这些结果将发送给调度该任务的用户，但你也可以将结果发送到特定用户，例如管理员的电子邮件地址，或网络中另一个系统的账户。
- `HOME` 是任务的家目录，在示例中，它是顶级目录。

```bash
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/bin
MAILTO=root
HOME=
```

## cron.d 目录

在频繁使用的系统上，`/etc/crontab` 文件很容易变得拥挤。某些情况下，特定的条目可能需要不同的变量。例如，你可能需要在不同的 shell 下运行某些任务。为了帮助组织 crontab 任务，你可以将 crontab 条目存放在 `cron.d` 目录中。`cron.d` 中的文件均包含与 `/etc/crontab` 格式相同的 crontab 条目。它们可以命名任何名称。它们被视为添加的 crontab 文件，cron 会检查它们以查找运行的任务。例如，Linux 使用 `cron.d` 中的一个 `sysstat` 文件，其中包含运行收集系统统计工具的 crontab 条目。

## cron 命令

你使用 `cron` 命令将你的条目安装到 crontab 文件中。要此操作，创建一个文件并输入你的 crontab 条目。以你喜欢的名称保存此文件，例如 `mycronfile`。然后，要安装这些条目，输入 `crontab` 和该文本文件的文件名。`cron` 命令获取文本文件的内容并在 `/var/spool/cron` 目录下创建一个 crontab 文件，并添加发布命令的用户名。

在此示例中，`root` 用户将 `mycronfile` 的内容安装为 `root` 的 crontab 文件：

```bash
sudo mycronfile
```

这创建了一个文件 `/var/spool/cron`。如果用户 `justin` 安装了一个 crontab 文件，它会创建一个 `/var/spool/cron` 文件。你可以通过 `/etc/cron.allow` 文件来控制普通用户对 `cron` 的使用。只有名称出现在此文件中的用户才能创建自己的 crontab 文件。`/etc/cron.deny` 文件列出了被拒绝 cron 工具的用户，防止他们调度任务。如果两个文件都不存在，则对所有用户拒绝访问。如果用户不在 `/etc/cron.allow` 文件中，则拒绝访问。然而，如果 `/etc/cron.allow` 文件不存在而 `/etc/cron.deny` 文件存在，则所有未列在 `/etc/cron.deny` 中的用户都被允许访问。

## 在 cron 中编辑

永远不要尝试直接编辑 crontab 文件。相反，请使用带有 `-e` 选项的 `crontab` 命令。这将用标准文本编辑器（如 Vi）打开 `/var/spool/cron` 目录下的你的 crontab 文件（crontab 使用由 `EDITOR` 环境变量指定的默认编辑器）。要为 crontab 使用不同的编辑器，通过将编辑器的程序名称分配给 `EDITOR` 变量并导出该变量来更改默认编辑器。通常，`EDITOR` 变量在 `/etc/profile` 脚本中设置。带有 `-l` 选项运行 `crontab` 会显示 crontab 文件的内容，`-r` 选项删除整个文件。使用另一个包含 crontab 条目的文本文件调用 `crontab` 将覆盖你当前的 crontab 文件，并用文本文件的内容替换它。

## 组织调度任务

你可以将管理性 cron 任务组织为两个大类：需要定期运行的常见管理任务，以及需要在特定时间运行的特殊任务。特殊任务可以如下一节所示在 `/etc/crontab` 文件中运行。常见管理任务虽然可以从 `/etc/cron` 文件运行，但将它们组织到专门的 cron 目录中效果更好。在这些目录中，每个任务都存放在它自己的脚本中，该脚本在运行时将调用该任务。假设管理任务需要在每种特定的日期运行，例如，安排在周日早晨的系统维护。对于这类任务，cron 提供了几个用于每天、每月和每年任务的专用目录。每个目录都包含一个时间间隔的 cron 前缀和后缀。`/etc/cron.daily` 目录用于每天需要执行的任务，而每周任务可以放在 `/etc/cron.weekly` 目录中。cron 条目列于表 21-3。

| cron 命令和工具 | 说明 |
| :--- | :--- |
| `crontab options filename` | 以 `filename` 作为参数，将文件中的 crontab 条目安装到 crontab 文件中；这些是在指定时间执行的操作：`-e` 编辑 crontab 文件，`-l` 列出 crontab 文件内容，`-r` 删除 crontab 文件 |
| `Kcron` | KDE 界面 cron 管理工具 |
| `Schedule` | GNOME 界面 cron 管理工具 |
| Cron 文件和目录 |  |
| `/etc/crontab` | 系统 crontab 文件，仅 root 用户可访问 |
| `/etc/cron.d` | 包含多个 crontab 文件的目录，仅管理员可访问 |
| `/etc/cron.d/cron_hourly` | 用于每小时执行任务的目录 |
| `/etc/cron.d/cron_daily` | 用于每天执行任务的目录 |
| `/etc/cron.d/cron_weekly` | 用于每周执行任务的目录 |
| `/etc/cron.d/cron_monthly` | 用于每月执行任务的目录 |
| `/etc/cron.d/cron_yearly` | 用于每年执行任务的目录 |
| `/etc/cron.d/cron.allow` | 允许使用 cron 的用户 |
| `/etc/cron.d/cron.deny` | 禁止使用 cron的用户 |

表 21-3 cron 命令、工具和目录

## 运行 cron 目录

每个目录都包含要运行的脚本。每个组的调度由 `/etc/crontab` 文件决定。Linux 提供了指定的时间，你可以根据需要进行更改。此处显示默认 crontab 文件，带有每天（22）或每月第一天（1）。小时脚本在每小时的一后运行。

```bash
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/bin
MAILTO=
HOME=
# run-parts
0 * * * run-parts /etc/cron.hourly
2 4 * * run-parts /etc/cron.daily
22 4 * * run-parts /etc/cron.weekly
4 1 * * run-parts /etc/cron.monthly
```

> 提示：目录内的脚本按字母顺序运行。如果你需要脚本在其他脚本之前运行，可能需要修改其名称。一种方法是在名称前加数字。例如，在 `cron.weekly` 目录中，`anron` 脚本被命名为 `anachron`，以便它在其他脚本之前运行。

请记住这些简单的目录包含可执行文件。实际调度是由 `/etc/crontab` 文件中的条目执行的。例如，如果 `cron.weekly` crontab 条目中的每周字段从 `0` 改为 `*`，并将每月字段改为 `1`（`22 4 1 * *`），`cron.weekly` 文件中的任务将每月运行而不是每周。

## cron 目录名称

这些目录使用的名称仅为约定。它们对 cron 进程没有特殊含义。你可以创建自己的目录，在其中放置脚本，并调度 `run-parts` 在给定时间运行这些脚本。在下一个示例中，放在 `/etc/cron.mydocs` 中的脚本将在每周三的中午 12 点运行：

`* 12 * * 3 run-parts /etc/cron.mydocs`

## Anacron

对于可能在 cron 预期运行期间关机的系统，你可能需要用 `anacron` 补充 `cron`，`anacron` 在需要执行调度任务时激活。例如，如果系统在安排 cron 任务的周末关机，这些任务将无法执行；然而，`anacron` 在系统重新启动时检查需要执行哪些任务，然后运行它们。它是为仅每天或每周运行一次的任务设计的。

# 464 第七部分：系统管理

对于 `anacron` 任务，你将 `crontab` 放在 `/etc/anacrontab` 文件中。对于每个计划任务，你需要指定执行任务之间的间隔天数（每周 7 天，每月 30 天）、运行时间（以分钟为计数）、任务描述以及要执行的命令。对于备份，使用的命令是 `tar` 操作。

## 系统目录

你的 Linux 文件系统组织成不同的目录，其中包含不同系统功能的文件，如表 21-4 所示。对于基本的系统管理，你应该熟悉存放应用程序的系统程序目录、存放大多数配置文件的系统配置目录（`/etc`）以及存放系统日志（记录系统活动）的日志目录（`/var/log`）。其他系统目录将在各自的章节中介绍，许多将在第25章中讨论。

| 目录 | 描述 |
| /bin | 与系统相关的程序 |
| /sbin | 用于特殊任务的系统程序 |
| /lib | 系统和应用程序库 |
| /etc | 系统、网络服务及应用程序的配置文件 |
| /home | 用户家目录和服务器数据目录，例如 Web 和 FTP 站点文件 |
| /media | CD-ROM 和软磁盘文件系统的挂载点（第23章） |
| /var | 文件不断变化的系统目录，如日志、打印机队列文件和锁文件（第25章） |
| /usr | 用户相关的程序和文件；包括几个关键子目录，如 `/usr/bin`、`/usr/X11` 和 `/usr/doc` |
| /usr/bin | 用户的程序 |
| /dev | 动态生成的目录文件（第25章） |
| /etc/X11 | X Windows 系统配置文件 |
| /usr/share | 共享文件 |
| /usr/share/doc | 应用程序文档 |
| /tmp | 系统临时文件目录 |
| /var/log | 日志目录 |
| /var/log/ | syslog 生成的系统日志 |
| /var/log/audit | auditd 生成的审计日志 |

表 21-4 系统目录

# 第21章：基础系统管理 465

## 程序目录

名称中包含 `bin` 的目录用于存放程序。`/bin` 目录存放基本用户程序，例如登录 shell（`BASH`、`TCSH` 和 `ZSH`）以及文件命令（`cp, mv, rm, in` 等）。`/sbin` 目录存放用于系统管理任务（如 `fsck, fdisk, mkfs`）以及关机和启动操作（如 `init`）的特殊程序。`/usr/bin` 目录存放为用户任务设计的程序文件。`/usr/sbin` 目录存放与用户相关的操作，例如用于添加新用户的 `useradd`。`/lib` 目录存放系统使用的所有库，包括主 Linux 库 `libc` 以及包含所有当前内核模块的子目录 `modules`（注：此处原文为 modules，通常为 modules，此处按原文保留或译为 `modules`）。

## 配置目录和文件

在配置系统的不同元素（如用户、应用程序、服务器或网络连接）时，使用保存在 `/etc` 目录中的配置文件。`/etc` 目录存放了你的系统、网络和服务器配置文件。你可以找到列出文件的 `fstab` 文件、包含系统上主机 IP 地址的 `hosts` 文件以及默认的 BASH shell 配置文件 `/etc/profile`。该目录包含各种子目录，例如用于 Web 服务器配置文件的 `/etc/apache` 以及用于在 `/dev` 中生成设备文件的 `/etc/udev`。你可以通过直接编辑它们的配置文件来配置许多应用程序和服务，尽管最好是使用相应的管理工具。表 21-5 列出了 `/etc` 目录中常见的几个常用配置文件。

## 系统日志：/var/log 和 syslog

在你的系统上执行的任务完成的各种系统日志存储在 `/var/log` 目录中。在这里，你可以找到邮件、新闻以及所有其他系统操作（如服务器日志）的日志。`/var/log/messages` 文件是未被其他日志涵盖的所有系统任务日志。这通常包括启动任务，例如加载驱动程序和挂载文件系统。如果显卡驱动程序在启动时加载失败，你将在这里找到它的错误信息。登录信息也记录在该文件中，显示了谁尝试登录哪个账户。`/var/log/maillog` 文件记录邮件传输和新闻传输。

> 要查看日志，你可以使用 GNOME 日志查看器。

`syslogd` 守护进程管理你系统上的所有日志，并与网络上其他系统的任何日志操作协调。`syslog` 的配置信息保存在 `/etc/syslog.conf` 文件中，其中包含系统日志文件的名称和位置。在这里你可以找到 `/var/log/messages` 和 `/var/log/maillog` 等条目。每当你更改 `syslog.conf` 文件时，都需要重启 `syslogd` 守护进程。

# 466 第七部分：系统管理

| 文件 | 描述 |
| --- | --- |
| /etc/bashrc | Bash 配置文件 |
| /etc/group | 组列表以及每个组的配置 |
| /etc/fstab | 启动系统时自动挂载的文件系统 |
| /boot/grub/menu.list | GRUB 引导程序的 GRUB 配置，由 /etc/menu.list 链接 |
| /etc/event.d | 启动脚本 |
| /etc/initab | 启动脚本 |
| /etc/profile | 默认 shell 配置文件 |
| /etc/modules | 系统中的模块 |
| /etc/motd | 当日消息 |
| /etc/mtab | 挂载的文件系统 |
| /etc/passwd | 用户密码 |
| /etc/services | 服务定义 |
| /etc/shadow | 加密密码 |
| /etc/shells | Shell 列表 |
| /etc/termcap | 终端规范 |
| /etc/xinetd.conf | Xinetd 配置 |
| /etc/cron.d | cron 脚本 |
| /etc/cups | CUPS 配置 |
| /etc/init.d | System V 初始化脚本 |
| /etc/mail | 邮件配置 |
| /etc/skel | 拷贝给新用户 |
| /etc/X11 | X 系统配置 |
| /etc/udev | 生成设备的规则 |
| /etc/hal | 可移动设备的规则 |

表 21-5 常见配置文件和目录

# 第21章：基础系统管理 467

## syslog.conf 条目

`syslog.conf` 中的目由两个字段组成：选择器（selector）和动作（action）。选择器是要记录的服务类型（如邮件或新闻），动作是放置消息的位置。动作通常是一个日志文件，也可以是远程主机或指向另一个程序的管道。服务的类型被称为设施（facility）。`syslog` 守护进程使用几个术语来指定服务的类型（见表 21-6）。

| 设施 (Facilities) | 描述 |
| auth_priv | 安全/授权消息（私有） |
| cron | 守护进程（cron 和 at） |
| daemon | 其他系统守护进程消息 |
| kern | 内核消息 |
| lpr | 打印机子系统消息 |
| mail | 邮件子系统消息 |
| mark | 仅内部使用 |
| news | Usenet 子系统消息 |
| syslog | syslog 内部消息 |
| user | 通用用户级消息 |
| uucp | UUCP 子系统消息 |
| local0 到 local7 | 留作本地使用 |
| 优先级 (Priorities) | 描述：7, 调试消息，优先级最低 |
| info | 6, 提示消息 |
| notice | 5, 通知，正常但重要的情况 |
| warning | 4, 警告 |
| err | 3, 错误消息 |
| crit | 2, 关键情况 |
| alert | 1, 警报，必须采取行动 |
| emerg | 0, 紧急消息，系统不可用，优先级最高 |
| 运算符 (Operators) | 描述 |
| * | 匹配扇中的所有设施或优先级 |
| = | 限制为指定的优先级 |
| ! | 排除指定的优先级及更高的 |
| / | 用于保存消息的文件 |
| @ | 发送消息的主机 |
| | | 发送消息的 FIFO 管道 |

表 21-6 Syslog 设施、优先级和运算符

# 468 第七部分：系统管理
