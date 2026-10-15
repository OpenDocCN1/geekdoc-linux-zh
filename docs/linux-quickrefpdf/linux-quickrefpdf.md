
# Linux 快速启动指南

## /etc/NETWORKING

(Slackware)

`HOSTNAME=hostname.domain.com`

Jialong He
jialong_he@bigfoot.com
http://www.bigfoot.com/

启动项和名称从这些文件中读取。可以手动更改。

# NFS 文件共享

# 用户管理

## 文件

- `/etc/group`
- `/etc/passwd`
- `/etc/shadow`
- `/etc/bashrc`
- `/etc/profile`

用户账户信息。

- `/etc/fstab`
- `/etc/exports`
- `/etc/auto.master`

启动期间挂载的文件系统。NFS 服务器导出列表。auto 主文件。

- `/etc/ssh_config`
- `/etc/login`
- `$HOME/.bashprofile`
- `$HOME/.bashrc`

bash 系统级和用户初始化文件。

### 命令

- `/etc/resolv.conf`

指定服务器 DNS、DNS 域

`search 192.168.1.200`

- `/etc/hosts`

主机名到 IP 地址的映射。

- `/etc/hostname`

查找顺序。

`order hosts, bind`

`multion on`

- `/etc/netswitch.conf`
- `/etc/networks`
- `/etc/protocols`
- `/etc/interfaces`

指定信息的新方式。

- `/etc/rpc`

TCP/IP 服务和端口映射。

RPC 服务映射到程序号。

### 命令

- `mount`
- `exports`
- `showmount -e hostname`

挂载文件系统或 `fstab` 中的所有条目。显示 `exports` 中的导出系统列表。显示已导出的系统。

# 打印机配置

- `netconfig`
- `ppsetup`

菜单驱动的以太网设置程序。设置 PPP 连接 (Slackware)。例如设置启动设置。

## 文件

- `/etc/printcup`
- `/etc/printcap.local`
- `/etc/lpd.conf`
- `/etc/lpds.conf`

打印机功能数据库。LPR 配置。LPR 行打印机池进程的权限控制。

- `/etc/hosts.lpd`
- `/etc/hosts.quiv`

访问控制 (BSD LPD)。受信任主机。打印机的环境变量。

### 命令

- `useradd`, `usermod`
- `usermod`
- `newusers`
- `groupadd`, `groupdel`
- `chage`, `fix`, `chsh`

创建新用户账户的脚本 (slackware) 或链接到用户理想 (Redhat)。删除、创建、修改新用户或更新默认新用户。更新并创建新用户（批量模式）。添加或修改组。

## PRN

- `ifconfig`
- `ppsetup`

```bash
$ifconfig $1 $IPADDR $BROADCAST $($BROADCAST netmask $NETWORK $ETHMASK) out
```

并行端口。

- `host`
- `domainname`
- `arping`
- `ipchains`
- `iptables`

查找主机名 IP（或类似的查找）。DNS 名称查找。先通过以太网地址通过 `arp` 查找。防火墙和 NAT (Redhat 的 `etc/sysconfig/network`) 防火墙和 NAT (Linux 的 `etc/sysconfig/iptables`)。

## 文件

- `sendmail.conf`
- `sendmail.mc`

"`sendmail.conf`" 是配置文件。"`sendmail.mc`" 是一个宏文件，可以通过以下方式通过 `mkmff > sendmail.conf` 生成 "`sendmail.conf`"。

- `aliases`

邮件列表，在任何更改后运行。在文件中包含头部列表。邮件访问控制，`FEATURE(access)`，应在 `sendmail.conf` 中设置。在 `/etc/mail` 访问 `cyberpro.com relay domain.com relay DISCARD`。

- `access`

生成哈希 `/etc/mail access / <etc/mail access all 通过条目组成所有主机和子域名`。

# 网络配置

