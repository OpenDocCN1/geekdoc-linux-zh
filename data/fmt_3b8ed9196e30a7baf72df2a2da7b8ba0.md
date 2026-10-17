
| lmhosts | root / 644 |

| smb.conf | root / 644 |

| 用户名映射文件 | root / 600 |

| smbpasswd | root / 600 |

| secrets.tdb | root / 600 |

每个文件相关的风险类型各异。Samba 的主配置 `smb.conf` 对修改最为敏感，因为 Samba 是以 root 用户运行的。如果普通用户有修改此文件的能力，那么该用户可以在五分钟内获得系统的 root 权限。考虑一下如果一个名为 bob 的用户创建了如下共享，会发生什么：

```
myshare
path = /
read only = no
admin users = bob
```

bob 现在将拥有服务器文件系统上每个文件的写入权限。从这里开始，将 root 密码更改为 shell 提示符只需要对 `/etc/passwd` 进行几处编辑。一旦 bob 能够登录到服务器上的 root shell，他所能造成的恶作剧将是无止境的。

此警告也适用于对用户可写且稍后通过 `include` 参数合并到 `smb.conf` 中的文件。这种情况并不比之前用户可以直接修改 `smb.conf` 的情况好。事实上，结果完全相同。

被忽视的用户名映射文件也可能是安全问题的来源。想象一下我们的用户 bob 在用户名映射文件中插入了这样一行：

```
root = bob
```

这不像一个可写的 `smb.conf` 那样巨大的安全漏洞（尽管这是一个非常糟糕的情况），因为无法一眼看出 bob 将如何获得 root shell。然而，如果 bob 在 Samba 共享上创建一个指向 `/etc/passwd` 的符号链接，并且开启了 `symlinks = yes`（默认设置），那么 bob 就再次接管了服务器。

在第 7 小节中，我们学习了存储在 `smbpasswd` 文件中的 LanMan 和 NT 密码哈希是明文段。为了参与 NTLM 身份验证会话，客户端只需要原始密码的哈希值。因为密码字符串始终会哈希为相同的值，所以在更改原始密码之前，哈希值都是有效的。如果入侵者能够简单地读取服务器的 `smbpasswd` 文件，他就可以伪装文件中的任何用户。

Samba 2.2 的某些功能，例如 Windows NT 安全选项卡中的“取得所有权”按钮，可以在以 root 身份连接 Samba 服务器时利用。由于为了利用 Samba 2.2 的某些新功能，`smbpasswd` 文件包含 root 条目的概率增加，保护密码哈希列表的风险随之提高。如果用户在连接到 Samba 服务器时能够伪装 root，其可能性与 bob 能够修改用户名映射文件的情况相同。

Samba 的 `secrets.tdb` 包含了各种信息。最常见的是 Samba 作为 Windows 域成员时的机器信任账户信息。此密码可用于伪装 Samba 服务器以与 Windows 域控制器进行通信。成员服务器可以获取有关域用户的某些信息。允许非 root 用户访问此文件可能会导致你的 Windows 域遭受安全性。

最后，`lmhosts` 文件经常被管理员忽略，但它实际上是……

- 在某些情况下，

- 该选项在 `ssh(8)` 手页中有详细描述，提供了一种无需提示密码即可验证客户端的方法，适用于 `cron(8)`。

# 病毒和蠕虫防护

在编写时，最近的互联网病毒……

Samba 无论运行在何种硬件平台上，都不会执行 Windows 代码，包括 VBScript 等脚本语言。在这方面，Samba 服务器不会被 Windows 病毒感染。然而，利用 Samba 服务器（或任何文件服务器）来传播病毒或蠕虫是可能的。

防止病毒传播的最简单方法是禁止用户访问受感染的文件。可以通过 `smb.conf` 服务级参数 `veto files` 实现。`veto files` 接受一组文件名或通配符，这些文件对用户是不可见的。这与 DOS 隐藏属性不同。

> 在 Samba 2.2 及之前的版本中，用户可以在 Samba 共享上创建匹配 `veto files` 列表的文件，但永远无法访问它们。

以下设置用于防止 Samba 传播 Nimda 蠕虫。注意 `veto files` 参数定义在 `[global]`，使其成为所有共享的默认设置。

