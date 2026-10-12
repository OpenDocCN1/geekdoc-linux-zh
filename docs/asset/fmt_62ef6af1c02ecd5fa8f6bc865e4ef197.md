
## 额外的网络命令

虽然本书专注于考试涵盖的主题，但我希望你了解常用的网络命令。这些命令在以下情况下非常有用：

- `dig`：域名信息，一个允许你查询 DNS 的工具。
- `wireshark`：类似于 `tcpdump`，但更强大且以图形界面显示。
- `ethtool`：允许对网络驱动进行更改。
- `strace`：一个优秀的故障排除工具。它可以记录程序的

`NetworkManager` 自带有实用工具。例如，`nm-tool` 命令提供了有关网络设备状态的信息，如示例 16-5 所示。

### 示例 16-5 `nm-tool` 命令

```
[root@localhost]# nm-tool

NetworkManager Tool

State: connected

Device: eth0 [System eth0] ---------------------------------------

Type:               Wired

Driver:             e1000

State:              connected

Default:            yes

HW Address:         08:00:27:E0:E2:DE

Capabilities:

  Carrier Detect:   yes

  Speed:             1000 Mb/s

Wired Properties

  Carrier:           on

IPv4 Settings:

  Address:           10.0.2.15

  Prefix:            24 (255.255.255.0)

  Gateway:           10.0.2.2

DNS:                192.168.1.1
```

另一个有用的 `NetworkManager` 命令是 `nmcli` 命令。它为 `NetworkManager` 提供了一个命令行界面，允许你查看有关 `NetworkManager` 的信息及其更改。

例如，你可以通过执行以下命令查看 `Network-Manager` 组件的当前状态：

```
[root@localhost]# nmcli status

RUNNING     STATE       WIFI-HARDWARE WIFI      WWAN-HARDWARE WWAN

running     connected   enabled      enabled      enabled
```

你也可以通过执行以下命令禁用 WiFi：

```
[root@localhost]# nmcli wifi off
```

还有一个基于 GUI 的工具称为连接编辑器（Connection Editor）：

```
[root@localhost]# nm-connection-editor
```
