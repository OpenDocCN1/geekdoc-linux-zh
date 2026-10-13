
```
option broadcast-address 192.168.0.255;
option domain-name-servers 192.168.0.1, 192.168.0.4;
option domain-name "mytrek.com";
```

您的 `dhcpd.conf` 文件通常以您为 DHCP 服务器所服务的网络定义的声明、参数和选项开头。以下示例向客户机提供路由器（网关）、子网掩码、域名和 DNS 服务器信息。其他参数定义了动态分配的 IP 地址的默认租约时间和最大租约时间。

```
option routers 192.168.0.1;
option subnet-mask 255.255.255.0;
option domain-name "mytrek.com";
option domain-name-servers 192.168.0.1;
default-lease-time 21600;
max-lease-time 43200;
```

使用子网、主机和组声明，您可以引用特定网络中的客户机、特定客户机或跨越网络的客户机分组。在这些声明内，您可以输入仅适用于这些客户机的参数、声明或选项。作用域内的声明、参数和选项用花括号包围。例如，要为特定主机定义声明，请使用此处所示的 `host` 声明：

```
host rabbit {
    declarations, parameters, or options;
}
```

您可以使用 `group` 声明将不同的子网、全局和主机声明收集到组中。在这种情况下，全局声明仅应用于组内声明的子网和主机。

### 动态地址

您的 DHCP 服务器可以配置为从给定范围中选择 IP 地址并将其分配给不同的客户机。在拥有许多并非始终连接到网络的客户机的情况下，您可以有效地使用较小的 IP 地址池为其提供服务。IP 地址仅在需要时才分配。使用 `range` 声明，您指定可以动态分配给客户机的地址范围。该声明接受两个参数，即范围内的第一个和最后一个地址。

```
range 192.168.1.5 192.168.1.128;
```

例如，如果您正在设置自己的小型家庭网络，您将使用以 192.168 开头的网络地址。该范围将指定该网络的可能 IP 地址。因此，对于地址为 192.168.0.0 的网络，您将放置一个 `range` 声明以及您想要提供给客户机主机的任何其他信息。在以下示例中，从 192.168.0.1 到 192.168.0.128 的 IP 地址范围可以分配给该网络上的主机：

```
range 192.168.0.5 192.168.0.128;
```

您还应该定义您的租约时间，包括默认和最大值：

```
default-lease-time 21600;
max-lease-time 43200;
```

对于一个简单的小型家庭网络，您只需要像下面这样列出 `range` 声明和任何全局选项即可。如果您的 DHCP 服务器管理着多个子网，您将不得不使用子网声明。

为了向网络分配动态地址，DHCP 服务器要求映射您的网络拓扑。这意味着它需要知道哪些网络地址属于给定网络。即使您只使用一个网络，您也需要指定其地址空间。您使用子网声明定义网络。在此子网声明内，您可以指定用于该网络的任何参数、声明或选项。子网声明告知 DHCP 服务器给定子网包含的可能 IP 地址。这是由该网络的 IP 地址和子网掩码确定的。下一个示例定义了一个地址空间从 192.168.0.0 到 192.168.0.255 的本地网络。`range` 声明允许从 192.168.0.5 到 192.168.0.128 分配地址。

```
subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.0.5 192.168.0.128;
}
```

DHCP 3.0 之前的版本要求即使是由 DHCP 不提供服务的连接网络接口也要被映射。因此，每个网络接口都必须有一个对应的子网声明。那些未由 DHCP 提供服务的将具有 `not authoritative` 参数，如下所示（192.168.2.0 是不由 DHCP 提供服务的网络）。在 3.0 及更高版本中，DHCP simply 忽略未映射的网络接口：

```
subnet 192.168.2.0 netmask 255.255.255.0 {
    not authoritative;
}
```

以下示例 `dhcpd.conf` 文件展示了一个用于动态地址的非常简单 DHCP 服务器的实现。

