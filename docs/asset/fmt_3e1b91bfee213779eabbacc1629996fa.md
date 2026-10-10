
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

# 第 2 章 软件组件

- `Calc`—一个与 Microsoft Excel 类似的电子表格，具有相似的功能范围；`Calc`还提供了 Excel 中不具备的功能，包括一个根据用户数据布局自动定义绘图序列的系统。它可以保存为`.xlsx`文件，这是 Microsoft Excel 使用的开放 XML 电子表格格式扩展名。`Calc`还可以直接将电子表格写入`PDF`文件。
- `Impress`—一个与 Microsoft PowerPoint 类似的演示文稿程序；`Impress`可以将演示文稿导出为 Macromedia Flash (`SWF`)文件，允许在任何安装了 Flash 播放器的计算机上播放。它还支持导出为`HTML`、`HTML`和矢量图形格式（`SVG`、`EPS`）。你也可以用`Impress`创建`PDF`文件。

如果你正在运行`CentOS 7`系统，`LibreOffice`是一个极佳的选择。（图 2-24 显示了 LibreOffice 套件中的默认组件。）对于`Windows 10`用户，`LibreOffice`是免费的。然而，如果你是一个与运行 Microsoft Office 用户共享文档的学生，那么 Office 家庭学生版对于`Windows 10`来说是更好的选择。

![](img/290e46d5832f20e3707f4841e4e6d75a_95_0.png)

| 应用程序 | 位置 |
|---|---|
| 收藏夹 | LibreOrganizer |
| 辅助程序 | TimeTracker |
| 文档 | LibreOffice Calc |
| 图形 | LibreOffice Draw |
| 办公 | LibreOffice Imp |
| 互联网 | LibreOffice Writer |
| 声音 | |
| 通用 | |
| 其他 | |

## 章节总结

- PC 的软件组件用于执行各种任务。每个组件协同工作，而用户通常察觉不到这些过程。每个组件在 PC 的整体性能中都起着特定的作用，没有哪个组件比另一个更重要。PC 资源由操作系统内部运行的许多程序管理。
- PC 的第一个操作系统是`DOS`。PC 操作系统系统的核心是内核（`kernel`），它是保护硬件并为每个应用程序服务的地方。
- 操作系统通过控制处理器、内存、设备、存储和用户界面来管理资源。现代操作系统防止了抢占式多任务、多线程和虚拟内存。
- 操作系统同时与硬件和应用程序交互。例如，操作系统通过安装和运行应用程序来与它们交互。操作系统提供磁盘和网络访问以及打印服务。
- PC 有许多种操作系统。最常见的是`DOS`、`Windows`和`CentOS 7`。它们都从诞生之初就不断演进，允许用户使用编辑器、图形用户界面以及打印机、键盘、显示器和磁盘驱动器等外设备。最好的操作系统是稳定、安全且可扩展的。
- 操作系统与不同的系统工具配合工作，在你的 PC 上执行各种任务。例如，要更新配置文件，你需要一个配置编辑器。使用`Windows 10`时，你使用`Regedit`更新注册表文件。当你需要监控系统时，在`Windows 10`中使用任务管理器，在`CentOS 7`中使用系统监器。根据注册表或配置文件是指操作系统、工具还是应用程序，使用不同类型的编辑器。
- 你在 PC 上使用许多应用程序，包括文字处理器、电子表格和网络浏览器。

## 关键术语

添加打印机向导（`Add Printer Wizard`）`Windows 10`中的一种向导，用于为应用程序提供打印机。

应用程序（`application`）帮助用户在 PC 上执行任务的程序，例如创建电子表格。

块设备（`block device`）以数据块或字节组而非字符来移动信息的设备。例如磁盘驱动器。

总线驱动程序（`bus driver`）一种用于 I/O 总线的 WDM 驱动程序。它提供了由设备驱动的插槽功能。

字符设备（`character device`）以字符流的形式（一次一个字符）传输或接收信息的设备。例如键盘。

命令行界面（`CLI`）你用于向操作系统发送命令的程序。

协作式多任务（`cooperative multitasking`）多任务的一种形式，其中每个进程控制其保持 CPU 独占控制的时间长度。

核心（`core`）处理器中实际读取和执行指令的部分。

磁盘操作系统（`DOS`）一个通用术语，指在系统启动或重启时从磁盘设备加载的任何操作系统。

