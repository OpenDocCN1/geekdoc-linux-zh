
在 `nis` 文件中，你还可以指定 NIS 服务器使用的端口（请参阅页第 751 页的“防火墙”）以及用户可以修改 `/etc/passwd` 中的哪些值（请参阅页第 757 页的“允许 GECOS 和登录 Shell 修改”）。

## 配置 NIS 客户端

本节列出了设置和运行 NIS 客户端的步骤。

### /etc/defaultdomain: 指定 NIS 域名称

DNS 域名与 NIS 域名不同。

- 提示：DNS 域名在整个互联网中用于指代一组系统。DNS 将这些名称映射到 IP 地址，以便系统之间能够通信。

NIS 域名专门用于标识 NIS 服务器可以识别的系统，并且通常由用户和其他程序查看或使用。虽然某些管理员将同一个名称既作为 DNS 域名又作为 NIS 域名，但这种做法会降低安全性。

`/etc/defaultdomain` 文件存储了本地系统所属的 NIS 域名称。如果你更改了此值，需要重新加载客户端和/或服务器以便让 NIS 识别该更改。`nis` 初始化脚本读取 `defaultdomain` 文件并设置系统 NIS 域的名称。如果在安装 NIS 时该文件不存在，`dpkg` 后置脚本会提示输入（请参阅页第 745 页的“安装”）。你可以使用 `nisdomainname` 工具来查看或显示 NIS 域名，但通过这种方式设置的在执行 `nis` 初始化脚本时不会保持该名称（例如，当系统重启时）：

```
$ sudo nisdomainname

(none)

$ sudo nisdomainname mgs

$ sudo nisdomainname

mgs
```

### 为了避免混淆，请使用 nisdomainname 而不是 nisdomainname

`domainname` 和 `nisdomainname` 工具的功能相同：它们用于显示或设置系统的 NIS 域名。当你同时处理 DNS 域名时，请使用 `nisdomainname` 以避免混淆。

### 你必须设置本地系统的 NIS 域名

如果不存在 `/etc/defaultdomain` 文件，NIS 服务器和客户端将不会启动。

### /etc/yp.conf: 指定 NIS 服务器

编辑 `/etc/yp.conf` 以指定一个或多个 NIS 服务器（主服务器和/或从服务器）。你可以使用三种格式之一来指定每个服务器：

- `domain nisdomain server server_name`
- `domain nisdomain broadcast`（不使用）
- `ypserver server_name`

其中 `nisdomain` 是本地（客户端）系统所属的 NIS 域名称，`server_name` 是本地系统查询的 NIS 服务器主机名。最好将 `server_name` 指定为 IP 地址或 `/etc/hosts` 中的主机名。如果你指定了一个需要 DNS 查找的主机名，NIS 将找不到该服务器。第二种格式将 `ypbind` 置于广播模式，安全性低于第一和第三种格式，因为它通过广播请求服务器自标识，从而将路由器暴露在风险之中。在 Ubuntu Linux 下，如果你没有指定 NIS 服务器，或者你指定的服务器不可用，NIS 客户端将在广播模式下运行。

以下是 `mgs` 域中客户端的简单 `yp.conf` 示例，其服务器位于 `192.168.0.10`：

```
$ cat /etc/yp.conf
domain mgs server 192.168.0.10
```

你可以使用多行来指定一个或多个域的服务器。为单个域指定多个服务器允许系统在当前服务器变慢或宕机时切换到另一个服务器。

当你指定了多个 NIS 域时，必须在启动 `ypbind` 之前设置系统的 NIS 域名，以便客户端查询正确的服务器。在运行 `ypbind` 脚本之前在 `/etc/defaultdomain` 中指定 NIS 域名可以解决此问题（第 746 页）。

## 测试设置

启动 `ypbind` 后，使用 `nisdomainname` 确保设置了正确的 NIS 名称。如果需要设置 NIS 域名，请参阅页第 746 页的 "/etc/defaultdomain: 指定 NIS 域名"。接下来使用 `ypwhich` 检查系统是否已配置连接到正确的服务器；该服务器的名称设置在 `/etc/yp.conf` 中（第 747 页）：

```
$ ypwhich
plum
```

## 第 21 章 NIS 和 LDAP

使用 `rpcinfo` 检查 NIS 服务器是否正在运行（将 `plum` 替换为 `ypwhich` 返回的服务器名称）：

```
$ rpcinfo -u plum pyserv
program 100004 version 1 ready and waiting
program 100004 version 2 ready and waiting
```

启动 `ypbind` 后，检查它是否已向 `portmap` 注册：

```
$ rpcinfo -u localhost ypbind
program 100004 version 1 ready and waiting
```

如果 `rpcinfo` 未报告 `ypbind` 正在运行，请停止 NIS 并调试：

以 root 权限运行可以更改任何用户的密码（root 或系统账户的密码）。如果 ypasswd 守护进程允许这些更改，用户也可以使用 ypasswd 修改其登录 shell 和 GECOS（第 150 页）信息。请参考第 757 页的“ypasswd: The NIS Password Update Daemon”，获取如何配置 ypasswd 以允许用户更改这些值的信息。使用 ypasswd 的 `-p` 选项更改密码，使用 `-f` 更改 GECOS 信息，使用 `-l` 更改登录 shell：

```
$ ypasswd -l
```

正在更改 plum 上 sam 的 NIS 账户信息。
输入密码：

