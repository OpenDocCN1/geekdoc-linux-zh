
# 第一部分：入门

## 硬盘安装

将 DVD 的 ISO 镜像复制到未用于 CentOS 安装的磁盘分区后，您可以使用硬盘安装。如果 ISO 镜像位于您的 IDE 硬盘第一个分区的 `/tmp/rh` 目录中，您可以将设备标识为 `/dev/sda1`，并将包含镜像的目录标识为 `/tmp/rh`。

## 启动 VNC 安装

VNC CentOS 安装类型并不完全符合其他安装类别，但我在此添加它是因为您可能会发现它有用。通过 VNC 安装，您可以在要安装 CentOS 的机器上启动安装过程，然后在另一台计算机（运行 VNC 服务器）上逐步完成安装屏幕。如果您希望在安装 CentOS 在走廊另一头计算机时坐在自己的办公桌前，这会非常方便。以下是操作步骤：

- 前往您想要查看安装过程的计算机（在本例中，IP 地址为 10.0.0.1 的计算机），并通过在终端窗口中输入以下内容来启动 VNC 客户端进程：
  ```
  vncviewer -listen
  ```
  如果找不到 vncviewer，请安装 vnc 包（`yum install vnc`）。

- 在你要安装 CentOS 的计算机上，插入安装 DVD 并重启计算机。应该会出现 CentOS 安装启动屏幕。

- 通过识别你想观看安装过程的计算机屏幕来启动 VNC 安装过程。你还应输入一个*密码*（至少六个字符）。例如，要在 IP 地址为 10.0.0.1 的计算机上显示安装屏幕，密码为 *myF10pass*，请在启动行中指定以下内容（*password* 是可选的）：
  ```
  vnc vncconnect=10.0.0.1 vncpassword=myF10pass
  ```

- 就像通过 DVD 进行常规 CentOS 安装一样回答前几个问题：*媒体检查*、*选择语言*和*键盘类型*。接下来，你会被询问是否要配置 *TCP/IP*。

- 选择*动态 IP 配置*（如果你的网络配置了 BOOTP 或 DHCP 服务器）或*输入你自己的 IP 地址*、*网络掩码*、*默认网关*以及*本地计算机的主要名称服务器*。选择“确定”继续。如果网络连接成功启动，你会看到类似以下消息（你的文本可能有所不同）：
  ```
  Starting VNC...
  The VNC server is now running
  Attempting to connect to vnc client on host 10.0.0.1...
  Connected!
  Starting graphical installation...
  ```

- 返回到你将观看安装过程的桌面。桌面上应该会显示一个包含 CentOS 欢迎屏幕的 VNC 窗口。按照常规继续安装。

> **注意**
> 如果你无法连接到 vncviewer，请确保桌面系统上的端口 5500 是开放的并且正在接受连接。查看第 13 章中关于 iptables 的描述，以获取有关在防火墙中打开端口的更多信息。

## 执行 Kickstart 安装

如果你正在多台计算机上安装 CentOS，你可以通过预配置安装过程中提出的问题的答案来省去一些麻烦。这种自动化安装过程的方法被称为*kickstart* 安装。

> **警告**
> 根据你在 ks.cfg 文件中提供的信息，kickstart 将在不干预的情况下静默安装 CentOS。如果此文件不正确，你可能会意外删除主引导记录并擦除硬盘上的所有内容。仔细检查 ks.cfg 文件，并在尝试在持有关键数据的计算机上之前，先在一台非关键计算机上测试。

执行 kickstart 安装的一般步骤如下：

- **创建 Kickstart 文件** — kickstart 文件，名为 *ks.cfg*，包含提供给安装过程的问题响应。
- **安装 kickstart 文件** — 你必须将 *ks.cfg* 放在软盘或 CD 上、本地硬盘上，或网络上的可访问位置。
- **启动 Kickstart 安装** — 当你启动安装过程时，你需要识别 *ks.cfg* 文件的位置。

在本章的示例中，你直接使用文本编辑器创建你的 kickstart 文件。如果你愿意，可以使用 Kickstart 配置器（来自同名包的 *system-config-kickstart* 命令），这是一个用于创建 kickstart 文件的图形化工具。

## 创建 Kickstart 文件

开始创建你的 kickstart 文件的一个好方法是从一个示例 *ks.cfg* 文件开始。当你安装 CentOS 时，安装过程会将一个名为 *anaconda-ks.cfg* 的文件放到 `/root` 目录中。你可以使用此文件作为你用于 kickstart 安装的 *ks.cfg* 文件的基础。

