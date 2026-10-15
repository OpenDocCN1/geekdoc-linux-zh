
如果您的计算机名为 `pine.handsonhistory.com`，您将安装服务器标识为 `pine.handsonhistory.com`，目录标识为 `pub/fedora`。

### 硬盘安装

当 DVD 的 ISO 镜像被复制到未用于 Fedora 安装的磁盘分区时，您可以使用硬盘安装。如果 ISO 镜像存在于 IDE 硬盘第一个分区的 `/tmp/fedora` 目录中，您可以将设备标识为 `/dev/sda1`，将容纳镜像的目录标识为 `/tmp/fedora`。

### 启动 VNC 安装

VNC Fedora 安装类型并不完全符合其他安装类别，但我在此添加它，因为它可能对您有用。通过 VNC 安装，您可以启动要在其上安装 Fedora 的机器上的安装过程，然后在另一台计算机（运行 VNC 服务器）上逐步通过安装屏幕。如果您希望坐在自己的办公桌前，同时在走廊另一端的计算机上安装 Fedora，这会非常方便。以下是操作步骤：

- 前往您希望查看安装过程的计算机（在我们的示例中，是 IP 地址为 `10.0.0.1` 的那台），通过从终端窗口输入以下内容来启动 VNC 客户端进程：

```bash
# vncviewer -listen
```

如果找不到 `vncviewer`，请安装 `vnc` 软件包（`yum install tigervnc`）。

- 从您想要安装 Fedora 的计算机插入安装 DVD 并重新启动计算机。应该会出现 Fedora 安装启动屏幕。

- 通过标识您希望观看安装过程的计算机屏幕来启动 VNC 安装过程。您还应该输入一个密码（至少六个字符）。例如，要使安装屏幕出现在 IP 地址为 `10.0.0.1` 的计算机上，密码为 `myF11pass`，请在高亮显示 Install 菜单时按 Tab 键。然后在出现的 `vmlinuz` 行末尾添加以下内容（密码是可选的）：

```bash
vnc vncconnect=10.0.0.1 vncpassword=myF11pass
```

- 回答前几个问题，就像从 DVD 进行常规 Fedora 安装一样：媒体检查、选择语言、键盘类型。接下来，系统会询问您是否想要配置 TCP/IP。

- 选择动态 IP 配置（如果网络上配置了 BOOTP 或 DHCP 服务器），或者为您的本地计算机输入自己的 IP 地址、子网掩码、默认网关和主要名称服务器。选择“确定”以继续。如果网络连接成功启动，您将看到类似以下消息（您的文本可能有所不同）：

```text
Starting VNC...
The VNC server is now running
Attempting to connect to vnc client on host 10.0.0.1...
Connected!
```

开始图形化安装...

- 返回您将查看安装过程的桌面。桌面上应会出现一个包含 Fedora 欢迎屏幕的 VNC 窗口。按照常规步骤继续安装。

> **注意：** 如果您无法连接到查看器，请确保桌面系统的 `5500` 端口已开放并接受连接。有关在防火墙中开放端口的更多信息，请查阅第 13 章中关于 `iptables` 的描述。

### 执行 kickstart 安装

如果您需要在多台计算机上安装 Fedora，可以通过预先配置安装过程中询问的问题的答案来省去一些麻烦。这种自动化安装过程的方法被称为 *kickstart* 安装。Kickstart 文件不仅可以用于驱动常规的 Fedora 安装，还可以用于创建 Fedora Live CD。

> **警告：** 根据您在 `ks.cfg` 文件中提供的信息，kickstart 将静默执行并安装 Fedora，期间无需人工干预。如果该文件不正确，您很容易移除主引导记录并擦除硬盘上的所有内容。请仔细检查 `ks.cfg` 文件，并在包含关键数据的计算机上使用之前，先在一台非关键的计算机上对其进行测试。

执行 kickstart 安装的一般步骤如下：

- **创建 kickstart 文件。** kickstart 文件名为 `ks.cfg`，其中包含输入给安装过程的问题答案。

- **安装 kickstart 文件。** 您必须将 `ks.cfg` 放置在软盘或 CD 上、本地硬盘上，或网络上的可访问位置。

