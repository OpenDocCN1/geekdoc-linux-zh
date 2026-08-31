

# 技术观察清单

> From: [eLinux.org](http://eLinux.org/Technology_Watch_List "http://eLinux.org/Technology_Watch_List")

## Technology Watch List

This page lists technologies and projects that CELF members are interested in the status of. This includes kernel patches, new technology research, and middleware and user-space projects of key interest for consumer electronics products. The projects may be the topics of discussion at CELF meetings, and we plan to watch and report the status of these technologies.

Please add any information you have about the technology items listed below!

## Contents

1. Latest Watchlist
2. Kernel Stuff
   1. Size Stuff
   2. File Systems
   3. Tracing and instrumentation
   4. Realtime
   5. Security
   6. Power Management
   7. Bootup Time
   8. Miscellaneous
3. Middleware

## Latest Watchlist

The **Status** field in the table below indicates whether this feature is on track for being mainlined. The **When was last activity** field indicates the kernel version number or date when the last activity was noted for this feature. This could be the last kernel version where bits from this patch were mainlined, or the last date of visible feature development activity outside the main tree.

See also: Embedded linux status

## Kernel Stuff

### Size Stuff

| Technology, Feature or Patch | Status | When was last activity | Notes |
| --- | --- | --- | --- |
| [Linux-tiny](http://elinux.org/Linux_Tiny) | In active maintenance. Path set published for 2.6.24 | Latest full patchset was published Oct. 13, 2007, Latest patch (`CONSOLE_TRANSLATIONS`) was mainlined in June 2008 | Maintainer is Michael Opdenacker (with help from Thomas Petazzoni). See [Linux Tiny Patch Details](http://elinux.org/Linux_Tiny_Patch_Details "Linux Tiny Patch Details") for details about the patch status. |
| `kpagemap` - memory instrumentation | mainlined in Feb, 2008 (for 2.6.25) | Feb 2008 | - Can show details about every allocated and virtual page on the system.<br>- Introduces PSS and USS size metrics:<br>&nbsp;&nbsp;- PSS - Proportional Set Size<br>&nbsp;&nbsp;- USS - Unique Set Size<br>- Resources:<br>&nbsp;&nbsp;- ELC 2007 presentation: [`selenic.com/repo/pagemap/raw-file/tip/memory-profiling.html`](http://selenic.com/repo/pagemap/raw-file/tip/memory-profiling.html)<br>&nbsp;&nbsp;- LWN.net article: [`lwn.net/Articles/230975/`](http://lwn.net/Articles/230975/)<br>&nbsp;&nbsp;- Visualization tools: [`selenic.com/repo/pagemap`](http://selenic.com/repo/pagemap) |
| [Bloatwatch](http://www.selenic.com/bloatwatch/) (2.0) | Now actively reporting kernel sizes | April 2008 | See [Matt's presentation from ELC 2008](http://www.celinux.org/elc08_presentations/elc2008.odp) |
| `gcc -ffunction-sections -fdata-sections` | Patches submitted to LKML | July 2008 | See [Function sections](http://elinux.org/Function_sections "Function sections") |

### File Systems

| Technology, Feature or Patch | Status | When was last activity | Notes |
| --- | --- | --- | --- |
| [Squash Fs](http://elinux.org/Squash_Fs "Squash Fs") | Mainlined in January 2009 (for 2.6.29). See [`lwn.net/Articles/314326/`](http://lwn.net/Articles/314326/). | As of Feb, 2009, Phillip was working on some user-space tools issues, to support the new filesystem format (version 4.0) | Good job Phillip! |
| [AXFS](http://elinux.org/AXFS "AXFS") | Not mainlined. | Some required (predecessor) bits were mainlined in March, 2008. A version was submitted to LKML in August 2008. | Flash filesystem that allows for tuning the amount of [XIP](http://elinux.org/Application_XIP "Application XIP").<br><br>See [AXFS: Architecture and Results](http://www.celinux.org/elc08_presentations/AXFS_at_ELC_2008.ppt) - Jared Hulbert's presentation for ELC 2008 |
| `LogFS` | Not mainlined. | Last mainline attempt was May, 2008. | - Home page is at: [`logfs.org/logfs/`](http://logfs.org/logfs/)<br>- Jörn Engel is working on a re-write to address several major issues.<br>- CELF is funding this work. |
| `UBIFS` | mainlined in 2.6.27 |  | Resources:<br>- [home page?](http://www.linux-mtd.infradead.org/doc/ubifs.html)<br>- [white paper](http://www.linux-mtd.infradead.org/doc/ubifs_whitepaper.pdf)<br>- [LWN.net article](http://lwn.net/Articles/276025/) |
| [Pram Fs](http://elinux.org/Pram_Fs "Pram Fs") | submitted for review for 2.6.31 | June 2009 | See [`lkml.org/lkml/2009/6/13/86`](http://lkml.org/lkml/2009/6/13/86) |

### Tracing and Instrumentation

| Technology, Feature or Patch | Status | When was last activity | Notes |
| --- | --- | --- | --- |
| `LTTng` | core not mainlined. Markers were mainlined in 2.6.24 | ? | LTTng instrumentation was changed to use markers, in early 2007 |
| [SystemTap](http://elinux.org/System_Tap) (and `Kprobes`) for non-i386 arches | ARM support merged for 2.6.25 | ? | KProbes ports for ARM, MIPS and PPC32 were reported on at ELC 2007. SystemTap for SH was demo'ed at ELC 2007 |
| [Kernel Function Trace](http://elinux.org/Kernel_Function_Trace) (KFT) | not mainlined | Last published patches for 2.6.22 | Nicholas McGuire was taking over maintainership from Tim Bird, with funding from CELF. Haven't heard much recently (as of June 2008) |
| `ftrace` | mainlined in 2.6.27 |  | This was formerly the latency-trace features from the RT-preempt patch set, refactored for general use |
| `printk-times` (arch support) | fully mainlined? | April, 2005 | Some arches had problems with accessing the clock too early in the kernel bootup sequence, but a new setup routine defers turning on the timestamping until after timekeeping is initialized |

### Realtime

| Technology, Feature or Patch | Status | When was last activity | Notes |
| --- | --- | --- | --- |
| `KTimers` | mainlined, but needs lots of porting to embedded architectures | 2.6.23 / 2.6.24 | Adding clock driver support for various architectures is an ongoing process |
| `RT-preempt` | some parts mainlined | current RT patches are still against 2.6.26 | Next target is to integrate threaded interrupts in 2.6.29 - as discussed on LinuxPlumbers conference Oregon 2008 |
| `Xenomai` | external project | 2.6.25 - stable release, newer in development | Xenomai is a real-time development framework cooperating with the Linux kernel, in order to provide a pervasive, interface-agnostic, hard real-time support to user-space applications, seamlessly integrated into the GNU/Linux environment. Ready to deploy. |

### Security

| Technology, Feature or Patch | Status | When was last activity | Notes |
| --- | --- | --- | --- |
| `App Armour` | not mainlined | May, 2007 | - LSM framework was removed from kernel in 2.6.24<br>- AppArmour group was let go from Novell in late 2007<br>&nbsp;&nbsp;- See [`www.news.com/8301-13580_3-9796140-39.html`](http://www.news.com/8301-13580_3-9796140-39.html)<br>&nbsp;&nbsp;- [LWN.net article](http://lwn.net/SubscriberLink/254740/f71fe8e26c906233/) |
| [TOMOYO Linux](http://elinux.org/TomoyoLinux) | not mainlined | [Nov 17, 2007](http://lwn.net/Articles/258905/) (4th post) [(trying now)](http://elinux.org/TomoyoLinux#Mainline) | "TOMOYO Linux has only recently surfaced on the wider mailing lists; its reception has not been entirely friendly. This project's developers have some work to do if they are (1) to get past the same obstacles which have slowed AppArmor, and (2) show that their project is sufficiently different from AppArmor to merit inclusion as yet another security framework." (from [Linux Weather Forecast](http://www.linux-foundation.org/en/Linux_Weather_Forecast/security)) |
| `SMACK` | mainlined in 2.6.25 | . | [LWN.net article on SMACK](http://lwn.net/Articles/244531/) |
| `SELinux` (usable in embedded) | SELinux is mainlined, but some issues for making SELinux usable for embedded remain | April 2008 | - There has been much progress recently to support SELinux in the embedded space<br>- Requires filesystem with xattrs (some flash filesystems do not support xattrs) |




在ELC 2008上，Yuichi Nakamura描述了SELinux嵌入式配置，其体积可小至700K。

*   [Development of Embedded SELinux](http://www.celinux.org/elc08_presentations/ELC2008_nakamura.pdf) —— Yuichi Nakamura在ELC 2008上的演示文稿。

### 电源管理

| 技术、特性或补丁 | 状态 | 最后活动时间 | 备注 |
| --- | --- | --- | --- |
| `powertop` | 已并入主线支持（针对x86架构） | ？ |  

*   `powertop`显示定时器和电源状态持续时间。
*   仅在x86上得到良好支持？？
    *   要在其他架构上支持，平台需要支持`CPUIdle`接口，以便显示C状态（电源状态）。**对于非Intel处理器已有一些相关活动。

|
| `PM QoS` | 已并入`2.6.23-mm1` | 2007年10月 |（参见[`lesswatts.org`](http://lesswatts.org)）需要嵌入式领域的人员参与审查，帮助定义接口、扩展功能，并从嵌入式视角提出问题。 |
| Wolfson电压调节器相关 | 尚未并入主线？？ | 2008年3月？ | 参见[Every Microamp is Sacred - A Dynamic Voltage and Current Control Interface for the Linux Kernel](http://www.celinux.org/elc08_presentations/regulator-api-celf.pdf) —— Liam Girdwood在ELC 2008上的演示文稿。 |

### 启动时间

| 技术、特性或补丁 | 状态 | 最后活动时间 | 备注 |
| --- | --- | --- | --- |
| `deferred module load` | 未并入主线，无补丁 | 2008年7月 | Tim Bird在linux-embedded邮件列表中提出，但未附带补丁。 |
| `async initcalls` | 未并入主线 | 2008年7月 | 补丁由Arjan van de Ven提交。 |
| 快照启动 | 未并入主线 | 2006年7月 | Sony在OLS 2006上发表了论文。该技术已用于Sony产品中。 |
| `fastboot`内核配置选项 | 未并入主线？ | 2006年7月 | Arjan van de Ven作为其`async initcalls`补丁的一部分提交。 |

### 其他

| 技术、特性或补丁 | 状态 | 最后活动时间 | 备注 |
| --- | --- | --- | --- |
| 用户空间I/O | 似乎已并入主线（参见：[`lwn.net/Articles/242483/`](http://lwn.net/Articles/242483/)） | 2007年7月 | 参考：[`www.kroah.com/log/linux/uio.html`](http://www.kroah.com/log/linux/uio.html) |

## 中间件

| 项目 | 状态 | 最后活动时间 | 备注 |
| --- | --- | --- | --- |
| `libdlna` | 开发者已支持除MPEG-4和WMV之外的所有配置文件（[`hg.geexbox.org/libdlna/`](http://hg.geexbox.org/libdlna/)） | 2007年8月29日 | 短期目标是为Ushare媒体服务器提供DLNA支持，长期目标是提供通用的DLNA参考库。参考：[`libdlna.geexbox.org/`](http://libdlna.geexbox.org/) |

[Category](http://eLinux.org/Special:Categories "Special:Categories")：

*   [Community](http://eLinux.org/Category:Community "Category:Community")
