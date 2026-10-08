
所有其他 DHCP 服务器都提供了类似的/重启配置脚本——如果您安装了另一个 DHCP 服务器，请检查 `/etc/init.d` 中的其控制文件，以获取需要执行的脚本名称以及您可能需要提供的任何额外参数。

## 指定额外的 DHCP 服务器配置条目

除了上一节中讨论的 DHCP 配置语句外，您还可以在 DHCP 服务器的配置文件中指定几个其他选项。使用这些其他选项可以为您的 DHCP 服务器提供额外的配置信息，使其能够将这些信息转发给它的任何客户端。

以下是您可能会发现有用的全局 `dhcpd.conf` 语句。在列表之后提供了一个使用这些语句的 `dhcpd.conf` 文件示例，以便明确每个语句所使用的上下文：

-   default-lease-time: 此 DHCP 服务器配置选项允许您指定租约有效的默认时间。该时间段以秒的整数形式指定。

-   ddns-update-style: 此声明用于当您的站点使用 DNS（动态域名系统）并自动更新 IP 地址时。如果您的站点不接受更新的 DNS 服务器，您可能将此项设置为 `off`。

-   ip-forwarding: 此选项用于允许 DHCP 服务器在网络之间转发 IP 数据包。如果您不想让其转发 IP 数据包，您可能将此项设置为 `off`。

-   max-lease-time: 此 DHCP 服务器配置选项允许您指定租约有效的长时间。该时间段以整数的形式指定。

一个使用这些语句的 `dhcpd.conf` 文件示例如下，以便明确每个语句所使用的上下文：

```
authoritative;
option domain-name "example.org";
option ddns-update-style none;
option default-lease-time 600;
option max-lease-time 86400;
option ip-forwarding off;
subnet 192.168.1.0 netmask 255.255.255.0 {
  range 192.168.1.100 192.168.1.200;
}
```

```
host dorothy {
    hardware ethernet 00:1E:0C:75:1D:7;
    fixed-address 192.168.1.69;
    option host_name "dorothy";
}
```

注意，名为 `dorothy` 的特定主机会覆盖文件中的任何默认值。
