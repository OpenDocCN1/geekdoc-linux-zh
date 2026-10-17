
linux `/root/vmlinuz-6.1.0-204.x86_64` root=...

initrd `/root/initramfs-6.1.0-204.x86_64.img`

`vmlinuz` 代表压缩内核，`initrd` 代表包含启动所需的模块和工具的初始内存磁盘。只需在行末尾添加更多选项。

如果你在光盘上的 `/root/ks.cfg` 有引导文件，你在启动提示符添加以启动安装的信息可能如下：

```
ks=cdrom:/root/ks.cfg
```

## 用于禁用功能的启动选项

有时，Linux 安装失败是因为电脑具有某些故障或不支持的硬件。通常，你可以通过向安装程序传递选项（例如在需要驱动程序时禁用硬件）来绕过这些问题。
表 9.1 提供了一些示例。

| 安装程序选项 | 告诉系统 |
|---|---|
| `nofirewire` | 不加载对火线设备的支持 |
| `nodma` | 不加载硬盘的 DMA 支持 |
| `noide` | 不加载 IDE 设备的支持 |
| `nompath` | 不启用多路径设备支持 |
| `nopoport` | 不加载并行端口支持 |
| `npcmcia` | 不加载 PCMIA 控制器的支持 |
| `noprobe` | 不探测硬件；而是提示用户驱动程序 |
| `noscsi` | 不加载 SCSI 设备支持 |
| `nousb` | 不加载 USB 设备支持 |
| `noipv6` | 不启用 IPv6 网络支持 |
| `nonet` | 不探测网络设备 |

# 第三部分：成为 Linux 系统管理员

## 视频问题的启动选项

如果你在视频显示遇到问题，可以按照表 9.2 所示指定视频设置。

### 表 9.2 视频问题的启动选项

| 启动选项 | 告知系统 |
| --- | --- |
| `xdriver=vesa` | 使用标准的 vesa 视频驱动 |
| `resolution=1024x768` | 选择要使用的精确分辨率 |
| `nofb` | 不使用 VGA 16 帧缓冲区驱动 |
| `skipddc` | 不探测显示器的 DDC（探测可能会导致安装程序挂起） |
| `graphical` | 强制进行图形化安装 |

## 特殊安装类型的启动选项

默认情况下，当你坐在控制台回答问题时，安装将以图形化模式运行。如果你有一个纯文本控制台，或者 GUI 工作不正常，你可以以纯文本模式运行安装：通过输入 `text`，你会让安装以文本模式运行。

如果你想在某台计算机上启动安装，但想在另一台计算机上回答安装问题，可以启用 VNC（虚拟网络计算）安装。完成此类类型的安装后，你可以去另一个系统并打开 vnc 查看器，为查看器提供安装机器地址（例如 `192.168.0.99`）。表 9.3 提供了必要的命令以及系统指令。

### 表 9.3 VNC 安装的启动选项

| 启动选项 | 告知系统 |
| --- | --- |
| `vnc` | 作为 VNC 服务器运行安装 |
| `vncconnect=hostname[:port]` | 连接到 VNC 客户端主机名和可选端口 |
| `vncpassword=password` | 客户端使用密码（至少八位）连接到安装程序 |

## kickstart 和远程仓库的启动选项

你可以从仅包含内核和初始 RAM 磁盘的介质上启动安装过程。如果是这种情况，你需要识别存在软件软件包的仓库。你可以通过提供 kickstart 文件或以某种方式识别仓库的位置来实现。为了让安装程序提示输入仓库位置（CD/DVD、硬盘、NFS、FTP 或 HTTP），请在安装启动选项中添加 `askmethod`。

## 第 9 章：安装 Linux

使用 `repo=options`，你可以识别仓库位置。以下示例显示了创建 `repo=` 条目时使用的语法：

```
repo=hd://dev/sda:/myrepo
位于磁盘 1 第一分区的 /myrepo 仓库

repo=http://abc.example.com/myrepo
从 Web 服务器上的 /myrepo 可用的仓库

repo=ftp://ftp.example.com/myrepo
从 FTP 服务器上的 /myrepo 可用的仓库

repo=cdrom
从本地 CD 或 DVD 可用的仓库

repo=nfs://mynys.example.com:/myrepo/
从 NFS 服务器上的 /myrepo 可用的仓库

repo-nfsiso:nfs.example.com:/mydir/rhel10.iso
从 NFS 服务器可用的安装镜像
```

与其识别仓库，你可以在 kickstart 文件中指定它。以下是识别 kickstart 文件位置的某些方法：

```
ks=cdrom://stuff/ks.cfg
从 CD/DVD 获取 kickstart。

ks=hd=sda2:/test/ks.cfg
从硬盘 (sda2) 上的目录获取 kickstart。

ks=http://example.com/ksfiles/ks.cfg
从 Web 服务器获取 kickstart。

ks=ftp://ftp.example.com/allks/ks.cfg
从 FTP 服务器获取 kickstart。

ks=nfs://mynys.example.com:/somks/ks.cfg
从 NFS 服务器获取 kickstart。
```
