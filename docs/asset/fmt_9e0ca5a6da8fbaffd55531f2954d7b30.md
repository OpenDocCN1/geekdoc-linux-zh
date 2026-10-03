
## 表 4-3

| 键 | 功能 |
| :--- | :--- |
| t | 邮件。。 |
| e | 编辑消息。 |
| d | 删除消息。 |
| u | 取消删除消息。 |
| R | 回复发送者。 |
| r | 回复所有接收者。 |
| m | 指定特定用户。 |
| q | 退出。 |
| x | 退出并保存更改。 |

以下是 `mail` 的常用选项：

| 选项 | 描述 |
| :--- | :--- |
| `-a` | 将指定文件附加消息。 |
| `-b` | 向列表发送密抄。列表应为逗号分隔的名称。 |
| `-c` | 向列表发送抄送。 |
| `-q` | 使用指定的内容开始消息。仅用于发送模式。 |
| `-s` | 在命令行上指定主题（只有 `-s` 后面的第一个参数作为主题；注意包含空格的主题）。 |
| `-R` | 在命令行上指定回复地址（只有 `-R` 后面的第一个参数作为地址）。 |
| `-F` | 打开 mbox 读取这些旧邮件消息。 |

## 练习 4-1

### 向 root 发邮件

在此练习中，你使用 `mail` 命令向 root 用户发送电子邮件。你还要切换到 root 并读取这封邮件。你可以在练习本中找到此练习。

（练习结束）

## 理解 Postfix 的架构和组件

Venema 使用一系列模块化功能单元实现了他的 Postfix 设计目标。与 Sendmail 不同，Postfix 不是一个巨大的单一程序块。相反，它由许多小程序组成，每个程序分配了一个特定的任务（例如，接收电子邮件）。

这种模块化使得系统更加透明。单个组件更容易管理，有利于 Postfix 的进一步开发。

下图摘自原始 Postfix 文档，显示了 Postfix 模块化的概要概述。

本阶段未涵盖的模块位于 `/usr/share/doc/packages/postfix/html/OVERVIEW.html`。

## 图 4-2

![](img/b7f4ef3c9bdffc8caed3395478c04bab_242_0.png)

单个 Postfix 进程在图中椭圆表示。深色方形代表查找表，浅色方形表示邮件队列或邮箱。

出于安全考虑，Postfix 与四个邮件队列协同工作。对于每个邮件队列，在 `/var/spool/postfix/` 下都有一个同名的目录。

队列的功能和 Postfix 文件的描述请参考：

- 入站邮件处理流程
- 出站邮件处理流程
- Postfix 程序包的组件

## 入站邮件处理流程

下图显示了邮件如何到达 Postfix 以及它是如何被处理的。

### 图 4-3

![](img/b7f4ef3c9bdffc8caed3395478c04bab_243_0.png)

以下描述了这些过程：

- 本地接收的邮件
- 通过网络接收的邮件

## 本地接收的邮件

Postfix 使用 `postdrop` 命令将本地发送的邮件放入 maildrop 队列中，然后由 `pickup` 守护进程进行取用。

`pickup` 守护进程根据规则检查内容、大小和其他因素；然后将邮件传递给 `cleanup` 守护进程。

`cleanup` 守护进程执行以下操作：

- 在邮件中插入缺失的头部行（`Resent.*`、`From.*`、`To.*`、`Message-ID`、`Date:`）（如果邮件是通过 telnet 写入的）
- 删除重复的收件地址
- 使用 `trivial-rewrite` 守护进程（`/usr/lib/postfix/trivial-rewrite`）将头部中的邮件地址转换为 `user@fully-qualified-domain` 格式
- 根据 `/etc/postfix/canonical` 和 `/etc/postfix/virtual` 查找表中的规则写入头部中的数据

之后，邮件被复制到入站队列（incoming queue），并通知队列管理器 `/usr/lib/postfix/qmgr` 该邮件已到达。

## 通过网络接收的邮件

通过互联网或局域网接收的邮件由守护进程 `smtpd` 接收，它在将邮件传递给 `cleanup` 守护进程之前会检查邮件的内容、大小和其他因素。

`cleanup` 守护进程执行以下操作：

- 替换邮件中缺失的头部行（`Resent.*`、`From.*`、`To.*`、`Message-ID.*`、`Date:`）
- 删除重复的收件地址
- 使用 `trivial-rewrite`（`/usr/lib/postfix/trivial-rewrite`）守护进程将头部中的邮件地址转换为 `user@fully-qualified-domain` 格式
- 根据 `/etc/postfix/canonical` 和 `/etc/postfix/virtual` 查找表中的规则写入头部中的数据

