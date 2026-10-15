
SCAN 是用于为集群提供服务访问的名称。由于 SCAN 与整个集群关联而非特定节点，因此 SCAN 可以在无需重新配置客户端的情况下从集群中添加或删除节点。它还为数据库增加了位置无关性，使得客户端配置不必依赖于运行特定数据库的节点。客户端可以继续以以前版本相同的方式访问集群，但 Oracle 建议访问集群的客户端使用 SCAN。

注意：在典型（Typical）安装中，SCAN 提供的名称也是集群名称，因此 SCAN 名称必须满足集群名称的要求。在高级（Advanced）安装中，SCAN 和集群名称在安装期间在单独字段中输入，因此集群名称的要求适用于 SCAN 名称。

你可以使用 `nlookup` 命令来确认 DNS 是否正确与地址关联。例如：

```
root@node$ nlookup mycluster-scan
Server: dns.example.com
Address: 192.0.2.101
Name: mycluster-scan.example.com
Address: 192.0.2.202
Name: mycluster-scan.example.com
Address: 192.0.2.203
```

安装后，当客户端向集群发送请求时，Oracle Clusterware 监听器会将客户端请求重定向到集群中的服务器。

注意：Oracle 强烈建议你不要在 hosts 文件中配置 VIP 地址。请对 SCAN 使用 DNS 解析。如果你使用 hosts 文件解析 SCAN，你将只能解析到一个 IP 地址，并且只有一个 SCAN 地址。在 DNS 或 hosts 文件中配置 SCAN 是唯一支持的配置。不支持在网络信息服务 (NIS) 中配置 SCAN。另参阅：附录 D，“理解网络地址”

## 2.7.3 Oracle Grid Infrastructure 使用网络的广播要求

广播通信（ARP 和 UDP）必须在 Oracle Grid Infrastructure release 2 patchset 1 (2.1.0.2) 及更高版本使用的所有公共和私有接口上正常工作。广播必须跨越公共或私有接口使用的任何配置 VLAN 正常工作。

## 2.7.4 Oracle Grid Infrastructure 使用网络的多播要求

在 Oracle Grid Infrastructure release 2 (2.1) 中，每个集群成员节点守护进程在所有接口上均使用多播与集群中的其他节点通信。在 Oracle Grid Infrastructure release 2 patchset 1 (2.1.0.2) 及更高版本中，私有互连需要多播。出于这一原因，你至少必须为集群启用多播：

- 跨越为私有互连定义的广播域
- 在 IP 地址子网范围 `224.0.0.0/24` 和 `239.0.0.1/24` 上

你不需要跨越路由器进行多播通信。

## 2.7.5 用于向 Grid 命名服务进行委托的 DNS 配置

如果你计划使用 DNS 安装 Oracle Grid Infrastructure，你必须配置你的域名服务器 (DNS)，向集群成员节点子域发送 GNS 请求。以下是执行区域委托需要完成的操作概述。你的实际操作可能与此示例有所不同。

配置 DNS 使用委托发送 GNS 请求：

- 在 DNS 中为 GNS 虚拟 IP 地址创建一个条目，其中地址使用 `CLUSTERNAME.DOMAINNAME`。例如，如果集群名称为 `mycluster`，域名为 `example.com`，IP 地址为 `192.0.2.1`，则创建一个类似下面的条目：

```
mycluster-gns.example.com A 192.0.2.1
```

你提供的地址必须是路由的。

- 设置 GNS 子域到 GNS 虚拟 IP 地址的转发，以便 GNS 指向该虚拟 IP。为此，请在 DNS 中创建如下配置（假设使用 NS1）：

```
mycluster-gns.example.com NS ns1.example.com
```

- 在 DNS 中配置的 NS 记录解析当前未使用的地址：

```
ns1.example.com A 192.0.2.1
```

- 当使用 GNS 时，必须在 `/etc/resolv.conf` 中配置如下内容：

```
search example.com
nameserver mycluster-gns.example.com
```

