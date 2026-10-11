
例如，请考虑列表 6.4 中所示的客户端/服务器交互。

## 列表 6.4 POP3 会话：传统（USER/PASS）认证

```
[ramon]$ telnet pop3.example.com 110
Trying 209.1.78.12 ...
Connected to pop3.example.com.
Escape character is '^]'.
+OK QPOP (version 3.1b6) at pop3 starting. <3606.975375600@redhat>
USER ramon
+OK Password required for ramon.
PASS mysecret
+OK ramon has 1 visible messages (0 hidden) in 890 octets.
```

列表 6.4 中实现的主要安全缺陷在于，用户必须在认证序列中提供密码。这会将部分秘密材料暴露于公共互联网上的窃听之下，特别是考虑到某些 POP3 客户端可以被配置为定期自动联系服务器以检查新到达的邮件。

为了缓解这一风险，POP3 协议开发者通过修改原始标准，引入了一种挑战/响应机制，在这种机制下，POP3 服务器会向客户端呈现一个挑战（当前系统时钟的十进制值）。然后由客户端负责生成挑战的 MD5 单向哈希值，并将其附加到 POP3 管理员分配给用户的认证密码上。随后，客户端在 APOP 行中返回哈希结果。如果服务器在其端成功复现该响应，并且它与客户端返回的响应相匹配，则认证成功，用户将被允许从他们的邮件箱中检索邮件。

在列表 6.5 的示例中，用户名 ramon 正在尝试登录 pop3.example.com 以阅读他的邮件。

## 列表 6.5 POP3 会话：APOP 认证

```
[ramon]$ telnet pop3.example.com 110
Trying 209.1.78.12 ...
Connected to pop3.example.com.
Escape character is '^]'.
+OK QPOP (version 3.1b6) at pop3 starting. <3606.975375600@pop3>
APOP ramon 59df6759df98s7d9fs7d9f75d9f758g
+OK ramon has 1 visible messages (0 hidden) in 890 octets.
```

列表 6.5 中的 POP3 服务器向用户呈现挑战（即用户在回复中必须使用的字符串）：

`<3606.975375600@pop3>`

客户端将其附加到密码，以形成以下字符串：
`<3606.975375600@pop3>mysecret`

然后，它将此字符串输入 MD5 算法，从而生成一个哈希值
`s9df67$s9df798$s7d9f57d9f7s9df758g`

请注意，这种方法的稳健性源于从 MD5 哈希值中获取原始*种子*在数学上是不可行的这一事实。因此，即使窃听者知道 POP3 服务器发送给客户端的挑战，他们反向推导 MD5 函数以获取种子的风险也极小。

下一节将引导您完成安装高通 Qpopper 软件包的过程，包括如何配置 APOP 认证方法。

### 安装 Qpopper 软件

大多数 Linux 发行版默认通常不会安装 Qpopper 软件包，但可以轻松地以 RPM 格式获取它，并使用 Linux *rpm* 实用程序进行安装，步骤如下：

```
[ramon]$ sudo rpm -i qpopper-3.1b6-3k.i586.rpm
```

此命令将安装服务器二进制文件和手册页，以及有限的文档集。下一节将展示如何设置 POP3 服务器及其扩展认证功能。

### 配置 Qpopper 软件

本书撰写时的 Qpopper 最新版本（3.1）不会自动创建 *xinetd* 条目以便自动生成自身。为了确保这种情况发生，只需创建包含列表 6.6 中内容的文件 */etc/xinetd.d/qpopper* 即可。

## 列表 6.6 /etc/xinetd.d/qpopper 文件的内容

```
service pop3
{
    socket_type           = stream
    wait                  = no
    user                  = root
    server                = /usr/sbin/in.qpopper
    log_on_success        ++ USERID
    log_on_failure        ++ USERID
}
```

列表 6.6 中的指令确保您的服务器以 `/usr/sbin/in.qpopper` 为守护进程，监听对 POP3 服务（TCP 端口 110）的请求。

如果您使用的是 `inetd` 而不是 `xinetd`，只需在您的 `inetd.conf` 文件中输入以下内容：

```
pop3 stream tcp nowait root /usr/sbin/in.qpopper in.qpopper
```

配置中的下一步是创建一个用户名（例如，`pop`）来拥有用于 APOP 的认证数据库（用户/密码关联）（参见图 6.1）。在此图中，正在 Red Hat 上使用 `linuxconf` 来创建 POP3 管理账户。

![](img/3258bbaf790525f8c4eb25fabff7844a_186_0.png)

