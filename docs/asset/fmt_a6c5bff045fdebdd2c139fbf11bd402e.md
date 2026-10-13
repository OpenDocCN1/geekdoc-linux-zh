
`aset` 命令的选项描述见表 8.15。

# 第 8 章 系统安全

## 表 8.15

### `aset` 命令选项

| 选项 | 说明 |
| :--- | :--- |
| `<level>` | 指定安全级别。有效值为低 (`low`)、中 (`medium`) 和高 (`high`)。 |
| 低安全 | 此级别确保系统文件的属性被设置为标准发布值。`ASET` 执行若干检查并报告潜在的安全漏洞。在此级别下，`ASET` 不采取任何行动，且不影响系统服务。 |
| 中等安全 | 此级别为大多数环境提供了足够的安全控制。`ASET` 修改某些系统文件和参数的设置，限制系统访问以减少安全攻击的风险。`ASET` 会报告安全漏洞以及它为限制访问所做的任何修改。在此级别下，`ASET` 不影响系统服务。 |
| 高安全 | 此级别使系统处于高度安全状态。`ASET` 调整许多系统文件和参数设置以最大限度地减少访问权限。大多数系统应用程序和命令继续正常运行，但在该级别下，安全考量优先于其他系统行为。 |

`<pathname>` 指定 `ASET` 的工作目录。默认为 `/usr/aset`。

以下示例使用默认目录 `/usr/aset` 在低安全级别下运行 `ASET`：

```
# /usr/aset/aset -l low

======= ASET Execution Log ========

ASET running at security level low

Machine = host3285; Current time = 0530_14:03

aset: Using /usr/aset as working directory

Executing task list ...

  env

  sysconf

  usrgrp

  tune

  cklist

  eprom

All tasks executed. Some background tasks may still be running. Run /usr/aset/util/taskstat [aset_dir] to check their status: where aset_dir 是 ASET 的运行目录，当前为=/usr/aset。
```

当任务完成后，可以在以下位置找到报告：
`# /usr/aset/reports/latest/*.rpt`
你可以通过以下命令查看：
`# more /usr/aset/reports/latest/*.rpt`

## 常识安全技术

系统管理员可以采取最好的系统安全措施，但如果没有用户的配合，系统安全将受到破坏。系统管理员必须教授有关系统安全的常识规则，例如：

- 使用适当的密码。无数站点使用 `"admin"` 或 `"supervisor"` 作为 `root` 账户的密码。
- 不要将你的密码给任何人，无论他们自称是谁。最顶级的系统破解者之一就是通过伪装成系统支持人员，向用户索要密码，从而获得系统的控制权。
- 如果你离开系统，请注销或锁定屏幕。想象一下，如果有人走到你的工作站前向你公司总裁发送一封尖酸的邮件——还附上了你的名字！后果会怎样。
- 未经系统管理员批准，不要将调制调器连接到系统。

## 本章总结

本章讨论了系统安全的基本概念。
在考虑安全时，首先要将硬件放置在安全的地方。记住：任何能够物理接触计算机的人都可以访问操作系统和数据，无论你对其他任何部分做了多么安全防护。

通过控制系统上的用户登录来维护你的数据安全。
确保用户拥有安全的密码，并且不要公开他们的登录名和密码。在合适的地方实施过期策略和受限制的 shell (`restricted shells`)。

设置文件和目录权限，确保用户仅能访问其授权查看的数据。利用 `umask` 值，并在必要时使用 `ACL`。使用本章描述的 Solaris 工具监控所有用户活动。最后，除非绝对必要，否则不要设置 `setuid`。

如果你的系统在网络上，请实施本章中描述的安全措施。关闭未使用的服务。使用“先拒绝，后允许”的原则。尽可能关闭服务和服务应用程序，并选择性地开启必需。利用可信系统。此外，保持操作系统补丁更新。当发现新威胁时，会通过安全补丁快速修复。第 4 章“软件包管理”描述了获取和加载系统补丁的过程。

最后，限制 `root` 访问。

### 运用你的知识

+ 6. 当提示输入用户名时，尝试以 `root` 身份登录。如果 `/etc/ftpusers` 文件没有从其默认设置进行过修改，你将收到“Login Incorrect”（登录错误）的消息，并且无法登录。
+ 7. 从 `/etc/ftpusers` 文件中删除 `root`。现在 `FTP` 会话可以正常工作了吗？
+ 8. 通过注释掉 `/etc/inetd.conf` 文件中的某行，来禁用所有 `FTP` 连接：

```
#ftp stream tcp6 nowait \
/usr/sbin/in.ftpd  in.ftpd
```
