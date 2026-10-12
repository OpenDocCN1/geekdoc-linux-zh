

- /etc/passwd — 定义在计算机上设置了账户的用户。
- /etc/shadow — 包含在 /etc/passwd 文件中设置的用户的加密密码。
- /etc/gshadow — 包含与 /etc/group 文件中包含的组相关的加密密码。（此文件是可选的，通常不使用。）
- /etc/passwd.adjunct — 如果系统不使用 shadow 密码，则保护密码条目。（此文件用于 SunOS 系统。）
- /etc/aliases — 包含用于电子邮件的用户别名。它允许发送到特定用户名的邮件被重定向到另一个用户（或一组用户）。在某些系统上，此文件可能是 /etc/mailaliases。
- /etc/ethers — 由 RARP 使用，将以太网地址映射为 IP 地址。此文件是可选的。（默认情况下，Fedora 中未配置 RARP 支持。）
- /etc/bootparams — 包含启动无盘工作站所需的条目（通常用于启动 Sun Microsystems 无盘工作站）。
- /etc/hosts — 包含可以在 TCP/IP 网络上访问的计算机的名称和 IP 地址。（通常用于包含私有 LAN 的所有地址，而 Internet 地址则通过 DNS 服务器确定。）
- /etc/networks — 用于为网络附加名称。这样，你可以按名称而非数字引用网络。
- /etc/printcap — 包含打印机定义。
- /etc/protocols — 标识分配给不同 Internet 网络协议（如 IP、TCP、UDP 及其他）的号码。
- /etc/publickey — 在某些 UNIX 系统上，用于包含用户名以及用于 NFS 和相关功能的安全网络通信的关联公钥和私钥。
- /etc/rpc — 包含支持的远程过程调用 (rpc) 协议的列表。这些协议与 Sun Microsystems UNIX 系统一起使用，以允许请求 NIS 等其他网络服务。
- /etc/services — 包含识别用于 Internet 协议的受支持网络服务的端口号和协议的列表。
- /etc/netgroup — 用于定义用户（来自特定主机和域），用于与远程挂载、远程 shell 和远程登录相关的权限检查。
- /etc/netid — 包含将 RPC 网络名称映射到 UNIX 凭据的信息。

> 注意：上面展示的一些文件可能不适用于你的 Fedora 系统。如果其中一些文件不存在，请不要担心。在设置系统（添加用户、配置网络等）的过程中，你会设置所需的文件。

尽管这些文件是在 /etc 目录中创建的，但 NIS 管理员可以将这些文件复制到不同的位置并进行更改，以免共享主 NIS 服务器的原始配置文件。NIS 管理员也可以选择将此列表中添加文件或删除文件。当配置 NIS 客户端计算机时，可以从 NIS 主服务器获取此配置信息。

### 将 Fedora 设置为 NIS 客户端

如果你的网络使用 NIS 集中管理用户、组、网络地址和其他信息，你可以将 Fedora 系统设置为 NIS 客户端，以便使用该信息。要配置 Fedora 作为 NIS 客户端，你需要从 NIS 管理员那里获取以下信息：

- **NIS 域名** — 这是一个用于描述使用公共 NIS 文件组的主机组的关键词。使用“域名”这个术语来指代这个关键词是不幸的，因为它与 TCP/IP 域名没有任何关系。它唯一的相似之处在于它指代一组计算机。
- **NIS 主服务器名称** — 这是你的网络上维护 NIS 数据库并响应来自该信息的网络请求的计算机的名称。
- **NIS 从服务器名称** — NIS 域可以拥有一个以上的 NIS 服务器，它们可以处理来自该域 NIS 数据库的信息请求。NIS 从服务器保存 NIS 映射的副本，以便在主 NIS 服务器故障时能够响应请求。（NIS 从服务器是可选的。）

安装 Fedora 时，如果你知道你的网络使用 NIS，你可能已选择 NIS 作为处理计算机上用户名和密码的方式。如果你尚未为计算机配置 NIS，以下程序将描述如何执行此操作。这些程序包括定义 NIS 域名，设置 /etc/yp.conf 文件，并配置 NIS 客户端守护进程（ypbind 和 ypwhich）在启动系统时启动。

### 定义 NIS 域名

你可以使用 **domainname** 命令设置 Fedora 计算机的 NIS 域名。例如，如果你的 NIS 域名是 *trident*，你可以以 root 用户身份在 shell 中键入以下内容来设置它：