注意：在使用 GNS 时，请注意使用 NIS 可能会产生问题。

## 2.7.6 Grid 命名服务配置示例

如果你使用 GNS，则需要将 GNS 虚拟 IP 委托到该静态 IP 地址。

当节点添加到集群时，GNS 服务器可以动态提供这些地址。由于 GNS 自动分配和配置地址，无需进一步配置。以下示例提供了关于 GNS 的信息，集群名称为 `mycluster`，域名为 `example.com`，子域为 `example.com`，`192.0.2` 代表公共 IP 地址，`192.168.0` 代表私有 IP 子网：

### 表 2-3 Grid 命名服务示例

| 身份 | 主机名 | 给定名称 | 类型 | 地址 | 地址分配方式 | 解析 |

| :--- | :--- | :--- | :--- | :--- | :--- |

| GNS VIP | 无 | 由集群选择 | mycluster-gns.example.com | 虚拟 | 192.0.2.1 | 网络管理员固定 | DNS |

| 节点 1 公共 | 节点 1 | node1 | 公共 | 192.0.2.101 | 固定 | GNS |

| 节点 1 VIP | 节点 1 | 由集群选择 | node-vip | 虚拟 | 192.0.2.104 | DHCP | GNS |

| 节点 1 私有 | 节点 1 | node1-priv | 私有 | 192.168.0.1 | 固定或 DHCP | GNS |

| 节点 2 公共 | 节点 2 | node2 | 公共 | 192.0.2.102 | 固定 | GNS |

| 节点 2 VIP | 节点 2 | 由集群选择 | node2-vip | 虚拟 | 192.0.2.105 | DHCP | GNS |

| 节点 2 私有 | 节点 2 | node2-priv | 私有 | 192.168.0.2 | 固定或 DHCP | GNS |

| SCAN VIP 1 | 无 | 由集群选择 | mycluster-scan.cluster01.example.com | 虚拟 | 192.0.2.201 | DHCP | GNS |

| SCAN VIP 2 | 无 | 由集群选择 | mycluster-scan.cluster01.example.com | 虚拟 | 192.0.2.202 | DHCP | GNS |

| SCAN VIP 3 | 无 | 由集群选择 | mycluster-scan.cluster01.example.com | 虚拟 | 192.0.2.203 | DHCP | GNS |

## 2.7.7 手动 IP 地址配置示例

如果您选择不使用 GNS，在安装之前必须配置公有、虚拟和私有 IP 地址。此外，请检查可以通过 `ping` 命令访问默认网关。要找到默认网关，请使用操作系统实用程序中描述 `route` 命令。

例如，在一个双节点集群中，每个节点都有一个公网接口和一个私有接口，并且您定义了一个 SCAN 域地址以供您的 DNS 解析到三个地址之一，您的接口配置可能如下表所示：

| 表格 2-4 手动网络配置示例 |

| 节点身份 | 宿主机节点 | 别名 | 类型 | 地址 | 分配方式 | 解析方式 |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| 节点 1 公网 | node1 | node1¹ | 公网 | 192.0.201 | 固定 | DNS |

| 节点 1 VIP | 由 Oracle Clusterware 选择 | node1-vip | 虚拟 | 192.0.204 | 固定 | DNS 和 hosts 文件 |

| 节点 1 私有 | node1 | node1-priv | 私有 | 192.168.0.1 | 固定 | DNS 和 hosts 文件，或无 |

| 节点 2 公网 | node2 | node2¹ | 公网 | 192.0.202 | 固定 | DNS |

| 节点 2 VIP | 由 Oracle Clusterware 选择 | node2-vip | 虚拟 | 192.0.2.105 | 固定 | DNS 和 hosts 文件 |

| 节点 2 私有 | node2 | node2-priv | 私有 | 192.168.0.2 | 固定 | DNS 和 hosts 文件，或无 |

| SCAN VIP 1 | 无 | 由 Oracle Clusterware 选择 | mycluster-scan | 虚拟 | 192.0.2.201 | 固定 | DNS |
