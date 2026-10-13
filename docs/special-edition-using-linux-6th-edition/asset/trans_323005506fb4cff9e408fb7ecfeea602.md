

```text
#       /usr/sbin/mta-switch newconfig
#
# or the program `newaliases' (works for smail and sendmail).
# Otherwise, the changes won't be visible to your MTA.

# Basic system aliases -- these MUST be present.
MAILER-DAEMON:    postmaster
postmaster:       root

# General redirections for pseudo accounts.
bin:              root
games:            root
ingres:            root
system:           root
toor:              root
news:             root
uucp:             root
operator:         root
ftp:              root
nobody:           root

# Well-known aliases.
manager:          root
dumper:           root
newsadm:          news
newsadmin:        news
usenet:           news
netnews:          news
gnats:            root
ftpadm:           ftp
ftpadmind:        ftp
ftp-adm:          ftp
# trap decode to catch security attacks
decode:           root

# Person who is to get root's mail
#root:            col
```

如下所示，向 `/etc/mail/aliases` 文件添加一个条目，即可将发送至 webmaster@calderasystems.com 的所有邮件定向发送到 glenn@calderasystems.com：

```text
webmaster:        glenn
```

别名还可以用于设置小型（通常是内部的）邮件列表。对于较大的部门级列表，可以使用 `include` 语句来包含文件列表。大型邮件列表应使用诸如 majordomo 之类的邮件列表程序来处理。要创建小型邮件列表，请在 `/etc/mail/aliases` 中放入邮件列表名称，后跟逗号分隔的用户列表：

```text
maillistname:     john,sally,mike,andrew
```

运行 newaliases 后，发送到 maillistname 的任何邮件都将被转发给 john、sally、mike 和 andrew。

> **注意：** 要使对此文件的更改生效，您必须运行 newaliases 工具。

## Debian 系统注意事项

尽管无论您运行的是哪种系统（各种 Linux 发行版，甚至其他 UNIX 系统），sendmail 都是 sendmail，但仍存在一些您必须了解的特定于发行版的特点。

上一节中的信息在 Debian 上同样适用，但除了更改一些路径名和文件名之外，您还需要做一些额外的事情。

Debian 有一个 sendmailconfig 脚本，可用于进行基本的 sendmail 系统设置。此脚本适用于大多数 sendmail 安装。只有特殊或高级配置才需要额外添加。

当 sendmailconfig 运行时，它会做的一件事就是根据前面提到的 debproto.mc 文件创建 /etc/mail/sendmail.mc。如果此 sendmail.mc 文件不存在，sendmail 将不会在启动时运行。您可能会发现先使用 sendmailconfig 更容易，然后如果生成的配置不符合您的需求，可以修改 sendmail.mc 文件，并使用它来创建后续的 sendmail.cf 文件。

您可以通过手动修改 /etc/mail/sendmail.mc 文件并再次调用 sendmailconfig 来做到这一点。添加到此文件底部的更改不会受到影响。

Debian 还使用一个名称不同的文件作为其 SysV 启动文件。此文件是 /etc/init.d/sendmail，它接受以下任意参数：start、stop、restart、reload、force-reload 或 debug。

## Red Hat 系统注意事项

Red Hat 在 /etc 以及 /usr/lib/sendmail-cf/cf 中都维护一个 sendmail.mc 文件。sendmail-cf 目录中的 redhat.mc 文件和 /etc/sendmail.cf 文件基本上是彼此的副本。决定您要使用哪一个，修改它，并从中创建新的 sendmail.cf。安装期间会提供一个相当通用的 sendmail.cf。

在启动时，Red Hat 的 init 脚本会查看文件 /etc/sysconfig/sendmail 以决定是否运行。如果您希望 sendmail 运行，只需确保 /etc/sysconfig/sendmail 中包含一行 DAEMON=yes。将其更改为 no 即可在启动时停止运行 sendmail。

在 /etc/sysconfig/sendmail 文件中，您还可以修改队列设置。默认情况下，Red Hat 每小时运行一次队列。只需将 1h 更改为 15m 或 30m，即可更频繁地运行队列（每 15 或 30 分钟一次）。

## 投递代理

投递代理与用户代理非常相似；它只是一种将实际消息送到收件人手中的方法。例如，对于传统邮件，收件人可以走到前院的邮箱前，或者开车到邮政信箱所在地。同样，电子邮件收件人可以使用不同的方法来收取自己的邮件。

## POP 服务器

邮局协议（POP）为最终用户提供了一种检索邮件的方式。这就像您走出家门到邮箱取信，再走回屋里坐下来阅读一样。使用 POP，当您表示想要检索邮件时，电子邮件就会被传送到桌面上的电子邮件客户端。通常，客户端桌面被配置为在每次建立拨号连接时或按预定的时间间隔执行此操作。邮件实际上是从服务器移动到客户端。

POP3 几乎不需要任何设置，并且在标准 Linux 安装中默认运行。POP3 从 `/etc/inetd.conf` 运行，因此如果需要，可以使用 TCP Wrappers 控制访问。只要 pop3 条目列在 `/etc/services` 中，并且 pop3 行出现在 `/etc/inetd.conf` 中（并且没有被注释掉），您就已经在运行 POP3 了。您可以通过检查 `netstat -an` 的输出中是否有本地端口 110 在监听来验证这一点。

## IMAP 服务器

IMAP 服务器的行为与 POP 服务器非常相似，但有一个主要区别——IMAP 服务器并不会真正将电子邮件从服务器传输到客户端桌面。它基本上为给定用户创建一个“映射”，使其能够直接在电子邮件服务器系统上阅读邮件。IMAP 与 POP 相比的优点和缺点，与集中式处理与分布式处理的优缺点非常相似。

IMAP 虽然是与 POP3 不同的程序，但它的运行方式与 POP3 完全相同，也是通过 `/etc/inetd.conf`——只是使用端口 143 而不是 110。由于 IMAP 功能稍强一些，因此也稍更容易受到攻击。如果您使用 IMAP，您需要使用 TCP Wrappers 来限制访问。

## 启用 POP 和 IMAP 服务

如果尚未运行，启用 POP 或 IMAP 服务都是一项非常简单的任务。这两种协议都预先定义在 `/etc/services` 文件中。唯一真正的要求是安装 IMAP RPM。

安装 RPM 后，当在相应端口上检测到 POP 或 IMAP 服务请求时，就会调用相应的守护进程，如 `/etc/services` 文件中所定义。这就是设置 POP 和 IMAP 服务的全部工作。启用它们之后，就可以将电子邮件客户端配置为通过此服务器接收电子邮件。

## FETCHMAIL

fetchmail 是一种特殊类型的投递代理，它可以从 ISP 下载邮件包，或从不同的 POP 和 IMAP 服务器抓取邮件并将其存放在本地。

fetchmail 要求接收系统上运行着 sendmail。这是一个非邮件系统不需要运行 sendmail 的唯一例外。这是因为 fetchmail 会通过端口 25 将所有邮件转交给电子邮件服务器。

fetchmail 的文档写得非常清楚，包含如何将 fetchmail 设置为守护进程在启动后按指定时间间隔运行并下载邮件的示例，这使其非常适合仅拥有拨号连接的公司。但 fetchmail 附带一个 X 工具 fetchmailconf，可用于轻松配置和测试 fetchmail 以确保正常运行。此工具需要 python 才能运行。

## MBOX

本地系统上的邮件以称为 UNIX mbox（邮箱）格式的格式保存。这是一个文件，邮件消息到达时会追加到文件末尾。您的 sendmail 服务器在本地接收的邮件将由 deliver 或 procmail 程序存放到 /var/spool/mail/$USER 中。这些邮件可以通过前面提到的任何方法访问，也可以由 mail 程序直接访问。

## 加密与良好隐私（PGP）

想象一下，通过美国邮政服务寄出一封写有私人信件的明信片。所有经过这张明信片的人都能看到它，对吧？因此，不需要太多想象力就能理解为什么私人信件通常要装在密封的信封里寄达目的地。如果信件被错误投递，或者出现其他投递问题，信件仍会在信封密封的情况下被退回。那封信的隐私从未受到损害（除非有人决定撕开信封阅读它）。

现在，想象一下通过互联网（甚至在一个小型网络内）发送电子邮件。至少有一台发送机器之外的机器会收到该消息；如果您要与互联网上的某个人传递消息，那么会有许多不同的机器处于电子邮件的传输路径上。在每个停留点——以及中间的几个点——都完全有可能有人读到这条消息。毕竟，它是纯文本，没有被密封在任何东西中。如果投递过程中出现问题，消息最终被送到另一个目的地，那么在它被退回之前，很可能已经被阅读过。

简而言之，电子邮件默认情况下根本不安全。使用电子邮件发送的文件附件也是如此。即使是存放在本地计算机上、永远不会通过网络传输的敏感文件，只要计算机在一段时间内无人看管，也是不安全的。

电子文档、二进制文件以及任何其他可以存放在硬盘上并且需要保密的内容，都需要某种可以密封在它们周围的外壳。除了每次无人看管时都把计算机装进一个大盒子里并密封之外，似乎只有一种技术能提供有效的解决方案：加密。

不过，并非任何加密都有效。一种称为 *公钥加密* 的加密方案几乎已成为加密敏感信息的事实标准。

