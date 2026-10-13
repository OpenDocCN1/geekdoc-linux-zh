
通常情况下，每个系统都有其各自文件的副本，任何更改都必须单独地更新每个系统上的文件。使用 NIS，你可以在 NIS 服务器上为一组计算机维护一套配置文件。所有其他运行 NIS 客户端的计算机都可以访问这些文件。例如，如果你的用户名和密码在 NIS 密码数据库中，你将能够登录到网络上所有运行 NIS 客户端的计算机。

NIS 服务器位于 `ipserv` RPM 包中，它是 Fedora 中 `Network Services` 组的一部分。默认不安装 `ipserv`。要安装它，请使用包管理 GUI 工具（桌面：System Settings：Add/Remove Applications，点击 Network Services 包组中的 Details，并选择 `ipserv`）。

NIS 最初被名为 Sun Yellow Pages (YP)，但“Yellow Pages”（黄页）名称是英国电信（British Telecom）在英国的注册商标，因此太阳微系统不得不更改名称。然而，许多 NIS 命令、NIS 包名都以 `yp` 字母开头。

如果你想在网络中使用 NIS，必须至少设置一个 NIS 服务器。你可以在网络中拥有多个 NIS 服务器，拥有一个主 NIS 服务器和一或多个接收主服务器数据库副本的从服务器（slave servers）。主 NIS 服务器组支持一个 NIS 域或 YP 域。

主 NIS 服务器运行着 `ypbind`（它是 NIS 守护进程），它在数据库中维护共享信息（DBM 指的是数据库管理，一个维护键值对的函数库）。NIS 数据库是映射（maps）。你可以直接从配置文件创建这些映射——使用 `/etc/passwd`。

# 第 18 章：DNS 与 NIS

要交互式启动 `ybind`，请以 `root` 用户身份登录并输入以下命令：

```
service ybind start
```

如果您希望 `ybind` 在系统启动时启动，请以 `root` 用户身份登录并输入以下命令开启 `ybind`：

```
chconfig --add ybind
chconfig --level 35 ybind on
```

## 设置 NIS 服务器

要将您的 Linux 系统配置为 NIS 服务器，您应该首先将其配置为 NIS 客户端——设置 NIS 域名、配置 `/etc/yp.conf` 文件并配置 `ybind` 守护进程。（注意，在您拥有并运行 NIS 服务器之前，`ybind` 守护进程将无法工作。）完成客户端配置后，您就可以配置 NIS 服务器。这需要您执行以下任务：

- 使用 `ypinit` 创建 NIS 映射。
- 配置主服务器 `--ypserv`。
- 可选：配置一个或多个从 NIS 服务器。

接下来的两个章节将解释这些步骤：

### 创建 NIS 映射

NIS 映射的涉及使用 `makedm` 将文本文件（如 `/etc/passwd` 和 `/etc/group`）转换为 DBM 文件。映射的创建由 `/var/yp/Makefile` 控制，该文件可供 `make` 命令执行特定任务（有关 `make` 和 `Makefile` 的更多信息请参见第 23 章）。

您可以配置 NIS 服务器与 NIS 域内客户端共享的内容。您可以通过编辑 `/var/yp` 目录下的 `Makefile` 来实现。在文本编辑器中打开 `/var/yp/Makefile`，找到以 `all::` 开头的行。以下是 `Makefile` 的典型节录，显示了 `all` 行之前的注释：

```makefile
# 如果您不想构建这些映射中的某些项，可以随时从列表中将其注释掉。
all:
    passwd group hosts rpc services protocols mail \
    # netgroup shared publickey networks ethosts bootparams priccap \
    # amd.home.master.auto.home.local passwd.adjunct \
    # timezone locals metasks
```

正如注释行（以 `#` 开头的行所示所示，注释掉不需要构建的映射。在前面的示例中，最后三行中列出的映射将不会被构建。

接下来，您应该运行带有 `-m` 选项 `/usr/lib/yp/ypinit` 程序来生成 NIS 映射数据库。以下是该程序的示例会话：

