
### 10.1.2 Samba 原理

Samba 使用一组基于 `TCP/IP` 的 `SMB` (Server Message Block) 协议。该协议可以追溯到 20 世纪 80 年代，由英特、微软、`IBM`、施乐和 `3com` 公司联合发起，是在 `Linux`、`OS/2`、`Windows` 操作系统和 `Windows for Workgroups` 等计算机之间提供文件共享、打印机共享、域名映射、验证 (`Authentication`) 及浏览 (`Browsing`) 服务的网络通信协议。在早期，Samba 运行 `NBT` 协议 (`NetBIOS`) 在 `TCP/IP` 上，使用 `UDP` 协议的 `137`、`138` 和 `TCP` 协议的 `139` 端口，经过改进后，可以直接连接到 `TCP/IP` 协议上，没有额外的 `NAT` 层，使用 `TCP` 协议的 `445` 端口，通过 `SMB` 允许 `Linux` 服务器与 `Windows` 系统之间进行通信，跨平台的交互可以完成。

Samba 使用 `SMB API` 实现无方向的连接，该协议为 `Windows` 客户端和服务器提供了一个远程连接按照一种方式进行通信的。Samba 采用 C 模式，工作原理就是 Samba 与 `SMB` 协议运行在 `TCP/IP` 上，`Linux` 可以在 `Windows` 的局域网中访问。

Samba 的核心是两个守护进程，分别为 `samba` 和 `mbnd`。`samba` 是 `Linux` 服务器与 Samba 客户端之间的连接，验证用户身份并提供文件和打印机的访问，处理到来的 `SMB` 数据；`mbnd` 负责对外部缓存 Samba 服务器所提供的 `NetBIOS` 名称和浏览，使得 `Windows` 用户可以在“网络邻域”中找到 Samba 服务器共享的资源。

监控 `TCP139` (`NetBIOS over TCP/IP`) 端口和 `TCP445` (`SMB over TCP/CIFS`) 端口，监视 `UDP137` (`NetBIOS over UDP`) 端口和 `UDP138` (`NetBIOS over UDP`) 端口。

(1) 协议协商：当客户端访问 Samba 服务器时，信息通过 `SMB` 协议进行传输，具体工作流程如下：当客户端支持 `SMB` 协议，Samba 服务器接收客户端的请求，选择合适的 `SMB` 类型，若响应客户端的请求：即 客户端-> Samba 请求-> 服务器-> 响应->客户端。

(2) 建立连接：当 `SMB` 类型确定后，客户端发送 `session setup` 指令，提交标识和密码，与 Samba 服务器建立连接。如果客户端通过 Samba 请求，Samba 服务器作出响应，为客户端提供一个 `UID`，在客户端与服务器通信时，客户端->`session setup` & 请求->服务器->`session setup` & 请求->服务器->客户端。

(3) 访问共享资源：当客户端访问 Samba 服务器的共享资源，发送 `tree connect` 指令包，通知服务器需要需要的共享资源。如果设置了允许，Samba 服务器为每个客户端与共享资源连接到 `TCP`，客户端可访问所需的共享资源。客户端->`tree connect` & 请求->客户端。

(4) 断开连接：共享使用完毕，客户端向服务器发送 `tree disconnect` 请求，与服务器连接。客户端->`tree disconnect` & 请求->服务器->`tree disconnect` & 请求->客户端。

![](img/ec0e037f26e46c767b8ae4c4c4a36e86_195_0.png)

### 10.1.3 安装环境 Samba 服务

为了安装工作的顺利进行，在安装 Samba 服务之前首要做好准备工作。在本节：

(1) 检查系统是否安装 Samba 服务。

在 `Linux` 系统中检查是否已经安装 Samba 服务的情况下，可以进行如下检查：

```
[root@localhost ~]# rpm -q | grep samba
samba-client-libs-4.8.3-a.4.el7_64
samba-common-libs-4.8.3-a.4.el7_64
samba-common-4.8.3-a.4.el7.noarch
```

