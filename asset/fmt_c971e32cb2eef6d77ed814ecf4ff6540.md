
Yum 会咨询其配置文件 `/etc/yum.conf`，并执行更新系统中已安装包所需的所有操作。你可以指定包名来仅更新某些包。例如，要更新内核和 `xorg-x11` 包，请使用以下命令：

```
yum update kernel* xorg-x11*
```

此命令更新所有以 `kernel` 和 `xorg-x11` 开头的包。

你可以使用选项来进一步指示 Yum 做什么。例如，如果你想下载更新后的包但不安装它们，请输入：

```
yum --download-only update
```

另一个典型的选项是 `--exclude`，它允许你从更新过程中排除一个或多个包。假设你想更新除 GNOME 包（名称以 `gnome` 开头）和 `rhythmbox` 包之外的所有内容。那么你输入：

```
yum --exclude=gnome* update
```

## 升级和自定义 Linux 内核

程序员不断改进它的原因之一。例如，某些程序员会为新硬件（如声卡或网卡）编写驱动程序。所有这些创新都会以 Linux 内核的形式呈现给你。

虽然你并不需要在每次有新版本发布时都升级或修改 Linux 系统，但有时你只需要升级，仅仅是因为新版本纠正了某些问题或进行了增强。另一方面，如果较早的内核包含了你需要的所有内容，就没有必要升级。

内核 DVD 是通用的，并使用模块来支持所有类型的硬件；例如，如果你有一个 SCSI 驱动器，你可能想要创建一个支持你的 SCSI 适配器的内核（而不是奔腾处理器）。

在过去，应用补丁是可能的——你通常从网站 `www.kernel.org` 下载 Linux 包（以及最新的内核源码）并使用命令应用补丁。遗憾的是，这些步骤在 Fedora 上运行得不好，因为 Fedora 修改了一些内核文件。在 Fedora 中，你仍然可以将内核升级到更新版本——你必须从 Fedora FTP 服务器获取较新的内核。如果还没有适用于新内核的 RPM，你可以从 `www.kernel.org` 下载整个内核源码，并按照下一节中的说明构建内核。

### 使用 Fedora 内核升级

Fedora 以 RPM 文件的形式发布所有软件更新，包括新版本的内核。要下载并安装内核 RPM，请按照以下步骤操作：

- 1. 使用 Web 服务器从 Fedora 下载服务器下载内核 RPM 文件（下一节将解释细节）。如果你想重建内核，必须下载与新内核对应的 `kernel-devel` RPM。
- 2. 使用 `rpm` 命令安装 RPM。
- 3. 重启系统尝试新内核。

接下来的章节将进一步描述这些步骤。

### 下载新内核 RPM

Fedora 项目在其 FTP 服务器 `http://fedora.redhat.com/download/mirrors.html` 以 RPM 形式提供软件更新。更新根据 Fedora 版本组织目录。例如，对于 Fedora 4 的 x86 系统，使用 `updates/4/i386` 目录。使用 Web 浏览器（如 Mozilla）下载该站点的内核 RPM。

### 安装内核 RPM

要安装内核和模块，请按照以下步骤操作：

- 1. 以 root 身份登录。
- 2. 使用 `cd` 切换到 RPM 文件（从 Fedora 下载的文件）所在的目录。
- 3. 输入以下命令安装内核：

```
rpm -ivh kernel*.rpm
```

如果你想构建新内核，你需要安装 `kernel-devel` RPM。

当你安装新内核时，安装过程会创建一个 RAM 磁盘镜像——内核可以将其复制到内存块并作为内存留磁盘以加载访问硬盘所需的模块的文件。该文件名以 `initrd`（初始 RAM 磁盘的缩写）开头，并在文件名中包含内核版本。内核安装还将内核的描述添加到 GRUB 配置文件 `etc/grub.conf` 中。例如，我安装新内核后典型的 GRUB 配置文件：

```
title Fedora Core (2.6.11-1.1275_FC4)
root (hd0,5)
kernel /vmlinuz-2.6.11-1.1275_FC4 root=LABEL=1 /acpi=off
rhgb quiet
initrd /initrd-2.6.11-1.1275_FC4.img
title Fedora Core (2.6.11-1.1240_FC4)
root (hd0,5)
kernel /vmlinuz-2.6.11-1.1240_FC4 root=LABEL=1 /acpi=off
rhgb quiet
initrd /initrd-2.6.11-1.1240_FC4.img
```

