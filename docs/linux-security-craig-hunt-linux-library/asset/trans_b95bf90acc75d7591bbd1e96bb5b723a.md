

| 指令 | 含义 |
| :--- | :--- |
| `ssl = [yes|no]` | 添加 SSL 支持。 |
| `ssl hosts = host1 host2 ..` | 必须始终使用 SSL 连接到此服务器的主机 |
| `ssl hosts resign = host1 host2 ..` | 不使用 SSL 连接到此服务器的主机 |
| `ssl CA certDir` | 证书目录位置 |
| `ssl CA certFile` | 包含所有证书的文件 |
| `ssl server cert` | 服务器证书的位置 |
| `ssl server key` | 服务器私钥的位置 |
| `ssl cyphers` | 在协议协商过程中使用的密码套件 |

使用上一节中创建 CA 密钥和证书的目录，以下 smb.conf 语法可以配置您的 Samba 服务器启用 SSL 支持：

```
[global]
ssl = yes
ssl hosts = 209.1.78.
ssl hosts resign = 209.1.78.1
ssl CA certFile = /etc/samba/CA/ca-cert.pem
ssl server cert = /etc/samba/CA/server-cert.pem
ssl server key = /etc/samba/CA/server-key.pem
```

在此示例中，您强制 209.1.78.0/24 网络上的所有 SSL 代理使用 SSL，除了 209.1.78.1 之外。请注意，虽然 `ssl CA certDir` 允许您在指定目录中拥有多个 CA 证书，但 `ssl CA certFile` 用于所有 CA 证书都在同一个物理文件中的情况。因为您只有一个 CA 证书（您自己的），所以这更适合您。同样的原理也适用于 `ssl server cert` 和 `ssl server key`。

### 下载和安装 SSL 代理

Object Development 的 SSL 代理程序包（其 Web 页面如图 8.6 所示）可以安装在您网络中某台 Linux 服务器上，该服务器将代理所有指向您的远程 Samba 服务器的 SMB 请求。您可以从 http://www.oddev.eu/Products/ssl\_proxy.html 下载 SSL 代理程序包。

#### 图 8.6 Object Development 的 SSL 代理 Web 页面

![](img/3258bbaf790525f8c4eb25fabff7844a_252_0.png)

只需向下滚动到页面底部，点击源包名称。一旦您将文件传输到主目录，请输入以下命令：

```python
[ramon]$ ls sslproxy_2000_Jan_29.tar
sslproxy.2000_Jan_29.tar
[ramon]$ gunzip sslproxy_2000_Jan_29.tar.gz
[ramon]$ tar xvf sslproxy_2000_Jan_29.tar
sslproxy.2000_Jan_29/
sslproxy.2000_Jan_29/Makefile
sslproxy.2000_Jan_29/README.txt
sslproxy.2000_Jan_29/dummyCert.pem
sslproxy.2000_Jan_29/sslproxy.c
sslproxy.2000_Jan_29/stdheaders.h
```

由于 SSL 代理以源代码形式提供，您必须使用包含的 Makefile 进行编译。然而，在这样做之前，请确保您已安装 `openssl-devel` RPM 软件包，这是 SSL 代理所必需的。该软件包包含用于编译应用程序的 OpenSSL 头文件和库。大多数发行版的标准安装中并不包含 `openssl-devel`，但您应该能够从您喜欢的 RPM 归档中获取最新版本。一旦您获得了 RPM 软件包，请使用以下命令将其安装在您的服务器上：

```
[ramon]$ sudo rpm -i openssl-devel-0.9.5a-14.1386.rpm
```

现在，您已准备好构建 SSL 代理可执行文件。请输入以下命令：

```
[ramon]$ cd sslproxy.2000_Jan_29
[ramon]$ make
gcc -Wall -I/usr/local/openssl/include -O -c sslproxy.c -o sslproxy.o
gcc -Wall -I/usr/local/openssl/include -O -o sslproxy sslproxy.o \
    -L/usr/local/openssl/lib -lssl -lcrypto
[ramon]$ sudo mv sslproxy /usr/sbin/
[ramon]$ sudo chown root:root /usr/sbin/sslproxy
[ramon]$ ls -1 /usr/sbin/sslproxy
-rwxr-xr-x 1 root root 28016 Dec 19 21:35 /usr/sbin/sslproxy
```

