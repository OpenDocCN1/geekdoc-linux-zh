
### 内核配置步骤

你可以从登录 shell 运行 `make menuconfig` 工具来配置内核。`Menuconfig` 是一个非常好的系统。我在这里使用基于文本的系统，是因为我希望在初几次编译内核时，让你习惯所有潜在的配置选项。你有许多选择，我相信如果你手动操作，会更好地理解它们。

6. 持续按回车键（接受每个提示的默认值），直到进入提示网络选项的部分。确保对 `IP` 转发（`IP Forwarding`）、防火墙、伪装（`masquerading`）和分片的问题的回答均为是 (`Y`)，如列表 10-8 所示。

**列表 10-8：内核配置中的 `IP` 转发**

- 网络选项
- 网络防火墙 (`CONFIG_FIREWALL`) `[Y/n?]`
- 网络别名 (`CONFIG_NET_ALIAS`) `[Y/n?]`
- `TCP/IP` 网络 (`CONFIG_INET`) `[Y/n?]`
- `IP`: 转发/网关 (`CONFIG_IP_FORWARD`) `[Y/n]`
- `IP`: 多组播 (`CONFIG_IP_MULTICAST`) `[Y/n?]`
- `IP`: `syn` cookies (`CONFIG_SYN_COOKIES`) `[Y/n?]`
- `IP`: `rst` cookies (`CONFIG_RST_COOKIES`) `[Y/n?]`
- `IP`: 防火墙 (`CONFIG_IP_FIREWALL`) `[Y/n?]`
- `IP`: 防火墙数据日志 (`CONFIG_IP_FIREWALL_VERBOSE`) `[Y/n?]`
- `IP`: 伪装 (`CONFIG_IP_MASQUERADE`) `[Y/n?]` `Y`
- 特定协议的伪装支持将作为模块。
- `IP`: `ipautof` masq 支持 (`CONFIG_IP_MASQUERADE_IPAUTOFW`) `[Y/]`
- `IP`: `ICMP` 伪装 (`CONFIG_IP_MASQUERADE_ICMP`) `[Y/n?]`
- `IP`: 透明代理支持 (实验性) (`CONFIG_IP_TRANSPARENT_PROXY`) `[Y/n?]`
- `IP`: 始终去碎片 (`CONFIG_IP_ALWAYS_DEFRAG`) `[N/y]` `Y`
- `IP`: 计数 (`CONFIG_IP_ACCT`) `[Y/n?]`
- `IP`: 优化为路由器而非主机 (`CONFIG_IP_ROUTER`) `[Y/n?]`
- `IP`: 隧道 (`CONFIG_NET_IPIP`) `[M/n/?]`
- `IP`: 别名支持 (`CONFIG_IP_ALIAS`) `[M/n/?]`

#### 第四部分：运行真实的业务

![](img/29df11d9c5c608cff7b4fa65d0c78e37_445_0.png)

不要害怕随时跳出配置过程（按 `Ctrl+C`）。该过程在结束时仅会将你的选择写入配置文件。你可以随时重新开始。

8. 继续选择默认值，直到到达“网络设备支持”部分。针对你特定的适配器输入 `y`。如果我使用 `3Com 3c509` 适配器，我会对该设备回答 `yes`，如列表 10-9 所示。

**列表 10-9：`3c3509` 适配器的内核配置**

- 网络设备支持
- 网络设备支持 (`CONFIG_NETDEVICES`) `[Y/n/?]`
- Dummy 网络驱动支持 (`CO`)
- `PLIP`（并行口）支持 (`CONFIG_PLIP`) `[M/n/y/?]` `n`
- `PPP`（点对点）支持 (`CONFIG_PPP`) `[M/n/y/?]` `n`
- `PPP` 的 `CCP` 压缩器仅作为模块构建。
- `SLIP`（串口线）支持 (`CONFIG_SLIP`) `[M/n/y/?]` `n`
- `CSIP` 压缩头 (`CONFIG_SLIP_COMPRESSED`) `[M/n/y/?]` `n`
- 链路保持和行填充 (`CONFIG_SLIP_SMART`) `[Y/n/?]` `n`
- 六位 `SLIP` 封装 (`CONFIG_SLIP_MODE_SLIP6`) `[Y/n/?]` `n`
- 无射电网络接口 (`CONFIG_NET_RADIO`) `[Y/n/?]` `n`
- 以太网 (10 或 100Mbps) (`CONFIG_NET_ETHERNET`) `[Y/n/?]` `n`
- `3COM` 卡 (`CONFIG_NET_VENDOR_3COM`) `[Y/n/?]` `n`
- `3c501` 支持 (`CONFIG_EL1`) `[M/n/y/?]` `n`
- `3c503` 支持 (`CONFIG_EL2`) `[M/n/y/?]` `n`
- `3c505` 支持 (`CONFIG_ELPLUS`) `[N/y/m/?]` `n`
- `3c507` 支持 (`CONFIG_EL16`) `[N/y/m/?]` `n`
- `3c509/3c579` 支持 (`CONFIG_EL53`) `[M/n/y/?]` `y`

