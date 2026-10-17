
```
    host-specific parameters...

  )

  host cambridge.sambabook (

    host-specific parameters...

  )

  host birmingham.sambabook (

    host-specific parameters...

  )

}
```

`dhcpd.leases` 文件是 DHCP 客户端租约数据库，其默认位置为 `/var/state/dhcp`。该数据库是一个 ASCII 文件，包含一系列租约声明。每当获取、重租或释放租约时，其新值都会被追加到文件中。如果某个特定租约出现多个声明，则该租约的最后条目为当前版本。

当首次安装 `dhcpd` 时，不存在租约数据库。但是，`dhcpd` 要求在启动之前必须存在一个租约数据库。要创建一个空的租约数据库，请运行以下命令：

```
touch /var/state/dhcp/dhcpd.leases
```

这将按照要求创建该文件。

# 第 10 章 高级主题与管理问题

定期，`dhcpd.leases` 文件会由 `dhcpd` 程序自动调整大小，并维护一个包含旧信息的 `dhcpd.leases~` 文件。

文件中用于租约描述的条目按以下格式存储：

```
lease ip-address { statements... }
```

这些语句定义了租约的持续时间以及分配给谁。

租约的开始和结束时间在语句中以前缀 `starts` 或 `ends` 包含，如下：

```
starts date;
ends date:
```

日期遵循此结构：

```
weekday year/month/day hour:minute:second
```

```
hardware hardware-type mac-address:
```

如果客户端使用客户端标识符来获取其地址，则将使用 `uid` 语句记录客户端标识符：

```
uid client-identifier:
```

客户端标识符被记录为一系列十六进制字节，无论客户端指定的是 ASCII 字符串还是使用较新的硬件类型/MAC 地址格式。

如果客户端使用 `Client Hostname` 选项发送主机名（如某些版本的 DHCP-DNS 交互草案所示），则该主机名将使用 `client-hostname` 语句记录：

```
client-hostname "hostname":
```

如果客户端像 Windows 95 那样使用 `Hostname` 选项发送主机名，则将使用 `hostname` 语句记录：

```
hostname "hostname":
```

# 立即时解决方案

如果您正在替换原始的 WINS 安装，请确保在使用软件之前备份了当前的租约数据库。

# 创建 WINS 服务器

在 Samba 服务器上创建 WINS 服务器只需需在 `smb.conf` 文件中添加 `wins support = yes` 即可。如果您的网络中已经有一台 Microsoft NT 服务器执行此项任务，请不要向您的网络中添加 WINS 服务器，因为 Windows NT 服务器会期望接管此功能。此外，Microsoft WINS 服务器能够与另一个 WINS 服务器同步其数据库（例如，在公司的另一栋建筑中）。Samba 不支持这种能力，且只能在单配置中使用。Samba 服务器的 WINS 数据库包含在 `WINS.DAT` 文件，它是 `<samba_home>/var/locks/` 下的一个 ASCII 文本。列表 10.26 显示了此类示例。

## 列表 10.26 WINS.DAT 中的条目

```
VERSION 1.0.418

"SAMABOOK#00" 930028 255.255.255.255

"SAMABOOK#01" 930028 255.255.255.255

"LINUXDS1#00" 930028 192.168.1.1

"LINUXDS1#03" 930028 192.168.1.1

"LINUXDS1#20" 930028 192.168.1.1
```

在发生故障的情况下（例如对于持有数百台主机数据库的 WINS 服务器），能够为了恢复目的创建此数据库的副本是有意义的。然而，您不能在运行中的 Samba 服务器上复制此文件。您需要先关闭 `nmbd` 服务。Samba 服务器的 WINS 数据库包含在 `WINS.DAT` 文件中，它是 `<samba_home>/var/locks/` 中的一个 ASCII 文本。其示例见列表 10.26。
