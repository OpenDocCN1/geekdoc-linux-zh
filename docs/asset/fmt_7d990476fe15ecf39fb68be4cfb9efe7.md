
TCP/IP 网络中的每台计算机都必须拥有 `IP` 地址、子网掩码、网关 `IP` 地址以及 `DNS` 服务器 `IP` 地址。`DHCP` 服务器用于自动将这些基本配置发送给网络中的计算机。

`DHCP` 是一种客户-服务器协议。`DHCP` 服务器分配两种类型的地址租约：手动租约和动态租约。在手动租约中，`DHCP` 服务器通过将客户端硬件地址与特定 `IP` 地址关联，手动显式地分配 `IP` 地址。而在动态租约中，`DHCP` 从配置文件中提到的 `IP` 地址范围内，向客户端分配任何可用的 `IP` 地址。

#### 配置文件

服务器端的配置文件如下：

- `/etc/dhcpd.conf`：`DHCP` 服务器的主配置文件。
- `/var/lib/dhcp/dhcpd.leases`：存储已租约的客户端 `IP` 地址详情
- `/usr/share/doc/dhcp-version/dhcpd.conf.sample`：示例 `DHCP` 配置文件

- 客户端端：
- `/etc/sysconfig/network-scripts/ifcfg-eth0`：更改为 `DHCP`

#### 安装和配置 DHCP 服务器的步骤：

1. 使用以下命令安装 `DHCP` 软件包：

```
[root@netmon tmp]$ rpm -ivh dhcp-3.0.1-1.i386.rpm
```

2. 使用以下命令复制示例文件：

```
[root@netmon tmp]# cp /usr/share/doc/dhcp-3.0pl1/dhcpd.conf.sample /etc/dhcpd.conf
```

3. 使用以下命令编辑 `dhcpd.conf` 文件：

```
### 这是示例 dhcp 配置文件：
ddns-update-style interim
ignore client-updates
subnet 192.168.1.0 netmask 255.255.255.0 {
    # 服务器将颁发给
    # DHCP 启用 PC 客户端的 IP 地址范围
    # 在网络启动时
    range 192.168.1.201 192.168.1.220;

    # 设置客户端可以保留
    # IP 地址的时间（以秒为单位）
    default-lease-time 86400;
    max-lease-time 86400;

    # 设置 PC 客户端
    # 使用的默认网关
    option routers 192.168.1.1;

    # 不要将此
    # NIC 接口的 DHCP 请求转发
    # 到其他 NIC
    option ip-forwarding off;

    # 设置 DHCP 客户端
    # 使用的广播地址和子网掩码
    option broadcast-address 192.168.1.255;
    option subnet-mask 255.255.255.0;

    # 设置 DHCP 客户端
    # 使用的 DNS 服务器
    option domain-name-servers 192.168.1.100;

    # 设置 DHCP 客户端
    # 使用的 NTP 服务器
    option ntp-server 192.168.1.100;

    # 如果您为 Windows 客户端指定了 WINS 服务器，
    # 需要在 dhcpd.conf 文件中包含以下选项：
    option netbios-name-servers 192.168.1.100;

    # 您还可以根据客户端的
    # 以太网 MAC 地址分配特定的 IP 地址，如下所示（主机名为“laser-printer”）：
    host laser-printer {
        hardware ethernet 08:00:2b:4c:59:23;
        fixed-address 192.168.1.222;
    }
}

# List an unused interface here
subnet 192.168.2.0 netmask 255.255.255.0 {
}
```

![](img/f3b9cff79e19317416c12eaf5ded7245_163_0.png)

建议对 `dhcpd.conf` 文件进行如下修改：

1. 根据网络子网 ID 更改子网 `IP` 地址

   ```
   subnet 172.16.0.0 netmask 255.255.0.0 {
   ```

2. 指定要分配给网络中客户端的 `IP` 地址范围。

   ```
   range 172.16.0.1 172.16.0.100;
   ```

3. 指定客户端使用的默认网关：

   ```
   option routers 172.16.1.1;
   ```

4. 指定 `DNS` 服务器 `IP` 地址

   ```
   option domain-name-servers 192.168.1.100;
   ```

