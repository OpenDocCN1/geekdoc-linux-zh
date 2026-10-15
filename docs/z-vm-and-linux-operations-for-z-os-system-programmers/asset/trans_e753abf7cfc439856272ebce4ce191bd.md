

## 检查系统级别：`query cplevel` 和 `query cmslevel`

QUERY CPLEVEL 和 QUERY CMSLEVEL 命令对于确保维护已正确应用于每个系统非常有用。可以使用这些命令检查以下项目：

- 软件版本级别、发行级别和发行修改级别
- 软件服务级别号
- CP 系统软件写入 DASD 的日期和时间（转换为当前活动时区）
- CP 最后启动的日期和时间
- CMS 的发行版和服务级别

命令的示例显示在示例 5-2 中。

*示例 5-2 检查 CP 和 CMS 级别*

```
q cplevel
z/VM Version 5 Release 3.0, service level 0701 (64-bit)
Generated at 05/29/07 23:21:12 EDT
IPL at 06/11/08 07:58:34 EDT
Ready; T=01/0.01 11:45:20
q cmslevel
CMS Level 23, Service Level 701
Ready; T=01/0.01 11:45:24
```

## 检查 CP 加载参数：`query cpload`

使用 QUERY CPLOAD，如示例 5-3 所示，来显示有关上次 CP IPL 的信息。显示的信息包括上次使用的 CP 模块的位置、参数磁盘的位置以及 CP 的启动方式。

*示例 5-3 查询 CPLOAD*

```
q cpload
Module CPLOAD was loaded from minidisk on volume LX6RES at cylinder 39.
Parm disk number 1 is on volume LX6RES, cylinders 39 through 158.
Last start was a system IPL.
Ready; T=01/0.01 11:46:07
```

## 检查实际存储量：`query storage`

QUERY STORAGE 命令（缩写为 Q STO）用于显示 LPAR 启动后可用的实际内存量。参见第 239 页的示例 5-4。

## 检查扩展存储量：query xstorage

QUERY XSTORAGE 命令（缩写为 Q XSTO）用于显示分区中配置的实际扩展存储量。该命令的输出还显示正在使用的扩展存储量以及用于微型磁盘缓存（MDC）的量。参见示例 5-5。

```
q xstor
XSTORE= 2048M online= 2048M
XSTORE= 2048M userid= SYSTEM usage= 0% retained= 0M pending= 0M
XSTORE MDC min=0M, max=0M, usage=0%
XSTORE= 2048M userid= (none) max. attach= 2048M
Ready; T=0.01/0.01 11:47:27
```

## 检查所有处理器是否可用：query processors

QUERY PROCESSORS 命令（缩写为 Q PROC）用于显示分区的处理器当前分配情况。

MASTER 处理器是用于 IPL 的基本处理器，ALTERNATE 处理器在 IPL 时会自动上线，而 STANDBY 处理器可供分区使用，但处于离线状态。参见示例 5-6。PROCESSOR 行中的最后一个字段表示处理器的类型：CP、IFL、ICF、ZIIP 或 ZAAP。

```
q processors
PROCESSOR 00 MASTER CP
PROCESSOR 01 ALTERNATE CP
PROCESSOR 02 ALTERNATE CP
PROCESSOR 03 ALTERNATE CP
PROCESSOR 04 STANDBY CP
PROCESSOR 05 STANDBY CP
Ready; T=0.01/0.01 11:51:31
```

## 更改处理器对系统的可用性

在正常情况下，您会使用处理器群集或分区中的所有处理器启动并运行系统。但是，如果您安装的支持人员指示您这样做，您可以使用 VARY ONLINE PROCESSOR 或 VARY OFFLINE PROCESSOR 命令来控制处理器是否可供 z/VM 使用。有关这些命令的更多信息，请参阅 z/VM: CP Commands and Utilities Reference, SC24-6081⁵

## 检查系统 DASD 配置：query alloc

系统 IPL 后，检查所需的分页和排队是否可用且在线是一个良好的做法。您还可以检查临时磁盘空间。

QUERY ALLOC PAGE 检索分页空间配置。在示例 5-7 中，四个 3390-03（每个为 3339 个柱面）已配置为分页设备。在这些分页设备上总共只分配了 13 个页面。

示例 5-7 检查 LPAR 中可用的分页空间

```
q alloc page
VOLID RDEV EXTENT EXTENT TOTAL PAGES HIGH %
START END PAGES IN USE PAGE USED
---------- ---------- ---------- ---------- ---------- ---------- ----------
LX6PAG 1A22 1 3338 600840 0 0 0%
DK8226 8226 0 3338 601020 0 0 0%
DK8227 8227 0 3338 601020 13 26 1%
DK8228 8228 0 3338 601020 0 0 0%
---------- ---------- ---------- ---------- ---------- ---------- ----------
SUMMARY 2348K 13 1%
USABLE 2348K 13 1%
Ready; T=0.01/0.01 11:54:40
```

同样，QUERY ALLOC SPOOL 命令检查排队配置。在示例 5-8 中，只有一个 3390-03 DASD 被定义为排队设备，并且正在使用 140075 个页面，约占可用于排队的总页面的 23%。

示例 5-8 检查排队空间

```
q alloc spool
VOLID RDEV EXTENT EXTENT TOTAL PAGES HIGH %
START END PAGES IN USE PAGE USED
---------- ---------- ---------- ---------- ---------- ---------- ----------
LX6SPL 1A21 1 3338 600840 140075 145430 23%
---------- ---------- ---------- ---------- ---------- ---------- ----------
SUMMARY 600840 140075 23%
USABLE 600840 140075 23%
Ready; T=0.01/0.01 11:55:39
```

⁵ http://publibz.boulder.ibm.com/epubs/pdf/hcse4b21.pdf

