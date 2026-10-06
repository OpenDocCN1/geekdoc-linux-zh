
该值可以以 `ifname/`、`uuid/` 或 `id/` 为前缀以消除歧义。

`<config file>|<原始 JSON 数据>`

- team 的 JSON 配置

## bridge (桥接):

`[stp yes|no]`

- 控制在此桥接上启用生成树协议 `STP`（默认值: `yes`）

`[priority <num>]`

- 设置 `STP` 优先级（默认: `128`）

`[forward-delay <2-30>]`

- `STP` 转发延迟，单位为秒（默认: `15`）

`[hellotime <1-10>]`

- `STP` Hello包时间，单位为秒（默认: `2`）

`[max-age <6-42>]`

- `STP` 最大消息年龄，单位为秒（默认: `20`）

`[aging-time <0-1000000>]`

- 以太网 `MAC` 地址老化时间，单位为秒（默认: `300`）

`[mac <MAC 地址>]`

- 桥接 `MAC` 地址（注意：这需要较新的内核特性，最初在 `3.15` 上游内核中引入）

## bridge-slave (桥接从设备):

`master <ifname, 或连接 UUID 或名称>`

- `bridge` 接口名称，或桥接主连接配置的 `UUID` 或 `ID`。该值可以以 `ifname/`、`uuid/` 或 `id/` 为前缀以消除歧义。

`[priority <0-63>]`

- 此从设备的 `STP` 优先级（默认: `52`）

`[path-cost <1-65535>]`

- 通过此从设备到达目的地的 `STP` 端口开销（默认: `100`）

`[hairpin yes|no]`

- 从设备的“回环模式”，允许通过接收到帧的从设备接口发送出去（默认: `yes`）

## vpn:

`type openvpn|pptp|openconnect|openswan|ssh|l2tp|wireguard [user <username>]`

- `VPN` 类型
- `VPN` 用户名

## mesh (网格):

`ssid <SSID> [channel <number>]`

- 网络使用的通道
- 通过 `DHCP` 请求 `IP` 地址时使用的 `MAC` 地址

## IP_OPTIONS (IP 选项):

`ip4 <IPv4 地址> [gw4 <IPv4 网关>]`

- `IPv4` 地址

`ip6 <IPv6 地址> [gw6 <IPv6 网关>]`

- `IPv6` 地址

`edit [id | uuid | path | <ID>]`

`edit type <new connection type> [name <new connection name>]`

使用交互式编辑器编辑现有连接或添加新连接。现有连接通过其名称、`UUID` 或路径识别。如果 `<ID>` 存在歧义，可以使用关键字 `id`、`uuid` 或 `path`。使用 `connection show` 查看 `<ID>` 的描述。不提供 `<ID>` 意味着将创建一个新连接。交互式编辑器将引导你完成连接编辑，并允许你通过简单的菜单驱动界面根据需要更改连接参数。编辑器会指示哪些设置和属性可以修改并提供内联帮助。

可用选项：

`type` - 新连接的类型；有效类型与 `connection` 命令相同

`name` - 新连接的名称。稍后可以在编辑器中更改。

`modify [temporary | id | uuid | path | <ID>] -setting.<property> <value> [-setting.<property> <value>] ...`

修改连接配置中的一个或多个属性。连接通过名称、`UUID` 或路径识别。如果 `<ID>` 存在歧义，可以使用 `id`、`uuid` 或 `path`。请参见 `(5)` 获取设置和属性名称、其描述和默认值。此命令支持设置名称和属性名称的缩写，前提是它们是唯一的。空值将移除属性值（将属性设为默认值）。提供的值将覆盖现有值。如果你想在现有值后添加一个项，如果你想从容器属性中删除一个项，请使用属性名并指定要删除项的从零开始的索引（作为命名选项的值）。这对于像 `ipv4.addresses`、`bond.options` 等多值容器属性具有实际效果。连接配置的更改将由 `NetworkManager` 持久保存，除非提供了临时选项，在这种情况下更改在 Network 重后不会保留。

`delete [id | uuid | path] <ID> ...`

删除已配置的连接。连接通过名称、`UUID` 或 D-Bus 路径识别。如果 `<ID>` 存在歧义，请使用上面的 `connection show` 查看 `<ID>` 键的描述。如果未指定“wait”选项，默认超时时间为 `10` 秒。

