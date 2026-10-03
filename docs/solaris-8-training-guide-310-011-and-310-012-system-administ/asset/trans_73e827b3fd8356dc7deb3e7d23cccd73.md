
| 选项 | 描述 |
|---|---|
| -a | 启动程序将此标志解释为“询问我”，因此会提示输入要加载的独立程序的名称。 |
| -f | 在启动 Autoclient 系统时，此选项强制引导程序绕过客户端的本地缓存，并从客户端的文件服务器通过网络读取所有文件。此选项对所有非 Autoclient 系统均被忽略。-f 选项随后会传递给独立程序。 |
| -r | 在启动期间触发设备重新配置。（此选项在第 16 章“设备管理与磁盘管理”中介绍。） |
| flags | 引导程序将所有启动标志传递给 filename。它不会被 boot 解释。（请参阅下一节，了解默认独立程序 kernel/unix 可用的选项信息。） |

如果 auto-boot? 为 false 时想要启动默认程序，则在 ok 提示符下有几种启动系统的选项。

当你输入以下内容时：

```
boot
```

机器将使用默认启动设备启动，且不使用启动参数。这在 boot-device 变量中设置。

输入以下内容：

```
boot [OBP name]
```

当指定明确的 OBP 名称时，例如 disk3，机器将使用指定的启动设备启动，且不使用启动参数。

这里有一个示例：

```
boot disk3
```

系统将从由 devalias 命名为 disk3 的磁盘驱动器启动。然后它将加载 kernel/unix 作为默认的独立启动程序。

输入

```
boot [options]
```

当使用 boot 命令指定明确的选项时，机器将使用指定的参数从默认启动设备启动。

这里有一个示例：

```
boot -a
```

系统随后会询问要加载的独立程序的名称。如果指定 kernel/unix，即默认值，你将被提示输入包含内核模块的目录。（有关内核模块的详细信息，请参阅下一节。）

输入

```
boot [OBP name] [options]
```

当使用 boot 命令指定明确的启动设备和明确的参数时，机器将使用指定的参数从指定的设备启动。

这里有一个示例：

```
boot disk3 -a
```

此示例将给出与前一个示例相同的提示，只是现在指定了不同的启动设备。系统将从由 devalias 命名为 disk3 的磁盘驱动器启动 bootblock。

在启动过程中，OpenBoot 执行以下任务：

- 1. 固件如果在上次重置后已执行客户端程序，则可以重置机器。客户端程序通常是操作系统或操作系统的加载程序，但 boot 也可用于加载和执行其他类型的程序，例如诊断程序。例如，如果你刚刚发出 test net 命令，下次键入 boot 时，系统将在启动前重置。
- 2. 引导程序使用取决于所选设备类型的协议加载到内存中。你可以从磁盘、磁带、软盘或网络启动。磁盘启动可能从磁盘开头读取固定数量的块，而磁带启动可能读取特定的磁带文件。
- 3. 加载的引导程序被执行。如果在命令行上将参数字符串传递给 boot 命令，则可以进一步控制引导程序的行为。

启动过程中加载并执行的程序是二级引导程序，其目的是加载独立程序。第二级程序在从磁盘启动时为 ufsboot，在通过网络启动时为 inetboot。

如果从磁盘启动，自举过程包含两个概念上不同的阶段：主启动和次启动。PROM 假定主启动程序（bootblk）位于主引导块中，主引导块位于启动设备的扇区 1–15 中。引导块使用 installboot 命令创建。软件安装过程通常会为你安装引导块，因此除非你正在恢复损坏的引导块，否则无需发出此命令。

要将引导块安装到磁盘 c0t3d0s0 上，输入以下内容：

```
installboot /usr/platform/'uname -i'/lib/fs/ufs/bootblk \
/dev/rdsk/c0t3d0s0
```

你无法查看引导块。它位于磁盘中无法查看的受保护区域。引导块区域中的程序将加载名为 ufsboot 的次级启动程序。

