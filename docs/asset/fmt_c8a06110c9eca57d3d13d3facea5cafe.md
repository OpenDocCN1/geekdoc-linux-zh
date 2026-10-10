
## 3. 创建租约数据库
   - 输入 `touch /var/lib/dhcpd/dhcpd.leases` 以创建租约数据库。
   - 清屏。

## 4. 启动 dhcpd 服务
   - 输入 `service dhcpd start` 以启动 `dhcpd` 服务器。
   - 输入 `chkconfig dhcpd on` 以在启动时启动 `dhcpd` 服务器。
   - 清屏。

## 5. 检查 DHCP 设置是否已生效
   - 切换到标记为 `srvB` 的系统。
   - 输入 `system-config-network-tui` 以打开网络配置实用程序。
   - 通过选择 **Use DHCP** 选项启用 `eth0` 的 DHCP 支持。
   - 退出网络配置实用程序。
   - 输入 `service network restart` 以向 DHCP 服务器请求 IP 地址。
   - 输入 `ip addr` 以验证 IP 地址 `192.168.0.X/24` 是否已分配给 `srvB`。
   - 清屏。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_529_0.png)

# 主题 D
# 配置 DNS

你已配置 DHCP 服务以自动为网络系统分配 IP 地址。要连接到网络计算机并访问其资源，你需要知道其 IP 地址或其名称。DNS 在网络中翻译和解析 IP 地址及其等效的主机名或域名。在本主题中，你将配置 DNS。

网络中的计算机通过 IP 地址彼此识别。然而，网络用户很难记住 IP 地址。因此，网络计算机和设备的 IP 地址被描述性名称取代，以便用户定位网络资源并在它们之间共享信息和服务。IP 地址与其描述性名称之间的转换由 DNS 处理，这需要由网络管理员进行配置。

## 域名系统

域名系统（DNS）是一个分布式、分层数据库系统，维护网络中域名及其等效 IP 地址的信息。它使用这些信息将完全限定域名转换为数字 IP 地址，或反之亦然。网络计算机使用 IP 地址来定位、连接和彼此通信。DNS 将 IP 地址转换为相应的域名。它像一个中心系统一样工作，以确保网络上没有重复的域名和 IP 地址。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_530_0.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_530_1.png)

## DNS 实用工具

使用各种实用工具来解析 DNS 主机名。一些解析实用工具包括 `dig`、`host` 和 `nslookup`。

## 域名

**定义：**

*域名* 是赋予 *域* 的标签，该域是存储在 DNS 中的分层数据结构中的一个节点。它是从该节点到根节点的所有标签的拼接。域名由字符串表示，每个节点由一个点（`.`）分隔。每个域名在其父域内是唯一的。

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_531_0.png)

### 子域

子域是较大域名的一部分。DNS 层次结构包括根级域，其次是顶级域、二级域和子域。每个顶级域包含子域，这些子域被称为子域。

### 完全限定域名（FQDN）

*完全限定域名（FQDN）* 是在全球网络中唯一识别系统的方法。完整的域名由主机名、二级域和顶级域组成。

## 区域

**定义：**

*区域* 是 DNS 树结构中的一个委托点，映射到一个域。一个区域可以映射到包含所有子域的整个域，或者映射到域的具体部分。每个区域将有一个权威名称服务器或一个或多个辅助名称服务器。区域有两种类型：正向和反向。

示例：

![](img/477ccb2f05b6ba1b2d563ea74f18c197_532_0.png)

图 12-27：使用区域进行域委派。

## 正向区域和反向区域

两种主要的 DNS 区域是正向区域和反向区域。

| 区域 | 描述 |
| :--- | :--- |
| *正向区域* | 用于将主机名映射到 IP 地址的区域。它包含有关分配给 DNS 服务器获取更新的时间的信息。 |
| *反向区域* | 用于将 IP 地址映射到主机名的区域。反向区域可用于解析域名的 IP 地址，以追踪未授权用户。 |

## 区域文件

*区域文件* 包含关于特定命名空间的信息，这些信息对于将域名解析为 IP 地址是必要的。每个区域文件都包含资源记录，并可选项地包含指令。区域文件中的注释添加在分号之后。区域文件的命名依据 `named.conf` 文件中区域语句的 `file` 选项设置的值。默认情况下，区域文件存储在 `/var/named` 目录中。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_532_1.png)

区域文件

![](img/477ccb2f05b6ba1b2d563ea74f18c197_533_0.png)

**图 12-28：** *一个正向区域文件。*

### 根提示

根提示是 DNS 服务器中包含主机信息的文件，包括根 DNS 服务器的名称和地址。它用于定位权威 DNS 服务器并解析权威 DNS 域之外的名称。

### 命名空间

*命名空间* 是名称中对于 DNS 功能而言必须唯一的部分。对于任何给定域，子域中不得包含两个同名主机或子域。

### 区域文件语法

编写区域文件的语法如下：

```
$TTL time to live in seconds

$ORIGIN domain name

$INCLUDE file name

@ IN SOA master server name

  email address of the domain administrator

  (

    serial number

    time in seconds to refresh

    time in seconds to retry

    minimum TTL in seconds

  )

  IN DNS Record

  DNS server name

  IN DNS Record

  preference value

  mail server name

  hostname IN A IP address

  alias name IN CNAME real name of the host
```
