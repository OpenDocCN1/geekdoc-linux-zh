
如果 `yppasswdd` 守护进程配置为允许这些更改，请更改其登录 shell 和 GECOS（第 1084 页）信息。有关如何配置 `yppasswdd` 以允许用户更改这些字段的信息，请参阅第 709 页的“yppasswdd：NIS 密码更新守护进程”。使用 `yppasswd` 的 `-l` 选项来更改登录 shell。使用 `-f` 来更改 GECOS 信息：

```
$ yppasswd -f
  Changing NIS account information for mark on localhost.
  Please enter password:
  Changing full name for mark on localhost.
  To accept the default, simply press return. To enter an empty field, type the word "none".
  Name [MSobe11]: Mark G Sobe11
  Location []: SF
  Office Phone []:
  Home Phone []:
  The GECOS information has been changed on localhost.

  $ ypmatch mark passwd
  mark:$1$X49qrFYv/:500:500:Mark G Sobe11,SF:/home/mark:/bin/bash
```

## 添加和删除用户

有多种方法可以从 NIS passwd 映射中添加和删除用户。最简单的方法是保持 NIS 主服务器上的 `/etc/passwd` 文件与 passwd 映射同步。您也可以通过使用标准工具（如 `passwd`）修改 passwd 文件并运行 `yppinit` 来更新映射（第 708 页）来保持这些文件同步。

## 设置 NIS 服务器

本节讨论如何设置 NIS 服务器。

### 先决条件

确定 NIS 域名。一些站点将 DNS 域名用作 NIS 域名。选择不同的名称会更安全。

安装以下软件包：

- `ypserv`

运行 `chkconfig` 以便当系统进入多用户模式时启动 `ypserv`：

```
# /sbin/chkconfig ypserv on
```

仅在主要服务器上，运行 `chkconfig` 以便当系统进入多用户模式时启动映射服务器 `ypxfrd`（第 708 页）：

```
# /sbin/chkconfig ypxfrd on
```

此外，仅在主要服务器上，运行 `chkconfig` 以便当系统进入多用户模式时启动 NIS 密码更新守护进程 `yppasswdd`（第 709 页）：

```
# /sbin/chkconfig yppasswdd on
```

配置 `ypserv` 后，使用 `ypserv` 初始化脚本启动它：

```
# /sbin/service ypserv start
Starting YP server services:                    [  OK  ]
```

接下来，在运行主要服务器的系统上启动 `ypxfrd` 守护进程（第 708 页）：

```
# /sbin/service ypxfrd start
Starting YP map server:                       [  OK  ]
```

现在，在主要服务器上启动 `yppasswdd` 守护进程（第 709 页）：

```
# /sbin/service yppasswdd start
Starting YP passwd service:                   [  OK  ]
```

#### 注意事项

- NIS 客户端可以与 NIS 服务器运行在同一个系统上。
- 每个域必须只有一个主要服务器。
- 您可以在单个系统上运行多个 NIS 域服务器（针对不同的域）。
- NIS 服务器为 `/var/yp` 中列出的 NIS 域提供服务。为了系统更安全，在禁用 NIS 服务器时，请从 `/var/yp` 中移除映射目录。
- 当 SELinux 设置为使用定向策略时，NIS 受到 SELinux 的保护。如有必要，您可以禁用此保护。更多信息请参阅第 416 页的“使用 system-config-selinux 设置定向策略”。

### 逐步设置

本节列出了设置和启动 NIS 服务器所涉及的步骤。

#### 指定系统的 NIS 域名

通过在 `/etc/sysconfig/network` 文件中添加以下行来指定系统的 NIS 域名：

```bash
NISDOMAIN=nisdomainname
```

其中 *nisdomainname* 是本地系统所属 NIS 域的名称。更多信息请参阅第 699 页的“指定系统的 NIS 域名”。

#### 编辑 /etc/ypserv.conf 以配置 NIS 服务器

包含 NIS 服务器配置信息的 `/etc/ypserv.conf` 文件指定了选项和访问规则。选项规则指定服务器选项，并具有以下格式：

```bash
option: value
```

#### 选项

以下是*选项*及其默认*值*的列表：

| 选项 | 描述 |
| :--- | :--- |
| `files` | 指定 *ypserv* 缓存的最大映射文件数。设置为 0 可关闭缓存。默认为 30。 |
| `trusted_master` | 在从属服务器上，新映射将接受来自哪个主要服务器的名称/IP 地址。默认没有主要服务器，这意味着不接受新映射。 |
| `xfer_check_port` | `YES`（默认）要求主要服务器在*特权端口*上运行（第 1100 页）。`NO` 允许它在任何端口上运行。 |

