

本地配置信息和 NIS 源信息。）NIS 服务器可以根据需要包含以下多个源文件中的信息：

-   `/etc/group` 定义组及其成员
-   `/etc/gshadow` 提供组的影子密码
-   `/etc/hosts` 映射本地系统和 IP 地址
-   `/etc/passwd` 列出用户信息
-   `/etc/printcap` 列出打印机信息
-   `/etc/rpc` 映射 RPC 程序名称和编号
-   `/etc/services` 映射系统服务名称和端口号
-   `/etc/shadow` 提供用户的影子密码

NIS 提供的信息基于那些时常变化的文件。NIS 负责及时将更新后的信息提供给 NIS 域中的所有系统。

在 NIS 能够存储源文件中包含的信息之前，必须将其转换为一种称为 map 的 dbm 格式文件（参见第 1144 页）。每个 map 都以一个字段（列）作为索引。可以通过指定索引字段的值来从 map 中检索记录（行）。某些文件会生成两个 map，每个 map 以不同的字段为索引。例如，`/etc/passwd` 文件会生成两个 map：一个按用户名索引，另一个按 UID 索引。这些 map 分别命名为 `passwd.byname` 和 `passwd.byuid`。

> NIS map 对应于 C 库函数。`getpwnam()` 和 `getpwuid()` 函数在非 NIS 系统上从 `/etc/passwd` 获取用户名和 UID 信息。在 NIS 系统上，这些函数通过 RPC 调用向 NIS 服务器发送请求，这个过程对于调用该函数的应用程序来说是透明的。

NIS 使用的 map 名称对应于主服务器 `/var/yp/nisdomainname` 目录中的文件，其中 `nisdomainname` 是 NIS 域的名称。本章中的示例使用名为 mgs 的 NIS 域：

```
$ ls /var/yp/mgs
group.byuid   netgroup.byhost  protocols.byname   services.by servicename
group.byname   netgroup.byuser  protocols.bynumber  shadow.byname
hosts.byaddr   netid.byname     rpc.byname         ypservers
hosts.byname   passwd.byname    rpc.bynumber
netgroup       passwd.byuid     services.byname
```

为了更容易引用 NIS map，你可以为其分配昵称。位于客户端和服务器上的 `/var/yp/nicknames` 文件保存了常用昵称的列表：

```
$ cat /var/yp/nicknames
    passwd          passwd.byname
    group           group.byname
    networks        networks.byaddr
    hosts           hosts.byname
    protocols       protocols.bynumber
    services        services.byname
    aliases         mail.aliases
    ethers          ethers.byname
```

你还可以使用命令 `ypcat -x` 来显示昵称列表。**nicknames** 文件中的每一行包含一个昵称，后跟空白字符以及对应于该昵称的 map 名称。你可以通过更改 **nicknames** 文件来添加、删除或修改昵称。

`ypcat` 和 `ypmatch` 实用程序显示服务器 NIS map 中的信息。使用昵称 **passwd**，以下命令可以在本地域的任何 NIS 客户端上运行，用于显示 **passwd.byname** map 中包含的信息：

```
$ ypcat passwd
sam:x:1000:1000:Sam,,,:/home/sam:/bin/bash
sls:x:1001:1001:Sam the Great,,,:/home/sls:/bin/bash
...
```

默认情况下，NIS 仅存储 UID 大于或等于 1000 的用户的密码（参见第 753 页上的 **MINUID**）。因此，`ypcat` 不会显示 **root**、**bin** 和其他系统条目的行。你可以使用 `ypmatch` 显示单个用户的密码信息：

```
$ ypmatch sam passwd
sam:x:1000:1000:Sam,,,:/home/sam:/bin/bash
```

你可以通过将 `ypcat` 的输出通过 `grep` 进行过滤来获取相同的信息，但 `ypmatch` 效率更高，因为它直接搜索 map，并使用单个进程。`ypmatch` 实用程序仅针对 map 的键工作。要匹配组的成员或 map 中其他字段（例如 **passwd** 中的 **GECOS** 字段，参见第 1150 页）中的值，你需要使用 `ypcat` 和 `grep`：

```
$ ypcat passwd | grep -i great
sls:x:1001:1001:Sam the Great,,,:/home/sls:/bin/bash
```

本章使用以下定义：

-   **NIS 源文件** NIS 从中获取信息的 ASCII 文件
-   **NIS maps** 由 NIS 源文件创建的 dbm 格式文件
-   **NIS 数据库** NIS maps 的集合

## 更多信息

**本地** 手册页：**domainname**、**makedbm**、**netgroup**、**revnetgroup**、**ypbind**、**ypcat**、**ypinit**、**ypmatch**、**yppasswd**、**yppoll**、**yppush**、**ypset**、**ypservcr**、**ypserv.conf**、**ypwhich**、**ypxfr**、**ypxfrd**

**Web** www.linux-nis.org
*NIS-HOWTO*

## 运行 NIS 客户端

本节介绍如何在本地系统上设置 NIS 客户端。

### 先决条件

-   `nis`
-   `portmap`（随 nis 自动安装）

