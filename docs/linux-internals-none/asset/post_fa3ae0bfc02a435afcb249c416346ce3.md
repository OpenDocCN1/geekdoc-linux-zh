
# Linux Internals

Preface by
**Ingo Molnar,**
Red Hat Kernel Development Group

![](img/a248b1088891f07ca198e09ddb71aec7_0_0.png)

- Covers new Linux Kernel Version 2.4
- Detailed coverage of Linux file systems
- In-depth look at Linux system calls

![](img/a248b1088891f07ca198e09ddb71aec7_0_1.png)

**Moshe Bar,**
Linux columnist, *Byte.com*

# Linux Internals

**Moshe Bar**

McGraw-Hill
New York San Francisco Washington, D.C.
Auckland Bogotá Caracas Lisbon London Madrid
Mexico City Milan Montreal New Delhi San Juan
Singapore Sydney Tokyo Toronto

![](img/a248b1088891f07ca198e09ddb71aec7_3_0.png)

Copyright © 2000 by The McGraw-Hill Companies, Inc. All rights reserved. Printed in the United States of America. Except as permitted under the United States Copyright Act of 1976, no part of this publication may be reproduced or distributed in any form or by any means, or stored in a data base or retrieval system, without the prior written permission of the publisher.

1 2 3 4 5 6 7 8 9 0 DOC/DOC 0 5 4 3 2 1 0

P/N 0-07-212596-9

Part of ISBN 0-07-212598-5

The sponsoring editor for this book was Michael Sprague and the production manager was Clare Stanley. It was set in New Century Schoolbook by Patricia Wallenburg.

Printed and bound by R.R. Donnelley & Sons.

Throughout this book, trademarked names are used. Rather than put a trademark symbol after every occurrence of a trademarked name, we use names in an editorial fashion only, and to the benefit of the trademark owner, with no intention of infringement of the trademark. Where such designations appear in this book, they have been printed with initial caps.

Information contained in this work has been obtained by The McGraw-Hill Companies, Inc. ("McGraw-Hill") from sources believed to be reliable. However, neither McGraw-Hill nor its authors guarantee the accuracy or completeness of any information published herein and neither McGraw-Hill nor its authors shall be responsible for any errors, omissions, or damages arising out of use of this information. This work is published with the understanding that McGraw-Hill and its authors are supplying information but are not attempting to render engineering or other professional services. If such services are required, the assistance of an appropriate professional should be sought.

This book is printed on recycled, acid-free paper containing a minimum of 50% recycled, de-inked fiber.

To Yehoshua

May God bless you and give you peace.

![](img/a248b1088891f07ca198e09ddb71aec7_5_0.png)

Digitized by the Internet Archive
in 2018 with funding from
Kahle/Austin Foundation

https://archive.org/details/linuxinternals0000barm

## Contents

- Preface ....... xi
- Introduction ....... xiii
  - The Linux Kernel ....... xiii
  - Who Should Read This Book ....... xiii
  - What You Should Know Before Reading This Book ....... xiv
  - What This Book Contains ....... xiv
  - Where to Find More Information ....... xv
  - Suggestions, Comments ....... xv
- Acknowledgments ....... xvi
- 1 Open Source—Implications for a Modern Operating System ....... 1
  - History of Linux ....... 3
  - Linux Functionality ....... 5
  - Novelties in the 2.4 Kernel ....... 5
- 2 Compiling a Kernel ....... 9
  - Source Code Tree Structure ....... 10
    - The arch/ Directory ....... 14
    - The drivers/ Directory ....... 15
    - The fs/ Directory ....... 15
    - The include/ Directory ....... 15
    - The ipc/ Directory ....... 15
    - The init/ Directory ....... 15
    - The lib/ Directory ....... 16
    - The kernel/ Directory ....... 16
    - The mm/ Directory ....... 16
    - The net/ Directory ....... 17
  - Compiling It ....... 17
  - The GNU gcc Compiler ....... 19
  - Coding Conventions ....... 19
  - Architecture Dependencies ....... 20

## 3 Linux Kernel Base Functions ....... 21

- What's an OS Anyway? ....... 22
- Resource Management ....... 23
- CPU Management ....... 23
- Memory Load Latency ....... 24
- Caches ....... 28
- Branch Prediction ....... 28
- Software Issues ....... 29
- Spinlocks (Mutexes) ....... 30
- Data Structures—linux/smp.h ....... 33
- Data Structures linux/smp_lock.h ....... 34
- Device Handling ....... 35
- Block Device Handling ....... 36
- Components of Disk Access Time:
  - The Path of a Disk I/O Operation ....... 36
  - Mechanical Disk Operations ....... 37
  - RAID Comes to the Rescue ....... 37
- Character Device Handling ....... 38
- DMA Operation ....... 38
- DMA Addressing Limitations ....... 39
- Types of DMA Mapping ....... 40
- Using Consistent DMA Mappings ....... 40
- DMA Direction ....... 41
- Using Streaming DMA Mappings ....... 42
- Interrupts Handling ....... 45
- Data Structure—linux/interrupt.h ....... 50
- Linux Time-Keeping Functions ....... 51
- System Clock ....... 53
- Data Structure—linux/mc146818rtc.h ....... 61
- Real-Time Profiling ....... 63
- Time of Day (TOD) Functions ....... 65
- System Initialization and Boot ....... 67
- Sequence of Kernel Tables Creation at Boot ....... 68
- Hardware Recognition at Boot ....... 68
- Shutdown ....... 69
- Data Structures—linux/reboot.h ....... 70
- Data Structure—linux/mmzone.h ....... 71
- Data Structures—linux/timer.h ....... 73
- Data Structures—linux/time.h ....... 76
- Data Structures—linux/irq.h ....... 77

## 4 The Linux Process Model ....... 81

- Processes ....... 82
- Forking ....... 85
- Threads ....... 93
- The 2.4 Threaded Kernel ....... 96
- Performance Limitations ....... 96
- Data Structures-linux/sched.h ....... 98

## 5 The Linux VM Manager ....... 115

- VM Concepts ....... 116
- Swapping ....... 117
- Page Replacement ....... 118
- The Linux 2.4 Implementation ....... 119
- Address Translation ....... 119
- The TLB in Linux ....... 121
- Page Allocation and Deallocation ....... 122
- Page Deallocation ....... 123
- The Least Recently Used (LRU) Algorithm ....... 124
- Swapping and Discarding Pages ....... 124
- Swapping Pages Out ....... 125
- Reducing the Size of the Page and Buffer Caches ....... 128
- Swapping Out Shared Pages ....... 129
- Swapping Pages In (Demand Paging) ....... 129
- Page in Swap ....... 129
- Shared Page in Swap ....... 129
- Executable Image Page ....... 130
- Addressing Beyond 4GB on an Intel x86 ....... 130
- Improving the VM ....... 132
- Implementing Page Coloring ....... 133
- Data Structures-include/linux/sched.h ....... 133
- Data Structures-linux/include/mm.h ....... 150

## 6 The Linux Scheduler ....... 161

- Scheduling Classes ....... 164
- Threads ....... 165
- SMP Scheduler Heuristics ....... 167
- Kernel Preemption and User Preemption ....... 171
- Implications of the Linux Approach ....... 172
- Improving the Scheduler ....... 173
- Varying CPUs Offline and Online ....... 173
- CPU Affinity ....... 174
