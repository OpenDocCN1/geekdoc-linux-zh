# # Linux Kernel 2.4 Internals

**Tigran Aivazian tigran@veritas.com**

23 August 2001 (4 Elul 5761)

*Introduction to the Linux 2.4 kernel. The latest copy of this document can be always downloaded from:* [http://www.moses.uklinux.net/patches/klc.sgm](http://www.moses.uklinux.net/patches/klc.sgm) *This guide is now part of the Linux Documentation Project and can also be downloaded in various formats from:* [http://www.linuxdoc.org/guides.html](http://www.linuxdoc.org/guides.html) *or can be read online (latest version) at:* [http://www.moses.uklinux.net/patches/klc.html](http://www.moses.uklinux.net/patches/klc.html) *This documentation is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 2 of the License, or (at your option) any later version. The author is working as senior Linux kernel engineer at VERITAS Software Ltd and wrote this book for the purpose of supporting the short training course/lectures he gave on this subject, internally at VERITAS. Thanks to Juan J. QuinTELA (quintela@fi.udc.es), Francis Galiegue (fg@mandrakesoft.com), Hakjun Mun (juniofm@orgio.net), Matt Kraai (kraai@alumni.carnegiemellon.edu), Nicholas Dronen (mdronen@froi.com), Samuel S Chessman (chessman@tux.org), Nadeem Hasan (nhasan@nadm.com) for various corrections and suggestions. The Linux Page Cache chapter was written by: Christoph Hellwig (ch@exacer.de). The IPC Mechanisms chapter was written by: Russel Weight (weight@rs.ibm.com) and Mingming Cao (mcao@us.ibm.com)*

# ## 1. Booting

+   - [1.1 Building the Linux Kernel Image](#1.1-building-the-linux-kernel-image)
+   - [1.2 Booting: Overview](#1.2-booting-overview)
+   - [1.3 Booting: BIOS POST](#1.3-booting-bios-post)
+   - [1.4 Booting: bootsector and setup](#1.4-booting-bootsector-and-setup)
+   - [1.5 Using LILO as a bootloader](#1.5-using-lilo-as-a-bootloader)
+   - [1.6 High level initialisation](#1.6-high-level-initialisation)
+   - [1.7 SMP Bootup on x86](#1.7-smp-bootup-on-x86)
+   - [1.8 Freeing initialisation data and code](#1.8-freeing-initialisation-data-and-code)
+   - [1.9 Processing kernel command line](#1.9-processing-kernel-command-line)

# ## 2. Process and Interrupt Management

+   - [2.1 Task Structure and Process Table](#2.1-task-structure-and-process-table)
+   - [2.2 Creation and termination of tasks and kernel threads](#2.2-creation-and-termination-of-tasks-and-kernel-threads)
+   - [2.3 Linux Scheduler](#2.3-linux-scheduler)
+   - [2.4 Linux linked list implementation](#2.4-linux-linked-list-implementation)
+   - [2.5 Wait Queues](#2.5-wait-queues)
+   - [2.6 Kernel Timers](#2.6-kernel-timers)
+   - [2.7 Bottom Halves](#2.7-bottom-halves)
+   - [2.8 Task Queues](#2.8-task-queues)
+   - [2.9 Tasklets](#2.9-tasklets)
+   - [2.10 Softirqs](#2.10-softirqs)
+   - [2.11 How System Calls Are Implemented on i386 Architecture?](#2.11-how-system-calls-are-implemented-on-i386-architecture)