## reload

从磁盘重载所有连接。`NetworkManager` 默认不监控连接文件的更改。你需要使用此命令让 `NetworkManager` 在连接发生更改时从磁盘重新读取配置。可以启用自动加载功能，然后 `NetworkManager` 将在文件发生任何变化时重加载（`(5)` 中的 `monitor-connection-files=true`）。

`load <filename>`

从磁盘加载/重载一个或多个连接文件。在编辑连接后使用此命令以确保 `NetworkManager` 了解其最新状态。

## device - 显示和管理网络接口

`COMMAND := { status | show | connect | disconnect | delete | wifi | status }`

`status`

打印设备状态。如果没有对设备对象指定命令，这是默认操作。

`show [<ifname>]`

显示设备的详细信息。如果不带参数，则显示所有设备。

`connect <ifname>`

连接设备。`NetworkManager` 将尝试找到并激活相应的连接。如果没有指定 `wait` 选项，默认超时时间为 `90` 秒。

`disconnect <ifname> ...`

断开设备并防止设备自动激活连接。如果没有指定 `wait` 选项，默认超时时间为 `10` 秒。

`delete <ifname>`

删除设备。此命令从系统中删除接口。注意，这仅适用于 `bond`、`bridge` 等软件设备。硬件设备（如以太网）无法通过此命令删除。如果没有指定 `wait` 选项，默认超时时间为 `10` 秒。

## wifi [list [ifname]] [ssid <BSSID>]

列出可用 `Wi-Fi` 接入点。`ifname` 和 `ssid` 选项分别用于列特定接口或特定 `BSSID` 的接入点。

## wifi connect <BSSID> [password <password>] [wep-key-type key<phrase>] [ifname <ifname>] [ssid <BSSID>]

连接到通过 `SSID` 或 `BSSID` 指定的 `Wi-Fi` 网络。该命令将在设备上激活它。这是 GUI 客户端点击 `SSID` 的命令行对应。此命令始终创建一个新连接，主要用于连接新的 `Wi-Fi` 网络。对于已存在的网络，最好按照如下方式启动（激活）现有连接：`nmcli con <name>`。目前仅支持开放、`WEP` 和 `WPA-PSK` 网络。还假设通过 `DHCP` 获取 `IP` 配置。如果没有指定 `wait` 选项，默认超时时间为 `90` 秒。

可用选项：

- `password` - 安全网络（`WEP` 或 `WPA`）的密码
- `wep-key-type` - `WEP` 密钥类型，`ASCII/HEX` 密钥或密码
- `ifname` - 用于激活的接口
- `ssid` - 如果指定，创建的连接将限制特定的 `BSSID`
- `name` - 如果指定，连接将使用该名称（否则 `NM` 会自行生成名称）
- `private` - 如果设置为 `yes`，连接仅对创建它的用户可见。否则连接是全局的（默认值）。
- `hidden` - 在首次连接到不广播 `SSID` 的 `AP` 时设置为 `yes`。其他 `SSID` 将无法被发现且连接尝试将失败。

## wifi rescan [ifname <ifname>] [[ssid <BSSID> ...]

请求 `NetworkManager` 立即重新扫描可用 `Wi-Fi` 接入点。`NetworkManager` 定期扫描 `Wi-Fi` 网络，但在某些情况下手动启动扫描可能有用（例如在唤醒电脑后）。通过 `ssid`，可以扫描特定的 `SSID`，这对于隐藏 `SSID` 的 `AP` 很有用。你可以提供多个 `ssid` 参数以扫描 `SSIDs`。此命令不显示接入点（`APs`），请使用 `‘nmcli wifi list’` 查看。`wimax [list [ifname <ifname>] [nsp <name>]]` 列出可用的 `WiMax NSP`。`ifname` 和 `nsp` 选项可以分别用于列出特定接口或特定 `NSP` 的网络。

# agent -将 nmcli 作为 NetworkManager 密钥代理（secret agent）或 polkit 代理运行

```
COMMAND := { secret | polkit | all }
```

`secret`

将 `nmcli` 注册为 `NetworkManager` 密钥代理并监听凭据请求（secret requests）。你通常不需要此命令，因为 `nmcli` 在连接到网络时可以处理这些凭据。但是，当你使用其他工具激活连接且没有可用的密钥代理（如 `nm-applet`）时，你可能会发现该命令有用。

