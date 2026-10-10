

本身（通过检查已存在的路由和设备规范，以及路由被添加的位置）。在大多数正常网络中，你不需要这样做。

如果 **dev** 是命令行中的最后一个选项，则由于它是默认值，可以省略 **dev** 一词。否则，路由修饰符的顺序（metric - netmask - gw - dev）并不重要。

## 示例

**route add -net 127.0.0.0** 添加标准的回环条目，使用子网掩码 255.0.0.0（A 类网络，由目的地址决定），并关联到 “lo” 设备（假设该设备此前已通过 **ifconfig**(8) 正确设置）。

**route add -net 192.56.76.0 netmask 255.255.255.0 dev eth0** 通过 “eth0” 添加指向网络 192.56.76.x 的路由。C 类子网掩码修饰符在此处并非绝对必要，因为 192.* 是 C 类 IP 地址。此处可以省略 “dev” 一词。

**route add default gw mango-gw** 添加一条默认路由（如果没有其他路由匹配，则使用此路由）。使用此路由的所有数据包将通过 “mango-gw” 进行网关转发。实际用于该路由的设备取决于如何到达 “mango-gw” —— 必须事先设置好指向 “mango-gw” 的静态路由。

**route add ipx4 sl0** 通过 SLIP 接口添加指向 “ipx4” 主机的路由（假设 “ipx4” 是 SLIP 主机）。

**route add -net 192.57.66.0 netmask 255.255.255.0 gw ipx4** 此命令将网络 “192.57.66.x” 添加为通过前述指向 SLIP 接口的路由进行网关转发。

**route add -net 224.0.0.0 netmask 240.0.0.0 dev eth0** 这是一个相对冷门但已被记录的配置，旨在让人们知道如何操作。这将所有 D 类（组播）IP 路由设置为通过 “eth0” 转发。这是具有组播内核的正确常规配置行。

**route add 10.0.0.0 netmask 255.0.0.0 reject** 这安装了一个针对私有网络 “10.x.x.x” 的拒绝路由。

## 输出

内核路由表的输出按以下列组织：

- **Destination** 目的网络或目的主机。
- **Gateway** 网关主机，如果未设置则为 '*'。
- **Genmask** 目的网络的子网掩码，对于主机目的地址为 `255.255.255.255`，对于 **default** 路由为 `0.0.0.0`。
- **Flags** 可能的标志有：
    - **U**（路由已 **Up** 启动）
    - **H**（目标是**主机**）
    - **G**（使用**网关**）
    - **R**（为动态路由**重新建立**路由）
    - **D**（由守护进程或重定向**动态**安装）
    - **M**（由路由守护进程或重定向**修改**）
    - **!**（**拒绝**路由）
- **Metric** 到目标的‘*距离*’（通常以跳数计算）。它不被最近的内核使用，只有路由守护程序可能会使用它。
- **Ref** 对该路由的引用计数。在 Linux 内核中不使用，始终为 0。
- **Use** 对该路由的查找计数。在较新的内核中，这些数值非常低，因为套接字拥有自己的缓存，不需要查找路由。
- **Iface** 将发送 IP 数据包的目标接口。
- **MSS** 在此路由上 TCP 连接的最大分段大小默认值。
- **Window** 在此路由上 TCP 连接的默认窗口大小。
- **irtt** 初始 RTT（往返时间）。内核使用此值来猜测最佳的 TCP 协议参数，而无需等待（可能较慢的）响应。

## 文件

- /proc/net/route
- /etc/networks
- /etc/hosts
- /etc/init.d/network

## 另请参见

ifconfig(8), netstat(8), arp(8)

## 历史

Linux 的 route 最初由 Fred N. van Kempen 编写，<waltje@walt.n1.mugnet.org>，随后由 Johannes Stille 和 Linus Torvalds 为 pl5 进行了修改。Alan Cox 为 Linux 1.1.22 添加了 mss 和 window 选项。irtt 支持并与 Bernd Eckenfels 的 netstat 合并。

## 错误

无 :)

# RPM(8)

## 名称

rpm Red Hat 软件包管理器。

## 概要

```
rpm [options]
```

## 描述

rpm 是一个强大的软件包管理器，可用于构建、安装、查询、验证、更新和卸载单个软件包。一个软件包由文件归档和软件包信息组成，包括名称、版本和描述。

有十种基本操作模式，每种模式接受不同的一组选项。它们分别是：安装、查询、验证、签名检查、卸载、构建、重建数据库、修复权限、设置所有者和组，以及显示 RC。

