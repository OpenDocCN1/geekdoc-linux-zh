
用于登录系统的 `login(1)` 命令，可以配置为在 root 账户登录系统时生成 `auth.notice` syslog 消息。此外，多次以 root 身份登录失败的尝试也会被记录为 `auth.crit` syslog 消息。如果 `/etc/default/login` 文件中包含以下条目，则这些消息会由 `login` 命令生成：

```text
SYSLOG=YES
```

## 由 Internet 服务生成的消息

用于启动标准 Internet 服务的 Internet 服务守护进程 `inetd(1M)`，可以配置为跟踪传入的 TCP 连接，方法是将客户端 IP 地址、TCP 端口号和服务名称作为 `daemon.notice` syslog 消息进行记录。要启用此日志记录，请在 `/etc/init.d/inetsvc` 文件末尾的 `inetd` 命令中添加 `-t` 命令行参数。

## 审计登录账户和进程

有几条命令可用于监视系统和用户登录账户的使用情况。此外，您还可以使用几条命令来识别系统上当前正在运行的进程以及相关的登录账户。

### who 命令

您可以使用 `who(1)` 命令来确定当前登录到本地系统的系统账户和用户账户。不带参数时，`who` 命令会列出登录账户名称、终端设备、登录日期/时间，以及可选的 X Window 系统终端（:0.0）指示：

```text
$ who
root        console      Apr  4 18:57   (:0)
root        pts/5        Apr  8 22:13   (:0.0)
dla         pts/6        Apr 11 21:06   (winnt40)
$
```

当指定 `-q` 命令行参数时，仅显示登录账户名称和当前登录的用户数量，如下例所示：

```text
$ who -q
root    root    dla
# users=3
$
```

### whodo 命令

`whodo(1M)` 命令用于确定每个登录账户正在执行的进程。以下示例显示了（除其他内容外）用户 dla 正在使用 `vi(1)` 命令：

```text
# whodo
Thu Apr 19 02:22:25 EDT 2001
solaris8

    console       root    16:16
        ?         423    0:00 xsession
      pts/2       467    0:00 sdt_shell
      pts/2       483    0:00 ttsession
      pts/2       484    0:01 dtsession
        ?        1091    0:00 dtcscreen
        ?         491    0:04 dtwm
        ?         507    0:00 dtaction
        ?         492    0:01 sdtperf-meter
      pts/2       470    0:00 sh
?       433    0:00 fbconsole
?       468    0:00 dsdm

pts/3   root    16:17
pts/3   515     0:00 sh

pts/4   dla     11:02
pts/4   1051    0:00 sh
pts/4   1097    0:00 vi
```

当指定 `-l` 命令行参数时，会显示附加详细信息：

```text
# whodo -l
2:23am  up 14 day(s), 7 hr(s), 27 min(s)  3 user(s)
User  tty      login@    idle    JCPU  PCPU what
root  console  4Apr01    4days
root  pts/5    4Apr01    2days   1      /usr/bin/sdt_shell -c
                                                -sh
 dla  pts/6    11Apr01   8       8     whodo -l
#
```

此外，如果在 `-l` 命令行参数后指定登录账户名称，则仅显示该登录账户的信息。

`w(1)` 命令（未列为测试目标）可用于列出当前登录到系统的用户。其输出与 `whodo` 命令的输出类似。

### last 命令

`last(1)` 命令显示登录和注销信息。您可以使用此命令确定哪些账户登录到系统，并显示账户上次使用的时间（从最近开始）。以下示例显示了 `last` 命令的部分输出：

```text
# last
dla       ftp       winnt40 Fri Apr  6 02:10 - 02:33 (5+00:22)
root      console   :0      Wed Apr  4 18:57  still logged in
reboot    system boot         Wed Apr  4 18:56
root      console   :0      Wed Apr  4 18:52 - 18:53 (00:01)
reboot    system boot         Wed Apr  4 18:51
root      console   :0      Tue Apr  3 21:46 - 18:49 (21:02)
```

dla 账户于 4 月 6 日 2:10 从 “winnt40” 系统登录，并于当天 2:33 注销。该示例还显示 root 账户仍然从控制台登录到系统。要仅列出特定登录账户的信息，请将账户名称指定为命令行参数：

```text
# last dla
dla       ftp       winnt40 Fri Apr  6 02:10 - 02:33 (5+00:22)
#
```

### 练习题

#### 问题 1

以下哪条命令用于确定某个特定登录账户最后一次使用的时间？

- ○ a. `logins`
- ○ b. `last`
- ○ c. `whodo`
- ○ d. `ps`

答案 b 正确。`logins` 命令显示登录账户的属性，而不是这些登录账户的使用情况。因此，答案 a 不正确。`whodo` 和 `ps` 命令列出的是进程相关信息。因此，答案 c 和 d 不正确。

#### 问题 2

`/etc/syslog.conf` 文件被修改，以捕获来自某个用户应用程序的消息，但日志文件仍然不包含这些消息。以下哪些原因可以解释这种情况？（选择所有适用项。）

- □ a. 添加的 `/etc/syslog.conf` 条目中存在拼写错误。
- □ b. `syslogd` 程序未重新启动。
- □ c. 用户应用程序未生成预期的设施和/或消息严重级别。
- □ d. `syslogd` 程序未运行。
- □ e. 检查了错误的日志。

答案 a、b、c、d 和 e 均正确。它们都是 syslog 设施无法按预期工作的原因。存在拼写错误的条目会被忽略，或导致其他条目被误解。`syslogd` 命令仅在启动时或收到 `SIGHUP` 信号时读取 `/etc/syslog.conf` 文件。`/etc/syslog.conf` 条目必须与用户应用程序提交消息时使用的预期设施/严重级别匹配。如果 `syslogd` 命令未运行，则无法接收和处理消息。请确保消息被发送到预期的日志文件。

#### 问题 3

指出将 `who` 命令与 `ps` 命令结合起来的命令名称。

正确答案是 `whodo`。

#### 问题 4

以下哪些是 syslog 消息的源设施？（选择所有适用项。）

- [ ] a. `login`
- [ ] b. `news`
- [ ] c. `local8`
- [ ] d. `kern`

答案 `b` 和 `d` 正确。`news` 和 `kern` 是 syslog 消息的源设施。与登录系统相关的源设施是 `auth`（而不是 `login`）。因此，答案 `a` 不正确。八个本地定义的源设施为 `local0` 到 `local7`。因此，答案 `c` 不正确。

#### 问题 5

以下哪些是 `logger` 命令的有效命令行参数？（选择所有适用项。）

- [ ] a. `-p`（指定优先级）
- [ ] b. `-l`（改为将消息发送到 `loghost` 系统）
- [ ] c. `-t`（指定随消息包含的标签）
- [ ] d. `-L`（指定应使用的日志文件）