`polkit`

将 `nmcli` 注册为当前用户会话的 `polkit` 代理并监听授权请求（authorization requests）。你通常不需要此命令，因为 `nmcli` 可以处理与 `NetworkManager` 操作相关的 `polkit` 动作（当带有 `--ask` 选项运行时）。但是，当你想要运行一个简单的文本界面 `polkit` 代理且没有桌面环境代理时，你可能会发现该命令有用。注意，运行此命令会让 `nmcli` 处理所有的 `polkit` 请求，而不仅仅是与 `NetworkManager` 相关的，因为一个会话只能运行一个 `polkit` 代理。

`all`

同时作为 `NetworkManager` 密钥代理和 `polkit` 代理运行 `nmcli`。

# 环境变量

`nmcli` 的行为受以下环境变量的影响。

# LC_ALL

如果设置为非空字符串值，它将覆盖所有其他国际化变量的值。

# LC_MESSAGES

确定用于国际化消息的区域（locale）。

# LANG

为未设置或为空的国际化变量提供默认值。

国际化说明：请注意 `nmcli` 是本地化的，因此输出取决于你的环境。在解析输出时意识到这一点非常重要。在脚本执行时，请调用 `LC_ALL=C nmcli` 以确保将区域设置设置为“C”。

`+ 0` 成功 - 表示操作成功

`1` 未知或未指定的错误

`2` 用户输入无效，`nmcli` 调用错误

`3` 超时（参见 `--wait` 选项）

`4` 连接激活失败

`5` 连接去激活失败

`6` 设备断开失败

`7` 删除删除失败

`8` `NetworkManager` 未运行

`9` `nmcli` 和 `NetworkManager` 版本不匹配

`10` 连接、设备或接入点不存在。

## 示例

本节展示了 `nmcli` 使用的各种示例。如果你需要更多示例，请参考 `(5)` 手册页。

```
nmcli -t -f RUNNING general
告诉你 NetworkManager 是否正在运行。
```

```
nmcli -t -f STATE general
显示 NetworkManager 的整体状态。
```

```
nmcli radio wifi off
关闭 Wi-Fi。
```

```
nmcli connection show
列出 NetworkManager 拥有的所有连接。
```

```
nmcli connection show -m multiline -f all con show
以多行模式显示所有配置的连接。
```

```
nmcli connection show -active
列出所有当前激活的连接。
```

```
nmcli -f name,autoconnect s
显示所有连接配置名称及其自动连接属性。
```

```
nmcli -p connection show "My default em1"
显示 "My default em1" 连接配置的详细信息。
```

```
nmcli connection show --show-secrets "My Home WiFi"
显示 "My Home WiFi" 连接配置的详细信息以及所有密码。
--show-opts
```

## 另另

完整文档位于：`<>` 或通过本地命令查看：`info ‘(coreutils) nproc invocation’`

# NROFF

`+` > 名字

`nroff` - 使用 `groff` 模拟 `nroff` 命令

## 概要

```
[-CchipStUvwW] [-dcs] [-Mdir] [-mmname] [-nnum] [-olist] [-rcn] [-Tname] [file~...] — 帮助 -v |--version
```

## 描述

`nroff` 脚本使用 `groff` 模拟 `nroff` 命令。只有 `ascii`、`latin1`、`utf8` 和 `cp1047` 设备被 `nroff` 接受，用于选择由 `grotty`（`groff` 的 `TTY` 输出设备）发出的输出编码。如果未通过 `GROFF_TYPESETTER` 环境变量或 `-T` 命令行选项（后者会覆盖环境变量）指定（合法的）设备，`nroff` 将检查当前的区域设置（locale）以选择默认输出设备。它首先尝试 `locale` 程序，然后是环境变量 `LC_ALL`、`LC_CTYPE` 和 `LANG`，最后是 `LESSCHARSET` 环境变量。

`-h` 和 `-c` 选项等于 `grotty` 的选项 `-h`（在输出中使用制表符）和 `-c`（使用旧输出方案而非 `SGR` 转义序列）。`-d`, `-C`, `-i`, `-m`, `-n`, `-o`, `-r`, `-w` 和 `-W` 的效果如 `(1)` 所示。此外，`nroff` 静默忽略选项 `-e`、`-q` 和 `-s`（这些选项在 `troff` 中未实现）。选项 `-p` (`pic`)、`-t` (`tbl`)、`-S` (`safer`) 和 `-U` (`unsafe`) 会传递给 `groff`。`-v` 和 `--version` 显示版本号，`--help` 打印帮助信息。

