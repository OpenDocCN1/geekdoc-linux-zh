
# 步骤 6

安装 ipa-client-包
=> `yum install ipa-client`

# 步骤 7

安装 ipa-client
=> `ipa-client-install [yes]`

+ authorize enroll computer : `admin`
→ password : `open12345`
=> `authconfig -enblemkhomedir -update`

[现在注销会话并使用管理员设置的域用户名和密码登录]

# 在 IPA 上配置 NFS 服务器

## 为什么要安装 NFS 服务器？

因为当你从一台电脑使用域用户登录并存储某些文件时。在 IPA 服务器中，如果你用另一台电脑登录，虽然你可以因为集中认证系统 (`IPA`) 使用域用户名和密码登录，但你找不到在另一台电脑上创建的资源，这意味着你的数据不是漫游的。它停留在你使用的电脑上。因此无法完成集中管理，因为我们的目标是无论你使用哪个 IP 客户端电脑，都可以使用域用户名和密码登录，并获取你的文件。为了实现这一点，我们需要制作 NFS 服务器

## 我们在哪里安装我们的 NFS 服务器？

你可以将 NFS 服务器安装在 IPA 服务器内部，但并不是

# UBUNTU $ CENTOS 管理员

推荐做法。虽然在示例中我们使用 ipa 服务器作为 nfs 服务器，但你可以在任何活跃的 ipa 客户端上安装 nfs 服务器[例如，你可以将其安装在“client1”上]。基本上，我们选择一个空间较大的客户端，所有用户的资源都将保存在 nfs 服务器中。

# NFS 服务器

## 步骤 1
选择服务器
我们选择 ipa 服务器作为 nfs 服务器 [`ipa.it.local`]

## 步骤 2
安装 nfs 服务包
=> `sudo yum install nfs-utils`

## 步骤 3
编辑文件 `/etc/exports`
=> `vim /etc/exports`

```
/home *(rw,sync)
```

## 步骤 4
启动 nfs 服务
=> `systemctl enable nfs-server`
=> `systemctl start nfs-server`

## 步骤 5
UBUNTU $ CENTOS 管理员

启动 rpcbind

- 1) `systemctl enable rpcbind`
- 2) `systemctl start rpcbind`

## 步骤 6
添加防火墙规则

```
=>firewall-cmd -permanent -add-service nfs
```

```
=>firewall-cmd -reload
```

## 步骤 7
查看 nfs 服务器的挂载卷

```
=>showmount -e
```

[如果一切顺利，你将看到已挂载的目录]

# IPA 客户端配置

[你必须重新配置 client1 以与 nfs 服务器同步数据]

## 步骤 1
安装 nfs utils 包

```
=>sudo yum install nfs-utils
```

## 步骤 2
编辑 `/etc/auto.master`

```
=>vim /etc/auto.master
```

添加此行：

```
/home /etc/auto.autofs
```

## 步骤 3
创建 `/etc/auto.autofs`
=> `vim /etc/auto.autofs`

添加此行：

syntax: * `<ipa_server>`:/home/

`*ipa`:/home/

[例如，如果 client1 是 nfs 服务器，命令将为 =>`* client1`:/home/ 记住，只使用客户端名称，而不要使用整个域名]

## 步骤 4
启动 autofofs 进程

```
=> systemctl enable autofofs
=> systemctl start autofofs
```

完成后，你可以使用任何域名和密码登录任何 ipa 客户端，并将找到你自己的资源

# 在 IPA 上配置 SAMBA 服务器

*要求：*
1) Centos 服务器，ip: `192.168.0.50`
2) 客户端（ubuntu 或 centos），ip: `192.168.0.100`
3) 互联网连接

## 步骤 1
1) 使用 IPA 服务器创建两个用户 '`smbuser1`' 和 '`smbuser2`'。你可以通过 Web 界面或终端添加。[这必须在 IPA 服务器上完成]

samba 服务器必须是 IPA 服务器的客户端。我们将一个 IPA 服务器的客户端制作成 samba 服务器。我们必须从 IPA 服务器添加用户，并将此用户添加为 samba 客户端。所有用户创建都由 IPA 服务器完成。samba 服务器会在创建服务器时将该用户作为 samba 用户添加。

