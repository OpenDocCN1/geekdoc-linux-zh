
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

# 安装内核包：/boot

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

# 第 7 章：内核管理

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

### 使用 Fedora SRPM 安装内核源码

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