- **启动 kickstart 安装。** 当启动安装过程时，您需要指定 `ks.cfg` 文件的位置。

在本章的示例中，您直接使用文本编辑器创建 kickstart 文件。如果您愿意，也可以使用 Kickstart 配置工具（`system-config-kickstart` 命令，来自同名软件包），这是一个用于创建 kickstart 文件的图形化工具。

### 创建 kickstart 文件

创建 kickstart 文件的良好起点是一个示例 `ks.cfg` 文件。当您安装 Fedora 时，安装过程会将一个名为 `anaconda-ks.cfg` 的文件放入 `/root` 目录。您可以使用此文件作为基础，来创建用于您的 kickstart 安装的 `ks.cfg` 文件。

您获得的特定 `/root/anaconda-ks.cfg` 文件基于您在常规安装（CD、NFS 等）期间输入的信息。可以推测，如果您正在为同一组织的其他计算机安装 Fedora，多台计算机可能拥有许多相同的硬件和配置信息。这使得该文件成为您开始创建 `ks.cfg` 文件的一个绝佳起点。

> **注意：** 有关如何使用 kickstart 的更多详细信息，请参阅 http://fedoraproject.org/wiki/Anaconda/Kickstart。若要使用更图形化的工具来配置 kickstart，请运行 `system-config-kickstart` 命令（在使用 `yum install system-config-kickstart` 命令安装同名软件包之后）。

首先，以 root 用户登录。然后制作一个 `anaconda-ks.cfg` 文件的副本以便进行编辑。

```
# cp anaconda-ks.cfg ks.cfg
```

使用任意文本编辑器编辑 `ks.cfg` 文件。请记住，必需项应按顺序排列，且每次省略某一项时，用户都会被提示提供答案。以下描述使用从 Fedora 常规 DVD 安装中创建的 `ks.cfg` 文件中的条目作为模型。您应该从自己的 `anaconda-ks.cfg` 文件开始，因此您的文件初始内容会有所不同。以井号（`#`）开头的行是被注释的行。

`ks.cfg` 文件中第一个未注释的行应指示安装是升级还是全新安装。`install` 选项执行全新安装。您也可以使用 `upgrade` 关键字来升级现有系统。（对于升级，唯一的要求是语言、安装方法、安装设备、键盘和引导加载程序。）

```
install
```

安装方法在下一行中指示。安装介质的可能位置包括：NFS（`nfs --server=servername --dir=installdir`）、FTP（`url --url ftp://user:password@server/dir`）、HTTP（`url --url http://server/dir`）或硬盘（`harddrive --dir=/dir --partition=/dev/partition`）。对于默认的 DVD 或 CD 安装，您可能会看到：

```
cdrom
```

由于 DVD 或 CD 安装是默认的，因此您可能也看不到安装方法。

必需的 `lang` 命令设置安装 Fedora 的语言（更具体地说，是国家/地区）。默认值为美式英语（`en_US.UTF-8`）：

```
lang en_US.UTF-8
```

您可以安装多种语言以在 Fedora 中支持。以下是将默认语言设置为美式英语的示例：

```
langs --default en_US.UTF-8 en_US.UTF-8
```

必需的 `keyboard` 命令默认标识美国（`us`）键盘。支持 70 多种其他键盘类型。（运行 `system-config-keyboard` 可查看可用键盘类型的列表。）

```
keyboard us
```

可选的 `xconfig` 命令可用于配置您的显示器和显卡。如果您改为使用 `skipx` 命令（如下面代码示例所示），则不会进行任何 X 配置。（系统安装完成后，运行 `system-config-display` 来设置您的 X 配置。）使用 `xconfig` 命令时，您可以根据显卡（`--xcard`）和显示器规格（`--hysync` 和 `--vysync`）来确定要使用的 X 服务器类型。还有少量其他选项可以设置色深（`--depth`，以位为单位）、屏幕分辨率（`--resolution`）、默认桌面是 GNOME 还是 KDE（`--defaultdesktop`）、登录屏幕是否为图形化（`--startxonboot`）以及显卡上的 RAM 数量（`--videoram`）。（`xconfig` 后面的所有信息实际上应该出现在一行中。）

```
skipx
```

或者
