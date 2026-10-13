
## 单一互联网连接的 DNS 域和子域

注意，仅激活了 `nullclient` 功能。此功能告诉所有客户端将本地生成的所有电子邮件发送到 `mailhost.starlight.com`，而不进行任何标头重写。

使用以下命令创建客户端 sendmail 配置文件。

```
# m4 /usr/lib/mail/corp-client.mc > /usr/lib/mail/corp-client.cf
```

将 `corp-client.cf` 配置文件复制到每个企业客户端工作站的 `/etc/sendmail.cf` 上。

## DNS 配置

将如下条目放入 `starlight.com` DNS 服务器中，以确保从互联网发送的所有邮件都能正确到达 `starlight.com` 或 `eng.starlight.com` 域。

| starlight.com | IN MX | 10 | gw |
| eng.starlight.com | IN MX | 10 | gw |
| gw | IN A | 205.3.46 |

此示例假设网关的 IP 地址为 `205.3.46`。任何尝试向 `username@starlight.com` 或 `username@eng.starlight.com` 发送邮件的互联网站点都会进行 DNS 查询，并发现邮件交换器 `MX` 记录直接指向 `gw.starlight.com`，优先级为 `10`。

正如你看到的，所有入站邮件都通过网关。这种行为不影响出邮件，因为邮件是由中枢处理的。记住，两个域的邮件客户端直接发送到各自的中枢，因此它们不需要查看 DNS。

## 带有 UUCP 网关的 DNS 域

为网关添加处理 UUCP 地址的能力很容易。只需在相关网关的宏文件的末尾添加以下行。

```
MAILER(uucp)dnl
```

通过 `m4` 宏处理器运行宏配置文件，并将生成的 sendmail 配置文件复制到 `/etc/mail/sendmail.cf`。重启 `sendmail`；你的网关现在可以处理 UUCP 地址。

# 4

## 设置和管理邮件服务

本章描述了如何设置、测试、管理和排排除邮件服务。如果你不熟悉管理邮件服务，请阅读第 1 章“理解邮件服务”以了解术语和结构。阅读第 3 章“规划邮件服务”以了解若干邮件服务的配置。

## 设置邮件服务的准备工作

如果你的站点不提供公司外部电子邮件服务的连接，或者你的公司位于单一域中，你可以相对容易地设置邮件服务。设置多个域的复杂服务超出了本书的范围。第 2 章“自定义 sendmail 配置文件”包含了如何创建多域站点所需的更复杂配置的信息。

邮件需要两种类型的本地邮件配置以及第三种用于与域外网络通信的配置。这些配置

# 邮件服务的设置与管理

可以在同一系统上组合，也可以由单独的系统提供。表 19 描述了这些种配置。

## 表 19 邮件配置

| 配置 | 描述 |
| --- | --- |
| 邮件中枢 | 你至少需要一个邮件中枢。邮件中枢在 `/var/mail` 目录下存储信箱。 |
| 邮件客户端 | 邮件客户端是指在本地或邮件服务器上拥有信箱的用户。 |
| 网关 | 网关是不同通信网络之间的连接。中继主机管理与你的网域外部网络的通信。中继主机也可以充当网关。你必须向用于生成 `sendmail.cf` 文件的 `.mc` 文件添加规则以设置网关。有关创建 `.mc` 文件的信息，请参阅第 2 章“自定义 sendmail 配置文件”。 |

在开始设置邮件服务之前，请选择作为邮件中枢和网关的系统。你还应该列出所有将为之提供服务的邮件客户端，并指明它们邮箱的位置。当你准备好为用户创建邮件别名时，此列表将对你有帮助。有关这些系统所提供功能的更多信息，请参阅第 1 章“理解邮件服务”。为了方便起见，后续章节描述了哪些系统是作为邮件中枢和网关的良好选择。

## 设置邮件服务

为了简化设置说明，以下章节将告诉如何设置单独的邮件中枢、邮件客户端和网关主机。如果你的邮件服务配置中的某个系统承担了多个角色，只需按照每种类型的相应说明操作。例如，如果你的邮件中枢和网关是同一个系统，请按照将该系统设置为邮件中枢的说明操作，然后按照将该系统设置为邮件网关的说明操作。

注意：当信箱通过 NFS 挂载时，适用于设置邮件服务器和邮件客户端的后续程序。当信箱在本地 `/var/mail` 目录中维护时，你不需要遵循这些程序。

## 设置邮件中枢

邮件中枢负责路由来自客户端的所有邮件。邮件中枢的唯一资源要求是为客户端信箱留有足够的池空间 `spool space`。关于池大小的建议，请参阅第 1 章“理解邮件服务”。

要设置邮件中枢，你必须导出 `/var` 目录。在 Solaris 系统上，输入 `share` 并按回车键检查 `/var` 目录是否已导出。在以下示例中，`/var/mail` 目录未导出。

```
cinderella% share

cinderella%$
```

如果 `/var` 目录未导出，变为超级用户，然后输入 `share -F nfs -o rw /var/mail` 并按回车。你可以输入不带参数的 `share` 来验证该目录已导出。你也可以将该行添加到 `/etc/dfs/dfstab` 文件中，这样该文件系统在系统重启时会被加固。

```
cinderella% share

cinderella% su

Password:

# share -F nfs -o rw /var/mail

# share

      /var/mail      rw *

# vi /etc/dfs/dfstab

添加该行：

share -F nfs -o rw /var/mail
```

> 注意：`mail.local` 程序在第一次递送邮件时会自动在 `/var/mail` 目录下创建信箱。你不需要为你的邮件客户端创建单独的信箱。

邮件中枢解析复杂的电子邮件地址，并在你的网域内重新路由邮件。邮件中枢的良好人选是连接到外部世界或父网域的系统。

使用以下步骤设置邮件中枢。

- 1. 在邮件中枢系统上变为超级用户。
- 2. 输入 `/usr/lib/mail/sh/check-hostname` 并按回车。`check-hostname` 脚本验证 `sendmail` 是否能识别此台服务器的完全限定主机名 `fully qualified host name`。如果脚本未能成功识别完全限定主机名，你必须将完全限定主机名作为第一个别名添加到 `/etc/hosts` 文件的主主机条目中。以下示例显示了一个不是完全限定的主机名。

```
paperback% su

Password:

# /usr/lib/mail/sh/check-hostname

Hostname paperwork could not be fully qualified.

我们建议更改 /etc/hosts 条目：

172.16.8.22 paperwork loghost

为：

172.16.8.22 paperwork.some.domain loghost
```

- 1. 使用 `admintool` 编辑 `/etc/hosts` 文件，并在邮件中枢的 IP 地址和系统名之后添加 `mailhost` 和 `mailhost.domain` 字。域名必须与 `/usr/lib/sendmail -bt -d /null` 输出中的子域字符串完全一致。以下示例显示了系统 `paperwork` 的命令输出，它是 `emailard.com` 子域的一部分。

```
paperwork% /usr/lib/sendmail -bt -d /null

Version 8.9.3+Sun

Compiled with: IDMAP_REGEXP MATCHES MIMETO NAMED_BIND BIND NETINET NETUNIX WDB MISPLUS SCANF SMTP USERDB

===================================

SYSTEM (short domain) = paperwork

(canonical domain name) = emailard.com

(subdomain name) = emailard.com

(node name) = paperwork

===================================
```

- 以下示例显示了 `/etc/hosts` 文件中的条目，将 `paperwork` 指定为网域 `emailard.com` 的邮件中枢。

```
# cat /etc/hosts

# Internet host table

127.0.0.1 localhost

172.16.8.22 paperwork mailhost emailard.com loghost
```
