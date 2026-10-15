
### 配置 `/etc/passwd`

如果你在重新编译二进制文件之前进行 `make install`，执行 `make clean`。如果你想在其他地方安装二进制文件，需要修改 `Makefile`。

请阅读随包的 `README` 文件以获取更多信息。

通常在 `/etc/passwd` 中为 Slip hosts 创建登录。

拨入者将作为标准登录过程登录，输入其用户名和密码，但登录后不会显示 shell，而是执行 `sliplogin`。该程序会搜索其配置文件（`/etc/slip.hosts`），查找一个与拨入者登录名匹配的条目。如果找到该条目，它会将线路配置为 8 位纯净链路，并使用 `io` 调用将线路规律转换为 SLIP。当此过程完成后，将进行最后阶段的配置，此时 `sliplogin` 调用一个脚本，该脚本使用相关的 `ip`、子网掩码配置 SLIP 接口并设置适当的入路由。该脚本被称为 `/etc/slip.login`；或者类似于 `fred` 的方式，如果你确定某些用户需要特殊的初始化，那么你可以创建名为 `/etc/slip.login.loginname` 的配置脚本，它们将代替默认脚本为这些用户运行。

你需要配置四个文件才能让 `sliplogin` 工作。我将详细说明如何获取软件以及如何详细配置每个文件。文件如下：

- `/etc/passwd`：用于拨入用户账户。
- `/etc/slip.hosts`：包含每个拨入用户的特有信息。
- `/etc/slip.login`：管理需要为用户执行的路由配置。
- `/etc/slip.tty`：只有在你为服务器配置动态地址分配时才需要，它包含待分配的地址表。
- `/etc/slip.logout`：包含在用户挂断或注销后清理的命令。

获取 `sliplogin`：你可能已经作为发行版的一部分安装了 `slip` 包，但如果没有，可以从这里获取 `sliplogin`：ssite.unc.edu `<ftp://sunsite.unc.edu/pub/linux/system/Network/serial/sliplogin-2.1.1.tar.gz>`。该文件包含了源码、编译后的二进制文件和 man 手页。

为了确保只有授权用户能够运行 `sliplogin` 程序，你应该在 `/etc/group` 文件中添加一个类似下面的条目：

```
slip::13:user,fred
```

当程序安装 `sliplogin` 包时，`Makefile` 会将 `sliplogin` 程序的组所有权更改 `slip`，这意味着只有属于该组的用户才能执行它。上面的示例仅允许使用 `radio` 和 `fred` 的用户执行 `slip`。

要将二进制文件安装到 `/usr/src` 目录并将 man 手页安装到第 8，请执行以下操作：

```
# cd /usr/src
# gzip -dc .../sliplogin-2.1.1.tar.gz | tar xvf -
# cd sliplogin
# make
```

如果你想在重新编译二进制文件之前进行 `make install`，执行 `make clean`。如果你想在其他地方安装二进制文件，需要修改 `Makefile`。

请阅读随包的 `README` 文件以获取更多信息。

最常见的 slip 模式有：

`normal` 用于启用普通的未压缩 SLIP。

### 网络技术特定信息

#### 压缩

启用 Jacobsen 头部压缩 (cSLIP)

自然情况下，这些是互斥的，你可以使用其中一种。有关其他可用选项的更多信息，请参考 man 手页。

### 配置 `/etc/slip.login` 文件

当 `sliplogin` 搜索了 `/etc/slip.hosts` 并找到匹配的条目后，它将尝试执行 `/etc/slip.login` 文件，以用其 IP 地址和网络掩码实际配置 SLIP 接口。

`sliplogin` 软件包提供的 `/etc/slip.login` 示例所示：

```
#!/bin/sh -

#

@()slip.login 5.1 (Berkeley) 7/1/90

#

# 这是一个为 SLIP 线路准备的通用登录文件，sliplogin 用以下参数调用它：

# $1 $2 $3 $4, $5, $6 ...

# SLIPUnit tspeed pid 是来自 slip.host 条目的参数

#/sbin/ifconfig $1 5 pointpoint $6 mtu 1500 -trailers add

#/sbin/route add $6

ar -s $6 <hw_addr> pub

exit 0

#
```

