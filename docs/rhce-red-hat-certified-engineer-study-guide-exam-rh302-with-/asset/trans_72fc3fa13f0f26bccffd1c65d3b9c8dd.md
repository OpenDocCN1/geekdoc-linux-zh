
摘要 445

- 通用设置
- 即插即用支持
- 块设备
- 网络选项
- QoS 和/或公平队列
- SCSI 支持
- SCSI 低层驱动程序
- 网络设备支持
- 业余无线支持
- IrDA 子系统支持
- 红外端口设备驱动程序
- ISDN 子系统
- 旧版 CD-ROM 驱动程序
- 其他选项

# 关键术语

在进入下一章节之前，请确保你熟悉以下术语：

内核 (kernel)
额外版本代码 (extraversion code)

# 更多信息来源

如果你对本章介绍的主题有更多信息，应该咨询以下来源：

- 官方红帽 Linux 参考指南 (Official Red Hat Linux Reference Guide)

- Linux 内核存档，www.kernel.org。

- 内核源码树中的文档，特别是 `/usr/src/linux/Documentation` 下的文件

- Brian Ward 编写的 Linux 内核 HOWTO，`/usr/doc/HOWTO/Kernel1-HOWTO`（有些过时，但仍有价值）

Copyright © 2000 SYBEX, Inc., Alameda, CA www.sybex.com

Copyright © 2000 SYBEX, Inc., Alameda, CA www.sysex.com

5. 定义额外版本代码值的是以下哪一个？

- A. `/usr/src/linux/make`
- B. `/usr/src/linux/Make`
- C. `/usr/src/linux/makefile`
- D. `/usr/src/linux/Makefile`

6. 在安装新内核的典型命令中，以下哪个是必要的？

- A. `cp /usr/src/linux/.config /boot/config-2.4.5-1r1`
- B. `cp /usr/src/linux/arch/i386/boot/bzImage /boot/vmlinuz-2.4.5-1r1`
- C. `cp /usr/src/linux/System.map /boot/System.map-2.4.5-1r1`
- D. `make modules_install`

7. 为了创建一个新的启动盘，你应该执行以下哪个命令？

- A. `mkbootdisk -device /dev/fd0 -verbose 2.4.5`
- B. `mkbootdisk -device /dev/fd0 -verbose 2.4.5-10`
- C. `mkbootdisk /dev/fd0 -verbose 2.4.5`
- D. `mkbootdisk /dev/fd0 -verbose 2.4.5-10`

# 复习题答案

- 1. A. 内核配置存储在隐藏文件 `.config` 中。`config` 文件作为参数提供给 `scripts/Configure`。如果 `.config` 文件不存在，则由 `arch/i386/defconfig` 提供默认值。红帽 Linux 内核的默认配置在 configs 中。
- 2. A, C. `config` 和 `menuconfig` 都具有基于文本的用户界面。
- 3. A. 响应 `m` 将驱动程序或其他设施编译为可加载内核模块的支持。
- 4. C. 要配置内核运行作为路由器而不是主机，你应该启用 `IP: Optimize as Router, not Host` 选项。这会抑制主机通常需要但路由器不需要的默认支持。
- 5. D. 额外版本代码的值定义在 `/usr/src/linux/Makefile` 中。
- 6. B, C, D. 你必须安装内核、系统映射和模块，但不需要安装系统映射和配置。
- 7. B. 你必须包含 `-device` 参数。版本参数应该包含额外版本代码，以便命令能够找到正确的内核镜像。

# 第 19 章

# 管理共享库

本章涵盖的 RHCE 备习主题：

- 理解并能够修订加载器配置文件 `/etc/ld.so.conf`。

![](img/7a53ebe77601d422c9f5ede463_0.png)

![](img/7a53ebe77601d422c9f5ede64_0.png)

除了内核和模块，Linux 系统最重要的部分是动态加载器及其共享库。几乎每个程序在加载时都会使用加载器提供的一个或多个库。如果加载器配置错误，程序——即使是基本命令——也将运行。本章将解释共享库和加载器的配置程序。

