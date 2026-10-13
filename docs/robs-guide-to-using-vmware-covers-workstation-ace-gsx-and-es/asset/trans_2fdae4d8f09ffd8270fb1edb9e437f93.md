
从 Linux 安装介质（CD-ROM、DVD 或 ISO）启动时，您必须选择要安装的组件并分区和格式化硬盘。让安装程序完成其工作，包括任何重启，直到完成为止。建议以桥接模式运行虚拟机，以便在安装期间（如果您的发行版支持此功能）可以下载可用的补丁和更新。

Tip: 如果在安装过程中出现图形问题，请查看第 13.2 节中的提示，以解决 Linux 安装问题。

安装完成后，将 VMware Tools 安装到您的 Linux 来宾操作系统中。完成后，您就完成了，现在您拥有一个完全功能正常的 Linux 系统。

Tip: 在输入 Linux 用户等配置时，复制文件后立即（如果您的发行版顺序如此）拍摄快照。这样您就可以返回到一切正常的状态，而无需重新进行整个安装。

## 4.4 安装您的第一个 NetWare 来宾

与 Windows 和 Linux 一样，您的 NetWare 安装始于 CD-ROM 或 ISO 文件。在安装过程中，您创建 DOS 分区和 NetWare 系统分区（池和卷 SYS）。让安装完成整个过程，包括重启，并在过程完成后安装 NetWare 的 VMware Tools。

Tip: 在安装 NetWare 时，当图形界面安装要求您输入服务器名称时拍摄快照。如果在创建环境的安装过程中出现任何问题，回退到此点会比重新开始整个安装更容易。

## 4.5 安装 VMware Tools

如果没有 VMware 可用的额外工具，您的虚拟机仍可运行任何受支持的操作系统；但是，您可能会错过重要功能并且性能可能会下降。工具可解决多个问题，并根据您运行的来宾操作系统为虚拟机添加功能。

工具为您提供的一些功能和好处包括：

- 当鼠标指向虚拟机时自动捕获或释放虚拟机输入的能力。
- 使用 SVGA 视频驱动程序增强图形性能。
- 改进的鼠标输入性能。
- 主机与来宾之间的时间同步。
- 用于在主机和来宾之间共享文件的文件夹共享（Windows 和 Linux）。
- 将文件拖放至虚拟机以及从虚拟机拖放。
- 主机与来宾剪贴板之间的复制和粘贴操作。
- 为虚拟磁盘收缩操作做好准备。

工具随 VMware 软件作为 ISO 文件提供，并存储在 VMware 程序目录中。如果打开 ISO 文件，您会看到 VMware Tools 软件位于虚拟 CD-ROM 映像中，采用其所针对的来宾操作系统的原生应用程序格式：Windows 的 setup.exe、NetWare 的 setup.ncf，以及 Linux 的压缩 tarball 和 RPM 包，其中包含安装脚本。

通过选择 VM → 安装 VMware Tools 可为每个操作系统启动工具的安装。这会将 VMware Tools ISO 文件作为 CD-ROM 设备添加到您的虚拟机中。根据来宾操作系统的设置，安装应用程序将自动启动或需要手动启动。有关如何继续为您的操作系统安装的说明在下一节中介绍。

### Windows 来宾的 VMware Tools

从菜单启动 VMware Tools 安装后，CD-ROM 将在您的 Windows 来宾中可用，如果未禁用自动运行，则会自动启动。否则，您可以从虚拟 CD-ROM 的根目录启动 setup.exe。

对于 Windows NT/XP/2000/2003，您必须以来宾内部的管理员用户身份登录才能安装工具。

通过向导继续 VMware Tools 的安装。工具将被安装，并且显示器、鼠标、SCSI 控制器和 VMXnet 驱动程序的驱动程序将被添加到您的环境中。根据您的 Windows 版本，您可能需要重新启动才能完成安装。

Tip: 工具将显示在 Windows 机器的系统托盘中。如果您在不想让用户知道他们处于虚拟机中的环境中运行 VMware，您可能希望禁用系统托盘图标。您可以通过右键单击系统托盘图标并选择禁用图标来执行此操作。要访问工具设置或启用系统托盘图标，您可以从 Windows 来宾操作系统中的控制面板打开 VMware Tools 配置。

控制面板应用程序可通过阻止访问控制面板的 Windows 策略禁用。或者您可以重命名或删除 Windows 来宾中 VMware Tools 程序目录中的 VMControlPanel.cpl 文件，或以下注册表项中的 VMControlPanel.cpl 值：HKEY_CURRENT_USER\Control Panel\MMCPL。

### Linux 来宾的 VMware Tools

Linux 的工具有两种格式。这些工具是 RPM 包和压缩 tarball。使用 tar 安装时，无法立即启动安装。您首先必须将文件提取到 Linux 来宾中的临时位置。可能需要挂载您的 CD-ROM。您必须以 root 身份运行安装。

安装 Linux VMware Tools 的步骤包含在以下各节中。您的 Linux 发行版可能存在细微差异。对于许多 Linux 发行版，CD-ROM 是一个名为 /dev/cdrom 的设备。这在下一个命令行示例中使用。如果适用于您的 Linux 来宾，请使用其他设备名称。

1. 使用 su - 命令将您的用户环境更改为 root 用户。

2. 如果未自动挂载，您可能需要挂载 CD-ROM。

```
mount /dev/cdrom /media/cdrom
```

如果 /media/cdrom 不存在，请先创建它。您的发行版也可以使用 /mnt/cdrom 或名为 /media/cdrecorder 的目录作为挂载点。

3. 使用 RPM 安装程序时，使用以下命令启动安装：

```
rpm -Uhv /media/cdrom/VMwareTools-5.0.0-13124.i386.rpm
```

使用实际安装的正确路径和文件名。

4. 使用 tar 安装选项时，将安装文件提取到临时目录并运行安装脚本。如果您将临时目录设为当前工作目录，则无需先将文件复制到硬盘。使用以下命令执行此任务：

```
cd /tmp
tar zxf /media/cdrom/VMwareTools-5.0.0-13124.tar.gz
cd vmware-tools-distrib
./vmware-install.pl
```

安装脚本会提示您输入软件和文档将要安装的目录。以下是安装期间建议的默认目录列表：

| 项目 | 路径 |
|---|---|
| 二进制文件 | /usr/bin |
| 初始化目录 | /etc/init.d |
| 初始化脚本 | /etc/init.d |
| 守护进程文件 | /usr/sbin |
| 库文件 | /usr/lib/vmware-tools |
| 文档文件 | /usr/share/doc/vmware-tools |

5. 安装完 RPM 或提取归档后，您可以使用以下命令卸载包含工具的虚拟 CD-ROM：

```
umount /media/cdrom
```

您也可以为特定安装使用挂载点的正确路径。

6. 下一步是运行 VMware Tools 的配置实用程序。要执行此步骤，请使用以下命令执行脚本：

```
vmware-config-tools.pl
```

您可能会遇到脚本关于编译 vmhgfs（虚拟机主机-来宾文件系统）或 VMXnet（网络适配器）驱动程序的错误。如果是这种情况，请确保已安装 C 编译器和内核源代码。Linux 的 VMware Workstation 安装在第 29 页有详细说明。

脚本会提示您为 X 环境选择屏幕分辨率。从建议的分辨率中选择一个适合您需求的分辨率。

Tip: 如果工具配置脚本建议您需要在 GUI 外安装，您可以通过从命令行提示符执行 init 3 命令或按 Ctrl-Alt-Backspace 来结束图形环境。