```
# domainname trident
```

要验证 NIS 域名已设置，只需键入 **domainname**，你将看到该名称。不幸的是，你还没有完成。运行 **domainname** 不会永久设置 NIS 域名。一旦重新启动计算机，它就消失了。（你可以在重新启动后再次键入 **domainname** 来验证这一点。）

要使 NIS 域名永久化，你需要让 *domainname* 命令在每次系统启动时自动运行。有很多方法可以做到这一点。我所做的是将命令行（*domainname trident*）添加到一个在 *ypbind* 守护进程启动之前运行的运行级别脚本中。我编辑了 /etc/init.d/network 文件，并在第一组注释行（大约在第 9 行）之后添加了以下内容。

```
# 设置 NIS 域名。
domainname trident
```

这导致我的 Fedora 系统每次启动时都会设置我的 NIS 域名。添加此条目时，确保正确拼写 NIS 域名（包括大写字母和小写字母）。如果你稍微拼写错误，启动时你会看到 *ypbind* 失败消息。

> 警告：编辑运行级别脚本时要非常小心。编辑前请制作副本。如果你在这些文件中犯错，你可能会发现自己拥有不起作用的网络或其他基本服务。当你稍后升级系统时，你还有丢失此信息的风险。

### 设置 /etc/yp.conf 文件

*ypbind* 守护进程需要有关你的 NIS 域和 NIS 服务器的信息才能工作。这些信息在 /etc/yp.conf 文件中设置。前几个条目定义你的 NIS 域名和 NIS 服务器。例如，如果你有一个名为 *trident* 的 NIS 域和一个名为 *maple* 的主服务器，你在 /etc/yp.conf 文件中将有以下条目：

```
domain trident server maple
```

例如，如果你有名为 *oak* 和 *pine* 的其他从 NIS 服务器，你还可以有以下条目：

```
domain trident server oak
domain trident server pine
```

你还可以将计算机设置为向本地网络广播你的 NIS 服务器。例如，如果你的域名为 *trident*，你将按如下方式使用 domain/broadcast 选项：

```
domain trident broadcast
```

如果你的 NIS 服务器地址包含在 /etc/hosts 文件中，你可以指定 *ypbind* 在该文件中查找服务器的 IP 地址。例如，如果你的 NIS 主服务器名为 *maple*，你将添加以下条目：

```
ypserver maple
```

当 *ypbind* 启动时，读取此文件中的所有信息。然后，它被用于联系适当的 NIS 服务器。

一旦设置了所有 NIS 客户端信息，你只需要启动 ypbind 和 ypwhich 守护进程即可将 NIS 作为客户端运行。ypbind 守护进程作为两个进程连续运行：主 ypbind 进程处理来自 NIS 服务器的信息请求，从 ypbind 进程定期检查绑定。ypwhich 守护进程查找你的 NIS 主服务器。

启动这些守护进程相当简单。你可以设置名为 ypbind 的现有运行级别脚本，以便在启动时自动启动。为此，你可以运行以下命令（在 Terminal 窗口中以 root 用户身份）：

```
# chkconfig ypbind on
```

要立即启动 ypbind 守护进程，键入：

```
# /etc/init.d/ypbind start
```

> **交叉参考：** 有关运行级别脚本的更多信息，请参阅第 12 章。

### 检查 NIS 是否正常工作

要检查 NIS 客户端是否正在与 NIS 主服务器通信，请遵循本节中的说明。

> **注意：** 如果 NIS 服务器尚未配置，请参阅本章后面的“将 Fedora 设置为 NIS 主服务器”部分，配置 NIS 服务器。然后返回此过程，确保一切正常工作。

在 NIS 客户端计算机上，键入以下命令以确保你正在与 NIS 服务器通信：

```
# ypwhich
maple
```

这里显示的输出表明 NIS 客户端已绑定到名为 maple 的 NIS 服务器。接下来，使用 ypcat 命令检查映射是否正在共享。（要查看正在从 NIS 服务器共享哪些文件，请查看服务器的 /var/yp/nisdomain 目录，其中 nisdomain 由你的 NIS 域名替换。）键入该目录中显示的文件之一，并加上 ypcat 命令。这是一个例子：

```
# ypcat hosts
10.0.0.45		azh
10.0.0.46		pine
10.0.0.47		maple
```

如果你正在与 NIS 服务器通信并且能够访问映射文件，那么你现在可以定义 NIS 客户端使用哪些共享映射文件中的映射。