`/etc/dhcpd.conf`

```
option routers 192.168.0.1;
option subnet-mask 255.255.255.0;
option domain-name "mytrek.com";
```

### 动态 DNS 更新

对于同时支持域名服务器（Domain Name Server）的网络，动态分配 IP 地址目前需要解决一个主要约束条件：DHCP 需要与 DNS 服务器同步。DNS 服务器将主机名与特定的 IP 地址关联，而在动态分配的情况下，DHCP 服务器随机为其自身的不同主机分配 IP 地址。这些 IP 地址可能与 DNS 服务器期望与某个主机名关联的 IP 地址相同，也可能不同。针对这个问题，正在开发一种称为动态 DNS（Dynamic DNS）的解决方案。借助动态 DNS，DHCP 服务器能够自动使用其分配给不同主机的 IP 地址来更新 DNS 服务器。

**注意**

或者，如果你想使用固定地址静态同步你的 DHCP 和 DNS 服务器，你需要配置 DHCP 将那些固定地址分配给主机。然后你可以让 DHCP 服务器执行 DNS 查询以获取它应该分配的 IP 地址，或者你可以手动在 DHCP 配置文件中分配相同的 IP 地址。执行 DNS 查询的优点在于只需在一个地方（即 DNS 服务器）指定 IP 地址。

3.0 版 DHCP 服务器具有动态更新 BIND DNS 服务器区域配置文件的能力。如第 34 章所述，DNS 服务器必须通过在 `named.conf` 文件中为区域文件指定 `allow-update` 选项来启用动态更新。此外，强烈建议你使用 TSIG 签名密钥（参见第 34 章）来引用和验证 BIND 和 DHCP 服务器。目前，DHCP 使用临时 DNS 更新方案（Interim DNS Update Scheme）来执行动态 DNS 更新，取代了早期的临时 DNS 更新方案（Ad-Hoc DNS Update Scheme）。未来 DHCP 版本将实现最终确定的方案。你可以在 `dhcpd.conf` 的手册页中找到关于动态 DNS 的详细信息。

启用 TSIG 密钥的使用涉及同步 DHCP 和 DNS 服务器的配置。两者都必须配置为对相同的域使用相同的密钥。首先，你需要使用 `dnssec-keygen` 创建一个共享密钥 TSIG 签名密钥，如第 34 章所述。在 DNS 服务器中，你将在服务器的 `named.conf` 文件中放置 TSIG 密钥声明和 `allow-update` 条目，如以下示例所示：

```
key mydhcpserver {
  algorithm HMAC-MD5;
  secret "CNQAfBbLNvWU9H8hRqq/WA==";
};

zone "mytrek.com" {
  type master;
  file "mytrek.com";
  allow-update {key mydhcpserver;};
};

zone "1.168.192.IN-ADDR.ARPA" {
  type master;
  file "192.168.0";
  allow-update {key mydhcpserver;};
};
```

在 DHCP 服务器中，你在服务器的 `dhcpd.conf` 文件中放置相应的 TSIG 密钥声明和 `allow-update` 条目，如以下示例所示。密钥声明的语法与 DNS 服务器相同。然后使用 DHCP 区域语句来指定域的 IP 地址以及要使用的 TSIG 密钥。域名称和 IP 地址在 DNS 和 DHCP 服务器的配置文件中必须完全匹配。与 `named.conf` 文件不同，`dhcpd.conf` 文件中的域名称和 IP 地址周围没有引号。在 `dhcpd.conf` 文件中，区域语句中使用的域名称和 IP 地址也必须以句号结尾，就像在 DNS 区域文件中一样。密钥语句列出了要使用的密钥。虽然 DHCP 会尝试确定要更新的 DNS 服务器，但建议你在区域条目中通过 `primary` 语句明确标识它们。

```
key mydhcpserver {
    algorithm HMAC-MD5;
    secret "ONQAfBLnVwU9H8hRqq/WA==";
};
```
