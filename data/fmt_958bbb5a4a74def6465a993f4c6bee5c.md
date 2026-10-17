
```
castle kill -9 458
castle kill -KILL 459
```

# 内置 Shell kill 命令

Bourne shell、Korn shell 和 C shell 都有内置的 `kill` 版本，它们为通过作业（job）标识的进程提供 `kill` 命令的功能。

`csh` `kill` 内置命令默认向指定的进程 ID、作业索引或当前作业发送 `TERM`（终止）信号或指定的信号。可以通过编号或名称指定信号。没有默认值。如果 `kill` 不向当前作业或进程发送信号，而是发送了 `CONT`（继续）或 `HUP`（挂起），则该作业将再次运行。

`ksh` `kill` 的语法下所示。

Korn shell 发送 `TERM`（终止）信号或指定的作业或进程。可以通过编号或名称（如 `signal(5)` 中给出的名称，但去掉了前缀 `SIG`）指定信号。如果发送的是 `TERM`（终止）或 `HUP`（挂起）信号，且作业或进程处于停止状态，则向其发送 `CONT`（继续）信号。

`job-id` 参数是指非活动作业成员进程的进程 ID。

# kill

## 选项

`-l`

（字母 L。）写出 `jsh`、`ksh` 和 `csh` 实现支持的所有 `signal` 值。对于 `/usr/bin/kill`，如果你没有指定 `exit-status` 操作数，则写出所有 `signal` 值。如果你指定了 `exit-status` 操作数，且其值为特殊参数 `?` 并且对应于一个被信号终止的进程的等待，则写出与终止进程的信号对应的信号。如果你给出一个 `exit-status` 操作数且它是某个 `signal` 的无符号进制值，则写出该信号对应的信号。否则，结果不确定。

`-s signal`

使用信号编号或 `signal(5)` 手册页中定义的符号名称，向指定的进程或作业 ID 发送指定的信号。`signal` 的值不区分大小写，且不带 `SIG` 前缀。此外。

## 操作数

- `pid`

一个非活动作业成员的进程的进程 ID。

- `exit-status`

一个表示进程退出状态的整数。如果进程是由信号终止的，则退出状态为该信号编号。

## 使用

`kill` 命令的语法下所示：

```
kill [-l] [-s signal] [-n-status]...
```

`-l`

写出 `jsh`、`ksh` 和 `csh` 实现支持的所有 `signal` 值。对于 `/usr/bin/kill`，如果你没有指定 `exit-status` 操作数，则写出所有 `signal` 值。如果你指定了 `exit-status` 操作数，且其值为特殊参数 `?` 并且对应于一个被信号终止的进程的等待，则写出与终止进程的信号对应的信号。如果你给出一个 `exit-status` 操作数且它是某个 `signal` 的无符号进制值，则写出该信号对应的信号。否则，结果不确定。

`-s signal`

使用信号编号或 `signal(5)` 手册页中定义的符号名称，向指定的进程或作业 ID 发送指定的信号。`signal` 的值不区分大小写，且不带 `SIG` 前缀。

- `pid`

一个非活动作业成员进程的进程 ID。

- `exit-status`

一个表示进程退出状态的整数。如果进程是由信号终止的，则退出状态为该信号编号。

## 描述

`kill` 命令向进程或作业发送信号。你可以通过信号编号或 `signal(5)` 手册页中列出的逻辑信号名称（去掉 `SIG` 部分）来指定信号。

当你不指定信号时，`kill` 命令默认发送信号 15 (`SIGTERM`)。信号 15 在可行的情况下会终止进程，是杀死进程的首选方法。有时即使你使用 `kill` 命令，进程仍然不会终止。常见的有三种情况：

