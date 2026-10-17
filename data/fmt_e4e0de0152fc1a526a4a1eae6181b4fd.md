
`send host-name "<hostname>"`

```
该请求从 DHCP 服务器中提取特定信息。如果 `send host-name` 指令指定了主机名，则从下述请求指令所指定的列表中删除 `host-name` 选项。有关所注命令的更多信息见表 11-2。
```

`request subnet-mask, broadcast-address, time-offset, routers, domain-name, domain-name-servers, host-name, netbios-name-servers, netbios-scope;`

| 指令 | 说明 |
| --- | --- |
| send | 为后续的指令提供信息 |
| host-name | 指定主机名 |
| request | 请求与后续指令相关的信息 |
| subnet-mask | 指定子网掩码，也称为网络掩码 |
| broadcast-address | 指定广播地址 |
| time-offset | 指定相对于 UTC 的偏移量（单位为秒） |
| routers | 指定路由器 |
| domain-name | 指定域名 |
| domain-name-servers | 指定域名服务器 |
| netbios-name-servers | 指定 NetBIOS 服务器 |
| netbios-scope | 指定 NetBIOS 范围 |
| **表 11-2.** | dhclient.conf 中的建议指令 |

`/etc/sysctl.conf` 中的指令以及 `/proc` 目录下的关联文件在过去的不同的 Ubuntu 版本中有所不同，因此如果指令再次发生变化，请不要惊讶。请参考当前的 `/etc/sysctl.conf` 获取最新信息。

# Ubuntu/hosts

在 DNS 流行之前，主机名和 IP 地址被存储在 `/etc/hosts` 静态文件中。当本地系统查找 IP 地址时，某些应用程序引用 `/etc/hosts` 配置文件来确定要查询的数据库。

