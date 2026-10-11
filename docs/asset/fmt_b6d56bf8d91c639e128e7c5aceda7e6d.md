
## 7.5. 通用网络配置

### 7.5.1. 创建网络接口配置文件

网络脚本启动和关闭哪些接口通常取决于 `/etc/sysconfig/` 中的文件。该目录应包含每个需要配置的接口对应的文件，格式为 `ifconfig.xyz`，其中 "`xyz`" 应该描述网卡。接口名称（例如 `eth0`）通常是合适的。此文件中包含该接口的属性，例如其 IP 地址、子网掩码等。文件名的主干部分（stem）必须是 `ifconfig`。

> 注意
>
> 如果没有使用上一节中的步骤，Udev 将根据物理特性（如 `enp2s1`）分配网络接口名称。如果你不确定接口名称是什么，在启动系统后可以随时运行 `ip link` 或查看 `/sys/class/net`。

以下命令为 `eth0` 设备创建一个带有静态 IP 地址的示例文件：

```
cd /etc/sysconfig/
cat > ifconfig.eth0 << "EOF"
ONBOOT=yes
IFACE=eth0
SERVICE=ipv4-static
IP=192.168.1.2
GATEWAY=192.168.1.1
PREFIX=24
BROADCAST=192.168.1.255
EOF
```

为了进行正确的设置，必须在每个文件中更改变量的值。

如果 `ONBOOT` 变量设置为 "`yes`"，System V 脚本将在系统启动期间启动网卡（NIC）。如果你将任何其他项设置为 "`yes`"，网卡将被网络脚本忽略且不会自动启动。可以使用 `ifup` 和 `ifdown` 命令手动启动或停止接口。

`IFACE` 变量定义了接口名称，例如 `eth0`。所有网络设备配置文件中都是必需的。

`SERVICE` 变量定义了用于获取 IP 地址的方法。LFS-Services 软件包采用了模块化的分配格式，在 `/lib/services/` 目录下创建额外的文件允许使用其他分配方法。这通常用于动态主机协议（DHCP），该内容在 BLFS 中介绍。

`GATEWAY` 变量应包含默认网关地址，如果存在，则注释掉该变量。

`PREFIX` 变量包含子网中使用的位数。IP 地址中的每个字节是 8 位。如果子网掩码是 255.255.255.0，则是 24 位。长 24 位的前缀通常由 DSL 和电缆互联网提供商（ISP）使用。在示例（`PREFIX=24`）中，掩码是 255.255.255.0。调整 `PREFIX` 变量到你的子网。如果省略，默认为 24。

### 7.5.2. 创建 /etc/resolv.conf 文件

系统需要一些域名系统（DNS）手段将解析到 IP 地址，反之亦然。最佳方法是将 ISP 或网络管理员提供的 DNS 服务器 IP 地址放入 `/etc/resolv.conf`。运行以下命令创建文件：

```
cat > /etc/resolv.conf << "EOF"
# Begin /resolv.conf

domain <Your Domain Name>
nameserver <primary nameserver>
nameserver <secondary nameserver>

# End /resolv.conf
EOF
```

`domain` 语句可以省略或替换为 `search` 语句。详情请 `resolv.conf` 手页。将 `nameserver` 地址替换为最适合设置的 IP 地址。会有多个条目（备用服务器）。如果你只需要一个 DNS 服务器，请从文件中删除 `nameserver` 行。IP 地址可以是本地网络上的路由器。

> 注意
>
> 公共 IPv4 地址是 `8.8.8.8` 和 `8.8.4.4`。

### 7.5.3. 配置系统主机名

在启动过程中，`etc/hostname` 文件用于建立系统主机名。运行以下命令创建 `/etc/hostname` 并输入主机名：

```
echo "<hostname>" > /etc/hostname
```

`<hostname>` 需要替换为赋予计算机的名字。不要输入域名（FQDN）。该信息放在 `/etc/hosts` 文件中。

### 7.5.4. 自 /etc/hosts 文件

确定 `/etc/hosts` 文件中的 IP 地址、完全限定域名（FQDN）以及可能的别名。语法如下：

```
IP_address myhost.example.org aliases
```