- `/etc/rc.d/1` (Slackware)
- `/etc/sysconfig/network-scripts/ifcfg-eth0` (Redhat)
- `/hostname`

IP 地址、网络掩码。默认网关在这些文件中。可以手动编辑以修改网络参数。`hostname` 由 `hostname` 设置。

## 配置文件 /etc/sysconfig

- `keyboard`

`keyboard_map`, eg.

`KEYBOARD="/usr/lib/keysmaps.map"`

鼠标类型，例。

`MOUSEYPE=`

- `network`

网络设置，包含 `NETWORKING=`

### 命令

重建邮件别名数据库。

- `newaliases`

创建新的别名数据库，例如。

- `makemap`

构建访问数据库哈希值。

### 有用配置文件

- `httpd`

Apache Web 服务器配置。

- `smb`

Samba 服务器文件 (for print)。

- `lilo`

LILO 引导加载器配置。

- `syslog`

系统守护进程 (`syslog`) 配置。

- `ssh_config`

SSH 客户端和服务器配置。

- `ldconfig.conf`

默认路径 (`ldconfig`)。

- `tools.conf`

工具配置 (`access`)。

- `named.conf`

DNS 服务器名称 (Redhat)。

- `sysctl.conf`

通过 `sysctl` 设置内核参数。

- `ntp.conf`

时间服务器。

- `arada.conf`

Internet 服务器。

- `/etc/resolv.conf`

扩展索引配置。

- `postfix.conf`

`postfix` 服务器。

- `protpd.conf`

网络备份服务器。

- `mime.conf`

邮件服务器配置。

# 配置内核

- `makeconfig`

使用菜单配置内核，或 X Window 接口。

- `makedep`

构建并安装内核。

## 管理模块

`insmod`, `lmmod`, `modprobe`, `rmmod`, `depmod`

可加载模块。

## 杂文件

- `/etc/shells`

允许登录的 shell

- `/etc/ftpsusers`

用于 ftp 的用户名。

- `/etc/htost.allow`

TCP wrapper 配置。

- `/etc/host.deny`

包含系统配置。

- `/etc/sysconfig` (redhat)

软驱驱动。

- `/dev/loop`

系统运行级。

- `/etc/init.d`

转换文件到 linux 格式。

- `toml.conf` (Slackware)

`zux`, `unit`。

- `unit.conf` (Redhat)

权限和组文件。

- `pwck`
- `grpcnv`

转换 shadow 和组。

- `shadowconf`
- `quota`
- `quotacheck`

配额

- `quotas`
- `quotaf`

请求配额

- `lilo - D`

设置 LILO OS (默认在 `lilo.conf` 中)

- `crontab`

显示或编辑 cron 任务。

- `sys-unconfig`

未配置系统

- `chfkroot-list`

在运行级启动的服务。探测新硬件 (Redhat)。

- `rpm`

```bash
rpm -i package
rpm -U package
rpm -q package
rpm -U package
```

## 配置 Apache 2.0 带 SSL

- `mod_ssl`

当 apache 时，指定 `--enable-ssl` 配置。默认情况下，ssl 未启用。编译后，使用 "mod-ssl" 位于模块列表中，“mod-ssl" 应在头部中。

(2) 生成私钥

(3) 生成证书

(4) 生成自签名证书

```bash
openssl -x509 -days 365 -newkey server.key -out server.key -out server.crt
```

(5) "mod_ssl", 将包含在 `httpd.conf` 中。否则包含 `<IfModule SSL>`。

## Syslog

