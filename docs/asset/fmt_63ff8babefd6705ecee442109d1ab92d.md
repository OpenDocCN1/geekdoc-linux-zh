
启动 `ltspcfg` 命令后，输入 `I` 来更改运行级别。对于 Fedora 和其他 Red Hat Linux 系统，默认运行级别通常为 5（导致控制台上出现图形登录界面）。如果你希望出现文本提示符进行登录，可以使用运行级别 3。其他 Linux 系统可能为图形界面和文本登录使用不同的运行级别值。

# 第 11 章 — 使用 LTSP 301 构建瘦身客户端服务器

## 接口选择（Interface Selection）

启动 `ltspcfg` 命令后，输入 `2` 来选择服务器的哪一个以太网接口连接到瘦身客户端。你的服务器可能有两个（或更多）网络网卡（`NIC`），例如，它连接到了一个局域网（连接到瘦身客户端）和一个互联网连接（如 `DSL` 或 `ISDN` 硬件）。选择合适的接口，使“Used”（已使用）列下出现箭头（`------`）。

## DHCP 配置（DHCP Configuration）

启动 `ltspcfg` 命令后，输入 `3` 设置你的 DHCP 服务（`dhcpd`）。在回答提示后，你需要编辑 `/etc/dhcp.conf` 文件（稍后会描述）。以下是这些提示及其在 Fedora 或其他 Red Hat 系统上的结果：

- 启用 `dhcp` 守护进程（Enable `dhcp` daemon） — `Y` 开启 `DHCP` 服务（在系统启动时启动 `dhcpd` 守护进程）
- 构建 `dhcpd.conf` 文件（Build a `dhcpd.conf` file） — `Y` 创建 `dhcpd` 守护进程使用的配置文件（如果你已经有一个 `dhcpd.conf` 文件，`LTSP` 信息将在不同的文件中创建：`/etc/dhcpd.conf.sample`）。

> 有多种方法可以设置 `DHCP` 服务器。我建议你参考 `dhcpd` 页面（`man` page `dhcpd`），以及其他手册（`dhcrelay`、`dhcp.leases` 和 `dhcp-event`）获取有关配置 `DHCP` 的更多信息。

![](img/1b8a24a162893627b8005ac678b79236_325_0.png)

在 Fedora 系统上，完成上述步骤后，`dhcp` 服务应该应在系统启动时运行（运行级别 5），且 `dhcpd.conf` 文件将填充默认设置。此时，你可以在另一个终端中编辑 `/etc/dhcpd.conf` 文件，并根据你的客户端网络需求进行定制。接下来的步骤将引导你了解该文件以及如何更改它。

在以下几行中，动态 DNS 已关闭（如果你想了解此功能，请参考 `dhcpd.conf` 手页中的 `Dynamic DNS Updates` 部分），默认和最大租约时间设置为 21600 秒（6 小时）。租约值设置了客户端在需要更新之前保留 IP 地址的时间。

```
dns-update-style      none;
default-lease-time   21600;
max-lease-time       21600;
```

接下来的行是关于如何布局网络。你需要编辑这些行以适应你的环境。请返回图 11-2 以查看我们是如何配置示例客户端的。

例如，我们选择使用私有 IP 地址 `10.0.0.100` 到 `10.0.0.104` 设置局域网（在这种安排下，你可以使用到 IP 地址 `10.0.0.254`）。拥有局域网的服务器 IP 地址为 `10.0.0.100`（它在另一块网卡上有一个面向互联网的额外 IP）。

## 302 第四部分 — 小型企业项目

你必须从 ISP 获取 DNS 服务器的 IP 地址并输入 `domain-name-servers` 行。（这些不是真实的 IP 地址，因为 IP 地址不能超过 255，请确保将其修改为你自己的。将 `example.com` 替换为你的域名。）

```
option subnet-mask 255.255.255.0
option broadcast-address 10.0.0.255
option routers 10.0.0.1
option domain-name-servers 10.0.0.1
option domain-name-servers 10.0.0.2
option domain-name "example.com"
```

