

如果您的系统有 SCSI 控制器或任何其他专用硬件，RPM 还会创建一个 RAM 磁盘来保存适当的支持模块（您可以使用 mkinitrd 命令手动创建 RAM 磁盘）。RAM 磁盘名为 initrd-kernel-version.img，位于 /boot 目录中，如 /boot/initrd-2.4.22-1.img。

> 提示 redhat-config-packages 工具不支持内核软件包安装。您必须使用终端窗口中的 rpm 命令手动安装内核软件包。

如果您正在定制内核，安装内核的源代码和头文件也是必不可少的。您需要源代码来生成任何模块，并根据自己的需要调整内核。例如，您可以使用源代码生成包含您可能已安装的任何不常见设备驱动程序的模块，如下所示：

```
# rpm -Uvh kernel-source-2.4.22-1.2115.nptl.1386.rpm
```

在大多数发行版中，内核安装在 /boot 目录中。对该目录执行 ls -l 操作会列出所有当前已安装的内核。现在会有一个旧内核文件和一个新内核文件，以及一个名为 vmlinuz 的链接文件，它指向新的内核文件。如果您按照上一节所述采取了预防措施，则可能已经重命名了旧内核。如果您使用的是 GRUB 之类的引导加载程序，则无需更改其配置文件（grub.conf），因为调用内核的条目仍然引用 /boot/vmlinuz 链接，而该链接现在指向新内核。内核通过 /boot/vmlinuz 链接启动内核文件。在 grub.conf 文件中，内核文件的内核行引用此链接。您还需要为 RAM 磁盘 initrd 添加一行。

```
kernel /boot/vmlinuz-2.4.22-1.2115.nptl ro root=/dev/hda 3
initrd /boot/initrd-2.4.22-1.2115.nptl.img
```

> 提示 虽然 Red Hat 10 中没有包含用户模式 Linux（UML），但它是内核的一个可选版本，设计为独立于内核的单独程序运行。实际上，它创建了一个虚拟机，其磁盘存储在用户文件上实现。UML 常用于测试软件或试验内核配置，而不会破坏真实系统。您还可以使用 UML 通过在单个物理主机上运行多个虚拟机来实现虚拟主机。通过虚拟机，您可以控制对主机系统的访问，提供更高的安全性。您可以在 user-mode-linux.sourceforge.net 上找到有关用户模式 Linux 的更多信息。

## 修改相同版本内核的预防措施

如果您想修改内核配置并构建新内核，则应保留当前内核的副本。如果修改后的版本出现问题，您始终可以从保留的副本启动。如果您安装的是新版本的内核，则不必担心这种情况。新内核会被赋予不同的名称，因此旧内核不会被覆盖。

和 module-info。这个 System.map 文件包含了模块启动内核功能所需的内核符号。例如，内核映像文件名为 vmlinuz-version，其中 version 是附加的版本号，如 vmlinuz-2.4.22-1。该内核的 System.map 文件名为 System.map-2.4.22-1。以下是版本 2.4.22-1 的内核文件。

```
/boot/vmlinuz-2.4.22-1
/boot/System.map-2.4.22-1
/boot/module-info-2.4.22-1
/boot/config-2.4.22-1
```

特定内核的 vmlinuz、System.map 和 module-info 文件也有使用这些名称（不带版本号）的符号链接。例如，vmlinuz 是指向当前内核映像文件（此处为 vmlinuz-2.4.22-1）的链接，System.map 是指向当前 System.map 文件 System.map-2.4.22-1 的链接。当您安装新内核时，链接会改为指向该内核。因此，如果您安装了新版本（如 2.4.22-10），/boot/vmlinuz 将会链接到该内核的 vmlinuz 文件 /boot/vmlinuz-2.4.22-10。

```
/boot/vmlinuz          /boot/vmlinuz-2.4.22-1
/boot/System.map       /boot/System.map-2.4.22-1
/boot/module-info      /boot/module-info-2.4.22-1
```

另一方面，如果您正在创建同一内核的修改版本，内核文件（此处称为 vmlinuz-2.4.22-1）将连同 System.map 和 module-info 文件一起被新的内核映像文件覆盖。为了保留当前可用的版本，您必须首先制作这些文件的副本。您可以将 /boot/vmlinuz-2.4.22-1 文件复制一份，并赋予另一个名称，如下所示：

```
cp /boot/vmlinuz-2.4.22-1 /boot/vmlinuz-2.4.22-1.old
```

您还应该备份 System.map 和 module-info 文件。System.map 文件是指向 System.map-2.4.22-1 文件的符号链接。您还应该备份位于 /lib/modules/version 目录中的模块，其中 version 是内核的版本号。否则，您将丢失已经设置为与原始内核一起工作的模块。对于版本 2.4.22-1，库位于 /lib/modules/2.4.22-1。如果您编译的是不同版本，这些库将放在以新版本号命名的新目录中。

## 引导加载程序

如果您使用引导加载程序，则应在引导加载程序配置文件中为旧内核创建一个新条目。然后您可以为新内核创建一个条目。建议保留旧内核的条目，以防新内核出现问题。这样，您可以随时重新启动并选择旧内核。例如，在 grub.conf 中，添加一个类似于旧内核的新条目，其 kernel 语句中引用了新内核。grub.conf 条目如下代码所示。然后您可以在 GRUB 菜单中选择标题为 "Old Linux (2.4.22-1.old)" 的条目来启动旧内核。

```
title Old Linux (2.4.22-1.old)
root (hd0,2)
kernel /boot/vmlinuz-2.4.22-1.old root=/dev/hda3
initrd /boot/initrd-2.4.22-1.old.img
```

