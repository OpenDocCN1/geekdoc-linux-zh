

查看包含各种 *_id 程序* 输出的行。"by-id" 模式如果 ID_SERIAL 存在且不为空，则将使用它；否则，将使用 ID_MODEL 和 ID_REV 的组合。"by-path" 模式将使用 ID_PATH 值。如果默认模式不适用于你的情况，则可以对 `/etc/udev/rules.d/70-persistent-rules` 文件进行如下修改（其中 mode 为 "by-id" 或 "by-path" 之一）：

```
sed -i 's/link= /link=' /etc/udev/rules.d
```

请注意，此时没有必要创建规则或链接，因为你已经将主机的 `/dev` 目录绑定到了 Linux 系统中，规则和符号链接将在你首次启动 LFS 时创建。然而，如果你有多个设备，届时生成的符号链接可能指向与预期的不同的设备，因为设备并不是以可预测的顺序被发现的。在启动 LFS 系统时创建的分配将是稳定的，因此只有当你在两个系统上都使用符号链接指向同一个设备时，这才是一个问题。如果你有这种需求，请检查（并可能编辑）生成的 `/etc/udev.rules.d/70-persistent-rules` 文件。

## 7.4.3. 处理重复设备

如第 7.3 节“设备处理概述”所示，具有相同功能的设备在 `/dev` 中出现的顺序本质上是随机的。例如，如果你有一个 USB 摄像头和一个电视调谐器，有时 `/video0` 指向摄像头，`/video1` 指向调谐器，而有时重启后顺序会发生相反。对于除了声卡和网卡以外的所有类别，都可以通过创建自定义名称的 udev 规则来解决。对于你可能遇到此问题的每个设备（即使该问题在你当前的发行版中并不存在），在 `/sys/class` 或 `block` 下找到对应的目录。对于视频设备，这可能是 `/sys/class/videoX`。确定能够唯一标识设备的属性（通常厂商产品 ID 和/或序列号有效）：

```
adm /sys/class/video0
```

然后 udev 将创建符号链接：

```
# 持久化符号链接
KERNEL="video*", ATTRS{idProduct}="1910", ATTRS{idVendor}="0d81", SYMLINK+="webcam"
KERNEL="video*", ATTRS{device}="0x36f", ATTRS{vendor}="0x19e", SYMLINK+="tvtuner"
EOF
```

结果是 `/dev/video0` 和 `/video1` 仍然指向调谐器和摄像头（并且不应直接使用它们），但存在 `/dev/tvtuner` 和 `/dev/webcam` 符号链接，它们始终指向正确的设备。

## 7.5. 通用网络配置

### 7.5.1. 创建网络接口文件

网络脚本启动关闭哪些接口通常取决于 `/etc/sysconfig/` 下的文件。该目录应该包含每个需要配置的接口的文件，格式如 `ifconfig.xyz`，其中 "xyz" 描述网络网卡。接口名称（例如 `eth0`）通常是合适的。此文件包含该接口的属性，例如其 IP 地址、子网掩码和设置。文件名的主干必须是 `ifconfig`。

> **注意**
> 如果没有使用上一节中的步骤，udev 将根据系统物理特征（如 `enp2s1`）分配网络接口名称。如果你不确定接口名称是什么，可以在启动系统后运行 `link` 或 `ls /sys/class/net`。

以下命令为 `eth0` 设备创建一个带有静态 IP 地址的示例文件：

```
cd /etc/sysconfig/
cat > ifconfig.eth0 << "EOF"
ONBOOT=yes
INTERFACE=eth0
SERVICE=ipv4static
IP=192.168.1.2
GATEWAY=192.168.1.1
PREFIX=24
BROADCAST=192.168.1.255
EOF
```

必须在文件中更改其中的值以匹配适当的设置。

如果 `ONBOOT` 变量设置为 "yes"，则 System V 网络脚本将在系统启动期间启动网络接口卡（NIC）。如果设置为除 "yes" 以外的任何值，网卡将会被网络脚本忽略且不会自动启动。可以使用 `ifup` 和 `ifdown` 命令手动启动或停止接口。

`IFACE` 变量定义接口名称，例如 `eth0`。所有设备配置文件都是必须的。文件名扩展名必须与此值匹配。`FS-Bootscripts` 包具有模块化的 IP 分配格式，在 `/lib/services/` 目录下创建额外的文件允许其他 IP 分配方法。这通常用于动态主机协议（DHCP），BLFS 书中会有介绍。

`GATEWAY` 变量应该包含默认网关 IP 地址（如果存在）。如果没有，请注释掉 `PREFIX` 变量。

