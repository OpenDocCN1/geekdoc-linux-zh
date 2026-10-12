

![](img/a7eec43a54473e95dc5ea333fecf1bd7_719_0.png)

要交互式启动 ypbind，请以 root 身份登录并输入以下命令：

```
service ypbind start
```

如果希望 ypbind 在系统启动时启动，请输入以下命令：

```
chkconfig --add ypbind
chkconfig --level 35 ypbind on
```

## 设置 NIS 服务器

将你的 Red Hat Linux 系统设置为 NIS 服务器，首先将其设置为 NIS 客户端——设置 NIS 域名，配置 /etc/yp.conf 文件，并配置 ypbind 守护进程。 （请注意，在你拥有正在运行的 NIS 服务器之前，ypbind 守护进程将无法工作。）客户端配置完成后，你可以配置 NIS 服务器。这需要你执行以下任务：

- 使用 ypinit 创建 NIS 映射。
- 配置主 NIS 服务器 — ypserv。
- 可选地，配置一个或多个从 NIS 服务器。

我将在接下来的两个部分中解释这些步骤。

### NIS 映射创建

创建 NIS 映射涉及使用 makedbm 将文本文件（如 /etc/passwd 和 /etc/group）转换为 DBM 文件。映射的创建由 /var/yp/Makefile 控制，该文件可由 make 命令使用以执行特定任务。

你可以配置 NIS 服务器希望与 NIS 域中的客户端共享的内容。你可以通过编辑 /var/yp 目录中的 Makefile 来实现。 在文本编辑器中打开 /var/yp/Makefile 并找到以 all: 开头的行。以下是 Makefile 的典型摘录，显示了 all: 行之前的注释：

```
# If you don't want some of these maps built, feel free to comment
# them out from this list.
all: passwd group hosts rpc services netid protocols mail \
# netgrp shadow publickey networks ethers bootparams printcap \
# amd_home auto_master auto_home auto_local passwd.adjunct \
# timezone locale netmasks
```

正如注释行（以 # 开头的行）所示，你可以注释掉任何不想构建的映射。在前面的示例中，最后三行中列出的映射将不会被构建。

接下来，编辑 /var/yp/secure nets 文件（如果不存在则创建新文件），以指定可以访问 NIS 映射的客户端计算机的 IP 地址。例如，要允许来自 localhost 和 192.168.0.0 网络中的主机的连接，请使用以下内容作为 /var/yp/secure nets 文件的内容：

```
# Always allow access for localhost
host 127.0.0.1
# allow connections from any host
# on the 192.168.0.0 network
255.255.255.0 192.168.0.0
```

最后一行仅允许 192.168.0.1 到 192.168.0.254 范围内的计算机访问 NIS 映射。

接下来，你应该通过使用 -m 选项运行 /usr/lib/yp/ypinit 程序来生成 NIS 映射数据库。以下是使用该程序的示例会话：

```
/usr/lib/yp/ypinit -m
```

该程序会询问你将运行 NIS 服务器的主机名称。它会自动选择你的主机作为 NIS 服务器，并提示输入任何其他 NIS 服务器的名称。你可以一次添加一个服务器名称，并在完成后按 Ctrl-D。然后你必须验证 NIS 服务器列表是否正确（输入 y）。之后，程序会根据 Makefile 中的 all: 行指定的内容生成 NIS 映射。映射文件存储在 /var/yp 的子目录中，该子目录的名称与你之前为系统设置的 NIS 域名相同。例如，对于 NIS 域 admin，映射文件位于 /var/yp/admin 目录中。

### 主 NIS 服务器配置

要配置 NIS 服务器守护进程 ypserv，你必须准备配置文件 /etc/ypserv.conf。你可以通过输入命令 man ypserv.conf 来了解此文件的语法。

你可以在 /etc/ypserv.conf 中添加指定访问规则的行——哪些主机可以访问哪些映射。访问规则的格式如下：

```
Host : Map : Security : mangle [: field_to_mangle]
```

