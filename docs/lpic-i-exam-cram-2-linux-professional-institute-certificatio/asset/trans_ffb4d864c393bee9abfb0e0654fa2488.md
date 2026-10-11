

- `/etc/sendmail.cw`—此文件应包含 sendmail 服务器应接收并保留邮件的域名列表，而不是转发邮件。

## sendmail.cf 文件

> “sendmail.cf 文件中的文本行，有人形容其类似调制解调器噪声；也有人形容其类似漫画《Blondie》中 Dithers 先生的脏话连篇”—Bryan Costales

`sendmail.cf` 和 `sendmail.mc` 这两个文件都非常复杂，不适合在此详细展开，但简要提及它们以及 sendmail 如何读取和使用它们会很有帮助。

首先，你需要编辑 `/etc/mail/sendmail.mc` 文件，并插入你的邮件环境所需的配置参数和规则。接下来，你需要使用 m4 宏处理器（例如）编译 `.mc` 文件：

```bash
m4 sendmail.mc > /etc/sendmail.cf
```

这将生成经过编译或处理的 `sendmail.cf` 文件。

每次启动 sendmail 时，它都会重新读取 `/etc/sendmail.cf` 文件。不建议直接编辑 `sendmail.cf`。

> 如果你确实需要禁用某个主机的 SMTP 中继，你可以编辑 `/etc/mail/sendmail.mc` 或 `/etc/sendmail.cf`，但必须重启 sendmail 才能使更改生效。

智能主机（Smart host）是 sendmail 配置中的一个特定条目，在关于考试的讨论中已多次出现。

智能主机通常用作将邮件送达难以到达的主机（例如位于企业防火墙背后的主机）的焦点。在当今的环境中，防火墙或安全主机更可能作为一个域中所有主机的控制点。

从广域网 Internet 无法访问的主机在发送邮件包时可能特别困难，因此智能主机要么位于防火墙本身，要么属于非军事区（DMZ）的一部分——即内部防火墙与通往 Internet 的网关之间的准安全区域。

## 别名设置与邮件转发

当你为一个组织，特别是为一个提供电子邮件服务的 Web 站点进行管理时，某些别名或昵称应被路由到另一个地址。

例如，如果你运行一个电子商务网站或使用 Web 进行产品支持，你可能会为 support（支持）、sales（销售）、comments（评论）和 information（信息）设置账户。必须有人经常检查这些账户，否则邮件会堆积，客户会不满意。

一个更优雅的解决方案是为这些名称在 `/etc/aliases` 文件中定义别名。在别名字段中，你可以配置哪些实际用户将接收到发送到这些别名的任何邮件。

### 定义别名

要配置别名，你需要编辑 `/etc/aliases` 文件，并添加符合以下格式的别名：

`alias_name: name1, name2, name3`

例如，要定义别名 `support`，并让发送到 `support@example.com` 的邮件发送给 `peter`、`paul` 和 `maria`，你需要在 `/etc/aliases` 文件中添加一行，如下所示：

`support: peter, paul, maria`

要更新 sendmail 以反映别名文件的新内容，你只需运行以下命令之一：

`newaliases`

或者

`sendmail -bi`

> 你不需要重启 sendmail 就能让它重新读取 `/etc/aliases` 文件。如果你更改了其他 sendmail 配置文件，则需要重启它，但别名除外。

### 为用户转发电子邮件

有时，用户无法从她常用的系统接收电子邮件，而让用户脱离循环或让她的邮件收件箱膨胀到超过配额的程度并不是明智之举。

要将原本由用户在其系统上读取的任何邮件发送到另一个电子邮件地址（例如用户从家中可访问的外部地址），你或用户可以创建一个名为 `.forward` 的文件在她的家目录中。

`.forward` 文件极其简单，通常由包含用户邮件应发送到的电子邮件地址的单行组成。要创建一个将 `snuffy` 账户的邮件发送到其家庭电子邮件的 `.forward` 文件，你可以使用以下命令：

```bash
echo snuffy@homemail.net > /home/snuffy/.forward
```

这会在 `/home/snuffy` 中创建一个名为 `.forward` 的文件，并使发送到 `snuffy` 的邮件被转发到该电子邮件地址。

