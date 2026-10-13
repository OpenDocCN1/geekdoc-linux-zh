
**表6.1 续**

| 映射名称 | 描述 |
|---|---|
| `netgroup` | 包含以组名为键的netgroup信息 |
| `netgroup.byhost` | 包含以主机名为键的netgroup信息 |
| `netgroup.byuser` | 包含以用户名为键的netgroup信息 |
| `netid.byname` | 包含主机和用户的安全RPC网络名，以及它们的UID和GID |
| `netmasks.byaddr` | 包含IP子网所使用的网络掩码，以地址为键 |
| `networks.byaddr` | 包含命名空间中的网络名称和地址，以地址为键 |
| `networks.byname` | 包含命名空间中的网络名称和地址，以网络名为键 |
| `passwd.byname` | 包含以用户名为键的密码信息 |
| `passwd.byuid` | 包含以用户ID为键的密码信息 |
| `protocols.byname` | 列出所使用的网络协议 |
| `protocols.bynumber` | 列出以协议号为键的网络协议 |
| `publickey.byname` | 包含用于安全RPC的公钥和私钥 |
| `rpc.bynumber` | 列出已知的RPC程序名称和编号 |
| `services.byname` | 列出可用的互联网服务 |
| `ypservers` | 列出命名空间中所有NIS服务器及其IP地址 |

## 设置NIS主服务器

设置NIS主服务器包括三个基本步骤：

1. 设置NIS域名。
2. 填充NIS映射的配置文件。
3. 运行ypinit。

### 设置NIS域名

NIS网络通过域名来标识。一个NIS服务器服务于特定域，客户端配置为属于特定域，并使用该域的一个或多个服务器来处理其发出的任何NIS请求。

同一物理网络上可以存在不同的NIS域。每个域都有自己的NIS主服务器和一个或多个从服务器，各个客户端系统将配置为属于网络上的其中一个域。

每个域通过名称标识。通常，NIS域与DNS域名不同。域名使用`domainname`命令设置。该命令接受系统应加入的NIS域名。例如，如果你想将NIS域命名为`mydomain`，你需要执行以下命令，使你的主服务器成为`mydomain`域的服务器：

```bash
# /bin/domainname mydomain
```

### 填充NIS映射的配置文件

在NIS主服务器上，NIS映射是基于`/etc`目录中的标准Linux配置文件构建的。

- `/etc/passwd`：用户数据库
- `/etc/group`：组数据库
- `/etc/hosts`：主机到IP地址表
- `/etc/networks`：网络地址
- `/etc/services`：网络端口号和服务名称
- `/etc/protocols`：网络协议名称和编号
- `/etc/netgroup`：netgroup定义
- `/etc/rpc`：远程过程调用程序编号

按照正常方式配置这些文件，加入任何你想通过NIS传播到整个网络的数据。

### 运行ypinit

在填充了`/etc`中的配置文件之后，使用`ypinit`命令从这些文件生成必要的NIS映射。使用以下命令：

```bash
# /usr/lib/yp/ypinit -m
```

这将创建`/var/yp/<domainname>`目录，并使用`makedbm`生成dbm类型的数据库文件。每个NIS映射都会生成一对dbm文件。例如，对于`hosts.byname`映射，将有两个文件：`hosts.byname.dir`和`hosts.byname.pag`。此外，主机可以通过地址而不是名称进行查找，因此还会有一个`hosts.byaddr`映射，由`hosts.byaddr.dir`和`hosts.byaddr.pag`组成。同样地，在`/var/yp/<domainname>`目录中，还会为各种NIS映射创建其他dbm文件。

### 确保一切正常运行

在主服务器上设置好NIS后，你需要启动以下程序：

- `ypserv`
- `ypbind`
- `rpc.ypasswdd`
- `rpc.ypxfrd`

> **注意**
>
> `rpc.ypasswdd`是一个只在NIS主服务器上运行的程序，允许用户更改他们的NIS密码。`rpc.ypxfrd`也只在NIS主服务器上运行，可加速向NIS从服务器传输映射。

要启动`ypserv`和`ypbind`，请使用以下命令：

```bash
# /etc/rc.d/init.d/ypserv start
# /etc/rc.d/init.d/ypbind start
```

要启动`rpc.ypasswdd`，请使用此命令：

```bash
# /etc/rc.d/init.d/ypasswdd start
```

要启动`rpc.ypxfrd`，请使用此命令：

```bash
# /usr/sbin/rpc.ypxfrd
```