动态链接库（`DLL`）可以被`Windows 10`应用程序使用的执行函数或数据的库。

`exFAT`一为外部驱动器开发的`Windows 10`文件系统。

快速用户切换（`Fast User Switching`）`Windows 10`中的一项功能，允许用户在单台 PC 上切换用户账户而无需退出应用程序和注销。

过滤驱动程序（`filter driver`）一种过滤设备、设备类或总线 I/O 请求的 WDM 驱动程序。

免费软件（`freeware`）个人使用免费提供的软件。免费软件经常在网络上分发。

函数驱动程序（`function driver`）一种驱动单个设备的 WDM 驱动程序。

`Ghostscript`一套基于 Adobe PostScript 和便携文档格式（`PDF`）页面描述语言解释器的免费软件套件。

`GNOME`红帽发行版`CentOS 7`发行版的默认桌面。

图形设备接口（`GDI`）Windows 系统的显示语言界面。

图形用户界面（`GUI`）一种允许用户通过图形图标和视觉指示与计算机交互的界面。

主目录（`home directory`）`CentOS 7`下与用户关联的目录。

内核（`kernel`）操作系统的核心。内核管理内存、文件和外围设备，以及启动应用程序和分配系统资源。

库（`libraries`）帮助你管理文档、音乐、图片和其他文件的文件结构。

`Linux`指使用 Linux 内核的类 Unix 计算机操作系统族。

微软 Windows 安装程序（`Microsoft Windows Installer`）作为`Windows 10`操作系统的一部分提供的安装和配置服务。

多任务处理（`multitasking`）在单台计算机内多个进程同时执行指令。

多任务（`multitasking`）在 PC 上并发运行所有活动进程和线程。

多线程（`multithreading`）在程序内部以快速顺序运行多个进程（多任务处理）。

网络文件夹（`Network folder`）用于定位和连接网络计算机上共享文件夹的文件夹。

网络设备（`networking device`）`CentOS 7`用于网络设备的类别。`CentOS 7`内核使用带有这些设备的数据包。

数据包（`packet`）在网络上作为整体从一个设备传输到另一个设备的信息单元。

物理地址（`physical address`）标识计算机物理内存中实际存储（内存）位置的数字。

`PostScript`由 Adobe Systems 开发并营销的页面描述语言。

`PowerShell`一种用于 Windows 的自动化平台和脚本语言。`PowerShell`利用了`.NET Framework`的力量，提供了丰富的对象和大量的内置功能集。

抢占式多任务（`preemptive multitasking`）一种多任务处理过程，其中操作系统确保所有活动线程都有执行的机会。抢占式多任务防止单个线程垄占处理器。

注册表编辑器（`Regedit`）一种允许用户编辑注册表条目的应用程序。

注册表（`Registry`）`Windows 10`使用的种中心分层数据库，用于存储配置为一个或多个用户、应用程序和硬件设备配置系统所需的信息。

弹性文件系统（`ReFS`）一种为 Windows 设计的“下一代”文件系统。

`RPM`（红帽包管理器）`CentOS 7`中提供安装服务的管理器。

`Samba``CentOS 7`用于支持跨网络资源共享的通信协议。

服务器消息块（`SMB`）基于 Windows 的操作系统用于支持跨网络资源共享的通信协议。

软件组件（`software components`）与操作系统相关的应用程序集合。

标准输入设备（`standard input device`）用于输入设备，如键盘。

标准输出设备（`standard output device`）显示器的另一种别称。

对称多处理（`SMP`）使用负载均衡方法在 CPU 之间分配任务的系统。

打印机配置（`system-config-printer`）`CentOS 7`中的管理工具。

系统监控（`System Monitor`）Windows 中跟踪进程活动的工具。

文本编辑器（`text editor`）允许你创建或编辑文本文件的程序。

线程（`thread`）程序执行的基本单元。一个进程可以有多个线程，每个线程执行不同的工作。

工具（`utility`）对操作系统执行系统相关任务和维护的程序。

虚拟地址（`virtual address`）硬件和软件映射到物理内存的内存位置。

Windows Driver Model（`WDM`）创建 Windows 设备驱动程序的 32 位架构。

`YUM`作为`CentOS 7`的一部分安装和配置服务。

## 复习题

2. 下面哪些管理任务是操作系统的功能？（选择所有适用）

a. 处理

b. 内存

c. 设备

d. 存储

e. 应用程序