然后，邮件被复制到入站队列，并通知队列管理器 `/usr/lib/postfix/qmgr` 该邮件已到达。

## 出站邮件处理流程

下图显示了邮件在离开系统进行投递之前，是如何被 Postfix 处理的：

### 图 4-4

![](img/b7f4ef3c9bdffc8caed3395478c04bab_245_0.png)

以下主题描述了这个过程：

- 将邮件投递给本地用户
- 将邮件投递给远程系统的用户
- 处理无法投递的邮件

## 将邮件投递给本地用户

一旦活动队列（active queue）没有其他邮件，队列管理器就会从入站队列获取邮件并将其复制到活动队列。

`trivial-rewrite` 守护进程根据 `/etc/postfix/transport` 查找表检查程序，以判断收件人是在本地系统还是远程系统。

如果该守护进程决定邮件应该在本地投递，队列管理器将调用本地投递服务（`/usr/lib/postfix/local`）投递到收件人的邮箱，并考虑别名数据库（`/etc/aliases`）以及用户的任何转发文件（`~/.forward`）。

本地守护进程也可以配置为通过外部程序（如 Procmail）交付邮件。

## 将邮件投递给远程系统的用户

一旦活动队列为空，队列管理器就会从入站队列获取邮件并将其复制到活动队列。

`trivial-rewrite` 守护进程使用 `/etc/postfix/transport` 查找表查看收件人是在本地系统还是远程系统。

如果守护进程决定邮件应该投递到远程系统，队列管理器将激活 SMTP 服务来投递邮件。

SMTP 服务会尝试查找目标主机指定的邮件交换器（MX）；然后将邮件投递到收件人主机邮件交换器。

## 处理无法投递的邮件

队列管理器无法从活动队列中投递的邮件会被复制到延迟队列（deferred queue）。

随后，队列管理器会定期从延迟队列将这些邮件复制回活动队列，并再次尝试投递邮件。

## Postfix 程序包的组件

在 Postfix 安装期间，文件被保存到 SUSE Linux Enterprise Server 10 系统的各种位置。这些位置可以根据以下标准分组：

- `/etc/aliases`：这是 `/etc/` 下的唯一文件。它的格式与 MTA Sendmail 的别名文件相同，包含本地别名。
- `/etc/postfix/`：所有定义 Postfix 邮件处理的配置文件都在此目录中。通常，只有 Postfix 管理员可以修改这些文件。
- `/usr/lib/postfix/`：此目录包含 Postfix 直接需要的所有程序。准确来说，这些是 Postfix 的二进制文件。系统管理员不会直接访问这些程序。
- `/usr/sbin/`：此目录包含维护和手动控制 Postfix 的管理程序。管理员在维护期间使用这些程序。
- `/usr/bin/`：此目录包含符号链接。
- `/var/spool/postfix/`：此目录包含邮件队列。
- `/etc/sysconfig/postfix`：此文件包含特定系统的配置。
- `/usr/share/man/postfix/`：此目录包含手册页（man pages）。
- `/usr/share/doc/postfix/`：此目录包含文档。
- `/usr/share/locale/`：此目录包含本地化文件。

---

# 非 Postfix 软件的接口。务必检查非 Postfix 软件的手册页，以确定它所需的选项。

# maildrop。详情请参见 Postfix MAILDROP_README 文件。

| service | type | flags | user | argv |
| :--- | :--- | :--- | :--- | :--- |
| maildrop | unix | - n - n - pipe flags=DRhu | vmail | argv=/usr/local/bin/maildrop -d $(recipient) |
| cyrus | unix | - n - n - pipe | cyrus | argv=/usr/lib/cyrus/bin/deliver -e -r $(sender) -m $(extension) $(u) |
| uuccp | unix | - n - n - pipe flags=Fqhu | uuuc | argv=uuuc -r -nz -a$sender $nexthop!mail $(recipient) |
| ifmail | unix | - n - n - pipe flags=F | fetn | argv=/usr/lib/ifmail/ifmail -r $(recipient) $nexthop |
| bsmtp | unix | - n - n - pipe flags=Fq $(sender) | foo | argv=/usr/local/sbin/bsmtp -f $(sender) $nexthop $(recipient) |
| vscan | unix | - n - n - 10 pipe | vscan | argv=/usr/sbin/amavis $(sender) $(recipient) |
| procmail | unix | - n - n - pipe flags=R | nobody | argv=/usr/bin/procmail -t -m /etc/procmailrc $(sender) $(recipient) |

