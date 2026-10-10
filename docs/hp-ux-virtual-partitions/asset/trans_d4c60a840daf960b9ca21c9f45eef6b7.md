
## 初始系统加载

如前所述，初始系统加载器（ISL）在 PDC 之后运行。通常你只需从 ISL 运行“autoboot”序列，但是，你可以在 ISL 提示符下运行许多命令。

承接前面示例的进展，我们选择从设备 *p0* 进行 *BOOT*（启动），并与 IPL 进行交互，如下例所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_176_0.png)

```text
Main Menu: Enter command or menu > bo p0
Interact with IPL (Y, N, Or Cancel)? > Y

Booting ...
Boot TD Dependent Code (IGDC) revision 1

HARD Booted.

ISL Revision A.00.33 OCT 26, 1994

ISL> ?

HELP      Help Facility
LS        List ISL utilities
AUTOBOOT  Set or clear autoboot flag in stable storage
AUTORESEARCH
SET or clear autoresearch flag in stable storage
PRIMARYBOOT
Modify primary boot path in stable storage
ALTPATH   Modify alternate boot path in stable storage
CONSPATH  Modify system console path in stable storage
DISPLAY   Display boot and console paths in stable storage
LSBUTOPTL List contents of autoboot file
FASTSIZE  Sets or displays FASTSIZE
B00SUPPORT Boots the a800 Support Kernel from the boot device
700SUPPORT Boot the a700 Support Kernel from the boot device
READNV    Displays contents of one word of NVM
REBADRS   Displays contents of one word of stable storage
LSBATCH   List contents of batch file
BATCH     Execute commands in batch file
LREST     List contents of EST (Extended Self Test) file
EST       Execute commands in EST (Extended Self Test) file

Enter 'LS' to see a list of the ISL utilities.

ISL>
```

输入 *?* 会列出我们可以发出的 ISL 命令列表。发出 *DISPLAY* 命令会显示启动和控制台路径，而 *LS* 则列出可用的 ISL 实用程序，如下例所示：

```text
ISL> display
Fastsize value is 0000000F
Autoboot is ON (enabled)
Autosearch is ON (enabled)
Primary boot path is 0/0/1/1.2.0.0.0.0.0
Primary boot path is (hex) 0/0/1/1.2.0.0.0.0.0
Alternate boot path is 0/0/2/0.2.0.0.0.0.0
Alternate boot path is (hex) 0/0/2/0.2.0.0.0.0.0
System console path is 0/0/4/0.0.0.0.0.0
System console path is (hex) 0/0/4/0.0.0.0.0.0

ISL> ls
Utilities on this system are:

| filename | type   | start | size | created       |
| :------- | :----- | :---- | :--- | :------------ |
| ODE      | -12960 | 584   | 1216 | 00/01/23 15:45:48 |
| HPUX     | -12928 | 540   | 800  | 99/10/28 15:23:53 |

ISL>
```

DISPLAY 产生了我们基于前一节中由 PDC 产生的内容所预期的信息。LS 产生了两个可用的实用程序：ODE 和 HPUX。ODE 是离线诊断环境（Offline Diagnostics Environment）。以下示例展示了通过运行 ODE、查看可用命令的 HELP 命令以及列出 ODE 实用程序的 LS 来列出系统上可用的 ODE 实用程序：

```text
ISL> ode

Offline Diagnostic Environment

(C) Copyright Hewlett-Packard Co. 1993-2000
All Rights Reserved

HP shall not be liable for any damages resulting from the
use of this program.

TC  Version A.02.20
SysLib Version A.00.74
Loader Version A.00.52
Mapfile Version A.01.23
```

Type HELP for command information.

```text
ODE> help

ODE Help

Basic Commands

- HELP -- Prints detailed information to the screen, when "help <command>" or "help <var>" is typed
- LS -- List modules available on boot medium
- <Module Name> -- Load and initialize a module by typing its name
  (for more help, type "help module_name")
- MENU -- Launch ODE's ease-of-use interface
- RUN -- Run a module (after setting desired environment variables)
- Control-c (control-C) -- Abort an ODE command; pauses a module run
- RESUME -- Restart a paused module
- DISPLOG -- After running a module, display contents of a log
- EXIT -- Return to next higher level prompt

Environmental Variables

- SHOWSTATE -- Display the value of the following environment variables:
  - LOOP -- Run a test this many times
  - ERRPRINT [ON|OFF] -- Print low-level error messages to console
    (primarily for manufacturing use)
  - ERRNUM [ON|OFF] -- Print one-line, numbered errors to the console

Continue ([y]/n)? y

- ERRPAUSE [ON|OFF] -- Pause module upon error detection
- ERROR101 [ON|OFF] -- Print OMLE error messages; disable non-error and isolation message printing
- INFOPRINT [ON|OFF] -- Print informational messages to the console
- ISOPRINT [ON|OFF] -- Print fault isolation messages to the console
- ISOPAUSE [ON|OFF] -- Pause module when isolation message is generated
- LOGSIZE -- Set the size of a message log
- DEFAULT -- Reset environment variables to default state

ODE> ls

Modules on this boot media are:

| filename | type | size | created  | description                                |
| :------- | :--- | :--- | :------- | :------------------------------------------- |
| MAPPER2  | TM   | 126  | 05/01/21 | 64 bit version of the system mapping ut    |
| JOTEST2  | TM   | 88   | 05/01/21 | 64 bit version that runs ROM-based self    |
| PERFVER2 | TM   | 124  | 05/01/21 | 64 bit version that runs ROM-based self    |

ODE>
```

