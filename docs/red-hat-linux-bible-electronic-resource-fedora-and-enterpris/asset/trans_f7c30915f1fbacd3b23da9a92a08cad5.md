
## 定义 NIS 域名

你可以使用 `domainname` 命令设置你的 Red Hat Linux 计算机的 NIS 域名。例如，如果你的 NIS 域名是 *trident*，你可以通过以下命令以 root 用户从 shell 设置它：

```
# domainname trident
```

要验证你的 NIS 域名是否已设置，只需输入 `domainname`，你就会看到该名称。不幸的是，你还没有完成。运行 `domainname` 并不会永久设置 NIS 域名。一旦重启计算机，它就会消失。（你可以在重启后再次输入 `domainname` 来验证这一点。）

要使 NIS 域名永久生效，你需要在系统每次启动时自动运行 `domainname` 命令。有很多方法可以做到这一点。我所做的是将命令行（`domainname trident`）添加到在 `ypbind` 守护进程启动之前运行的运行级脚本中。我编辑了 `/etc/init.d/network` 文件，并在第一组注释行之后（大约第 9 行）添加了以下内容。

```
# Set the NIS domain name.
domainname trident
```

这样每次我的 Red Hat Linux 系统启动时，NIS 域名都会被设置。当你添加此条目时，请确保正确拼写 NIS 域名（包括大小写字母）。如果拼写稍有错误，启动时你会看到 `ypbind` 失败消息。

**警告：编辑运行级脚本时务必非常小心。编辑前请先备份。如果你在编辑这些文件时出现错误，你可能会发现网络或其他关键服务无法工作。你在日后升级系统时也可能丢失此信息。**

## 设置 /etc/yp.conf 文件

`ypbind` 守护进程需要有关你的 NIS 域和 NIS 服务器的信息才能工作。这些信息在你的 `/etc/yp.conf` 文件中设置。第一个条目定义你的 NIS 域名和 NIS 服务器。例如，如果你有一个名为 *trident* 的 NIS 域和一个名为 *maple* 的主服务器，你的 `/etc/yp.conf` 文件中会有以下条目：

```
domain trident server maple
```

如果你还有其他名为 *oak* 和 *pine* 的从属 NIS 服务器，例如，你也可以有以下条目：

```
domain trident server oak
domain trident server pine
```

你还可以将计算机设置为向本地网络广播以查找 NIS 服务器。例如，如果你的域名为 trident，你可以使用 domain/broadcast 选项如下：

```
domain trident broadcast
```

如果你的 NIS 服务器地址包含在 /etc/hosts 文件中，你可以指定 ypbind 在该文件中查找服务器的 IP 地址。例如，如果你的 NIS 主服务器名为 maple，你将添加以下条目：

```
ypserver maple
```

当 ypbind 启动时，会读取此文件中的所有信息。然后它被用来联系适当的 NIS 服务器。

## 配置 NIS 客户端守护进程

在你的 NIS 客户端信息全部设置好后，要以客户端身份运行 NIS，你需要做的就是启动 ypbind 和 ypwhich 守护进程。ypbind 守护进程作为两个进程持续运行：主 ypbind 进程处理来自你的 NIS 服务器的信息请求，而从 ypbind 进程会不时检查绑定。ypwhich 守护进程查找你的 NIS 主服务器。

启动这些守护进程非常容易。你可以设置一个名为 ypbind 的现有运行级脚本，使其在启动时自动启动。为此，你可以运行以下命令（以 root 用户从终端窗口）：

```
# chkconfig ypbind on
```

要立即启动 ypbind 守护进程，输入：

```
# /etc/init.d/ypbind start
```

> 交叉引用：有关运行级脚本的更多信息，请参阅第 12 章。

## 检查 NIS 是否正常工作

要检查你的 NIS 客户端是否正在与 NIS 主服务器通信，请按照本节中的说明操作。

> 注意：如果你的 NIS 服务器尚未配置，请参阅本章稍后的“设置 Red Hat Linux 作为 NIS 主服务器”部分来配置你的 NIS 服务器。然后返回此过程以确保一切正常工作。

从 NIS 客户端计算机，输入以下命令以确保你正在与 NIS 服务器通信：

```
# ypwhich
maple
```

