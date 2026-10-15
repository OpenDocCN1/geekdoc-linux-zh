
使用 `sudo` 的主要优势之一是它提供的日志记录功能。默认情况下，所有 `sudo` 日志消息都通过 `local2` 设施（关于 `syslog` 工具的更多信息，请参阅第 8 章；关于可以更改此行为的选项，请参阅第 175 页的表 9.1）由 `syslogd` 处理。标准的 Red Hat `5.2/6.0 /etc/syslog.conf`（关于第 8 章第 165 页的示例 8-1）条目将级别为 `info` 及以上的所有消息放入 `/var/log/messages` 文件。你可能希望将所有 `sudo` 日志隔离到特定位置，在这种情况下，`/etc/syslog.conf` 可能如示例 9-13 所示。显示的条目将使所有 `sudo` 消息写入本地系统的 `/var/log/sudo.log`；它们也会被发送到主机 `central` 上运行的 `syslogd`。

### 示例 9-13 在 `/etc/syslog.conf` 中隔离 `sudo` 日志条目

```
# cat /etc/syslog.conf
*.info@mail.none:authpriv.none;local2.none			/var/log/messages
<output snipped>
...
local2.debug					/var/log/sudo.log
local2.debug					@central
#
```

## 读取 `sudo` 日志

示例 9-14 向我们展示了一些来自 `sudo` 的示例日志条目（由于格式限制导致换行）。每个日志条目包含日期、时间戳、执行主机名、用户名、终端名称、当前工作目录、执行的用户命令以及命令本身。在示例 9-14 的第一条目中，请注意 `COMMAND=/bin/bash`。此条目可能由 `sudo -s` 或 `sudo /bin/bash` 生成。特别要注意的是，存在

### 示例 9-14 典型的 `sudo` 日志条目

```
Mar  9 15:01:55 f0ghorn sudo:     mary : TTY=ttyp0 ; PWD=/home/mary ;
USER=root ; COMMAND=/bin/bash
Mar 10 05:06:30 f0ghorn sudo:     paul : TTY=ttyp0 ; PWD=/home/paul ;
USER=root ; COMMAND=/usr/sbin/lpc restart all
Mar 10 05:16:13 f0ghorn sudo:     paul : TTY=ttyp0 ; PWD=/home/paul ;
USER=root ; COMMAND=validate
Mar 10 05:57:33 f0ghorn sudo:     paul : command not allowed ; TTY=ttyp0
; PWD=/home/paul ; USER=root ; COMMAND=/sbin/shutdown now
Mar 10 06:49:17 f0ghorn sudo:     paul : TTY=ttyp0 ; PWD=/home/paul ;
USER=root ; COMMAND=list
```

请注意，`mary` 在第一条日志条目之后没有其他记录。她在 `sudo` 调用 shell 之后执行的任何操作都不会被记录。对于 `vi` 等命令也是如此；在 `vi` 会话中输入的任何命令（包括 shell 转义命令）都不会被记录。²

在下一条记录中，我们看到 `paul` 执行了 `lpc`。在那条记录之后，我们看到 `COMMAND=validate`。这意味着 `paul` 执行了 `sudo -v` 以重新初始化他的凭证。之后，我们看到 `paul` 尝试运行 `shutdown` 但被拒绝的记录；`sudo` 在此条目中生成了错误信息“command not allowed”。最后，我们看到包含 `COMMAND=list` 的条目。这意味着 `paul` 执行了 `sudo -l`。

`sudo` 工具生成大量的日志条目——比通常从 `pam_wheel` 和 `su` 看到的信息要多得多。`sudo` 的大量日志记录本身往往就足以成为使用它的动机。从安全和管理角度来看，这些日志都极具价值。

不幸的是，大量的日志记录也意味着必须花费更多时间分析日志。别担心！第 17 章讨论了许多自动化分析日志文件的方法。

## PAM 和 `sudo`

PAM, PAM, PAM... 精彩的 PAM！有关 PAM 的更多信息，请参见第 5 章。

由于 `sudo` 是支持 PAM 的（我们就是这样编译它的——参见第 177 页的示例 9-1），我们可以创建一个 `/etc/pam.d/sudo` 文件。示例 9-15 展示了如何使用 `pam_if` 和 `pam_opie`（参见第 143 页的 OPIE 和 PAM）来强制使用 OPIE，除非我们在控制台或直接连接的终端上。

### 示例 9-15 使用 `pam_if` 和 `pam_opie` 的 `/etc/pam.d/sudo` 文件示例

```
auth    sufficient    /lib/security/pam_if.so tty=tty[0-2]
--  pam_pwb.so shadow
auth    required    /lib/security/pam_opie.so
```

> 2. 在 `vi` 中，`:shell` 命令将调用 shell，在这种情况下将是一个 `root` shell。

你不需要使用 PAM 来实现 OPIE 或 S/Key 支持，因为这种支持可以通过独立于 PAM 的配置选项来实现（参见第 175 页的表 9.1）。

如果你通常使用 OPIE 或 S/Key 进行网络连接（换句话说，你在 `/etc/pam.d/login` 和 `/etc/pam.d/ftp` 等其他文件中实现了 `pam_opie`），或者你正在使用 OPIE 或 S/Key 替代程序，那么对于 `sudo`，你也应该像在示例 9-15 中那样或进行类似的操作。如果你实现了此示例，一切都将像以前一样进行，只不过当从控制台或可接受的其他设备以外的来源执行 `sudo` 时，`sudo` 会提示你输入 OPIE OTP。

需要注意的是，截至本文撰写时，`sudo` 仅关注 `auth` 类型的模块。因此，不幸的是，你无法利用像 `pam_time` 这样的会话专用模块。

### 禁用 ROOT 访问

你可能希望部分或完全禁用 `su` 的使用。你至少应禁用到 `root` 的 `su`，并强制所有 `root` 访问通过 `sudo`。实现这一目标的最简单方法在第 5 章第 102 页围绕示例 5-19 的说明中提供。简而言之，你可以配置 `/etc/pam.d/su` 文件，如示例 9-16 所示。相关条目显示在 `lo14` 中。请注意，文件 `/etc/security/sudeny` 必须包含 `root` 以及你希望消除其 `su` 访问的其他任何用户名。如果你希望完全禁用 `su` 的使用，示例 9-17 提供了一种简单的机制来实现此目的。在这里，我们看到在 `/etc/pam.d/su` 文件的顶部添加了 `pam_deny` 条目（显示在 `lo14` 中）。这将拒绝所有 `su` 尝试。

#### 示例 9-16 使用 `pam_listfile` 拒绝 `su`

```text
auth    required    /lib/security/pam_listfile.so onerr=fail \
                item=user sense=deny file=/etc/security/sudeny
auth    required    /lib/security/pam_pwdb.so
account   required    /lib/security/pam_listfile.so
password  required    /lib/security/pam_cracklib.so minlen=20 retry=3
password  required    /lib/security/pam_pwdb.so md5 use_authtok
session   required    /lib/security/pam_pwdb.so
```

#### 示例 9-17 完全禁用 `su`
