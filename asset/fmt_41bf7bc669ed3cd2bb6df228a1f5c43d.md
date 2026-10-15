
| hosts | 主机名和号码 |

| netgroup | 网络范围的主机和用户列表，用于访问规则；glibc 2.1 之前的 C 库仅通过 NIS 支持 netgroups |

| network | 网络名称和号码 |

| passwd | 用户密码 |

| protocols | 网络协议 |

| publickey | NFS 和 NIS+ 使用的 SecureRPC 的公钥和密钥 |

| rpc | 远程过程调用名称和号码 |

| services | 网络服务 |

| shadow | 影子用户密码 |

### 表 38-10：NSS 配置服务

| 服务 | 描述 |

|---|---|

| files | 检查相应的 `/etc` 文件以获取配置（例如，hosts 的 `/etc/hosts`）；此服务对所有文件都有效 |

| db | 检查相应的 `/var/db` 数据库以获取配置；除 netgroup 外对所有文件都有效 |

| compat | 仅对 passwd、group 和 shadow 文件有效 |

| dns | 检查 DNS 服务；仅对 hosts 文件有效 |

| nis | 检查 NIS 服务；对所有文件都有效 |

| nisplus | NIS 版本 3 |

| hesiod | 使用 Hesiod 进行查找 |

操作项指定对特定服务采取的操作。操作项放在服务后的括号内。配置规范可以列出多个服务，每个服务都有自己的操作项。在以下示例中，network 文件的条目具有配置规范，说明检查 NIS 服务，如果未找到，则检查 `/etc/protocols` 文件：

```
protocols: nisplus [NOTFOUND=return] files
```

操作项由状态和操作组成。状态保存服务查找的可能结果，操作是在状态为真时要采取的操作。目前，可能的状态值是 `SUCCESS`、`NOTFOUND`、`UNAVAIL` 和 `TRYAGAIN`（服务暂时不可用）。可能的操作是 `return` 和 `continue`：`return` 停止配置文件查找过程，而 `continue` 继续进行到下一个列出的服务。在前面的示例中，如果记录在 NIS 中未找到，则查找过程结束。

这里显示的是当前 Red Hat `/etc/nsswitch.conf` 文件的副本，其中列出了常用的条目。注释和注释掉的条目以 `#` 符号开头。

`/etc/nsswitch.conf`

```
#
# /etc/nsswitch.conf
#
# An example Name Service Switch config file.
passwd:      files nisplus
shadow:      files nisplus
group:       files nisplus
hosts:       files nisplus dns
bootparams:  nisplus [NOTFOUND=return] files
ethers:      files
netmasks:    files
networks:    files
protocols:   files
rpc:         files
services:    files
netgroup:    nisplus
publickey:   nisplus
automount:   files nisplus
aliases:     files nisplus
```

#### 网络接口和路由：`ifconfig` 和 `route`

您系统通过特定的硬件接口（如以太网卡或调制解调器）连接到网络。通过此接口传输的数据随后被路由到您的网络。`ifconfig` 命令配置您的网络接口，`route` 命令相应地设置网络连接。如果您使用网络配置工具（如 `redhat-config-network`）配置接口，则无需使用 `ifconfig` 或 `route`。但是，如果您愿意，可以直接使用 `ifconfig` 和 `route` 配置接口。每次启动系统时，网络接口及其路由都必须建立。当您启动系统时，这由 `/etc/rc.d/init.d/network` 初始化文件为每个接口执行的 `ifconfig` 和 `route` 命令自动完成，该文件在您启动系统时执行。如果您手动添加自己的接口，则必须设置网络脚本以对新接口执行 `ifconfig` 和 `route` 操作。

#### 网络启动脚本：`/etc/rc.d/init.d/network`

在 Red Hat 上，您的网络接口使用 `/etc/rc.d/init.d` 目录中的 `network` 脚本启动。此脚本将激活您的网络接口卡 (NIC) 并实现网关、主机和名称服务器标识等配置信息。您可以使用此脚本以及 `restart`、`start` 或 `stop` 选项手动关闭和启动网络接口。您可以使用 `service` 命令在 Red Hat 上运行脚本。以下命令关闭然后启动您的网络接口：