```
127....1111.....，
在 /etc/hosts
，
是....。以下是一个在 /etc/hosts 配置文件中列出的条 地址：
```
127.0.0.1 localhost
192.168.0.60 laptop
```

# /etc/resol.许多

为网络为本地etc/一个etc/hosts 文件，为 DNSetc/etccp3/dhclient.conf 配置文件中包含了所有 IP 地址，这通常是错误。

# /etc/nsswitch.conf

大多数应用程序查看 `/etc/nsswitch.conf` 配置文件中的一行来确定名称搜索顺序。

```
hosts: files dns
```

# /etc/network/interfaces

Ubuntu 系统的默认网络设置存储在 `/etc/network/interfaces` 配置文件中。该文件对 Linux 用户来说可能很晦懂，我们将逐行分析我系统中的版本。首先，`auto` 指令识别要配置的网络接口——在本例中环环适配器，如 `lo` 标签所示：

```
auto lo
```

## 第 11 章：网络配置与故障排除

如果没有 `auto` 指令，指定的接口在下次你管理地运行 `/etc/init.d/networking restart` 脚本或 `ifup -a` 命令时将不会激活。

但该指令不会自动配置回环适配器。接口也需要配置，这就是 `iface` 指令的作用。它将由 `inet` 指令定义的 IPv4 网络（IPv6 网络将使用 `inet6` 配置）以及回环地址应用到回环适配器 `lo` 上：

```
iface lo inet loopback
```

接的一组指令说明了它们的顺序并不关键重要。随后的指令（如 `static` 指令所示）为接口 `eth0` 指定了使用 IPv4 地址的静态配置：

```
iface eth0 inet static
```

要配置 DHCP 客户端，将 `static` 替换为 `dhcp`。在这种情况下，接口不需要进一步的信息，因为它们通常由远程 DHCP 服务器配置。

假设是静态配置，此处显示指定的 IP 地址：

```
address 192.168.0.104
```

接下来配置子网掩码（network mask 的缩写）和网关地址。`gateway` 指令指定与默认路由相关的 IP 地址。

```
netmask 255.255.255.0
gateway 192.168.0.1
```

> 如果你没有 DHCP 服务器上配置 DNS 服务器，可以通过以下方式进行：

```
dns-namesvers 68.87.69.146 68.87.85.98
```

最后，以下内容根据扩展集标识（ESSID）配置特定的无线网络 ID。这里的 `wireless-essid` 指令命名了你的家庭无线网络 ID kiedrickens（以我们的狗和猫命名）：

```
wireless-essid kiedrickens
```

`/etc/network/interfaces` 文件还有其他可用指令。表 11-3 列出了常用的指令，包括已描述的指令。

## 其他 /etc/network/ 配置文件

`/etc/network/` 配置文件包含了在网络启动或停止时运行的脚本。这些脚本都位于 `/etc/network` 的子目录下，并在表 11-4 中进行了描述。位于 `if-up.d/` 或 `if-pre-up.d/` 子目录下的脚本通过 `ifup` 命令激活。位于 `if-down.d/` 或 `if-post-down.d/` 子目录下的脚本通过 `ifdown` 命令禁用。

### Ubuntu 服务器管理

| 指令 | 用途

| --- | --- |

| auto | 识别网络设备文件，如 lo 和 eth0 |

| allow-hotplug | 支持网络接口的热插即用访问 |

| iface | 识别与设备关联的网络地址系统和类型 |

| lo | 标记回环适配器 |

| eth0 | 指定第一个以太网；使用与网络设备文件相同的名称，如 eth1、ath0、wlan0 等 |

| static | 指定静态 IP 地址 |

| dhcp | 将关联设备指向 DHCP 服务器 |

| bootp | 将网络设备指向远程网络上的 DHCP 服务器 |

| inet | 配置 IPv4 网络 |

| inet6 | 配置 IPv6 网络 |

| address | 位于静态 IP 地址之前 |

| netmask | 位于静态 IP 地址子网掩码之前 |

| gateway | 位于网络默认网关 IP 地址之前 |

| hwaddress | 位于硬件地址之前 |

| hostname | 指定主机名 |

| network | 指定网络地址 |

| dns-nameserver | 分配 DNS 服务器 |

表 11-3. 常见的 /etc/network/interfaces 指令

在表 11-4 列出的目录中可以配置其他几个服务。例如，当我在另一个 Ubuntu 系统上配置 SSH 和 Postfix 服务器时，相关的脚本会被添加到 `/etc/network/if-up.d/` 目录。

## 无线网络

经验用户一想到通过无线网络连接服务器就会不之而栗，至少有两个原因：此类网络比有线网络不可靠，且更容易受到干扰。但随着 802.11 网络的上线将将用户配置通过无线网络连接的服务器。为此，Ubuntu 服务器管理员需要掌握与无线网络相关的基本配置命令。本节涵盖了 `iwlist`、`iwconfig`、`iwgetid` 命令。

但重要的是要意识到 Linux 和 Ubuntu 并不支持所有的网卡。确定哪些网卡被支持可能是困难的。Ubuntu 在 https://help.ubuntu.com/community/WifiDocs/WirelessCardsSupported 提供了支持网卡的当前列表。如第 1 章所示，某些无线支持基于 Ubuntu 限制存储库中的专有驱动。

如果你的无线网卡没有在 wiki 或其他 Linux 相关的列表中，下一步是使用 `iwconfig` 命令查找更多信息。

| 脚本 | /etc/network 的子目录 | 用途 |

| --- | --- | --- |

| wireless-tools | if-up.d/, if-post-down.d | 激活和禁用无线接口 |

| wpas supplicant | all | 读取并使用无线网络的 WPA 密钥（可用）；在四个目录中均相同 |

| mountfs | if-up.d/ | 挂载在 /etc/fstab 中配置的 NFS 文件系统 |

| ntpdate | if-up.d/ | 如果配置为启动启动，则启动 NTP 服务 |

表 11-4. 典型的 /etc/network 脚本

# 第 11 章：网络配置与故障排除

| 输出 | 说明 |

| --- | --- |
