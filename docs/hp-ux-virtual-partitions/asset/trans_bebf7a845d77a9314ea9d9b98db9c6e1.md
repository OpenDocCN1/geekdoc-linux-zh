
## 引导控制台处理器（BCH）与处理器相关代码（PDC）

`hpx` 实用程序负责加载 HP-UX 内核并将控制权交给内核。ISL（初始系统加载程序）可以运行 `hpx` 的“自动执行”文件，也可以交互地输入命令。在大多数情况下，你只需要自动启动系统；不过，我们将查看一些可以执行的 `hpx` 命令。这有时也称为次级系统加载器（SSL）。

我发现对于新的系统管理员来说，关于引导过程存在许多困惑。首先，随新系统提供的关于 HP 9000 引导的文档并不多。其次，如果对引导过程没有任何背景知识，很难确定系统在给定时间处于引导的哪个阶段。表 3-3 显示了一些系统状态以及你在系统启动时按大致的顺序可能看到的每个状态对应的提示符：

### 表 3-3 /sbin/set_parms 参数

| 系统引导状态 | 提示符 |
| --- | --- |
| 引导控制台处理器（BCH） | 主菜单：输入命令或菜单 > |
| *在引导开始后 10 秒内中断引导时可见。用于执行与 PDC 相关的工作。* | |
| 初始系统加载器（ISL） | ISL> ? |
| *在与 PDC 相关的工作之后可见。* | |
| hpx | 取决于系统状态而有所不同。 |
| *提示符各不相同。你通常在 ISL 提示符处输入 hpx 命令来启动。这有时也称为次级系统加载器（SSL）。* | |
| 监护服务处理器（GSP） | GSP> |
| *在键入 \*b（控制 b）以访问 GSP 时可见* | |

描述引导过程只有一种方式，那就是通过示例。在即将介绍的章节中，我们将涵盖一个硬件配置最简系统的引导过程。我选择硬件配置最简系统的引导过程，是为了避免陷入硬件相关的细节，而是专注于引导过程本身。启动这个简单系统所显示的信息将使我们能够专注于引导过程，而不是众多硬件组件。对于任何 HP 9000 系统，引导过程通常由基本相同的步骤组成，因此你可以将这些信息应用于你的系统。然而，你可能拥有一个包含更多组件的大型系统，它会生成更冗长的引导信息。

## 引导控制台处理器（BCH）与处理器相关代码（PDC）

如前所述，HP 9000 系统预装了称为处理器相关代码（PDC）的固件。在系统通电或处理器复位后，PDC 会运行自检操作并初始化处理器。PDC 还会识别控制台路径，以便提供消息并接受输入。PDC 随后将开始“自动启动”过程，除非你在提供的 10 秒间隔内中断该过程。如果你中断“自动启动”过程，你可以发出各种命令。

下面的示例展示了一个 L 类系统的引导过程以及我们在系统上接收到的与 PDC 相关的消息。你看到的第一组消息是各种自检相关的消息。处理器、内存、I/O 及其他组件会经历一系列测试。我在示例中省略了部分消息列表，凡见到三个省略号之处，是因为完整的测试结果列表过长，无法收录在本书中：

