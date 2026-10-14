
```
lrwx-xr-x 1 root root    17 May 16:35 K00login -> ../init/dlinog
lrwx-xr-x 1 root root    10 May 16:05 K01.ms_srv -> ../init/ms_srv
lrwx-xr-x 1 root root    10 May 16:01 K01.lascup -> ../init/autoscp
lrwx-xr-x 1 root root    20 May 16:03 K02.asoundlink -> ../
lrwx-xr-x 1 root root    10 May 16:02 K03.asounduna -> ../init/asounduna
lrwx-xr-x 1 root root    10 May 16:02 K03.asoundlink -> ../init/asoundlink
lrwx-xr-x 1 root root    13 May 16:39 K05idpid -> ../init/idpid
lrwx-xr-x 1 root root    11 May 16:07 K06.tlog -> ../init/tlog
lrwx-xr-x 1 root root    14 May 16:33 K07.audit -> ../init/audit
lrwx-xr-x 1 root root    11 May 16:39 K08kbddmp -> ../init/kbddmp
lrwx-xr-x 1 root root    15 May 16:37 K14.snmpd -> ../init/snmpd
lrwx-xr-x 1 root system 10 May 16:16 K16console -> ../
lrwx-xr-x 1 root root    16 May 16:31 K16login -> ../init/alignog
lrwx-xr-x 1 root root    15 May 16:27 K19.dterm -> ../init/dtermp
lrwx-xr-x 1 root root    15 May 16:37 K21timed -> ../init/timed
lrwx-xr-x 1 root root    14 May 16:35 K23.cron -> ../init/cron
lrwx-xr-x 1 root root    08 May 16:38 K26kernel -> ../init/kernel
lrwx-xr-x 1 root root    13 May 16:30 K30dfs -> ../init/dfs
lrwx-xr-x 1 root root    16 May 16:35 K31presto -> ../init/presto
lrwx-xr-x 1 root root    18 May 16:37 K35fsmsount -> ../
lrwx-xr-x 1 root root    13 May 16:37 K38kmis -> ../init/nis
lrwx-xr-x 1 root root    11 May 16:08 K39camed -> ../init/camed
lrwx-xr-x 1 root root    15 May 16:37 K42rwho -> ../init/rwho
lrwx-xr-x 1 root root    15 May 16:37 K43route -> ../init/route
lrwx-xr-x 1 root root    17 May 16:37 K44gateway -> ../
lrwx-xr-x 1 root root    16 May 16:35 K45syslog -> ../init/syslog
```

通用系统命令以字母 `S` 开头，停止命令以字母 `K` 开头。以 `K` 开头的命令仅在系统运行级别从高级别更改到低级别时运行。以 `S` 开头的命令在所有情况下都会运行。`/sbin/rc2.d` 目录中命令的编号非常重要，因为数字是排序的，命令会按升序执行。

更多信息请参见 `rc2(8)`。

### 3.1.2.4 rc3.d 目录和 rc3 运行命令脚本

`/sbin/rc3` 脚本包含了用于将系统初始化为联网多用户状态（运行级别 3）的运行命令。在此之前，`initab` 文件包含了 `init` 程序在系统启动或将其状态更改为运行级别 3 时运行并执行的操作。例如：

```
s3:3wait:/sbin/rc3 < /dev/console > /dev/console 2&1
```

`rc3` 脚本是指定的命令。除了脚本本身列出的命令外，`rc3.d` 命令还链接到 `init.d` 目录中的文件。`rc3` 脚本定义了命令执行的条件；某些命令在系统启动时运行，其他命令在系统运行时运行。按照惯例，`/sbin/rc3.d` 目录下的文件以字母 `S` 开头，后跟一个 2 位数字和名称。例如，`/sbin/rc3.d` 目录内容的列表可能如下：

```
lrwx-xr-x 1 root root    15 May 16:37 S00if -> ../init/d
lrwx-xr-x 1 root root    17 May 16:37 S01net -> ../init/net
lrwx-xr-x 1 root root    14 May 16:37 S02inet -> ../init/inet
lrwx-xr-x 1 root root    18 May 16:37 S03spget -> ../init/spget
lrwx-xr-x 1 root root    14 May 16:37 S04ucbd -> ../init/ucbd
lrwx-xr-x 1 root root    15 May 16:37 S05start -> ../init/start
lrwx-xr-x 1 root root    16 May 16:37 S06skylog -> ../init/skylog
lrwx-xr-x 1 root root    15 May 16:37 S07binlog -> ../init/binlog
lrwx-xr-x 1 root root    16 May 16:37 S11gateway -> ../init/gateway
lrwx-xr-x 1 root root    17 May 16:37 S12route -> ../init/route
lrwx-xr-x 1 root root    14 May 16:37 S13winet -> ../init/winet
lrwx-xr-x 1 root root    18 May 16:37 S14time -> ../init/time
lrwx-xr-x 1 root root    16 May 16:37 S16snount -> ../init/snount
lrwx-xr-x 1 root root    17 May 16:37 S17sysv -> ../init/sysv
lrwx-xr-x 1 root root    15 May 16:37 S19nfs -> ../init/nfs
lrwx-xr-x 1 root root    16 May 16:37 S20ffount -> ../init/ffount
lrwx-xr-x 1 root root    15 May 16:37 S21audit -> ../init/audit
lrwx-xr-x 1 root root    16 May 16:37 S22preserve -> ../init/preserve
lrwx-xr-x 1 root root    14 May 16:37 S23files -> ../init/files
lrwx-xr-x 1 root root    18 May 16:37 S33presto -> ../init/presto
lrwx-xr-x 1 root root    15 May 16:37 S35sendmail -> ../init/sendmail
lrwx-xr-x 1 root root    16 May 16:37 S40klog -> ../init/klog
lrwx-xr-x 1 root root    15 May 16:37 S44timed -> ../init/timed
lrwx-xr-x 1 root root    16 May 16:37 S49insight -> ../init/insight
lrwx-xr-x 1 root root    15 May 16:37 S55venmon -> ../init/venmon
```

通用系统命令以字母 `S` 开头，停止命令以字母 `K` 开头。（注：此处原文似乎存在部分内容重复或截断错误，已根据上下文逻辑进行翻译）。

## 3.1.3 使用 crontabs 目录
