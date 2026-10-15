
to compile the software. And finally, run
`sudo make install`.

If the compile fails, check the error messages for the reason and run
`make clean`
before you start again. You can also run
`sudo make uninstall`
to remove the software if you do not like it.

## Relevant Ubuntu and Linux Commands

You will use these commands while managing your Ubuntu system resources and software packages:

- `apt-get`—The default command-line package-management tool (see Chapter 30 for more on APT)
- `gnome-app-install`—The Ubuntu GUI Package Manager
- `synaptic`—Advanced tool for software manipulation and repository editing
- `update-manager`—The primary source of Ubuntu package updates

#### Reference

- http://www.debian.org/doc/manuals/project-history/ch-detailed.en.html—History of the Debian Linux package system.
- http://www.nongnu.org/synaptic/—Home of the Synaptic package manager.
- http://www.ubuntu.com/usn—The official list of Ubuntu security notices.

This page intentionally left blank

## CHAPTER 32

## Kernel and Module Management

#### IN THIS CHAPTER

- The Linux Kernel
- Managing Modules
- When to Recompile
- Kernel Versions
- Obtaining the Kernel Sources
- Patching the Kernel
- Compiling the Kernel
- When Something Goes Wrong
- Reference

A kernel is a complex piece of software that manages the processes and process interactions that take place within an operating system. As a user, you rarely, if ever, interact directly with it. Instead, you work with the applications that the kernel manages.

The Linux kernel is Linux. It is the result of years of co-operative (and sometimes contentious) work by numerous people around the world. There is only one common kernel source tree, but each major Linux distribution manages and patches its version slightly to add features, performance, or options. Each Linux distribution, including Ubuntu, comes with its own precompiled kernel as well as the kernel source code, providing you with absolute authority over the Linux operating system. In this chapter, we will examine the kernel and learn what it does for us and for the operating system.

In this chapter, you also learn how to obtain the kernel sources, as well as how and when to patch the kernel. The chapter leads you through an expert’s tour of the kernel architecture and teaches you essential steps in kernel configuration, how to build and install modules, and how to compile drivers in Ubuntu. This chapter also teaches you important aspects of working with GRUB, the default Ubuntu boot loader. Finally, the chapter’s troubleshooting information will help you understand what to do when something goes wrong with your Linux kernel installation or compilation process. As disconcerting as these problems can seem, this chapter shows you some easy fixes for many kernel problems.

Most users find that the precompiled Ubuntu kernel suits their needs. At some point, you might need to recompile
the kernel to support a specific piece of hardware or add a new feature to the operating system. If you have heard horror stories about the difficulties of recompiling the Linux kernel, you can relax; this chapter gives you all the information you need to understand when recompiling is necessary and how to painlessly work through the process.

## The Linux Kernel

The Linux kernel is the management part of the operating system that many people call “Linux.” Although many think of the entire distribution as Linux, the only piece that can correctly be called Linux is the kernel. Ubuntu, like many Linux distributions, includes a kernel packaged with add-on software that interacts with the kernel so that the user can interface with the system in a meaningful manner.

The system utilities and user programs enable computers to become valuable tools to a user.

## The First Linux Kernel

In 1991, Linus Torvalds released version .99 of the Linux kernel as the result of his desire for a powerful, UNIX-like operating system for his Intel 80386 personal computer. Linus wrote the initial code necessary to create what is now known as the Linux kernel and combined it with Richard Stallman’s GNU tools. Indeed, because many of the Linux basic system tools come from the GNU Project, many people refer to the operating system as GNU/Linux. Since then, Linux has benefited as thousands of contributors add their talents and time to the Linux project. Linus still maintains the kernel, deciding on what will and will not make it into the kernel as official releases, known to many as the “vanilla” or “Linux” Linux kernel.

## The Linux Source Tree

The source code for the Linux kernel is kept in a group of directories called the kernel source tree. The structure of the kernel source tree is important because the process of compiling (building) the kernel is automated; it is controlled by scripts interpreted by the `make` application. These scripts, known as makefiles, expect to find the pieces of the kernel code in specific places or they will not work. You will learn how to use `make` to compile a kernel later in this chapter.

It is not necessary for the Linux kernel source code to be installed on your system for the system to run or for you to accomplish typical tasks such as email, web browsing, or word processing. It is necessary that the kernel sources be installed, however, if you want to compile a new kernel. In the next section, we will show you how to install the kernel source files and how to set up the special symbolic link required. That link is `/usr/src/linux-2.6`, and it is how we will refer to the directory of the kernel source tree as we examine the contents of the kernel source tree.

