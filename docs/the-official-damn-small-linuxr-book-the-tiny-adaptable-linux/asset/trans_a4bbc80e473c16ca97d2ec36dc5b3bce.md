

## 注意

rc.firewall 脚本基本上为你的 DSL 系统添加 iptables 规则。由于 rc.firewall 软件包本身也包含了 iptables 功能，因此你可以直接使用 iptables 命令配置防火墙，或使用设置 iptables 规则的其他脚本。寻找此类脚本，特别是更复杂的防火墙时，LinuxGuruz 网站（www.linuxguruz.com/iptables）是一个很好的地方。

## 安装防火墙软件

要在 DSL 中使用 rc.firewall 软件包，必须从 MyDSL 功能中安装 rc.firewall 软件包和 gnu-utils 软件包。首先，从桌面选择 MyDSL 图标。之后，选择以下内容：

- **防火墙软件包**—选择 UNC→ rc.firewall.unc.info。当 rc.firewall.unc.info 页面出现时，选择 Download 并将软件包下载到 /tmp 目录。

- **GNU 工具软件包**—选择 UNC→ gnu-utils.unc.info。当 gnu-utils.unc.info 页面出现时，选择 Download 并将软件包下载到 /tmp 目录。

rc.firewall 和 gnu-utils 两个软件包在下载后会自动安装。虽然 iptables 立即启用，但 rc.firewall 脚本在安装时不会运行，也不会阻止任何传入连接。下一步是配置并运行 rc.firewall 脚本。

## 配置 rc.firewall 脚本

按原样提供时，rc.firewall 脚本配置为阻止所有传入到计算机的连接。你需要打开与你希望允许外部人员使用的服务相关联的端口的访问权限：即 Web 和 FTP 服务。

由于 rc.firewall 是一个 shell 脚本，你可以使用任何文本编辑器编辑它。我将首先将 rc.firewall 的副本制作到 /opt 目录，以便你可以从那里运行它。（另外，如果你搞砸了，你可以只制作一个文件的新副本。）例如，打开一个 root Terminal 窗口并运行此复制命令，然后使用 vi 命令或 Beaver 编辑器打开文件，如下所示：

```
# cp /etc/init.d/rc.firewall /opt/
# beaver /opt/rc.firewall
```

你可以在 rc.firewall 文件中有很多种方式更改防火墙配置。就我们的目的而言，我们只会打开几个端口以允许外部访问 Web 服务器（端口 80）和 FTP 服务器（端口 21）。

打开 rc.firewall 脚本后，你可以通过将这些端口号添加到 PERMIT="" 行来打开对 Web 服务器和 FTP 服务器端口的访问。因此，对于最简单的情况，编辑 permit 行使其如下所示：

```
PERMIT="80 21"
```

前面的 PERMIT 行打开对标准 Web 服务端口（80）和 FTP 服务端口（21）的访问。请注意，条目之间需要空格。有了这一行，所有网络接口都允许任何人访问这些接口以请求 Web 和 FTP 服务。当然，如果你用密码保护了这些服务，用户还需要该用户名/密码信息才能最终查看与这些服务相关的内容。

以下是你可以配置 PERMIT 行以打开对 Web 和 FTP 服务访问的几种不同方式：

```
PERMIT="80/tcp 21/tcp"
PERMIT="192.168.0.0/24:80 192.168.0.0/24:21"
PERMIT="192.168.0.0/24 10.0.0.150"
```

你可以使用前面任何 PERMIT 行中的示例来允许访问你的服务器。在第一个示例中，tcp 添加到每个端口号，以表示只有 TCP 协议可以访问这些服务（默认情况下，允许 TCP 和 UDP）。下一个示例仅允许 192.168.0 网络上的计算机访问端口 80 和 21（如果你想将访问限制在你的 LAN 上的计算机上，这是一个不错的方法）。最后一个示例允许访问 192.168.0 网络上的任何可用端口，并特别允许来自 IP 地址 10.0.0.50 的主机的访问。

在你的 rc.firewall 脚本中配置防火墙服务的方式还有很多很多。例如，如果你的 Web 服务器也用作你在 LAN 和 Internet 之间的路由器（这不是一个非常安全的安排，但很多人这样做），脚本允许你为此设置防火墙。假设你希望允许从你的 LAN（eth1 接口）计算机路由到 Internet（eth0 接口），以下行将告诉你的防火墙允许这样做：

```
INTERNAL_INTERFACES="eth0"
```

让你的服务器和 LAN 上的工作站位于同一 Internet 连接后面的更安全的方法是配置所谓的非军事区（DMZ）。使用 DMZ 配置，服务器位于一个防火墙后面，而你的私有 LAN（通常是你的用户工作站）位于

