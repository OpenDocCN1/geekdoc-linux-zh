
- 环境变量可以使用 `env` 命令查看。

- 变量可以通过使用 `set` 命令和 `export` 添加到环境中；它们可通过使用 `unset` 删除。

- `/etc/profile` 配置文件在用户登录时执行。

- 对于使用 `bash` shell 的用户，shell 首先查找 `.bash_profile`；如果找不到该配置文件，则查找 `.bash_login`。

- 当 bash 用户注销时，shell 会查找 `.bash_logout` 并执行其中找到的任何命令。

- 而其他配置文件仅在用户登录或注销时运行，`.bashrc` 文件可在每次运行 shell 时执行。

- Shell 脚本必须具有可执行权限才能运行，或必须由 shell 调用 (如 `sh script`)。任何脚本或应用程序的正常退出状态为 `0`；其他任何值表示非正常退出。

## 用户界面和桌面

表 2-7 显示了本主题的子主题、权重、描述和关键知识领域。

为了充分应对这些主题，请重点关注以下文件、术语和实用程序：`/etc/inittab`、`/etc/x11/xorg.conf`、盲文显示器、`DISPLAY`、`emacsspeak`、`gdm` 配置文件、手势、`GOK`、高对比度桌面主题、`kdm` 配置文件、大屏幕桌面主题、鼠标键、屏幕阅读器、`orca`、屏幕放大器、屏幕阅读器、慢速/防抖/切换键、粘滞/重复键、`X`、`xdm` 配置文件、`xdpyinfo`、`xhost` 和 `xwininfo`。

### 表 2-7 领域 106 的细分

| 子主题 | 权重 | 描述 | 关键领域 |
|---|---|---|---|
| 安装和配置 X11 | 2 | 安装和配置 X11 | 需具备 X Window 配置以及 X 字体服务器的基本理解。 |
| 设置显示管理器 | 2 | 设置和自定义显示管理器 | 使用 XDM (X Display Manager)、GDM (Gnome Display Manager) 和 KDM (KDE Display Manager)，并能够对 LightDM 进行基本配置。 |
| 无障碍访问 | 1 | 了解并意识到无障碍技术 | 理解辅助技术 (AT) 和键盘设置 (如 AccessX 所能实现的)。主题还包括视觉设置和主题。 |

这里是你在学习本领域时需要了解的十项主要内容：

- `emacspeak` 语音接口是 Linux 上最受欢迎的语音接口之一。

- `xdpyinfo` 实用程序可用于查看有关 X 服务器的信息。它可与 `all` 选项一起使用，以查看服务器支持的所有扩展的信息。

- X 的窗口信息可通过 `xwininfo` 实用程序查看。使用 `-all` 选项可显示所有可能的信息。

- X 的服务器访问控制程序是 `xhost`。该程序用于跨网络连接到主机并在图形界面中工作。

- X 显示管理器 (`xdm`) 是随 X Window System 包含的默认显示管理器。

- `/etc/x11/xorg.conf` 文件是用于初始设置的 X 配置文件。

- 已为 KDE (KDE Accessibility Project) 和 GNOME (GNOME Accessibility Projects) 开发了多个 AT 项目。

- `Orca` 是 GNOME 项目的屏幕阅读器，旨在帮助盲人或视力受损的人。`Orca` 可与 Mozilla Firefox、Thunderbird、OpenOffice.org/LibreOffice 以及其他应用程序配合使用。

- GNOME 屏幕键盘阅读器 (`GOK`) 是另一种辅助技术，它使用 XML 文件并可动态创建键盘以适应用户的需求。

- `慢速键` 可以为键盘首选项配置为仅在按住键时接受输入，从而防止误触被计为输入。`防抖键` 可以配置为忽略快速重复按键；`粘滞键` 可用于模拟同时按键。

## 管理任务

表 2-8 显示了本主题的子主题、权重、描述和关键知识领域。

### 表 2-8 领域 107 的细分

| 子主题 | 权重 | 描述 | 关键领域 |
|---|---|---|---|
| 管理用户和组账户及相关系统文件 | 5 | 添加、删除、暂停和更改用户账户 | 处理用户和组账户，包括为特殊目的和受限账户创建的账户。 |
| 通过调度作业自动化系统管理任务 | 4 | 使用 cron 和 anacron | 通过使用 cron 和 anacron 在定期间隔和特定时间运行作业。 |
| 本地化和国际化 | 3 | 将系统本地化为英语以外的语言以及时区设置、本地设置和环境变量。 | 理解为什么 `LANG=C` 在脚本中有用，并了解如何配置本地设置和环境变量。 |

