

# 配置 Sendmail

**注意** 通过 sendmail.mc 中的 `FEATURE` 命令传递的选项通常用单引号括起来。然而，与大多数配置工具不同，m4 需要不同的起始和结束引号。起始引号是反引号字符（back-quote），它通常位于键盘上数字键 1 左侧的键上。结束引号是普通的单引号字符，在许多键盘上位于分号（;）右侧的键上。

当然，你应该修改 `mail.cf` 以匹配你组织的 ISP 邮件中继系统。当你重建 `sendmail.cf` 并重启 sendmail 后，结果将是通过你本地 sendmail 发送的所有邮件都将通过你指定的邮件中继系统中继。

**提示** 使用 ISP 邮件中继的一个常见反对来自使用多个 ISP 的用户。因为大多数 ISP 拒绝来自其域之外的中继尝试，这种配置仅在一个 ISP 上有效。解决这个问题的一种方法是创建两个 `sendmail.cf` 文件，每个 ISP 创建一个。为它们命名为合适的名称，例如 `sendmail.cf.isp1` 和 `sendmail.cf.isp2`。然后你可以修改你的 PPP 拨号脚本（在第 12 章中描述），将自定义文件复制到常规 `sendmail.cf` 并重启 sendmail。结果是，sendmail 将通过任何合适的 ISP 邮件服务器进行中继。

# 配置 Sendmail 为域名进行中继

在作为工作站的小型 Linux 系统上，配置 sendmail 使用另一个邮件服务器作为中继通常非常方便。然而，Linux 经常用作其他邮件服务器。当 Linux 服务器具有始终连接的互联网专用连接时，这种配置效果最好。默认情况下，Red Hat Linux 7.0 的配置为不中继来自其他系统的邮件。这是一项反垃圾措施，但它阻碍了将 Linux 服务器作为你自己电脑的中继使用。技巧是放宽而不是移除反中继限制。

**注意** 要让 sendmail 作为中继运行，它还必须配置为接收邮件。这在安装时通常能正常工作，但如果你遇到问题，请检查“接收邮件”（Receiving Mail）章节。

![](img/4fb617eb648f87def380ef5d92052d01_612_0.png)

为了允许 sendmail 中继某些类计算机的邮件，你必须在 `sendmail.mc` 或其等效文件中添加 `FEATURE` 行。该 `FEATURE` 行包含以下选项之一：

- **promiscuous_relay** *极其危险* 选项告诉 sendmail 中继任何经过它的邮件。不要使用此选项，因为这几乎保证了垃圾邮件发送者迟早会滥用你的系统。

- **relay_based_on_MX** 此选项配置 sendmail 接受来自其他计算机的中继，只要这些计算机的域名被配置为将你的系统显示为 MX。此选项在安全性上相当松散，因为它本质上允许他人（任何控制远程系统 DNS 服务器的人）决定你的系统是否将作为中继运行。

- **relay_entire_domain** 如果你设置了此选项，sendmail 将接受来自其所属域内任何主机的邮件。这可以是将 Linux 系统配置为受限中继的一种方便方法。

- **relay_local_from** 此选项告诉 sendmail，如果发送者使用服务器的地址作为自己的地址，则接受中继。这在某些情况下很方便，但也容易被滥用。

- **relay_hosts_only** 此选项与访问数据库（稍后描述）配合工作，允许你将单独的主机列为可接受或不可接受中继。

- **access_db** 此功能允许你使用访问数据库（稍后描述）列出 sendmail 将进行中继的域名。

例如，Red Hat Linux 的默认 `sendmail.mc` 文件包含以下行：

> FEATURE(`access_db`)

你可以根据网络情况修改此行以使用其他中继选项。或者，你可以调整访问数据库。在 Red Hat 7.0 中该文件是 `/etc/mail/access`，但在某些发行版中可能出现在其他地方。该文件包含每行一个域名、主机名或 IP 地址，后跟着指示 sendmail 如何处理来自发送者的标签。（以 # 开头的行会被忽略。）Red Hat 7.0 的默认配置如下：

```
# by default we allow relaying from localhost
localhost.local      RELAY
localhost               RELAY
127.0.0.1               RELAY
```

