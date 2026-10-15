
一旦您在 Linux 机器上成功安装了硬件和软件并验证了它们的可用性，就可以调整网络设备的设置，前提是它们仍然正常工作。进行这些调整的最简单方法可能是使用几种提供的图形用户界面 `GUI` 之一来编辑文本设置，这些设置控制所有网络配置。或者，您可以手动编辑文件，这对于可能需要远程完成此任务且没有 X 接口的许多用户来说是一个更可取的选择。本节首先检查这些文件本身以及它们如何建立网络连接。然后，您将探索使用几种不同的 GUI 通过各种工具完成相同任务的可选项。有关设置 X 窗口系统或启动 GUI 的更多信息，请参阅第 12 章。

需要知道的最重要文件如下：

- `/etc/HOSTNAME` 为计算机提供特定的主机名。
- `/etc/hosts` 列出网络系统上的各种主机。它还将不同的主机名映射到各种 IP 地址。这有助于加快数据包传输，因为不需要主机名查找。
- `/etc/services` 列出所有可用端口及其相关使用服务或进程。
- `/etc/inetd.conf` 告诉系统哪些服务应被视为有效请求，并由守护程序按需启动。
- `/etc/resolv.conf` 告诉系统哪些域名应列在 DNS 搜索顺序中。它通常概述要搜索的域名和名称服务器的顺序。
- `/etc/host.conf` 指定解析主机名时搜索名称系统的顺序。
- `/etc/sysconfig/network` 列出主机名、IP 地址和网关等各种项目。此文件最好通过 GUI 配置，但也可以手动编辑。
- `/etc/sysconfig/network-scripts/` 保存各种设备启动选项。在此目录中，您可以设置网络设备（如 `eth0` 或 `ppp0`）的启动方式。

## 定义计算机的主机名

第一个变量 `HOSTNAME` 是一个简单的文本文件，包含计算机的名称和域名。`HOSTNAME` 文件的示例可能如下所示：

```
antares.astronomy.org
```

在某些情况下，对此设置的更改不会生效，直到网络进程重启、当前用户注销或计算机重新启动。由于在 Linux 下您可以停止并重新启动几乎所有内容，而无需关闭计算机电源，因此在尝试重新启动之前，您应始终尝试停止并重启该进程。只有在极端情况下才应关闭系统电源。

重启网络进程的标准方法是使用大多数 Linux 发行版提供的网络脚本。以下是 Red Hat 建议用户执行的重启操作示例：

```bash
/etc/rc.d/init.d/network restart
```

## 配置 Hosts 文件

第二个变量 `/etc/hosts` 对于大型网络和小型网络都很方便。你无需在系统中输入每台计算机的完整地址，也无需查询每台计算机及其位置的名称服务器。相反，你可以查阅 `/etc/hosts` 文件，该文件提供了网络中所有可用计算机的 IP 地址、主机名、域名和别名的列表。最后一个字段可能是最重要的，因为它允许你只需输入别名而无需键入完整路径即可登录到该计算机。例如，你无需输入 `antares.astronomy.org`，只需输入 `antares` 即可。

如果频繁更改 IP 地址和计算机名称，在大型网络上维护此文件可能会带来问题。如果你的网络相对静态，且不需要经常重新配置，`/etc/hosts` 文件将减轻名称服务器的一些负载，并提供到其它机器的快速连接。

表 15.2 描述了一个示例 `/etc/hosts` 文件。

| IP 地址 | 计算机全名 | 别名 |
| :--- | :--- | :--- |
| 127.0.0.1 | localhost.localdomain | localhost |
| 192.168.0.1 | antares.astronomy.org | antares |
| 192.168.0.2 | vega.astronomy.org | vega |
| 192.168.0.3 | deneb.astronomy.org | deneb |
| 192.168.0.254 | polaris.astronomy.org | polaris |
| 192.168.0.253 | regulus.astronomy.org | regulus |
| 142.58.12.213 | sirius.nasa.gov | sirius |

根据该表，本地系统由几台计算机组成，每台计算机都有一个与其域名结合的具体天文名称。最后一行描述了一台位于本地域名之外但此服务器也可能拥有本地访问权限的额外计算机。通常，域名外的计算机由系统名称服务器上的 DNS 条目覆盖，但为了说明，此示例列出了 `sirus.nasa.gov` 以演示 `/etc/hosts` 如何提供对域名外主机的轻松访问。

## 设置服务

第三个文件 `/etc/services` 提供了 Linux 下所有可用进程的更长的列表。这些内容包括第一字段中的服务名称、端口号和协议类型、服务的别名，以及通常解释该服务功能的注释字段。

以下是示例 `/etc/services` 文件中的简要摘录：

```
www             80/tcp          http              # WorldWideWeb HTTP
www             80/udp                   # HyperText Transfer Protocol
link            87/tcp          ttylink
kerberos        88/tcp          kerberos5 krb5    # Kerberos v5
kerberos        88/udp          kerberos5 krb5    # Kerberos v5
supdup          95/tcp                   # 100 - reserved
hostnames       101/tcp         hostname        # usually from sri-nic
iso-tsap        102/tcp         tsap          # part of ISODE.
csnet-ns        105/tcp         cso-ns        # also used by CSO name server
csnet-ns        105/udp         cso-ns
rtelnet         107/tcp                  # Remote Telnet
rteInet         107/udp
pop-2           109/tcp         postoffice      # POP version 2
pop-2           109/udp
pop-3           110/tcp         pop3          # POP version 3
pop-3           110/udp
```

大多数被访问的进程使用 TCP 或 UDP。要启用其中一项服务，你需要通过 RPM 文件安装可执行文件，或者自行编译源码并将守护进程安装到正确位置，以验证是否已安装该可执行文件。

例如，要在 Linux 系统上启用 `pop3` 守护进程，你可以使用随大多数安装提供的简单 RPM 二进制文件，或从其站点 `ftp://ftp.eac.washington.edu/pine/` 下载源码。解包并解压源码，运行必要的命令以编译源码，然后验证并将可执行文件安装到 `/usr/sbin`。在端口号 110 下的第三个字段中，放置单词 `pop3` 或相应的进程名称。如果尚未存在，你可能希望随后添加一个注释。你可以向 1024 以上的端口添加新的守护进程，但建议不要对 1024 以下的端口进行任何更改。你必须遵守已制定的端口号及附带进程的标准的设定。如果你正在安装一个新进程，例如在端口 1984 下运行的大哥监控系统（Big Brother monitoring system），请验证正确的设置并做出正确的条目。

## 选择 inetd.conf 文件中的条目

第四个选项 `/etc/inetd.conf` 与 `/etc/services` 文件中的前几项条目紧密相关。要在启动时启用各种守护进程，请通过删除文本前面的井号（`#`）来取消该守护进程所在行的注释。由于大多数 Linux 发行版都安装了 `tcp_wrappers` 以增加安全性并为运行中的各种进程提供额外的日志记录，你会发现 `/usr/sbin/tcpd` 守护进程经常取代进程本身被执行。`tcpd` 守护进程是一个静默的端口监控器，它在以适当权限执行进程之前检查用户的真实性。

> **注意**
>
> Red Hat Linux 在正常安装过程中默认安装 `tcp_wrappers`。很少发现有机器未运行 `tcp_wrappers`。如果你选择了自定义或有限的设置例程，请确保启用此实用程序。

`/etc/inetd.conf` 文件中示例行的语法如下：