您应该将 POP3 提供的 `popauth` 工具的所有者更改为 `pop`，并使用以下命令使其变为 `suid pop`：

```
[ramon]$ cd /usr/sbin
[ramon]$ sudo chown pop popauth
[ramon]$ sudo chmod u+s popauth
```

第一次运行 `popauth` 工具时，您将使用它来创建认证数据库，步骤如下：

```
[ramon]$ sudo popauth -init
```

您必须确保新创建的认证数据库文件只能由 `pop` 用户读取：

```
[ramon]$ ls -1 /etc/pop.auth
-rw-------  1 pop popusers 1544 Nov 27 22:08 /etc/pop.auth
```

此时，您拥有一个崭新的 Qpopper 安装环境，已准备好填入新的 POP3 用户。下一节将解释如何执行此操作。

## 使用 Qpopper 软件

当向服务器添加新用户时，您还需要允许他们使用 APOP 认证访问您的 POP3 服务器。这需要为每个新用户添加 `/etc/pop.auth` 中的条目。要添加这些条目，只需发出如下 `popauth` 命令：

```
[ramon]$ sudo popauth -user ramon
Changing only APOP password for ramon.
New password: mysecret
Retype new password: mysecret
```

请注意，此示例使用 `sudo` 命令以 root 身份运行 `popauth`，但事实上，该命令也可以由用户 `pop` 执行。如果需要撤销用户的 POP3 访问权限，只需使用以下命令将该用户从数据库中删除：

```
[ramon]$ sudo popauth -delete ramon
```

一旦用户被添加到 `/etc/pop.auth`，他们就可以更改自己的密码，作为自己的用户调用 `popauth` 实用程序，不带任何命令行选项，步骤如下：

```
[ramon]$ popauth
Changing only APOP password for ramon.
Old password: mysecret
New password: newsecret
Retype new password: newsecret
```

本节讨论了 POP3 协议、其安全缺陷以及您如何绕过它们。下一节讨论 IMAP 协议的实现，它是 POP3 的一种替代方案，在 Linux 服务器社区中正获得极大的普及。

## IMAP

虽然 POP3 仍然是最流行的邮件检索协议，但其基本缺陷之一是需要将消息下载到用户计算机（客户端）才能访问它们。这使得用户很难在实际上下载之前选择他们想要查看哪些消息。它同时也使得从多个客户端读取邮件的同时保持邮箱同步变得具有挑战性。互联网邮件访问协议（IMAP）于 1986 年左右在斯坦福大学开发，以解决这一缺陷，并针对通用的 POP3 协议添加了许多其他改进。

IMAP 是一个真正的客户端/服务器协议，独立于访问邮件服务器所使用的传输方式。它还允许您访问远程服务器上的不同邮件文件夹，无论您的身份如何，也无论拥有远程邮箱的用户是谁。虽然这提供了前所未有的灵活性，但也带来了一些担忧，并增加了恶意窃听邮件流量（当其从 IMAP 服务器接收时）的风险。更重要的是，如果在客户端和服务器之间没有加密，用户名/密码交换也将以明文形式进行。

如果您的需求使得您能够受益于向邮件用户提供 IMAP 服务，下一节将指导您完成安装 IMAP 服务器软件的过程，而不会危及服务器的安全性或邮件内容及用户认证交换的隐私性。

### 安装 IMAP 服务器软件

华盛顿大学的 IMAP 服务器是目前 Linux 上最受欢迎且支持最积极的 IMAP 软件包。虽然大多数 Linux 发行版通常不会默认安装它，但可以轻松地以 RPM 格式获取并使用 Linux *rpm* 实用程序进行安装：

```
[ramon]$ sudo rpm -i imap-2000-3.1386.rpm
```

此命令将安装服务器二进制文件和手册页，以及有限的文档集。下一节将展示如何设置安全的 IMAP 服务器，以及如何在 xinetd 和 inetd 上启用它。

### 配置安全的 IMAP 服务器

imapd-2000 软件包使用 OpenSSL 作为其安全传输选项（imapd）。为了配置 SSL 服务，只需使用以下命令创建一个自签名证书：

```
[ramon]$ cd /usr/share/ssl/certs
[ramon]$ sudo make imappd.pem
```

这将导致创建文件 /usr/share/ssl/certs/imappd.pem，其中包含 imapd-2000 将用于为 IMAP 交换添加 SSL 保护的密钥和证书。请注意，IMAP 会在 /etc/xinetd.d 目录中插入两个文件，如列表 6.7 中的步骤所示。