每行由一个选择器和一个动作组成。部分包含部分：优先级和设施，用括号 () 分隔。你可以使用等号 (=`) 定义优先级以指定此优先级或其他。如果两者有效，工具将通过感叹号 (!) 包括此优先级以外的任何更高优先级。

示例：

```
* *emerg /var/log/log 到文件
* #myhost.domain.com # 日到远程主机
```

- `facilities`



- `priorities`

- `action`

## 编译模块

- `make modules`

- `make modules_install`

构建并安装模块。

## IPtables (Netfilter)

## X Window (XFree86)

# 命令语法

其他命令：

文件

要设置分辨率，在 `"Screen"` 部分和 `"Section Display"` 中指定模式。例如：模式 `"1024x768"`

```
iptables [-command] <chain> <parameters>
(1) --name -d (2) -delete -D (4) -erase -Z
(5) check -C (6) delete -X (7) rename -E
```

保存和恢复

`/sbin/iptables-save /etc/sysconfig/iptables`

`/sbin/iptables-restore /etc/sysconfig/iptables`

要指定刷新率，在 `"Monitor"` 部分指定一个速率。例如：`Verfresh 70-120`

防火墙脚本示例

`http://linux.example.com/iptables_examples.html`

X 启动后运行的客户端

## 参数

按协议；通过数字或使用名称, `dp`, `icmp`

```
X11/xinit/rc
X11/xinit/rc
```

### 构建表格

| 参数 | 说明 |
| :--- | :--- |
| `--protocol` | 匹配协议 |
| `--source` | 匹配源地址 |
| `--destination` | 匹配目标地址 |
| `--fragment` | 匹配分片 |
| `--port` | 匹配源端口 |
| `--port` | 匹配目标端口 |

### 命令

此表允许创建规则。在链中：

1. `INPUT` - 此链允许通过网络接口接收的数据包。

2. `OUTPUT` - 此链允许本地数据包在通过网络接口路由之前通过。

3. `FORWARD` - 此链允许从一个接口接收并发送到另一个接口的数据包。

此文件使用配置文件 `X86Config` 或 `"x86cfg"` 目录进行设置。`X86Config` 文件由若干节（sections）组成，这些节可以以任何顺序出现。每个节遵循以下格式

`Option "OffTime" "time"`

设置 DPMS 模式下“关闭”阶段的闲闲超时时间，默认 40 分钟。

`Section "InputDevice"`

`Identifier "Generic Keyboard"`

`Driver Keyboard`

`Option "AutoRepeat" "30"`

`Section "SectionName"`

图形在 `Device` 节中描述，`Mouse` 由 `InputDevice` 节报告。`Keyboard` 和 `Pointer` 均在 `ServerLayout` 节中注册。

`Option "DefaultLayout" "layout-id"`

设置用于服务的默认 `ServerLayout`。默认是第一个 `ServerLayout` 节。

`Section "ServerFlags"`

`Option "BlankTime" "99"`

`Option "StandbyTime" "99"`

`Option "SuspendedTime" "99"`

`Option "OffTime" "99"`

`Section "InputDevice"`

`Identifier "PS2 Mouse"`

`Driver mouse`

`Option "CorePointer" "true"`

`Option "Device" "dev/mouse"`

`Option "Protocol" "PS2"`

`Option "EmulateButtons" "true"`

`Section "Module"`

`Load "module"`。模块名称应为模块名，而不是文件名。

`Section "Module" "extmod"`

`Load "type"`

`Section "File"`

`Option "Path" "path"`

字体元素可以是绝对路径，也可以是字体服务器标识符。

`Option "GBPath" "path"`

用于为 X11 服务器设置存储已加载模块的多个目录。

`Section "Files"`

`Path "/usr/X11/rgb"`

`FontPath "/etc/type"`

`Section "ServerLayout"`

`Option "DontZoom" "boolean"`

禁用 `Ctrl+Alt+Keypad` 终止 X 服务器。

启用 `"Ctrl+Alt+Keypad"` 切换视频模式。

`Option "BlankTime" "time"`

设置屏幕屏保护程序空闲阶段的闲闲超时时间，单位为分钟。默认 10。

`Option "StandbyTime" "time"`

设置 DPMS 模式下“待机”阶段的闲闲超时时间，单位为分钟。默认 20。

`Option "SuspendedTime" "time"`

设置 DPMS 模式下“挂起”阶段的闲闲超时时间，默认 30。

`Section "InputDevice"`

至少有两个 `InputDevice` 节，分别用于 `Keyboard` 和 `Mouse`。

`Identifier`

为此输入设备指定唯一名称。

`Driver`

指定用于输入设备的驱动程序名称。

`Option "CorePointer"`

`Option "CoreKeyboard"`

此输入设备是主驱动设备。

`Section "Device"`

关于系统使用的显卡的规格。你必须在配置文件中至少包含一个 `Device` 节。这些设备在 `ServerLayout` 节中使用。

`Identifier`

为显卡指定唯一名称。

`Driver`

指定用于显卡的驱动程序名称。

示例：

`Section "Device"`

`Identifier "ATI MACH64"`

`VendorName "ATI MACH64"`

`VideoRam 2048`

`EndSection`

`Section "Monitor"`

`Monitor` 节描述显示器。必须至少有一个显示器，激活的显示器将在 `ServerLayout` 节中使用。

`Identifier`

为此显示器指定唯一名称。

`HorizSync "horiz-sync"`

设置此显示器水平同步频率的范围（单位为 kHz）。

`VertRefresh "vert-refresh"`

设置此显示器垂直同步频率的范围（单位为 kHz）。

示例：

`Section "Monitor"`

`Identifier "Generic Monitor"`

`VendorName "Monitor Vendor"`

`ModelName "Monitor Model"`

`HorizSync "31.5-56.6"`

`VertRefresh "40-70"`

`EndSection`

`Section "Screen"`

`Screen` 节绑定了 `Device` 和 `Monitor` 节。必须至少有一个 `Screen` 节。激活的节位于 `ServerLayout` 节中。

`Identifier`

为此节指定唯一名称。

`Device "device-id"`

指定用于此屏幕的 `Device ID`。

`Monitor "monitor-id"`

指定用于此节的 `Monitor ID`。

`Default "depth"`

默认颜色深度，8、16 或 24。

`Option "acc"`

XAA（X 加速相关性），默认开启。

`DISPLAY` 节

每个节必须至少有一个匹配 `DefaultDepth` 值的 `Display` 节。

`Depth - depth`

此项指定此 `Display` 节的颜色深度。

`Virtual - yim`

指定使用的虚拟分辨率。

`Viewport - x0 y0`

设置初始显示的左上角。

`Mode "mode-name..."`

指定要使用的视频模式列表。指定的每个 `mode-name` 必须加双引号。它们必须对应相应 `Monitor` 节中指定的模式（包括隐引的标准模式），可以通过 `Ctrl+Alt+KeypadPlus` 或 `Ctrl+Alt+KeypadMinus` 进行切换。

示例：

`Section "My Screen"`

`Device "ATI Mach64"`

`Monitor "Generic Monitor"`

`DefaultDepth 16`

`Subsection "Display"`

`Depth 16`

`Modes "1024x768" "800x600" "640x480"`

`EndSubsection "Display"`

`Depth 24`

`Modes "1024x768" "800x600" "640x480"`

`EndSection`

`Section "ServerLayout"`



`ServerLayout`绑定一个`Screen`节和多个`Input`节以形成完整的配置。激活的`ServerLayout`节在`ServerLayers`中指定。如果没有，则激活第一个`ServerLayout`节。如果存在`ServerLayout`节，将根据相关节选择单个屏幕和两个激活（核心）输入设备。

### Identifier

为此`ServerLayout`节指定唯一名称。

### Screen

`screen-name "screen-id"`

`field-id`是强制性的，并引用所引用的`Screen`节。

### InputDevice

`"devaid" option...`

通常至少需要两个，一个核心指针，另一个用于主键盘设备。

示例：

```
Section "ServerLayout"

Identifier "Default Layout"

Screen "My Screen"

InputDevice "Generic Keyboard"

InputDevice "PS/2 Mouse"

EndSection
```
