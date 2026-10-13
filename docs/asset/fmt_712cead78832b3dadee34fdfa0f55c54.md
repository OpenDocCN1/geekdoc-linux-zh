
## 配置 in-addr.arpa 区域

在上一节中，你学习了如何设置普通区域，该区域用于将名称解析到其 IP 地址。设置 `in-addr.arpa` 区域也是一个好主意。这允许外部 DNS 服务器找到属于传入 IP 地址的名称。设置 `in-addr.arpa` 区域不是强制要求，即使没有 `in-addr.arpa` 区域，你的 DNS 服务器也能正常工作。

创建 `in-addr.arpa` 区域的工作与在 DNS 中创建普通区域类似。你需要修改 `/etc/named.rfc1912.zones` 文件来定义 `in-addr.arpa` 区域。该定义可能如下：

```
zone "100.173.192.in-addr.arpa" {
    type master;
    file "192.173.100.zone";
};
```

注意，在 `in-addr.arpa` 中你始终使用 IP 地址的反向网络部分。在这种情况下，网络是 `192.173.100.0/24`，因此反向网络部分是 `100.173.192.in-addr.arpa`。对于其余部分，你只需要像创建普通区域时那样创建一个区域文件。在 `192.173.100.zone` 文件中，你定义 `PTR` 资源记录。在资源记录的第一部分，你将输入 IP 地址的节点部分。因此，如果节点的 IP 地址是 `192.173.100.1`，你将输入 `1`。然后你使用 `PTR` 指明它是反向 DNS 记录。对于最后部分，你将使用完整名称并以点结尾。这样的一行可能如下：

```
PTR    1    example.com.
```

在 `in-addr.arpa` 中，你始终使用 IP 地址的反向网络部分。

## 设置 DNS 服务器

在设置 `etc...11100.0.2`。

设置主 DNS 服务器。在 `/etc/named.rfc1912.zones` 中定义了这些。

设置 DNS 服务器。为了安全，你必须使用密钥来同步主从。在 `/etc/named.rfc1912.zones` 中定义了这些。

### 列表 14.5：为主添加参数

```
zone "example.com" {
    type master;
    file "example.com";
    notify yes;
    allow-update { 192.168.1.220 };
};
```

### 列表 14.6：创建 DNS

```
zone "example.com" {
    type slave;
    file "example.com";
    notify yes;
    allow-update { 192.168.1.151 };
};
```

# 设置 DHCP 服务器

要设置 DHCP 服务器，在安装 `dhcp` 包后，你需要在主配置文件 `/etc/dhcp/dhcp.conf` 中更改常用的 DHCP 设置。安装 `dhcp` 包后，该文件是空的，在 `/usr/share/doc/dhcp-<version>/dhcp.conf.sample` 中有一个良好的注释示例文件。你可以在列表 14.7 中看到默认参数。

### 列表 14.7：示例 dhcp.conf 文件

```
[root@hn1 dhcp-4.1.1]# cat dhcp
dhcp6d.conf.sample dhcp.conf dhcp-conf-to-ldap
[root@hn1 dhcp-4.1.1]# cat dhcp.conf.sample
# dhcp.conf
#
# Sample configuration file for ISC dhcp
#
```

```
# option definitions common to all supported networks...
option domain-name="example.org"
option domain-name-servers ns1.example.org, ns2.example.org;
```

```
default-lease-time: 600;
max-lease-time: 7200;
```

```
# Use this to enable / disable dynamic dns updates globally.
#ddns-update-style none;
```

```
# If this DHCP server is the official DHCP server for the local
# network, the authoritative directive should be uncomment.
#authoritative
```

```
# Use this to send dhcp log messages to a different log file (you
# have to hack syslog.conf to complete the redirection).
log-facility local7;
```

```
# No service will be given on this subnet, but declaring it helps the
# DHCP server to understand the network topology.
```

```
subnet 10.152.187.0 netmask 255.255.255.0 {
}
```

# This is a very basic subnet declaration.

```
subnet 10.254.239.0 netmask 255.255.255.224 {
range 10.254.239.10 10.254.239.20;
option routers rtr-239-0-1.example.org, rtr-239-0-2.example.org;
}
```

# This declaration allows BOOTP clients to get dynamic addresses,

# we do not readily recommend.

```
subnet 10.254.239.32 netmask 255.255.255.224 {
range dynamic-bootp 10.254.239.40 10.254.239.60;
option broadcast-address 10.254.239.31;
option routers rtr-239-32-1.example.org;
}
```

```
# A slightly different configuration for an internal subnet.
subnet 10.5.5.0 netmask 255.255.255.224 {
range 10.5.5.26 10.5.5.30;
option domain-name-servers ns1.internal.example.org;
option domain-name "internal.example.org";
option routers 10.5.5.1;
option broadcast-address 10.5.5.31;
default-lease-time 600;
}
```

# Hosts which require special configuration options can be listed in

# host statements. If no address is specified, the address will be

# allocated dynamically (if possible), but the host-specific information

# will still come from the host declaration.

```
host passacaglia {
hardware ethernet 0:c0:5d:bd:95;
filename "vmunix.passacaglia";
server-name "toccata.fugue.com"
}
```

# Fixed IP addresses can also be specified for hosts. These addresses

# should not also be listed as being available for dynamic assignment.

# Hosts for which fixed IP addresses have been specified can boot using

# BOOTP or DHCP. Hosts for which no fixed address is specified unless there is an address range on the subnet

# to which a BOOTP client is connected that has the dynamic-bootp flag

# set
