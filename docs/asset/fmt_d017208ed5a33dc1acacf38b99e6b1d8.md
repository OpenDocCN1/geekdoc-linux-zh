
```
Anonymous login successful
Domain=[WORKGROUP] OS=[Unix] Server=[Samba 3.0.2a-Debian]

Sharename  Type  Comment
---------  ----  -------
IPC$         IPC
\\(Samba 3.0.2a-Debian)) IPC Service (knpxvm server
ADMINS       IPC
\\(Samba 3.0.2a-Debian)) IPC Service (knpxvm server
Anonymous login successful
Domain=[WORKGROUP] OS=[Unix] Server=[Samba 3.0.2a-Debian]

Server  Comment
------  -------
KNOPIX33  knpxvm server (Samba 3.0.2a-Debian)
WIDEBOXP

Workgroup  Master
---------  ------
WORKGROUP  KNOPIX33
```

`-L` 选项在功能上类似于在 Windows 服务器上使用的 `net view \\server` 命令。

当你在目标服务器上找到共享的名称后，可以很容易地将其挂载到 Linux 系统上。你可以从命令行挂载该共享，或者更好的做法是在 `/etc/fstab` 文件中添加一个条目，以便自动挂载。

以下是 `fstab` 条目的语法示例：

```
//server/share    /mnt/mtpt    smb    user=user    1 1
```

> 注意关于 `smbd` 和 `nmbd` 守护进程的问题，以及它们是否使用端口 139 和 NetBIOS 与 SMB/CIFS 客户端通信，还有 `smb.conf` 文件的各个部分。

## 域名系统

DNS 是网络上名称解析为 IP 地址的方式。正如你在第 17 章“基础网络”关于名称解析的讨论中所见，主机可以引用多个来源来解析它需要知道 IP 的名称。

在最简单的情况下，DNS 服务器提供从主机名到 IP 的名称解析，稍复杂一点的操作是确认某主机属于特定域名。

> 在 LPIC1 级别所需涉及的 DNS 信息并不多。在这种格式下，不可能对 DNS 涵盖的众多领域进行广泛讨论，因此我们将专注于基础内容以及一些可能会让你感到意外的领域。

### DNS 的组件

DNS 的主要组件包括 DNS 服务器守护进程 `named`、`/etc/named.conf` 文件（对于版本 2 及以上）或 `/etc/named.boot`（对于版本 4），以及定义区域或域名的区域文件。

通常，在安装发行版时会包含 Berkeley Internet Name Domain（BIND）软件包，或者至少在选择典型的服务器安装时会包含它。

典型的配置包括以下文件：

- **区域文件**——这些文件通常以区域名称和 `.db` 命名，例如 `example.db`，并将主机名映射到 IP。
- **反向区域文件**——这些文件的命名比较奇怪，由反转的网络地址后跟 `.in-addr.arpa` 组成。因此，`192.168.33.0` 网络的名称将是 `0.33.168.192.in-addr.arpa`，并包含从 IP 到主机名的反向映射。
- **named 配置文件**——根据版本不同，为 `/etc/named.conf` 或 `/etc/named.boot` 文件；这些包含 DNS 守护进程的参数，并指向正确的区域文件和提示文件。
- **提示文件**——这些文件包含根服务器信息，当服务器无法通过其数据或配置的服务器找到解析结果时，会参考此信息。

### DNS 服务器的类型

DNS 服务器主要有三种类型和功能：

- **主服务器（Master）**——某个域名或区域的权威服务器，它包含定义该域名的物理文件。
- **从服务器（Slave）**——用于为分布广泛的网络或主机提供负载均衡和名称解析，它只从主服务器接收区域。
- **缓存服务器（Cache）**——用于比其他服务器更长时间地缓存已解析的请求，它只能查询其他已配置的服务器。它本身没有区域或域名文件。

### named.* 文件

