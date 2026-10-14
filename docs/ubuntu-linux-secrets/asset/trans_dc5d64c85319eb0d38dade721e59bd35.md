

# 使用 named 作为本地缓存服务器

在服务器上使用 named 程序最简单的方法是在 Ubuntu 服务器上缓存 DNS 响应以供将来使用 DNS 请求。此配置将 Ubuntu 服务器接收到的所有 DNS 请求（无论来自服务器本身还是指向 Ubuntu 服务器的其他网络设备）指向在本地服务器上运行的 named 程序。named 程序配置将所有请求重定向到一个公共远程 DNS 服务器，通常由 ISP 提供。

这种方法的优点是 named 程序会缓存它处理的所有 DNS 请求。因此，它可以立即回答对同一主机名的任何未来请求，而无需联系远程 DNS 服务器。这种功能可以显著加快您本地网络在互联网上的交互速度。

要在 Ubuntu 服务器上设置此方法，您需要做两件事：

- ◆ 将 resolv.conf 文件中的 nameserver 条目设置为指向 localhost。
- ◆ 设置 named 配置以指向一个公共远程 DNS 服务器。

以下是更改 resolv.conf 文件中 nameserver 条目的所需步骤：

- 1. 在文本编辑器中打开 /etc/resolv.conf 文件。如果您正在 Ubuntu 服务器上工作，您需要使用命令行编辑器，例如 vim 编辑器。要编辑此文件，您必须具有管理权限（请参阅第 17 章，“用户和组”）。输入命令：
- sudo vim /etc/resolv.conf
- 2. 复制 nameserver 行中当前设置的值。默认的 Ubuntu 配置应已通过 DHCP 检测到网络 nameserver，除非您在安装时手动输入该值以为主服务器设置静态 IP 地址。nameserver 行应如下所示：
- nameserver 10.0.1.1
- 复制该 IP 地址。您将在后面的步骤中需要它。
- 3. 将该行上的 IP 地址更改为 127.0.0.1。这会将所有 DNS 请求重定向到服务器上运行的 named 程序。
- 4. 保存文件并退出编辑器。保存文件并退出编辑器的 vim 命令是 ZZ。

```
continued
2419200 ; Expire
604800 ) ; Negative Cache TTL
; @ IN NS localhost.
1.0.0 IN PTR localhost.
```

此信息为 127.0.0.1 地址定义了一个 PTR 记录（请记住，PTR 记录中 IP 八位组是按相反顺序列出的）。这定义了特殊 localhost IP 地址的反向查找。

接下来您需要配置 named 程序将所有 DNS 请求转发到最初列在 resolv.conf 文件中的远程 DNS 服务器。请按照以下步骤操作：

- 1. 在文本编辑器中打开 /etc/bind/named.conf.options 文件。同样，如果您正在 Ubuntu 服务器上工作，您需要使用命令行编辑器例如 vim 来编辑文件。要编辑此文件，您必须具有管理权限（请参阅第 17 章，“用户和组”）。要编辑文件，输入此命令：

```
sudo vim /etc/bind/named.conf.options
```

- 2. 在 named.conf.options 文件中查找 forwarders 部分，并将其更改为如下所示：

```
forwarders {
  10.0.1.1;
};
```

您必须删除这些行前面的注释（双正斜杠）才能使它们生效。您使用的 IP 地址应为从原始 resolv.conf 文件中复制的地址。

- 3. 保存文件，然后编辑编辑器。保存文件并退出编辑器的 vim 命令是 ZZ。

named 程序现在已准备就绪。您需要重新启动 named 程序，可以通过重新启动 Ubuntu 服务器或输入命令：

```
sudo /etc/init.d/bind9 restart
```

此命令重新启动 named 程序，它将读取新配置并作为本地缓存服务器运行。

# 使用 named 作为主 DNS 服务器

如果您希望 Ubuntu 服务器成为您网络的主要 DNS 服务器，您需要做更多的工作。负责网络的 DNS 服务器称为主 DNS 服务器。主 DNS 服务器包含定义网络上所有主机的记录，既用于内部通信，也用于网络外部的通信。如果互联网上的任何服务器需要知道您网络中主机名的 IP 地址，您的 Ubuntu 服务器必须能够回答该请求。

此配置使用与本地缓存服务器示例中相同的 named 配置文件，但它向配置文件中添加了网络区域信息。配置文件需要您希望向互联网提供的主机的主机名和 IP 地址信息。

- /etc/bind/named.conf.local: 此文件存储区域名称和文件位置。
- /etc/bind/db.smallorg.org: 基于您的域名的一个区域配置文件，它存储您主机区域主机名信息。
- /etc/bind/db.10: 基于您 IP 网络地址的第一个八位组的一个反向查找配置文件，它存储您主机的反向 IP 地址信息。

