
### 审计字段说明

- `ppid`: 父进程的进程 ID。
- `uid`: 用户 ID。
- `euid`: 有效用户 ID。
- `suid`: 设置用户 ID。
- `fsuid`: 文件系统用户 ID。
- `gid`: 组 ID。
- `egid`: 有效组 ID。
- `sgid`: 设置组 ID。
- `fsgid`: 文件系统组 ID。
- `auid`: 审计 ID，或用户登录时的原始 ID。
- `msgype`: 消息类型编号。应仅用于排除过滤器列表。
- `pers`: 操作系统个性性编号。
- `arch`: 系统调用的处理器架构。指定具体的架构，例如 `i686`（可以通过 `uname -m` 命令获取）或使用 `b32` 来使用 32 位系统调用表，使用 `b64` 来使用 64 位系统调用表。
- `devmajor`: 设备主号。
- `devminor`: 设备次要号。
- `inode`: Inode 号。
- `exit`: 系统调用的退出值。
- `success`: 系统调用的成功值。用 1 表示真/是，0 表示假/否。
- `a0`, `a1`, `a2`, `a3`: 分别为系统调的前四个参数。只能使用数值。
- `key`: 设置一个过滤器键，用于为事件标记审计日志消息。示例请参见列表 25.2 和列表 25.3。类似于添加监视时的 `-k` 选项。请参考“编写审计规则与监视”中关于 `-k` 选项的详情。
- `obj_user`
- `obj_role`: 资源的 SELinux 角色。
- `obj_type`: 资源的 SELinux 类型。
- `obj_lev_low`: 资源的 SELinux 低级别。
- `obj_lev_high`: 资源的 SELinux 高级别。
- `sub_user`: 程序的 SELinux 用户。
- `sub_role`: 程序的 SELinux 角色。
- `sub_type`: 程序的 SELinux 类型。
- `sub_sen`: 程序的 SELinux 敏感性。
- `sub_clr`: 程序的 SELinux 权限。

`-a` 选项将规则添加到列表。若要将规则添加到列表开头，请将 `-a` 替换为 `-A`。删除规则的语法相同，但将 `-a` 替换为 `-d`。要删除所有规则，请指定 `-d` 选项。列表 25.2 包含了针对 `/etc/audit/audit.rules` 的一些示例审计规则。

### 列表 25.2 示例审计规则

```
# 记录用户 501 打开的所有文件
# 请谨慎使用，因为这会快速
# 产生大量的记录
-a exit,always -S open -F uid=501 -F key=501open
# 记录文件权限更改
-a entry,always -S chmod
```

> 如果安装了审计包，额外的示例位于 `/usr/share/audit-<version>/` 目录下的 `*.rules` 文件中。

当发生触发了定义规则的操作时，如果在 `/etc/audit/auditd.conf` 中定义了分发器，则它将通过分发器发送，然后将日志消息写入 `/var/log/audit.log`。例如，列表 25.3 包含了列表 25.2 中第一条规则的日志条，该规则记录了用户 501 打开的文件。该规则包含一个过滤器键，该键出现在列表 25.3 日志目的末尾。

### 列表 25.3 示例审计规则日志消息

```
type=SYSCALL msg=audit(1168206647.422:5227) arch=c00000a3e syscall=2 success=no
exit=-2 a8=fff77c5ca00 a1=02aaaaaaab00 a3=0 items=1 ppid=2664 pid=2716
uid=501 uid=501 gid=501 euid=501 suid=501 fuid=501 egid=501 sgid=501 fsgid=
type=tty cmd="vim" exe=/usr/bin/vim="501open"
```

## 编写审计监视

Linux 审计系统还允许管理员监控文件和目录。如果对文件或目录放置了监视，成功和失败的操作（如打开和执行文件或目录）将被记录。要审计监视，请使用 `-w` 选项后跟要监视的文件或目录。

> 注意
> 
> 如果你在守护进程运行时添加了 `/etc/audit/audit.rules`，请确保通过 root 身份重启 `service auditd` 服务来启用更改。列表 25.4 包含了包含在 `/etc/audit/audit.rules` 中的示例监视。如果使用 `-w` 使用 `-k <key>` 选项，监视产生的所有记录将包含一个警告（限制字节），以便从审计日志中过滤。要过滤特定文件或目录的操作，使用 `-p` 选项后跟以下之一：`r` 读取，`w` 写入，`a` 追加。要删除监视，使用 `-d` 选项后跟文件或目录。

### 列表 25.4 示例监视

```
# 监控 sysconfig 文件
-w /etc/sysconfig -k SYSCONFIG
# 监控审计文件
-w /etc/audit/audit.rules -k AUDIT_RULES
-w /etc/audit/auditd.conf -k AUDIT_CONF
-w /var/log/audit/ -k LOG_AUDIT
# 监控启动客户端
-w /usr/bin/nc -k NC -p
# 监控密码文件
-w /etc/passwd -k PASSWD
-w /etc/group -k PASSWD
-w /etc/shadow -k PASSWD
```

例如，列表 25.4 包含了对密码文件的监视，键为 `PASSWD`。在删除这些密码文件后，列表 25.5 包含了来自 `/var/log/audit.log` 的日志目的。类似于列表 25.3 中带有过滤器键的规则，键被添加到日志条目的末尾，以便从剩余日志中轻松过滤。

### 列表 25.5 监视示例日志目的

```
type=SYSCALL msg=audit(116822741.566): arch=c0000a3e syscall=82
success=yes exit=0x7ff05d a=6b8a70 a2=0 items=5 ppid=26575
pid=414 comm=userdel audid=501 uid=0 gid=0 suid=0 egid=0 sgid=0 fsgid=0
tty=userdel exec="/usr/sbin/userdel" key="passwd"
```

## 自定义 auditd

配置审计参数的命令行选项也可以包含在 `/etc/audit/audit.rules` 中。表 25.1 列出了这些选项。

### 表 25.1 配置审计系统的 auditctl 选项

| 选项 |  |
| :--- | :--- |
| `-b <backlog>` | 允许的审计缓冲区最大数量。内核默认64。如果所有缓冲区满了，内核将引用 `-f` 设置的失败标记来确定采取的操作。 |
| `-e [0,1]` | 设置为0禁用审计，设置为1启用审计。将其用于临时禁用其他进程的审计。 |
| `-f [0,2]` | 设置失败标记告知内核如何处理缓冲区满或内存不足的错误。值为0（无操作）、1（使用 printk 将消息写入 `/var/log/messages`）和2（崩溃）。默认是1，但2更安全。 |
| `-r <rate>` | 每秒消息限制。如果设置为0则无限制。如果超过限制，内核计算 `-f` 选项的失败标记以确定采取的操作。 |
| `-i` | 从文件读取时忽略错误。 |

要验证它们是否已设置，使用 `auditctl -s` 命令查看状态。输出如下：

```
AUDIT_STATUS:enabled=1 flag=1 pid=1954 rate_limit=0 backlog_limit=256
lost=0 backlog=0
```

## 启动和停止守护进程

配置守护进程并添加规则和监视后，以 root 身份通过 `service auditd start` 启动守护进程。要停止它，使用 `service auditd stop` 命令。要在启动时自动启用，以 root 身份执行 `chkconfig auditd on` 命令。

修改配置时如果守护进程已运行，以 root 身份使用 `service audit restart` 命令启用更改。要验证规则和监视已修改，以 root 身份使用 `auditctl -l` 命令列出所有活动规则和监视。例如，列表 25.6 显示了列表 25.2和25.4中规则和监视的 `auditctl -l` 输出。

### 列表 25.6 审计规则与监视
