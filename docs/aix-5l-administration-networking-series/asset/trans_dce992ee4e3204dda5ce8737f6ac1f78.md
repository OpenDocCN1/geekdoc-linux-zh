

## 安全注意键

可信计算基（TCB）的安全注意键（SAK）功能可确保用户在通过串行连接终端登录系统时，只能使用可信命令。请注意，SAK 不适用于通过网络建立的会话。

要配置 SAK，root 用户必须修改 `/etc/security/login.cfg` 文件，并在 SAK 需要可用的每个 TTY 端口的配置项中添加 `sak_enabled=true`。完成此操作后，已获得 SAK 使用权限并通过该 TTY 登录的用户可以通过输入按键组合 CTRL-X CTRL-R 来调用可信通信路径。该按键组合应在输入用户名和密码之前输入。

用户调用 SAK 并按照常规方式登录系统后，系统将不再启动常规 shell，而是为该用户启动可信 shell（tsh）。可信 shell 在语法上与 Korn shell（ksh）相似，但有几个关键区别：

- 只能执行可信程序（即被 TCB 标记为可信的程序）。
- 不支持函数和别名定义。
- 无法重新定义 IFS 和 PATH 环境变量。
- 不可用历史记录机制。
- 仅执行 `/etc/tsh.profile` 配置文件；用户主目录中的 shell 配置脚本不会被运行。

## 审计子系统

在讨论安全性时，仅仅定期检查是否有人忘记了锁门往往是不够的。更好的做法是主动接收门被打开的通知。AIX 5L 包含一个审计子系统，可以跟踪和记录任意数量的预定义或自定义系统活动。通过启用审计功能，您可以轻松监控广泛的安全相关事件。请注意，默认情况下，审计功能是禁用的。与审计相关的日志文件可能会迅速增长，且审计过程产生的开销会对系统性能产生轻微但可测量的影响。

### 审计类别

AIX 审计子系统提供四个可监控和记录的通用类别。

### 事件

*事件* 是一种系统活动，通常定义在系统调用级别。每次执行命令时，都会发起若干系统调用。这些系统调用中的每一个都对应一个事件，并会被审计过程记录。事件的名称、导致该事件的命令、执行命令的用户、日期和时间，以及该事件的成功或失败状态都将记录在日志中。

### 类

*类* 简单来说就是事件的分组。一个类可以包含一个或多个事件，将相关事件分组有助于简化审计日志的管理和解释。请注意，AIX 限制为 31 个类（加上包含所有系统事件的 ALL 类）。

### 对象

*对象* 即文件。当特定文件被定义为受审计对象时，所有对该文件的读取、写入和执行尝试都将被记录。

### 用户

*用户类别* 定义了针对特定用户账户要审计的具体事件和类。可以根据用户对可信程度的感知来增加或减少记录的事件数量。

### BIN 模式与 STREAM 模式

审计子系统可以以两种模式运行：BIN 模式或 STREAM 模式。每种模式都有其优势，如果需要也可以同时使用两者。

BIN 模式（二进制模式）将审计数据发送到两个交替使用的“bin”中，并以紧凑的二进制格式将其数据写入文件 `/audit/trail`。它最适合长期存储审计记录。

要将此文件转换为可读格式，必须运行 **auditpr** 命令：

```sh
# /usr/sbin/auditpr < /audit/trail
```

STREAM 模式将审计记录写入文件 `/audit/stream.out`，并在生成时处理审计信息。此文件为纯文本格式，可以边写边读。但请注意，每次重启审计时，该文件都会被擦除。因此，STREAM 模式最适合实时监控受审计事件。

### 审计配置

审计子系统的所有配置文件都位于 `/etc/security/audit` 目录中。

```sh
# ls -l /etc/security/audit
total 56
-rw-r----- 1 root audit     37 Sep 30 1997 bincmds
-rw-rw---- 1 root audit   2116 Nov 06 16:37 config
-rw-rw---- 1 root audit  12236 Nov 06 22:00 events
-rw-rw---- 1 root audit    340 Sep 30 1997 objects
-rw-r----- 1 root audit     54 Sep 30 1997 streamcmds
```

`/etc/security/audit/config` 文件由若干部分组成（stanzas），每个部分定义了审计子系统行为的一个方面。start 部分设置了启动审计时运行的模式——BIN、STREAM 或两者：

```ini
start:
  binmode = on
  streammode = off
```

接下来的两个部分定义了这两种模式的位置和其他行为。对于 BIN 模式，可以定义两个 bin 的名称和位置以及输出文件。STREAM 部分仅包含包含审计流处理命令的文件的位置。