你会注意到，此脚本使用 `ifconfig` 和 `route` 命令来用 IP 地址、远程 IP 地址和网络掩码配置 SLIP 设备，并创建一个通过 SLIP 设备到达远程地址的路由。这与你使用 `slant` 命令是一样的。

此外，请注意使用代理 ARP（Proxy ARP），以确保与服务器机器处于同一以太网的其它主机知道如何到达拨号入主机。`<hw_addr>` 字段应该是机器上以太网网的硬件地址。如果你的服务器机器不在以太网网络上，你可以完全省略此行。

### 配置 `/etc/slip.logout` 文件

当拨号断开时，你希望确保串口设备恢复到正常状态，以便以后的拨号者能够正确登录。这是通过使用 `/etc/slip.logout` 文件实现的。它的格式非常简单，并以与 `/etc/slip.login` 文件相同的参数被调用。

```
#!/bin/sh -

#

slip.logout

#

#/sbin/ifconfig $1 down

ar -d $6

exit 0

#
```

它所做的只是关闭（down）接口，这将删除之前创建的手动路由。它还使用 `arp` 命令删除任何设置的 arp 条目。再次，如果你的服务器机器没有以太网端口，你就不需要 `arp` 命令。

### 配置 `/etc/slip.tty` 文件

如果你使用动态 IP 地址分配（在 `/etc/slip.hosts` 文件中为任何主机配置了 `dynamic` 关键字），那么你必须配置 `/etc/slip.tty` 文件，列出哪些地址被分配给哪些端口。只有当你希望服务器为用户动态分配地址时，你才需要此文件。

该文件是一个表格，列出了支持拨号连接的 tty 设备以及分配给拨入该端口的用户的 IP 地址。

其格式如下：

```
# slip.tty tty-> IP 地址映射（用于动态 SLIP）
# 格式: /dev/tty?? xxx.xxx.xxx.xxx

/dev/ttyS0  192.168.0.100
/dev/ttyS1  192.168.0.101
```

此表的意思是，拨入端口 `/dev/ttyS0` 且在 `/etc/slip.hosts` 中其远程地址字段设置为 `dynamic` 的拨号者将被分配地址 `192.168.0.100`。

通过这种方式，你将为所有不需要专用服务器的用户每个端口仅分配一个地址。这有助于你将所需的地址数量减少到最低，以避免浪费。

### 使用 `dip` 的 SLIP 服务器

让我先说明一下，下面的某些信息来自 `dip` 手页，其中简要说明了如何运行 Linux 作为一个 slip 服务器。请同时注意，以下内容基于 `dip370-uri.lg` 软件包，可能不适用于 `dip` 的其他版本。

`dip` 有一种输入操作模式，在该模式会自动为调用它的用户创建一个条目，并根据它在 `/etc/diphosts` 文件中找到的信息将串口配置为 SLIP 链路。这种输入操作模式通过调用 `dip` 作为 `login` 来激活。因此，这就是你使用 `dip` 作为 SLIP 服务器的方法：通过创建以 `dip` 为登录 shell 的账户。

你可能需要的第一件事是建立如下符号链接：

```
# ln -sf /usr/sbin/dip /usr/sbin/login
```

然后你需要向你的 `/etc/passwd` 和 `/etc/diphosts` 文件中添加条目。你需要创建的条目格式如下：

要使用 `dip` 将 Linux 配置为 slip 服务器，你需要为用户创建一些特殊的 SLIP 账户，其中 `dip`（输入模式）是登录 shell。建议的习惯是让所有 SLIP 账户都以大字母 'S' 开头，例如 `Sfred`。

一个 SLIP 用户的 `/etc/passwd` 示例条目如下：

```
Sfred:ij/SMxTiVGCo:1004:10:Fred:/tmp:/usr/sbin/dip

|        |        |        |        |                | \__ 使用 login 作为登录 shell
主目录
用户全名
用户组 ID
用户 ID
加密密码
Slip 登录名
```
