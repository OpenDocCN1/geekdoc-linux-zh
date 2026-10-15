

## 指定共享文件

在网络上实际共享的文件列在 `all:` 条目中，该条目位于配置文件列表之后。只有部分定义的文件被列为共享，即在 `all:` 之后的第一行中列出的文件。其余行会被自动注释掉（前面加上 # 号）。你可以通过移除 # 号或将其条目移动到第一行来添加文件。

```
all: passwd group hosts rpc services netid protocols mail \
  # netgrp shadow publickey networks ethers bootparams printcap \
  # amd.home auto.master auto.home auto.local passwd.adjunct \
  # timezone locale netmasks
```

请务必不要修改 Makefile 的其余部分。

## 创建 NIS 数据库

然后你使用 `-m` 选项输入 `ypinit` 命令来创建由 NIS 配置文件组成的 NIS 数据库。你的 NIS 服务器将被检测到，然后你将被要求输入此 NIS 域中使用的任何从属 NIS 服务器的名称。如果有，请输入它们。完成后，按 CTRL-D。NIS 数据库文件随后将被创建。

```
ypinit -m
```

对于 NIS 从属服务器，你将使用

```
ypinit -s masterhost
```

如果收到以下错误，这很可能意味着你的 NIS 服务器未运行。请确保在运行 `ypinit` 之前启动 `ypserv`。

```
failed to send 'clear' to local ypserv: RPC: Program not registered
```

如果你以后需要更新 NIS 服务器文件，你需要切换到 `/var/yp` 目录并发出 `make` 命令。

```
cd /var/yp
```

```
make
```

## 控制访问

`/var/yp/secure` nets 文件启用主机访问你的 NIS 服务器。主机可以通过网络或单独引用。条目由子网掩码和 IP 地址组成。例如，你可以通过以下条目为本地网络中的所有主机提供访问权限：

```
255.255.255.0 192.168.1.0
```

对于单个主机，你可以使用掩码 255.255.255.255 或仅使用术语 "host"，如下所示：

```
host 192.168.1.4
```

控制不同主机访问 NIS 共享数据的方式在 `/etc/ypserv.conf` 中确定。

## Netgroups

你可以使用 NIS 设置 netgroups，这允许你创建用户网络级组。而普通组是在单独主机上本地创建的，NIS netgroup 可用于网络范围的服务。例如，你可以使用 NIS netgroups 控制对 NFS 文件系统的访问。Netgroups 在 `/etc/netgroup` 文件中定义。条目由 netgroup 名称后跟成员标识符组成，成员标识符由三个段组成：主机、用户和 NIS 域：

```
group  (host, user, NIS-domain) (host, user, NIS-domain) ...
```

例如，在 NIS 域 `myturtles.nis` 中，要定义一个名为 `myprojects` 的组，由主机 `rabbit` 上的用户 `chris` 和主机 `lizard.mytrek.com` 上的用户 `george` 组成，你将使用以下内容：

```
myprojects (rabbit, chris, myturtles.nis) \
            (lizard.mytrek.com, george, myturtles.nis)
```

空白段将匹配任何值。以下条目包含主机 `rabbit` 上的所有用户：

```
newgame (rabbit, , myturtles.nis)
```

如果你的组使用不需要用户或主机段，你可以使用连字符 `-` 消除其中一个或另一个。以下示例生成一个仅由主机名组成的 netgroup，没有用户名：

```
myservers (rabbit, -, ) (turtle.mytrek.com, -, )
```

然后你可以通过在 netgroup 名称前加上 @ 符号在各种配置文件中引用不同的 netgroup，如下所示：

```
@newgame
```

## NIS 客户端

要使主机在你的网络上使用 NIS，首先需要在该主机上指定你的 NIS 域名。此外，你的 NIS 客户端需要知道你的 NIS 服务器的名称。如果你已在已运行 NIS 的网络上安装了 Linux，你可能已在安装过程中输入了此信息。

## 指定 NIS 域和服务器

在 Red Hat 上，你可以使用 `authconfig-gtk` 工具指定你的 NIS 域名和服务器，你可以从系统设置窗口访问该工具。在该窗口中，选择身份验证。这将打开身份验证配置窗口。在用户信息面板上，单击配置 NIS 按钮以打开一个对话框，在其中可以输入 NIS 域的名称以及 NIS 服务器。务必也在用户信息面板上启用 NIS。NIS 域将保存在 `/etc/sysconfig/network` 文件中，而 NIS 服务器则保存在 `/etc/yp.conf` 文件中。

