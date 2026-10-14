

edit，做出你想要的更改，然后按 Ctrl x 根据这些选项启动。

**注意**  如果你发现及时按下 Shift 键有困难，你可能需要编辑 /etc/default/grub 文件并将 GRUB_HIDDEN_TIMEOUT 值改为更大的数字（比如 10），然后运行 sudo update-grub。这样会给你更多时间按下 Shift 键。

## 内核启动过程

当你通过 GRUB 菜单选择一个内核启动时，GRUB 会将内核连同其 initrd 文件（初始 RAM 磁盘）一起加载到内存中。initrd 文件实际上是一个 gzip 压缩的 cpio 归档，在 Ubuntu 下被称为 initramfs 文件。如果你好奇某个特定的 initramfs 文件中包含哪些文件，可以执行以下步骤来提取它：

```
```bash
$ cp initrd.img-2.6.32-14-generic-pae /tmp/initrd.img-2.6.32-14-generic-pae.gz
$ cd /tmp
$ gunzip initrd.img-2.6.32-14-generic-pae.gz
$ mkdir initrd
$ cd initrd
$ cpio -idv < /tmp/initrd.img-2.6.32-14-generic-pae
```
```

现在在你的当前目录中，你应该会看到一组看起来很像常规根目录的目录。bin、sbin、etc、lib 以及其他目录都在那里，但内部只有有限的文件。

当内核启动时，它至少需要能够挂载根文件系统，以便访问基本配置文件、内核模块和系统二进制文件。几年前，拥有一个内置文件系统支持以及 SCSI 和 IDE 设备驱动程序的内核是很常见的。如今有太多硬件和文件系统需要支持，还有诸如软件 RAID、LVM 以及根文件系统加密等特性，因此让这些支持以模块形式存在，使内核在需要时才加载它们，这更有意义。这样可以保持整体内核大小更小，并在各种不同的环境中更灵活。

模块化内核的问题在于它需要从某个地方获取这些模块。如果模块位于根文件系统上，就会产生鸡生蛋蛋生鸡的问题——它必须先挂载根文件系统才能访问挂载根文件系统所需的文件。这就是 initramfs 文件发挥作用的地方。initramfs 文件为内核提供了挂载根文件系统并完成启动过程所必需的基本内核模块和系统二进制文件。当 Ubuntu 内核编译时，构建过程的一部分也会构建 initramfs 文件，并识别并包含内核启动时可能需要的所有核心模块和二进制文件。

当内核启动时，它会将 initramfs 解压到 RAM 中并运行位于 initramfs 根目录下的名为 init 的脚本。如果你对内核启动过程更感兴趣，可以提取 initramfs 并查看此脚本。这里其实并没有太多魔法——只是一个标准的 shell 脚本，它创建一些系统挂载点并挂载实际的根分区。顺便说一下，如果你想知道它如何知道根文件系统在哪里，GRUB 会将该信息作为参数传递给内核，使用 root= 启动参数。最后，在此 init 脚本挂载了真正的根文件系统后，它的最后一个任务是运行根文件系统上的 /sbin/init 程序，从而启动启动过程的下一阶段。

## /sbin/init

/sbin/init 程序是系统上运行的每个程序的父进程。此进程始终具有 PID 为 1，并且负责启动构成运行 Linux 系统的其他进程。那些使用 Linux 有一段时间的人知道，Ubuntu Server 上的 init 与你可能习惯的不同。初始化 UNIX 操作系统有几种不同的标准，但大多数经典 Linux 发行版都使用被称为 System V init 模型（如下所述）的模型，而 Ubuntu Server 已切换到一个名为 Upstart 的系统。Ubuntu 仍然保留了 System V init 的大部分外部结构，例如运行级别和 /etc/rc?.d 目录，以保持向后兼容；然而，Upstart 现在在幕后管理一切。

**经典 System V Init**  在我解释 Upstart 的工作原理之前，先描述经典 System V init 系统的工作方式，然后讨论 Upstart 如何管理一切是有意义的。System V 指的是由

