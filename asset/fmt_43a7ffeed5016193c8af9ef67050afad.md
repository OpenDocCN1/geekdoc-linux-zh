
8. 编辑 `/etc/sysconfig/network` 文件。你需要设置 `FORWARD_IPV4` 为 `true`，以便内核可以将 IP 数据包从私有网络传输到防火墙网络和防火墙服务器（作为互联网的网关）。这为发往互联网的数据包提供了通往 PPP 连接的路径。你还需要设置 `GATEWAY` 和 `GATEWAYDEV` 变量，以指定私有网络中的数据包如何通过防火墙服务器访问互联网。使用 `vi` 编辑文件，如列表 10-14 所示。

列表 10-14: `/etc/sysconfig/network`

```
NETWORKWORKING=yes

FORWARD_IPV4=true

HOSTNAME=bart.paunchy.com

DOMAIN=paunchy.com

GATEWAY=192.168.32.1

GATEWAYDEV=eth1
```

## 第四部分：运行真实业务

9. 使用切换目录命令进入 `/etc/rc.d` 目录：

```
cd /etc/rc.d
```

10. 编辑文件 `/etc/rc.d/rc.local`。你需要在启动时启动地址伪装（`masquerading`）。开启伪装功能后，来自私有网络的 IP 地址将更改为防火墙网络的 IP 地址。这意味着这些地址会自动从文件服务器/路由器上的一个网络适配器传输到另一个适配器，而无需指定显式路由。一旦到达防火墙服务器，它们就会被路由到互联网。返回的数据包将找到文件服务器/路由器，并改回其原始 IP 地址。此时，它们会被传回私有网络，并最终回到源地。通过这种方法，你不需要在文件服务器/路由器或防火墙服务器上添加任何显式路由。我相信这使网络更加安全，因为没有直接通往你私有网络的路径。任何入侵你防火墙服务器的人都无法直接看到私有网络。

如列表 10-15 所示，将 `ipfwadm` 命令作为 `rc.local` 的最后一行。使用 `vi` 编辑该文件的第二行，然后保存并退出。

列表 10-15: `/etc/rc.d/rc.local` 文件

```
( 仅显示最后三行。 )

cp -f /etc/issue /etc/issue.net

echo > /etc/issue

echo "Masquerade priv net packets as firewall net ones."

echo "This precludes the need to add an explicit route"

echo " back to your private network on the firewall"

echo " server."

ipfwadm -F -a masquerade -S 192.168.1.0/24 -D 0.0.0.0/0
```

### 第 10 章：建立真实网络

11. 你需要让系统识别所有这些新信息。使用 `/etc/rc.d/init.d/network` 脚本停止网络并重新启动它，如后续命令所示：

```
/etc/rc.d/init.d/network stop

/etc/rc.d/init.d/network start
```

你的文件服务器/路由器现在已配置为私有网络和防火墙网络之间的路由器。

## 检查你的网络连接

如果一切顺利，第二个网络接口应该会被激活。遗憾的是，除非你提前跳过并配置了防火墙服务器（这对我没影响），否则你现在还无法尝试与其直接通信。（如果它已配置并连接，请尝试 `ping` 它 —— `ping 192.168.32.1`。）

- 1. 在 shell 窗口中输入以下命令，查看两个网络适配器是否已激活：
  `ifconfig`

- 2. 你应该看到两个网络适配器以及本地回环接口 (`lo`) 的条目，如列表 10-16 所示。

列表 10-16: `ifconfig` 列表

```
lo    Link encap:Local Loopback
inet addr:127.0.0.1 Bcast:127.255.255.255 Mask:255.0.0.0
UP BROADCAST RUNNING MTU:3584 Metric:1
RX packets:307 errors:0 dropped:0 overflows:0
TX packets:307 errors:0 dropped:0 overflows:0
```

```
eth0    Link encap:Ethernet Hwaddr 00:A0:24:2F:30:69
inet addr:192.168.1.254 Bcast:192.168.1.255 Mask:255.255.255.250
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:1645 errors:0 dropped:0 overflows:0
TX packets:1366 errors:0 dropped:0 overflows:0
Interrupt:11 Base address:0x210
```

```
eth1    Link encap:Ethernet Hwaddr
inet addr:192.168.32.254 Bcast:192.168.32.255 Mask:255.255.255.255
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:799 errors:0 dropped:0 overflows:0
TX packets:905 errors:0 dropped:0 overflows:0
Interrupt:10 Base address:0x330
```

- 3. 如果你没有看到第二个接口 `eth1`，尝试按照如下手动手动配置：

  ```
  ifconfig eth1 192.168.32.254
  ```

- 4. 如果无法配置接口，它会返回如下消息：

  ```
  SIOCSFADDR: No such device
  ```

- 5. 在这种情况下，第二个接口尚未被识别。极可能是内核守护进程没有安装网络适配器模块（遗憾的是，内核配置器不会返回错误信息）。尝试手动加载模块。在我的情况下，我输入以下命令加载 `/lib/modules/2.0.31/net` 目录下的 `3c509.o` 模块：

  ```
  /sbin/modprobe 3c509
  ```

- 6. 如果成功，你将看到关于第二个接口的信息显示。如果没有，尝试重新加载模块并指定 I/O 地址和中断号 (`irq`)，如下例：

  ```
  modprobe 3c509 io=0x330, irq = 10
  ```
