

# **balance-tlb or 5**

自适应传输负载均衡：一种无需任何特殊交换机支持的通道绑定。传出流量根据每个从设备当前的负载（相对于速度计算）进行分配。传入流量由当前从设备接收。如果接收从设备发生故障，另一个从设备将接管故障接收从设备的 MAC 地址。

# **balance-alb or 6**

自适应负载均衡：包含 balance-tlb 加上用于 IPv4 流量的接收负载均衡（rlb），并且不需要任何特殊交换机支持。接收负载均衡通过 ARP 协商实现。绑定驱动程序拦截本地系统发出的 ARP 回复，并在其传出时用绑定中某个从设备的唯一硬件地址覆盖源硬件地址，使得不同的对等方对服务器使用不同的硬件地址。

那么你应该使用哪种绑定模式？这可能是一个难以回答的问题，因为不同的网络对某些模式的支持更好。我的建议是尝试一些不同的绑定模式，并在 ping 服务器的同时拔掉一根网线来测试其故障转移。不同的模式对端口故障的处理方式不同，尤其是在网线重新连接（或交换机重启）且端口需要 30 秒左右才能恢复的情况下。在某些绑定模式下，ping 将会持续进行且没有中断，而在其他模式下，端口恢复期间你可能会有 30 秒的中断。请注意，因为绑定模式是在绑定模块加载时设置的，如果你更改绑定模式，你可能需要重启（或至少关闭 bond0 接口并卸载然后重新加载模块）。在本示例中我选择绑定模式 1，因为它一次只有一个端口处于活动状态，因此在任何交换机上都相对安全。

配置绑定的第一步是安装 ifenslave 包：

```
sudo apt-get install ifenslave
```

该包包含 ifenslave 实用程序，系统将使用它将两个接口绑定在一起。下一步是打开 /etc/modprobe.d/ aliases（如果不存在则创建它），滚动到文件底部，并添加

```
alias bond0 bonding
options bonding mode=1 miimon=100
```

options 行是你用来更改绑定模式的地方。miimon 选项告诉内核以毫秒为单位多久检查一次接口的链路状态。在本例中，每 100 毫秒检查一次。

下一步是打开你的 /etc/network/interfaces 文件并注释掉你将要绑定的网络接口的任何配置行（你可能只有 eth0 的配置）。此外，如果你有任何对 auto eth0 的引用，也将其注释掉。然后为 bond0 接口创建一个新的配置，其设置模仿你之前为 eth0 设置的设置。在 bond0 配置的最后，你添加一个名为 slaves 的额外行，列出你想要绑定在一起的不同接口。以下是我的服务器的 interfaces 文件示例：

```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
#auto eth0
#iface eth0 inet static
#    address 192.168.0.5
#    netmask 255.255.255.0
#    gateway 192.168.0.1

auto bond0
iface bond0 inet static
    address 192.168.0.5
    netmask 255.255.255.0
    gateway 192.168.0.1
    slaves eth0 eth1
```

保存更改后运行 sudo service networking restart 或 sudo /etc/init.d/networking restart。一旦运行 ifconfig，你应该能看到新的 bond0 设备：

```
$ sudo ifconfig

bond0     Link encap:Ethernet  HWaddr 00:0c:29:28:13:3b
          inet addr:192.168.0.5  Bcast:192.168.0.255  Mask:255.255.255.0
          inet6 addr: fe80::20c:29ff:fe28:133b/64 Scope:Link
          UP BROADCAST RUNNING MASTER MULTICAST  MTU:1500  Metric:1
          RX packets:38 errors:0 dropped:0 overruns:0 frame:0
          TX packets:43 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:16644 (16.2 KB)  TX bytes:3282 (3.2 KB)

eth0      Link encap:Ethernet  HWaddr 00:0c:29:28:13:3b
          UP BROADCAST RUNNING SLAVE MULTICAST  MTU:1500  Metric:1
          RX packets:37 errors:0 dropped:0 overruns:0 frame:0
          TX packets:43 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:16584 (16.1 KB)  TX bytes:3282 (3.2 KB)
          Interrupt:17  Base address:0x1400

eth1      Link encap:Ethernet  HWaddr 00:0c:29:28:13:3b
          UP BROADCAST RUNNING SLAVE MULTICAST  MTU:1500  Metric:1
          RX packets:1 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:60 (60.0 B)  TX bytes:0 (0.0 B)
          Interrupt:18  Base address:0x1480

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:16436  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

现在你可以通过在 ping IP 的同时拔掉 eth0 来测试故障转移。每当某个接口宕机时，内核都会同时记录到 dmesg 和 /var/log/syslog。以下是如果你拔掉 eth0 时会看到的示例日志条目：