有效标签如下：

- **OK** 强制 sendmail 接受邮件，即使其他规则拒绝它。
- **RELAY** 接受来自或发往指定域的中继邮件。默认配置接受本地邮件；技术上，当本地程序通过 sendmail 发送邮件时，它作为邮件中继，因此如果你想发送邮件，就需要此配置。
- **REJECT** 拒绝来自或发往指定域的邮件。sendmail 生成退信邮件告知发送者失败。
- **DISCARD** 类似于 REJECT，但 sendmail 不生成退信邮件。
- **fail** 类似于 REJECT，但向发送者返回错误代码。

可以通过域名（如 spam.net）或 IP 地址（如 192.168.0.0，匹配 192.168.0/24 网络）来指定域。配置 sendmail 最安全的方法是通过 IP 地址指定网络，因为这比域名更容易强制。假设你想配置来自 192.168.0/24 网络的 sendmail 中继，你可以在 `/etc/mail/access` 中添加以下条目：

```
192.168.0.0                RELAY
```

但在在使用此条目之前，你必须将文本模式的 `/etc/mail/access` 文件转换为存储在 `/etc/mail/access.db` 中的二进制格式。通过输入以下命令来实现：

```
makemap /etc/mail/access < /etc/mail/access
```

> 提示 在 Linux 上，你不需要执行 makemap 命令，因为 sendmail 启动脚本会自动执行。

一旦输入了命令，你可以重启 sendmail，它将配置为中继来自 192.168.0/24 网络的邮件。最好的方法是在另一台计算机上配置 MUA 使用你调整的系统作为邮件服务器来测试你的设置。你应该从一台不应该该系统作为邮件中继的计算机检查系统是否过于松散。

# 接收邮件

Linux 也可以接收通过 SMTP 发送的邮件。为了做到，sendmail 必须以守护模式运行——也就是说它必须一直运行并监听 25 端口。要以守护模式运行 sendmail，必须带有 -bd 切换启动，如 `sendmail -bd`。这是 Red Hat Linux 7.0 的默认配置。你可以使用 `ps` 命令检查 sendmail 是否以此种方式运行：

```
$ ps ax | grep sendmail
```

```
2536 ?S    0:00 sendmail: accepting connections
```

sendmail "accepting connections" 语句表示 sendmail 确实以守护模式运行。但如果不是呢？在这种情况下，你必须手动启动 sendmail 或修改你的启动脚本。在 Red Hat 7.0 中，相关脚本是 `/etc/init.d/sendmail`，但在其他发行版中相应的脚本可能有其他名称。你应该找到对 sendmail 的调用；在 Red Hat 7.0 的情况下，启动脚本通过 -bd 参数设置此参数。在 `/etc/sysconfig/sendmail` 文件中设置了 DAEMON 变量的情况下，该文件在 sendmail 启动脚本早期被加载。

sendmail 接收邮件的另一个要求是程序必须配置为接受其已知主机名的邮件。例如，考虑虚构的邮件服务器 express.gov。如果 express.gov 的 DNS 记录包含指向 express.gov 的 MX 记录，该机器必须接受发往 express.gov 的本地邮件，尽管机器名不是 express.gov。幸运的是，这很容易实现：你只需要将计算机的别名添加到 `/etc/mail/hosts` 并重启 sendmail（某些发行版中为 `/etc/sendmail.cc`）。例如，以下 `/etc/mail/local-hosts` 文件告诉系统除了计算机使用的主机主机外，还接受发往 express.gov 和 postit.gov 的邮件：

```
express.gov
postit.gov
```

你应该问自己一个问题，你是否希望你的系统接收 SMTP 邮件。普通工作站不需要这种能力，因为另一台计算机作为工作站的邮件服务器；工作站使用拉取邮件协议从服务器检索邮件。如果你更改了 `/etc/sysconfig/sendmail` 或 `/etc/rc.d/init.d/sendmail` 启动脚本使 DAEMON=no 而不是 yes，你仍然可以从本地程序发送邮件，但你需要使用拉取协议接收邮件。如果一个系统不需要接收 SMTP 邮件，这样配置它是一个好主意。这样做消除了坏分子进入

