
Fedora 和 Red Hat 为 32 位和 64 位提供了不同的内核包。每个内核都将包含多处理器支持。内核将包含 x86 版本和 64 位版本。对于 32 位，三个不同的内核包，分别针对 Intel（CPU 及以上）、AMD CPU 以及 PAE（用于大于 4GB 的 32 位系统）。每个包的名称中都包含 CPU 参考：

```
kernel-2.6.version.i586
kernel-PAE-2.6.version.i686
```

对于 64 位系统（如 Athlon 64 系列和 Intel Core Duo），64 位发行版仅包含 x86_64 包：

```
kernel-2.6.version.x86_64
```

注意：Xen 虚拟化、SMP（多处理器支持）和 kdump（调试支持支持）已集成到内核中。

对于每个内核，还有相应的内核头文件（也称为 devel），用于编译内核模块或不需要完整内核源码的应用程序，只需头文件即可。内核头文件将安装在 `/etc/src/kernels` 目录，并在内核的 `/lib/modules` 目录中有指向它的链接。

## 安装内核包：`/boot`

带有最新补丁的新内核作为更新提供。你可以使用 PackageKit 安装其他类型的 PAE 内核。你也可以创建并手动安装自己的自定义内核。

## 更新内核包

PackageKit 更新系统会在内核可用时自动下载并安装，选择适用于你系统的版本。通常你不需要执行任何操作来安装最新内核，只需执行安装即可。它们将由包更新程序为你安装。旧内核将保留安装，以防新内核出现问题。如果出现问题，你可以从 GRUB 菜单中选择旧内核并使用。

GRUB 引导加载程序配置文件将自动为你编辑以启动新内核。新内核条目将放置在 `/boot/grub/grub.conf` 文件中，保留旧内核条目。所有其他条目和配置将保持不变。仅添加了新内核条目。

## 安装不同的内核包

如果你想安装特定的内核，而不仅仅是更新当前安装的版本，可以使用 PackageKit 或 `yum` 命令来选择并安装新内核。如果你想安装不同类型的内核，例如 PAE 内核（大内存寻址），可能需要执行此操作。在 PackageKit 上，搜索“kernel”以列出可用内核包。使用 `yum`，只需输入模式 `kernel*` 即可列出可用包。安装你需要的那个。

```
yum list kernel*
```

PackageKit 和 `yum` 命令使用 YUM，它会自动选择并安装任何依赖包，并跟踪任何需要的更新。出于此原因，PackageKit 和 `yum` 命令是安装新内核的首选方法。

## 安装自定义内核包

或者，你也可以在窗口中通过 `rpm` 命令安装特定的内核 RPM 包。对于可能不在你的 YUM 仓库中的自定义内核包，可能需要这种方法。为了确保内核 RPM 包下载时没有错误并验证其身份，你可以使用带有 `--checksig` 选项的 `rpm` 命令（要安装该包，请使用新的公钥）：

```
rpm --checksig rpm
```

你现在可以安装内核了。作为安全预防措施，你应该保留旧内核，以防新内核由于某些原因无法工作。这涉及使用安装 (`-i`) 选项而不是更新 (`-U`) 选项，为新内核创建一个独立的 RAM ，然后修改 `grub.conf` 让 GRUB 使用新内核。

```
rpm -ivh kernel-2.6.version.i686.rpm
```

## 对已安装内核进行 GRUB 修改

内核安装在 `/boot` 目录下。在此目录下执行 `ls -l` 操作会列出所有当前安装的内核。你的旧内核文件和一个新内核文件都存在。当安装新内核时，GRUB 启动加载器配置文件 (`/boot/boot.conf`) 会自动修改以添加调用新内核的条目。内核使用 `/boot/mlinuz-version` 内内核启动。在你的 `grub.conf` 中，将有一行引用此内核文件。

还会有一个 RAM 磁盘文件 `initrd`。如果你的系统有 RAID 磁盘或任何特殊硬件，RPM 还会使用 `mkinitrd` 命令创建一个 RAM 磁盘来存放适当的支持模块。RAM 磁盘命名为 `initrd-kernel-version.img`，位于 `/boot` 目录，例如 `/boot/initrd-2.6.version.img`。

```
kernel /boot/mlinuz-version root=/dev/sda3
initrd /boot/initrd-version.img
```

