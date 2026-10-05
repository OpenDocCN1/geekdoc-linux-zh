

# 删除网络连接

**nmcli con name** 会从系统中删除名为 **name** 的连接，将其从设备断开并移除文件 **/etc/sysconfig/network-scripts/ifcfg-name**。

```
[root@host ~]# nmcli con static-ens3
```

# 谁可以修改网络设置？

root 用户可以使用 **nmcli** 进行任何必要的网络配置更改。

登录到本地控制台的普通用户也可以对系统进行许多网络配置更改。他们必须在系统的键盘上登录到文本虚拟控制台或图形桌面环境才能获得这种控制权限。这背后的逻辑是：如果有人物理出现在电脑旁，那么该电脑可能被用作工作站或笔记本电脑，他们可能需要配置、激活和停用某个有线或无线网络接口。相比之下，如果系统位于数据中心，通常登录到机器本身的用户应该是管理员。

使用 **ssh** 登录的普通用户在不成为 root 用户的情况下，没有更改网络权限的权限。

你可以使用 **nmcli gen permissions** 命令查看你当前的权限。

# 命令总结

下表列了本节讨论的常用 **nmcli** 命令列表。

| 命令 | 目的 |
| :--- | :--- |
| nmcli dev status | 显示所有网络接口的 NetworkManager 状态。 |
| nmcli con show | 列出所有连接。 |
| nmcli con show name | 查看连接 *name* 的当前设置。 |
| nmcli con add con-name name | 添加新的连接 *name*。 |
| nmcli con mod name | 修改连接 *name*。 |
| nmcli con reload | 重新加载配置文件（在手动编辑后很有用）。 |
| nmcli con up name | 激活连接 *name*。 |
| nmcli dev dis dev | 禁用并断开网络接口 *dev* 上的当前连接。 |
| nmcli con del name | 删除连接 *name* 及其配置文件。

# 参考文献

> NetworkManager(8), nmcli(1), nmcli-examples(5), nm-settings(5), hostnamectl(1), resolv.conf(5), hostname(5), ip(8), 以及 ip-address(8) 手页

# 引导性练习

# 从命令行配置网络

在此练习中，你将使用 **nmcli** 配置网络设置。

# 结果

你应该能够将系统从 DHCP 转换为静态配置。

# 开始之前

在工作站上使用密码 `student` 登录 `student` 用户。

从工作站运行 **lab net-config start** 命令。该命令运行一个脚本，用于判断主机 servera 是否在网络上可达。

```
[student@workstation ~]$ lab net-config start
```

- 1. 使用 ssh 命令以 `student` 用户身份登录 `servera`。系统配置为使用 SSH 密钥认证。

```
[student@workstation ~]$ ssh student@servera
[student@servera ~]$
```

- 2. 这些指令假设你的 MAC 地址为 52:54:00:00:00:fa 的网络接口名为 ens3。使用 **ip link** 检查此处，如果你的系统有不同的接口名称，请在练习的剩余部分使用该名称。

```
[student@servera ~]$ ip link
1: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default
len 1000
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: ens3:<BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fcod_type state UP default qlen 1000
link/ether 52:54:00:00:00:fa brd ff:ff:ff:ff:ff:ff
```

- 3. 使用 **nmcli** 查看网络设置。

- 3.1. 显示所有连接。

```
[student@servera ~]$ nmcli con show
```

| 名称 | UUID | 类型 | 设备 |
| :--- | :--- | :--- | :--- |
| ens3 | 03da038a-3257-4272-a478-53055cc0128 | 以太网 | ens3 |

| Wired connection 1 91d515af-5367-384b-a012-6bdd2e390f66 | 以太网 |

- 3.2. 仅显示激活的连接。
你的网络接口名称应出现在 DEVICE 列下，该设备激活的连接名称位于同一行的 NAME 列下。本练习假设激活的连接是 ens3，与网络接口名称匹配。
如果激活连接的名称不同，请在练习的剩余部分用该名称代替 ens3。

```
$student@servera~$ nmcli con show --active
NAME UUID DEVICE
ens3 03d0a38a-3257-a472-a478-53055cc90128 ethernet ens3
```

- 3.3. 显示激活连接的所有设置。

```
$student@servera~$ nmcli con show "ens3"
connection.id:
ens3
connection.uuid:
03d0a38a-3257-a472-a478-53055cc90128
connection.stable-id:
-
connection.type:
802-3-ethernet
connection.autoconnect:
yes
..output omitted...
ipv4.method:
manual
ipv4.dns:
172.25.250.254
ipv4.dns-search:
lab.example.com,example.com
"
ipv4.priority:
0
ipv4.addresses:
172.25.250.10/24
172.25.250.254
ipv4.gateway:
..output omitted...
GENERAL.NAME:
GENERAL.NAME:\ens3
GENERAL.UUID:
03d0a38a-3257-a472-a478-53055cc90128
GENERAL.DEVICE:
ens3
GENERAL.STATE:
activated
GENERAL.DEFAULT:
yes
GENERAL.DEFAULT6:
no
GENERAL.SPEC-OBJECT:
-
GENERAL.VPN:
no
GENERAL.DBUS-PATH:
/org/freesktop/NetworkManager/ActiveConnection/2
GENERAL.CON-PATH:
/org/freesktop/NetworkManager/Settings/2
GENERAL.ZONE:
-
GENERAL.MASTER-PATH:
-
IP4.ADDRESS[1]:
172.25.250.10/24
172.25.250.254
IP4.GATEWAY:
dst = 172.25.250.24, nh = 0.0.0.0, mt = 100
IP4.ROUTE[1]:
IP4.ROUTE[2]:ndst = 0.0.0.0/0, nh = 172.25.250.254, mt = 100
IP4.DNS[1]:
172.25.250.254
```

