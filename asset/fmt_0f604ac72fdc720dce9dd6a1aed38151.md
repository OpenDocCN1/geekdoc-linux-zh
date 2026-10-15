
## 虚拟机管理命令

`modifyvm` 命令用于更改虚拟机的设置。如果您想更改虚拟机的任何特性，可以使用它。

### 关键信息

`VBoxManager` 是除图形界面外，`VirtualBox` 的多个前端之一。它的功能不仅限于暴露某些选项，还用于虚拟机的创建和部署。

## 命令与控制

常规的 `VirtualBox` 管理程序安装还会安装 `VBoxManage` 命令，该命令设置的虚拟机设置将遵循所有虚拟机（默认情况下为 `--virtualbox`）。接下来，使用以下命令为虚拟机创建硬盘：

```bash
VBoxmanage --filename Debian --size 20480 --format vdi fixed
```

`fixed` 用于分配整个 20GB 的磁盘空间。如果您想要此选项，命令将是为：

```bash
VBoxManage create --name Debian --register
```

现在，我们通过以下命令为虚拟机添加 SATA 控制器：

```bash
VBoxManage storage --name "SATA" --controller add
```

默认情况下，它会创建一个 IDE 控制器。您可以使用 `--controller` 选项指定不同类型的控制器。控制器添加后，可以使用以下命令将虚拟磁盘挂载到控制器：

```bash
VBoxManage storageattach --name "SATA" --controller 0 --type 0 --medium debian.vdi
```

在这一步中，我们将为客户机添加带有 DVD 光驱的 IDE 控制器。首先，自定义虚拟机：

```bash
VBoxManage storagectl --name "IDE" add ide
```

然后将 ISO 镜像插入到：

```bash
VBoxManage modifyvm --name Debian --storage IDE:0 --type dvddrive --medium /path/to/iso
```

`VirtualBox` 支持 `modifyvm --name Debian`。同样：

```bash
VBoxManage modifyvm --memory 4096
```

设置其内存和视频内存。要连接网络，请使用：

```bash
VBoxManage modifyvm --nic1 --bridge eth0
```

以网桥接模式连接到宿主机上的网络。一旦一切准备就绪，您现在可以使用以下命令启动虚拟机：

```bash
VBoxManage start Debian
```

您的虚拟机现在将启动并准备就绪。一个更有实用的选项是在无头模式（headless）下启动虚拟机。CLI 提供了所有功能，包括图形界面端无法访问的功能。虚拟机的设置遵循所有虚拟机（默认为 `--virtualbox`）。

## 增强功能 (Guest Additions)

为了获得更好的性能，您需要安装一组应用程序和驱动程序。这些程序以 ISO 格式打包。一旦您在宿主机上安装了增强功能，可以使用以下方式挂载：

使用以下命令压缩磁盘空间：

```bash
VBoxManage modifydisk debian.vdi --compact
```

## 管理层

| 控制台 GUI | 命令行界面 | Web 服务 API |
| --- | --- | --- |

## Oracle VM VirtualBox API 层

| Mac OS | 实时迁移 | 资源监器 | RDP 服务器 | 其他设备 |
| --- | --- | --- | --- | --- |
| Linux | | | | 虚拟 USB 磁盘 |
| Windows | | | | 虚拟网卡 |
| Solaris OS 可移植性端口 | | | | 虚拟设备 |

![](img/1fdb1204e7e4788f3fb478a4ef813223_34_0.png)

## VirtualBox 平台支持

`VirtualBox` 支持 `Windows`、`Linux`、`Mac OS`、`Solaris`、`FreeBSD`。

## 内核模式

`controlvm`。`Debian`。`reboot`。`savestate` 在关机之前将虚拟机的当前状态保存到状态。如果虚拟机无响应，请使用 `VBoxmanage control reboot power` 命令，这等同于拔掉电源。你必须使用该命令启动它以恢复一个已关闭的虚拟机。

## 脚本启动

`VirtualBox` 最流行的用途之一是将机器虚拟化为 `Windows`，该机器需要合适的操作系统且无法在 `Windows` 上运行。`VirtualBox` 可以通过单个脚本启动客户，你可以使用启动器或快捷方式执行该脚本。