在此示例中，当我们运行 ODE 并发出 LS 时，示例末尾列出了三个实用程序。我总是在系统安装过程中加载 ODE，以协助诊断可能出现的系统硬件问题，HP CE（客户工程师）可能需要诊断此类问题。

接下来，我们将通过运行 HPUX 实用程序继续进行启动过程：

如前所述，*hpx* 实用程序管理 HP-UX 内核的加载，并将控制权交给内核。ISL 可以运行 hpxux 的“autoexecute”（自动执行）文件，也可以交互式地给出命令。在大多数情况下，你只需要自动启动系统。然而，在我们目前的示例中，为了查看 ISL 中的一些功能，我们决定与 ISL 进行交互。我们只需发出 HPUX 实用程序名称即可继续启动过程，如下例所示：

```text
ISL: hpxux
Boot:
 /disk/0/0/1/2.0.0.0.0.0/stand/vmunix
 7094272 + 849200 + 724128 sttext 0x241068

alloc_pdc_pages: Relocating PDC from 0xf00000000 to 0x7fab000.
gsata4: aycvc_addr = 0x0002000 for 1 pages
NOTICE: nfsa_link( ): File system was registered at index 4.
NOTICE: autofs_link( ): File system was registered at index 6.

    System Console is on the Built-In Serial Interface
    Entering cifs_init... 
    Initialization finished successfully.  slott is 8
    Logical volume 64, 0x3 configured as ROOT
    Logical volume 64, 0x4 configured as SWAP
    Logical volume 64, 0x2 configured as CDMP
    Swap device table: ( start + size given in 512-byte blocks)
    entry 0 - major is 64, minor is 0x2: start = 0, size = 2097152
    Starting the STREAMS daemons-phase 1
    Checking root file system:
    file system is clean - log replay is not required
    Root check done.
    Create SPCP device files
    Starting the STREAMS daemons-phase 2
    B3252B/9245X8 HP-UX (B.11.00) #1: Wed Nov  5 22:38:19 PST 1997

Memory information:
 physical page size = 4096 bytes, logical page size = 4096 bytes
 Physical: 2097152 Kbytes, lockable: 1574352 Kbytes, available: 18155496 Kbytes
```

```text
/sbin/ioinitrc:

/sbin/hcheckrc:
 Checking for LVM volume groups and Activating ( if any exist)
 Volume group `/dev/vg0' has been successfully changed.
 vxfs fsck: sanity check: root file system OK (mounted read/write)
 Checking file file systems
 /sbin/fsclean: /dev/vg00/lvol1 (mounted) OK
 NFS file systems are OK, non running fock
 Checking vxfs file systems
 /dev/vg00/lvol5
 vxfs fsck: sanity check: /dev/vg00/lvol5 OK
 /dev/vg00/lvol3
 vxfs fsck: sanity check: root file system OK (mounted read/write)
 /dev/vg00/lvol4
```

## HPUX 二级系统加载器 (hpx)

![](img/eff8b9287a5f38c5adf538f24aacf29e_179_0.png)

```text
vxfs fsck: sanity check: /dev/vg00/lvol4 OK
/dev/vg00/lvol5
vxfs fsck: sanity check: /dev/vg00/lvol5 OK
/dev/vg00/lvol6
vxfs fsck: sanity check: /dev/vg00/lvol6 OK
/dev/vg00/lvol7
vxfs fsck: sanity check: /dev/vg00/lvol7 OK
```

```text
(c)Copyright 1983-1997 Hewlett-Packard Co. All Rights Reserved.
(c)Copyright 1973, 1980, 1983, 1985-1997 The Regents of the Univ. of California
(c)Copyright 1984, 1984, 1986 Novell, Inc.
(c)Copyright 1986-1992 Sun Microsystems, Inc.
(c)Copyright 1985, 1996, 1998 Massachusetts Institute of Technology
(c)Copyright 1989-1993 The Open Software Foundation, Inc.
(c)Copyright 1986 Digital Equipment Corp.
(c)Copyright 1990 Motorola, Inc.
(c)Copyright 1990, 1991, 1992 Cornell University
(c)Copyright 1989-1991 The University of Maryland
(c)Copyright 1988 Carnegie Mellon University
(c)Copyright 1991-1997 Mentat, Inc.
(c)Copyright 1994 Morning Star Technologies, Inc.
(c)Copyright 1996 Progressive Systems, Inc.
(c)Copyright 1997 Isogon Corporation
```

RESTRICTED RIGHTS LEGEND
Use, duplication, or disclosure by the U.S. Government is subject to restrictions as set forth in sub-paragraph (c)(1)(ii) of the Rights in Technical Data and Computer Software clause in DFARS 252.227-7013.

Hewlett-Packard Company
3000 Hanover Street
Palo Alto, CA 94304 U.S.A.

Rights for non-DOD U.S. Government Departments and Agencies are as set forth in FAR 52.227-19-(1)(1,2).

Console Login:

我在 *Console Login:* 提示符前出现三个地方的地方对清单进行了缩写。

我们可以使用 *HPX* 实用程序发出许多选项。本章末尾的手册页详细描述了几个选项。表 3-5 列出了一些常见 *HPX* 实用程序启动选项的示例，其中一些来自 man 手册页：

![](img/eff8b9287a5f38c5adf538f24aacf29e_180_0.png)

hpx - 3

