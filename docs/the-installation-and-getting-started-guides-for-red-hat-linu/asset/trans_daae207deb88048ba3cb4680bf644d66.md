

# 安装和入门指南
for Red Hat® Linux® 6.0

![](img/46f4935125ba89e12897afbe9d77a097_0_0.png)

![](img/46f4935125ba89e12897afbe9d77a097_0_1.png)

LINUX RESOURCE SERIES

# 安装
and
入门指南
for
Red Hat Linux 6.0

Copyright © 1999 Linux Press

# 第一版
首次印刷 1999

Red Hat 是注册商标，Red Hat Shadow Man 标志、RPM、RPM 标志和 Glint 是 Red Hat Software, Inc. 的商标。

Linux 是 Linus Torvalds 的注册商标。

Motif 和 UNIX 是 The Open Group 的注册商标。

Alpha 是 Digital Equipment Corporation 的商标。

SPARC 是 SPARC International, Inc. 的注册商标。带有 SPARC 商标的产品基于 Sun Microsystems, Inc. 开发的架构。

Netscape 是 Netscape Communications Corporation 在美国和其他国家/地区的注册商标。

Windows 是 Microsoft Corporation 的注册商标。

所有其他提及的商标和版权均为其各自所有者的财产。

Linux Press
P.O. Box 220
Penngrove, CA 94951

- Phone: (707) 773-4916
- Fax: (707) 765-1431
- Web: http://www.linuxpress.com
- E-mail: sales@linuxpress.com

在准备本书时已采取一切预防措施，但出版商不对错误或遗漏，或因使用其中所含信息而造成的损害承担责任。

《Red Hat Linux 6.0 安装和入门指南》可在任何物理或电子媒介中整体或部分复制和分发，只要所有副本上均保留此版权声明且保持不变。商业再分发是允许的，并且鼓励这样做，但您不得在比您收到时更严格的条款下整体或部分再分发它。

国际标准书号：0-9659575-3-5

Printed in Canada

## Linux Press
致谢

Copy Editor Dale Scheetz

Proofreading Les Villanyi

Cover Art Folio Creative Services
of Glen Ellen, California

# 安装指南
for
Red Hat Linux 6.0

Copyright © 1999 Red Hat Software, Inc.

Red Hat 是注册商标，Red Hat Shadow Man 标志、RPM、RPM 标志和 Glint 是 Red Hat Software, Inc. 的商标。

Linux 是 Linus Torvalds 的注册商标。

Motif 和 UNIX 是 The Open Group 的注册商标。

Alpha 是 Digital Equipment Corporation 的商标。

SPARC 是 SPARC International, Inc. 的注册商标。带有 SPARC 商标的产品基于 Sun Microsystems, Inc. 开发的架构。

Netscape 是 Netscape Communications Corporation 在美国和其他国家/地区的注册商标。

Windows 是 Microsoft Corporation 的注册商标。

所有其他提及的商标和版权均为其各自所有者的财产。

Red Hat Software, Inc.
2600 Meridian Parkway
Durham, NC 27713
P. O. Box 13588
Research Triangle Park, NC 27709
(919) 547-0012
redhat@redhat.com
http://www.redhat.com

在准备本书时已采取一切预防措施，但出版商不对错误或遗漏，或因使用其中所含信息而造成的损害承担责任。

《官方 Red Hat Linux 安装指南》可在任何物理或电子媒介中整体或部分复制和分发，只要所有副本上均保留此版权声明且保持不变。商业再分发是允许的，并且鼓励这样做，但您不得在比您收到时更严格的条款下整体或部分再分发它。

# 目录

- Preface ........................................................... 19
- What is Linux? ........................................................... 19
- What is Red Hat Linux? ................................................... 20
- An Overview of This Manual ............................................... 21
- Quick Start Information ................................................. 22
- Upgrading from a Prior Version of Red Hat Linux .......................... 23
- A Word From the Developers ............................................... 23
- Notes from the Editor .................................................... 23
- I Couldn't Have Done it Without........................................... 24
- 1 New Features of Red Hat Linux 6.0........................................... 27
- Installation-Related Enhancements ....................................... 27
- New HTTP Installation Method ............................................ 27
- 'Out-of-the-Box' Processor Optimized Kernel Support ...................... 27
- New Boot Disks .......................................................... 28
- Improved Package Selection Screen ...................................... 28
- New Authentication Configuration Screen ............................... 28
- Xconfigurator Now Part of the Install ................................... 29
- Desktop and Window Managers ............................................. 29
- GNOME with Enlightenment Included ...................................... 29
- KDE Included ........................................................... 29
- Miscellaneous New Features .............................................. 30
- Enhanced Font Support .................................................. 30
- Enhanced Init scripts .................................................. 30
- Switchdesk Feature ..................................................... 30
- Latest Stable 2.2 Kernel Included ....................................... 30
- 2 Before You Begin ......................................................... 31
- Getting Documentation ................................................... 31
- The Red Hat Linux 6.0 Components ....................................... 32
- Installation Guide ...................................................... 32
- Red Hat Linux Getting Started Guide .................................... 32
- CDs 1 and 2 ............................................................. 33
- Boot Diskette .......................................................... 33
- Checking for Updated Diskette Images ................................... 33
- Things You Should Know .................................................. 34
- Basic Hardware Configuration ........................................... 34
- Learning About Your Hardware With Windows® .............................. 35
- Video Configuration .................................................... 38
- Network-related Information ............................................ 38