#### 访问规则

指定哪些主机和域可以访问哪些映射的访问规则，具有以下格式：

> *host*:*domain*:*map*:*security*

其中 *host* 和 *domain* 指定该规则适用的 IP 地址和 NIS 域；*map* 是该规则适用的映射名称；*security* 为 **none**（始终允许访问）、**port**（允许从特权端口访问）或 **deny**（从不允许访问）。

Fedora/RHEL 提供的 *ypserv.conf* 文件中包含以下行：

```
$ cat /etc/ypserv.conf
# Not everybody should see the shadow passwords, not secure, since
# under MSDOS everybody is root and can access ports < 1024 !!!
*       : *        : shadow.byname : port
: *      : passwd.adjunct.byname : port
```

这些行将 *shadow.byname* 和 *passwd.adjunct.byname*（带有 shadow [星号] 条目的 *passwd* 映射）映射限制为只能从编号小于 1024 的端口访问。然而，正如注释所指出的，网络中任何使用 DOS 或早期 Windows 系统的人都可以读取这些映射，因为他们可以访问编号小于 1024 的端口。

以下示例描述了一个 LAN，其中有一些地址您希望授予 NIS 访问权限，而有些则不希望；也许您有一个无线段或一些公共网络连接，您不希望暴露给 NIS。您可以在 *ypserv.conf* 中列出您希望授予访问权限的系统或 IP 子网。然后，从其他 IP 地址登录的任何人都将被拒绝 NIS 服务。*ypserv.conf* 中的以下行授予从 192.168.0.1 到 192.168.0.255 范围内的 IP 地址登录的任何人的访问权限（指定为 192.168.0.1，子网掩码 [第 443 页] 为 /24）：

```
$ cat /etc/ypserv.conf
192.168.0.1/24 : * : * : none
```

#### 创建 /var/yp/securenets 以增强安全性

为了增强系统安全性，创建 `/var/yp/securenets` 文件，该文件可防止未经授权的向 NIS 服务器发送 RPC 请求并获取 NIS 映射。值得注意的是，**securenets** 可以防止未经授权的用户获取包含加密密码的 **shadow** 映射。当 **securenets** 不存在或为*空*时，NIS 服务器接受来自任何系统的请求。

**securenets** 的每一行列出一个 netmask 和 IP 地址。NIS 接受来自 **securenets** 中指定的 IP 地址系统的请求，并忽略并记录来自其他地址的请求。您必须在 **securenets** 中包括（本地）服务器系统作为 **localhost** (127.0.0.1)。一个简单的 **securenets** 文件如下：

```
$ cat /var/yp/securenets
# you must accept requests from localhost
255.255.255.255           127.0.0.1
#
# accept requests from IP addresses 192.168.0.1 - 192.168.0.62
255.255.255.192           192.168.0.0
#
# accept requests from IP addresses starting with 192.168.14
255.255.255.0             192.168.14.0
```

#### 编辑 /var/yp/Makefile 以指定映射

*make* 实用程序由 `/var/yp/Makefile` 控制，使用 *makedb* 创建 NIS 映射，这些映射包含 NIS 分发的信息。当您在主要服务器上运行 *ypinit* 时，*ypinit* 会调用 *make*：您不需要手动运行 *make*。编辑 `/var/yp/Makefile` 以设置选项并指定要创建哪些映射。以下部分详细讨论 `/var/yp/Makefile`。

#### 变量

以下是您可以在 `/var/yp/Makefile` 中设置的变量列表。Fedora/RHEL 后面的值是该文件中 Fedora/RHEL 分发的值。

- **B**: 请勿更改。Fedora/RHEL：未设置
- **NOPUSH**: 指定 *yperserv* 不应将映射复制（推送）到从属服务器。如果您没有任何从属 NIS 服务器，则设置为 TRUE；设置为 FALSE 以促使 NIS 将映射复制到从属服务器。Fedora/RHEL：TRUE
- **MINUID, MINGID**: 指定要包含在 NIS 映射中的最低 UID 和 GID 号。在 `/etc/passwd` 和 `/etc/group` 文件中，较低的 ID 号属于 **root** 以及系统账户和组。为了增强安全性，NIS 不分发关于这些用户和组的密码和组信息。将 MINUID 设置为要包含在 NIS 映射中的最低 UID 号，并将 MINGID 设置为要包含的最低 GID 号。Fedora/RHEL：500/500