你获得的特定 `/root/anaconda-ks.cfg` 文件基于你在常规安装（CD、NFS 等）期间输入的信息。假设，如果你在为同一组织的其他计算机安装 CentOS，多台计算机可能具有许多相同的硬件和配置信息。这使得这个文件成为你开始创建你的 *ks.cfg* 文件的绝佳基础。

> **注意**
> 有关如何使用 kickstart 的更多详情，请参阅 Red Hat Linux 配置指南。你可以从任何 Red Hat 镜像站点获取此指南。要使用更图形化的工具来配置 kickstart，请在通过 `yum install system-config-kickstart` 命令安装同名包后运行 system-config-kickstart 命令。

首先，以 root 用户登录。然后制作一份 anaconda-ks.cfg 文件的副本以进行操作：

```
# cp anaconda-ks.cfg ks.cfg
```

使用任何文本编辑器编辑 ks.cfg 文件。请记住，必需项应按顺序排列，并且任何时候你省略一个项目，用户都会被提示提供答案。以下描述以从 CentOS 常规 DVD 安装创建的 ks.cfg 文件中的条目为模型。你应该从你自己的 anaconda-ks.cfg 文件开始，因此，你的文件开头会略有不同。注释行以井号（#）开头。

ks.cfg 文件中的第一个未注释行应表明安装是升级还是安装。install 选项运行新安装。你也可以使用 upgrade 关键字来升级现有系统。（对于升级，唯一的要求是语言、安装方法、安装设备、键盘和引导加载程序。）

```
install
```

安装方法在下一行指示。安装介质可能的位置包括：NFS（`nfs --server=servername --dir=installdir`）、FTP（`url --url ftp://user:password@server/dir`）、HTTP（`url --url http://server/dir`）或硬盘（`harddrive --dir=dir --partition=/dev/partition`）。对于默认的 DVD 安装，你会看到：

```
cdrom
```

必需的 lang 命令设置安装 CentOS 的语言（更具体地说，也是国家）。默认值为美国英语（en_US.UTF-8）：

```
lang en_US.UTF-8
```

你可以安装多种语言以在 CentOS 中支持。以下是默认设置为美国英语的示例：

```
langsupport default en_US.UTF-8
```

必需的 keyboard 命令默认标识美国（us）键盘。支持其他 70 多种键盘类型。（运行 system-config-keyboard 以查看可用键盘类型的列表。）

```
keyboard us
```

可选的 xconfig 命令可用于配置你的显示器和视频卡。如果你使用 skipx 命令代替（如下面代码示例所示），则不会进行 X 配置。系统安装后，运行 xconfig 来设置你的 X 配置。当你使用 xconfig 命令时，可以根据你的视频卡（--card）和显示器规格（--hsync 和 --vtsync）来识别要使用的 X 服务器类型。少量其他选项允许你设置位色深（--depth）、屏幕分辨率（--resolution）、默认桌面是 GNOME 还是 KDE（--defaultdesktop）、登录屏幕是否图形化（--startxonboot），以及你的视频卡上的内存量（--videoram）。（xconfig 之后的所有信息实际上应出现在同一行上。）

```
skipx
```

或者

```
xconfig --card="NVIDIA GeForce FX (generic)" --videoram=131072 --hsync=31.5-37.9 --vtsync=50-70 --resolution=800x600 --depth=16 --startxonboot --defaultdesktop gnome
```

可选的 network 命令允许你配置你的 CentOS 系统对网络的接口。示例告诉你的计算机从 DHCP 服务器获取其 IP 地址和相关网络信息（--bootproto dhcp）。如果你想分配特定的 IP 地址，使用 --bootproto static 选项。然后将 IP 地址（--ip）、网络掩码（--netmask）、网关的 IP 地址（--gateway）和 DNS 服务器的 IP 地址（--nameserver）更改以适合你的系统。你还可以添加主机名（--hostname）。

> **注意**
> 虽然网络值似乎在三行上，但所有值必须在同一行上。

```
network --device eth0 --bootproto dhcp
```

或者

```
network --device=eth0 --bootproto static --ip=192.168.0.1 --netmask 255.255.255.0 --gateway 192.168.0.1 --nameserver 192.168.0.254 --hostname duck.example.com
```

rootpw 命令将密码设置为跟随的任何单词（在以下示例中，pAssWord）。让此密码存在是一个安全风险，因此你应在安装 Linux 后更改此密码（使用 passwd 命令）。你还有选择添加加密密码的选项（`--iscrypted`）。

```
rootpw pAssWord
```

或者

```
rootpw --iscrypted g_UJ.RQe0V3Bg --enablemd5
```

firewall 命令允许你设置你的 CentOS 系统使用的默认防火墙。默认值是启用（如果防火墙已开启）。你也可以将防火墙设置为禁用（无防火墙）。（这些值在本章前面安装过程中已描述。）