```
/usr/lib/yp/ypinit -m
```

此时，您必须构建一个运行 NIS 服务器的主机列表。`localhost.localdomain` 已包含在 NIS 服务器主机列表中。请继续添加其他主机的名称，每行一个。完成列表后，输入 `<Ctrl-D>`。

```
next host to add: localhost.localdomain
ext host to add: <在此处按 Ctrl-D>
当前的 NIS 服务器列表如下：
```

localhost.localdomain

```

这是否正确？[y/n]: y
我们需要几分钟来构建数据库...
正在构建 /var/yp/admin/ypservers...
正在运行 /var/yp/Makefile...
gmake[1]: 进入目录 '/var/yp/admin'
正在更新 passwd...
... 已删除。

`/usr/lib/ypbind` 程序会自动选择您的主机作为 NIS 服务器，用于任何其他 NIS 服务器的提示。您可以一次添加一个服务器，完成后按 Ctrl-D。然后，您必须验证 NIS 服务器列表是否正确（输入 y）。之后，`make` 将配合 `/var/yp/Makefile` 运行并根据 `Makefile` 中 `Make` 行指定的生成映射。映射文件存储在 `/var/yp` 的子目录下，该目录名称与您之前为服务器设置的 NIS 域名相同。例如，对于 NIS 域名，映射文件位于 `/var/yp/admin` 目录。

### 配置主 NIS 服务器

要配置 NIS 服务器守护进程 `ypserver`，您必须准备配置文件 `etc/ypserver.conf`。您可以通过阅读其 man 页来了解文件语法，通过输入命令 `ypserver.conf` 可以访问它。在其他选项中，您可以使用以下选项指定不要使用 DNS 来查找 `/etc/hosts` 文件映射中不存在的主机名：

```
dns: no
```

您可以在 `/etc/ypserver.conf` 中添加其他行来指定访问规则——主机可以访问映射。访问规则的格式如下：

`Host : Domain : Map : Security`

`field_to_mangle` 字段是可选的；它指示映射文件中的哪个字段应该被管理（默认是第二个字段，因为密码位于大多数文件（如 `/etc/passwd`）的第二个字段中）。混淆（mangle）一个字段是指如果请求来自非特权主机，将其替换为 x。其余字段具有以下含义：

- Host: IP 地址或通配符 (`*`)，表示规则适用于谁。
- Domain: 域名或通配符 (`*`)，表示规则适用于谁。
- Map: 规则适用的映射名称（映射名称与 `/var/yp/domainname` 目录下的映射文件名称相同，其中 `domainname` 是您的 NIS 域名）。
- **Security:** 以下内容之一：`none`（始终允许访问）、`deny`（拒绝访问）或 `secure`（需要身份验证）。

例如，对于 NIS 域名，映射文件位于：
`192.168.1.1 : * : passwd : none`
`192.168.1.1 : * : group : none`

# 第三部分：Linux 网络化

## 配置从服务器

要设置从 NIS 服务器，您需要配置 `/etc/ypbind.conf` 文件指向主服务器。文件的格式为：

```
server 192.168.1.1
```

配置完成后，您可以在从服务器上启动 `ybind` 守护进程：

```
service ybind start
```

## 测试 NIS

如果没有主服务器，请先执行客户端配置，然后按照前面的章节启动主服务器。接下来，如下所示启动 `ybind` 守护进程：

```
service ybind start
```

现在，您可以尝试各种客户端程序以确保一切正常。服务器和客户端使用远程调用（RPC）交换信息。网络文件系统（NFS，见第 19 章）也使用 RPC。`portmap` 服务将 RPC 服务映射到端口。当服务器启动时，它会向 `portmap` 注册。您的 Linux 系统应该已经运行 `portmap`。您可以使用以下命令检查：

```
ps ax | grep portmap
1856 ? S 0:00 portmap
3199 pts/3 S+ 0:00 grep portmap
```
