
```
* * * Top of File * * *
/*********************/
/*  Sample PROFILE XEDIT  */
/*********************/

/* Set up function keys to do something useful */
'SET PF01 HELP MENU'    /* XEDIT help                */
'SET PF02 SOS LINEADD'  /* Add a line at cursor position */
'SET PF03 QUIT'         /* Quit XEDIT                */
'SET PF07 BACKWARD'     /* Scroll backward           */
'SET PF08 FORWARD'      /* Scroll forward            */
'SET PF09 ='            /* Re-execute last subcommand entered */
'SET PF10 RIGHT 10'     /* Scroll document to right 10 columns */
'SET PF11 LEFT 10'      /* Scroll document to left 10 columns */
'SET PF12 ?'            /* Retrieve last command issued. */

/* Set up colors */
'SET COLOR PREFIX BLUE'
'SET COLOR ARROW WHITE'
'SET COLOR FILEAREA GREEN'

/* Set up display of editing window */
'SET NUM ON'            /* Show line numbers         */
'SET CMDLINE BOTTOM'    /* Command line at bottom of screen */
'SET SCALE OFF'         /* No "scale" bar across window */
'SET NULLS ON'          /* Allows you to insert text in middle of a line */
'SET CASE M I'          /* Allows uppercase and lowercase characters */
'SET CURLINE ON 3'      /* Current line is always the 3rd visible line. */
'SET FULLREAD ON'       /* move cursor to any spot and char stays put */
'SET STAY ON'           /* stay at loc of last find vs bottom of file */
* * * End of File * * *
```

尝试配置文件的各种选项。例如，将文件保存到你的 `CMS` 系统中的 `PROFILE XEDIT A` 会使配置覆盖生效。先从一次添加一行开始，确定你想要什么。示例 2-25 中显示的配置可能无法满足你的 requirements, but it is presented to illustrate the customization available to `XEDIT` users.

> **z/OS 类比：** `ISPF EDIT` 配置文件的工作方式类似。

> **提示：** `XEDIT PROFILE` 允许您自定义 `XEDIT`，使其行为更类似于 `ISPF EDIT`，如果您愿意的话。`SYNONYM` 命令是一个很好的起点。参见 `z/VM: XEDIT 用户指南`，`SC24-6132` 手册。

### 使用 XEDIT 获取帮助

如果您忘记了如何使用子命令，或想查看此处未解释的子命令信息，请选择 `PF1`，该键设置为 `HELP MENU` 子命令。`PF1` 选项列出编辑器可用的所有子命令和宏。

如果 `PF1` 未显示 `XEDIT` 的帮助菜单，您可以手动输入命令 `HELP XEDIT MENU`。将光标移动到所需子命令并按 Enter。子命令说明会出现在窗口中，替换全屏文本处理 `HELP` 菜单。

要返回到上一个窗口，请选择 `PF3`。要退出 `HELP` 显示并在窗口中恢复您的文件，请按 `PF4`。

> **z/OS 类比：** 在 `ISPF` 编辑器中，在 `ISPF` 编辑器中使用 `PF1` 的工作方式类似，但不能直接用于编辑主命令或行命令。相反，它们以陈旧的方式组织在面板中呈现。

# 向 z/OS 系统程序员介绍 System z 上的 Linux

在本章中，我们概述了 Linux 的来源、现状以及发展趋势。我们还深入探讨了 System z 上的 Linux 及其带来的好处。

## 目标

完成本章后，您应该能够：

- 讨论 Linux 的基本概念
- 使用基本技能在 Linux 中导航
- 识别基本的 Linux 命令

![](img/b0a4b9056f819dccd4781a5105c92d45_110_0.png)

## 3.1 Linux 概述

本节概述了 Linux 以及它如何与 System z 交互。它查看了 System z 上 Linux 发行版的构成，并突出了 System z 发行版最受欢迎的企业级 Linux 版本的主要功能。

### 3.1.1 Linux 历史

从最简单的角度来说，Linux 是一个操作系统。它由赫尔辛基大学的学生林纳斯·托瓦兹于 1991 年开始开发（Linux 代表 Linus UNIX）。Linux 本身实际上只是内核；它实现了多任务和多用户功能，管理硬件，分配内存，并使应用程序能够运行。

多年来，Linux 操作系统已成为 PC 用户、企业服务器和用户的一个真实且可行的替代方案。Linux 提供了 UNIX 服务器或桌面的强大功能和灵活性。它还提供了一套实用程序、Internet 应用程序和功能齐全的桌面界面。

Linux 操作系统已成为强大的 Internet 和许多其他应用程序的服务器平台。Linux 能够从企业 Web、文件传输协议（FTP）、文件和打印机服务器，到广域信息服务器（WAIS）网站甚至企业数据库服务器运行，并具有实时集群或高性能计算集群。

Linux 是一个与 UNIX 系统类似的功能齐全的操作系统。它具有企业 UNIX 系统的许多标准功能。命令结构的 管理通过 `shell` 实现。

> **z/OS 类比：** 这个 `shell` 与 `ISPF shell`（`ishell`）非常相似。这也类似于 `z/OS TSO` 环境。

增强的图形环境和桌面也可用。

Linux 的结构组织在文件系统上，这些文件系统提供了处理数据和文件所需的接口和抽象。文件与磁盘硬件一起组织在目录中。每个目录可以包含任意数量的子目录，每个子目录包含文件。这与经典的 PC 和 UNIX 操作系统文件结构类似。Linux 支持大多数现有文件系统，要么通过内核内置支持，要么通过内核模块。

### 3.1.2 Linux 组件

Linux 有三个基本组件：

- **内核**
  这提供了低级系统控制和接口、程序和硬件设备管理，以及用户级的抽象层。
- **init**
  这通常是在内核加载到内存后执行的 main 程序。从 `init`，您可以在用户空间执行不同的运行级别，具有不同的特性。
- **应用程序**
  Linux 应用程序涵盖许多类别。随着越来越多的公司采用这项技术，列表不断扩展。通过为 Linux 编写应用程序，开发成本通常会降低，从而催生新项目并增加整体标题数量。在 Linux 存在的众多水平和垂直市场中，我们可以列出以下类别：办公生产力、Internet 相关、网络和系统管理、软件开发、视频制作、数据管理、会计和金融，以及出版。

Linux 具有与大型 UNIX 操作系统相同的多用户和多任务处理能力。它提供了您在标准 UNIX 系统上找到的相同级别的系统管理。用户可以同时运行多个程序；它具有用户空间和内核空间的单独级别。您可以为不同用户创建用户帐户，并定义他们对文件和系统组件的访问权限。安装新设备和网络连接和控制也作为 Linux 操作系统的标准功能提供。

### 3.1.3 System z 上的 Linux 发行版

目前，System z 的受支持 Linux 发行版可从两个主要 Linux 分销商获得：Novell 的 `SUSE Linux Enterprise Server`（`SLES`）和 `Red Hat Enterprise Linux`（`RHEL`）。每个 Linux 发行版都有其优缺点。
