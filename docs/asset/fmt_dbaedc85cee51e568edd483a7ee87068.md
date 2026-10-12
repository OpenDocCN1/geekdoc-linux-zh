
> 每个区域通常有多个 DNS 服务器，以确保当一个服务器不可用时仍可解析名称。区域中的第一个 DNS 服务器称为 **主 DNS 服务器或主服务器**，所有额外的 DNS 服务器称为 *从 DNS 服务器或辅助服务器*。新的区域信息被添加到主 DNS 服务器；从 DNS 服务器通过称为 **区域传输** 的过程定期从主 DNS 服务器复制新记录。

要将你的 Linux 计算机配置为 DNS 服务器，你必须为特定区域配置名称守护进程（`named`），并添加资源记录，列出该区域中计算机的 FQDN 及其关联的 IP 地址。表 15-3 列出了可用于配置此区域信息的文件。

###### 表 15-3 常见区域配置文件

| 文件 | 描述 |
|---|---|
| `/etc/named.conf` | 包含名称守护进程将管理的 DNS 区域列表及其类型（主/从）。 |
| `/var/named/zone name.zone` | 包含用于执行特定 `zone name` 正向查找的资源记录。此文件中的行具有决定资源记录类型的类型：<br> - A（添加主机）记录将 FQDN 映射到 IP 地址。<br> - CNAME（规范名称）记录为 A 记录提供额外的别名。<br> - NS（名称服务器）记录提供该区域的 DNS 服务器名称。<br> - MX（邮件交换）记录提供该区域邮件服务器的 IP 地址。 |
| `/var/named/in-addr.arpa` | 包含类型为 PTR（指针）的资源记录，这些记录列出用于特定网络反向查找的名称。网络本身被纳入文件名中；例如，包含 192.168.1.0 网络 PTR 记录的文件名将被称为 1.168.192.in-addr.arpa。 |
| `/var/named/named.local` | 包含用于标识回环适配器（127.0.0.1）的 PTR 记录。 |
| `/var/named/named.ca` | 包含顶级 DNS 服务器的 IP 地址；通常称为 DNS 缓存文件。 |

在创建包含区域信息的文件后，你可以简单地使用命令 `/etc/rc.d/init.d/named start` 启动名称守护进程，以在网络中提供 DNS 服务。如果你修改了与名称守护进程相关的任何文件，例如添加额外的资源记录，你必须重启名称守护进程才能使这些更改生效。为此，你可以简单地使用命令 `/etc/rc.d/init.d/named restart`。

##### 配置 DHCP

回想一下，前一章中提到，你的网络接口可以手动配置，也可以使用 DHCP 自动配置。如果你的网络接口使用 DHCP 配置，它会在网络上发送 DHCP 广播，请求 IP 配置信息。如果网络上有一个具有 IP 地址范围的 DHCP 服务器，它会向客户端计算机租借一个 IP 地址，租期为特定时间段；此租期过期后，客户端计算机必须发送另一个 DHCP 请求。由于 DHCP 服务器跟踪它们租借给客户端计算机的 IP 地址，因此可以确保没有两台计算机收到相同的 IP 地址。如果两台计算机意外地被手动配置为具有相同的 IP 地址，那么它们都无法使用 IP 协议进行通信。

此外，DHCP 服务器还可以向客户端计算机发送其他 IP 配置信息，例如网络中应使用的默认网关和 DNS 服务器。

要将你的 Linux 计算机配置为 DHCP 服务器，只需创建一个 `/etc/dhcpd.conf` 文件，列出适用于你网络的适当 IP 地址范围，以及租约信息和其他 IP 配置选项。下面显示了一个在 192.168.1.0/24 网络上租借 IP 地址的示例 `/etc/dhcpd.conf` 文件：

```bash
[root@server1 root]# cat /etc/dhcpd.conf
default-lease-time 36000;
ddns-update-style ad-hoc;
option routers 192.168.1.254;
option domain-name-servers 192.168.1.200;
subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.1.1 192.168.1.100
}
[root@server1 root]# ~
```