- 安装模式：`rpm -i [install-options] <package_file>`
- 查询模式：`rpm -q [query-options]`
- 验证模式：`rpm -V [-y] [-verify [verify-options]]`
- 签名检查模式：`rpm -checksig <package_file>`
- 卸载模式：`rpm -e <package_name>`
- 构建模式：`rpm -b [t] [O [build-options] <package_spec>`
- 重建数据库：`rpm --rebuilddb`
- 修复权限：`rpm --setperms [query-package-specifiers]`
- 设置所有者和组：`rpm --setgids [query-package-specifiers]`
- 显示 RC：`rpm --showrc`

## 通用选项

这些选项可用于所有不同的模式：

- **-vv** 打印大量丑陋的调试信息。
- **--keeptemps** 不删除临时文件（//tmp/rpm-*）。主要用于调试 rpm。
- **--quiet** 尽可能少地打印 - 通常只显示错误消息。
- **--help** 打印比正常情况更长的使用消息。
- **--version** 打印一行包含正在使用的 rpm 版本号。
- **--rcfile <file>** 使用 <file> 代替 /etc/rpmrc 和 $HOME/.pmrc。
- **--root <dir>** 使用以 <dir> 为根的系统执行所有操作。请注意，这意味着将在 <dir> 下读取或修改数据库，并且任何预或后脚本将在 chroot() 到 <dir> 后运行。
- **--dbpath <path>** 使用 <path> 中的 RPM 数据库。
- **--ftp-proxy <host>** 使用 <host> 作为 FTP 代理。参见 FTP 选项。
- **--ftp-port <port>** 使用 <port> 作为 FTP 端口。参见 FTP 选项。

## 安装和升级选项

rpm 安装命令的一般形式为

**rpm -i [install-options] <package_file>**

这将安装一个新的软件包。rpm 升级命令的一般形式为

**rpm -U [install-options] <package_file>**

这将把当前安装的软件包升级到新 RPM 中的版本。这与安装相同，只是系统中该软件包的其他所有版本都将被删除。

<package_file> 可以指定为 ftp 样式的 URL，在这种情况下，软件包将在安装前下载。有关 RPM 内置 ftp 支持的信息，参见 FTP 选项。

- **--force** 等同于同时使用 **--replacepkgs**、**--replacefiles** 和 **--oldpackage**。
- **-h, --hash** 在解包软件包归档时打印 50 个哈希标记。与 **-v** 结合使用以获得良好的显示效果。
- **--oldpackage** 允许用旧版本替换较新的软件包进行升级。
- **--percent** 当从软件包归档解包文件时，打印百分比。这是为了使 RPM 容易从其他工具中运行。
- **--replacefiles** 即使软件包替换其他已安装软件包的文件，也要安装该软件包。
- **--replacepkgs** 即使其中一些软件包已在此系统上安装，也要安装该软件包。
- **--allfiles** 无论是否存在，安装或升级软件包中所有缺失可选的文件。
- **--nodeps** 在安装或升级软件包之前不进行依赖项检查。
- `--noscripts` 不执行 preinstall 或 postinstall 脚本。
- `--notriggers` 不执行由该软件包安装触发的脚本。
- `--excludedocs` 不安装任何标记为文档的文件（包括 man 页面和 texinfo 文档）。
- `--includedocs` 安装文档文件。仅当在 rpmc 文件中指定了 *excludedocs: 1* 时才需要此选项。
- `--test` 不安装软件包，仅检查并报告潜在冲突。
- `--prefix <path>` 对于可重定位的软件包，将安装前缀设置为 `<path>`。
- `--ignoresarch` 即使二进制 RPM 和主机的架构不匹配，也允许安装或升级。
- `--ignoreos` 即使二进制 RPM 和主机的操作系统不匹配，也允许安装或升级。

## 查询选项

rpm 查询命令的一般形式为

```
rpm -q [query-options]
```

您可以指定应打印软件包信息的格式。为此，使用 `--queryformat` 选项，后跟格式字符串。

查询格式是标准 **printf(3)** 格式化的修改版。格式由静态字符串（可包含用于换行、制表符和其他特殊字符的标准 C 字符转义）和 **printf(3)** 类型的格式化程序组成。由于 rpm 已经知道要打印的类型，因此必须省略类型说明符，并用要打印的标头标签名称替换，并用 `{}` 字符包围。标签名称中的 **RPM\*** 部分可以省略。

可以通过在标签后跟随 **:type tag** 来请求替代输出格式。目前，支持以下类型：*octal*、*date*、*sheepse*、*perms*、*flags* 和 *deps.*。

例如，要仅打印所查询软件包的名称，可以使用 %{NAME} 作为格式字符串。要打印软件包的名称和