`root-path` 行指示每个客户端使用的 Linux 操作系统文件位置（称为 `LTP` client）。第一部分（`10.0.0.100`）指示包含 `LTP` 树的服务器，路径（`/opt/ltsp/i386`）指示该目录在服务器上的位置。

```
option root-path "10.0.0.100:/opt/ltsp/i386"
```

接下来定义网络本身。例如，有一个物理局域网的 IP 地址。然后，在子网内，每个计算机都单独定义，带有独立的 `host` 条目。

```
subnet 10.0.0.0 netmask 255.255.255.0
use-host-decl on
option log-servers 10.0.0.100
```

```
host station001
  hardware 00:11:22:33:44:55
  fixed-address 10.0.0.101
  filename "/fts/mlinuz-2.4.26-ltsp-2"
}
```

```
host station002
  hardware 00:11:22:33:44:66
  fixed-address 10.0.0.102
  filename "/fts/2.4.26-ltsp-2/pxelinux.0"
}
```

```
host station003
  hardware 00:11:22:33:44:77
  fixed-address 10.0.0.103
  filename "/fts/mlinuz-2.4.26-ltsp-2"
}
```

```
host station004
  hardware 00:11:22:33:44:88
  fixed-address 10.0.0.104
  filename "/fts/mlinuz-2.4.26-ltsp-2"
}
```

确保每个文件名与服务器上 `/tftp` 目录中的 Linux 启动文件匹配。当你指定文件位置时，移除路径中的 `/tftp` 部分（因此 `/fts/mlinuz-2.4.26-ltsp-2`），因为

## 第 11 章 — 使用 LTSP 构建瘦身客户端服务器

`TFTP` 服务在 Red Hat Linux 环境运行。（在其他 Linux 系统上位置可能不同）。前面的代码中的 `workstation002` 显示了一个通过 `PXE` 网络启动的工作站配置示例（参见“启动工作站”部分）。服务器上的 `influx.0` 文件是一个 16KB 的引导文件（而不是用于启动机器的 2MB `vmlinuz` 文件）。先启动引导文件，然后加载内核，因为网卡上的 `PXE` 功能无法处理大于 32KB 的文件。

你可以添加任意数量的工作站（`host`）。你可以使用 IP 地址方案和主机命名方案，也可以编写自己的。但是，你需要确定用于工作站的每个硬件条目的网卡的 `MAC` 地址。

如果工作站上运行的是 Linux 版本，可以使用 `/sbin/ifconfig` 查看 `MAC` 地址。在 Windows 系统的 `DOS` 窗口中，输入 `ifconfig`。`MAC` 地址将分别通过 `HWaddr` 或 `Physical Address` 列出。

![](img/1b8a24a162893627b8005ac678b79236_327_0.png)

你看到的示例是一种相当安全的方法，因为只有特定网卡（基于唯一 `MAC` 地址）的计算机才能连接到它。在许多情况下，你可能只想让连接到局域网的任何机器都能启动到 `LTSP` 服务器。以下是更开放的 `LTSP` 设置中子网部分的样式：

```
subnet 10.0.0.50 255.255.255.0 {
  range 10.0.0.10 10.0.0.200;
  if subscribing (option vendor-class-identifier, 0, 9) = "PXClient"
  filename = "/ltsps/2.4.26-ltsp-2"; # PXE 引导器
else
  filename = "/vmlinuz-2.4.26-ltsp-2"; # 以太网内核
}
```

在这个示例中，`DHCP` 服务器将处理 `10.0.0.102` 到 `10.0.0.300` 范围内的地址。此示例改编自 `LTSP` `DHCP` 页面，那里显示了一个更长的示例（包括 `PPC` 启动）（`http://wiki.ltsp.org/wiki/bin/view/Ltsp`）。有关为 `LTSP` 服务器设置 `DHCP` 的更多细节，请参考该页面。

## TFTP 配置

启动 `ltspcfg` 命令后，输入 `4` 设置服务器的 `TFTP` 服务（`ftpd` 守护进程）。提示时，输入 `y` 启用该服务。在 Fedora 或其他 Red Hat 系统上，这将 `ftpd` 设置为启动，但不会立即启动服务。（按回车键返回菜单）。

## 304 第 IV 部分 — 小型企业项目

## Portmapper 配置