- 进程正在等待设备（如磁带驱动器）完成操作后再结束。
- 进程正在等待由于 NFS 问题导致不可用的资源。对于此类进程，请使用信号 3 (`SIGQUIT`)。
- 进程是一个僵尸进程（zombie），如 `ps` 报告中的 `defunct` 消息所示。僵尸进程是指已释放所有资源但尚未收到父进程确认的进程，通常收到确认后其条目就会从进程表中移除。当系统下次重启时，僵尸进程会被清除。僵尸进程不会影响系统性能，你不需要删除它们。

当进程无法通过信号 15 终止时，使用信号 9 (`SIGKILL`) 强制进程终止。

## 输出

`kill` 命令在成功时不产生任何输出，除非使用了 `-l` 选项，此时它会列出所有支持的信号。

## 示例

下面的示例演示了如何通过 PID 杀死进程：

```
castle kill 456
```

下面的示例演示了如何通过信号名称杀死进程：

```
castle kill -TERM 456
```

# kinit

## 563

在指定的有效期之后，你必须再次运行 `kinit` 来刷新票据。`kinit` 会销毁缓存中的任何现有内容。在结束登录会话之前，可以使用 `kdestroy(1)` 命令销毁任何活跃的票据。

## 配置文件

你必须通过对 `/etc/krb5/krb5.conf` 文件进行适当修改，在你计划计划运行 `kinit` 的 Kerberos 客户端的系统上进行配置。默认的 `krb5.conf` 文件所示。

```
#
#pragma ident "(@)krb5.conf 1.2 99/07/20 SMI"
# Copyright (c) 1999, by Sun Microsystems, Inc.
# All rights reserved.
#
#krb5.conf template
# 为了完成此配置文件的
# 你将需要将 __name>__ 占位符替换
# 为适用于你网络的适当值。
#
[libdefaults]
  default_realm = __default_realm__

[realms]
  default_realm = (
    kdc = master_kdc_
    _slave_kdc_
    admin_server = master_kdc_
  )

[domain_realm]
  domain_mapping_

[logging]
  default = FILE:/var/krb5/kdc.log
  kdc = FILE:/var/krb5/kdc.log
krotate = {
# 多久滚动一次 kdc.log。日志滚动频率会比
# 该周期更频繁，如果 KDC 不被频繁使用
# 则频率更低。

  period = 1d

# 保留多少版本的 kdc.log (kdc.log.0, kdc.log.1, ...)

  versions = 10

[appdefaults]
  kinit = {
    renewable = true
```

## 564

# kinit

`forwardable= true`

```
)
gkadmin = {
  help_url = http://docs.sun.com:80/ab2/coll.384.1/SEAM/@AB2PageView/1195
}
```

以下示例显示了为 `gmarler.domain` 配置的文件。

- * Kerberos 5 客户端的配置文件
- 该客户端位于 `gmarler.com` DNS 域，且 Kerberos 5 域
- 以 DNS 域命名
- 因此，客户端的默认 Kerberos 域是 `GMARLER.COM`

[libdefaults/]

```
default_realm = GMARLER.COM
```

- * 对于 `GMARLER.COM` 域，我们有一个主和次要密钥
- 分发中心 (KDC): `kdc.gmarler.com` 和 `kdc2.gmarler.com`
- `kdc.gmarler.com` 同时兼任 Kerberos 管理服务器

[realms]

```
GMARLER.COM = {
  kdc = kdc.gmarler.com
  kdc = kdc2.gmarler.com
  admin_server = kdc.gmarler.com
}
```

- * 此节将 `.gmarler.com` DNS 域中的任何主机映射到
- `GMARLER.COM` Kerberos 域

[domain_realm]

`.gmarler.com` = `GMARLER.COM`

- * 此节为感知 Kerberos 的应用程序定义了默认值：请参阅有关 Kerberos
- 的 Sun 在蓝图：http://www.sun.com/blueprints/online.html

[appdefaults]

```
gkadmin = {
  help_url = http://localhost:8888/ab2/coll.384.2/SEAM
```

```
kinit = {
  renewable = true
  forwardable= true
  proxiable = false
}
```

```
rlogin = {
  renewable = true
  forwardable= true
  encrypt = true
}
```