5. 使用以下命令启动 `DHCP` 服务器：

```
[root@netmon tmp]# touch /var/lib/dhcpd/dhcpd.leases
[root@netmon tmp]# chkconfig --level 345 dhcpd on
[root@netmon tmp]# service dhcpd start
[root@netmon tmp]# service dhcpd stop
[root@netmon tmp]# service dhcpd restart
```

6. 测试 `DHCP` 服务器：

   您也可以使用以下命令测试 `DHCP` 进程是否正在运行；您应该收到普通旧进程 ID 号的响应：

```
[root@netmon tmp]# pgrep dhcpd
```

#### 设置 LINUX 客户端以使用 DHCP

您可以配置 `Linux` `NIC` 接口以使用 `DHCP` 获取其 `IP` 地址。

```
[root@netmon tmp]# nano /etc/sysconfig/network-scripts/ifcfg-eth0
更改为                    BOOTPROTO=dhcp
[root@netmon tmp]# service network restart
```

图 1 显示了用于 `DHCP` 的 `Linux` 客户端。

![](img/f3b9cff79e19317416c12eaf5ded7245_164_0.png)

#### 设置 Windows 客户端以使用 DHCP

让我们执行以下步骤来设置 `Windows` 客户端：

1. 前往 → 网络/邻居 → 右键单击 → 属性 → `TCP/IP`。
2. 选择“自动获取 `IP` 地址”单选按钮以自动获取 `IP` 地址。图 2 显示了用于使用 `DHCP` 服务器的 `Windows` 客户端配置对话框。

![](img/f3b9cff79e19317416c12eaf5ded7245_165_0.png)

让我们总结在这个实验中学习到的关键点。

### 摘要

在这个实验中，您已经学会了安装和配置 `DHCP` 服务器。您还学会了配置客户端以使用 `DHCP`。

### 笔记

...

### 16 实验：网络文件系统协议 (NFS)

`目标` 安装并配置 `NFS` 协议服务器和客户端。

`要求` 配有 `Fedora`/`RHEL` 和 `Linux` 发行版 `CD`/`DVD` 的 `IV` 类 `P` 型 `PC`。

`概念` `NFS` 是一个分布式文件系统。`NFS` 服务器拥有一个或多个由 `NFS` 客户端挂载的文件系统。`NFS` 文件系统使用标准的 `UNIX` `mount` 命令进行挂载。所有 `Unix` 实用程序在处理 `NFS` 挂载的文件时，其表现与处理本地磁盘上的文件一样好。

`NFS` 代表网络文件系统（`Network File System`），它是 `Linux` 和类 `Unix` 系统之间共享文件的标准方法。系统管理员必须在 `NFS` 服务器上定义需要激活或导出以供 `NFS` 客户端访问的目录。此外，它还在客户端上定义 `NFS` 服务器及其导出目录的子集。

#### 重要的 NFS 守护进程

`NFS` 服务器需要以下特定守护进程和实用程序：

- `portmap`：指所有其他依赖的主要守护进程。它管理使用 `RPC` 规范的应用程序的连接。默认情况下，`portmap` 监听 `TCP` 端口 111，并在此建立初始连接。然后使用它来协商 `TCP` 端口范围，通常高于 1024 端口，用于后续数据传输。您需要在 `NFS` 服务器和客户端上运行 `portmap`。
- `nfs`：启动提供共享 `NFS` 文件系统所需的 `RPC` 进程。`nfs` 守护进程仅在 `NFS` 服务器上运行。
- `nfslock`：允许 `NFS` 客户端通过 `RPC` 进程锁定服务器上的文件。`nfslock` 守护进程需要在 `NFS` 服务器和客户端上运行。
- `netfs`：允许在 `NFS` 客户端上运行的 `RPC` 进程挂载 `NFS` 文件系统。`netfs` 守护进程仅在 `NFS` 客户端上运行。

#### 安装和配置 NFS 服务器/客户端的步骤

执行以下 `NFS` 步骤以安装和配置 `NFS` 服务器/客户端：

1. 安装 `nfs`

`Red Hat Linux` 默认安装 `nfs`，并且在系统启动时也会默认激活它。运行以下命令以检查是否已安装 `nfs` 相关软件包。