当系统重新启动时，这些程序将自动启动。在某些Linux系统上，`rpc.ypxfrd`可能未配置为在引导时启动，你需要编辑`/etc/rc.d/init.d/`中的脚本，以确保程序在系统启动时启动。有关启动过程及`/etc/rc.d/init.d/`中脚本的详细信息，请参阅第4章“启动和关闭Linux”。

## 设置NIS客户端

完成NIS主服务器的设置后，你可以配置NIS客户端，让主服务器处理NIS服务请求。配置NIS客户端需要以下三个步骤：

1. 在`/etc/yp.conf`文件中设置NIS域名
2. 运行`ypbind`
3. 编辑`/etc/passwd`文件

### 在`/etc/yp.conf`文件中设置NIS域名

在NIS客户端上，你在`/etc/yp.conf`文件中设置NIS域名。该文件由`ypbind`守护进程读取，它负责将你的NIS客户端连接到相应的NIS域。

- 在`yp.conf`文件中你有两个选择：
  - **配置ypbind守护进程广播寻找正确域名的NIS服务器：** 包含指令`domain domainname broadcast`。该指令表示客户端应连接到指定域名，并广播寻找服务器来处理请求。
  - **配置ypbind守护进程连接到特定的NIS服务器：** 包含指令`ypserver hostname`。该指令用于使用特定主机作为NIS服务器。主机名及其IP地址必须列在客户端的`/etc/hosts`中。

### 运行ypbind

在`/etc/yp.conf`中输入正确的配置后，你需要运行`ypbind`，将客户端绑定到NIS域。使用以下命令：

```sh
# /etc/rc.d/init.d/ypbind start
```

如果`ypbind`已经在你的系统上运行，你应当先停止`ypbind`，然后使用上述命令重新启动它。要停止`ypbind`，请使用以下命令：

```sh
# /etc/rc.d/init.d/ypbind stop
```

### 编辑`/etc/passwd`文件

当你的系统成为NIS网络的客户端后，你需要配置它，使其对NIS映射执行用户认证。为此，请在`/etc/passwd`文件末尾添加以下行：

```text
+::::::
```

加号告诉系统，对于本地`/etc/passwd`文件中未定义的用户名，将通过NIS进行查找。

但是，如果某个用户已经在本地`/etc/passwd`文件中有一个出现在+条目之前的条目，并且`/etc/nsswitch.conf`文件配置为先查阅本地密码文件、再查阅NIS数据库，那么该密码条目将覆盖NIS密码条目。关于`nsswitch.conf`文件的使用说明，请参阅“理解名称服务器开关”一节。

通常应避免密码文件覆盖，除非用户确实有充分理由在特定机器上拥有不同的UID、GID、主目录或本地密码。在单个机器上维护本地用户账户会产生NIS旨在避免的相同管理开销。

## 添加NIS从服务器

将系统配置为NIS从服务器需要两个步骤：

1. 设置NIS域名
2. 运行`ypinit`

### 设置NIS域名

域名使用`domainname`命令设置。该命令接受系统应加入的NIS域名。例如，如果你的主服务器已配置了NIS域`mydomain`，你需要执行以下命令，使你的从服务器成为`mydomain`域的一部分：

```bash
# /bin/domainname mydomain
```

### 运行ypinit

与主服务器一样，`ypinit`用于在你的NIS从服务器上初始化所有必需的文件。NIS从服务器上命令的格式为：

```bash
# /usr/lib/yp/ypinit -s masterhostname
```

其中`masterhostname`是NIS主服务器的主机名。该主机名及其IP地址必须存在于NIS从服务器的`/etc/hosts`文件中。

与使用`ypinit`创建主服务器时一样，从服务器上也会创建`/var/yp/<domainname>`目录。然后，NIS映射将从主服务器复制到从服务器的该目录中。

## 将NIS主服务器功能迁移到另一台机器

一旦你配置了担任主、从NIS服务器角色的机器，就没有直接简便的方法来更改这些角色。然而，有时有必要更换主服务器系统。

例如，如果你的NIS主服务器运行在一个需要升级或退役的旧系统上，你需要将主服务器服务迁移到新系统。

粗暴的方法是全新构建一个新的主服务器，然后重建所有从服务器。然而，这是一个耗时且不必要的过程。这个过程可以简化。

尽管如此，这并不像将从服务器提升为主服务器，或者构建一个新的主服务器然后要求所有从服务器开始接受新主服务器的NIS映射那样简单。