执行 boot 命令时，如果指定了 filename，则该 filename 是要加载的独立启动程序的名称。如果路径名是相对路径（不以斜杠开头），ufsboot 将在依赖于平台的搜索路径中查找程序。换句话说，独立程序的相对路径将加上 /platform/<platform-name> 前缀。<platform-name> 将特定于你的硬件。

注意
使用 uname -i 命令确定系统的平台名称。例如，在 SPARCstation10 上，路径将为 /platform/SUNW,SPARCstation-10。使用命令 uname -m 查找系统的硬件类名称；对于 SPARCstation10，硬件类名称将为 sun4m。如果查看 /platform 目录，你会看到 /platform/SUNW,SPARCstation-10 只是指向 /platform/sun4m 的链接。

另一方面，如果 filename 的路径是绝对路径，boot 将使用指定的路径。然后启动程序加载独立程序并将控制权转移给它。

以下示例显示了如何从 OpenBoot ok 提示符指定独立启动程序：

```
ok boot disk5 kernel/unix -s
```

在示例中，PROM 将在 disk5（/iommu/sbus/espdma@f,400000/esp@f,800000/sd@0,0）上查找主引导程序（bootblk）。主启动程序随后将加载 ufsboot。这将使用 -s 标志加载名为 /platform/SUNW,SPARCstation-10/kernel/unix 的独立启动程序。典型的二级启动程序，例如 kernel/unix，接受形如 filename -flags 的参数，其中 filename 是独立程序的路径，-flags 是要传递给独立程序的选项列表。示例将启动操作系统内核，其在下一节中描述。-s 标志将指示内核以单用户模式启动。

## 内核

前一节中描述的二级启动程序 ufsboot 加载操作系统内核。ufsboot 使用的特定于平台的内核名为 /platform/`uname -m`/kernel/unix。

内核初始化自身并开始加载模块，使用 ufsboot 读取文件。在内核加载足够模块以挂载根文件系统后，它会取消映射 ufsboot 程序并继续，使用自己的资源。内核创建一个用户进程并启动 /sbin/init 进程，该进程通过读取 /etc/inittab 文件启动其他进程。（/sbin/init 进程在第 1 章中描述。）

在 Solaris 8 中，内核是动态配置的。它由一个小的静态核心和许多可动态加载的内核模块组成。内核模块是用于在系统上执行特定任务的硬件或软件组件。可加载内核模块的一个示例是设备驱动程序，在访问设备时加载。驱动程序、文件系统、STREAMS 模块和其他模块在需要时自动加载，要么在启动时，要么在运行时。在这些模块不再使用后，可以卸载它们。模块保留在内存中，直到需要该内存为止。modinfo 命令提供有关系统上当前加载的模块的信息。

内核加载时，它会读取存储系统配置信息的 /etc/system 文件。该文件修改内核的参数和对可加载模块的处理。它具体控制以下内容：

- 启动时要加载的默认模块的搜索路径，以及启动时不加载的模块
- 在首次访问前强制在启动时加载的模块
- 根类型和设备
- 用于覆盖默认内核参数值的新的值

以下是默认 /etc/system 文件的示例：

```
*ident      "@(#)system      1.18    97/06/27 SMI" /* SVR4 1.5 */
*
* SYSTEM SPECIFICATION FILE
*
* moddir:
*
*Set the search path for modules. This has a format similar to the
*csh path variable. If the module isn't found in the first directory
*it tries the second and so on. The default is /kernel /usr/kernel
*
*Example:
*moddir: /kernel /usr/kernel /other/modules
* root device and root filesystem configuration:
*
*The following may be used to override the defaults provided by
*the boot program:
*
*rootfs:          Set the filesystem type of the root.
*
*rootdev:         Set the root device. This should be a fully
                  expanded physical pathname. The default is the
                  physical pathname of the device where the boot
                  program resides. The physical pathname is
                  highly platform and configuration dependent.
```