如果你正在安装自定义内核，你可能需要自己进行这些修改。

提示：虽然 Fedora 不包含它，但用户态 Linux (UML) 是内核的一个可选版本，设计为作为独立于内核的程序运行。

## 第 7 章：内核管理

实际上，它创建了一个在用户文件上实现磁盘存储的虚拟机。UML 通常用于测试软件或实验内核配置，而不会损坏真实系统。你还可以使用 UML 通过在一个物理宿主机上运行虚拟机来实现虚拟托管。通过虚拟机，你可以控制对宿主系统的访问，从而提供更高的安全性。你可以在 http://user-mode.linux.sourceforge.net 了解更多关于用户态 Linux 的信息。

## 修改相同版本内核的预防步骤

如果你想修改内核配置并构建新内核，你应该尝试给内核起一个不同的名称。这样你的内核就不会被覆盖。作为预防措施，你可以为当前内核创建一个备份副本。万一修改后的版本出现问题，你也可以从保留的副本中启动。如果你正在安装新版本的内核，就不必担心这种情况。新内核被赋予了不同的名称，因此旧内核不会被覆盖。

## 启动加载器手动配置

安装内核包将自动为新内核创建 GRUB 启动加载器条目。你可以在启动时选择它。你的内核条目将保持保留。你应该创建一个当前内核的自定义版本，并保留原始版本作为备份。然后你需要在启动加载器配置文件中为原始内核创建一个新条目。建议保留原始条目，以防新内核出现问题。通过这样，你也可以重启并选择原始内核。例如，在 `/boot/grub.conf` 中添加一个与旧内核条目类似的新条目，其在系统中引用新内核。`grub.conf` 条目看起来像下面的代码。你可以取消选择原始内核。

```
title Original Kernel
kernel /boot/mlinuz-version root=/dev/sda3
initrd /boot/initrd-version.img
```

## 从源码创建内核

与其使用已经编译的内核二进制版本，你可以在系统上安装内核源码并使用它自己创建二进制文件。内核源文件与其他源码一样使用 `gcc` 编译器编译。编译内核的一个优势是你可以增强其配置，增加对某些设备的支持。

务必参考 Fedora 项目关于构建内核的文档：http://fedaproject.org/wiki/Building_a_kernel

## 使用 Fedora SRPM 安装内核源码

你可以通过 Yum 也可以直接从 Fedora 发行版的 `SRPMS` 目录获取 Fedora 的源码包。源码包不包含二进制文件。

要从 Fedora 发行版下载，首先使用浏览器或 FTP 客户端访问 Fedora 发行版的 FTP 或镜像站点。然后切换到源码目录。以下是 Fedora 发行站点内核包的完整 URL。

```
http://download.fedora.org.com/pub/fedora/linux/Fedora/source/SRPMS/kernel-2.6.29-591.fcc1.src.rpm
```

要安装该包，请在终端窗口中使用所示的 `rpm` 命令。使用浏览器，你也可以在下载时使用安装选项。

```
rpm -ivh kernel-2.6.29-591.fcc1.src.rpm
```

或者，你可以使用 `yum` 下载源码包。除非你需要经常为应用程序下载源码，否则你可能想要启用源码仓库以下载内核源码包。要执行此操作，你在终端窗口中使用 `yum` 命令并指定 `--enablingrepo=fedora-source`。

```
--enablingrepo=fedora-source
```

你还需要 `rpm-build` 包中的 `rpmbuild` 工具，以及 `rpmdevtools` 包中额外的 rpm 开发工具。还要确保已安装 `yum-utils` 包。该包包含了 `yumdownloader` 工具，你可以用它下载特定的 rpm 包而不是安装它。你将使用 `yumdownloader` 或 FTP 下载源码 rpm 包。

`rpm-build`

`rpmdevtools`

`yum-utils`

`yumdownloader --enablerepo-kernel-source --source kernel`

你应该确保已经安装了构建内核源码所需的所有工具和包。要做到这一点，请在内核源码 RPM 包上运行 `yum-builddep` 命令。你必须以 root 用户身份运行此命令。你可以使用 `su -` 命令

```bash
su -c 'yum-builddep kernel-2.6.29.5-191.fc11.src.rpm'
```

