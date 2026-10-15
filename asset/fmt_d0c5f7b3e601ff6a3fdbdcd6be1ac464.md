
| Volatility Foundation Volatility Framework 2.4 |
| 模块基地址 | 模块名称 | 结果 |
| :--- | :--- | :--- |
| 0xffffff8803d00000 UNKNOWN | OK: driver.ffff88003d00000.sys |

如果你计划将提取的模块加载到 IDA Pro 进行静态分析，请记住一点：PE 头中的 `ImageBase` 需要更改以匹配其在内核内存中的实际加载地址。换句话说，对于最后一个示例，你应该使用 `0xffffff8803d...`。以下是使用来自 `https://code.google.com/p/pefile` 的 `pefile` Python 模块来实现的方法：

```
$ python

Python 2.7.6(v2.7.6:db074e, Nov 10 2013, 00:42:54)

[GCC 4.2.1 (Apple Inc. build 5566) (3)] in darwin

Type "help", "copyright", "credits" or "license" for more information.

>>> import pefile

>>> ps = pefile.PE("driver.ffff88003d00000.sys", fast_load = True)

>>> ps.OPTIONAL_HEADER.ImageBase = 0xffffff8803d00000

>>> ps.write("driver.ffff88003d00000.sys")

>>> quit()
```

这个简单的修复为 IDA 提供了正确显示函数、跳转和字符串引用所需的额外上下文。根据二进制文件导入地址表的状态，你可能还需要使用 Volatility 的 `impscan` 插件来生成可以应用到 IDA 数据库的标签。稍后你将看到使用 `impscan` 的示例。

# 378 第二部分：Windows 内存取证

在本（另参见《恶意软件分析实》中的“Recipe 16-8：使用 ImpScan 扫描导入函数”）。

## 内核模式下的线程

当内核模块使用 `PsCreateSystemThread` 创建线程时，System 进程（XP 及更高版本中 PID 为 4）成为该线程的所有者。换句话说，System 进程是内核模式下启动的线程的默认所在地。你可以通过 Process Explorer 探索这一点，发现 System 进程拥有的线程的起始地址是内核模块（如 `ACPI.sys` 和 `HTTP.sys`）的偏移（见图 13-3）。

![](img/9e59079ff66884b5d70128a9edb02f4c_403.png)

**图 13-3：在内核模式启动的线程由 System 进程所有。解析内存转储时，你可以根据以下因素将这些线程与其他线程区分开：

- `ETHREAD.SystemThread` 值为 1。
- `ETHREAD.CrossThreadFlags` 成员设置为 `PS_THREAD_FLAGS_SYSTEM`。
- 所有者进程为 4。

这些信息可以帮助发现试图隐藏在内核中的恶意软件家族，如 Root。当 Rootkit 模块最初加载时，它们分配内核内存池，将可执行代码拷贝到池中并调用 `PsCreateSystemThread` 开始执行。线程创建后，模块可以加载。这些操作让 Rootkit 在运行于未标记池时保持隐蔽。然而，这为取证产生了明显的痕迹，因为你有一个线程的起始地址指向一个不存在模块的内核区域。

## 内核线程

图 13-4 显示了受 Root 感染的机器 System 进程所有的线程。你可以看到图 13-3 中不存在的四个新线程。Process Explorer 显示的起始地址格式为 `driverName.sys+0xabcd`，而不是正常格式，因为起始地址不在加载模块的范围内。

![](img/9e59079ff66884b5d70128a9edb02f4c_404.png)

**图 13-4：Process Explorer 显示四个没有已知模块的线程线程。**

## 检测孤立线程

`threads` 插件可以帮助你识别此类方式的隐藏尝试。它通过遍历双向链表并记录加载模块的基地址和大小，然后扫描系统线程并检查 `_THREAD.StartAddress` 值是否在某个模块的范围内。如果插件无法将线程与其所有驱动程序配对，则假设该线程是脱离或隐藏的。由于此原因，线程变成了孤立线程。以下输出显示了孤立线程在内存转储中的情况。你会在起始地址（`0xffedd150`）右侧看到显示 UNKNOWN 的 OrphanThread 。

```
$ python vol.py -f orphan.vmem -F OrphanThread --profile=WinXP86

ETHREAD:0xff92b00 Pid: 4: 1648

Tags: OrphanThread,SystemThread

Created: 2010-08-15 19:26:13

Exited: 1970-01-01 00:00:00

Owned Process: System

Attached Process: System

State: DelayExecution

BasePriority: 0x8

Priority: 0x0

TEB: 0x0000000

StartAddress: 0xffedd150 UNKNOWN

ServiceTable: 0x8552180

[0] 0xffff501010

[1] 0x0000000

[2] 0x0000000

[3] 0x0000000

Win32Thread: 0x0000000

CrossThreadFlags: PE_THREAD_FLAGS_SYSTEM
```

如果你怀疑系统存在内核 Rootkit，请使用 `modscan` 插件寻找孤立线程的支持证据。请记住，线程的起始地址将指向恶意文件内部的函数，而不是 PE 文件的基地址。因此，你可能需要一些脚本从给定地址向前扫描以找到第一个有效的 PE 头。

> 警告 Rootkit 可以通过将 `_THREAD.StartAddress` 值指向已知驱动来轻松绕过孤立检测技术。在你的 VB2008 演讲（`http://www.virusbt.com/pdf/conference_slides/2008/Kasslin-Florio-VB2008.pdf`）中，Kimmo Kasslin 和 Elia Flora 注意到第三代 Root 开始应用这些补丁来增加隐蔽性。

## 驱动程序对象与 IRP

通常，当内核模块加载时，除了创建 `KL_DATA_TABLE_ENTRY` 结构外，还会初始化相应的 `_DRIVER_OBJECT`。这是重要的，因为驱动程序对象包含了关于内核模块的关键信息，例如模块基地址的副本、卸载例以及指向其处理函数的指针。当章节后面描述的元数据结构取消链接或损坏时，这些信息可以帮助定位模块。此外，通过寻找驱动程序对象，你可以检查处理例中的钩子。

为了提供更多背景，Windows 中的应用程序通过发送 IO 包（IRP）与驱动程序通信。IRP 是一种数据结构，其中包含一个用于识别所需操作（创建、读、写等）的整数以及用于驱动程序读取或写入任何数据的缓冲区。每个驱动程序对象都有一个 28 个函数指针的表，它可以注册以处理不同的操作。驱动程序通常在加载后的入口处配置此表，称为主函数表或 IRP 函数表。以下输出显示名为 `MajorFunction` 的 28 个指针表是每个驱动程序都有：

```
>> *(DRIVER_OBJECT)

'_DRIVER_OBJECT (336 bytes)

0x0 : Type ['short']

0x2 : Size ['short']

0x8 : DeviceObject ['pointer64', ['DEVICE_OBJECT']]

0x10 : Flags ['unsigned64', ['long']]

0x18 : DriverStart ['pointer64', ['void']]

0x20 : DriverSize ['unsigned long']

0x28 : DriverSection ['pointer64', ['void']]

0x30 : DriverExtension ['pointer64', ['DRIVER_EXTENSION']]

0x38 : DriverName ['UNICODE_STRING']

0x48 : HardwareDatabase ['pointer64', ['UNICODE_STRING']]

0x50 : FastIoDispatch ['pointer64', ['FAST_IO_DISPATCH']]

0x58 : DriverInit ['pointer64', ['void']]

0x60 : DriverStartIo ['pointer64', ['void']]

0x68 : DriverUnload ['pointer64', ['void']]
```