# 环境变量

`GROFF_TYPESETTER`

`groff` 的默认设备。如果没有设置（通常情况），则默认为 `'ps'`。

`GROFF_BIN_PATH`

一个用冒号分隔的目录列表，在搜索 `PATH` 之前从中搜索 `groff` 可执行文件。如果未设置，则使用 `'/usr/bin'`。

# 注意事项

此 shell 脚本基本上旨在用于 `(1)`。还加载了 `nroff` 风格的字符定义（在 `tty-char.tmac` 文件中）以模拟无法表示的字形。

## 另另

`(1)`, `(1)`, `(1)`

允许在上述修改版本的条件下将此手册的翻译版本复制并分发到另一种语言，但此许可公告可以包含在自由软件基金批准的翻译中，而不是原始英文版中。

# NSENTER

`+` > 名字

`nsenter` - 使用其他进程的命名空间运行程序

## 概要

```
nsenter [options] [program [arguments]]
```

## 描述

进入一个或多个其他进程的命名空间并执行指定的程序。可以进入的命名空间有：

### 挂载命名空间 (mount namespace)

挂载和卸载文件系统不会影响系统的其他部分（`CLONE_NEW` 标志），除非显式标记为共享的文件系统（使用 `mount --make-shared`；共享标志请参阅 `/proc/self/mountinfo`）。

### UTS 命名空间

设置主机名或域名不会影响系统的其他部分。（`CLONE_NEWUTS` 标志）

### IPC 命名空间

该进程将为 `System V` 消息队列、信号量和共享内存段拥有独立的命名空间。（`CLONE_NEWIPC` 标志）

### 网络命名空间 (network namespace)

进程将拥有独立的 `IPv4` 和 `IPv6` 栈、`IP` 路由表、防火墙规则、`/proc/net` 和 `/sys/class/net` 目录树、socket 等。（`CLONE_NEWNET` 标志）

### PID 命名空间

子进程将有一组与 `nsenter` 进程不同的 `PID` 进程映射（`CLONE_NEWPID` 标志）。`nsenter` 默认通过更改 `PID` 命名空间进行 `fork`，使得新程序及其子进程共享相同的 `PID` 命名空间并互相可见。如果使用 `no-fork`，则新程序将在不 `fork` 的情况下执行 `exec`。

### 用户命名空间 (user namespace)

进程将拥有一组不同的 `UIDs`、`GIDs` 和能力。（`CLONE_NEWUSER` 标志）。

有关标志的确切语义请参阅 `(2)`。

如果未给出 `program`，则运行 `"${SHELL}"`（默认：`/bin/sh`）。

## 选项

`-t, --target pid`

指定一个目标进程以获取上下文。由 `pid` 指定的上下文路径分别为：

- `/proc/pid/ns/mnt`: 挂载命名空间
- `/proc/pid/ns/uts`: `UTS` 命名空间
- `/proc/pid/ns/ipc`: `IPC` 命名空间
- `/proc/pid/ns/net`: 网络命名空间
- `/proc/pid/ns/pid`: `PID` 命名空间
- `/proc/pid/ns/user`: 用户命名空间
- `/proc/pid/root`: 根目录
- `/proc/pid/cwd`: 工作目录

`-m, --mount[=file]` 进入挂载命名空间。如果没有指定文件，则进入目标进程的挂载命名空间。如果指定了文件，则进入文件指定的挂载命名空间。

`-u, --uts[=file]` 进入 `UTS` 命名空间。如果没有指定文件，则进入目标进程的 `UTS` 命名空间。如果指定了文件，则进入文件指定的 `UTS` 命名空间。

`-i, --ipc[=file]` 进入 `IPC` 命名空间。如果没有指定文件，则进入目标进程的 `IPC` 命名空间。如果指定了文件，则进入文件指定的 `IPC` 命名空间。

`-n, --net[=file]` 进入网络命名空间。如果没有指定文件，则进入目标进程的网络命名空间。如果指定了文件，则进入文件指定的网络命名空间。