上面显示的输出表明 NIS 客户端已绑定到名为 *maple* 的 NIS 服务器。接下来，使用 `ypcat` 命令检查映射是否正在共享。（要查看 NIS 服务器共享了哪些文件，请查看服务器的 `/var/yp/<nisdomain>` 目录，其中 *nisdomain* 用你的 NIS 域名替换。）输入该目录中显示的一个文件以及 `ypcat` 命令。这里有一个示例：

```
# ypcat hosts
10.0.0.45    ash
10.0.0.46    pine
10.0.0.47    maple
```

如果你正在与 NIS 服务器通信并且能够访问映射文件，现在你可以定义 NIS 客户端使用哪些共享映射文件。

## 使用 NIS 映射

为了使 NIS 服务器分发的信息能被 NIS 客户端使用，你必须配置 `/etc/nsswitch.conf` 文件，将 `nis` 包含在你想要使用的每个文件的搜索路径中。

以下是从 `/etc/nsswitch.conf` 文件中摘录的内容，显示了可用于访问不同配置文件搜索路径的有效值。

```
# Legal entries are:
#
#    nisplus or nis+        Use NIS+ (NIS version 3)
#    nis or yp              Use NIS (NIS version 2), also called YP
#    dns                    Use DNS (Domain Name Service)
#    files                  Use the local files
#    db                     Use the local database (.db) files
#    compat                 Use NIS on compat mode
#    hesiod                 Use Hesiod for user lookups
#    [NOTFOUND=return]     Stop searching if not found so far
#
```

对于我们的目的，我们希望将 `nis` 添加到我们希望从 NIS 服务器分发到此 NIS 客户端的文件路径中。在大多数情况下，只会检查本地文件（*files*）。以下是某些条目的示例：

```
passwd:        files
shadow:        files
group:         files
hosts:        files dns
```

对于这些条目中的每一个，首先检查原始文件（`/etc/passwd`、`/etc/shadow` 等）。对于主机名，会在本地 hosts 文件之后检查 DNS 服务器。对于我们的目的，我们可以添加 `nis` 来访问 NIS 服务器共享的映射。（Linux NIS 服务器仅实现 `nis` 而不是 `nisplus`。）然后这些行将如下所示：

passwd:     files nis
shadow:    files nis
group:     files nis
hosts:     files nis dns

一旦 /etc/nsswitch 文件被更改，NIS 映射中的数据即可访问。无需重启 NIS 服务。你可以更改 /etc/nsswitch 文件中列出的任何文件，以便配置系统访问共享的 NIS 映射。

## 设置 Red Hat Linux 作为 NIS 主服务器

要将你的 Red Hat Linux 系统配置为 NIS 主服务器，你应首先将其配置为 NIS 客户端（即，设置 NIS 域名，设置 /etc/yp.conf，并按前面所述配置客户端守护进程。）然后你创建 NIS 映射并配置 NIS 主服务器守护进程（ypserv 和 rpc.yppasswdd）。下一节将描述这些过程。

> **注意：** 如果你的 NIS 服务器上存在防火墙，你必须开放 UDP 端口 111（sunrpc），否则 NIS 客户端将无法连接到你的 NIS 服务。如果计算机也是路由器，尽可能阻止本地网络之外的对端口 111 的访问。

### 创建 NIS 映射

为了创建 NIS 映射使你的 Red Hat Linux 系统能够成为 NIS 主服务器，请以 root 用户从终端窗口开始进入 /var/yp 目录。在该目录中，一个 Makefile 使你能够配置与 NIS 共享哪些文件。默认共享的文件列在本章开头以及 Makefile 本身中。

#### 选择要映射的文件

如果你不想共享 Makefile 中设置的任何文件，可以阻止该文件被构建。方法是找到 Makefile 中的以下行并简单删除你想要排除的文件：

```makefile
all: passwd group hosts rpc services netid protocols mail \
    # netgrp shadow publickey networks ethers bootparams printcap \
    # amd.home auto.master auto.home auto.local passwd.adjunct \
    # timezone locale netmasks
```

你可能会注意到 all: 行中的并非所有名称都代表确切的文件名。例如，netgrp 并不是指 /etc/netgroup 文件。每个名称代表的文件在 Makefile 中 all: 行下方几行处列出。你可能还会注意到许多文件已被注释掉，包括 shadow 文件。
