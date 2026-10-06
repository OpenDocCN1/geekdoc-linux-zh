
告诉 `sendmail` 在端口 `10025` 上监听来自 `amavisd` 的返回消息。它会以 `transmittingMTA` 的名称记录任何信息或错误消息，以便将其与 `receivingMTA` 区分开来。

还有更多可以调整的设置（例如性能限制），以让两个 `sendmail` 实例良好地协同工作。需要经过思考来决定具体将进行哪些检查、由哪个进程执行，以及执行顺序如何。

`amavisd-new` 分发包中的 `README.FILES/README.sendmail-dual` 文件是一个很好的参考。

# 20.11 安全与 sendmail

随着互联网的爆炸式增长，像 `sendmail` 这样的程序接受任意用户提供的输入并投递到本地用户、文件或 `shell`，这经常为黑客提供可乘之机。`sendmail` 与同 `DNS` 甚至 `IP`，正在尝试身份验证和加密作为某些基本安全问题的内置解决方案。

`sendmail` 同时支持 `SMTP` 身份验证和基于 `TLS`（传输层安全，以前称为 `SSL`，安全套接层）的加密。`TLS`

# 第 20 章 电子邮件

`TLS` 带来了证书文件和密钥文件的新配置选项。访问数据库匹配的新操作可能要求身份验证必须成功。

在本节中，我们将描述 `sendmail` 的权限模型、所有权和隐私保护。然后，我们将简要讨论 `TLS` 和 `SASL`（简单认证与安全层）以及它们在 `sendmail` 中的用法。

`sendmail` 在相信例如转发文件或别名文件（`aliases file`）的内容之前，会仔细检查文件权限。虽然这种安全性的加强通常很欢迎，但有时有必要放宽严格的策略。为此，`sendmail` 引入了 `DontBlameSendmail` 选项，此命名是为了向系统管理员提示他们所做的操作是不安全的。

此选项有许多可能的值——在 `root` 下为 `55`。默认值是安全的，也是最严格的。有关值的完整列表，请参见 `sendmail` 分发书籍中的 `doc/op/op.ps`。或者直接将该选项留为 `safe`。

## 所有权

用户账户在 `sendmail` 世界中非常重要：`DefaultUser`（默认用户）、`RunAsUser`（运行用户）和 `TrustedUser`（受信任用户）。

默认情况下，所有的 `sendmail` 邮件器都以 `DefaultUser` 身份运行，除非邮件器的标记另有规定。如果 `/etc/passwd` 文件存在 `mailname`、`sendmail` 或 `daemon`，则 `DefaultUser` 将是那个。否则，它默认为 `UID 1` 和 `GID 1`。我们建议使用 `mailnull` 账户和 `mailnull` 组。将其添加到 `/etc/passwd`，密码为 `*`，没有有效的 `shell`，没有主目录，且默认组为 `mailnull`。你还必须将 `mailnull` 条目添加到组文件中。`mailnull` 账户不应拥有任何文件。如果 `sendmail` 未在运行，邮件器必须设置 `setuid`。

如果设置了 `RunAsUser`，`sendmail` 会忽略 `DefaultUser` 的值并以 `RunAsUser` 身份运行一切。如果你正在运行带 `setgid` 的 `sendmail` (`to smtp`)，那么提交的 `sendmail` 将通过 `SMTP` 将消息传递给真实的 `sendmail`。真实的 `sendmail` 没有 `setuid` 位，但它从启动文件中以 `root` 身份运行。

`RunAsUser` 是 `sendmail` 在打开到 `25` 的套接字连接时的 `UID`。编号小于 `1024` 的端口只能由超级用户打开；`sendmail` 必须最初以 `root` 运行。然而，在执行此操作时，`sendmail` 可以切换到不同的 `UID`。这种切换可以在 `sendmail` 被欺骗执行坏事时降低损坏或访问的风险。不要在支持用户账户或其他服务的机器上使用 `RunAsUser` 功能；它仅用于防火墙或堡垒机。¹³