配置行中各个字段的含义及其可能的值列在下方。

如果有默认值，将列在描述中。如果某项设置为 `--`，则使用默认值。

- **service**：Postfix 进程的名称。

  由 inet 守护进程控制的服务的条目以 `host:port` 的形式指定。

  inet 是控制谁可以连接到你的计算机以及他们可以使用哪些服务。

  SMTP 服务的条目可以是：

  # **localhost:smtp**

  此条目将启动 Postfix 进程 `/usr/lib/postfix/smtpd`，使其仅在环回接口的端口 25 上接收电子邮件（如果该端口在 `/etc/services` 文件中正确输入）。

  主机前缀和后面的冒号是可选的。

- **type**：允许你指定连接类型。

  可能的条目有：

  - **inet**：用于互联网套接字 (TCP/UDP)
  - **unix**：用于 UNIX 套接字（仅用于本地通信）
  - **fifo**（先进先出）：用于命名管道
  - **private**：配置对服务的访问。

    - **y**（是）：仅定义从邮件系统对此服务的访问。
    - **n**（否）：也允许邮件系统外部组件访问此服务。对于类型为 inet 的服务，必须始终设置 **value n**。

    默认值为 **y**。

## 配置邮件服务器

- **unpriv.**：配置运行此服务的 UID。

  当取值为 **y**（是）时，配置的服务将以 `/etc/postfix/main.cf` 文件中变量 `mail_owner` 配置的非特权用户（通常为用户 postfix）身份运行。

  如果将此值设置为 **n**（否），该服务将以 root 权限（UID 0）运行。

  默认值为 **y**。

- **chroot.**：指定服务的 chroot 行为。

  取值 **y**（是）会导致服务在 chroot 环境中启动。

  该环境的根路径由 `/etc/postfix/main.cf` 文件中的变量 `queue_directory` 定义（通常是目录 `/var/spool/postfix/`）。

  默认值为 **y**。

- **wakeup.**：在指定的秒数过期后再次运行该服务。

  默认值 **0** 禁用该服务的此功能。

  目前只有 pickup 守护进程和队列管理器使用此功能。

  默认值为 **0**（从不）。

- **maxage.**：定义可以同时运行的最大进程数。

  默认值在 `/etc/postfix/main.cf` 文件的变量 `default_process_limit` 中定义。

  默认值为 **100**。

- **command + args.**：配置要运行的命令，包括所需的参数。

  要运行的命令路径相对于 `/etc/postfix/main.cf` 文件中通过变量 `daemon_directory` 定义的目录（通常是目录 `/usr/lib/postfix/`）。

  如果给出了一个或多个 `-v` 参数，则增加给定命令的调试级别。

  指定 `-D` 参数允许通过在 `/etc/postfix/main.cf` 文件中由变量 `debugger_command` 指定调试命令进行调试。

## 配置全局设置

所有其他配置定义（查找表中的处理规则配置除外）都设置在以下文件中：

`/etc/postfix/main.cf`

在 SUSE Linux Enterprise Server 10 上，此文件的最常用参数可以使用文件中的变量进行修改：

- `/etc/postfix/main.cf`
- `/etc/postfix/master.cf`
- `/etc/postfix/aliases`
- `/etc/postfix/maps`
- `/etc/postfix/generic`
- `/etc/postfix/warning_maps`
- `/etc/postfix/virtual`
- `/etc/postfix/transport`
- `/etc/postfix/regexp`
- `/etc/postfix/lpdtable`
- `/etc/postfix/miltertable`
- `/etc/postfix/header_checks`
- `/etc/postfix/header_maps`
- `/etc/postfix/body_checks`
- `/etc/postfix/body_maps`
- `/etc/postfix/content_checks`
- `/etc/postfix/content_maps`
- `/etc/postfix/access_checks`
- `/etc/postfix/access_maps`
- `/etc/postfix/sender_checks`
- `/etc/postfix/sender_maps`
- `/etc/postfix/recipient_checks`
- `/etc/postfix/recipient_maps`
- `/etc/postfix/restriction_checks`
- `/etc/postfix/restriction_maps`
- `/etc/postfix/timeout_checks`
- `/etc/postfix/timeout_maps`
- `/etc/postfix/virtual_checks`
- `/etc/postfix/virtual_maps`
- `/etc/postfix/transport_checks`
- `/etc/postfix/transport_maps`
- `/etc/postfix/relay_checks`
- `/etc/postfix/relay_maps`
- `/etc/postfix/warning_checks`
- `/etc/postfix/warning_maps`

