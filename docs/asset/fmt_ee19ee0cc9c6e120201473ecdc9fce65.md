
## 2. 在启动 `iptables` 之前，您必须拥有一组可以工作的规则，并将其放置在 `/etc/sysconfig/iptables` 文件中。要创建这些规则，请参考接几个章节中的示例。（如果没有相应的配置文件，`iptables` 将静默失败。）

> 提示：如果您是 `iptables` 的新手，可以在安装 Fedora 或 RHEL 过程中通过配置防火墙，从一组可以运行的默认值开始。我建议您选择启用防火墙，并仅启用那些您已经准备好配置的服务。生成的 `/etc/sysconfig/iptables` 文件将让您学习 Fedora 或 RHEL 是如何创建规则的。

## 3. 如果您正在进行 NAT 或 IP 伪装（Masquerading），请开启 IP 数据包转发。允许此操作的一种方法是将 `/etc/sysctl.conf` 文件中的 `net.ipv4.ip_forward` 的值改为 `1`。以 root 用户身份使用任何文本编辑器打开该文件，并将该行修改如下所示：

```
net.ipv4.ip_forward = 1
```

## 4. 重启网络接口以使 IP 数据包转发生效。

```
# /etc/init.d/network restart
```

## 5. 规则就绪后，启动 `iptables`：

```
# /etc/init.d/iptables start
```

## 6. 此时，`iptables` 已作为您的防火墙安装。您可以使用 `lsmod` 命令检查 `iptables` 使用的模块已加载，如下：

```
# lsmod |grep ^iptables
ipt_REJECT 4736 1
ipt_state 1536 7
ipt_conntrack 24368 1 ipt_state
iptables_filter 2176 1
iptables_tables 13568 3 IPT_REJECT,ipt_state,iptable_tables
```

如果您的 `/etc/sysconfig/iptables` 文件存在错误，可以创建一个该文件的副本，然后通过运行 `system-config-securitylevel` 并设置基础防火墙来尝试创建一个可工作的配置。然后，您可以对防火墙进行更改以添加您需要的功能。

> 提示：随着您添加 `iptables`，会有更多的模块需要加载。当引入新规则时，应该自动加载相应的模块。在添加几个规则后，运行 `lsmod | grep ip` 查看添加了哪些模块。请注意，如果您决定停止 `iptables`，这些模块不会被卸载。它们将保持加载，直到下次重启或您将其删除（`modprobe -r`）。

后续章节包含 `iptables` 规则的示例。

# 创建 iptables 规则

配置 `iptables` 的一种方法是从命令行向内核添加和删除规则。当您获得了一组喜欢的规则时，请保存系统中当前运行的规则。您用于配置防火墙规则并使其持久化的工具如下：

- `iptables` — 使用此命令追加 (`-A`)、删除 (`-D`)、替换 (`-R`) 或插入 (`-I`) 规则。使用 `-L` 选项列出所有当前规则。
- `service save` — 使用此命令从内核保存规则并将其安装到配置文件中。
- `/etc/sysconfig/iptables` — 这是配置文件，包含了从 `service iptables save` 命令保存的规则。
- `/etc/sysconfig/iptables-config` — 您可以向 `iptables-config` 文件添加用于管理 `iptables` 规则的设置。例如，可以将任何 `iptables` 模块（如 `conrack`）添加到 `IPTABLES_MODULE` 行中以便自动加载。您还可以设置当 `iptables` 停止时，运行内核中的 `iptables` 表是否被保存到文件中。
- `/etc/init.d/iptables` — 这是 `iptables` 启动脚本，每次 Fedora 重启时必须自动运行。它启动时，会清除所有 `iptables` 规则和计数器，并从 `/etc/sysconfig/iptables` 文件安装新规则。您还可以从命令行使用此脚本的不同选项来检查 `iptables` 状态 (`status`) 或运行 `iptables-save` 为您保存当前规则 (`save`)。

为了开始使用 `iptables`，我提供了一组示例 `iptables` 规则以及如何根据不同情况更改这些规则的说明。以下是您可以加载并保存后续示例中描述的任何规则的方法：

### 1. 停止 `iptables` 并清除所有现有：

`/etc/init.d/iptables stop`

### 2. 使用任何文本编辑器将示例所示的规则添加到文件中。修改规则以适应您的情况并保存文件。

### 3. 以 root 用户身份运行该文件作为 shell 脚本。例如，如果您将其命名为 `firescript`，可以这样运行：

```
# sh firescript
```

### 4. 查看规则是如何加载到内核的：

```
# iptables -L
```

### 5. 如果一切看起来没问题，将现在内核中的规则保存到 `/etc/sysconfig/iptables` 文件中：

```
# cp /etc/sysconfig/iptables /etc/sysconfig/iptables-old
# service iptables save
```

从现在起，每当重启或重启 `iptables` 时，都会读取这些规则。保存一份您用于创建规则的脚本副本，以防您再次需要它。

# 示例 1：共享的防火墙

由于防火墙配置根据您尝试实现的目标而可能大不同，我说明了如何根据几种设置配置防火墙。此示例包含了一个充当 Web 服务器、FTP 服务器和 DNS 服务器的家庭办公室。图 14-2 显示了此配置。

如果您想使用后续的示例防火墙脚本，则必须更改以下信息以匹配您的配置：防火墙计算机设置如下：

- host — `127.0.0.1`（IP 地址）和 `lo`（接口）。您不需要更改这些内容。
- 连接到互联网 — `123.45.67.89`（IP 地址）和 `eth0`（接口）。请将它们替换为与您的互联网连接相关的 IP 地址和接口名称。
- 连接到局域网（LAN） — `10.0.0.1`（IP 地址）和 `eth1`（接口）。请将 `10.0.0.1` 和 `eth1` 分别替换为与您的局域网连接相关的 IP 地址和接口名称。
- 局域网上的计算机 — 示例中的每台计算机都有一个来自 `10.0.0.2/22` 的 IP 地址。

以下是一个 `iptables` 脚本示例，它展示了如何根据上述设置配置防火墙。防火墙计算机设置如下：

[![Figure 14-2: Home office acting as a Web server, FTP server, and DNS server]() 所示的配置]

由于防火墙配置根据您尝试实现的目标而可能大不同，我说明了如何根据几种设置配置防火墙。此示例包含了一个充当 Web 服务器、FTP 服务器和 DNS 服务器的家庭办公室。图 14-2 显示了此配置。

如果您想使用后续的示例防火墙脚本，则必须更改以下信息以匹配您的配置：防火墙计算机设置如下：

- host — `127.0.0.1`（IP 地址）和 `lo`（接口）。您不需要更改这些内容。
- 连接到互联网 — `123.45.67.89`（IP 地址）和 `eth0`（接口）。请将它们替换为与您的互联网连接相关的 IP 地址和接口名称。
- 连接到局域网（LAN） — `10.0.0.1`（IP 地址）和 `eth1`（接口）。请将 `10.0.0.1` 和 `eth1` 分别替换为与您的局域网连接相关的 IP 地址和接口名称。
- 局域网上的计算机 — 示例中的每台计算机都有一个来自 `10.0.0.2/22` 的 IP 地址。

以下是一个 `iptables` 脚本示例，它展示了如何根据上述设置配置防火墙。防火墙计算机设置如下：

[![Figure 14-2: Home office acting as a Web server, FTP server, and DNS server]() 所示的配置]

以下是一个 `iptables` 脚本示例，它展示了如何根据上述设置配置防火墙。