> 13. 堡垒机（Bastion hosts）是经过加固的主机，旨在位于 DMZ 或防火墙之外时承受攻击。

## 权限

默认情况下，`sendmail` 不切换身份并继续以 `root` 身份运行。如果你将 `RunAsUser` 改为 `root` 以外的内容，你也必须更改一切。`RunAsUser` 必须拥有邮件队列，能够读取所有 `maps` 和包含文件，能够运行程序等。花费几个小时找到所有文件和目录的所有权。

`sendmail` 支持 `SMTP` 身份验证和基于 `TLS`（传输层安全，以前称为 `SSL`，安全套接层）的加密。`TLS` 带来了证书文件和密钥文件的新配置选项。访问数据库匹配的新操作可能要求身份验证必须成功。

`sendmail` 在相信例如转发文件或别名文件的内容之前，会仔细检查文件权限。虽然这种安全性的加强通常很欢迎，但有时有必要放宽严格的策略。为此，`sendmail` 引入了 `DontBlameSendmail` 选项，此命名是为了向系统管理员提示他们所做的操作是不安全的。

此选项有许多可能的值——在 `root` 下为 `55`。默认值是安全的，也是最严格的。有关值的完整列表，请参见 `sendmail` 分发书籍中的 `doc/op/op.ps`。或者直接将该选项留为 `safe`。

### 文件和目录权限

| 路径 | 所有者 | 模式 | 包含的内容 |
|---|---|---|---|
| /var/spool | mailUser | 700 | Queue |
| Ubuntu | /usr/lib | /usr/lib |
| SUSE | /usr/lib/sendmail.d/bin | /usr/lib/sendmail.d/bin |
| Red Hat | /usr/sbin | | /adm |
| Solaris | /usr/lib | | / |
| HP-UX | /usr/sbin | | /adm* |
| AIX | /usr/sbin | | /adm* |

`sendmail` 的权限非常重要。使用表 20.13 帮助你找到友好供应商存放它们的地方。

## 更安全的邮件与程序

我们建议使用 `smrush` 代替 `/bin/sh` 作为你的程序，并使用 `mail.local` 代替 `/bin/mail` 作为你的本地程序。两者都包含在 `sendmail` 分发中。要将它们整合到配置中，在你的 `.mc` 文件中添加以下行：

```
FEATURE(smrush, 'path-to-smrush')
FEATURE(local, 'path-to-local')
```

如果你省略显式路径，假设命令位于 `/usr/libexec`。你可以使用 `sendmail` 的 `BINDIR` 选项将二进制文件的默认位置更改为你想要的任何位置。表 20.14 可能帮助你找到...

`smrush` 是一个受限 `shell`，默认只执行一个目录（`/usr/adm/sm.bin`）中的程序。`smrush` 忽略用户指定的路径，并尝试在其已知的目录下查找任何请求命令。`smrush` 还使用某些 `shell` 元字符块，例如 `<`。`sm.bin` 中允许符号链接，因此你不需要复制允许程序的副本。`vacation` 程序是 `sm.bin` 的良好候选者。不要放入 `procmail`；它是不安全的。

这里是一些示例 `shell` 命令及其可能的 `smrush` 解释：

```
vacation eric # 执行 /usr/adm/sm.bin/vacation eric
cat /etc/passwd # 被拒绝，sm.bin 中没有 cat
vacation eric /etc/passwd # 被拒绝，不允许使用 <
```

## 隐私选项

`sendmail` 的 `SafeEnvironment` 选项控制了当邮件通过别名或转发文件重定向到文件时，文件可以写入的位置。它会导致 `sendmail` 执行一个 `chroot` 系统调用，使得文件系统的根目录不再是 `/` 而是 `/safe/` 或你在 `SafeEnvironment` 选项中指定的任何路径。例如，一个将邮件定向到 `/etc/passwd` 文件的别名实际上会被写入到 `/safe/etc/passwd`。

