
## 内核调优：内核运行时参数

可以通过不重新编译和安装新内核或模块的方式开启或关闭若干内核功能，例如 IP 转发或最大文件数。这些可调参数由 /proc/sys 目录中的文件控制。第 30 章中描述了 proc 文件系统。您可以使用 redhat-config-proc 工具为这些参数赋值。redhat-config-proc 可从“更多系统工具”菜单中的“内核调优”访问。redhat-config-proc 列出了网络、文件系统、虚拟内存、内核和硬件等标题。网络选项允许您控制 IP 转发、ICMP 广播消息和 TCP 时间戳等功能。文件系统选项允许您设置最大文件数。内核选项允许您控制日志记录、共享内存以及禁用调试等某些安全功能。硬件选项允许您控制 RAID 速度。

您设置的参数会保存在 /etc/sysctl.conf 文件中。Red Hat 安装此文件时带有基本配置条目，例如 IP 转发和调试控制的条目。redhat-config-proc 工具会覆盖此文件，用为不同 /proc/sys 文件赋值的条目替换它。只有在您点击“激活已保存的配置”按钮后，对 /proc/sys 文件的更改才会生效。例如，如果您在网络 IP 面板中打开 IP 转发，一旦您保存并激活 proc 值，/proc/sys/net/ipv4/ip_forward 的内容就会设置为 1。

除了使用 redhat-config-proc，您还可以直接使用 sysctl 命令。-p 选项使 sysctl 从 /etc/sysctl.conf 文件（您也可以指定其他文件）读取参数。您可以使用 -w 选项更改特定参数。通过其键引用参数。键是由其 proc 系统类别（目录）前缀加参数名称组成的，例如 /proc/sys/net/ipv4/ 中的 ip_forward 参数对应的键为 net.ipv4.ip_forward。要显示特定参数的值，只需使用其键即可。-a 选项列出所有可用的可更改参数。在下一个示例中，用户更改了域名参数，通过 kernel.domainname 键引用它（domainname 命令也会设置 kernel.domainname 参数）：

```
# sysctl -w kernel.domainname="mytrek.com"
```

以下示例用于打开 IP 转发：

```
# sysctl -w net.ipv4.ip_forward=1
```

如果仅使用键，将显示该参数的当前值：

```
# sysctl net.ipv4.ip_forward
net.ipv4.ip_forward = 1
```

## 安装新内核版本

要安装新内核，您需要将该内核的软件包下载到您的系统上。您可以通过从发行版的网站下载二进制版本并安装它，或者下载源代码、编译内核，然后安装生成的二进制文件及其模块来安装新内核。对于 Red Hat，内核的二进制版本以 RPM 软件包形式提供。您可以像安装任何其他 RPM 软件包一样安装新内核。

在 Red Hat 上安装新内核最简单的方法是使用 Red Hat Network 更新代理（Red Hat Network 现在是一项需要付费的订阅服务）。更新代理会自动下载、更新并安装新内核。Red Hat Network 不会自动选择内核文件进行下载。尽管列表中有所显示，您必须明确选择它们才能下载和安装。

如果您想手动直接从 Red Hat 下载内核 RPM 软件包，请记住，完整的内核安装通常包含一系列 RPM 软件包，所有这些软件包都以“kernel”一词开头。还有一些您可能需要的其他软件包，它们包含新内核使用的更新系统配置文件。您可以使用系统中已安装的软件包作为参考。使用带有 -qa 选项的 rpm 命令列出所有软件包，然后通过 grep 命令加上 kernel 模式过滤，仅显示内核软件包：

```
rpm -qa | grep kernel
```

源代码版本可从发行版 FTP 站点下载，并包含在发行版 CD-ROM 中。您也可以直接从 www.kernel.org 下载最新源代码。无论您从哪里下载内核版本，它们总是相同的。从发行版站点下载的特定内核版本的源代码与从 www.kernel.org 下载的相同。该版本的补丁可应用于任何发行版。

### Red Hat 内核软件包

作为示例，此处列出了 Red Hat 的内核软件包。您应只安装 kernel-version-i386 和 athlon 软件包中的一个。这对于标准单处理器计算机就足够了。其他软件包是优化、支持或配置软件包，可能需要根据您 PC 的硬件配置进行安装，特别是针对多处理器机器、笔记本电脑以及内存大于 4GB 的计算机。名称中包含 nptl，表明该版本内核支持原生 POSIX 线程库（NPTL），提供更高效的进程控制，从而改进性能和处理器可扩展性。