安装 **nis** 软件包时，**dpkg postinst** 脚本会启动一个 NIS 客户端。如果你想启动 NIS 服务器或不想启动 NIS 客户端，请参阅下面的“nis 初始化脚本”部分。如果在 `/etc/default/domain` 中找不到 NIS 域名称，**dpkg postinst** 脚本会要求你指定本地系统的 NIS 域名称。如有必要，脚本会创建该文件并将 NIS 域名称存储在该文件中。如果该文件不存在，NIS 客户端（ypbind）将不会启动。如果你指定的域有服务器，客户端会迅速绑定到该服务器。

如果安装或启动 NIS 客户端或启动系统时，没有可供 NIS 客户端绑定的 NIS 服务器，客户端将花费几分钟时间尝试查找服务器，在此期间显示以下消息：

```
Setting up nis (3.17-14ubuntu2) ...
* Setting NIS domainname to: mgs
* Starting NIS services
* binding to YP server...
* ...
* ...
```

最终，客户端（ypbind）放弃查找服务器，并在后台以广播模式运行：

```
$ ps -ef | grep ypbind
root        16832     1  0 19:33 ?          00:00:00 /usr/sbin/ypbind -broadcast
sam        17390  5839  0 19:38 pts/0      00:00:00 grep ypbind
```

广播模式比其他模式的安全性低，因为它通过广播请求服务器自我识别的方式，使系统暴露给流氓服务器。如果 ypbind 以此模式启动，建议在设置 NIS 服务器（参见第 750 页）并如下一节所述配置 NIS 客户端后重新启动它。

配置 **nis** 后，调用 nis 初始化脚本来重启 **nis**。但是，如前所述，如果无法连接到服务器，启动 **nis** 需要一些时间。`/etc/default/nis` 文件指定此脚本是启动 NIS 客户端、服务器还是两者：

```
$ sudo service nis restart
```

在活跃的服务器上的更改 **nis** 配置后，使用 **reload** 代替 **restart** 来重新加载 **nis** 配置文件，而不会干扰连接到服务器的客户端。

### 注意事项

如果本地系统的 NIS 域没有 NIS 服务器，你需要设置一个（参见第 750 页）。如果有 NIS 服务器，你需要知道系统所属的 NIS 域的名称，以及（可选地）一个或多个 NIS 域 NIS 服务器的名称或 IP 地址。

NIS 客户端可以与 NIS 服务器运行在同一系统上。

**/etc/default/nis** `/etc/default/nis` 文件控制本地系统上运行的 NIS 的多个方面，包括 nis 初始化脚本是启动客户端、服务器还是两者。默认安装时，此文件使 nis 初始化脚本启动 NIS 客户端（ypbind）而不启动 NIS 服务器（ypserv）。如果本地系统不是 NIS 服务器，请将 NISSERVER 设置为 *false*；如果是服务器，则根据情况设置为 *master* 或 *slave*。如果本地系统是一个 NIS 客户端，请将 NISCLIENT 设置为 *true*；否则设置为 *false*。

```
$ head /etc/default/nis

# Are we a NIS server and if so what kind (values: false, slave, master)?
NISSERVER=false

# Are we a NIS client?
NISCLIENT=true
```

在 nis 文件中，你还可以指定 NIS 服务器使用哪些端口（参见第 751 页的“防火墙”）以及用户可以修改 `/etc/passwd` 中的哪些值（参见第 757 页的“允许修改 GECOS 和登录 Shell”）。

## 配置 NIS 客户端

本节列出了设置和启动 NIS 客户端的步骤。

### /etc/defaultdomain：指定 NIS 域名称

**DNS 域名称与 NIS 域名称不同**

> DNS 域名称在整个互联网中用于指代一组系统。DNS 将这些名称映射到 IP 地址，以便系统之间能够相互通信。
> 
> NIS 域名称严格用于标识共享 NIS 服务器的系统，通常不被用户或其他程序看到或使用。虽然一些管理员使用一个名称同时作为 DNS 域名称和 NIS 域名称，但这种做法可能会降低安全性。

`/etc/defaultdomain` 文件存储本地系统所属 NIS 域的名称。如果更改此值，你需要重新加载客户端和/或服务器守护进程，以便 NIS 能够识别该更改。nis 初始化脚本读取 defaultdomain 文件并设置系统的 NIS 域名称。如果在安装 NIS 时 defaultdomain 文件不存在，dpkg postinst 脚本会提示你输入（参见第 745 页的“安装”）。你可以使用 nisdomainname 实用程序来设置或查看 NIS 域名称，但以此方式设置名称时，当 nis 初始化脚本执行时（例如，当系统重新启动时）不会保留该名称：

```
$ sudo nisdomainname
(none)
$ sudo nisdomainname mgs
$ sudo nisdomainname
mgs
```

![](img/2344fc4a798f29dca9e8b5ed7288171a_795_0.png)

![](img/2344fc4a798f29dca9e8b5ed7288171a_795_1.png)

![](img/2344fc4a798f29dca9e8b5ed7288171a_795_2.png)

