
```
subnet 192.168.1.0 mask 255.255.255.0 (
  range 192.168.1.116 192.168.1.127;
  default-lease-time 14000;
  max-lease-time 172800;
  host hacker {
    fixed-address 192.168.1.1;
    hardware ethernet 00:00:1c:b5:5a:58;
  }
}
```

注意这些固定主机位于子网声明内部。同样注意行尾分号的重要性。

# 其他选项

您可以在文件开头添加 `authoritative` 关键字。如果您这样做，这意味着您的 DHCP 服务器是控制该子网服务的服务器；客户端随后将忽略网络上的任何“流氓”服务器。

> 在有其他运行的网络上测试 DHCP 服务器不是好主意。在公共网络上提供错误范围的流氓 DHCP 服务器会导致严重的混乱并非常不受欢迎。

> 要让 `dhcpd` 在系统启动时启动，使用 `systemconfig -a dhcpd`。

## 定义主机组

如果您需要为一组指定显式配置，可以使用组定义。组定义允许您定义一组具有特定配置的主机，该配置还继承全局配置。请考虑列表 20-1。

### 列表 20-1

```
group {
  option subnet-mask 255.255.255.0;
  option domain-name-servers 192.168.1.254, 62.30.112.39;
  option domain-name "disruptive.org.uk";

  host bible {
    option host-name "bible.disruptive.org.uk";
    hardware ethernet 00:03:FF:69:68:12 fixed-address 192.168.1.8;
  }
  host sospan {
    option host-name "sospan.disruptive.org.uk";
    hardware ethernet 00:03:FF:69:68:13 fixed-address 192.168.1.9;
  }
}
```

> 定义组时，确保不要忘记打开和结束括号。

# 第四部分

## 在 SUSE Linux 中实现网络服务

此示例指定了 12 小时的下限和 24 小时的上限，直到客户端重新租租约为止。

```
default-lease-time 43200 # 12 小时
max-lease-time 86400 # 24 小时
```

## 其他 DHCP 选项

当你有许多必须配置的客户端机器时，DHCP 是一个极其强大的工具。它不仅局限于 IP 地址分配，还可以扩展到网络配置的大部分内容，从 WINS 服务器到网络时间服务器。

你还可以定义选项，允许从网络启动的机器从服务器获取启动镜像，只要也设置了简易文件传输协议 `TFTP`，无盘客户端就可以从 DHCP 服务器启动。`dhcp-options` 帮助页（`man` page）提供了关于你的 DHCP 服务器可以向网络客户端呈现的选项的更多信息。

## 启动和停止 DHCP 客户端

为了能够使用 DHCP，你的客户端机器必须知道如何向网络发送 DHCP 请求进行配置。在 SUSE 中，你可以使用 YaST 的网络配置（网络设备 网卡）来配置使用 DHCP 的网络接口。

另一种启动 DHCP 请求的有用方法是使用 `ifup-dhcp` 和 `ifdown-dhcp`。如果你在使用无线网络，或者如果你想临时使用 DHCP 启用网络接口，可以使用 `ifup-dhcp` 命令：

```
~ ifup-dhcp eth0
Starting DHCP Client Daemon on eth0 . . .
```

此命令启动 DHCP 客户端并将其附加到 `eth0` 接口上。

如果你想从网络接口中移除 DHCP 客户端并移除其动态配置，你需要使用 `ifdown-dhcp` 命令：

```
~ ifdown-dhcp eth0
```

这将从指定的网卡（在本例中为 `eth0`）中移除 DHCP 客户端。

如果你正在使用 `NetworkManager`，重启 `NetworkManager` 或在其中选择不同的网络，将重新启动 DHCP 客户端。

你也可以使用 `dhclient` 命令手动运行 DHCP 客户端。

## 配置和使用 DHCP 服务

```bash
root@bible: # dhclient
Internet Systems Consortium DHCP Client V3.0.6
Copyright 2004-2007 Internet Systems Consortium.
All rights reserved.
For info, please visit http://www.isc.org/sw/dhcp/
Listening on LPF/eth0:00:16:6f:62:30
Sending on LPF/eth1:00:16:6f:62:30
Listening on LPF/eth0:15:c5:0c:2f:5a
Sending on LPF/eth0:15:c5:0c:2f:5a
DHCPDISCOVER on eth0 to 255.255.255.255 port 67 interval 5
DHCPPOFFER from 192.168.1.254 interval 2
DHCPDISCOVER on eth0 to 255.255.255.255 port 67 interval 5
DHCPREQUEST on eth0 to 255.255.255.255 port 67
DHCPACK from 192.168.1.254
bound to 192.168.1.4 - renewal in 1537 seconds.
```

在这里我们看到 DHCP 客户端尝试了两个网络（`eth0` 和 `eth1`），并从 DHCP 服务器 `192.168.1.254` 获取了地址 `192.168.1.254`。如果你查看 `/var/log/messages`，我们将看到相同事件的记录：

```
Jan 16 11:10:58 rogerwhittaker dhcpd: DHCPDISCOVER from 00:15:c5:0c:2f:5a via eth1
Jan 16 11:10:58 rogerwhittaker dhcpd: DHCPPOFFER on 192.168.1.4 to 00:15:c5:0c:2f:5a via eth0
Jan 16 11:11:02 rogerwhittaker dhcpd: DHCPREQUEST for 192.168.1.4 (192.168.1.254) from 00:15:c5:0c:2f:5a via eth0
Jan 16 11:11:03 rogerwhittaker dhcpd: DHCPACK on 192.168.1.4 to 00:15:c5:0c:2f:5a via eth0
```

## 故障排除 DHCP 客户端和服务器

你很少会遇到启动或使用 DHCP 服务器的问题，这使得这些问题在发生时更加令人沮丧。另一方面，DHCP 客户端问题非常常见，通常是由于网络中存在多个不同步的 DHCP 服务器。本节提供了一些识别和解决 DHCP 客户端服务器问题的技巧。

### 故障排除 DHCP 客户端

你在 DHCP 环境中看到的大多数问题与从 DHCP 服务器获取错误信息的 DHCP 客户端有关。这几乎总是人们在其他系统上启动了相同 IP 地址范围或完全不同 IP 地址范围的 DHCP 服务器导致的。

如果你系统上的 DHCP 客户端获取的 IP 地址与 DHCP 服务器交付的范围相同，但其任何方面都不同，则你需要寻找网络中的另一个 DHCP 服务器。如果你系统上的 DHCP 客户端获取的 IP 地址与网络范围完全不同，那么你的网络中可能存在配置错误的 DHCP 服务器。无论 DHCP 客户端获取的信息类型如何，你都可以使用 `dhcp` 工具进行检查。要使用此工具，请查看示例 20-2。

#### 使用 dhclient 获取 DHCP 信息

```
root@bible: # dhclient
eth0:DHCPDISCOVER from broadcast to 255.255.255.255 port 67, 5
eth0:0CPPOFFER from 192.168.1.2542 155.2222..2222222222222.25555 

eth:::CP from broadcast to 192.168.1.254 port 675  2.25.2.2555555552222.2122222222222.2...2..222222..2.5.. 65
eth0:CP5ACK to 192.168.1.254 port 67 from 5
 
eth0:bound to 192.168.1.4, lease for 1537 seconds
```

## 故障排除 DHCP 服务器
