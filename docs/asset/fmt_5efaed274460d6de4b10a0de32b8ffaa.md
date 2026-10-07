
如果 `ONBOOT` 变量设置为 `"yes"`，系统网络脚本将在系统启动过程中启用网卡（NIC）。如果设置为 `"yes"` 之外的任何值，网卡将被网络脚本忽略且不会自动启动。可以使用 `ifup` 和 `ifdown` 命令手动启动或停止接口。

`IFACE` 变量定义了接口名称，例如 `eth0`。所有网络配置文件都需要它。文件扩展名必须匹配此值。

`SERVICE` 变量定义了用于获取 IP 地址的方法。LFS-Bootscripts 包具有模块化的 IP 分配格式，创建额外的文件可以实现此功能。

`GATEWAY` 变量应包含默认网关。

`PREFIX` 变量包含子网掩码位数。如果没有提供，则默认为 24。`BROADCAST` 变量是广播地址。根据设置更改 `PREFIX` 值。如果掩码是 255.255.255.0，则为 24 位。如果掩码是 255.255.255.128，则为 25 位。如果掩码是 255.255.0.0，则为 16 位。如果掩码是 255.0.0.0，则为 8 位。

`IP` 变量是 IP 地址。

如果 `ONBOOT` 变量设置为 `"yes"`，系统网络脚本将在系统启动过程中启用网卡（NIC）。如果设置为 `"yes"` 之外的任何值，网卡将被网络脚本忽略且不会自动启动。

`nameserver` 变量包含主 DNS 服务器地址。

### 9.5.2. 创建 resolv.conf 文件

为了解析域名，系统需要在 `/etc/resolv.conf` 文件中放置 DNS 服务器地址。如果需要，请在启动前创建文件。`resolv.conf` 文件可以包含多个 `nameserver` 条目，以备用 DNS 服务器地址。

`domain` 语句可以定义搜索域。如果不需要，可以将其注释掉。

通过运行以下命令创建 `/etc/resolv.conf`：

```bash
cat /etc/resolv.conf << "EOF"
# Begin /resolv.conf

domain <Domain>
nameserver <DNS 服务器地址>
nameserver <备用 DNS 服务器地址>

EOF
```

### 9.5.3. 配置系统 hostname

在启动过程中，系统使用 `/etc/hostname` 文件来确定主机名。通过运行以下命令创建 `/etc/hostname`：

```bash
echo "<hostname>" > /etc/hostname
```

### 9.5.4. 定制 /etc/hosts 文件

即使不使用网络连接，有效的 FDN 也对于某些程序的正确运行是必须的。在 `/etc/hosts` 文件中使用 IP 地址、完全限定域名（FQDN）以及可能的别名。格式如下：

```
IP_address myhost aliases
```

除非计算机对互联网可见，否则确保 IP 地址在私有网络范围内：

```
127.0.0.1 localhost.localdomain
127.0.1.1 <FQDN> <HOSTNAME>
<192.168.1.1> <FQDN> <HOSTNAME> [alias1] [alias2 ...]
::1 localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
```

创建 `/etc/hosts` 文件：

```bash
cat > /etc/hosts << "EOF"
# Begin /etc/hosts

127.0.0.1 localhost.localdomain
127.0.1.1 <FQDN> <HOSTNAME>
<192.168.1.1> <FQDN> <HOSTNAME> [alias1] [alias2 ...]
::1 localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters

# End /etc/hosts
EOF
```

## 9.6. System V 引导脚本使用与配置

### 9.6.1. System V 启动脚本是如何工作的？

Linux 使用一种基于运行级别（run-levels）概念的特殊启动方式 SysVinit。它在不同系统之间可能不同，因此不能假设某个特定的 Linux 发行版中的某些操作是有效的，它们会以自己的方式工作，但遵循了通用的标准。

SysInit（下文简称为“init”）使用运行级别（run-level）方案工作。共有七个（编号从 0 到 6）运行级别（实际上，还有更多运行级别，但它们用于特殊情况，通常不被使用）。详情请参阅 `init`（第 8 节），其中每一个运行级别都对应于计算机启动时应该执行的动作。默认运行级别为 3。以下是已实现的不同运行类别的描述：