field_to_mangle 是可选的；它指示映射文件中应被篡改的字段（默认为第二个字段，因为密码在大多数文件（如 /etc/passwd）的第二个字段中）。篡改一个字段是指如果请求来自非特权主机，则将其替换为 x。其余字段的含义如下：

- Host — IP 地址或通配符 (*)，表示规则适用于谁。
- Map — 规则适用的映射名称。（映射的名称与 /var/yp/domainname 目录中的映射文件相同，其中 domainname 是你的 NIS 域名。）
- Security — 以下之一：none（始终允许访问）；port（从小于 1024 的端口访问）；deny（拒绝访问映射）；或 des（需要 DES 身份验证）。
- mangle — 以下之一：yes（如果请求来自未经授权的主机，则应将 field_to_mangle 指定的字段替换为 x）或 no（不篡改）。

例如，/etc/ypserv.conf 文件中的以下行将对密码映射的访问限制为 192.168.0 网络中的系统：

```
192.168.0 : passwd.byname : port : yes
192.168.0 : passwd.byuid : port : yes
```

如果你未指定任何访问规则，ypserv 将允许所有计算机访问所有映射。

在设置好 /etc/ypserv.conf 文件后，你可以使用以下命令启动 NIS 服务器：

```
service ypserv start
```

为确保每次重新启动系统时 ypserv 都会启动，请输入以下命令启用它：

```
chkconfig --level 35 ypserv on
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_721_0.png)

为处理来自客户端的密码更改，你还必须在域的主 NIS 服务器上运行 rpc.yppasswd 服务器。rpc.yppasswd 服务器使客户端系统上的用户能够输入 yppasswd 命令并在 NIS 数据库中更改其密码。如果主 NIS 服务器上未运行 rpc.yppasswd 服务器，用户在输入 yppasswd 命令时将收到以下错误消息：

```
yppasswd: yppasswdd not running on NIS master host
```

为纠正此问题，以 root 身份登录并输入

```
service yppasswdd start
```

要在系统启动时自动启动 rpc.yppasswd，请输入

```
chkconfig --level 35 yppasswdd on
```

在主 NIS 服务器运行后，你可以使用各种 NIS 客户端程序（如 ypwhich、yppoll、ypcat 和 ypmatch）对其进行测试。

## 配置从 NIS 服务器

要将系统设置为从 NIS 服务器，首先将其设置为 NIS 客户端并验证客户端是否正常工作。特别是，输入 ypwhich -m 并查找 NIS 映射列表以及每个映射的主 NIS 服务器名称。（在下一节中，我将向你展示 ypwhich -m 命令的工作原理。）

在确认系统已配置为 NIS 客户端后，输入以下命令将系统设置为从 NIS 服务器：

/usr/lib/yp/ypinit -s nismaster

其中 nismaster 是该域的主 NIS 服务器的名称。

## 尝试使用 NIS

在网络中拥有主 NIS 服务器并且 ypbind 客户端正在运行后，你可以尝试各种 NIS 客户端程序和其他实用程序，以查看一切是否正常工作。

NIS 服务器和客户端使用远程过程调用（RPC）交换信息。RPC 需要 portmap 服务，该服务将 RPC 服务映射到 TCP 和 UDP 端口。当支持 RPC 的服务器启动时，它会向 portmap 注册并列出其支持的服务和使用的端口。你的 Red Hat Linux 系统应该已经运行了 portmap。你可以使用以下命令检查它：

```
ps ax | grep portmap
```

在输出中你应该看到显示 portmap 进程的行。例如，以下是该命令在 Red Hat Linux 系统上的输出：

```
525  ?  S  0:00 portmap
26222 pts/2  S  0:00 grep portmap
```

要查看 ypserv 和 ypbind 进程是否在主 NIS 服务器上运行，请输入以下命令：

```
rpcinfo -p
```

输出应显示 ypserv 和 ypbind 在最后一列中。

要确定系统正在使用哪个 NIS 服务器，请尝试 ypwhich 命令。以下是一个典型示例：

```
ypwhich
```