这里列出所有已安装的 Samba 软件包，可见 Samba 服务可能未安装。主要包括：

- `samba-client-libs-4.8.3-a.4.el7_64`: 客户端组件，当 `Linux` 作为 Samba Client 时需要的指令，如挂载文件使用的 `smb`。
- `samba-common-4.8.3-a.4.el7.noarch`: 提供了 Samba 的主配置文件 (`samba.conf`)，`samba.conf` 语法程序 (`testparm`)。
- `samba-4.8.3-a.4.el7_64`: 服务端组件，提供了 Samba 服务的守护程序、共享文档。

(2) 在 `RHEL7` 通过 `RPM` 包或 `Yum` 源安装 Samba，也可以采用图形化。通过以下图形化：

- 将 `Red Hat Enterprise 7` 安装盘放入，`Linux` 系统中配置好 `YUM` 的本地仓库，然后继续。
- 选择“应用程序”→“系统工具”→“软件”，打开“软件”对话框，如图 10-1 所示。
- 在搜索框中输入“Samba”，在右侧选择 Samba 主程序-4.8.3，下面有关软件点击“安装”，系统自动安装 Samba 及依赖。

![](img/ec0e037f26e46c767b8ae4c4c4a366)

(4) 在系统中查看所有安装的 Samba 软件包。

```
[root@localhost ~]# rpm -q | grep samba
samba-common-tools-4.8.3-a.4.el7_64
samba-client-libs-4.8.3-a.4.el7_64
samba-common-libs-4.8.3-a.4.el7_64
samba-common-4.8.3-a.4.el7.noarch
samba-libs-4.8.3-a.4.el7_64
```

(3) 进行其他工作。配置 Samba 服务器的 `IP` 地址为 `172.16.42.188`，关闭防火墙，设置系统的安全机制为 `Permissive` 生效。

```
[root@localhost ~]# vi /etc/network/scripts/ifcfg-ens3
[root@localhost ~]# ifconfig ens3
ens3: flags=416<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500
inet 172.16.42.188 mask 255.255.255.0 broadcast 172.16.42.255
inet6 fe80:0000:0000:c52f:8b92:34db%64 scope link<link>
ether 00:0c:29:37:87:64 (Ethernet)
packets 1950 bytes 14460 (141.2 KiB)
RX errors 0 dropped 0 overflows 0 frame
TX packets 6530 bytes (6.4 KiB)
TX errors 0 dropped 0 overflows 0 collisions 0
[root@localhost ~]# systemctl stop firewalld
[root@localhost ~]# systemctl disable firewalld
[root@localhost ~]# vi /etc/selinux/config
[root@localhost ~]# setenforce 0
[root@localhost ~]# getenforce
```

## 10.2 项目实施

为了学院中 `Windows` 客户端能够访问网络上的资源，`IT` 学会配置一台 Samba 服务器，服务器的 `IP` 地址为 `172.16.42.188`，子网掩码为 `255.255.255.0`，默认网关为 `172.16.42.1`。工作名为 `SAMBA`，共享目录为 `xx`，共享名为 `xx`，使用 `Linux` 客户端和 `Windows` 客户端访问 `Linux` 服务器，但访问时必须使用用户名 `xx`，密码为 `123456`。

### 10.2.1 Samba 服务器的配置

1. 配置主文件 `/etc/samba/smb.conf`

配置 Samba 服务器的主要是对对应的主文件 `/etc/samba/smb.conf` 进行相应的设置。Samba 在启动时会读取 `smb.conf` 文件的内容，以决定何时启动、提供服务，以及权限限制、共享限制、打印机和机器所属工作组等各项参数，如图 10-2 所示。

```
[root@localhost ~]# vi /etc/samba/smb.conf
```

10-2 `/etc/samba/smb.conf` 文件内容