（注：由于提供的原始 OCR 文本存在大量重复和错误，此处已根据逻辑进行了处理。）

## 配置邮件服务器

如果 `POSTFIX_LOCALDOMAINS` 为空，SUSEconfig 将该变量设置为 `$myhostname, localhost.$mydomain`。

- **POSTFIX_NULL_CLIENT**：空客户端（nullclient）是一种只能通过网络发送邮件、不通过网络接收邮件、且不在本地投递任何邮件的宿主机。

  如果你输入 yes，运行 SuSEconfig 后，文件 `/etc/postfix/main.cf` 中的变量 `mydestination` 将保持为空。

  默认项为 no。

- **POSTFIX_DIALUP**：如果此值设置为 yes，无法在本地投递的邮件在运行 `sendmail -q` 命令之前不会被发送到其目的地。

  该设置对于拨号系统非常有用；否则，当系统未上线时发送邮件将出现错误信息，或者如果使用按需拨号，则每条消息都会建立一个连接。

  值 no 将立即尝试投递任何等待投递的邮件。

  如果此变量赋值为 yes，运行 SuSEconfig 将会在 `/etc/postfix/main.cf` 文件中添加 `defer_transports = smtp` 行。

- **POSTFIX_NODNS**：如果此变量设置为 yes，Postfix 在处理邮件时将不对发件域和接收方域进行任何 DNS 查询。

  如果此变量赋值为 yes，运行 SuSEconfig 将激活 `/etc/postfix/main.cf` 文件中的变量 `disable_dns_lookups = yes`。

- **POSTFIX_CHROOT**：如果此变量设置为 yes，在可能的情况下，服务将在 chroot 环境中运行。你可以在 `/var/spool/postfix` 找到 chroot 环境。

  如果该变量设置为 no（默认值），则所有 Postfix 进程将在普通环境中运行。

- **POSTFIX_UPDATE_CHROOT_JAIL**：如果要让 SuSEconfig 设置 chroot 环境，则此值应设置为 **yes**。默认情况下，该变量被设置为 **no**。

- **POSTFIX_LAPTOP**：某些 Postfix 服务频繁访问 FIFO，导致硬盘无法停止旋转。然而，如果笔记本电脑上为了节电目的需要此操作，可以将该变量设置为 **yes**。

- **POSTFIX_UPDATE_MAPS**：如果让 SuSEconfig 从相应的查找表创建数据库文件，则此变量应设置为 **yes**（默认值）。

- **POSTFIX_MAP_LIST**：如果 `POSTFIX_UPDATE_MAPS` 设置为 yes，你可以在此处选择 Postfix 应支持的列表。

- **POSTFIX_RBL_HOSTS**：在此处你可以指定一个逗号分隔的主机列表，从这些主机可以获取 RBL（实时黑洞列表）。不接受来自这些列表中的客户端的邮件。只有当 **POSTFIX_BASIC_SPAM_PREVENTION** **未**设置为 off 时，此项才有意义。

- **POSTFIX_BASIC_SPAM_PREVENTION**：在此处，指定如何配置针对 UCE（垃圾商业邮件）的严格程度的过滤规则。可能的级别有 **off**、**medium** 和 **hard**。更多细节可以在 http://www.postfix.org/uce.html 找到。

- **POSTFIX_MDA**：在此处，指定 Postfix 应该与之协作的 MDA。条目如下：

  - **procmail**：使用 Procmail 在本地投递邮件。
  - **cyrus**：使用 lmtp 投递到 cyrus-imapd。
  - **local**：使用 Postfix 本地 MDA。

- **POSTFIX_SMTP_AUTH***：这些变量控制 Postfix 关于身份验证的行为：即 Postfix 是否接受邮件，以及 Postfix 是否向其他服务器投递邮件。

- **POSTFIX_SMTP_TLS_SERVER, POSTFIX_SMTP_TLS_CLIENT**：如果这些变量设置为 yes，在配置了以下变量的情况下，Postfix 在发送和接收邮件时可以与对方加密通信。

- **POSTFIX_SSL*, POSTFIX_TLS***：这些变量控制加密所需的各种证书和密钥管理的各个方面。本课程不涵盖加密连接；本手册不提供有关单个变量的任何细节。