# 共享库概念

C 语言是编写 Linux 程序最流行的语言。然而，程序员编写的 C 程序并没有准备好执行，因为计算机不处理 C 程序。计算机接受的机器语言模型与计算机的内部架构密切相关，因此通常与其他计算机接受的机器语言不兼容。对象代码类似于机器语言，但像源代码一样，它是不可执行的。因此，计算机程序在执行之前必须经过一系列转换。图 19.1

使用 Perl、Python 或 shell 等脚本语言编写的程序可以立即执行。这是脚本语言与编程语言的主要区别。

# 图 19.1 创建并运行程序

![](img/7a53ebe77601d422c9f5ede465_0.png)

程序员编写的程序形式被称为*源代码*。一个特殊程序*编译器*将源代码转换为*对象代码*的形式。对象代码类似于机器语言，但像源代码一样，它是不可执行的。程序员通常不需要编写代码来处理通用操作，例如计算字符串中的字符数；否则程序员将反复编写相同的代码。

Copyright © 2000 SYBEX, Inc., Alameda, CA www.syex.com

相反，通用操作被编写一次并组织为库。当程序员需要执行这些操作之一时，只需编写库的引用。这加速了编程过程并减少了编程错误。静态链接的可执行程序已就绪。

静态链接程序有几个缺点。例如，每个使用库例计算字符串字符数的可执行程序都包含执行此操作的机器指令。如果系统包含数千个使用几十或数百个库例的程序，冗余存储浪费大量的磁盘空间。此外，会在库例中发现错误：每个使用该程序的程序都包含错误代码。修复缺陷需要将使用错误的程序链接到修复的库。

通常，更好的方法是动态链接程序。动态链接程序不包含它引用的库例。相反，它包含了所需的库的存根。当动态链接程序加载时，特殊动态加载器解析程序的库引用。系统在虚拟内存中保留一份动态加载库；所有程序共享同一个拷贝。

动态链接程序节省磁盘空间，因为程序不包含库例的冗余拷贝。此外，修复缺陷只需替换对应的库：对该程序的任何后续引用将解析到该代码。动态链接程序的执行速度很慢，但差异是显著的。

# 共享库

Linux 可执行文件通常使用名为 ELF（执行和链接格式）的结构。然而，旧的可执行文件有时使用 out。这种不一致的一个复杂之处是系统库分别存在于 ELF 和 out 格式中。最终，对 out 的可能会消失。

Linux 链接器被称为 `/usr/bin/ld`。曾经，Linux 有针对 out 文件（`/lib/ld.so`）和 ELF 文件（`/lib/ld-linux.so-1`）的动态加载器。然而，Linux 现在使用单一动态加载器 `/lib/ld-version.so` 来支持两种文件格式。红帽 Linux 包含了新版本的动态加载器。

# 库的位置和文件名

Linux 共享库存储在几个目录中，例如：

- /lib，主共享库
- /usr/lib，辅助共享库
- /usr/i486-linux-libc5/lib，旧版 C 标准库 libc5 的共享库
- /usr/X11R6/lib，与 XFree86 相关的共享库
- /usr/i486-linuxaout/lib，out 共享库

静态库文件格式为 `libname.a`，其中 `libname` 是库的名称。动态库文件的命名方式特殊，旨在实现与共享库新版本的向上兼容。共享库的名称通常具有 `libname-major.minor.patch.so` 格式，其中：

- libname 是库的名称
- major 是库的主版本号
- minor 是库的次版本号
- patch 是库的补丁级别
- so 表示该文件是共享库

例如，标准 C 库可能位于名为 `libc-2.1.1.so` 的文件中。如果库刚刚发布，则可以省略补丁级别，文件名将具有 `libname-major.minor.so` 或 `libname-major.so` 格式。
除了库文件外，还有两个符号链接，它们指向库文件：

- libname.so
- libname.so.major