```
0: 停止计算机
1: 单用户模式
2: 不带网络的多用户模式
3: 带网络的多用户模式
4: 留作自定义，否则功能与 3 相同
5: 与 4 相同，通常用于 GUI 登录（如 X 的 xdm 或 KDE 的 kdm）
6: 重启计算机
```

## 9.6.2. 配置 Sysinit

在内核初始化期间，运行的第一个程序是在命令行上指定的，或者默认为 `init`。该程序读取初始化文件 `/etc/inittab`。通过以下命令创建此文件：

```
cat > /etc/inittab << "EOF"
# Begin /etc/inittab
id3:initdefault:

s::sysinit:/etc/rc.d/init.d/rc

10:0:wait:/etc/rc.d/init.d/rc 0
11:1:wait:/etc/rc.d/init.d/rc 1
12:2:wait:/etc/rc.d/init.d/rc 2
13:3:wait:/etc/rc.d/init.d/rc 3
14:4:wait:/etc/rc.d/init.d/rc 4
15:5:wait:/etc/rc.d/init.d/rc 5
16:6:wait:/etc/rc.d/init.d/rc 6

ca:12345:ctrlaltdel::/bin/shutdown -tl -a -r now

su:SO106:once:/sbin/sulogin

1:2345:respawn:/sbin/agetty --nuclear tty1 9600
2:2345:respawn:/sbin/agetty tty2 9600
3:2345:respawn:/sbin/agetty tty3 9600
4:2345:respawn:/sbin/agetty tty4 9600
5:2345:respawn:/sbin/agetty tty5 9600
6:2345:respawn:/sbin/agetty tty6 9600

# /etc/inittab
EOF
```

关于此初始化文件的解释位于 `inittab` 的主页。对于 LFS 而言，运行的命令是 `rc`。上述初始化文件将指示 `rc` 运行 `/etc/rc.d` 中所有以 S 开头的脚本，紧接着运行 `/etc/rc.d` 中所有以 S 开头的脚本，其数字由默认值指定。

为了方便起见，`rc` 脚本会读取 `/lib/init-functions` 中的函数库。该库还会读取一个可选的配置文件 `/etc/sysconfig/rc`。后续章节中描述的任何系统参数都可以备选放在此文件中。

为了调试方便，脚本将所有输出记录到 `/run/log`。`/run` 目录是 `tmpfs`，此文件在重启后不会持久，但在启动过程结束时，会被追加到持久文件 `/var/log/boot` 中。

## 9.6.2. 修改运行级别

更改运行级别通过 `init <runlevel>` 完成，其中 `runlevel` 是目标运行级别。例如，要重启计算机，用户可以使用 `init 6` 命令，它是 `reboot` 命令的别名。同样，`init 0` 用于 `halt` 命令。

在 `/etc/rc.d` 下有许多看起来像 `rc.d?` 的目录（其中 `?` 是运行级别的数字），所有它们都包含许多符号链接。某些以 `K` 开头，另一些以 `S` 开头以启动服务。数字决定了脚本从 0 到 99 的执行顺序——数字越小执行越早。当 `init` 切换到另一个运行级别时，将根据所定的运行级别启动或停止相应的服务。

真正的脚本位于 `/etc/rc.d/init.d` 中。它们执行实际工作，所有的符号链接都指向它们。K 链接和 S 链接指向 `/etc/rc.d/init.d` 中的同一个脚本。当遇到 K 链接时，带 `stop` 参数运行相应的脚本。当遇到 S 链接时，带 `start` 参数运行相应的脚本。

此说明有一个例外。在 `rc.0` 和 `rc.d` 目录中以 S 开头的链接不会导致任何启动。如果系统只需要停止，它们将带有参数被调用。

以下是这些参数如何使脚本执行的描述：

- `start`: 启动服务。
- `stop`: 停止服务。
- `restart`: 停止服务然后重新启动。
- `reload`: 在修改配置文件后更新服务的配置，而无需重启。
- `status`: 告知服务是否正在运行以及具有哪些 PID。

可以随意修改启动过程的工作方式（毕竟，这是你自己的 LFS 系统）。这里提供的文件是实现如何操作的示例。

## 9.6.3. Udev 启动脚本