- **POSTFIX_ADD***：这些变量可用于设置 Postfix 变量。变量必须转换为大写字母并附加到 `POSTFIX_ADD_` 之后。例如，要设置 Postfix 变量 `message_size_limit` 为 100000，在 `/etc/sysconfig/postfix` 中输入 `POSTFIX_ADD_MESSAGE_SIZE_LIMIT=100000`。随后，SuSEconfig 将在 `/etc/postfix/main` 中生成相应的条目 `message_size_limit=100000`。可以使用 `postfix` 列出所有可用的 Postfix 变量。

- **POSTFIX_REGISTER_SLP**：如果此设置为 yes，Postfix 会自动注册到 SLP。除了此方法外，还可以直接在 `/etc/postfix/main.cf` 文件中进行设置，该文件有非常详细的注释。手动修改文件 `/etc/postfix/main.cf` 后，修改 `/etc/sysconfig/postfix` 并随后运行 `/sbin/SuSEconfig` 将不会影响 `/etc/postfix/main.cf` 文件。

一些重要的变量有：

- **queue_directory**：邮件队列所在的目录。默认项为 `/var/spool/postfix`。
- **command_directory**：Postfix 工具所在的目录。默认项为 `/usr/sbin`。
- **daemon_directory**：Postfix 守护进程所在的目录。默认项为 `/usr/lib/postfix`。
- **mail_owner**：邮件队列的所有者。默认是 postfix。

## 配置邮件服务器

- **hostname**：定义计算机的主机名。此值将作为其他参数的默认值。默认给出 FDN（完全限定域名）。
- **mydomain**：计算机的域名。此值将作为其他参数的默认值。
- **myorigin**：本地发送邮件时显示的发送者域。默认值是 FDN。
- **mydestination**：描述计算机接受邮件的域列表。
- **masquerade_domains**：对于指定域的发件地址，将移除主机部分。例如，`user@domain.com` 变为 `user@domain.com`。
- **masquerade_exceptions**：指定不应隐藏的用户。默认输入 root。
- **relayhost**：所有无法在本地处理的邮件将发送到指定的计算机。
- **inet_interfaces**：指定 Postfix 等待邮件的网络地址。默认是 `127.0.0.1`。要让 Postfix 从其他主机接收，请输入网卡号或 all。
- **mynetworks**：列出属于网络的 IP 范围。Postfix 可以配置为转发这些网络的邮件。如果你不想手动指定网络范围，可以使用 **mynetworks_style** 选项，它允许三个值：

  - **class**：Postfix 信任同一 IP 类（A/B/C）的所有 SMTP 客户端。
  - **subnet**：Postfix 信任同一 IP 子网内的所有 SMTP 客户端。
  - **host**：Postfix 仅信任本地主机。

- **smtpd_recipient_restrictions, smtpd_helo_restrictions, smtpd_client_restrictions, smtpd_sender_restrictions**：控制谁允许通过邮件服务器转发邮件。

## 配置通用场景

以下场景假设 `/etc/sysconfig/mail` 文件中的变量 `MAIL_CREATE_CONFIG` 设置为 no。如果是这样，执行 SuSEconfig 将不会更改 `/etc/postfix/main.cf` 文件，也不会生成 `/etc/postfix/main.cf.SuSEconfig`。

由于这些文件通常包含有用的设置，某些部署场景下只需要少量修改。但请记住，文件 `/etc/postfix/main.cf` 中变量最后一个条目是有效的。

如果某个条目发生了更改，如果在文件的后半部分分配了不同的值，则该更改不会生效。

本文描述了以下主题：

- 将邮件转发到提供商的邮件服务器
- 通过互联网接收邮件

## 将邮件转发到提供商的邮件服务器

如果所有流量都通过 ISP 的邮件服务器运行，那么一个小型网络只需要一个接收客户端邮件并将其传递给 ISP 邮件服务器的邮件服务器即可。

由于本地邮件服务器不作为互联网上公司域名的邮件服务器，因此配置非常简单。

这样的邮件服务器必须：

- 接受来自内网客户端的邮件。
- 拒绝由其他客户端投递的邮件。
- 可能重写发送者地址。
- 将所有邮件提交到提供者的邮件服务器。

在 `/etc/postfix/main.cf` 文件中只需要少量更改。

以下条目仅确保 Postfix 只接受来自本地网络客户端的邮件：

```
```