除非计算机要对互联网可见（即有一个注册域名和有效的分配地址范围——大多数用户没有），否则请确保 IP 地址在私有网络范围内。有效范围如下：

| 私有网络地址 | 正常前缀 |
|---|---|
| 10.0.0.1 - 10.255.255.254 | 8 |
| 172.x.0.1 - 172.x.255.254 | 16 |
| 192.168.y.1 - 192.168.y.254 | 24 |

`x` 可以是 16-31 之间的任何数字。`y` 可以是 0-255 之间的任何数字。有效的私有 IP 地址可以是 `192.168.1.1`。此 IP 的有效 FQDN 可能是 `lfs.example.org`。

即使不使用网卡，仍然需要有效的 FQDN。这是某些程序正确运行的必要。运行以下命令创建 `/etc/hosts` 文件：

```
cat > /etc/hosts << "EOF"
# Begin /etc/hosts
127.0.0.1 localhost
127.0.0.1 <FQDN> <HOSTNAME>
<192.168.1.1> <FQDN> <HOSTNAME> [alias1] [alias2 ...]
::1 localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
# End /etc/hosts
EOF
```

`192.168.1.1>` `<FQDN>` 和 `<HOSTNAME>` 值需要根据特定用途或需求更改（如果由网络/系统管理员分配了 IP 地址且机器将连接到现有网络）。可选的别名可以省略。

## 7.6. System V 启动脚本的使用和配置

### 7.6.1 System V 启动脚本是如何工作的？

Linux 使用基于运行级别（run-levels）概念的特殊启动设施 SysVinit。它在不同系统之间可能很大，因此不能假设在某个特定 Linux 发行版中运行的东西在 LFS 中也应该工作。LFS 有它自己的处理方式，但它通常接受标准。

SysVinit（以后将称为 "`init`」）使用运行中的运行级别。共有七个（0 到 6 个运行级别，实际上还有更多级别，但它们用于特殊情况且通常不使用）。请查看 `init`（详见第 8 节），每个级别对应于计算机启动时应该执行的操作。默认运行级别为 3。以下是实现的不同运行级别的描述：

+   0: 停止计算机
+   1: 单用户模式
+   2: 不带网络的多用户模式
+   3: 带有网络的多用户模式
+   4: 留作自定义，否则与 3 相同
+   5: 与 4 相同，通常用于 GUI 登录（如 X xdm 或 KDE 的 kdm）
+   6: 重启计算机

### 7.6.2. 配置 Sysvinit

在内核初始化期间，运行的第一个程序要么是在命令行中指定的，要么是默认的 `init`。该程序读取初始化文件 `/etc/initab`。通过以下命令创建此文件：

```bash
cat > /etc/initab << "EOF"
# Begin /etc/initab

id:3:initdefault

si::sysinit:/etc/rc.d/init.d/rc S

10:0:wait:/etc/rc.d/init.d/rc 0
11:S:wait:/etc/rc.d/init.d/rc 1
12:2:wait:/etc/rc.d/init.d/rc 2
13:3:wait:/etc/rc.d/init.d/rc 3
14:4:wait:/etc/rc.d/init.d/rc 4
15:5:wait:/etc/rc.d/init.d/rc 5
16:6:wait:/etc/rc.d/init.d/rc 6

ca:12345:ctrltdelt:/sbin/shutdown -tl -a -r now

su:S016:once:/sbin/slogin

1:2345:respawn:/sbin/agetty --nuclear tty1 9600
2:2345:respawn:/sbin/agetty tty2 9600
3:2345:respawn:/sbin/agetty tty3 9600
4:2345:respawn:/sbin/agetty tty4 9600
5:2345:respawn:/sbin/agetty tty5 9600
6:2345:respawn:/sbin/agetty tty6 9600

# End /etc/initab
EOF
```

关于此初始化文件的解释请参考 `initab` 的主页。对于 LFS 来说，运行的关键命令是 `rc`。上面的初始化文件将指示 `rc` 运行 `/etc/rc.d/rcS` 目录中所有以 S 开头的脚本，然后运行 `/etc/rc.d/rc?` 目录中其中问号由 `initdefault` 值指定的脚本。
