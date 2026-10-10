
## pkginfo

用途：列出 Sun Solaris 系统上已安装的软件包。

用法语法：`pkginfo [OPTIONS] [PACKAGE]`

```
# pkginfo | more
system        BRCMbnx     Broadcom NetXtreme II Gigabit Ethernet
system        CAdP160     Adaptec Ultra60 SCSI Host Adapter Driver
system        HFPC        Agilent Fibre Channel HBA Driver
system        NCRor86r    NCR Platform Support, OS Functionality
system        NVDGraphics NVIDIA Graphics System Software
system        NVDGraphicsr NVIDIA Graphics System Device Driver
system        SK98sol     SysKonnect SK-NET Gigabit Ethernet Adapter
system        Skfp        SysKonnect PCI-FDDI Host Adapter
system        SUNW1251f   Russian 1251 fonts
system        SUNW1394    Sun IEEE1394 Framework
system        SUNW1394h   Sun IEEE1394 Framework Header Files
system        SUNWGl1b    GLIB - Library of useful routines for C
system        SUNWGtk     GTK - The GIMP Toolkit (Root)
system        SUNWGtiku   GTK - The GIMP Toolkit (Usr)
GNOME2        SUNWPython  The Python interpreter, libraries and
...      
```

列出 Solaris 系统上已安装的软件包

**pkginfo** 命令用于列出 Solaris 系统上已安装的软件包。不带任何选项执行 **pkginfo** 会列出所有已安装的软件包，如上例所示。指定软件包名称将显示该软件包的信息，如下例所示。

```
# pkginfo SUNWapch2r
system        SUNWapch2r Apache Web Server V2 (root)   
```

使用 pkginfo 显示特定软件包

常见用法示例：

- `pkginfo` | 列出所有已安装软件包
- `pkginfo [PACKAGE]` | 列出指定的软件包

## make

用途：从源代码编译并安装软件。

用法语法：`make [OPTIONS] [FILE]`

```
# ls -l Makefile
-rw-r-- 1 nick nick 1636 2007-08-10 13:48 Makefile
# make 66 make install

*** Stopping make sense ***
make[1]: Entering directory '/home/nick/Desctop/chkrootkit-0.48'
gcc -DHAVE_LASTLOG_H -o chklastlog chklastlog.c
chklastlog.c: In function 'main':
chklastlog.c:167: warning: format '%ld' expects type 'long int', but
option 3 has type 'int'
chklastlog.c:167: warning: format '%ld' expects type 'long int', but
option 4 has type 'uid_t'
gcc -DHAVE_LASTLOG_H -o chkxtmp chkxtmp.c
...
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_243_0.png)

`make` 命令用于从源代码编译和安装程序。与 `make` 命令兼容的源代码通常随一个名为 Makefile 的文件一起分发。Makefile 是一个脚本，用于使用 `make` 命令构建和安装源代码。

在上述示例中，将 `make` 和 `make install` 命令结合使用，以构建程序的源代码并将其安装。

> 大多数用户无需从源代码编译软件，因为主要发行版为几乎所有可用程序提供了预构建的软件包。此外，Linux 工具如 yum、apt 和 eme 极大地简化了软件安装和依赖项满足。

常见用法示例：

- **make** 编译源代码
- **make install** 安装编译后的源代码

## 第 15 节：系统管理实用工具

### 概述

本节介绍两个对商用 Unix 系统非常实用的系统管理工具：

- **SMIT：** AIX 的系统管理界面工具
- **SAM：** HP-UX 的系统管理管理器

SMIT 和 SAM 是菜单驱动的应用程序，可用于简化复杂的任务，如管理硬件、软件、用户/组等。虽然可以在命令行上执行 SMIT 或 SAM 中的每项任务，但在这些实用工具中执行相同任务通常要容易和快捷得多。它们还通过确保请求的任务以正确的参数执行，从而提供了一层额外的防错保护。

### 本节涵盖的命令：

| 命令 | 用途 |
|---|---|
| **sam** | HP-UX 系统管理管理器 |
| **smit** | AIX 系统管理界面工具 |

## sam

用途：HP-UX 系统的菜单驱动系统管理实用工具。

用法语法：sam

![](img/fa2f95b64a707c963dfa0445bd9281a7_245_0.png)

sam 是 HP-UX 系统的菜单驱动管理实用工具。它可用于管理 HP-UX 系统的各个方面。

上述示例显示了 sam 主菜单的屏幕截图。在 sam 中，使用方向键导航菜单，使用 Enter 键选择项目。按下 Tab 键可激活屏幕顶部的菜单栏，从而访问更多功能。

常见用法示例：  
sam 启动 HP-UX 系统管理管理器

## smit

用途：IBM AIX 系统的菜单驱动系统管理实用工具。

用法语法：smit

```
# smit

                      System Management.
Move cursor to desired item and press Enter.
[TOP]
Software Installation and Maintenance
Software License Management
Devices
System Storage Management (Physical & Logical Storage)
Security & Users
Communications Applications and Services
Workload Partition Administration
Print Spooling
Advanced Accounting
Problem Determination
Performance & Resource Scheduling
System Environments
Processes & Subsystems
Applications
Installation Assistant
[MORE...3]
F1=Help
F2=Refresh
F3=Cancel
F8=Image
F9=Shell
F10=Exit
Enter=Do
Screenshot of the IBM AIX System Management Interface Tool
```

smit 是 IBM AIX 系统的菜单驱动管理实用工具。它可用于管理 AIX 系统的各个方面。

上述示例显示了 smit 主菜单的屏幕截图。在 smit 中，使用方向键导航菜单，使用 Enter 键选择项目。功能键（即 F1、F2 等）在 smit 中提供额外选项，并定义在每个屏幕的底部。

常见用法示例：

- smit | 启动 AIX 系统管理界面工具

## 附录 A：
Bash 快捷键

在 www.dontfearthecommandline.com 下载并打印此列表

| 按键 | 功能 |
| :--- | :--- |
| CTRL + C | 终止当前程序 |
| CTRL + Z | 暂停当前程序 |
| CTRL + D | 退出当前 shell |
| Tab | 命令/文件自动补全 |
| Home | 移动到命令行开头 |
| End | 移动到命令行末尾 |
| CTRL + L | 清屏 |
| Backspace | 删除光标后的文本 |
| ALT + Backspace | 删除光标后的整个单词 |
| Delete | 删除光标前的文本 |
| CTRL + R | 搜索命令历史 |
| Up Arrow | 向后循环浏览命令历史 |
| Down Arrow | 向前循环浏览命令历史 |
| Left Arrow | 光标向左移动一个字符 |
| Right Arrow | 光标向右移动一个字符 |
| ALT + B | 光标向后移动一个单词 |
| ALT + F | 光标向前移动一个单词 |
| CTRL + U | 剪切光标前的所有文本 |
| CTRL + K | 剪切光标后的所有文本 |
| ALT + D | 剪切当前选定的单词 |
| CTRL + Y | 粘贴之前剪切的文本 |
| CTRL + _ (下划线) | 撤销在命令行上输入更改 |
| CTRL + T | 交换命令行上前两个字符 |
| ALT + T | 交换命令行上前两个单词 |
| ALT + L | 将单词转换为小写 |
| ALT + U | 将单词转换为大写 |

