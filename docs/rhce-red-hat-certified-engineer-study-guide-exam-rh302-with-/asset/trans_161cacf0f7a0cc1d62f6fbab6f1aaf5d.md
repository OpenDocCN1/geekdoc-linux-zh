
现在，请通过尝试练习 8.7 来测试你对 kickstart 安装的理解。

## 练习 8.7

## 执行 Kickstart 安装

执行 kickstart 安装，在另一台计算机上复制现有的 Linux 系统。

## 总结

在本章中，你学习了如何在某些特殊情况下安装 Red Hat Linux。涵盖的最重要主题包括：

- **笔记本电脑**在笔记本电脑上安装 Red Hat Linux 可能遇到特殊的兼容性问题。
- **多系统安装**：使用 LILO——或其他提供类似功能的引导加载程序——你可以配置系统启动多个操作系统。
- **特殊安装：PCMCIA 硬件**：你可以在从 PCMCIA 硬件启动的系统上安装 Red Hat Linux。
- **特殊安装：网络安装**：你可以从存储在 FTP、HTTP 或 NFS 服务器上的介质安装 Red Hat Linux。
- **特殊安装：Kickstart 安装**：你可以使用 `mkkickstart` 程序安装 Red Hat Linux，该程序让你自动化安装过程。

## 关键术语

在进入下一章之前，请确保你熟悉以下术语：

- 启动参数 (boot arguments)
- 引导加载程序 (boot loader)
- 启动提示符 (boot prompt)
- kickstart 安装 (kickstart installation)
- 多系统安装 (multi-boot installation)
- 网络安装 (network installation)
- 主引导加载程序 (primary boot loader)
- 次引导加载程序 (secondary boot loader)

## 更多信息来源

- 如果你想进一步了解关于本章介绍的主题的信息，应该咨询以下资源：
- /usr/doc/lilo-/ 下的 LILO 文档文件
- 官方 Red Hat Linux 安装指南
- 官方 Red Hat Linux 参考指南
- 《Red Hat Linux Kickstart HOWTO》
- 《Win95 + WinNT + Linux Multiboot Using LILO Mini-HOWTO》

## 复习题

- 1. 关于 Linux 笔记本电脑安装，以下哪些说法是正确的？
    - A. 配置音频很少不是问题。
    - B. 配置视频很少不是问题。
    - C. 给定的笔记本电脑所需的硬件配置可能与相同型号的笔记本电脑不同。
    - D. 笔记本安装通常比台式电脑安装更容易。
- 2. 关于多系统 Linux 安装，以下哪些说法是正确的？
    - A. Linux 可以与 Windows 95 和 Windows 98 共存。
    - B. Linux 可以与 Windows NT 共存。
    - C. 一次只有一个操作系统在运行。
    - D. 你必须将 Linux 引导程序 LILO 安装在 MBR 上。
- 3. 关于 Linux 引导程序，以下哪些说法是正确的？
    - A. 安装在分区的引导区时，LILO 作为次引导加载程序作用。
    - B. 安装在分区的引导区时，LILO 作为主引导加载程序作用。
    - C. 安装在 MBR 上时，LILO 作为次引导加载程序作用。
    - D. 安装在 MBR 上时，LILO 作为主引导加载程序作用。
- 4. 非 Linux 分区的 LILO 配置必须包含？
    - A. image 选项
    - B. label1 选项
    - C. other 选项
- 5. kickstart 指令表示什么？
    - A. LILO 第一阶段加载。
    - B. LILO 第二阶段加载。
    - C. LILO 第二阶段启动。
- 6. 以下哪个是 Windows 引导器的配置文件？
    - A. boot.ini
    - B. boot.nt
    - C. loader.ini
    - D. loader.boot
- 7. 你可以使用哪些服务进行网络安装？
    - A. FTP
    - B. HTTP
    - C. NFS
    - D. SMB
- 8. 服务器 DNS 允许什么？
    - A. 将主机名映射到 IP 号
    - B. 将 IP 号映射到主机名
    - C. 将 IP 地址映射到 DHCP 服务器
    - D. 将主机名映射到 DHCP 服务器
- 9. 关于该程序，以下哪些说法是正确的？
    - A. 它为运行的系统生成 kickstart 指令。
    - B. 程序由默认安装。
    - C. 它将脚本写入标准输出流。
    - D. 它生成的脚本应该被编辑。
- 10. 何何放置 shell 命令以便作为 kickstart 安装的一部分自动执行？
    - A. %packages 指令之后
    - B. %post 指令之后
    - C. 作为 shell 指令的参数
    - D. 在 ks.com 文件中
- 11. 如果 kickstart 指令中未指定信息会怎样？
    - A. 安装程序提示缺失的信息。
    - B. 安装程序异常终止。
    - C. 安装程序使用默认值。
    - D. 安装失败。
- 12. 在 LILO 提示符上输入什么可以启动从 DHCP 服务器获取 kickstart 文件的安装？
    - A. linux ks
    - B. linux ks=dhcp
    - C. linux ks=floppy

## 复习题答案

- 1. C
- 2. C
- 3. D
- 4. A
- 5. C
- 6. A
- 7. C
- 8. B
- 9. C
- 10. B
- 11. A
- 12. B

## 配置与管理

### 安装后配置选项

- 理解并实施安装选项的后期配置。
- 能够配置键盘。
- 能够配置鼠标。
- 能够设置系统时间。
- 能够配置音频。
- 能够配置运行级别 (runlevel)。
- 能够配置身份验证。
- 能够配置基础网络。

### 配置键盘

要配置系统键盘，执行命令 `kbdconfig`

将出现配置键盘界面（如图9.1所示）。要指定键盘类型，请突出列表中键盘并点击确定。

### 配置鼠标

要配置系统鼠标，执行命令 `mouseconfig`。该命令将启动配置鼠标界面（如图9.2所示）。