为了充分应对这些主题，请重点关注以下文件、术语和实用程序：`/etc/at.allow`、`/etc/at.deny`、`/etc/cron`、`/etc/cron.allow`、`/etc/cron.deny`、`/etc/crontab`、`/etc/group`、`/etc/localtime`、`/etc/passwd`、`/etc/shadow`、`/etc/skel`、`/etc/timezone`、`/usr/bin/locale`、`/usr/share/zoneinfo`、`/var/spool/cron/*`、`ASCII`、`at`、`atq`、`atrm`、`chage`、`crontab`、`date`、环境变量、`groupadd`、`groupdel`、`groupmod`、`iconv`、`ISO-8859`、`passwd`、`tzconfig`、`tzselect`、`Unicode`、`useradd`、`userdel`、`usermod` 和 `UTF-8`。

这里是你在学习本领域时需要了解的十项主要内容：

- 用户可以通过手动编辑配置文件或使用 `useradd` 命令添加 (并且用户可以用 `userdel` 删除)。

- `groupadd` 实用程序可用于创建组，`groupdel` 可用于删除组。组可以用 `groupmod` 修改，用户可以用 `newgrp` 命令从一个组移动到另一个组。

- 要安排作业在无人值守模式下仅运行一次，可以使用 `at` 命令。

- 已安排的作业可以用 `atq` 命令查看，并在执行前用 `atrm` 删除。

- 可以通过创建 `at.allow` 文件并在其下方仅放置有效用户名，来限制谁可以使用 at 服务 (`atd`)。

- 你可以创建 `at.deny` 文件——代替 `at.allow`——并在其中放置不能使用该 at 服务的用户名 (意味着未列出的人员仍可使用)。

- 如果需要安排无人值守作业按任何规律的间隔运行，可以为其创建 `crontab` (cron 表) 条目。

- `crontab` 文件由 `cron` 守护进程读取，后者每分钟检查是否有作业需要运行。

- 可以通过创建 `cron.allow` 或 `cron.deny` 文件来限制谁可以使用 `cron`。

- `cron` 表中每个条目有六个字段：作业运行的分钟 (`0` 到 `59`)、作业运行的小时 (`0` 到 `23`)、每月的日期 (`1` 到 `31`)、每年的月份 (`1` 到 `12`)、每周的日期 (`0` 到 `6`) 以及要运行的可执行文件的路径。

## 关键系统服务

表 2-9 显示了本主题的子主题、权重、描述和关键知识领域。

### 表 2-9 领域 108 的细分

| 子主题 | 权重 | 描述 | 关键领域 |
|---|---|---|---|
| 维护系统时间 | 3 | 正确维护系统时间并同步时钟 | 使用 NTP 配置和 `pool.ntp.org` 服务。 |
| 系统日志 | 2 | 配置 syslog 守护进程 | 配置日志守护进程 (`syslog`) 将日志输出发送到服务器，使用 `logrotate`，并了解 `rsyslog` 和 `syslog-ng`。 |
| 邮件传输代理 (MTA) 基础 | 3 | 使用常见可用的 MTA 程序 | 能够在主机上执行基本的转发和别名配置。 |
| 管理打印机和打印 | 2 | 管理打印队列和用户打印作业 | 同时使用 CUPS 和旧版 LPD。 |

为了充分涵盖这些主题，请重点关注以下文件、术语和实用程序：`/etc/cups`、`/etc/localtime`、`/etc/ntp.conf`、`/etc/timezone`、`/usr/share/zoneinfo`、`~/.forward`、`CUPS` 配置文件/工具/实用程序、`date`、`exim`、`hwclock`、`klogd`、`logger`、`lpd` 旧版接口 (`lpr`, `lprm`, `lpq`)、`mail`、`mailq`、`newaliases`、`ntpd`、`ntpdate`、`pool.ntp.org`、`postfix`、`qmail`、`sendmail`、`syslog.conf`、和 `syslogd`.

以下是您在学习本领域时应了解的十大要点：

- 网络时间协议（NTP）守护进程（`ntpd`）维护使用 NTP 的所有服务器的时间。

- `hwclock` 命令可用于显示系统硬件时钟（也称为实时时钟）的日期和时间。

- 时区在 `/etc/timezone` 文件中配置。本地时间同样在 `/etc/localtime` 中配置。

- `sendmail` 服务是一种通用 SMTP 程序，用于在服务器之间发送电子邮件。