> 请记住，只有 **root** 或具有相应权限的用户才能更改 `/etc/aliases` 文件，但每个用户默认都有创建 `.forward` 文件的能力，这可能导致邮件被不当转发。

## 与 sendmail 相关的实用工具

值得提及的是，`sendmail` 像其他任何服务一样受到控制，可以通过 Red Hat 的 `service` 命令或直接通过守护进程本身进行控制。

例如，要在 Debian 系统上使用守护进程的完整路径重启 `sendmail`，你会使用此命令：

```bash
/etc/init.d/sendmail restart
```

邮件被排队等待投递的两个位置是：

- `/var/spool/mqueue`—未送达的远程邮件存储在此目录中，等待远程主机可以接收数据。
- `/var/spool/mail`—未送达的本地用户邮件存储在此目录中。邮件包含在单个以用户账户命名的文本文件中。

> 请记住，`/var/spool/mail` 位置是一个目录，用户的邮件存储在该目录内的文件中。

要查看未发送或排队的邮件，你会使用 `mailq` 实用工具，如下所示：

```bash
mailq
```

这将产生如下输出：

```text
/var/spool/mqueue is empty
```

![](img/49f4f38f3aec011238fa50f89e643db3_498_0.png)

## Apache

如前所述，本章涵盖或 LPI 目标中涵盖的服务不需要完全安装，只需在分布版安装后进行配置和适度维护。这同样适用于 Apache：考试将 Apache 视为已安装，只需进行配置。

### Apache 如何运行

Apache 不仅仅运行单个进程，而是运行一个主进程，然后运行处理来自客户端 Web 请求的其他子进程。

Apache 的结构使其不适合由 **inetd** 或 **xinetd** 按需运行。主进程和子进程所需的启动时间通常会导致客户端请求超时并带有错误消息。

在 Red Hat 机器上，Apache 作为 **httpd** 进程运行，主进程的所有者设置为 **root** 用户，子进程作为 **apache** 用户运行。

在 Debian 3.x 机器上，Apache 以主进程的所有者设置为 **root** 用户，子进程作为 **www-data** 用户运行的方式运行。

### 使用 apachectl

尽管 Apache 非常重要，你应该有一个前端控制器，**apachectl** 实用工具在这方面表现出色。

**apachectl** 的选项包括：

- **start**—启动 **httpd** 守护进程
- **stop**—停止 **httpd** 守护进程
- **restart**—重启 **httpd** 守护进程（也会导致 Apache 重新读取其配置文件）
- **fullstatus**—报告状态（需要 lynx 和 mod_status 模块存在并编译到 Apache 中）
- **graceful**—重启并让当前连接完成
- **configtest**—检查 `/etc/httpd/conf/httpd.conf` 文件中的语法

大多数系统管理员使用 `apachectl` 从 shell 立即影响 Apache 服务器，或者从脚本中触发作为正常维护一部分的动作。

> 当你想要关闭 Web 服务但不想断开当前连接的用户时，请使用 `apachectl graceful` 命令。它旨在允许当前连接完成，同时禁止新连接。这比冷停止对用户来说更可接受得多。

### Apache 配置文件

在过去，Apache 使用两个配置文件，而当今使用主配置文件：

- `access.conf`—用于控制对目录的访问以及其他访问相关的配置
- `srm.conf`—用于设置服务器指令或参数

某些 Apache 实例根据服务器的年代和将配置整合到单个配置文件中被认为造成的麻烦程度，使用其中任何一个或所有文件。

在较新版本中，Apache 的主配置文件是 `/etc/httpd.conf`。几年前，决定将聚集在 `/etc` 目录树根部的众多配置文件移至它们自己的命名目录中。这意味着在 Red Hat 机器上，`httpd.conf` 文件位于 `/etc/httpd/conf/httpd.conf`。

在 Debian 机器上，该文件现在通常位于 `/etc/apache/httpd.conf`。

> 如果你在考试中被要求选择哪些文件被视为 Apache 的配置文件，`access.conf`、`srm.conf` 和 `httpd.conf` 三个文件都是有效且可能的选择。如果你被要求选择所有适用的项，这三个都是正确的。如果你被要求选择一个答案，只有 `httpd.conf` 是有效的。