`SafeEnvironment` 选项还通过允许向普通文件写入内容，来保护设备文件、目录和其他特殊文件。通过提高安全性，该选项减轻了用户操作失误的影响。某些站点将该选项设置为 `/home`，以允许访问主目录，同时将系统文件排除在访问范围之外。

邮件递器（Mailers）也可以在 `chroot` 环境中运行。

`sendmail` 拥有一些隐私选项，可以控制：

- 外部人员通过 `SMTP` 确定关于你站点的哪些信息
- 你对 `SMTP` 连接另一端主机有何要求
- 你的用户是否可以使用或运行邮件队列

表 20.15 列出了截至本文编写时隐私选项的可能值：当前信息请参阅发行版中的 `doc/op/op.ps` 文件。

### 表 20.15 PrivacyOption 变量的值

| 值 | 含义 |
| :--- | :--- |
| public | 不进行任何隐私/安全检查 |
| needmailhero | 需要 SMTP HELO（识别远程主机） |
| noexpn | 禁止 SMTP EXPN 命令 |
| novrfy | 禁止 SMTP VRFY 命令 |
| needexphnlo | 在没有 HELO 的情况下不扩展地址 (EXPN) |
| needvrfhely | 在没有 HELO 的情况下不验证地址 (VRFY) |
| noverb | 禁止对 EXPN 使用冗详细模式 (verbose) |
| restrictmailq | 仅允许队列目录组查看队列 |
| restricturn | 仅允许队列目录的所有者运行队列 |
| restrictexpand | 限制 -bv 和 -v 标志显示的信息 |
| noetrn | 禁止异步队列运行 |
| authwarnings | 当发出的邮件似乎被伪造时添加警告标头 |
| norecipe | 关闭成功返回回执的状态通知 |
| nobody | 在 DSN（递送状态通知）中不返回正文 |
| goaway | 禁止 SMTP 状态查询（EXPN, VRFY 等） |

> a. 详细模式（Verbose）。当给出 EXPN 命令时转发文件，并报告关于用户邮件去向的更多。在任何暴露在外部的机器上，请使用 `noverb`，或者更好的做法是使用 `noexpn`。
> b. 除非由 `root` 或信任用户（`TrustedUser`）执行。
> c. `ETRN` 是一个为拨号连接主机设计的 `SMTP` 命令。它请求仅针对该主机的消息运行队列。

# 第 20 章

# 电子邮箱

我们建议采取保守策略；在你的 `.mc` 文件中

```
define(confPRIVACY_OPTIONS, 'goaway', authwarnings, restrictmail,
      restrictqrun)
```

`sendmail` 隐私选项的默认值是 `authwarnings`；上述行将重置该值。注意双重引号；某些版本的 `m4` 需要双重引号来在隐私选项值列表中放置逗号。`Red Hat`、`Solaris` 和 `AIX` 默认设置为 `authwarnings`；`SUSE` 和 `Ubuntu` 默认设置为 `authwarnings, needmailhello, nofy, noexpn, and no`；`HP-UX` 默认设置为 `restrictqrun, goaway, 和 authwarnings`，这是最安全的——go, HP！

## 运行 chrooted sendmail（针对极度追求安全的用户）

如果你担心 `sendmail` 对你文件系统的访问，你可以在 `chroot` 狱中启动它。（有关 `chroot` 的更多信息，请参见第 22 章“安全”第 913 页）。在狱创建一个最小的文件系统，包含 `/dev/`、`/etc essentials`（`passwd, resolv.conf, sendmail.cf, 任何映射文件, mail/*`）、`sendmail` 需要的共享库、二进制文件、邮件队列以及任何日志文件。你可能需要反复调整列表以达到完美状态。使用 `chroot` 命令启动被禁的 `sendmail`。例如：

```
$ sudo chroot /jail /usr/sbin/sendmail -bd q30m
```