`PREFIX` 变量包含用于子网的位数。IP 地址中的每个字节是 8 位。如果子网掩码为 `255.255.255.0`，则它使用前 24 位来指定网络号。如果网络是 `255.255.255.240`，则它将使用前 28 位。比 24 位长的前缀通常由 DSL 和电缆的互联网服务提供商（ISP）使用。在本例中（`PREFIX=24`），掩码是 `255.255.255.0`。根据需要调整 `PREFIX`。

### 7.5.2. 创建 resolv.conf

系统需要某种方式来获取 DNS（域名系统）解析。通过以下方式创建 `resolv.conf`：

```bash
cat > resolv.conf << "EOF"
# Begin resolv.conf
domain <Domain>
nameserver <primary nameserver>
nameserver <secondary nameserver>
EOF
```

`resolv.conf` 中的 `domain` 语句可以省略，或者根据需要替换为 `search` 语句。请将 `nameserver` 替换为 DNS 服务器地址。

> **注意**
> 如果没有使用上一节中的步骤，udev 将根据系统物理特征分配网络接口名称（如 `enp2s1`）。如果你不确定接口名称是什么，可以在启动系统后运行 `link` 或 `ls /sys/class/net`。

### 7.5.3. 配置 hostname

在启动过程中，`/etc/hostname` 文件用于设置主机名：

```bash
echo "<hostname>" > /etc/hostname
```