要接受默认值，只需按回车。要使用系统默认 shell，请使用单词 "none"。
登录 shell [/bin/bash]: /bin/sh

plum 登录 shell 已更改。

```
$ ypmatch sam passwd
sam:x:1000:1000:,,:,/home/sam:/bin/sh
```

如果 ypasswd 不起且服务器系统正在运行防火墙，请参阅第 751 页的“Firewall”。

## 添加和删除用户

有多种方法从 NIS passwd map 中添加和删除用户。最简单的方法是保持 NIS 主服务器上的 `/etc/passwd` 文件与 passwd map 同步。你可以通过使用标准工具（如 `adduser` 和 `deluser` 或其图形界面对应）对 passwd 文件进行更改，然后运行 `ypinit`（第 755 页）来更新 map，保持这些文件的同步。

## 设置 NIS 服务器

本节解释了如何设置 NIS 服务器。

## 前提条件

安装：确定一个 NIS 域名（第 746 页）并安装以下软件包：

- `nis`
- `portmap`（随 nis 自动安装）

`nis` init 脚本：当你安装该包时，`dpkg` postinst 脚本会启动 NIS 客户端。请参阅第 745 页的“Install”获取有关启动服务器或两者的信息。`/etc/default/nis` 文件控制 NIS 服务器是作为主（master）还是从（slave）启动（第 746 页）。你可能还想指定 NIS 服务器和 ypasswdd 的端口（参见下一页“Firewall”）。配置服务器后，你可以使用 nis init 脚本启动、重启或重载它：

```
$ sudo service nis restart
```

## 注意事项

NIS 客户端可以在与 NIS 服务器相同的系统上运行。

每个域必须只有一个主服务器。

你可以在单个系统上运行多个 NIS 域服务器（用于不同的域）。

NIS 服务器为 `/var/py` 中列出的 NIS 域提供服务。为了系统安全，在禁用 NIS 服务器时从 `/var/py` 移除 maps 目录。

NIS 服务器 (`ypersver`) 和 NIS 密码守护进程 (`yppasswd`) 使用 `portmap`（第 462 页）来选择接受查询的端口。当服务如 ypserver 请求端口时，portmap 服务器会处理 1024 以下的随机未用端口。让 ypserver 和 yppasswd 使用随机端口号使得在 NIS 服务器上设置防火墙变得困难。你可以通过编辑 `/etc/default/nis` 中的 ypserver 和 ypasswd 选项行来指定端口（选择任何小于 1024 的未使用端口）：

防火墙

```
YPSERVERARGS='--port 114
YPPASSWDARGS='--port 112'
```

如果 NIS 服务器正在运行防火墙，请打开你指定的端口。使用 `gufw`（第 876 页），通过设置两个策略来打开这些端口：一个允许服务于这些端口的。如果你遵循前面的示例，请允许在端口 114 和 112 上运行服务。

## 配置 NIS 服务器

本节列出了设置和启动 NIS 服务器涉及的步骤。

### /etc/default/nis: 允许 NIS 服务器启动

按照第 746 页的描述编辑 `/etc/default/nis` 文件，以便 nis init 脚本启动 NIS 服务器。你也可以在该文件中指定供 NIS 服务器和 yppasswd 监听的端口；请参考上文“Firewall”。

## 指定系统的 NIS 域名

按照第 746 页的说明指定系统的 NIS 域名。此步在安装 nis 软件包时会自动完成。

### /etc/ypserv.conf: 配置 NIS 服务器

`/etc/ypserv.conf` 文件保存了 NIS 服务器配置信息，指定了选项和访问规则。选项规则指定服务器选项并具有以下格式：

`option: value`

# 752 第 21 章 NIS 和 LDAP

# 选项

以下是选项及其默认值的列表：

- `files`: 指定 ypserv 缓存的 map 文件最大数量。设置为 0 可关闭缓存。默认值为 30。
- `trusted_master`: 在从服务器上，主服务器的名称/IP 地址，从服务器从此处接受新 map。默认没有主服务器，意味着不接受新 map。
- `xfer_check_port`: YES（默认）要求主服务器运行在特权端口上（第 1166 页）。NO 允许运行在任何端口。

## 访问规则

访问规则指定哪些主机和域可以访问哪些 map，具有以下格式：

```
domain:map:security
```

其中 host 和 domain 指定该规则适用的 IP 地址和 NIS 域；map 是 map 的名称；security 为 (allow）（允许）、(port）（端口）或 (deny）（拒绝）。

以下行出现在 `/ypserv.conf` 中：

```
domain:map:security
```

其中 host 和 domain 指定该规则适用的 IP 地址和 NIS 域；map 是 map 的名称；security 为 (allow)、(port) 或 (deny)。

### /var/yp/securenets: 增强安全性

为了增强系统安全性，你可以创建 secureets 文件，防止未经授权的系统获取 shadow map。当 secureets 不存在或为空时，NIS 接受任何系统的请求。

secureets 的每行列出网络掩码和 IP 地址。NIS 接受来自 secureets 指定系统的请求；它忽略其他地址。你必须在 secureets 中包含（本地）服务器 localhost (127.0.0.1)。一个简单的 secureets 文件如下：

```
$ /var/yp/securenets
# 你必须接受来自 localhost 的请求
255.255.255.255      127.0.0.1

# # 接受来自 IP 地址 192.168.0.1 的请求
255.255.255.192      192.168.0.0

# # 接受来自以 192.168.14 开头的 IP 地址的请求
255.255.255.0        192.168.14.0
```