现在您已创建可执行文件 /usr/sbin/sslproxy，用于接受来自您的私有网络中 Windows 客户端的 SMB 请求，并通过 SSL 隧道将它们转发到公共网络中的远程 SMB 服务器。`sslproxy` 可执行文件接受表 8.2 中列出的命令行选项。

#### 表 8.2 sslproxy 命令行选项

| 选项 | 含义 |
| :--- | :--- |
| -h | 显示帮助信息。 |
| -L local-address | 代理应绑定的地址（默认为 0.0.0.0） |
| -l port | 代理应绑定的端口 |
| -R address | 要连接的远程 IP 地址 |
| -r port | 要连接的远程端口号 |
| -s | 作为服务器代理运行 |
| -n | 支持 NetBIOS |
| -p protocol | 要使用的协议：ssl23, ssl1, ssl3, 或 tls1（默认为 ssl23） |
| -c certificate | 使用以下证书 |
| -k keyfile | 使用以下私钥 |
| -v file | CA 证书的位置 |

要启动 SSL 代理服务，请输入以下命令：

```bash
[ramon]$ sudo sslproxy -l 139 -R tippecanoe -r 139 -s -n -c /etc/ssl/proxy-cert.pem -k /etc/proxy-key.pem
```

此命令监听端口 139 上的 SMB 请求，并通过 SSL 隧道将它们转发到主机名 `tippecanoe`（远程 SMB 服务器）。请注意，文件 `/etc/ssl/proxy-cert.pem` 和 `/etc/proxy-key.pem` 是您在上一节中创建的文件。只需将它们复制到代理的 `/etc` 目录中即可。

至此，本章已讨论了 SMB 客户端认证、对 SMB 请求应用访问控制的方方面面，甚至展示了如何保护穿越公共网络的 SMB 流量。为了结束关于 Samba 安全的话题，让我们来看看 Samba 的最新功能之一：它能够作为 Windows NT 域的主域控制器。

## 将 Samba 用作 Windows NT 主域控制器

上一节关于用户认证和访问控制讨论了允许 Samba 将一组客户端凭据传递给域控制器进行认证的功能。在 Windows NT 认证模型中，用户可以使用“域”认证登录到任何 NT 工作站，其中本地工作站依赖于一组域控制器来持有整个域的认证、访问控制和策略。被指定为主要认证者的 NT 主机称为*主域控制器*（PDC），而其下属则称为*备份域控制器*（BDC）。

Samba 不仅可以作为现有 NT PDC 的客户端；它实际上可以被配置为充当 PDC，并处理来自网络中 Windows NT 主机和其他 Samba 服务器的授权和访问控制请求。虽然本书撰写时的当前版本（2.0.7）提供实验性的 PDC 支持，但 2.1 版本（在您阅读本书时可能已发布）计划将其作为标准功能纳入。

> **注意**
> Samba 2.0.7 不支持 Windows 2000 登录。只有 Windows NT 3.51 SP5+ 和 4.0 SP4+ 机器才能向 Samba 的 PDC 进行认证。

Samba PDC 支持包括将新的 Windows NT 客户端机器添加到域中，并为这些机器上的用户提供域认证。可以使用“服务器管理器”和“用户管理器”工具分别在 Windows NT 主机上查看这些账户。Samba 允许远程更新机器和用户密码。支持功能列表中未包含的是在 Samba PDC 和另一个域控制器之间建立信任关系的能力，以及充当 BDC 的能力。

下一节将详细解释如何配置标准的 Samba 安装以充当 PDC。

## 设置 Samba PDC

首先，确保修改您的 `smb.conf` 文件中的 `[global]` 部分，以使用密码加密。您还需要使用 Samba PDC 启用域登录。以下示例中启用了这两项功能：

```
[global]
    encrypt passwords = yes
    workgroup = ACCOUNTING
    domain logons = yes
```

接下来，在 Samba 服务器上创建机器账户，以便它知道如何与 Windows NT 客户端主机交互。使用 NT 客户端的 NetBIOS 名称创建一个 `/etc/passwd` 条目，并在末尾添加 $。例如，以下条目是名为 `acct_server1` 的 NT 客户端的机器账户：

```text
acct_server1$:*:305:100:Accounting NT Server 1:/dev/null:~/bin/false
```

