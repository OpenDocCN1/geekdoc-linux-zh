
### 4. 像正常从 DVD 或 CD 安装 Fedora Core 一样回答前几个问题
介质检查、选择语言和键盘类型。接下来，系统会询问您是否要配置 TCP/IP。

### 5. 配置网络
选择动态 IP 配置（如果您在网络上配置了 BOOTP 或 DHCP 服务器）或输入本地计算机的 IP 地址、子网掩码、默认网关和主 DNS。选择 `OK` 继续。如果网络连接启动成功，您将看到如下消息：

```
Starting VNC...
The VNC server is now running
Attempting to connect to vnc client on host 10.0.0.1...
Connected:
Starting graphical installation...
```

### 6. 查看安装过程
回到要查看安装过程的桌面。桌面上应该出现一个 VNC 窗口，包含 Fedora Core 欢迎界面。按照正常程序继续安装。

> 注意：如果无法连接到 `vnc`，请确保桌面系统的防火墙端口是打开的。关于防火墙的详细信息请参阅第 14 章。

## 执行 kickstart 安装

通过预配置安装过程中提出的答案，在安装 Fedora 或 RHEL 时可以节省时间。自动化安装过程的方法被称为 kickstart 安装。

执行 kickstart 安装的一般步骤如下：

1. 创建 `kickstart` 文件。`kickstart` 文件名为 `ks.cfg`，包含了馈给安装过程的回答。

在本章中，通过文本编辑器创建 `kickstart` 文件。如果您更喜欢，可以使用 Kickstart 配置器（`system-configstart` 命令），它是创建 `kickstart` 文件的图形化工具。

### 创建 kickstart 文件

创建 `kickstart` 文件的良好方法是使用示例 `.cfg` 文件。当您安装 Fedora Core 或 RHEL 时，安装过程会在 `/root` 目录下创建一个名为 `anaconda-kscfg` 的文件。可以使用此文件作为您的 `.cfg` 文件基础。

要配置 `kickstart`，运行 `system-configstart`。以 `root` 用户身份登录。然后复制 `anaconda-kscfg` 进行操作。

```bash
### cp anaconda-kscfg ks.cfg
```

使用任何文本编辑器编辑 `ks.cfg` 文件。记住，项目应按顺序排列，任何您遗漏的，用户都会提示回答。来自从普通 DVD 创建的条目，注释行以井号 (`#`) 开头。

`ks.cfg` 文件的第一行应指示安装是升级还是安装。`install` 选项运行新安装。您可以使用 `upgrade` 关键字来升级现有系统。（对于升级，唯一的要求是语言、安装方法、安装设备、键盘和引导加载程序）。

```bash
install
```

安装方法在下一行指示。可能的安装位置包括：`NFS` (`nfs --server=servername --dir=instaldir`)、`FTP` (`url --url ftp://user:passwd@server/dir`)、`HTTP` (`url --http://server/dir`) 或硬盘 (`harddrive --dir=/partition=/dev/partition`)。对于默认 DVD 或 CD 安装，您将看到：

```
cdrom
```

所需的 `lang` 设置安装 Fedora 的语言（以及国家）。默认值为美国英语 (`en_US.UTF-8`)。

```bash
lang en_US.UTF-8
```

您可以在 Fedora 中安装支持多种语言。这里有一个默认设置为美国英语的示例：

```bash
langsupport -default en_US.UTF-8 en_US.UTF-8
```

[文本继续...]

## 第 2 章：安装 Fedora 55

所需的 `keyboard` 命令默认识别美国 (`us`) 键盘。系统还支持超过 70 种其他键盘类型。（运行 `system-config-keyboard` 可查看可用键盘类型列表。）

```
keyboard
```

可选的 `xconfig` 命令可用于配置您的显示器和显卡。如果你改用 `skippx` 命令（如下面的代码所示），则不会进行任何 X 配置。（在系统安装完成后，运行 `system-config-desktop` 来设置您的 X 配置。）当您使用 `xconfig` 命令时，可以根据显卡（`--card`）和显示器规格（`--hync --vsync`）来识别要使用的 X 服务器类型。其他一些选项允许您设置位深位数（`--depth`）、屏幕分辨率（`--resolution`）、默认桌面是 GNOME 还是 KDE（`--defaultdesktop`）、登录界面是否为图形界面（`--startxboot`）以及显存大小（`--videoram`）。（`xconfig` 之后的所有信息实际上应该显示在同一行。）

```
skippx
xconfig --card=NVIDIA GeForce FX (generic) --videoram=131072
--hync=31.5-37.9 --vsync=50-70 --resolution=600x600
--depth=16 --startxboot --defaultdesktop gnome
```

`network` 命令允许您配置 Fedora 或 RHEL 系统的网络接口。示例告诉您从 DHCP 服务器获取其 IP 地址和相关的网络信息（`--bootproto dhcp`）。如果你想分配特定的 IP 地址：

> 注意：尽管网络值显示在三行，但所有值必须在同一行上。

```
network --device eth0 --bootproto dhcp
network --device=eth0 --bootproto static --ip=192.168.0.1
--netmask 255.255.255.0 --gateway 192.168.0.1
--nameserver 192.168.0.254 --hostname duck.example.com
```

`rootpw` 命令将密码设置为其随后的任何单词（在以下示例中为 `paSSword`）。留下此密码存在安全风险，因此您应该在 Linux 安装后更改此密码（使用 `passwd` 命令）。您还可以选择添加加密密码来代替（`--iscrypt u.UJ.RQeOV3BBg --enablemd5`）。

```
rootpw paSSword
rootpw --iscrypt u.UJ.RQeOV3BBg --enablemd5
```

### 第一部分：在 Fedora 和 RHEL 中入门

`firewall` 命令允许您设置 Fedora 或 RHEL 系统使用的默认防火墙。默认值为启用（如果防火墙已开启）。您也可以将防火墙设置为禁用（无无防火墙）。这些值在在本章前面的安装步骤中已有所描述。如示例所示，您可以选择性地指定对特定接口（`--eth0`）没有来自主机的限制。您还可以添加单个服务（`--ssh`）或特定的端口:协议对（`--port 1234:udp`）。

```
firewall --enabled --trust=eth0 --ssh --port=1234:udp
```

`selinux` 命令指示是否启用了安全增强型 Linux（Security Enhanced Linux）。下一行显示启用并强制执行：

```
selinux --enforcing
```

所需的 `authconfig` 命令设置用于保护用户密码的身份验证类型。`--enableshadow` 选项启用使用 `/etc/shadow` 文件存储您的密码。`--enablemd5` 允许使用长达 256 个字符的密码。（您通常会同时使用两者。）

```
authconfig --enableshadow --enablemd5
```

`timezone` 命令为您的 Linux 系统设置时区。此处显示的默认值是美国，纽约（`America/New_York`）。`--utc` 选项表示计算机的硬件时钟设置为 UTC 时间。如果您不设置时区，将使用 `US/Eastern`。运行 `timedate` 命令可以查看其他有效时区。

```
timezone --utc America/New_York
```

`bootloader` 命令设置引导加载程序（默认为 GRUB）的位置。例如，`--location=mbr` 将 GRUB 添加到主引导记录（MBR）中。（使用 `--location=none` 来添加 GRUB）。`driveorder` 描述了首先在哪个硬盘上查找主引导记录。您还可以通过使用 `append` 选项（`--append hide-scsi`）在启动时读取内核选项，或使用 GRUB 的可选参数（`--password=GRUBpassword`）。

```
bootloader --location=mbr --driveorder=hda --append="rhgb quiet"
password=GRUBpassword
```
