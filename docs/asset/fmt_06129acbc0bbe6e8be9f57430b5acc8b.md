
首先，加载 `parport` 和底层驱动程序（参见第 267 页的*并行端口*一节）。

示例：`modprobe pt`

### 并行端口通用 ATAPI 设备

模块名称：`pg.o`

首先，加载 `parport` 和底层驱动程序（参见第 267 页的*并行端口*一节）。

示例：`modprobe pg`

## SuSE Linux 的特殊功能

本章提供有关*文件系统层次结构标准（FHS）*和*Linux 标准规范（LSB）*、各种软件包以及使用“initrd”启动、linuxrc 和“救援系统”等特殊功能的信息。

- 文件系统层次结构标准（FHS）和 Linux 标准规范（LSB） ........ 272
- FTP 和 HTTP 的示例环境 ........ 272
- 关于特殊软件包的提示 ........ 273
- 使用初始 RAM 磁盘启动 ........ 276
- linuxrc ........ 281
- SuSE 救援系统 ........ 285
- 虚拟控制台 ........ 290
- 键盘布局 ........ 291
- 本地调整 — I18N/L10N ........ 292

## 文件系统层次结构标准（FHS）和 Linux 标准规范（LSB）

### 文件系统层次结构标准（FHS）

SuSE Linux 尽可能遵循文件系统层次结构标准（FHS，软件包 `fhs`，系列 doc。另请参见 http://www.pathname.com/fhs/）。因此，有时有必要将文件或目录移动到文件系统中它们的“正确”位置。

### Linux 标准规范（LSB）

SuSE 支持 Linux 标准规范（LSB）项目。有关此项目的最新信息可在 http://www.linuxbase.org 找到。

8.0 的 LSB 规范版本为 1.0。今后，文件系统层次结构标准（FHS）被包含在该规范中，并定义了软件包格式和系统初始化等设置。参见第 297 页的“SuSE Linux 启动概念”一章。

### teTeX — SuSE Linux 中的 TeX

teTeX 按照 TeX 目录结构（TDS）组织而成（参见 ftp://ftp.dante.de/tex-archive/tds/），同时又不损害 FHS。

## FTP 和 HTTP 的示例环境

### 关于 FTP

为了简化 FTP 服务器的设置，软件包 `ftpdir` 包含一个示例环境。它安装在 `/usr/local/ftp`。

### 关于 HTTP

Apache 是 SuSE Linux 中的标准 Web 服务器。安装 Apache 后，`/usr/local/httpd` 中会提供一些示例文档。要设置自己的 Web 服务器，建议在 `/etc/httpd/httpd.conf` 中输入您自己的 DocumentRoot。

## 关于特殊软件包的提示

### 软件包 cron

cron 表现在位于 `/var/cron/tabs`（而不是以前的 `/var/lib/cron`）。`/etc/crontab` 用作系统范围的 cron 表。请在时间表之后直接输入应运行该命令的用户名（参见文件 36，其中输入了 root）。位于 `/etc/cron.d` 的软件包专用表具有相同的格式。参见 cron 的手册页（`man 8 cron`）。

```
1-59/5 * * * * root test -x /usr/sbin/atrun && /usr/sbin/atrun
```

> *文件 36：/etc/crontab 中的条目示例*

`/etc/crontab` 不能通过 `crontab -e` 处理。必须直接加载到编辑器中进行修改，然后保存。

许多软件包将 shell 脚本安装到目录 `/etc/cron.hourly`、`/etc/cron.daily`、`/etc/cron.weekly` 和 `/etc/cron.monthly` 中，这些脚本由 `/usr/lib/cron/run-crons` 控制。`/usr/lib/cron/run-crons` 每十五分钟从主表（`/etc/crontab`）运行一次。这保证了可能被忽略的进程能够在适当的时间运行。如果在启动后不久，用户 nobody 出现在进程表中并且十分活跃，不必感到奇怪。这很可能只是 nobody 在更新区域设置（locale）（参见第 316 页的*安全与本地管理服务*一节）。

### 日志文件 — logrotate 软件包

