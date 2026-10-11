
要在宿主机与 Kali Linux 虚拟机之间共享文件夹需要完成几个步骤。

从 VirtualBox 管理器选择您的 Kali Linux 虚拟机，并点击右侧的“共享文件夹”链接。这将启动一个添加文件夹的弹出窗口。在“文件夹路径”框中提供您想要共享的路径，或点击下拉箭头浏览您的宿主机。选择允许“自动挂载”和“永久”的复选框，并两次点击 OK 按钮。

![](img/a9ef2e82e60ca0e2c1f6c67b184f6420_68.png)

您的共享文件夹现在将位于 `media` 目录下。您可以创建一个书签或链接以便访问该目录。

## Kali Linux

官方 Kali Linux 文档

此 PDF 在 `docs.kali.org` 上自动生成 - 2013年8月19日

### 书签

- 首页
- 桌面
- 文件系统
- 垃圾箱

### 网络

- 浏览网络

![](img/a9ef2e82e60ca0e2c1f6c67b184f6420_69_0.png)

![](img/a9ef2e82e60ca0e2c1f6c67b184f6420_69_1.png)

![](img/a9ef2e82e60ca0e2c1f6c67b184f6420_69_2.png)

## 启动 Metasploit 框架

与 Kali Linux 网络服务一样，启动时没有运行网络服务（包括数据库服务），因此需要采取几个步骤使 Metasploit 在数据库支持下运行。

### 启动 Kali PostgreSQL 服务

Metasploit 使用 PostgreSQL 作为其数据库，因此需要先启动。

```
service postgresql start
```

您可以通过检查 `ss -ant` 的输出并确保端口 `5432` 正在监听来验证 PostgreSQL 是否运行。

```
State Recv-Q Send-Q Local Address:Port Peer Address:Port
LISTEN 0 128 * ::22 ::*:
LISTEN 0 128 *:*22 ::*:
LISTEN 0 128 127.0.0.1:5432 *:*
LISTEN 0 128 ::1:5432 :::*
```

### 启动 Kali Metasploit 服务

运行 PostgreSQL 后，接下来我们需要启动 `metasploit` 服务。服务首次启动将创建一个 `msf3` 数据库用户和一个名为 `msf3` 的数据库。服务还将根据需要启动 Metasploit RPC 和 Web 服务器。

```
service metasploit start
```

### 在 Kali 中启动 msfconsole

现在 PostgreSQL Metasploit 服务正在运行，您可以启动 `msfconsole` 并使用下所示的 `db_status` 命令验证数据库连接。

```
msfconsole
```

```
msf > db_status
[*] postgresql connected to msf3
msf >
```

### 配置 Metasploit 开机启动

如果您希望 PostgreSQL 和 Metasploit 在启动时运行，可以使用 `update-rc.d` 如下启用服务：

```
update-rc.d postgresql enable
update-rc.d metasploit enable
```

# Kali Linux 取证模式

BackTrack 为操作系统引入了“取证启动”选项，该选项一直持续到 BackTrack 5 现在存在于 Kali Linux 中。由于我们操作系统的普及，“取证启动”选项已被证明非常受欢迎。很多人手里都留着 Kali ISO，当取证需求出现时，可以快速让 Kali Linux 开始工作。Kali 预装了最流行的开源取证软件，当您需要进行开源取证工作时，Kali 是一个非常手手的工具。

![](img/a9ef2e82e60ca0e2c1f6c67b184f6420_72_0.png)

进入取证启动模式时，会发生一些非常重要的更改。

- 1. 首先，内部硬盘不会被接触。这意味着如果有分区，它将不会被使用，且不会挂载内部磁盘。为了验证这一点，我们取了一个标准系统并移除了硬盘。将其连接到商业取证软件包后，我们对硬盘进行了哈希计算。然后我们重新-

将硬盘连接到计算机并以取 取证模式启动 Kali。在运行 Kali 一段时间后，我们关闭了系统，拆下硬盘并再次获取哈希值。这些哈希值是匹配的，表明硬盘在任何时候都没有发生过任何更改。

