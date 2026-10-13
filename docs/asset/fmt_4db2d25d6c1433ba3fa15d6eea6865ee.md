
`item` 字段指示当前记录是 `SYSCALL` 类型记录中引用的总项目数中的哪一个。此数字从零开始；值为 0 表示它是第一个项目。

## name="/etc/ssh/sshd_config"

`name` 字段记录作为参数传递给系统调用的文件或目录的完整路径。在此情况下，它是 `/etc/ssh/sshd_config` 文件。

## inode=409248

`inode` 字段包含与此事件中记录的文件或目录关联的 inode 号。以下命令显示与 `409248` inode 号关联的文件或目录：

```bash
-]# find / -inum 409248 -print
/etc/ssh/sshd_config
```

## dev=fd:00

`dev` 字段指定包含此事件中记录的文件或目录的设备的小号和大号 ID。在此情况下，该值代表 `/dev/fd/0` 设备。

## mode=0100600

`mode` 字段记录文件或目录的权限，编码为数字表示，由 `stat` 命令在 `st_mode` 字段中返回。有关更多信息，请参阅 `stat(2)` 手册页。在此情况下，`0100600` 可以解释为 `-rw-------`，这意味着只有 root 用户具有对 `/etc/ssh/sshd_config` 文件的读写权限。

## ouid=0

`ouid` 字段记录对象所有者的用户 ID。

## ogid=0

`ogid` 字段记录对象所有者的组 ID。

## rdev=00:00

`rdev` 字段仅包含特殊文件的记录设备标识符。在此情况下，它未被使用，因为记录的文件是常规文件。

## obj=system_u:object_r:etc_t:s0

`obj` 字段记录在执行时标记记录的文件或目录所使用的 SELinux 上下文。

## objtype=NORMAL

`objtype` 字段记录在给定 syscall 上下文中每个路径记录的操作意图。

## cap_fp=none

`cap_fp` 字段记录与设置文件或目录对象的允许文件系统基于的能力相关的数据。

## cap_fi=none

`cap_fi` 字段记录与设置文件或目录对象的继承文件系统基于的能力相关的数据。

`cap_fe=0`

`cap_fe` 字段记录文件或目录对象基于文件系统的能力的有效位设置。

`cap_fver=0`

`cap_fver` 字段记录文件或目录对象基于文件系统的能力的版本。

## 第4条记录

`type=PROCTITLE`

`type` 字段包含记录的类型。在此示例中，`PROCTITLE` 值指定该记录给出了触发此审计事件的完整命令行，该事件由调用内核的系统调用触发。

```
proctitle=636174002F6574632F7373 82F737368645F636F6E6669677
```

`proctitle` 字段记录用于调用被分析进程的完整命令行。该字段以十六进制编码形式记录，以防止用户影响审计日志解析器。该文本解码为触发此审计事件的命令。在使用 `ausearch` 命令搜索审计记录时，使用 `-i` 或 `--interpret` 选项可自动将十六进制值转换为其人类可读的等价值。`636174002F6574632F737382F737368645F636F6E6669677` 值被解释为 `x86_64`。

上述分析的审计事件仅包含事件可能包含的所有字段的一个子集。有关所有事件字段及其解释的列表，请参见第 B.1 节“审计事件字段”。有关所有事件类型及其解释的列表，请参见第 B.2 节“审计记录类型”。

### 示例 6.6. 额外的 audit.log 事件

以下审计事件记录了 `auditd` 守护程序的成功启动。`ver` 字段显示了启动的审计守护程序的版本。

```
type=DAEMON_START msg=audit(1363713609.192:5426): auditd start, ver=2.2 format=raw kernel=2.6.32-358.2.1.el6.x86_64 audit=1000 pid=4979 subj=unconfined_u:system_r:auditd_t:s0 res=success
```

以下审计事件记录了 UID 为 1000 的用户尝试登录为 root 用户失败的情况。

```
type=USER_AUTH msg=audit(136475353.159:24270): user pid=3280 uid=1000 auid=1000 ses=1 subj=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023 msg='op=PAM:authentication acct="root" exe="/bin/su" hostname=? addr=? terminal=pts/0 res=failed'
```

## 6.7. 搜索审计日志文件

`ausearch` 实用程序允许您搜索审计日志文件中的特定事件。默认情况下，`ausearch` 搜索 `/var/log/audit/audit.log` 文件。您可以使用 `ausearch` 选项 `-if file_name` 命令指定其他文件。在一个 `ausearch` 命令中提供多个选项等价于在字段类型之间使用 AND 运算符，并在同一字段类型的多个实例之间使用 OR 运算符。

### 示例 6.7. 使用 ausearch 搜索审计日志文件

要搜索 `/var/log/audit/audit.log` 文件中的登录失败尝试，请使用以下命令：

```
~]# ausearch --message USER_LOGIN --success no --interpret
```

要搜索所有账户、组和角色更改，请使用以下命令：

```
~]# ausearch -m ADD_USER -m DEL_USER -m ADD_GROUP -m USER_CHAUTHTOK -m DEL_GROUP -m CHGRP_ID -m ROLE_ASSIGN -m ROLE_REMOVE -i
```

要搜索由特定用户执行的所有已记录操作，使用该用户的登录 ID（audit），请使用以下命令：

```
~]# ausearch -ua 1000 -i
```

要搜索从昨天至今的所有失败的系统调用，请使用以下命令：

```
~]# ausearch --start yesterday --end now -m SYSCALL -sv no -i
```

有关所有 `ausearch` 选项的完整列表，请参见 `ausearch(8)` 手册页。

## 6.8. 创建审计报告

`aureport` 实用程序允许您生成针对记录在审计日志文件中的事件的摘要和列式报告。默认情况下，会查询 `/var/log/audit/` 目录中的所有 `audit.log` 文件以创建报告。您可以使用 `aureport` 选项 `-if file_name` 命令指定运行报告所针对的其他文件。

### 示例 6.8. 使用 aureport 生成审计报告

要为过去三天（不包括当前示例日期）记录的已记录事件生成报告，请使用以下命令：

```
~]# aureport --start 04/08/2013 00:00:00 --end 04/11/2013 00:00:00
```

要为所有可执行文件事件生成报告，请使用以下命令：

```
~]# aureport -x
```

要为上述可执行文件事件报告生成摘要，请使用以下命令：

```
~]# aureport -x --summary
```

要为所有用户的失败事件生成摘要报告，请使用以下命令：

```
~]# aureport -u --failed --summary -i
```

要为每个系统用户的所有失败登录尝试生成摘要报告，请使用以下命令：

```
~]# aureport --login --summary -i
```

要从搜索用户 ID 1000 的所有文件访问事件的 `ausearch` 查询生成报告，请使用以下命令：

```
~]# ausearch --start today --loginuid 1000 --raw | aureport -f --summary
```

要为所有被查询的审计文件以及它们包含的事件时间范围生成报告，请使用以下命令：

```
~]# aureport -t
```

有关所有 `aureport` 选项的完整列表，请参见 `aureport(8)` 手册页。

## 6.9. 其他资源

有关 Audit 系统的更多信息，请参见以下来源。

### 在线资源

- Linux Audit 文档项目页面：https://github.com/linux-audit/audit-documentation/wiki。

### 已安装的文档

`audit` 包提供的文档可以在 `/usr/share/doc/audit/` 目录中找到。

### 手册页

- `audispd.conf(5)`

- `auditd.conf(5)`

- `ausearch-expression(5)`

- `audit.rules(7)`
