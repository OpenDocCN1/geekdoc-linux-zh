
named 用户和组应该与系统中的其他内容隔离以实现安全；`dns` 是一个很好的选择。当然，在 `/etc/passwd` 用户条目的第二个字段中指定加密密码将防止此类账户的登录。将 `/dev/null` 指定为用户的登录 shell 将进一步锁定该账户。

请记住，守护进程的工作是确定主机名的 IP 地址，它需要做的只是在 53 端口进行通信并写入几个它自己的文件。因此，它是被放入 chroot 监狱的极佳候选者，这样它就不会损坏任何东西（可能对 IP 地址 撒谎除外）。在 Red Hat、Mandatory 以及其他使用 `/etc/rc.d/*.init/named` 文件的发行版中修改读取行：

`daemon named`

`daemon named -u dns -g dns`

创建 `dns` 用户和组时，应具有一个未被使用的 UID 和 GID，并禁用密码，使用 `/dev/null` 作为 shell，并拥有自己的主目录，例如 `/home/dns`，模式为 700。

`-t` 标志可用于指定启动时进行 chroot 的目录。`/home/dns` 是 `-t` 的良好参数。你需要将任何动态库拷贝到 `/home/dns` 以及它所需的配置文件（通常为 `/etc/named*`）。由于 root 可能会逃出 chroot “监狱”，因此在打开 53 端口后，务必使用 `-u` 和 `-g` 标志以切换到非特权用户和组。

#### 4.6.2 提供服务

就像《阴影之地》第 3 集一样，你需要决定其他系统可能如何使用你系统的服务。你不希望网络外的系统能够：

> 危险等级 ☠☠☠☠

`named` 程序（即名称守护进程或 DNS 守护进程）是用于将完全限定主机名（例如）

`www.realworldlinuxsecurity.com`

转换为其数字 IP 地址（例如）

`192.168.57.88`

如果没有它，就没有通过 `www.cute-name.com` 的互联网；将只有 `63.236.72.248`，而且更难处理且不那么华丽。不为其他系统路由流量的叶节点不需要运行它。它们只需要在 `/etc/resolv.conf` 中指定其名称服务器的数字 IP 地址，任何程序（如 `sendmail`、`telnet` 和 `Netscape`）将只需读取 `/etc/resolv.conf` 并直接向远程名称系统的 `named` 发起 DNS 查询请求。小型“仅内部”网络可能完全不使用 DNS，它们将依靠每个系统的 `/etc/hosts` 文件设置正确。

### 4.7 POP 和 IMAP 服务器

这种 set-GID 技术将限制某人在读取、修改或删除所有人的邮件时可能造成的破坏。使用 PGP 的用户仅面临被删除的风险。IMAP 服务器与 POP 非常相似，但由于是独立的代码，因此它会有不同的缓冲区溢出漏洞。

POP3 和 IMAP 通过 `libwrap` 支持 TCP Wrappers。除非员工需要在办公室以外下载电子邮件，否则应使用 TCP Wrappers 或 IP Chains 来阻止组织外部访问您的服务器。

若要在 Linux 服务器上启用经过 SSL 封装的 IMAP 和 POP3，请遵循以下步骤：

- 1. 如果尚未存在，请将服务添加到 `/etc/services`：

```
imaps 993/tcp
pop3s 995/tcp
```

- 2. 在 `/etc/xinetd.d` 目录下创建以下文件，由 root 所有，权限模式为 644 或 600（基于 xinetd 的系统）。

```
# IMAPS 服务允许远程用户使用支持 SSL 的
# IMAP 客户端（如 Netscape Communicator 或 fetchmail）
# 访问其邮件。
service imaps
{
socket_type       = stream
wait             = no
user             = root
server           = /usr/sbin/imapsd
log_on_success  += DURATION USERID
log_on_failure  += USERID
disable          = no
}
```

`pop3s`:

```
# POP3S 服务允许远程用户使用支持 SSL 的
# POP3 客户端（如 fetchmail）
# 访问其邮件。
service pop3s
{
socket_type       = stream
wait             = no
user             = root
server           = /usr/sbin/ipop3sd
log_on_success  += USERID
log_on_failure  += USERID
disable          = no
}
```

- 3. 将调用添加到 `/etc/inetd.conf`（基于 inetd 的系统）：

```
imaps stream tcp nowait root /usr/sbin/tcpd sslproxy -t 3600 -p imap
pop3s stream tcp nowait root /usr/sbin/tcpd sslproxy -t 3600 -p pop-3
```

`sslproxy` 程序（以及 SSL 的其他组件）可以从此处下载：

`www.openssl.org/`

SSL 封装的 POP 和 IMAP 其他替代方案，包括使用 Kerberos 的 SSH 封装的 POP 和 KPOP。设置 SSH 封装的 POP 的文档可以从此处获取：

`www.linuxdoc.org/HOWTO/mini/Secure-POP+SSH.html`

### 4.7.1 命令行上的密码，天哪！

| 危险等级 | ☠ ☠ ☠ ☠ |

| :--- | |

少数程序（如 `popclient` 和 `smbpasswd`）允许你在命令行上指定密码。这些密码对系统上任何调用该命令的人都是可见的。

命令行上真的不应该允许密码，建议获取这些程序的源代码并将此功能替换为从指定文件读取密码，该文件应为调用程序的用户以外的用户无法访问（权限为 400 或 600）。

对于 `popclient` 和类似的程序，建议移除 `-p password` 标志并创建一个 `-P password_file`，用于从 `password_file` 文件读取密码（该文件可以是 `-` 表示标准输入）。通常，`-p` 的参数存储在环形指针或缓冲区中。你可能需要添加自己的缓冲区，并当程序以特权（set-UID，set-GID）或以 root 等特权用户运行时创建缓冲区以防止缓冲区溢出。

对于 `popclient`，对 `popclient.c` 中的 `parsecmdline` 函数进行以下更改将解决此问题，允许其在自动化脚本中安全使用。带有此或其他增强版本的程序源码可在配套 CD-ROM 获取。

- 1. 通过更改以下内容添加 `-p` 标志：

```
while (!errflag &&
    (c = getopt(argc, argv, "23Vkvcu:p:f:m:n:")) != EOF) {}
```

改为：

```
while (!errflag &&
    (c = getopt(argc, argv, "23Vkvscu:P:f:o:m:n:*")) != EOF) {
```

- 2. 找到行：

```
case 'p':
```

并将其后的两行从：

```
    strcpy(options->password, optarg);
    break;
```

改为：

```
    fprintf(stderr, "popclient: -p disabled for security; use -P\n");
    exit(1);
```

- 3. 然后在禁用 -p 的最后一个更改之后紧接着添加以下 `case` 情况：

```
case 'P':
    if (!strcmp(optarg, "-**"))
        c = 0; /* - 是 stdin. */
    else
        c = open(optarg, 0);
    if (c < 0) (
        perror(optarg);
        exit(2);
    )
    i = read(c, options->password, PASSWORDLEN);
    if (c)
        close(c);/* 如果不是 stdin 则关闭。 */
    if (i < 0 || i >= PASSWORDLEN
        || ! (s = strchr(options->password, '\n'))) {
            fprintf(stderr, "popclient: -p disabled for security; use -P\n");
            exit(1);
        }
        *s = '\0';
    break;
```

# 210 第 4 章 • 常见的黑客子系统