+ 2. 另一个同样重要的更改是，我们禁用了任何可移动介质的自动挂载。因此，插入优 盘、CD 等设备将不会自动挂载。这一切背后的想法非常简单：在没有用户直接操作的情况下，任何介质都不应该发生任何变化。你作为用户所做的任何操作都由你负责。

如果你对使用 Kali 进行任何类型的真实世界取证感兴趣，我们建议不要仅仅听信我们的话。所有的取证工具都应该始终经过验证，以确保你了解它们在你可能放置它们的任何情况下如何表现。

最后，由于 Kali 专注于提供最全面的开源渗透测试工具，我们可能错过了你最喜欢的开源取证工具。如果是这样，请告诉我们！我们一直在寻找高质量的开源工具并将其添加到 Kali 中以使其变得更好。

## Kali 虚拟机中的 VMware Tools

如果你决定创建自己的 VMware 版 Kali Linux 安装，而不是使用我们的预制 VMware 镜像，你将需要按照下面的说明在你的 Kali 安装中成功安装 VMware Tools。你可以选择安装 `open-vm-tools` 或原生的 VMware tools。

### 安装 open-vm-tools

这可能是获取 Kali VMware 虚拟机获取“VMware tools”功能最简单的方法。

```
apt-get install open-vm-tools
```

### 在 Kali 中安装 VMware Tools

如果 `open-vm-tools` 对你不起，或者你更倾向于使用原生的 VMware tools，请从安装 VMware Tools 安装程序所需的某些包开始：

```
echo cups enabled >> /usr/sbin/update-rc.cd
echo vmware-tools enabled >> /usr/sbin/update-rc.cd

apt-get install gcc make linux-headers-$(uname -r)
in -s /usr/src/linux-headers-$(uname -r)/include/generated/uapi/linux/version.h /usr/src/linux-headers-$(uname -r)/include/
```

接下来，通过从相应的菜单中点击“安装 VMware Tools”来挂载 VMware Tools ISO。一旦 VMware Tools ISO 已附加到虚拟机，我们就挂载硬盘并将 VMware Tools 安装程序复制到 `/tmp/`。

```
mkdir /mnt/vmware
```

## KALI LINUX

官方 Linux 文档

此 PDF 在 `docs.kali.org` 上自动生成 - 2013年8月19日

`mount /dev/cdrom/mnt/vmware/`

`cp -rf /mnt/vmware/VMwareTools* /tmp/`

最后，切换目录到 `/tmp/`，解压 tar 包并启动安装程序：

```
cd /tmp/
tar zxpf VMwareTools-*.tar.gz
cd vmware-tools-distrib/
./vmware-tools-install.pl
```

按照 VMware Tools 安装的提示操作，完成后你就完成了。

### VMware 中鼠标移动缓慢

如果你的鼠标在 Kali Linux VMware 虚拟机中移动缓慢且迟钝，请尝试在 Kali 虚拟机中安装 `xserver-xorg-input-vmmouse` 包。

```
apt-get install xserver-xorg-input-vmmouse
reboot
```

### VMware Tools 无法编译！

这是一个困扰了我们的不幸现实，因为 Kali Linux 使用的是前沿内核，VMware 并不总是支持它。偶尔，可能需要从 [VMware 社区] 搜索“上游兼容 VMware Tools 补丁”。

### 已知问题

截至 2013年3月2日，VMware tools 将可以在内核 3.7 下进行编译，共享文件夹模块除外。已存在补丁可以修复此问题。

# 06. Kali Linux ARM 架构

在 EfikaMX 上安装 Kali ARM

![](img/a9ef2e82e60ca0e2c1f6c67b184f6420_77_0.png)

EfikaMX 是一款低端、低成本的 ARM 计算机。尽管规格并不理想，但廉廉的价格使其成为小型 Linux 系统的极极选择。

## EfikaMX 上的原生 Kali - 易用版