以下是两个文件的示例——BIND v4 的 `/etc/named.boot` 和 BIND v8 的 `/etc/named.conf`：

BIND v4 `/etc/named.boot` 文件示例：

```
############### bind configuration file
directory /usr/local/named
primary	somecoll.edu	db.somecoll
primary	33.168.192.in-addr.arpa	db.33.168.192
primary	0.0.127.in-addr.arpa	db.0.0.127
cache	db.cache
```

版本 4 文件简单直接，以注释开始，然后进入配置部分。

该文件中的行按顺序定义了以下内容：

- **directory**——包含以下行中提到的配置文件的目录。
- **primary**——第一个 `primary` 条目将该服务器定义为 `somecoll.edu` 域名的主服务器或主服务器；然后它引用了实际存储区域信息的区域文件（`db.somecoll.edu`）。
- **primary**——第二个 `primary` 条目定义了使用网络 `192.168.33.0` 的区域的反向查找。
- **primary**——最后一个 `primary` 条目定义了本地 `127.0.0.0` 反向查找区域，这是大多数配置的常见部分。
- **cache**——此条目定义服务器缓存存在，并命名为 `db.cache`。

当你知道文件的内容以及它的外观时，你就准备好与 v8 文件进行对比了。

以下是 BIND v8 `/etc/named.conf` 文件的示例：

```
// bind configuration file
options {
	directory "/usr/local/named";
};
zone "somecoll.edu" in {
	type master;
	file "db.somecoll";
}
zone "33.168.192.in-addr.arpa" in {
    type master;
    file "db.33.168.192";
}
zone "0.0.127.in-addr.arpa" in {
    type master;
    file "db.0.0.127";
}
```

BIND v8 文件更复杂，格式更多，看起来更像 C 或 C++ 源文件，而不是 v4 配置文件中的纯文本关键字/值条目。

为了避免让你进行逐行比较，简而言之，在 v4 文件中你会使用单行条目，而在 v8 文件中，使用由诸如 `options` 或 `zone` 这样的关键字定义块，并将一组参数完全包含在花括号中作为关键字的值。

![](img/49f4f38f3aec011238fa50f89e643db3_512_0.png)

> 在你的考试经验中，预计会看到这些文件中的一个，并有关于服务器角色以及区域可能服务的网络的各种问题。仔细检查示例将告诉你考试所需知道的一切，甚至更多。

### 区域和记录类型

*区域* 是一种类似于域名的组织单位。快速浏览各种类型的区域将帮助你确定服务器的角色：

- **主区域（Master）**——主区域包含将主机名解析为 IP 所需的信息，并被视为该域的权威。
- **从区域（Slave）**——从区域是主区域的副本或复制品，用于流量管理或负载均衡。它只能从主服务器接收区域信息，而不能更新主服务器。
- **转发（Forward）**——此区域类型简单地指向另一个服务器，通常是 ISP 或更高级别的企业 DNS 服务器以进行解析；它本身不进行任何解析。
- **提示（Hint）**——提示区域用于定位根服务器，以便本地服务器无法解析的查询可以得到解析。

BIND 使用几种资源记录类型。你最可能熟悉的是 A 记录，或地址记录，它只是主机名和 IP 记录。

最常见和有用的记录类型有：

- **SOA**——**权限起始**记录定义了区域，并设置了区域覆盖的域名或一组域名的部分。
- **NS**——名称服务器记录定义了哪些服务器负责哪些区域。
- **A**——地址记录是主机名到 IP 的映射。
- **PTR**——指针记录是 IP 到主机名的映射。
- **MX**——邮件交换器记录设置了用于电子邮件传输的 SMTP 连接应建立的服务器。
- **CNAME**——规范名称记录是一种简单的负载均衡方法；*www* 的多个 CNAME 记录应指向包含相同数据的不同主机，并在它们之间随机化。
- **TXT**——文本记录用于保存关于配置的笔记和评论。在区域文件之外没有其他含义。