```
kernel-2.4.22-1.2115.nptl.athlon.rpm
kernel-2.4.22-1.2115.nptl.i586.rpm
kernel-2.4.22-1.2115.nptl.i686.rpm
kernel-doc-2.4.22-1.2115.nptl.i386.rpm
kernel-bigmem-2.4.22-1.2115.nptl.i686.rpm
kernel-pcmcia-cs-3.1.31-13.i386.rpm
kernel-smp-2.4.22-1.2115.nptl.i686.rpm
kernel-smp-2.4.22-1.2115.nptl.athlon.rpm
kernel-utils-2.4.9-1.101.fedora.i386.rpm
kernel-source-2.4.22-1.2115.nptl.i386.rpm
kernel-BOOT-2.4.22-1.2115.nptl.i686.rpm
```

### CPU 内核软件包

Red Hat 提供了针对不同流行 CPU 优化的不同内核软件包。请选择适合您机器的软件包。每个软件包都命名为 kernel，但每个都有不同的限定符。Red Hat 包含三种不同的内核软件包：一种用于 Athlon 和 Duron CPU，一种用于 Pentium 2、3 和 4 CPU，另一种用于较旧的 Pentium、AMD K6 CPU 和其他旧系统。每个软件包的文件名中都会有 CPU 引用：Athlon 和 Duron 使用 athlon，Pentium 2、3 和 4 使用 686，Pentium、K6 和其他系统使用 586。

```
kernel-2.4.22-1.2115.nptl.athlon.rpm
kernel-2.4.22-1.2115.nptl.i586.rpm
kernel-2.4.22-1.2115.nptl.i686.rpm
```

此外，如果您正在笔记本电脑上使用或安装使用 PCMCIA 卡的系统，您还需要安装 pcmcia-cs 软件包。

```
kernel-pcmcia-cs-3.1.31-13.i386.rpm
```

如果您的计算机拥有超过 4GB 的 RAM 内存，您还需要安装 bigmem 软件包。

```
kernel-bigmem-2.4.22-1.2115.nptl.i686.rpm
```

如果您的系统支持多个 CPU 处理器，您还需要安装 smp 软件包以代替标准 cpu 软件包。Red Hat 为 Athlon 和 Pentium 计算机提供软件包。

```
kernel-smp-2.4.22-1.2115.nptl.i686.rpm
kernel-smp-2.4.22-1.2115.nptl.athlon.rpm
```

### 提示

kernel-BOOT 软件包是 kernel 的较小版本，仅用于软盘安装。

### 支持软件包

此外，如果您计划自定义内核，应下载 source 软件包。doc 软件包提供更新的文档。utils 软件包包含各种硬件监控工具，如用于硬盘的 smartctl，以及用户模式 Linux（UML）工具。

```
kernel-utils-2.4.8-31.1386.rpm
kernel-source-2.4.22-1.2115.nptl.i386.rpm
kernel-doc-2.4.22-1.2115.nptl i386.rpm
```

### 安装内核软件包：/boot

您可能不需要所有这些软件包。例如，对于基本 Pentium 计算机（内存小于 4GB 的单处理器 Pentium 3 或 4，且无自定义设置）的简单内核升级，您只需要 686 软件包。对于 Athlon 或 Duron 系统，您应使用 athlon 软件包。对于更完整的升级，您应包含 pcmcia、source、doc 和 utils 软件包。如果您的系统支持多处理器，您应使用 smp 软件包。

为了确保内核 RPM 软件包没有错误地下载并验证其身份，您可以使用带有 -K 选项的 rpm 命令（要验证软件包身份，您需要 Red Hat 公钥）：

```
rpm -K *rpm
```

现在您可以安装内核了。作为一种安全措施，您应保留旧内核，以防新内核因某些原因无法正常工作。这涉及使用安装（-i）选项而不是更新（-U）选项进行安装，为新内核创建单独的 RAM 磁盘，然后修改 grub.conf 使 GRUB 使用新内核启动。

```
# rpm -ivh kernel-2.4.22-1.2115.nptl.i686.rpm
```

如果您的系统有 SCSI 控制器或其他专用硬件，RPM 也会创建 RAM 磁盘以保存相应的支持模块（您可以使用 mkinitrd 命令手动创建 RAM 磁盘）。该 RAM 磁盘名为 initrd-kernel-version.img，位于 /boot 目录中，例如 /boot/initrd-2.4.22-1.img。