注意：Fedora 源仓库配置在 `/etc/yum.repos.d/fedora.repo` 文件中，位于 `[fedora-source]` 部分。`enabled` 选项默认设置为 0，禁用了该源。要启用它，你可以编辑 `fedora.repo` 文件并将 `enabled` 选项设置为 1。

### 编译内核源码

Fedora RPM 源码是通过 Fedora RPM 目录管理的，而不是传统的 `/usr/src`。始终建议你不要以 root 用户身份管理和构建内核源码。你不应该以 root 用户直接安装 RPM 源码内核包，这将把文件放在 `/usr/src/redhat` 目录下。应避免在该目录下使用内核源码。

相反，你应该始终作为本地用户将内核源码安装在本地目录，而不是 root 用户（从 http://kernel.org 下载的内核归档文件也是如此）。你仍然需要使用 `rpmbuild` 一组指令，如 `SPEC` 和 `BUILD`。要设置此本地构建环境，你使用 `rpmdev-settree` 命令（来自 `rpmdevtools` 包）。在登录你想要用于管理内核源码的用户后，运行此命令。

`rpmdev-settree`

此命令将创建一个 `rpmbuild` 目录，并带有包含 `SPEC`、`Build`、`RPMS`、`SOURCES` 和 `SRPMS` 的子目录。二进制文件构建在 `$(HOME)/rpmbuild`，其中 `$(HOME)` 为你的家目录。

将 RPM 包移动到 `rpmbuild` 目录，然后运行 `rpm` 命令 `-Uvh` 来提取它。会出现错误消息显示正在使用 root，但实际上并不是你。你可以忽略该错误消息。

```bash
rpm -Uvh kernel-2.6.27.9-159.fc11.src.rpm
```

RPM 规格文件 `kernel-2.6.27.spec` 将被放在 `SPEC` 目录。配置信息、补丁和内核源码的压缩包被放在 `SOURCES` 目录。

要生成源码，你随后使用 `rpmbuild` 命令配合内核规格文件，并指定你想要的架构类型。切换到 `SPECS` 目录并运行

### 第一部分：系统管理

带有 `-bp`（构建）选项和指定架构的 `--target` 选项的 `rpmbuild`。以下命令将提取 i86 版本的内核：

```bash
rpmbuild -bp --target=i86 kernel.spec
```

提取的内核源码将位于 `BUILD` 目录下的 `kernel-2.6.29` 中，其中包含 i86 版本和原生版本 `linux-2.6.29.i86` 以及 `vanilla-2.6.29` 的子目录。你可以切换到 i86 目录然后运行 `make xconfig` 命令来配置内核源码。

一旦完成对内核的修改，你将使用 `rpmbuild` 命令生成内核二进制文件并封装成 RPM 包以进行安装。

### 不同的内核系统配置

如果你想使用不同的配置，则需要为该特定变体配置内核源码。这些配置位于内核源码的 `configs` 目录中。对于 i386 RPM 源码，你将找到适用于 x86 系统、i386 和 i686 的内核配置文件。

`.config` 文件将是在你从 `rpmbuild` 提取源码时在 `target` 选项中指定的版本。对于不同的配置，你将所需的配置文件复制为 `.config` 文件并放在内核源码的根目录下。以下示例将 i686 配置复制为内核源码配置目录：

```bash
cp configs/kernel.2.6.29-i686.config .config
```

然后，通过执行以下命令使用新配置更新你的内核源码：

`make oldconfig`

> 提示：如果你在使用原始内核源码，还应该检查补丁。

### 配置内核

一旦安装了源码，你就可以配置内核。配置包括确定你希望为其提供内核级支持的功能。这些包括针对不同设备的驱动程序，例如声卡和 SCSI 设备。你可以将功能配置为直接包含在内核中，或者作为内核可以加载的模块。你也可以专门排除某些功能。直接整合到内核的功能会产生更大的内核程序。设置为模块的功能也可以被易于更新。许多提供音频、视频或网络支持的设备文档可以在 `/usr/share/doc` 目录下找到。检查 `kernel-doc` 包可以找到所提供的文档列表。

```bash
rpm -ql kernel-doc
```

注意：如果你之前配置过内核，现在想从默认设置重新开始，可以使用 `make mrproper` 命令恢复默认内核配置。

