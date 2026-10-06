

# 第四部分 ♦ 在 SUSE Linux 中实现网络服务

## 主机规范

如果您有特定的主机需要特殊设置，可以在 `dhcpd.conf` 中的 `host` 部分进行设置。

要使主机规范生效，您需要指定要配置的机器的硬件地址。可以通过在机器上对相关接口执行 `ifconfig` 命令来找到该地址。参见列表 20-2 的示例。

### 列表 20-2：ifconfig 的输出

```
eth0-# ifconfig
eth0  Link: HWaddr 00:03:ff:69:68:12
      inet addr:192.168.131.70 Broadcast:192.168.131.255 Mask:255.255.255.0
      inet addr:fe80:203:fff:69:68/64 Scope:Link
      UP BROADCAST MULTICAST RUNNING MULTICAST MTU:1500  Metric:1
      RX packets:30256 errors:0 dropped:0 overflows:0 frame:0
      TX packets:35690 errors:0 dropped:0 overflows:0 carrier:0
      collisions:0 txqueuel:1000
      RX bytes:404865 (3.8 Mb) TX bytes:34473633 (32.8 Mb)
      Interrupt:1 Base address:0x1080
```

您可以在上述 `ifconfig` 的输出中找到 `eth0` 接口的硬件地址（HWaddr） 00:03:ff:69:68:12。

一旦找到了目标机器的硬件地址，您可以在 `/etc/dhcpd.conf` 中定义一个主机条目。

```
host {
  option host-name "bible.wiley.com";
  hardware ethernet 00:03:ff:69:68:12;
  fixed-address 192.168.0.8;
}
```

主机配置的重要部分是 `hardware ethernet` 和 `fixed-address` 参数：

- *hardware ethernet 参数需要是通过 `ifconfig` 命令指定的 HWaddr。
- *fixed-address 参数将是专门用于此主机的 IP 地址。

## 定义主机组

如果您需要为一组机器指定显式配置，可以使用组定义（group definition）。组定义允许您定义一组具有特定配置的机器，该配置同时也继承全局配置。请考虑列表 20-3。

### 列表 20-3：定义主机组

```
group {
  option subnet-mask 255.255.255.0;
  option domain-name-server 192.168.0.2, 192.168.0.3;
  option domain-name "wileybible.com";

  host bible {
    option host-name "bible.wiley.com";
    hardware ethernet 00:03:FF:69:12;
    fixed-address 192.168.0.8;
  }

  host sospan {
    option host-name "sospan.wiley.com";
    hardware ethernet 00:03:FF:69:13;
    fixed-address 192.168.0.9;
  }
}
```

我们现在有两台机器，bible 和 sospan，它们在 `dhcpd.conf` 中被定义为静态主机。专门针对这些机器，我们只定义了它们的主机（host-name）和 IP 地址（fixed-address）。由于我们定义了一个包含这些主机的组，这些主机还继承了子网掩码、DNS 服务器和域名设置。

> 确保您在定义组时不要忘记开启和闭合大括号。

## 指定租期（Leases）

DHCP 在有限的时间内保留其信息。您可以使用 `default-lease-time` 指定客户端保留 DHCP 信息的时间（以秒计）。如果客户端没有指定过期时间，将使用服务器的偏好。如果客户端指定了租期，服务器可以强制执行最大时间 `max-lease-time` 来覆盖客户端的偏好。

同时指定这两个选项为客户端持有 DHCP 配置的租期设置上下限制。（再次，您需要向 /etc/dhcpd.conf/ 添加这些选项。）

```
default-lease-time 43200 # 12 小
max-lease-time 86400 # 24 小
```

此示例指定了 12 小时的下限，以及在客户端续租租期之前 24 小时的上限。

## 其他 DHCP 选项

当您有许多必须配置的客户端机器时，DHCP 是一个极其强大的配置工具。它不仅限于 IP 地址分配，还可以扩展到涵盖很大比例的网络配置，从 WINS 服务器到网络时间服务器。

查看 `dhcp-options` 页面以获取更多关于您的 DHCP 服务器可以向网络客户端提供的选项的信息。

## 启动和停止 DHCP 客户端

为了使用 DHCP，您的客户端机器必须知道如何实际向网络发送请求进行配置。在 SUSE 中，您可以使用 YaST 的网络配置（网络设备：网卡）来使用 DHCP 配置网络接口。发送 DHCP 请求的另一种方法是使用 `ifup-dhcp`。在无线网络中，如果想临时启动接口，可以使用 `ifup-dhcp`：

```
ifup-dhcp eth0
```
这将启动 DHCP 并将其附加到 eth0 接口。如果您需要从网络移除 DHCP 客户端，请使用 `ifdown-dhcp`：

```
ifdown-dhcp eth0
```
这将从网络移除 DHCP。

## 排除 DHCP 客户端和服务器的故障

在启动或使用 DHCP 服务器时，您很少会遇到问题。另一方面，DHCP 客户端的问题非常常见，通常是由于存在多个 DHCP 服务器。本节提供了识别和解决 DHCP 问题的提示。在 DHCP 环境中看到的绝大多数问题与客户端有关。无论 DHCP 类型如何，您都可以使用 `dhcd` 工具来检查它们正在获取的信息。要使用该工具，请在以太网上执行 `dhcd-test` 命令。

### 列表 20-4：从 DHCP 服务器检索信息

```
dhcd-test eth0
dhcd: MAC address = 00:02:2d:31:b8:c8
IPADDR=192.168.6.242
NETMASK=255.255.255.0
NETWORK=192.168.6.0
BROADCAST=192.168.6.255
GATEWAY=192.168.6.1
```

您可以使用 `dhcpdump` 获取有关网络上 DHCP 流量的更多详细信息。`dhcp-tools` 包提供的 `dhcpdump` 命令可以通过 `tcpdump` 命令从数据包中过滤 DHCP 相关信息，如列表 20-5 所示。

### 列表 20-5：使用 tcpdump

```
# tcpdump -len -s 1500 | tcpdump
Error in packet:
TIME: 01:27:46.168382
IP: 192.168.6.200124 (00:30:65:27:f7:0e) > 255.255.255.254 (ff:ff:ff:ff:ff:ff)
OP: 60 (Boot file size) HTYPE: 49 (null)
HLEN: 52
HOPS: 50
XID: 3e103537
SECS: 14112
FLAGS: 33c
CIADDR: 49.32.68.77
YIADR: 67.80.32.83
SIADDR: 69.82.86.69
GIADDR: 82.32.79.102
CHADDR: 66:55:72:65:64:20:20:20:20:20:7c:20
NAME: ordering: 192.168.6.243 To: 00112F8D94B8 By: 192.168.6.200.
NAME:

Error in packet:
TIME: 01:28:15.044104
IP: 192.168.6.2190 (00:26:05:27:f7:0e) > 192.168.6.2190 (ff:ff:ff:ff:ff:ff)
OP: 016 (SMTP server) HTYPE: 105 (Static route)
```