> 注意，我对这些问题中的大多数都回答了否，因为我的文件服务器/路由器永远不会使用其中任何一个。我的选择反映了我使用的组件，你应该根据自己的配置来回答它们。

9. 继续按回车键直到配置完成。

10. 要创建依赖关系并编译源码以创建你的新内核，请输入以下命令：

```
make dep

make image
```

11. 创建新内核后，你需要将该文件移动到 `/boot` 目录并告诉 `LILO` 它的位置。`make image` 在 `/usr/src/linux/arch/i86/boot` 目录下创建了一个名为 `zimage` 的文件。要将其移动到 `/boot` 目录，输入以下命令：

```
mv /usr/src/linux/arch/i86/boot/zImage /boot
```

12. 编辑 `/etc/lilo.conf` 以包含新内核。列表 10-10 显示了修改后的 `lilo.conf`。

```
boot=/dev/hda

map=/boot/map

timeout=50

append="ether=0.0,eth0"

image=/boot/zImage

label=newlinux

root=/dev/hd1

read-only

image=/boot/vmlinuz

label=linux

root=/dev/hd1

read-only
```

我已将 `zimage` 文件标记为 `newlinux`。这是你在 `LILO` 提示处输入的内容，以便将其设置为默认内核。如果你想启动旧内核 `vmlinuz`，需要在启动时的 `LILO` 提示处输入 `linux`。

13. 通过输入以下命令让 `LILO` 重新配置以使其持久化：

```
lilo
```

14. 输入以下命令优雅地关闭你的文件服务器/路由器（`-h` 选项表示停止而非重启）：

```
/bin/shutdown -h now
```

15. 当计算机关闭后，关闭电源。

16. 断开电源线。

#### 第四部分：运行真实的业务

17. 打开机箱安装第二个网络适配器。最好物理上分开两个适配器，因为如果它们挨在一起，连接 `Thinnet` 适配器可能会困难。

18. 关闭机箱并插入电源线。

19. 开启电源。新内核已启动。你应该参考列表 10-11 获取信息。

**列表 10-11：我的 `3c509` 适配器**

```
eth0: 192.168.1.1 mask:255.255.255.0 broadcast:192.168.1.255

eth1: 192.168.32.1 mask:255.255.255.0 broadcast:192.168.32.255
```

##### 配置网络参数

以下说明了如何修改：

1. 进入 `/etc/sysconfig/network-scripts` 目录。

2. 进入 `/etc/sysconfig/network-scripts` 中的 `eth0`。

**列表 10-12:/etc/sysconfig/network-scripts/ifcfg0**

```
DEVICE=eth0

ADDR=192.168.1.254

NETMASK=255.255.255.0

NETWORK=192.168.1.0

BROADCAST=192.168.1.255

ONBOOT=yes

BOOTPROTO=none
```

> 注意，我将公网地址 `192.168.32.0` 分配给了防火墙网络。这是我的主观决定。我选择 `192.168.32` 是因为它比 `192.168.2` 更容易与私有网络地址 `192.168.1` 区分。

3. 将 `ifcfg-0` 复制到 `ifcfg-1`：

```
cp ifcfg-0 ifcfg-1
```

4. 使用 `vi` 编辑器将 `ifcfg-1` 编辑得如列表 10-13 所示。

**列表 10-13:/etc/sysconfig/network-scripts/ifcfg1**

```
DEVICE=eth1

ADDR=192.168.32.254

NETMASK=255.255.255.0

NETWORK=192.168.32.0

BROADCAST=192.168.32.255

ONBOOT=yes

BOOTPROTO=none
```

> 请注意，我将公网地址 `192.168.32.0` 分配给了防火墙网络。这是我的主观决定。

5. 按 `Escape` 键退出插入模式。

6. 输入 `:wq`（保存并退出命令）保存你的新文件，文件将在退出 `vi` 时被保存。

7. 使用切换目录命令返回上一级：

```
cd ..
```