```
service network stop
service network start
```

如果您正在更改网络配置，则必须重新启动网络接口才能使更改生效：

```
service network restart
```

要测试接口是否正常工作，请使用 `ping` 命令并提供网络上系统的 IP 地址，例如您的网关机器。`ping` 命令会不断重复，直到您使用 CTRL-C 停止它。

```
ping 192.168.0.1
```

#### 接口配置脚本：`/etc/sysconfig/network-scripts`

`/etc/rc.d/init.d/network` 文件通过执行位于 `/etc/sysconfig/network-scripts` 目录中的多个专用脚本来执行启动操作。`network` 脚本使用该目录中的名为 `ifup` 的脚本来激活网络连接，并使用 `ifdown` 来关闭它。`ifup` 和 `ifdown` 将调用针对正在操作的设备类型的其他脚本，例如使用 PPP 协议的调制解调器的 `ifup-ppp`，或使用 IP 协议版本 6 地址的网络设备的 `ifup-ipv6`。

注意 您可以使用从“系统工具”菜单访问的“网络设备控制”工具激活和停用网络接口。

如同使用发行版的网络管理工具或第三方工具如 `rp3` 或 `Webmin`。你也可以手动编辑这些接口配置文件，进行诸如是否在启动时启动接口之类的更改（尽管使用 `redhat-config-network` 之类的配置工具更容易）。下面展示了一个使用静态 IP 地址的 `ifcfg-eth0` 文件示例。对于 DHCP，请将 `BOOTPROTO` 设置为 `dhcp`。

```
DEVICE=eth0
BOOTPROTO=static
BROADCAST=192.168.0.255
IPADDR=192.168.0.1
NETMASK=255.255.255.0
NETWORK=192.168.0.0
ONBOOT=yes
```

#### `ifconfig`

`ifconfig` 命令以接口名称和 IP 地址以及选项作为其参数。然后 `ifconfig` 命令将 IP 地址分配给接口。你的系统现在知道这样的接口存在，并且它引用了一个特定的 IP 地址。此外，你可以指定 IP 地址是主机地址还是网络地址。你可以使用域名作为 IP 地址，前提是该域名连同其 IP 地址一起列在 `/etc/hosts` 文件中。`ifconfig` 命令的语法如下：

```
# ifconfig interface -host_net_flag address options
```

`host_net_flag` 可以是 `-host` 或 `-net`，以指示主机或网络 IP 地址。`-host` 为默认值。`ifconfig` 命令可以有多个选项，设置接口的不同特性，例如它可以传输的最大字节数（`mtu`）或广播地址。`up` 和 `down` 选项激活和停用接口。在下一个示例中，`ifconfig` 命令配置一个以太网接口：

```
# ifconfig eth0 192.168.0.1
```

对于这种简单的配置，`ifconfig` 会自动生成标准的广播地址和网络掩码。标准广播地址是网络地址，其主机地址数字为 255。对于 C 类网络，标准网络掩码是 255.255.255.0，而对于 A 类网络，标准网络掩码是 255.0.0.0。然而，如果你连接到具有特定网络掩码和广播地址的网络，则在使用 `ifconfig` 时必须指定它们。指定广播地址的选项是 `broadcast`；对于网络掩码，则是 `netmask`。表 38-11 列出了不同的 `ifconfig` 选项。在下一个示例中，`ifconfig` 包含网络掩码和广播地址：

```
# ifconfig eth0 192.168.0.1 broadcast 192.168.0.255 netmask 255.255.255.0
```

##### 表 38-11：`ifconfig` 选项

| Option | Description |

|---|---|

| Interface | 网络接口的名称，例如 `eth0` 表示第一个以太网设备，或 `ppp0` 表示第一个 PPP 设备（调制解调器） |

| up | 激活一个接口；如果指定了 IP 地址则隐含 |

| down | 使接口停用 |