下次你重启系统时，这两个内核将作为选项出现在 GRUB 启动屏幕上。从屏幕，你可以选择想要启动的内核。

## 第21 章：软件安装与更新

### 尝试新内核

安装完新的 RPM 后，是时候尝试新内核了。要重启系统，请以 root 身份登录并在 Linux 提示符下输入以下命令：

```bash
reboot
```

在退出 GNOME 或 KDE 桌面时，你也可以重启系统。在对话框中重启内核，然后点击 OK。

当系统重启并你选择 GRUB 界面时，按下新内核的名称。由于新内核的描述在 GRUB 文件中出现在所有操作系统之前，即使你不在启动界面上做任何操作，内核也应该启动。

Linux 启动后，使用图形化登录界面。以用户身份登录，打开终端窗口，并输入 `uname -sr` 命令查看版本号。响应结果显示你的系统正在运行新版本的内核。

### 重新编译内核

重新编译内核涉及为 Linux 操作系统创建一个新的二进制文件。该二进制文件是 Linux 启动时运行的文件。你可能由于以下原因而需要重新编译内核：

- 如果你最初安装 Linux，你可能想要创建一个包含系统上安装的硬件支持的新内核。特别是，如果你可能想创建一个链接了 SCSI 驱动器的内核。伴随 DVD 中的内核包含了 SCSI 驱动器作为外部模块。
- 如果你有某个只有实验性支持的硬件，你可能需要重新编译内核将其包含在操作系统。
- 你可能想要重新编译内核并生成在你的特定处理器上运行良好的的代码（而不是标准 Linux 发行版自带的通用 386 处理器代码）。

要重新编译内核，你需要内核源码文件。内核源码文件通常不会安装。使用以下步骤在你的系统上安装内核源码文件（内核源码 RPM）：

1. 以 root 身份登录并将伴随 DVD 插入 DVD 驱动器。
2. 如果 DVD 没有自动挂载，输入以下命令挂载 DVD（如果你使用的是 DVD/CD 刻录器，请将 `cdrom` 更改为 `cdrecordver`）：

```bash
mount /media/cdrom
```

如果你使用的是 GNOME 或 KDE，DVD-ROM 会自动挂载，你不必手动执行此步骤。
3. 切换到 DVD-ROM 上的 `Fedora/RPM` 目录，并使用 `rpm` 命令安装内核源码文件。输入以下命令：

```bash
cd /media/cdrom/RPMS
rpm -iv kernel*.src.rpm
```

在 `rpm` 命令完成内核源码包的安装后，源码文件出现在 `/usr/src/redhat` 目录的各个子目录下。
4. 输入以下命令准备内核源码文件：

```bash
cd /usr/src/redhat/SPECS
pmbuild --target i586 -bp kernel*.spec
```

`rpmbuild` 命令解压内核源码文件，将其放置在 `/usr/src/redhat/BUILD` 目录，并应用内核源码 RPM 中的任何补丁。
5. 输入以下命令将源码树移动到 `/usr/src/kernel`：

```bash
cd /usr/src/redhat/BUILD/kernel-*
mv linux-* /usr/src/kernels
```

整个内核源码树应该位于 `/usr/src/kernels/linux-VERSION`，其中 `VERSION` 是当前的内核版本。例如，对于内核 2.6.11，文件位于 `/usr/src/kernels/linux-2.6.11` 目录。现在可以进入该目录并按照本章其余部分的步骤重新编译内核。

如果你在 DVD 上找不到内核源码 RPM，你必须从 `http://fedora.redhat.com/download/mirrors.html` 的其中一个镜像站点下载。点击列出的下载站点之一的链接，然后查找与 Fedora Linux 版本对应的目录。例如，Fedora 4 的源码 RPM (SRP) 文件应该在 `4/SRPMS` 文件中。使用 浏览器下载 `kernel-*.src.rpm` 文件，并按照前文所述的步骤进行安装。

构建内核涉及以下关键阶段：

- 配置内核
- 构建内核
- 构建并安装模块（如果有）
- 构建新的 RAM 磁盘 (`initrd`) 文件
- 安装内核并设置 GRUB

下一节将描述使用硬件支持与直接将硬件支持链接到内核的区别。后续章节将描述内核构建的各个阶段。

## 创建单体内核与模块化内核
