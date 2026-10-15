
登录程序首先请求用户名，然后要求 PAM 运行此栈以验证用户。请参阅第 105 页的表 17-19 和第 106 页的表 17-20。

（用户正在登录。）因此，当在不久的将来安排了关机时，系统管理员可以防止用户登录机器，以免他们在登录几分钟后就遇到关机。这在多用户环境中最为有用。

账户模块（`account module`）的工作原理类似于认证模块（`auth module`）类型，但在用户通过身份验证后进行调用；它是用户访问系统的额外安全检查或要求。例如，账户模块可以强制要求用户只能在工作时间内登录。

会话模块（`session module`）负责会话的建立和销毁（例如挂载和卸载用户的家目录）。Red Hat 系统上一个常见的会话模块是 `pam_console` 模块，它会为从物理控制台登录的用户设置系统，而不为从远程登录的用户设置。本地用户可以访问软驱驱动器、CD-ROM 驱动器、声卡，以及系统管理员定义的其他设备。

密码模块（`password module`）类型有点特殊：栈中的所有模块都会被调用一次，并被要求获取所需的所有信息以将密码存储到持久内存（如磁盘）中，但实际上并不执行存储操作。如果模块确定自己无法或不应该存储密码，则会报告失败。所有模块会被再次调用，以存储它们在第一次通过时获取的密码。密码模块负责更新认证信息（即更改用户的密码）。

任何一个模块都可以充当多个模块类型；许多模块可以充当所有四种模块类型。例如，`pam_pwdb` 模块在登录模块（第1045页）中被调用四次，作为所有四种模块类型工作。

## 控制标志字段中方括号 `([])` 的使用注意事项

你可以以更复杂的方式设置控制标志。当你在 PAM 配置文件的控制标志位置看到方括号 `([])` 时，说明正在使用较新的、复杂的方法。每个由逗号分隔的参数都是一个“值-动作”对。当函数的返回值与“值”（`value`）匹配时，就会执行相应的“动作”（`action`）。更多信息请参阅《系统管理员指南》(`/usr/share/doc/pam-*/pam.txt`)。

## 修改 PAM 配置

某些 UNIX 系统要求用户必须是 `wheel` 组的成员才能使用 `su` 命令。虽然 Red Hat 默认没有这样配置，但 PAM 允许你通过编辑 `/etc/pam.d/su` 文件来更改默认设置：

```
# $ cat /etc/pam.d/su
```

```
%PAM-1.0

auth sufficient /lib/security/pam_rootok.so

# 取消下面行的注释以隐式信任 "wheel" 组中的用户。

#auth sufficient /lib/security/pam_wheel.so use_uid

# 取消下面行的注释以要求用户在 "wheel" 组中。

#auth required /lib/security/pam_wheel.so use_id

auth required /lib/security/pam_stack.so service=system-auth

account required /lib/security/pam_stack.so service=system-auth

password required /lib/security/pam_stack.so service=system-auth

session required /lib/security/pam_stack.so service=system-auth

session optional /lib/security/pam_xauth.so
```

`su` 模块的第三行到第六行包含了注释，这些注释包含了允许 `wheel` 组成员在无需提供密码的情况下运行 `su`（`sufficient`）以及仅允许 `wheel` 组中的用户使用 `su`（`required`）的必要行。当你希望你的系统遵循这些规则之一时，请取消其中一行的注释。

## 不要创建 `/etc/pam.conf`

你可能在其他系统中遇到过 PAM，那里所有的配置都安排在一个文件中（`/etc/pam.conf`）中。该文件在 Red Hat 上并不存在。相反，`/etc/pam.d/` 目录包含了独立的配置文件，每个使用 PAM 的应用程序都有一个。这使得安装和卸载使用 PAM 的应用程序变得简单，而无需每次都修改 `/etc/pam.conf` 文件。如果你在不支持该文件的系统上创建了 `/etc/pam.conf` 文件，你的 PAM 配置可能会变得混乱。不要使用来自不同系统的 PAM 文档。此外，某些支持 PAM 的系统并不提供所需的控制标志。

## 管理工具