在内核初始化期间，运行的第一个程序是在命令行上指定的，或者默认为 `init`。该程序读取初始化文件 `/etc/inittab`。上述初始化文件将指示 `rc` 运行 `/etc/rc.d` 中所有以 S 开头的脚本，紧接着运行 `/etc/rc.d` 中所有以 S 开头的脚本，其数字由默认值指定。

为了方便起见，`rc` 脚本会读取 `/lib/init-functions` 中的函数库。该库还会读取一个可选的配置文件 `/etc/sysconfig/rc`。后续章节中描述的任何系统参数都可以备选放在此文件中。

为了调试方便，脚本将所有输出记录到 `/run/log`。`/run` 目录是 `tmpfs`，此文件在重启后不会持久，但在启动过程结束时，会被追加到持久文件 `/var/log/boot` 中。

更改运行级别通过 `init <runlevel>` 完成，其中 `runlevel` 是目标运行级别。例如，要重启计算机，用户可以使用 `init 6` 命令，它是 `reboot` 命令的别名。同样，`init 0` 用于 `halt` 命令。

在 `/etc/rc.d` 下有许多看起来像 `rc.d?` 的目录（其中 `?` 是运行级别的数字），所有它们都包含许多符号链接。某些以 `K` 开头，另一些以 `S` 开头以启动服务。数字决定了脚本从 0 到 99 的执行顺序——数字越小执行越早。当 `init` 切换到另一个运行级别时，将根据所定的运行级别启动或停止相应的服务。

真正的脚本位于 `/etc/rc.d/init.d` 中。它们执行实际工作，所有的符号链接都指向它们。K 链接和 S 链接指向 `/etc/rc.d/init.d` 中的同一个脚本。当遇到 K 链接时，带 `stop` 参数运行相应的脚本。当遇到 S 链接时，带 `start` 参数运行相应的脚本。

此说明有一个例外。在 `rc.0` 和 `rc.d` 目录中以 S 开头的链接不会导致任何启动。如果系统只需要停止，它们将带有参数被调用。

以下是这些参数如何使脚本执行的描述：

- `start`: 启动服务。
- `stop`: 停止服务。
- `restart`: 停止服务然后重新启动。
- `reload`: 在修改配置文件后更新服务的配置，而无需重启。
- `status`: 告知服务是否正在运行以及具有哪些 PID。

可以随意修改启动过程的工作方式（毕竟，这是你自己的 LFS 系统）。这里提供的文件是实现如何操作的示例。

## 9.6.5. 配置 Linux 控制台

本节讨论了如何配置控制台，设置键盘映射、字体和内核级别。非 ASCII 字符（如版权符号）将使用，控制台是美国式的，否则不是。如果没有配置（或 `rc` 中的相应设置），启动脚本将无所作为。`/etc/sysconfig/console` 文件应该包含 `VARIABLE="value"` 格式的行。以下变量是可识别的：

- `LOGLEVEL`: 该变量指定通过 `dmesg -n` 发送到控制台的内核日志级别。有效范围从“1”（无消息）到“8”。默认级别为“7”。
- `KEYMAP`: 该变量指定 `loadkeys` 程序的参数，通常是要加载的映射名称，例如 "it"。如果未设置变量，启动脚本将不会运行 `loadkeys` 程序，并将使用默认内核映射。注意某些映射具有同名的多个版本（qwerty/ 中的 cz 及其变体以及 olpc/ 中的 trf）。在这些情况下，还应指定父目录（例如 qwerty/）以确保加载正确的映射。
- `KEYMAP_CORRECTIONS`: 该（很少使用的）变量指定 `loadkeys` 程序的参数。如果键映射不完全满意且必须进行微调，则非常有用。例如，为了将欧元符号引入通常没有它的键图中，将此变量设置为 "euro2"。
- `FONT`: 该变量指定 `setfont` 程序的参数。通常包括字体名称、"-m" 以及要加载的应用程序字符映射名称。例如，为了加载 "lat16" 字体配合 "8859-1" 字符映射（这在美国是合适的），将此变量设置为 lat16 -m 8859-1。在 UTF-8 模式下，内核使用应用程序字符映射将键映射中的 8 位代码转换为 UTF-8，因此 "-m" 参数的设置应设置为组合键码的编码。
- `UNICODE`: 将此变量设置为 "1"、yes" 或 "true" 以将控制台处于 UTF-8 模式。这对于 UTF-8 区域语言很有用，否则会有害。

