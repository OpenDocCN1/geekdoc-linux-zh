
## 使用 firewalld 配置 RHEL 9 防火墙

在期望更高信任级别的地方。可以在系统中添加新的区域，并修改现有区域以添加或删除规则。区域也可以从系统中完全删除。表 14-1 列出了 RHEL 9 系统默认可用的区域集：

| 区域 | 描述 |
|---|---|
| drop | 最安全的区域。仅允许传出连接，所有传入连接都会被丢弃，且不会向连接客户端发出任何通知。 |
| block | 与 drop 区域类似，不同之处在于传入连接会被拒绝，并伴随 icmp-host-prohibited 或 icmp6-adm-prohibited 通知。 |
| public | 适用于连接到公共网络或互联网且其他计算机不可信时使用。允许选定的传入连接。 |
| external | 当系统作为计算机网络的互联网网关时，external 区域应用于连接到互联网的接口。该区域在实现伪装或网络地址转换（NAT）时与 *内部* 区域一起使用，如本章后面所述。允许选定的传入连接。 |
| internal | 与 *外部* 区域一起使用并应用于连接到内部网络的接口。假定内部网络上的计算机是受信任的。允许选定的传入连接。 |
| dmz | 用于系统在非军事区（DMZ）运行时。这些通常是可公开访问但与内部网络其他部分隔离的计算机。允许选定的传入连接。 |
| work | 用于在工作环境网络中运行系统且其他计算机受信任时。允许选定的传入连接。 |
| home | 用于在家庭网络中运行系统且其他计算机受信任时。允许选定的传入连接。 |
| trusted | 最不安全的区域。所有传入连接均被接受。 |
| nm-shared | 该区域在实现连接共享时由 NetworkManager 内部使用。 |
| libvirt | 由虚拟网络使用，通常在服务器托管虚拟机时使用。 |

表 14-1

若要查看某个区域的具体设置，请参考系统上位于 `/usr/lib/firewalld/zones` 目录中的相应 XML 配置文件。例如，以下内容列出了 *public.xml* 区域配置文件的内容：

```
<?xml version="1.0" encoding="utf-8"?>
<zone>
    <short>Public</short>
    <description>For use in public areas. You do not trust the other computers on networks to not harm your computer. Only selected incoming connections are accepted.</description>
    <service name="ssh"/>
    <service name="dhcpv6-client"/>
    <service name="cockpit"/>
    <forward/>
</zone>
```

### 14.1.2 接口

任何连接到互联网或网络（或两者）的 RHEL 9 系统都至少包含一个 *接口*，形式为物理或虚拟网络设备。当 firewalld 处于活动状态时，每个接口都会被分配到一个区域，从而允许为不同接口分配不同级别的防火墙安全性。例如，考虑一台包含两个接口的服务器；一个外部连接到互联网，另一个连接到内部网络。在这种情况下，面向外部的接口很可能被分配到更严格的 *外部* 区域，而内部接口可能使用 *内部* 区域。

### 14.1.3 服务

TCP/IP 定义了一组在标准端口上通信的服务。例如，安全的 HTTPS Web 连接使用端口 443，而 SMTP 电子邮件服务使用端口 25。为了有选择地为特定服务启用传入流量，可以向区域添加 firewalld 规则。例如，*家庭* 区域默认不允许传入 HTTPS 连接。可以通过向区域添加规则来允许传入 HTTPS 连接，而无需引用特定的端口号。

### 14.1.4 端口

尽管在添加 firewalld 规则时可以引用常见的 TCP/IP 服务，但会出现需要在未分配给服务的特定端口上允许传入连接的情况。这可以通过添加引用特定端口而不是服务的规则来实现。这种技术在章节“An Overview of the Cockpit Web Interface” 中被使用，当时打开了端口 9090 以允许访问 Cockpit Web 界面。

## 14.2 检查 firewalld 状态

firewalld 服务默认安装并在所有 RHEL 9 安装中启用。可以通过以下命令检查服务的状态：

```
# systemctl status firewalld
  firewalld.service - firewalld - dynamic firewall daemon
    Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
```

```
Active: active (running) since Thu 2019-02-14 14:24:31 EST; 3 days ago
Docs: man:firewalld(1)
Main PID: 816 (firewalld)
Tasks: 2 (limit: 25026)
Memory: 30.6M
CGroup: /system.slice/firewalld.service
816 /usr/libexec/platform-python -s /usr/sbin/firewalld --nofork
--nopid
```

如有必要，可以按如下方式安装 firewalld 服务：

```
# dnf install firewalld
```

firewalld 服务默认启用，并在安装后以及系统每次启动时自动启动。

## 14.3 使用 firewall-cmd 配置防火墙规则

firewall-cmd 命令行实用程序允许查看 firewalld 配置的信息，并从终端窗口中对区域和规则进行更改。

在更改防火墙设置时，了解运行时和永久配置的概念非常重要。默认情况下，任何规则更改都被视为运行时配置更改。这意味着虽然更改会立即生效，但在系统下次重启或 firewalld 服务重新加载时会被丢失，例如通过发出以下命令：

```
# firewall-cmd --reload
```

必须使用 --permanent 命令行选项使更改永久生效。永久更改在 firewalld 服务重新加载之前不会生效，但会一直保留直到手动更改。

### 14.3.1 识别和更改默认区域

要识别默认区域（换句话说，除非专门选择不同区域，否则所有接口将被分配到的区域），请按如下方式使用 firewall-cmd 工具：

```
# firewall-cmd --get-default-zone
public
```

要将默认区域更改为其他区域：

```
# firewall-cmd --set-default-zone=home
success
```

### 14.3.2 显示区域信息

列出系统上所有可用区域：

```
# firewall-cmd --get-zones
block dmz drop external home internal libvirt nm-shared public trusted work
```

按如下方式获取当前活动的区域列表以及它们所分配的接口：

```
# firewall-cmd --get-active-zones
external
    interfaces: eth0
internal
    interfaces: eth1
```

可以按如下方式列出特定区域当前配置的所有规则：

```
# firewall-cmd --zone=home --list-all
home (active)
    target: default
    icmp-block-inversion: no
    interfaces: eth0
    sources:
    services: cockpit dhcpv6-client mdns samba-client ssh
    ports:
    protocols:
    masquerade: no
    forward-ports:
    source-ports:
    icmp-blocks:
    rich rules:
```

使用以下命令列出当前可用于包含在 firewalld 规则中的服务：

```
# firewall-cmd --get-services
RH-Satellite-6 amanda-client amanda-k5-client amqp amqps apcupsd audit bacula
bacula-client bgp bitcoin bitcoin-rpc bitcoin-testnet bitcoin-testnet-rpc ceph
ceph-mon cfengine cockpit ...
```

列出区域当前启用的服务：

```
# firewall-cmd --zone=public --list-services
cockpit dhcpv6-client ssh
```

可以按如下方式获取端口规则列表：

```
# firewall-cmd --zone=public --list-ports
9090/tcp
```

### 14.3.3 添加和删除区域服务

要向区域添加服务，在本例中向 public 区域添加 HTTPS，将使用以下命令：

```
# firewall-cmd --zone=public --add-service=https
success
```

默认情况下，这是一个运行时更改，因此在系统重启后添加的规则将丢失。要永久添加服务，使其在系统下次重启时仍然有效，请使用 --permanent 标志：

```
# firewall-cmd --zone=public --permanent --add-service=https
```