本节简要描述了许多可以帮助你执行系统管理任务的工具中的几个。你将从 Red Hat 文档（包括 Red Hat 文档光盘）、Red Hat 网站、其他互联网资源（包括新闻组）以及 GNU/Linux 用户那里学习其他工具。阅读本节所描述工具的 `man/info` 页面以了解更多关于使用方法的信息。某些工具是作为 K 或 GN 菜单的一部分包含的，某些工具对系统管理员以外的用户也有用。

### `kudzu`：添加或删除设备

`kudzu` 工具可以发现新的和更改的硬件并对其进行配置。该工具通过探测内部和外部总线上的所有设备，并将结果与 `/etc/sysconfig/hwconf` 数据库进行比较来实现。在默认配置下，`/etc/rc.d/init.d/kudzu` 脚本在机器进入级别 3 和 5 时运行时调用 `kudzu`。如果它发现了新的或更改的硬件，`kudzu` 将给你机会配置它，或取消配置你已移除的任何硬件。

> 不要探测正在使用的串口设备

由于探测活动中的串口设备可能会干扰其使用，在运行 `kudzu` 之前，请确保所有串口设备未被使用。

### `sendmail`：发送和接收邮件

SMTP（简单邮件传输协议）是互联网邮件协议。邮件程序分为三类：(1) MUAs（邮件用户代理；用户界面，图形界面或其他）；(2) MTAs（邮件传输代理，或传输代理），负责投递邮件；(3) MDAs（邮件投递代理），负责将邮件投递给用户。常用的 MTA 是 `sendmail`、`qmail`、`exim` 和 `postfix`。常用的 MUAs 有 `pine`、`mutt`、`elm` 和 `mailx`。常用的 MDAs 有 `procmail`、`fastmail` 和 `maildir`。

# 第 17 章 红帽 Linux 系统管理

电子邮件（`mail`）将发送到一个地方。决定你的邮件是作为客户端/服务器的客户端还是作为服务器本身，决定了你如何进行后续操作。

## `sendmail`: 邮件客户端

在客户端机器上设置 `sendmail` 比在服务器上要容易。默认情况下，`sendmail` 配置文件已为客户端设置好，仅需进行极小的修改。

客户端机器需要知道邮件服务器或邮件主机的名称。如果你正在运行 DNS，请在你的 DNS 域中添加一个名为 `mailhost` 的机器。如果你正在运行 NIS 或 NIS+，可以在你的名称服务中为 `mailhost` 添加条目。执行每项任务的方法取决于站点。如果上述两种都不适用于你，请在 `/etc/hosts` 中添加 `mailhost` 的条目。不要添加单独的条目；只需在引用邮件服务器的行末尾第三列（或最后一列）添加 `mailhost` 单词即可。`/etc/hosts` 中的下一行标识了机器 `achilles` 为递送和中继邮件的服务器（即 `mailhost`）：

```
192.168.0.5    achilles mailhost
```

`mailhost` 条目向 `sendmail` 表明这是邮件服务器，且它知道如何联系主机；特殊主机、中继站和域；知道如何向这些主机递送和队列邮件。本地客户端将所有它不知道如何递送的邮件发送给 `mailall`。

```
45 * * * /usr/sbin/sendmail -q
```

## `sendmail`: 邮件服务器

配置 `sendmail` 服务器需要比配置客户端更多的工作量。某些配置文件非常复杂，并使用 `m4` 宏语言编写。讨论所有的规则、宏、变量及其作用足以写满一整本书。本节提供了提供了将 `sendmail` 配置为向 Internet 上的远程主机发送邮件以及从这些主机接收邮件所需的最少信息。

要开始，，通过定义默认配置文件:`/etc/mail/sendmail.mc` 将你的本地机器配置为主邮件服务器，该文件由 `m4` 处理以生成 `/etc/mail/sendmail.cf`。首先，保存这两个文件的备份。`-p` 标志使 `cp` 保留权限以及访问和修改时间，这样你就能拥有准确的记录：

```
# cp -p /etc/mail/sendmail.cf /etc/mail/sendmail.cf
# cp -p /etc/mail/sendmail.mc /etc/mail/sendmail.mc
```

默认情况下，`sendmail` 只在机器的本地回环地址上监听，因此 `sendmail` 不接受网络 SMTP 请求。要让 `sendmail` 接受指向你本地域的 SMTP 请求，请在 `sendmail.mc` 文件中注释掉以下行：