许多系统服务（“守护进程”）与内核本身一样，会定期将系统状态和特定事件记录到日志文件中。这样，管理员可以定期了解系统在特定时间点的状态，识别错误或故障功能，并进行故障排除以达成有针对性的解决方案。这些日志文件通常按照 FHS 的规定存储在 `/var/log` 中，并且每天都会增长。软件包 `logrotate` 有助于控制这些文件的增长。

### 更新到 logrotate（8.0）

更新到 8.0 时，将采用下面列出的旧设置：

- 来自 `/etc/logfile` 且未与特定软件包关联的条目会被移动到 `/etc/logrotate.d/aaa_base`。
- 原 `rc.config` 文件中的变量 `MAX_DAYS_FOR_LOG_FILES` 被映射为 dateext，并在配置文件中管理。请参阅 `logrotate` 的手册页（`man 8 logrotate`）。

### 配置

使用 `/etc/logrotate.conf` 文件配置 logrotate。特别是，include 指令主要配置要读取的其他文件。SuSE Linux 确保各个软件包将文件安装到 `/etc/logrotate.d`（例如 `syslog` 或 `yast`）。`/etc/cron.daily/logrotate` 每天通过 cron 激活 logrotate 本身。

> **注意**
>
> create 选项包含在 `/etc/permissions/*` 中完成的所有设置。请确保您自行进行的任何修改都不会引起冲突。参见第 304 页。

### 手册页

对于某些 GNU 应用程序（如 tar），其手册页已不再维护，取而代之的是 info 文件。info 是 GNU 的超文本系统。输入 `info info` 可获得使用 info 的入门帮助。`info` 可以通过 `emacs -f info` 启动，也可以直接运行 `info`。程序 `tkinfo` 和 `xinfo` 很容易单独使用来访问 SuSE 帮助系统。

### ulimit 命令

使用 `ulimit`（用户限制）命令，可以设置系统资源的使用限制并显示这些限制。`ulimit` 在限制应用程序可用内存方面尤其有用。通过这种方式，可以防止应用程序自行使用过多内存。这可能导致系统陷入停顿。

`ulimit` 可以使用多种选项。要限制内存使用量，请使用下一页中表 11.1 列出的选项。

- `-m` — 物理内存的最大大小
- `-v` — 虚拟内存（交换空间）的最大大小
- `-s` — 堆栈的最大大小
*表 11.1：接下页…*
- `-c` 核心转储文件的最大大小
- `-a` 显示已设置的限制
*表 11.1：`ulimit`：为用户设置资源*

系统范围的设置可以在 `/etc/profile` 中进行。在其中，必须启用创建核心转储文件的功能，程序员进行“调试”时需要用到这些文件。普通用户不能提高系统管理员在 `/etc/profile` 中指定的值，但可以在自己的 `~/.bashrc` 中添加特殊条目。

```sh
# 物理内存限制：
ulimit -m 98304

# 虚拟内存限制：
ulimit -v 98304
```

### *文件 37：`ulimit`：`~/.bashrc` 中的设置*

内存的详细信息必须以 KB 为单位指定。如需更详细的信息，请查看 bash 的手册页。

## free 命令

如果你的目标是了解当前正在使用多少 RAM，`free` 命令多少会有些误导性。

相关信息可以在 `/proc/meminfo` 中找到。如今，能够使用 Linux 这类现代操作系统的用户，确实不必过于担心内存问题。“可用 RAM”的概念要追溯到统一内存管理出现之前。*空闲内存是糟糕的内存*这句口号非常适合 Linux。因此，Linux 始终致力于平衡缓存，而不是真正允许空闲或未使用的内存存在。

基本上，内核并不直接了解任何应用程序或用户数据。相反，它在“页缓存”中管理应用程序和用户数据。如果内存不足，其中的一部分会被写入交换分区或文件，之后可以借助 `mmap` 命令（参见 `mmap` 的手册页（`man 2 mmap`））重新读回。

此外，内核还控制其他缓存，例如“slab 缓存”，其中存储了用于网络访问的缓存。这可以解释 `/proc/meminfo` 中计数器之间的差异。其中大多数（但不是全部）可以通过 `/proc/slabinfo` 访问。

## 文件 /etc/resolv.conf
