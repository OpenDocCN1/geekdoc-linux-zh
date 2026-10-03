
## 应用你的知识

20. 如果系统无响应，你会输入什么键组合来中断系统？
A. Ctrl+B
B. Ctrl+C
C. Stop+A
D. Ctrl+Alt+Delete
E. Ctrl+Break

21. ufsboot 程序做什么？
A. 从默认启动设备加载 bootblock
B. 加载内核
C. 查找并执行次要启动程序
D. 运行自检诊断（POST）以验证系统的硬件和内存

22. OpenBoot PROM 中设置的 auto-boot? 参数的功能是什么？
A. 上电或复位后自动启动
B. 设置默认启动设备
C. 看门狗复位后重启
D. 当生成系统核心文件时自动执行系统重启

23. 以下哪个命令用于设置 auto-boot 参数？
A. setenv auto-boot?=false
B. set auto-boot=false
C. eeprom auto-boot?=false
D. nvset

24. 要显示所有 OpenBoot 参数设置，例如 boot-device 和 ttya-mode，应该输入什么？
A. nvalias
B. devalias
C. printenv
D. show all

25. 要检查连接到所有 SCSI 控制器的所有 SCSI 设备上的目标 ID，应该输入什么？
A. test-all
B. probe-scsi
C. probe-scsi-all
D. test-scsi

26. 内核在加载时读取以下哪个文件？（系统配置信息存储在其中。）
A. /etc/system
B. /platform/<arch>/kernel/unix
C. /etc/inittab
D. /kernel/unix

## 复习问题的答案

1. A. 在操作系统启动之前看到的硬件级用户界面称为 OpenBoot PROM（OBP）。

2. C. NVRAM 是存储系统识别信息的地方，例如 hostid、Ethernet 地址和时间（TOD）时钟。

## 应用你的知识

3. A, B. OpenBoot 固件的两个主要任务是运行 POST 并加载 boot-block。

4. B. OpenBoot 运行 POST 以初始化系统硬件。它还从默认启动设备加载主启动程序 bootblk。bootblk 程序查找并执行次要启动程序 ufsboot，并将其加载到内存中。从那时起，ufsboot 程序加载操作系统内核。

5. D. 称为节点的设备通过设备树上互连总线的层次结构连接到主机计算机。代表主机计算机主物理地址总线的节点构成树的根节点。

6. A. 完整的设备路径名是一系列由斜杠（/）分隔的节点名称。树的根是机器节点，它没有明确命名，但由前导斜杠（/）表示。每个设备路径名具有以下形式：
`driver-name@unit-address:device-arguments`

7. A. OpenBoot 命令 show-devs 用于获取设备信息并显示设备路径名。

8. D. 使用 devalias 命令按如下方式创建名为 disk3 的临时设备别名：
`devalias disk3 /iommu/sbus/espdma@f,400000/esp@f,800000/sd@3,0`

9. B. 使用 OpenBoot PROM 中的 nvalias 命令或 Unix 提示符中的 eeprom 命令在 NVRAM 中创建永久别名，即使在重新启动后仍然有效。

10. A. 名称为 boot-device 的 NVRAM 变量包含默认启动设备的名称。

11. C. 使用以下命令之一修改 NVRAM 参数：setenv、set-default 或 set-defaults。

12. B. 要将 NVRAM 变量重置为其默认设置，请在机器启动时同时按住 Stop+N 键。

13. B. OpenBoot 命令 security-mode 限制用户在 OpenBoot 提示符下允许执行的操作集。

14. C. OpenBoot 命令 test-all 测试指定设备树节点下具有内置自检方法的全部设备。

15. D. 使用 -a 选项发出 OpenBoot boot 命令，以便提示输入要加载的独立程序的名称。

16. A. bootblk 位于启动设备的 1–15 块中。

17. A. 次要启动程序 ufsboot 加载操作系统内核。

18. D. 使用 sysdef 命令列出所有硬件设备、系统设备、可加载模块以及所选内核可调参数的值。

