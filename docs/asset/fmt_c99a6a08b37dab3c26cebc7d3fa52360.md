
# 第七部分：网络管理

## DHCP 动态 DNS 更新

对于同时也支持域名系统服务器（DNS）的网络，IP 地址的动态分配目前需要解决一个主要限制：DHCP 需要与 DNS 服务器同步。DNS 服务器将主机名与特定的 IP 地址关联，而在动态分配的情况下，DHCP 服务器随机将自己的 IP 地址 分配给不同的主机。这些地址可能与或与 DNS 服务器期望与主机名关联的 IP 地址相同。该问题的解决方案正在开发中，被称为动态 DNS（Dynamic DNS）。通过动态 DNS，DHCP 服务器能够自动向 DNS 服务器更新 DHCP 分配给主机的 IP 地址。

或者，如果你想通过固定地址静态地同步你的 DHCP 和 DNS 服务器，你可以配置 DHCP 将这些固定地址分配给主机。然后，你让 DHCP 服务器执行 DNS 查询以获取它应该分配的 IP 地址，或者在 DHCP 配置文件中手动分配 IP 地址。执行 DNS 查询的优势是在一个地方（即 DNS 服务器）同步 IP 地址。

DHCP 服务器具有动态更新 BIND DNS 区域配置文件的能力。如第 36 章所述，可以通过在 `named.conf` 文件中指定 `allow-update` 选项来启用 DNS 服务器上区域的动态更新。此外，强烈建议你使用 TSIG 签名密钥（参见第 36 章）来引用和验证 BIND 和 DHCP 服务器。目前，DHCP 使用中间更新方案（Interim Update Scheme）来执行动态 DNS 更新，取代了早期的即时 DNS 更新（Ad-Hoc DNS Update）。最终版本将在未来的 DHCP 版本中实现。你可以在 `dhcp.conf` 页面中找到有关动态 DNS 的详细信息。

启用 TSIG 密钥的使用涉及同步 DHCP 和 DNS 服务器的配置。两者都必须配置为对相同域使用相同的密钥。首先，你需要按照第 36 章所述，使用 `dnssec-keygen` 创建一个共享秘密 TSIG 签名密钥。在 DNS 服务器中，在服务器的 `named.conf` 文件中使用 TSIG 声明和 `allow-update` 条目，如下例所示：

```
key mydhcpserver {
  algorithm-MD5;
  secret "abcdef1234";
}
```

```
zone "mytrek.com" {
  type master;
  file "mytrek.com";
  allow-update (key mydhcpserver);
}
```

```
zone "1.168.192.in-addr.arpa" {
  type master;
  file "192.168.0";
  allow-update (key mydhcpserver);
}
```

## 第 37 章：网络自动配置：IPv6、DHCP 和 DHCP

在 DHCP 服务器中，你在服务器的 `dhcp.conf` 文件中提供相应的 TSIG 声明和 `allow-update` 条目，如此示例所示。密钥声明与 DNS 服务器具有相同的语法。区域语句用于指定域的 IP 地址和使用的 TSIG 密钥。域名和 IP 地址在 DNS 和 DHCP 服务器的配置文件中完全匹配。与 `named.conf` 文件不同，`dhcp.conf` 文件中没有域名或 IP 地址。区域语句中使用。密钥语句列出了使用的密钥。DHCP 服务器将驱动 DNS 服务器更新，建议你通过 `primary` 语句显式地标识它们。

```
key mydhcpserver {
  algorithm-MD5;
  secret "abcdef1234";
};
```

```
zone "mytrek.com" { #domain to update
    primary 192.168.0.1;
    address of DNS server
    key mydhcpserver
};
```

```
zone "192.168.0.in-addr.arpa" {
    primary 192.168.0.1;
    key mydhcpserver
    domain to update
    address of DNS server
};
```

为了生成完全限定主机名，DHCP 服务器通常使用它自己的域名和主机名（参见 `dhcp.conf` 中的异常情况）。如果你想为主机分配特定主机名，可以在子网部分使用 `dns-hostname` 语句指定它。域名在 `domain-name` 选项中指定：`"mytrek.com"` DNS 更新可以通过 `ddns-update` 样式对所有域开启或关闭。默认开启。对于特定域关闭更新，可以使用 `ddns-updates` 语句。这也是默认的。这里是 `dhcp.conf` 文件中的简单 DNS 配置：

`/etc/dhcpd.conf`
```
option routers 192.168.0.1;
option subnet-mask 255.255.255.0;
option domain-name "mytrek.com";
option domain-name-servers 192.168.0.1;
key mydhcpserver {
  algorithm-MD5;
  secret "abcdef1234";
};
```

```
subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.0.128;
    default-lease-time 21600;
    max-lease-time 42000;
zone "mytrek.com" {
  primary 192.168.0.1;
  key mydhcpserver;
}
zone "1.168.192.in-addr.arpa" {
  primary 192.168.0.1;
  key mydhcpserver;
}
```

## DHCP 子网络

如果你将网络空间划分为子网，可以使用单个 DHCP 服务器来管理它们。在这种情况下，每个子网都有一个子网声明。如果你正在设置自己的小型网络，将使用以 192.168 开头的网络地址。`range` 将指定网络内可能的 IP 地址。对于地址为 192.168.0.0 的网络，你创建一个掩码为 255.255.255.0 的子网声明。在此声明中，你放置 `range` 声明以及任何你想给主机的其他信息。在示例中，从 192.168.0.1 到 192.168.0.75 的 IP 地址范围可以分配给该网络的主机：

```
subnet 192.168.0.0 netmask 255.255.255.0 {
  range 192.168.0.5 192.168.0.75;
}
```

你可能希望为每个子网指定不同的策略，例如不同的租用时间。子网声明中的任何条目将覆盖全局设置。如果你已经设置了全局租用时间，子网声明中的设置将覆盖该子网的设置。接的示例为不同的子网设置了不同的租用时间以及不同的地址位置。第一个子网的租用时间从全局租用时间设置获取，而第二个子网定义了自己的租用时间：

```
default-lease-time 21600;
max-lease-time 42000;

subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.0.5 192.168.0.75;
}
subnet 192.168.1.128 netmask 255.255.255.252 {
  range 192.168.0.129 192.168.0.215;
  default-lease-time 56000;
  max-lease-time 62000;
}
```

如果你的子网络属于同一个物理网络，你需要通过将它们声明为共享网络来告知服务器。你通过将子网声明放置在 `shared-network` 声明内部来实现，并指定共享网络的名称。

## 第 37 章：网络自动配置：IPv6、DHCPv6 和 DHCP

使用的名称可以是描述性名称，也可以使用域名。在共享网络声明（shared-network declaration）和子网声明中指定的任何选项对所有子网都有效。例如，子网是物理网络的一部分，并放置在共享网络声明中：

```
shared-network mytrek.com
{
default-lease-time 21600;
max-lease-time 42000;
subnet 192.168.1.0 mask 255.255.255.0 (
range 192.168.0.5 192.168.0.75;

subnet 192.168.1.128 mask 255.255.255.252 (
range 192.168.0.129 192.168.0.215;
default-lease-time 56000;
max-lease-time 62000;
}
}
```