The `/usr/src/linux-2.6` directory contains the `.config` and the `Makefile` files among others. The `.config` file is the configuration of your Linux kernel as it was compiled.

默认情况下没有 `.config` 文件；你必须从 `/configs` 子目录中选择一个。在那里，你会找到 Ubuntu 提供的每种内核版本对应的配置文件；只需将适用于你系统的那个复制到默认目录并重命名为 `.config` 即可。

我们已经讨论过 `/configs` 子目录的内容，那么让我们来查看 `/usr/src/linux-2.6` 下的其他目录。对我们最有用的是 `Documentation` 目录。在它及其子目录中，你会找到关于内核各个部分的几乎所有文档。每个 `Documentation` 子目录都包含一个 `00-INDEX` 文件，`00-INDEX` 文件列出了主目录中的文件以及它们简要的说明。许多文件仅为内核程序员和应用程序编写者编写，但其中一些对于试图了解内核和设备驱动程序问题的中级或高级 Linux 用户来说是有用的。其中一些更有趣且有用的文档是

- `devices.txt`—列出了 `/dev` 目录中表示的所有可能的 Linux 设备，给出了主设备号和次设备号以及简短描述。如果你曾经收到过提及 char -major -xxx 的错误信息，这个文件就是该列表的存放位置。

- `ide.txt`—如果你的系统使用 IDE 硬盘，此文件讨论了内核如何与它们交互，并列出了可用于解决 IDE 相关硬件问题、手动设置数据传输模式以及以其他方式手动管理 IDE 驱动器的各种内核命令。大多数管理是自动的，但如果你想了解内核如何与 IDE 设备交互，此文件会进行解释。

- `initrd.txt`—此文件提供了关于初始 RAM 磁盘的更深入知识，详细说明了用于创建和挂载它们的回环文件系统，并解释了内核如何与它们交互。

- `kernel-parameters.txt`—此文件列出了可在启动时传递以配置内核或硬件设置的大多数参数，但乍一看似乎不太有用，因为它只是一个列表。然而，知道某个参数存在并且可能与你正在寻找的内容相关，可以帮助你追踪更多信息，因为现在你有了可输入到互联网搜索引擎（如 http://www.google.com/linux）中的术语。

- `sysrq.txt`—如果你曾经想过键盘上标记为“SysRq”的那个键是用来做什么的，这个文件有答案。简而言之，它是硬编码到内核中的一个键组合，可以帮助你从系统死锁中恢复。Ubuntu 出于安全原因默认禁用此功能。你可以通过输入命令 `# echo "1" > /proc/sys/kernel/sysrq` 来重新启用它，并通过回显 0 而不是 1 的值来禁用它。

在 `Documentation` 中找到的其他目录中，你会找到类似的文本文件，涉及 CD-ROM 驱动程序、文件系统驱动程序、游戏端口和操纵杆驱动程序、视频驱动程序（不是显卡驱动程序——那些属于 X11R6 而不是内核）、网络驱动程序以及 Linux 操作系统中找到的所有其他驱动程序和系统。同样，这些文档通常是为程序员编写的，但它们也可以为中级和高级 Linux 用户提供有用的信息。

名为 `scripts` 的目录包含许多使...使用的脚本。它真的不包含任何对非程序员或内核开发人员（也称为内核黑客）以外的任何人有兴趣的东西。

内核构建完成后，所有编译后的文件都会进入 `arch` 目录及其子目录。虽然你可以手动将它们移动到最终位置，但我们将在本章后面向你展示 `make` 脚本将如何为你完成此操作。在 Linux 的早期阶段，这种编译后的文件重新定位都是手工完成的；你应该感谢 `make`。

> **NOTE**
> 
> `make` 实用程序是一个非常复杂的程序。关于 `make` 文件的结构的完整文档，以及它可以接受的参数，可以在 http://www.gnu.org/software/make/manual/make.html 找到。

`/usr/src/linux-2.6` 中剩余的目录包含内核和内核驱动程序的源代码。当你安装内核源代码时，这些文件会自动放置在那里。当你修补内核源代码时，这些文件会自动被更改。当你编译内核时，这些文件会自动被访问。虽然你永远不需要触碰源代码文件，但它们可能很有用。内核源代码文件只不过是具有特殊格式的文本文件，这意味着我们可以查看它们并阅读程序员的注释。有时，程序员会编写一个应用程序，但不能（或通常不愿）编写文档。他在源代码中放入的注释通常是代码存在的唯一文档。