## 步骤 2
更新仓库并安装必要的 samba 包

```
=> yum update -y
=>yum install samba-client samba-common
```

## 步骤 3
创建目录并为该用户和组赋予适当权限

```
=>mkdir /share
=>chmod 777/share
```

## 步骤 4
我们必须将测试组的用户添加到 samba

```
=>smbpasswd -a smuser1
=>smbpasswd -a smuser2
```

## 步骤 5
配置 SELinux。你可以禁用 SELinux 或设置正确的布尔值和安全性，否则它将允许你连接到服务器。在这里我们不会禁用 SELinux，而是将更改布尔值。

```
=>setsebool -P samba_export_all_ro=1 samba_export_all_rw=1
=>getsebool -a | grep samba_export
=> manageage fcontext -at samba_share "/share(/.*)?*"
=> restorecon /share
```

```
[root@localhost ~]# setsebool -P samba_export_all_ro=1
[root@localhost ~]# setsebool -P samba_export_all_rw=1
[root@localhost ~]# getsebool -a | grep samba_export
samba_export_all_ro -> on
samba_export_all_rw -> on
[root@localhost ~]# semanage fcontext -at samba_share_t "/share/(.++)?"
[root@localhost ~]# restorecon /share
[root@localhost ~]#
```

## 步骤 6
我们必须更改防火墙设置以允许连接

=> `firewall-cmd --permanent --add-service=samba`
=> `firewall-cmd --reload`

```
[root@localhost ~]# firewall-cmd --permanent --add-service=samba
success
[root@localhost ~]# firewall-cmd --reload
success
[root@localhost ~]#
```

## 步骤 7
这是该部分最重要的路径。我们需要编辑 samba 共享的配置

```
=> vim /etc/samba/smb.conf
```

```
share
comment=共享目录
browsable=yes
path=/share
writable = no
list = smuser1
```

## 步骤 7
使用 '`testparm`' 命令测试配置。如果配置中有任何错误，此命令将告知你

```
=>testparm
```

```
[root@localhost ~]# testparm
Load smb config from /etc/samba/smb.conf
rlimit_max: increasing rlimit_max (1024) to minimum limit (16384)
Processing section [homes]
Processing section [printers]
Processing section [print$]
Processing section [share]
Loaded services OK.
Server role: STANDALONE
Press enter to see dump of service definitions
```

## 步骤 8
重启 samba 服务器使更改生效

=> `systemctl start smb`
=> `systemctl start nmb`

```
[root@localhost ~]# systemctl start smb
[root@localhost ~ systemctl start nmb
[root@localhost]#
```

## 步骤 9
我们必须启用 smb 和 nmb 服务在启动机时启动

=> `systemctl enable smb`
=> `systemctl enable nmb`

```
[root@localhost ~]# systemctl enable symlink from /etc/systemd/system/multi-user.wants/smb.service to /usr/lib/systemd/system/smb.service.
[root@localhost ~]# systemctl enable nmb
Created symlink from /etc/systemd/system/multi-user.wants/nmb.service to /usr/lib/systemd/system/nmb.service.
[root@localhost]#
```

## 步骤 10
从服务器测试连接

=> `smclient -L localhost -U smuser`

```
[root@localhost ~]# smclient -L localhost - user1
Enter SAMBA\user1's password:
```

# 在 UBUNTU 上配置 DHCP 服务器

## 配置要求

- GNS3 软件
- UBUNTU 服务器操作系统
- MIKROTIK 云托管路由器操作系统 (CHR)
- 用于启动系统的 VIRTUALBOX
- VPCS（作为客户端的虚拟小型电脑）
- 具有网络连接更佳

## 拓扑

![](img/5e8a2bb431e5309eb9c40e886b58672b_539_0.png)

云网络: `10.42.0.0/24`
云端网关: `10.42.0.1`
MIKROTIK 路由器: WAN 接口 IP: `10.42.0.99`
MIKROTIK 路由器: LAN 接口 IP: `192.168.88.1`
MIKROTIK 路由器: LAN 网络: `192.168.88.0/24`