```ini
bin:
  trail = /audit/trail
  bin1 = /audit/bin1
  bin2 = /audit/bin2
  binnsize = 10240
  cmds = /etc/security/audit/bincmds

stream:
  cmds = /etc/security/audit/streamcmds
```

各种类别在下一个部分中详细列出。默认情况下，以下格式定义了十个类别；您可以自由修改这些现有类别或添加自己的类别。

```ini
classes:
  general = USER_SU, PASSWORD_Change, FILE_Unlink, FILE_Link, FILE_Rename, FS_Chdir, FS_Chroot, PORT_Locked, PORT_Change, FS_Mkdir, FS_Rmdir
```

最后一部分 `users` 包含要审计的用户名称，以及为这些用户审计的具体类别。

```ini
users:
  root = general
```

可以通过手动将它们添加到该文件，或在 SMIT 的 **mkuser** 或 **chuser** 屏幕的相应字段中选择要监控的审计类别，来选择要审计的用户：

```sh
# smit chuser
    AUDIT classes                    [general,objects,files] *
```

分配给文件的审计类别必须在 `/etc/security/audit/objects` 文件中定义。该文件中的每个部分列出了要审计的对象名称、要审计的操作（读取、写入和/或执行）以及与该操作相关的事件。

```ini
/etc/security/passwd:
    r = "S_PASSWD_READ"
    w = "S_PASSWD_WRITE"
```

### 启动和停止审计

审计子系统由 `/usr/sbin/audit` 命令控制。完成必要的配置后，执行此命令：

```sh
# /usr/sbin/audit start
```

上述命令将启动系统审计。如果请求以 STREAM 模式进行审计，请注意，`/audit/stream.out` 文件中的任何先前数据都将被清除。如果您希望在每次系统启动时都激活审计功能，IBM 建议将 **audit start** 命令放在 `/etc/rc.file` 中，以便在启动过程的早期阶段监控事件。

要查询审计子系统的状态，请运行以下命令：

```sh
# /usr/sbin/audit query
```

如果审计未处于活动状态，将打印以下信息：

```
auditing off
    bin processing off
    audit events:
            none
    audit objects:
            none
```

如果审计处于活动状态，将显示审计进程的 PID，以及正在监控的事件、类别和对象的列表。要停止审计，请执行以下命令：

```sh
# audit shutdown
```

应将此命令添加到您的 /etc/rc.shutdown 脚本中，以确保审计过程正常终止。可以通过将 off 和 on 指定为 audit 命令的参数来暂停和重启审计。

## 附加安全工具

AIX 拥有大量开源和免费软件工具。这些工具有助于保护您的系统并确保其中存储的数据完整性。以下几个更流行的工具在下面的章节中列出。

请注意，虽然列表中许多工具都提供编译好的、随时可安装的格式，但尽可能从源代码构建程序是一项好的策略。

### John the Ripper

保护系统最重要的一项措施之一就是帮助用户养成好的密码习惯。用户可能不希望得到这种帮助，但他们必须理解这种必要性，并理解创建强密码以保护其账户的重要性。

John the Ripper 是一款密码破解工具。它以加密密码列表作为输入，试图确定其未加密的值。如果 John the Ripper 能够确定用户的密码，那么该密码可能强度不高。

John the Ripper 的主页是 http://www.openwall.com/john/。可以从该网站下载 John 的最新版本的源代码形式，或从 http://www.build.de/pub/ 下载编译好的 LPP 格式。

### Swatch

Swatch，即“简易监视器”，是一个 Perl 应用程序，它持续监控日志文件，查找配置文件定义的模式。当检测到该模式时，swatch 可以执行多种操作，例如执行程序或将检测到的错误电子邮件到指定地址。Swatch 自动化了不断阅读日志文件、从噪音中分离重要条目的繁琐过程。

Swatch 可从 http://eta.cs.colorado.edu/~swatch/ 下载。它需要 Perl，AIX 5L 已包含 Perl。

### Tripwire

Tripwire 是一款文件完整性监控工具，提供免费版和商业版。除了 TCB 提供的功能外，Tripwire 还提供许多其他功能和报告能力。它还适用于多种平台，因此是异构数据中心的绝佳解决方案。商业版提供集中配置、监控和报告。有关 Tripwire 的更多信息，请访问 http://www.tripwire.com/。关于在 AIX 上构建 Tripwire 免费版的说明可参见 IBM eServer