```。

### 7.5.4. 自定义 /hosts 文件

为 `/etc/hosts` 文件确定 IP 地址、完全域名名（FQDN）以及可能的别名。`/etc/hosts` 的语法如下：

```
IP_address hostname.org [alias1] [alias2 ...]
```

即使不使用网卡，有效的 FQDN 也是必需的。这对某些程序的正确运行是必要的。

| 私有网络范围 | 正常前缀 |
| :--- | :--- |
| 10.0.0.1 | 8 |
| 172.x.0.1 - 172.x.255.254 | 16 |
| 192.168.y.1 - 192.168.y.254 | 24 |

x 可以是 16-31 之间的任何数字。y 可以是 0-255 之间的任何数字。根据特定需求自定义 `/etc/hosts`。对于你可能遇到此问题的每个设备（即使该问题在你当前的发行版中并不存在），在 `/sys/class` 或 `block` 下找到对应的目录。对于视频设备，这可能是 `/sys/class/videoX`。确定能够唯一标识设备的属性（通常厂商产品 ID 和/或序列号有效）：

```
adm /sys/class/video0
```

然后 udev 将创建符号链接：

```
# 持久化符号链接
KERNEL="video*", ATTRS{idProduct}="1910", ATTRS{idVendor}="0d81", SYMLINK+="webcam"
KERNEL="video*", ATTRS{device}="0x36f", ATTRS{vendor}="0x19e", SYMLINK+="tvtuner"
EOF
```

结果是 `/dev/video0` 和 `/video1` 仍然指向调谐器和摄像头（并且不应直接使用它们），但存在 `/dev/tvtuner` 和 `/dev/webcam` 符号链接，它们始终指向正确的设备。

如 7.3 节“设备处理”所示，具有相同功能的设备在 `/dev` 中出现的顺序本质上是随机的。例如，如果你有一个 USB 摄像头和一个电视调谐器，有时 `/video0` 指向摄像头，`/video1` 指向调谐器，而有时重启后顺序会发生相反。对于除了声卡和网卡以外的所有类别，都可以通过创建自定义名称的 udev 规则来解决。对于你可能遇到此问题的每个设备（即使该问题在你当前的发行版中并不存在），在 `/sys/class` 或 `block` 下找到对应的目录。对于视频设备，这可能是 `/sys/class/videoX`。确定能够唯一标识设备的属性（通常厂商产品 ID 和/或序列号有效）：

```
adm /sys/class/video0
```

然后 udev 将创建符号链接：

```
# 持久化符号链接
KERNEL="video*", ATTRS{idProduct}="1910", ATTRS{idVendor}="0d81", SYMLINK+="webcam"
KERNEL="video*", ATTRS{device}="0x36f", ATTRS{vendor}="0x19e", SYMLINK+="tvtuner"
EOF
```

结果是 `/dev/video0` 和 `/video1` 仍然指向调谐器和摄像头（并且不应直接使用它们），但存在 `/dev/tvtuner` 和 `/dev/webcam` 符号链接，它们始终指向正确的设备。

## 7.5. 通用网络配置

### 7.5.1. 创建网络接口文件

网络脚本启动关闭哪些接口通常取决于 `/etc/sysconfig/` 下的文件。该目录应该包含每个需要配置的接口的文件，格式如 `ifconfig.xyz`，其中 "xyz" 描述网络网卡。接口名称（例如 `eth0`）通常是合适的。此文件包含该接口的属性，例如其 IP 地址、子网掩码和设置。文件名的主干必须是 `ifconfig`。

> **注意**
> 如果没有使用上一节中的步骤，udev 将根据系统物理特征（如 `enp2s1`）分配网络接口名称。如果你不确定接口名称是什么，可以在启动系统后运行 `link` 或 `ls /sys/class/net`。

以下命令为 `eth0` 设备创建一个带有静态 IP 地址的示例文件：

```
cd /etc/sysconfig/
cat > ifconfig.eth0 << "EOF"
ONBOOT=yes
INTERFACE=eth0
SERVICE=ipv4static
IP=192.168.1.2
GATEWAY=192.168.1.1
PREFIX=24
BROADCAST=192.168.1.255
EOF
```

必须在文件中更改其中的值以匹配适当的设置。

如果 `ONBOOT` 变量设置为 "yes"，则 System V 网络脚本将在系统启动期间启动网络接口卡（NIC）。如果设置为除 "yes" 以外的任何值，网卡将会被网络脚本忽略且不会自动启动。可以使用 `ifup` 和 `ifdown` 命令手动启动或停止接口。

`IFACE` 变量定义接口名称，例如 `eth0`。所有设备配置文件都是必须的。文件名扩展名必须与此值匹配。`FS-Bootscripts` 包具有模块化的 IP 分配格式，在 `/lib/services/` 目录下创建额外的文件允许其他 IP 分配方法。这通常用于动态主机协议（DHCP），BLFS 书中会有介绍。

`GATEWAY` 变量应该包含默认网关 IP 地址（如果存在）。如果没有，请注释掉 `PREFIX` 变量。

`PREFIX` 变量包含用于子网的位数。IP 地址中的每个字节是 8 位。如果子网掩码为 `255.255.255.0`，则它使用前 24 位来指定网络号。如果网络是 `255.255.255.240`，则它将使用前 28 位。比 24 位长的前缀通常由 DSL 和电缆的互联网服务提供商（ISP）使用。在本例中（`PREFIX=24`），掩码是 `255.255.255.0`。根据需要调整 `PREFIX`。

### 7.5.2. 创建 resolv.conf

系统需要某种方式来获取 DNS（域名系统）解析。通过以下方式创建 `resolv.conf`：

```bash
cat > resolv.conf << "EOF"
# Begin resolv.conf
domain <Domain>
nameserver <primary nameserver>
nameserver <secondary nameserver>
EOF
```

`resolv.conf` 中的 `domain` 语句可以省略，或者根据需要替换为 `search` 语句。请将 `nameserver` 替换为 DNS 服务器地址。

> **注意**
> 如果没有使用上一节中的步骤，udev 将根据系统物理特征分配网络接口名称（如 `enp2s1`）。如果你不确定接口名称是什么，可以启动系统后运行 `link` 或 `ls /sys/class/net`。

### 7.5.3. 配置 hostname

在启动过程中，`/etc/hostname` 文件用于设置主机名：

```bash
echo "<hostname>" > /etc/hostname
```

### 7.5.4. 自定义 /hosts 文件

为 `/etc/hosts` 文件确定 IP 地址、完全域名名（FQDN）以及可能的别名。`/etc/hosts` 的语法如下：

```
IP_address hostname.org [alias1] [alias2 ...]
```

| 私有网络范围 | 正常前缀 |
| :--- | :--- |
| 10.0.0.1 | 8 |
| 172.x.0.1 - 172.x.255.254 | 16 |
| 192.168.y.1 - 192.168.y.254 | 24 |

x 可以是 16-31 之间的任何数字。y 可以是 0-255 之间的任何数字。根据特定需求自定义 `/etc/hosts`。

即使不使用网卡，有效的 FQDN 也是必需的。这对某些程序的正确运行是必要的。创建 `/etc/hosts` 文件并运行：

```bash
cat > /etc/hosts << "EOF"
# Begin /etc/
127.0.0.1 localhost
127.0.0.1 <FQDN> <HOSTNAME>
192.168.1.1 <FQDN> <HOSTNAME> [alias1] [alias2 ...]
::1 localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
# End /etc/
EOF
```

## 7.6. System V启动脚本用法和配置

### 7.6.1. System V启动脚本是如何工作的？

Linux 使用一种名为 SysVinit 的特殊启动方式，它基于运行级别（run-levels）的概念。不同版本之间可能差异很大，因此不能假设它们在特定的 Linux 发行版中工作正常；它们在 LFS 中也是如此。LTS 有自己的处理方式，但它通常接受标准。

