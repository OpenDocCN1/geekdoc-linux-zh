
#### 2. IP 地址与子网掩码

Internet 中 IP 地址唯一标识。子网掩码与 IP 地址共同确定主机所在的网络。

语法：`ifconfig [选项] [地址]`

功能：显示配置信息。常用选项含义：
- `a`: 显示所有网卡（包括未启动的）配置信息。

例 1 配置 `ens33` 的 IP 地址，命令如下：

```bash
[root@d002]# ifconfig ens33 172.16.36.254 netmask 255.255.255.0
```

例 2 激活设备 `ens33`，命令如下：

```bash
[root@d002]# ifconfig ens33 up
```

例 3 禁用设备 `ens33`，命令如下：

```bash
[root@d002]# ifconfig ens33 down
```

例 4 查看指定的网络接口，命令如下：

```bash
[root@d002]# ifconfig ens33
```

```text
ens33:flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500
inet 172.16.36.254 netmask 255.255.255.0 broadcast 172.16.36.254
inet6 fe80::ff13:fe3b:5e70:bc6e prefixlen 64 scope<link>
ether 00:0c:29:32:c4 txuelen 1000 (Ether)
RX packets 2009 bytes 144563 (141.1 KiB)
RX errors 0 dropped 0 overruns 0 frame 0
TX packets 1588 bytes 17725 (17.3 KiB)
TX errors 0 dropped 0 carrier 0 collisions 0
```

例 5 查看所属的网络接口，命令如下：

使用 `ifconfig` 查看网卡的配置信息，如 IP 地址、MAC 地址等，如图 7-1 所示：

```bash
root@d002~# ifconfig
```

![](img/ec0e037f26e46c76b8ae4c4c4a36e86_139_0.png)

图 7-1 使用 `ifconfig` 查看网卡配置信息

其中，从 `flags` 查看该接口已启用，支持广播、组播、`mtu` 值：`inet4`: IP 地址，`code` 为物理地址，`broadcast` 为广播地址；
`inet6`: IP 地址，`prefix` 为网络掩码，长度，表示该接口的连接：
`eth`: 网卡的硬件地址，即 MAC 地址
`txqueue`: 传输队列，接口类型为 Ethernet。
`RX`: 接收收到的数据包(`packets`)接受情况
`TX`: 从发送到传输的数据包
`collisions`: 冲突信息包

由 `RX` 和 `TX` 可以了解网络是否繁忙。`collisions` 发生多次时说明网络状况不太好。

# 132 · Linux 基本应用

由于工作的需要，可能需要为一个网卡配置多个 IP 地址，可以通过设置虚拟网卡来实现。例如通过为网卡配置为 `ens3` 绑定一个 IP 地址 `172.16.36.253`，如图 7-3 所示。

```bash
[root@diani002~#] cd /etc/sysconfig/network-scripts
[root@diani002~#] network-scripts] cp ifcfg-ens3 ifcfg-ens3:1
[root@diani002~#] network-scripts] vim ifcfg-ens3:1
[root@diani002~#] network-scripts] systemctl restart network
[root@diani002~#] network-scripts] ifconfig
```

![](img/ec0e037f26e46c767b8ae4c4c4a36e86_141_0.png)

图 7-3 为网卡 `ens3` 再绑定一个 IP 地址

## 4 `nmcli` 命令

在 RHEL7 中默认的网络服务由 `NetworkManager` 提供，这是一个动态控制和配置网络的维护服务，它用于保持当前网络设备并连接于工作状态，同时也支持传统的 `ifcfg` 类型配置文件。`nmcli`(NetworkManager Command Line Interface)用于创建、显示、删除、激活和检测网络连接，还能管理网络设备。

例 1 查看连接情况，命令如下:

```bash
[root@diani002~#] nmcli connection show
```

| NAME | UUID | TYPE | DEVICE |
| :--- | :--- | :--- | :--- |
| ens3 | c60523f1-ec44-488-81d279e6483cac4 | ethernet | ens3 |
| virb0 | 487b35b4-8061-418c-a9d2-aldad9f2f08 | bridge | virb0 |

例 2 查看 `ens3` 的详细连接情况，命令如下:

```bash
[root@diani002~#] nmcli connection show
```

添加新的连接，并设置 IP 地址：`nmcli connection add con-name <接口名称> type <接口类型> ifname <网卡名称> ip4 <IPv4地址/子网掩码> gw <网关地址>`

例 3 创建新的连接 `ens3-nmcli`，设置 IP 地址为 `172.16.36.222`，网关为 `172.16.36.1`，命令如下:

```bash
[root@diani002~#] nmcli connection add con-name ens3-nmcli type ethernet ens3 ip4 172.16.36.222/24 gw 172.16.36.1。
```

## 项目 7 网络通信

例 4 启动网络服务，命令如下：

```bash
[root@dianzi002~] # nmcli connection up ens3-nmcli
```

或者

```bash
[root@dianzi002~] # nmcli connection up ens3
```

例 5 删除连接 `ens3-nmcli`，命令如下：

```bash
[root@dianzi002~] # nmcli connection delete ens3-nmcli
```

# 3. 其他配置网络参数的方法

### 1) 文本界面

通过终端输入 `nmtui`(NetworkManager Text-User Interface)打开网络管理文本界面，即网络管理器，如图 7-4 所示。

```bash
[root@dianzi002~] # nmtui
```