一些代码的注释中甚至“隐藏”了小型测试程序，以及注释和其他信息的引用。由于源代码是用一种几乎像英语一样容易阅读的语言编写的，非程序员可能能够大致了解应用程序或驱动程序实际在做什么（参见第 30 章，“Ubuntu 的 C/C++ 编程工具”）。当中级到高级 Linux 用户遇到与内核和驱动程序相关的问题时，这些信息可能很有用。

> **NOTE**
> 
> 硬件的交互和控制由内核中的一小部分代码处理，称为设备驱动程序。驱动程序告诉计算机如何响应用户提示与调制解调器、SCSI 卡、键盘、鼠标等进行交互。没有设备驱动程序，内核就不知道如何与相关设备交互。

## 内核类型

在 Linux 早期的日子里，内核是一个包含处理器、主板和其他硬件指令的单一代码块。如果你更换了硬件，就必须重新编译内核代码以包含你需要的部分并丢弃不需要的部分。包含额外的、不必要的代码会带来惩罚，因为内核变得更大并占用更多内存。在只有 4MB-8MB 内存的老系统上，为不必要的代码浪费宝贵内存被认为是不可以接受的。内核编译有点像“黑魔法”，早期的 Linux 用户试图从他们的计算机中榨取最多的性能。这些编译成单一代码块的内核被称为单体内核。

随着内核代码变得越来越大，能够添加到计算机中的设备数量也随之增加，重新编译的需求变得繁重。一种新的构建内核的方法被开发出来以使编译任务更容易。内核源代码中构成设备驱动程序代码的部分可以作为模块可选编译，该模块可以根据需要加载和卸载到内核中。这被称为构建内核的模块化方法。现在，所有的内核代码都可以一次性编译——其中大部分代码编译成这些模块。只有所需的模块会被加载；内核可以保持更小，添加硬件也变得简单得多。

典型的 Ubuntu 内核有一些驱动程序编译为内核本身的一部分（称为内联驱动程序），而其他驱动程序则编译为模块。只有在引导过程中编译为内联的设备驱动程序才可供内核使用；模块化驱动程序仅在系统引导后才可用。

> NOTE
> 作为一个常见例子，如果你打算从 SCSI 磁盘启动，SCSI 磁盘驱动程序必须可供内核使用。如果内核没有内联编译这些驱动程序，系统将无法启动，因为它将无法访问磁盘。
> 对于模块化内核，解决此问题的一种方法是使用稍后在“创建初始 RAM 磁盘映像”中讨论的初始 Ram 磁盘（initrd）。initrd 加载一个小型内核和适当的设备驱动程序，然后可以访问该设备以加载你想要运行的实际内核。

一些代码只能是两者之一（出于对普通用户不重要的技术原因），但大多数代码可以编译为模块化或内联。取决于应用，一些系统管理员更喜欢一种方式而不是另一种，但对于快速的现代处理器和充足的系统内存来说，性能差异对除最狂热的 Linux 黑客之外的所有人来说都无关紧要。

编译内核时，选择模块化或内联的步骤是 `make config` 步骤的一部分，我们将在本章后面详细说明。除非你有特定的理由另行操作，否则我们建议你在有选择时选择模块化选项。管理模块的过程将在下一节中介绍，因为你管理模块的频率会比编译内核更频繁。

## 管理模块

使用模块化内核时，需要特殊的工具来管理模块。模块必须加载和卸载，最好能尽可能自动完成。我们还需要能够在加载模块时传递必要的参数——例如内存地址和中断。（该信息因模块而异，因此你需要查看模块的文档以确定是否需要向其传递信息。）在本节中，我们将介绍用于管理模块的工具，然后看几个使用它们的例子。

Linux 为我们提供了以下模块管理工具。所有这些命令（以及 `modprobe.conf`）都有 man 手册：

- `lsmod`—此命令列出已加载的模块。将它通过 `less` 命令管道传输很有用，因为列表通常超过一页。
- `insmod`—此命令将指定的模块加载到正在运行的内核中。如果只给出模块名称而没有完整路径，则会搜索正在运行内核的默认位置 `/lib/modules/* /`。此命令提供了几个选项——最有用的是 `-f`，它强制加载模块。
- `rmmod`—此命令从正在运行的内核中卸载（移除）指定的模块。可以一次指定多个模块。
- `modprobe`—`insmod` 和 `rmmod` 的更复杂版本，它使用 `depmod` 创建的依赖文件并自动处理加载，或使用 `-r` 选项移除模块。然而没有强制选项。`modprobe` 的一个有用选项是 `-t`，它使 `modprobe` 在一组驱动程序中循环，直到找到匹配你系统的驱动程序。如果你不确定哪个模块适用于你的网卡，你会使用此命令：

```