```
Value of TERM has been set to \"vt100\"
WARNING: YOU ARE SUPERUSER [11.00] (see /etc/issue)
Console Login: root
# reboot -h...checking for disk quotas
Shutdown at 27:41 [in 6 minutes] Xcard Co., All Rights Reserved.
(c)Copyright 1979, 1980, 1983, 1985-1993 The Regents of The Univ. of California
(c)(c)** FINAL System shutdown message from root@sp.serviceengines.com **
(c)Copyright 1986-1992 Sun Microsystems, Inc.
System going down IMMEDIATELY Massachusetts Institute of Technology
(c)Copyright 1989-1993 The Open Software Foundation, Inc.
System shutdown time has arrived\n Corp.
(c)Copyright 1990 Motorola, Inc.
(c)Copyright 1990, 1991, 1992 Cornell University
System shutdown time has arrived\n Corp.
(c)Copyright 1989-1991 The University of Maryland
Console reset done\n arnspie Mellon University
(c)Copyright 1991-1997 Mentat, Inc.
Boot device reset done\n ng Star Technologies, Inc.
(c)Copyright 1996 Progressive Systems, Inc.
(c)Copyright 1997 Isogon Corporation

System has halted
OK to turn off power or reset\n\n\n RIGHT
LEGEND
UNLESS *WAIT for UPR to turn off power* message was printed above do not
restrings as set forth in sub-paragraph (c)(i)(1)\n of the Rights in
V VIRTUAL PROM PANEL****\n\n\n****ee in OPARS 252:227-701.\nSystem BOOT detected
Leds: RUN ATTENTION FAILT REMOTE POWER
 ON FLASH OFF U.S
ON A, CA 94104 U.S
platform  62EF
processor   1C1IYS are as set
processor   1I42
test    1100
processor   1100
processor   1100
test    1100
processor   1100
processor   1100
test    1100
processor   1100
processor   1100
processor   1100
PDR     322F
PDR     3149
PDR     3165
platform  616A
processor   1146
processor   INIT   1701
processor   INIT   1701
.
.
.
processor   111C
processor   111D
processor   111D
processor   1111
processor   2111
processor   2111
processor   2112
processor   2112
processor   2113
processor cache test 2113
processor cache test 2121
processor cache test 2121

memory test 7IA4
memory test 7IA5
memory test 7IA5
memory test 7IA6
memory test 7IA6
memory config 7210
:/0 INIT 8701
1/0 test 8118
1/0 test 8118
1/0 INIT 8701
2/0 INIT 8701
1/0 INIT 8701
1/0 INIT 8701
2/0 INIT 8701
2/0 INIT 8701
1/0 INIT 8701
1/0 INIT 8701
memory config 7240
memory INIT 7702
memory config 7241
memory config 7243
memory config 7240
memory test 7JA1
memory test 7IA2

processor test 1120
processor slave rendezvous 1C40
processor test 1142
processor test 1138
platform test 612A
1/0 config 8238

> ******* EARLY BOOT VPF ******
> End of early boot detected
> ******************************

Firmware Version 39.46

DuPlex Console IO Dependent Code (IODC) revision 1

> (c) Copyright 1995-1998, Hewlett-Packard Company. All rights reserved

Processor Speed State CoProcessor State Cache Size
Number

0 440 Mhz Active Functional 512 KB 1 MB
3 440 Mhz Idle Functional 512 KB 1 MB

+   - Central Bus Speed (in Mhz) : 82
+   - Available Memory : 2097152 KB
+   - Good Memory Required : 11468 KB

+   - Primary boot path: 0/0/1/1.2
+   - Alternate boot path: 0/0/2/0.2
+   - Console path: 0/0/4/0.0
+   - Keyboard path: 0/0/4/0.0

Processor is booting from first available device.

To discontinue, press any key within 10 seconds.
```

“早期”引导完成后，我们会得到一份简明的系统摘要，包括我们系统上的固件版本，然后我们有机会选择从主路径自动启动，或者按任意键停止引导过程。在正常的系统操作中，你会选择自动启动；不过，在我们的情况下，我们将中断引导过程，以查看 PDC 中有哪些可用命令。当我们中断引导过程时，会出现以下菜单：

```
Boot terminated.

Main Menu

Command Description
Boot [PRI|ALT] [<path>] Boot from specified path
PATH [PRI|ALT] [<path>] Display or modify a path
SEARCH [Display|PL] [<path>] Search for boot devices

Configuration menu Displays or changes configurations
Information menu Displays system information
Service menu Display service commands

Display Redisplay the current menu
HELP [<menu>|<command>] Display help for menu or command
RESET Restart the system

Main Menu: Enter command or menu >
```

PDC 的接口被称为引导控制台处理器（BCH）。在我们的讨论中，我们发出的命令是 PDC 命令，而用于发出这些命令的接口是 BCH。这个菜单中的许多命令对系统管理员非常有帮助，但有时它们被忽视，因为它们属于操作系统之前的阶段，通常容易被忽略。

我们暂时跳过前三个命令，先通过输入 co 来查看配置菜单（Configuration menu）。配置（Configuration）中的大写 "CO" 意味着你可以仅输入 co 作为 configuration 的缩写：
