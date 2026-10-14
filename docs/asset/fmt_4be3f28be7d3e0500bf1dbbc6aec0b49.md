
在网络术语中，`socket` 是两个进程之间的网络连接，这两个进程可能运行在相同或不同的进程上。从技术上讲，一个打开的 `socket` 有四个部分（源主机、源端口、目的主机、目的端口）。关闭的 `socket` 只有源端口和源主机。注意，`socket` 在连接的两端都有端口。当客户端尝试连接服务器时，它首先向系统请求一个空闲端口（一个未被任何程序使用的端口）。然后请求系统连接到目的主机和端口。这就是为什么相同主机之间可以有多个程序；例如，浏览器可以打开多个指向同一主机的窗口。系统跟踪源端口，并有不同的 `socket`。

### 配置网络

在每个现代 Linux 发行版中，基础网络配置在安装时完成。对于所有其他 UNIX 系统，所有配置数据都存储在 `/etc` 文件中。

# 网络与互联网服务

第二部分

需要考虑的一点是，Linux 与其他 UNIX 系统一样，可以动态重新配置。也就是说，几乎任何参数都可以在系统运行时更改而无需重启。对于重要的更改，建议重启。

# TCP/IP 与网络管理

第 7 章

- TCP（传输控制协议）
- UDP（用户数据agram协议）

# 图 7.2

路由器连接网络。

IP 是 TCP/IP 的最低公约数...

TCP 是 IP 之上的一个基于连接或面向流的协议...

![](img/cbac72550c7126a22162e94d91a0c360_208_2.png)

网络：10.0.2.0

子网掩码：255.255.255.0

广播地址：10.0.2.255

# 表 7.4 某些常用端口号

# Sockets

# 配置文件

本节介绍通过编辑存储在 `/etc` 中的文件进行静态网络配置。NIS 相关内容请参见第 14 节“NIS”。

Linux 系统中最重要的网络配置文件如下：

- `/etc/HOSTNAME`
- `/etc/hosts`
- `/etc/services`
- `/etc/host.conf`
- `/etc/nsswitch.conf`
- `/etc/resolv.conf`

下文将逐一介绍这些文件。所有这些文件都可以在系统运行时进行修改。修改将立即生效，无需启动或停止任何守护进程。请注意，这些文件中的大多数接受以井号（`#`）开头的注释。这些文件在 UNIX 手册的第 5 章中都有条目，因此你可以使用 `man` 命令来访问它们。

## 主机名: `/etc/HOSTNAME`

`/etc/HOSTNAME` 文件仅包含一行，即主机的主名称。因此，如果你的机器的完全限定域名（FQDN）为 `fooski.wiglerific.com`，那么你的 `/etc/HOSTNAME` 将包含单词 `foobski`。请注意，在 SuSE 下更改主机名的首选方法是使用 `YaST` 系统配置实用程序，它会自动为你更新此文件。此外，`YaST` 还会更改存储在 `/etc/rc.config` 和 `/etc/hosts` 中的完全限定域名。`YaST` 保证这些文件会同时用正确的信息进行更新。

## IP 地址与主机名之间的映射: `/etc/hosts`

`/etc/hosts` 文件包含了 IP 地址到主机名之间的映射，以及主机名的别名。IP 地址的设计是为了便于计算机读取，但人类很难记住它们。这正是在创建 `/etc/hosts` 文件的原因。以下是 `/etc/hosts` 文件的示例：

```
127.0.0.1       localhost
192.168.1.1     computer
192.168.1.2     server
192.168.1.3     router
192.168.3.45    othercomputer  otheralias
199.183.24.133   www.redhat.com
```

在这种情况下，`othercomputer` 还有一个别名。它也可以被称为 `aliases`。

在实践中，`/etc/hosts` 通常包含主机名、localhost 条目以及系统管理员常用的系统别名。其他主机名通常使用互联网的域名系统（DNS）进行解析。DNS 的客户端部分在 `/etc/resolv` 文件中配置。

尽管 `/etc/hosts` 中的主机名到 IP 地址的映射对于较小的网络非常方便，但对于较大的网络，通常建议使用替代系统（如第 8 节“DNS”中介绍的 DNS）。SuSE 未提供提供修改 `/etc/hosts` 文件内容的自动化方法，最好在更改主机名时对其进行修改。

## 端口号与服务名称之间的映射: `/etc/services`

`/etc/services` 文件包含了端口号与服务名称之间的映射，被多个系统程序使用。这是 SuSE 安装的默认 `/etc/services` 文件的开头：

```
tcpmux   1/tcp        # TCP port service multiplexer
echo      7/tcp
echo      7/udp
discard9/tcp        sink null
discard9/udp        sink null
sysstat 11/tcp      users
```

![](img/cbac72550c7126a22162e94d1a0c360_214_0.png)