19. D. 物理设备名称存储在 /devices 目录中。

20. C. 通过同时按下 Stop+A 键（Stop+A）中断无响应的系统。

21. B. ufsboot 程序加载操作系统内核。

## 应用你的知识

22. A. auto-boot? 控制系统在系统复位后或上电时是否自动启动。此变量的默认值是 true。当系统上电时，系统会自动启动到默认运行级别。

23. C. eeprom auto-boot?=false 用于设置 auto-boot? 参数。

24. C. 在 OpenBoot 提示符下，使用 printenv 命令显示所有 OpenBoot 参数设置。

25. C. 使用 probe-scsi-all 命令检查连接到所有 SCSI 控制器的所有 SCSI 设备上的目标 ID。

26. A. 内核加载时，它读取存储系统配置信息的文件 /etc/system。该文件修改内核的参数和对可加载模块的处理。

## 目标

本章描述了系统管理员必须遵循的步骤，以在网络独立系统上安装 Solaris 8 操作系统。这些步骤包括以下内容：

## 准备安装 Solaris 8 软件

安装操作系统时，系统会提示您提供一份项目清单。在开始安装之前，收集这些信息非常重要。

## 验证 Solaris 8 软件的最低系统要求

要在系统上安装和运行 Solaris 8，您必须验证硬件是否满足最低要求。

## 了解 Solaris 软件术语

要理解安装程序将呈现的对话框，您需要了解 Sun 的术语以及它如何捆绑其软件模块。

## 选择要安装的系统配置

您需要选择要安装的系统配置类型。本章将描述每种可用的配置类型。

## 了解磁盘存储系统和分区

在安装过程中，您需要设置磁盘和磁盘分区。为了正确设置，您首先需要了解磁盘存储和分区的概念。然后您需要考虑希望如何将数据存储在系统的磁盘上。

## 第 3 章

## 安装 Solaris 8 软件

## 了解设备驱动程序

设备驱动程序控制连接到系统的每个设备，有些设备使用多个设备驱动程序。在安装操作系统之前，您必须验证所有设备是否已连接并正常运行。本章解释设备驱动程序，以便您可以识别和验证连接到系统的所有设备。

## 了解安装 Solaris 8 软件的方法

本章确定了可用于安装操作系统的五种方法。它们被描述出来，以便您可以确定哪种方法最适合您的安装。

## 安装 Solaris 8

本章概述了安装操作系统的过程。

## 引言 102

## 安装 Solaris 8 软件的要求和准备 102

不受支持的 Sun4c 架构 104

最低系统要求 105

## 软件术语 105

软件包 105

软件集群和配置集群 106

Solaris 媒体 107

要安装的系统配置 108

## 磁盘存储系统 112

规划分区大小的基本考虑 115

多磁盘上的分区安排 116

## 设备驱动程序 117

物理设备名称 117

实例名称 118

逻辑设备名称 118

块和字符设备文件 120

## 安装 Solaris 8 软件的方法 121

交互式 121

JumpStart 121

自定义 JumpStart 122

Web Start 122

通过网络安装 123

Solaris 安装过程 123

## 摘要 126

## 应用你的知识 127

以下策略将帮助您为考试做准备：

- 了解用于安装操作系统的每一种方法。主要需要知道每种方法之间的区别，以及何时在何处使用每种方法。
- 了解安装 Solaris 8 操作环境的所有要求。
- 了解本章描述的所有术语和概念，以及本章末尾列出的术语。每个术语和概念很可能出现在考试中。
- 了解我在“磁盘存储系统”部分描述的所有内容。了解各种设备驱动程序和各种设备名称。确保您了解与磁盘分区相关的问题。
- 最后，练习本章介绍的所有命令，直到您可以从记忆中执行它们并描述它们。此外，在 Sun 或 Intel 系统上练习安装 Solaris 8 操作环境不少于三次，或直到您可以从记忆中执行所有任务。
