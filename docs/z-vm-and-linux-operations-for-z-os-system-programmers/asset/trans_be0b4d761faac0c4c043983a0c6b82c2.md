

# CP QUERY CPOWNED

使用此命令显示 CP 所拥有的 DASD 卷列表。如果出现分页或 spooling 问题，可以通过此命令检查所有必需的卷是否可用。参见示例 7-9。

### 示例 7-9 QUERY CPOWNED 命令及示例输出

```
q cpowned
Slot Vol-ID Rdev Type Status
1 LX6RES 1A20 Own Online and attached
2 LX6SPL 1A21 Own Online and attached
3 LX6PAG 1A22 Own Online and attached
4 LX6W01 1A23 Own Online and attached
5 LX6W02 1A24 Own Online and attached
6 DK8226 8226 Own Online and attached
7 DK8227 8227 Own Online and attached
8 DK8228 8228 Own Online and attached
9 ------ ---- ---- Reserved
10 ------ ---- ---- Reserved
```

# CP QUERY FRAMES

使用此命令显示主机实存的状况。你可能需要在检查存储利用率时执行此操作，而用户正处于合格列表中。

### 示例 7-10 Query FRAMES 命令

```
cp q frames
All Frames:
  Configured=1048575 Real=1048575 Usable=1048575 Offline=0
  Pageable=1026485 NotInitialized=0 GlobalClearedAvail=128
  LocalClearedAvail=128 LocalUnclearedAvail=124

Frames < 2G:
  GlobalUnclearedAvail=454261 Pageable=521003 LogicalFreeStorage=56
  RealFreeStorage=4 LockedRS=348 LockedCmd=0
  MinidiskCache=9339 Nucleus/Prefix=2430 Trace=325 Other=122

Frames > 2G:
  GlobalUnclearedAvail=436453 Pageable=505482 LogicalFreeStorage=1194
  RealFreeStorage=19 LockedRS=57 LockedCmd=0
  MinidiskCache=13138 Other=17536
```

> z/OS 类比：此命令类似于 z/OS 的 D M=STOR 命令。

# CP QUERY MAXUSERS

使用此命令显示允许的最大登录用户数。如果用户无法登录，这可能是一个很好的执行命令。

> z/OS 类比：要在 z/OS 环境中显示最大用户数，请浏览 SYS1.PARMLIB 串联中的成员 IEASYSSxx。

# CP QUERY MDC

从 B 类用户使用此命令查询整个系统的 minidisk 缓存（MDC）设置、真实设备、活动 minidisk 或目录中定义的 minidisk。参见示例 7-11。此命令对于调查 I/O 问题很有用。

### 示例 7-11 Query MDC 命令

```
q mdc
Minidisk cache ON for system
Storage MDC min=0M max=128M, usage=3%, bias=1.00
Xstore MDC min=0M max=0M, usage=0%, bias=1.00
Ready; T=0.01/0.01 10:23:24
```

# CP QUERY NAMES

使用此命令显示：
- 所有已登录用户的列表
- 每个用户所连接的显示器的真实或逻辑设备号

参见示例 7-12。

### 示例 7-12 Query Names 命令

```
q n
LNXCER - DSC , LNXGUI - DSC , LNXXEN - DSC , COSTA -L0004
FTPSERVE - DSC , TCPIP - DSC , DTCVSM2 - DSC , DTCVSW1 - DSC
VMSERVR - DSC , VMSERVU - DSC , VMSERVS - DSC , OPERSYMP - DSC
DISKACNT - DSC , EREP - DSC , OPERATOR - DSC , MAINT -L0003
VSM - DSC , TCPIP
Ready; T=0.01/0.01 10:26:04
```

> z/OS 类比：在 z/OS 系统上，你可以通过运行 SDSF 显示活动命令来显示类似信息。

# CP QUERY QIOASSIST

使用此命令确定虚拟机的队列 I/O 辅助的当前状态，如示例 7-13 所示。此命令对于调查 I/O 或网络问题很有用。

### 示例 7-13 Query QIOASSIST 命令

```
q qioassist
ALL USERS SET - ON

USER   SETTING   STATUS
MAINT  ON        INACTIVE
Ready; T=0.01/0.01 10:28:40
```

# CP QUERY QUICKDSP

使用此命令显示用户的 QUICKDSP 属性。参见示例 7-14 获取示例输出。

### 示例 7-14 QUICKDSP 命令

```
cp query quickdsp maint
USER MAINT  : QUICKDSP = OFF
```

# CP QUERY RESERVED

使用此命令显示保留的实存帧数，并为用户保留存储页。参见示例 7-15。

### 示例 7-15 Query RESERVED 命令

```
q res
MAINT    RSV=00000010 ACT=00000010
LNXGUI   RSV=00000020 ACT=00000020
REQUESTED FRAME TOTAL=00000030; ACTUAL FRAME TOTAL=00000030
Ready; T=0.01/0.01 10:57:15
```

CP QUERY RESERVED 命令在存储受限系统的用户调优时很有用。

# CP QUERY SRM

使用此命令显示调度程序用于设置系统资源访问优先级的系统范围参数。SRM 是系统资源管理器。参见第 333 页的示例 7-16。

重要提示：请谨慎使用此命令并监控其使用情况，因为如果使用不当可能会出现合格列表。