### 内核配置工具

`config`、`menuconfig`、`xconfig` (qconfig) 和 `gconfig` (gkc)。你也可以直接编辑配置文件。这些工具执行相同的配置任务，但使用不同的界面。`config` 工具是一个简单的配置脚本，为不同的配置选项提供基于行的提示。`menuconfig` 工具提供基于光标的菜单，你仍然可以从命令行运行它。（注：由于原始 OCR 文本包含大量 `menuconfig` 重复，此处已清理。）

### 206 第一部分：系统管理

用于实际的模块名称；可选 yes、no 和模块条目的 Range（范围）；以及选项状态的数据，标题为 Value（值）。

Range 条目标题为 N、M 和 Y，用于选择是否不包含某个选项 (N)、将其作为模块加载 (M) 或将其直接编译到内核 (Y)。你可以选择的条目将显示下划线。下划线会将条目更改为 Y（模块或直接包含内核内核）或 N（不包含）。Value 列将显示当前选中的是哪一个。

![](img/74df054815dc70d661e697bc3d5ff87a_207_0.png)

图 7-1：gconfig 内配置 (make gconfig)

Options（选项）列将包含一个状态，显示该选项是直接包含（标记）还是完全不包含（空）。要快速选择或取消选择条目，请双击 Options 字段中的选项名称。你将看到它是被勾选的、划线的（模块）还是空的。相应的用于不包含、模块或内核包含的 N、M 和 Y 条目会被选中。该选项每个模块或直接内核内核的默认偏好会自动选中。如果你需要，可以手动更改。

### menuconfig

`menuconfig` 选项生成一个基于选择器的文本菜单。你可以使用方向键、tab 和回车键在不同的菜单和条目之间移动（见图 7-2）。使用空格键选择或取消选择条目。

### xconfig (qconfig)

`xconfig` 选项调用 qconfig 工具，该工具基于 KDE QT 库。必须先安装 KDE。qconfig 工具打开一个 Linux 内核配置窗口，列出不同的配置类别。它的界面稍微简单，没有模块列的展开或折叠按钮，也没有 qconfig 拥状态行。

root@richards:~/src/refinet/build/linux-kernel-2.6.25/linux-2.6.25.x86_64 207

![](img/74df054815dc70d661e697bc3d5ff87a_208_0.png)

图 7-2：menuconfig 内核配置 (make menuconfig)

### 重要内核配置特性

`xconfig`、`menuconfig` 和 `gconfig` 工具为每个条目提供上下文相关的帮助。每个条目的右侧都有一个 Help（帮助）按钮。点击它可以详细说明该功能的作用以及你为什么要直接包含或作为模块包含它，甚至包含它。当你对某个功能有疑问时，始终使用 Help 按钮来了解它的具体作用以及你为什么要使用它。许多关键特性在这里都有了描述。功能的主要类别列在括号中。

提示：根据原则，持续使用的功能（如网络和文件系统支持）应该直接编译到内核。容易改变的功能（如声卡）或使用不频繁的功能应该编译为模块。否则，你的内核镜像文件可能会变得太大且运行速度变慢。

- 可载式模块支持：在大多数情况下，你应该确保你的内核可以加载模块。点击 Loadable Module Support 显示若干模块管理选项列表。确保 Enable Loadable Module Support 已勾选。此功能允许你的内核在需要时加载模块。Kernel Module Loader 也应设置为 Yes，这允许你的守护进程（例如你的 Web 服务器）加载它们可能需要的任何模块。

- 处理器类型和特性：Processor Type And Entries 允许你为特定系统设置支持。在这里，你选择你拥有的处理器类型和处理器特性。

- 电源管理特性：启用电源管理支持，如 CPU 调节和 ACPI。

- 设备驱动：Devices Drivers 列出了启用对你的 SATA、SCSI、视频、声音和 USB 设备等支持的条目。

### 208 第一部分：系统管理

- **多设备支持 (RAID 和 LVM) (Device Drivers)**：Multi-Device Support 列出了启用使用 RAID 设备的条目。你可以选择所需的 RAID 支持级别。在这里你还可以启用逻辑卷管理支持 (LVM)，它允许你将分区组合成可以动态管理的逻辑卷。
