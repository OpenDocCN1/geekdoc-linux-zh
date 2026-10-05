

# 推荐阅读

让链接器使用特定版本的共享库所需的具体步骤因系统而异。在 Linux 系统下，你可以通过设置 `LD_LIBRARY_PATH` 环境变量，或者使用链接器的 `-R` 选项。

# 包装脚本

遗憾的是，库级别的兼容性只是故事的一半。工具之间直接相互调用是另一个冲突发生点。例如，假设工具 `foo` 频繁地使用名为 `bar` 的工具。如果你更新了 `bar` 的默认版本，你可能会发现 `foo` 突然停止工作了。在这种情况下，你可以得出结论：`foo` 依赖于 `bar` 的某些不再受支持（或至少不再是默认）的行为。

如果你的软件仓库支持多个版本（例如 `/tools/util/bar-1.0` 和 `/tools/util/bar-2.0`），你可以通过将原始版本的 `foo` 重命名为 `real` 并将其替换为包装脚本来解决这个问题：

```bash
#!/bin/sh
# 确保程序首先找到与其捆绑的任何文件
# 如果它没有使用显式路径的话。
PATH=/tools/util/bar-1.0/bin:$PATH
export PATH
exec /util/foo-1.0/bin/foo.real "$@"
```

现在，`foo` 将通过自定义的 `PATH` 环境变量启动，并会优先调用旧版本的 `bar` 而不是新。

包装器是一个强大的工具，不仅可以解决包依赖问题，还可以解决安全、架构或操作系统依赖性以及使用跟踪等问题。许多站点对所有的共享二进制文件进行了包装。

# 12.13 推荐阅读

- INTEL CORPORATION AND SYSTEMSOFT. Preboot Execution Environment (PXE) 规范, v2.1. 1999. pix.net/software/pxeboot/archive/pxespec.pdf

- PXELinux 问题. syslinux.zytor.com/wiki/index.php/PXELUX

- RODIN, JOSIP. Debian 新维护者指南. debian.org/doc/maint-guide. 该文档包含了关于 `.deb` 包的有用信息。

- SILVA, GUSTAV NORONHA. APT 入门. debian.org/doc/manuals/apt-howto

- HOHNEL, DIRK, AND FABIAN HERSCHEL. 使用 YaST 自动安装 Linux 系统. usgen.org/linux/659/full_packages/hohnedel/hohnedel_html

- STUCKELBERG, MARC VIELLUMIER, AND DAVID CLERC. Linux 远程启动微型指南：使用 Linux, DOS, Windows 95/98 和 Windows NT 配置远程启动工作站. 1999. tldp.org/HOWTO/Remote-Boot.html

- 红帽企业系统管理指南. redhat.com/docs

![](img/579efec8c67772f31ecf34844bbb71a2_461_0.png)

第 12 章

软件安装与管理

- WACHSMANN, ALF. 如何通过 PXE 和 Kickstart 安装红帽 Linux. stanford.edu/~alfw/PXE-Kickstart/PXE-Kickstart.html

- BURGESS, MARK. Cfeengine: 站点配置引擎. USENIX Computing Systems, 第 8 卷 第 3 期. 1995. cfeengine.org

- HP Ignite-UX 管理指南. docs.hp.com/en/5992-5309/5992-5309.pdf

- NIM 从 A 到 Z. www.redbooks.ibm.com/redbooks/pdfs/sg24296.pdf. 这是一详尽的网络安装指南。

- Solaris 高级安装指南. docs.sun.com/app/docs/doc/082-5740

# 12.14 练习题

- E12.1 概述 Kickstart、JumpStart 和 Ignite-UX 之间的差异。它们各自优缺点是什么？

- E12.2 从 subversion.tigris.org 安装 Subversion。设置 `svversion` 并创建一个仓库。你如何让该仓库在本地网络上的任何地方都可用，同时又保持合理的安全性？

- E12.3 审查你所在站地的软件组织方式。该系统具有可扩展性吗？易用吗？请讨论。

- E12.4 配置管理系统最重要的功能有哪些？在网络上分发分布式配置文件的安全影响是什么？

- E12.5 设置你选择的网络安装程序，并使用你的服务器安装一台新机器。概述执行此任务所需的所有步骤。遇到了哪些障碍？你所选择的安装程序存在哪些可扩展性问题？

# 13 驱动程序与内核

内核在抽象的层层编程接口之下隐藏了系统的硬件。它提供了许多用户和用户级程序认为理所当然的设施。例如，内核从低级硬件特性创建了以下所有概念：

- 进程（分时、受保护地址空间）
- 信号和信号量
- 虚拟内存（交换、分页、映射）
- 文件系统（文件、目录、命名空间）
- 通用输入输出（特殊硬件、键盘、鼠标、USB）
- 进程间通信（管道和网络连接）

内核包含了设备驱动程序，用于管理它们与特定硬件的交互；内核的其他部分在很大程度上与设备无关。内核与其设备驱动程序之间的关系类似于用户级程序与内核之间的关系。当进程向内核请求时，内核（更准确地说是驱动程序）会将此请求转换为设备指令。

![](img/579efec8c67772f31ecf34844bbb71a2_463_0.png)

第 13 章

# 驱动程序与内核

内核大部分用 C 语言编写，带有少量汇编语言来接口硬件。

Linux 和其他开源环境的优势之一是源代码可用，使得相对容易进行定制。在 Linux 早期，拥有这方面的技能是必要的，因为如果不调整内核，很难管理系统。

幸运的是，系统管理员不需要亲手写代码就能非常高效。事实上，此类活动应该留给内核开发者。管理员应该关注用户的整体需求。（这并非总是如此！）

# 13.1 内核适配

本书涵盖的所有 UNIX 平台都运行内核内核，整个操作系统运行在内核空间（为特权函数保留的内存区域）。在内核内核中，设备驱动程序、进程间通信、虚拟内存和调度等服务在同一个地址空间运行。这与微内核架构形成对比，在微内核架构中，许多此类服务运行在用户模式（即作为普通进程）。两种架构的优缺点多年来一直激烈争论，但大多数内核开发者都认为两者都有价值。