## 设置所有内容

- 下载 GNS3 并安装
- 下载 MIKROTI RouterOS (云托管 CHR)(.ova) 镜像
- 下载 UBUNTU Server
- 下载 Virtualbox
- 导入 OVA 镜像

a) 进入设置，然后选择“网络”，并激活 4 个适配器(adapter1,adapter2,adapter3,adapter4)，对于第一个适配器，进入“高级”，并将“混杂模式”设置为“允许所有(allow all)”

- 然后进入 GNS3 → 编辑(Edit) → 首选项(Preference) → VirtualBox Vms → 新(New)→ 选择虚拟机
- 完成

b) 然后在窗口中选择 编辑(Edit) → 网络(Networks) → 适配器(Adapters) 设置为 4

c) 然后在最后一个选项勾选“允许 GNS3 使用任何配置的 VirtualBox 适配器(Allow GNS3 to use any configured VirtualBox adapter)”→ 是

d) 你可以更改图标（可选）

d) 然后点击完成

7) 安装 Ubuntu 镜像

a) 进入设置，然后选择“网络”，并激活 4 个适配器(adapter1,adapter2,adapter3,adapter4)，对于第一个适配器，进入“高级”，并将“混杂模式”设置为“允许所有(allow all)”

- 然后进入 GNS3 -> 编辑 -> 首选项 -> VirtualBox Vms -> 新 -> 选择虚拟机
- 完成 ->

b) 然后在窗口中选择 编辑(Edit) -> 网络(Networks) -> 适配器(Adapters) 设置为 4 (VVI)

c) 然后在最后一个选项勾选“允许 GNS3 使用任何配置的 Virtualbox 适配器”→ 是

最后两个 b 和 c 非常非常重要

- 启动路由器 OS

## Tanvir Rahman

用户名: `admin`
密码: `<无>`

## 路由器配置

```
[admin@MikroTik]/ip address add address=10.42.0.193/24 interface=ether1
[admin@MikroTik]/ip address add address=192.168.10.10 interface=ether2
[admin@MikroTik]/ip route add gateway=10.42.0.1
[admin@MikroTik]/ip firewall nat add chain=srcnat action=masquerade
[admin@MikroTik]/ip dns set servers=8.8.8.8
[admin@MikroTik]> ping yahoo.com
```

## 启动 ubuntu 服务器

- 打开终端
- 设置静态 IP

```
→ sudo vim /etc/network/interfaces
```

```
auto eth0
iface eth0 inet static
address 192.168.88.10
netmask 255.255.255.255
network 192.168.88.0
gateway 192.168.88.1
```

```
→ sudo /etc/init.d/networking restart
```

在此之后你将能够连接到互联网

## 安装 DHCP 服务器

更新仓库
→ `sudo apt-get update`
安装 dhcp 包

```
→ sudo apt-get install isc-dhcp-server
```

## 配置服务器

cd `/etc/dhcp`
vim `dhcpd.conf`

```
option domain-name "mydomain.org";
### 添加一个域名
option domain-name-servers 8.8.8.8;
```

### 这是一个非常基本的子网声明

```
subnet 192.168.88.0 netmask 255.255.255.0{
range 192.168.88.20 192.168.88.200;
option routers 192.168.88.1;
}
```

## 解释

```
subnet <提供网络地址> netmask<提供子网掩码>{
range <范围内的起始 IP> <范围内的结束 IP>;
option routers <网关>}
```

## 重启服务器

→ `sudo /etc/init.d/isc-dhcp-server restart`

## 客户端侧

→ 启动客户端（在本例中我使用 VPCS）

```
PC-1> ip dhcp
DORA
IP 192.168.88.21/24 GW 192.168.88.1→ 测试一下
PC-1> ping 8.8.8.8
84 bytes from 8.8.8.8 icmp_seq=1 ttl=116 time=59.929 ms
84 bytes from 8.8.8.8 icmp_seq=2 ttl=116 time=65.707 ms
```

→ 如果你运行的是 Linux 客户端，打开终端并输入
-> `dhclient`