## LEGACY_CHARSET

对于许多键盘布局，Kbd 软件包中没有内置的 Unicode 键位图。如果此变量设置为可用的非 UTF-8 键位图的编码，控制台启动脚本将动态将可用的键位图转换为 UTF-8。

以下是一些示例：

- 对于非 Unicode 的设置，通常只需要 `KEYMAP` 和 `FONT` 变量。例如，对于波兰语设置，可以使用以下内容：

```
cat /etc/sysconfig/console << "EOF"
# Begin /etc/sysconfig/console

KEYMAP="pl22"
FONT="lat2a-16 -m 8859-22"

# End /etc/sysconfig/console
EOF
```

- 如上所述，有时需要对内置键位图进行微调。以下示例为德语键位图增加了欧元符号：

```
cat /etc/sysconfig/console << "EOF"
# Begin /etc/sysconfig/console

KEYMAP="de-latin1"
KEYMAP_CORRECTIONS="euro2"
FONT="lat0-16 -m 8859-15"
UNICODE="1"

# End /etc/sysconfig/console
EOF
```

- 以下是一个适用于保加利亚语的 Unicode 示例，其存在内置的 UTF-8 键位图：

```
cat /etc/sysconfig/console << "EOF"
# Begin /etc/sysconfig/console

UNICODE="1"
KEYMAP="bg_bds-utf8"
FONT="LatArCyrHeb-16"

# End /etc/sysconfig/console
EOF
```

由于上一个示例使用了 512 字符的 LatArCyrHeb-16 字体，除非使用帧缓冲区（framebuffer），否则 Linux 控制台将无法使用亮色。如果希望在不使用帧缓冲区的情况下使用亮色且不出现非本语言字符，仍然可以使用特定语言的 256 字符字体，如下所示：

```
cat > /etc/sysconfig/console << "EOF"
# /etc/sysconfig

UNICODE="1"
KEYMAP="bg_bd-utf8"
FONT="cyr-sun16"

# /etc/sysconfig/console
EOF
```

以下示例说明了键位图从 ISO-8859-15 到 UTF-8 的自动转换，并在 Unicode 模式下启用死键（dead keys）：

```
cat > /etc/sysconfig/console << "EOF"
# /etc/sysconfig

UNICODE="1"
KEYMAP="de-latin1"
KEYMAP_CORRECTIONS="euro2"
LEGACY_CHARSET="iso-8859-15"
FONT="LatArCyrHeb-16 -m 8859-15"

# /etc/sysconfig/console
EOF
```

某些键位图可能包含死键（即本身不产生字符，但会在下一个按键产生的字符上添加重音符号）或定义组合规则（例如：默认键位图中的“按下 Ctrl. A 获取 Æ”）。Linux-5.13 在非多字节模式下可以正确解释键位图中的死键和组合规则。这种缺陷不会影响欧洲语言的按键，因为这些语言通过添加重音来避免使用 ASCII 字符或组合两个 ASCII 字符。然而，在 UTF-8 中这是一个问题；例如对于希腊语，需要在字母“alpha”上加上重音符号。解决方案是避免使用 UTF-8，或者安装在输入处理上不具有此局限性的 Windows 系统。

对于中文、日语、韩语及某些其他语言，Linux 控制台无法配置为显示所需的字符。需要这些语言的用户应该安装 X Window 系统、涵盖必要字符范围的字体以及适当的输入法（例如支持多种语言的 SCIM）。

> [!TIP]
> `/etc/sysconfig/console` 文件仅控制 Linux 文本控制台的本地化。它与 X Window 系统中设置正确的键盘布局和终端功能、ssh 会话或串口控制台无关。在这些情况下，上述最后两项中提到的局限性并不适用。

## 9.6.6. 在启动时创建文件

有时在启动时创建文件是有意义的。例如，通常需要 `/tmp/.ICE-unix` 目录。这可以通过在 `/etc/sysconfig/createfiles` 配置脚本创建一个条目来实现。该文件的格式嵌入在默认配置文件的注释中。