请注意，根据上述输出，DHCP 服务器为客户端分配了介于 192.168.1.1 和 192.168.1.100 之间的 IP 地址，租约时间为 36,000 秒。此外，DHCP 服务器还将客户端的默认网关配置为 192.168.1.254，DNS 服务器配置为 192.168.1.200。

在 `/etc/dhcpd.conf` 文件配置了相应信息后，您可以使用命令 `/etc/rc.d/init.d/dhcpd start` 启动 DHCP 守护进程，并通过检查 `/var/lib/dhcpd/dhcpd.leases` 文件来查看当前的 DHCP 租约。与 `daemon` 的名称类似，如果您修改了 `/etc/dhcpd.conf` 配置文件，必须重新启动 DHCP 守护进程。

##### 配置 Apache

Apache 是世界上最常见的 Web 服务器。回顾一下，Web 服务器使用超文本传输协议 (HTTP) 从目录树中的特定目录分发 HTML 文件和其他 Web 内容。此目录称为文档根目录，其中包含服务器上使用的默认网站。在 Red Hat Fedora Core 2 中，默认的文档根目录是 `/var/www/html`，从此目录分发的默认文档是 `index.html`。Apache 的大多数配置选项都在一个大型配置文件中设置；默认情况下，该配置文件是 `/etc/httpd/conf/httpd.conf`。`httpd.conf` 文件中的每一行都称为指令。表 15-4 列出了一些常见指令。

###### 表 15-4 常见的 `httpd.conf` 指令

| 指令 | 描述 |
| :--- | :--- |
| `Listen 80` | 指定 Apache 守护进程将在端口 80 上监听 HTTP 请求 |
| `ServerName server1.class.com` | 指定本地服务器的名称为 server1.class.com |
| `DocumentRoot "/var/www/html"` | 指定本地计算机的文档根目录为 /var/www/html |
| `DirectoryIndex index.html` | 指定将发送 `index.html` 文件给请求 HTML 文档的客户端 |
| `ErrorLog /var/log/httpd/error_log` | 指定所有 Apache 守护进程消息将写入 /var/log/httpd/error_log 文件 |
| `MaxClients 150` | 将最大同时请求数设置为 150 |
| `User apache` | 指定 Apache 守护进程将作为 "apache" 本地用户账户运行 |
| `Group apache` | 指定 Apache 守护进程将作为 "apache" 本地组账户运行 |
| `<Directory /var/www/html>`<br>`Order allow,deny`<br>`Allow from all`<br>`Deny from 192.168.1.51`<br>`</Directory>` | 指定除 IP 地址为 192.168.1.51 的计算机外，所有主机都允许访问 /var/www/html 目录中的 HTML 文件和其他 Web 内容 |

`httpd.conf` 文件中的默认设置对于大多数简单的 Web 服务器来说已经足够；因此，您只需要将相应的 HTML 文件（包括 `index.html` 文件）复制到 `/var/www/html` 目录，并启动 Apache Web 服务器守护进程（`/etc/rc.d/init.d/httpd start`），即可在网络上托管 Web 内容。如果您更改文档根目录内的 HTML 内容，无需重新启动 Apache 守护进程。但是，如果您更改了 `httpd.conf` 的内容，则需要重新启动 Apache 守护进程以激活这些更改。

##### 配置 Samba

目前网络上最常见的客户端计算机操作系统是 Windows。回顾前一章，Windows 计算机使用服务器消息块 (SMB) 格式化 TCP/IP 数据。因此，为了向 Windows 客户端计算机共享信息，您可以使用 Samba 守护进程，它模拟了 SMB 协议。此外，Windows 计算机使用 NetBIOS 协议广播其计算机名称；因此，您可以使用 NetBIOS 名称守护进程来创建和广播 Windows 计算机可以使用的 NetBIOS 名称，以便连接到您的 Linux 服务器。

当 Windows 客户端计算机使用 SMB 访问共享目录时，Windows 用户名和密码会随访问该共享目录的请求一起传输，该请求仅允许特定用户访问。因此，您应为每个 Windows 用户创建本地 Linux 用户账户，并使用 `smbpasswd` 命令为他们创建 Samba 密码，该密码应与他们在 Windows 计算机上使用的密码匹配，如下面的输出所示：