## 安全提示

```
[global]
<...>
## 阻止 Nlmda 蠕病毒的传播
veto files = /*.eml/*.news/riched20.dll/
```

指定否决文件（`veto files`）可能会在尝试从 Windows 客户端从 Samba 文件系统中删除目录时，导致令人困惑的行为。由于用户无法看到任何被否决的文件，一个目录可能看起来是空的，但实际上并非如此。这可能导致删除文件夹的操作失败，并显示“该目录仍包含文件或子目录”的错误信息。

如果在删除目录时需要自动删除否决文件，必须启用 `delete veto files` 选项。

```
[global]
<...>
## 在删除目录时移除任何否决文件
## 可能会导致性能损失。详情请见 smb.conf
delete veto files = yes
```

![](img/e6dc042fe420c610acdd193e834a4772_334_0.png)

# 通过 SSL 固化对 SWAT 的访问

在第 6 小节中提到的 SWAT 的主要安全缺陷是传输了未加密的数据，特别是在发送初始凭据以建立用户身份时（即服务器的 root 密码）。就像从服务器到服务器安全分发 `smbpasswd` 的解决方案一样，我们将寻求一些加密工具的帮助。

这里我们转向 Stunnel，它可以在 http://www.stunnel.org/ 处获得。stunnel 服务器使用 OpenSSL 库（http://www.openssl.org/）充当未启用 SSL 的应用程序的代理。图 17.3 显示了 stunnel 如何为 SWAT 添加 HTTPS 支持。客户端直接与 stunnel 守护进程通信，该守护进程仅处理 SSL 通信。所有的 HTTP 流量都会被传递给 SWAT。

> SSL 代表“安全套接层”（Secure Sockets Layer）。Unix（以及 Windows）上的标准网络编程接口是 Berkeley Socket API。通过将加密库与此编程模型相结合，我们得到了安全套接层，并因此得名。

![](img/e6dc042fe420c610acdd193e834a4772_334_1.png)

## 图 17.3

使用 stunnel 在 SWAT 中实现 HTTPS

![](img/e6dc042fe420c610acdd193e834a4772_335_0.png)

在继续之前，必须正确安装 OpenSSL 和 Stunnel。加密和加密软件的配置并非易事。坦率地说，这两个包都有二进制分发版本。请咨询您的 Unix 供应商或免费软件库以确认其可用性。如果显然 OpenSSL 和 Stunnel 需要从源码编译，只需按照软件自带以及各自网站上提供的文档操作即可。通常，这将归结为标准的 `/config && make && make install`。

一旦安装了 OpenSSL 和 Stunnel 软件包，仅剩最后三个步骤。

- 1. 创建新证书和私钥

```
root /usr/bin/openssl req -new -x509 -days 365 -nodes \ -config /usr/share/doc/packages/stunnel.conf \ -out /etc/stunnel.pem -keyout /etc/stunnel.pem
```

这一步将提出几个问题以生成证书。这些问题是自言自明的，例如，“您所在的国家是哪个？”以及“您的主机的完全限定域名是什么？”

- 2. 从 `[x]inetd` 中移除 swat 条目

- 3. 启动 stunnel 服务器，如下所示

```
root stunnel -p /etc/stunnel/stunnel.pem \ -d 901 -1 /usr/local/samba/bin/swat swat
```

应该可以将您选择的 Web 浏览器连接到 `https://<swathost>:901/` 并享受服务。

# Samba 与 SSL

许多网络协议（如 NFS）在设计时并未考虑安全性，尽管它们在校园网内部广泛使用。由于这些协议，许多网络连接是脆弱的。Samba 包含了对 SSL 的支持，许多中间人攻击可以通过使用加密工具来被阻的的。

如果你需要在 Samba 中启用 SSL，请遵循以下步骤：

- 1. 为配置脚本指定 `--with-ssl` 选项。

- 2. 使用标准的 `make` 编译安装 Samba。

- 3. 阅读 Samba-HOWTO。

关于 SSL、公钥加密的更多信息，Bruce Schneier 的著作《加密》（Applied Cryptography）是一个优秀的资源。

## 安全提示

网络安全通常分层实施。其中最重要的组件之一是“将外部排除”层。假设我们知道只有内部主机应该连接服务器。