首先，手动启动 `Windows` 虚拟机，并在安装 `VirtualBox` 增强功能后切换到无头模式（Headless mode）。现在复制命令，确保它是正确的，你现在就可以构建脚本来启动虚拟机了。首先，你需要使用类似 `VBoxmanage start "Windows 10"` 的命令启动虚拟机。虚拟机已启动并运行。

> 使用 `VirtualBox` 图形界面是方便的，特别是对于觉得界面过于复杂的桌面用户来说。对于每天作为日常工作的一部分需要管理虚拟机的资深系统管理员来说，管理 `VBox` 所花费时间的回报是巨大的。虽然你可以编写自己的脚本来控制虚拟机，但更好的选项是采用 `GitHub` 上的 `VirtualBox Manager` 提供的脚本 (https://github.com/greg/vbox)。这些脚本最初是为使用 `VirtualBox API` 编写的，但如果你阅读本文并根据你的需求修改脚本，一旦你掌握了它，你就再也不需要使用图形界面来进行部署了。

`Windows` 安装中对预定义用户的身份验证。

就是这样。一旦你使用完它，就可以关闭 `Windows` 虚拟机以保存状态。只需运行 `VBoxmanage controlvm "Windows 10" 90 savestate`。你可以从 `http://bit.ly/VM-IE` 下载脚本，并根据你的需求进行调整。一旦你完善了脚本，就可以使用它通过启动器或桌面图标/快捷方式启动虚拟机。

```bash
VBoxmanage controlvm "Windows 10" run --exe "C:\Program Files\VirtualBox\InternetExplorer.exe" --username [windows-username] --password [windows-password]
```

在此命令中，我们要求 `VirtualBox` 使用启动特定应用（在本例中为 `Internet Explorer`）。

### 快速贴士

#### 键盘命令

使用应用程序作为按键来通过键盘管理客户机，例如，使用功能键通过 `VirtualBox startvm Debian9` 启动虚拟机。

`VirtualBox` 使用分层架构，带有各种内核模块，用于管理客户机的 `API`，以及一组用户程序和服务。

## 教程

### Linux 基础

#### 第一部分

#### 精通 Shell 脚本编写：

##### 开始编写脚本

`Shell` 脚本允许通过将经常执行的任务收集到单个脚本中来实现任务自动化。

![](img/1fdb1204e7e4788f3fb478a4ef813223_35_0.png)

**`John Gowers`** 是编程和计算机科学的大学导师。他喜欢在他任何能拿到的设备上安装 `Linux`，并每天使用命令和脚本。

##### 资源

- 任何 `Linux` 发行版都应该具备的标准内容

在本教程的第一部分中（参见 p38 LU&D181），我们引入了 `Linux` 中的一些基础命令行工具。终端命令是 `Shell` 脚本背后的语言。在教程中，我们将引入拼图的第二部分：编写单条命令来实现任务自动化。我们将探索命令列表；当我们执行它们时，命令将一个接一个地运行。在教程中，我们最后使用复杂的脚本来创建一个我们可能想要脚本——一个用于创建目录本地备份的脚本。脚本的意义在于，你在终端中使用的提示符和功能是称为 `shell` 的特殊类型程序的示例。`Shell` 是一个等待你的命令的程序，它会打印一个提示符，你可以在其中输入命令名称；当用户按下回车键时，`shell` 运行该命令。

`Shell` 有很多例子，你可能想自己探索其中的一些，但我们在教程中将讨论的 `shell`（以及大多数人在 `Linux` 上使用的 `shell`）是 `GNU Bourne Shell`，或 `Bash`。如果我们在终端中输入 `bash` 并按回车，起初看起来什么都没有发生。事实上，我们的 `shell` 启动了一个

目前，我们将专注于学习编写 `shell` 脚本的基础知识。我们将引入一些新的脚本命令和工具，并将一切整合在一起

![](img/1fdb1204e7e4788f3fb478a4ef813223_35_1.png)

可用的教程文件：`files.co.uk`

```bash
File Edit View Help First Package

user@linux:~$ ls -l

-rw-r--r-- 1 user user 0 Oct 27 10:00 .bashrc
```
