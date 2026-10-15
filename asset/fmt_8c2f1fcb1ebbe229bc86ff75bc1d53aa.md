
- [自定义 Microsoft 服务 UNIX 安装](http://www.microsoft.com/technet/treeview/default.asp?url=/technet/prodtechnol/windows2000serv/deploy/sfucustom.asp?frame=true)
- [UNIX 环境下的 Windows 2000 专业版白皮书](http://www.microsoft.com/windows2000/library/planning/default.asp)
- [Windows 2000 工具包摘录](http://www.microsoft.com/windows2000/library/resources/reskit/default.asp)

# 第 7 章：创建开发环境

## 创建开发环境

## 引言

本章描述了如何为迁移创建开发环境。首先，它介绍了一些可用工具和功能。然后，在三个主要部分，它描述了如何：
- 配置开发环境
- 填充源代码和构建结构
- 使用开发环境

在制定迁移策略时做的决策将有助于定义开发环境。该环境是原生 Microsoft® `Win32®` 应用程序接口或 Microsoft `Interix`。

## 开发环境概述

开发环境包含了从 UNIX 迁移到 Microsoft Windows® 操作系统所需硬件和软件，包括：
- 软件开发包（`SDK`），包含编译器、编辑器和调试器，提供了创建、构建和调试应用程序的基础。
集成开发环境（`IDEs`），如 `Visual Studio`，为由 `SDK` 提供的工具提供了统一且一致的访问。
软件管理工具（如用于源代码管理和问题跟踪的软件）虽然不是关键，但它们为大型迁移项目添加了显著价值。
分析工具（如性能分析和测试工具）可提高应用程序的性能。
跨平台工具和库（包括 Rogue Wave `SourcePro` 等第三方包）可以集成到应用程序中。

这些设施适用于系统的开发人员或测试人员，如图 7.1 所示。

| 开发与测试 | | |
| :--- | :--- | :--- |
| 编译器 | 开发者 | |
| 源代码控制系统 | 测试人员 | |
| 集成开发环境 | | |
| 测试脚手架 | | |

图 7.1 开发环境

`Visual Studio` 是为开发者提供的一个全面且强大的工具。它包含了许多功能，例如用于源码编辑的交互式 `IntelliSense®`、编辑并继续

## 调试、与用于控制的 Visual SourceSafe 集成，以及大量的用户自定义和帮助。这些功能可能让 Visual Studio 看起来非常复杂，特别是对于习惯使用命令行工具和 `vi` 等编辑器的 UNIX 开发者来说。然而，Visual Studio 还提供了一系列快捷键和自动化宏来简化编辑会话。

克服对 Visual Studio 规模和功能集顾虑的最佳方法就是开始使用它。开发者很快就会发现 Visual Studio 是多易用，以及曾经看似难以胜任的功能如何带来更高的生产力。经验丰富的开发者很快会对 Visual Studio IDE 进行自定义，以满足他们的需求并消除任何不需要的功能。

## Windows 平台 SDK

`SDK` 包含用于构建、调试、测试和交付应用程序的工具。它还包含了编译编译程序所需的所有定义（包含文件）和库。通常，`SDK` 工具是从命令行运行的，就像应用程序在 UNIX 中从 shell 提示符运行一样。`SDK` 工具的输出可以创建在磁盘上、到控制台的文本输出（类似于 UNIX 中的 `stdout`），或者到单一个或多个对话框的图形化输出。

Microsoft Platform SDK 是一组工具和 API 定义，用于为 Windows 平台创建应用程序。它包含了 Windows 所有子系统和 API 的包含文件和文档。它还包含了 Microsoft .NET 企业服务器的定义和文档，包括 Microsoft `BizTalk® Server`、Microsoft `Commerce Server` 和 Microsoft `SQL Server`。安装 .NET 服务器组件是可选的。

Platform SDK 可通过 CD 提供，也可在 Web 上免费下载。它还随 Microsoft Visual C++ 开发系统和 Visual Studio 提供，或者通过 MSDN Professional 或 Universal 订阅。要订购或下载 SDK，请访问 http://www.microsoft.com/download/platformsdk/sdkupdate/。

## 应用构建工具

Windows Platform SDK 包含几类工具来帮助构建应用程序，包括：
- 加密，用于创建和管理证书。
- Microsoft `DirectX®` 应用程序接口，用于管理三维模型、图形和 DirectX 设备。
- 消息 API (`MAPI`)，用于消息、地址簿和其他查看器。
- 用于 AVI 编辑器的多媒体工具。
- 用于 OLE 对象和文件查看器的 OLE DB 以及 `MIDL` 编译器。
- 用于编辑器和资源编译器的资源文件。
- 电话 API (`TAPI`)，用于 TAPI 浏览器。

## UNIX 应用程序迁移指南

- 文本文件，用于识别差异。
- Windows Sockets，用于服务提供排序。

大多数迁移项目严重依赖文本文件工具。例如，`WinDiff` 是一个用于比较文件和目录的图形化工具，如果需要，可以递归比较。带有差异的文件可以通过颜色高亮不同行进行检查。另一个实用工具是 `Where`，它可以通过名称或模式在目录或子目录中查找文件。

Platform SDK 还包含 Windows Script 技术，包括 JavaScript 和 Microsoft Visual Basic Scripting Edition（`VBScript`）引擎。JavaScript 是 ECMAScript 或 JavaScript 的实现。`VBScript` 基于 Visual Basic。JavaScript 和 `VBScript` 引擎运行在 Windows Script Host 的上下文中，Windows Host 允许脚本从命令行或 Windows 环境运行。脚本可以以批模式运行且不需要用户输入。脚本还可以使用 Windows Script Host 提供的对象来访问操作系统资源，如文件。

## 调试工具

调试器可以设置断点、逐行执行并检查内存。平台 中的调试器有：
- 用户模式。
- 内核模式。

Platform SDK 还包含：
- `Spy` (`Spy.exe`)
- `Object` (`WinObj.exe`)

## 性能监控与调优

Visual Studio 包含了一些有助于提高性能的工具。本节讨论了：
- 属性标记分析器 (`CAP`)
- 性能计数器 (`Perfmtr`)
- 工作集调优器 (`WST`)

属性标记分析器 (`CAP`) 是一个普通工具，从命令行运行。为了控制分析的粒度，您指定要包含哪些函数：
- 可执行文件 (`.exe`)
- `DLL`
- 基于 Windows

`Perfmtr` 以文本显示信息，如表 7.1 所示。

### 表 7.1 Perfmtr 键盘命令

| 键 | 显示 | 键 | 显示 |
| :--- | :--- | :--- | :--- |
| C | CPU 使用率 | I | I/O 使用率 |
| V | 虚拟内存使用率 | X | X86 统计数据 |
| F | 文件缓存使用率 | S | 服务器统计数据 |
| R | 读写操作 | H | 重复信息 |
| P | 池使用率 | Q | 退出工具 |

`Pstat` 显示进程统计数据。根据指定的选项，输出可以：
- 每个地址及其大小、状态、保护和类型。
- 可执行文件的提交内存。
- 每个 `DLL` 的提交内存。
- 映射提交内存。
- 预留内存。
- 关于工作集的信息。
- 关于分页池和非分页池使用的信息。

注意：由于 `VADump` 会产生大量输出，建议将其重定向到文件。

工作集调优器 (`WST`) 减少程序使用的内存。`WST` 可以帮助程序与其他程序共存，并缩短加载应用程序的时间。

程序的工作集由从地址空间映射到进程活动物理内存的页面组成。它包括私有数据和共享数据（程序代码，包括可执行文件、`DLL` 和系统 `DLL`）。

## 编译器选项

编译器选项包括：
- 优化选项：用于开启或关闭优化。
- 代码生成选项：识别特定能力，例如结构化异常处理 (`SEH`) 模型和处理器。
- 输出文件：指定输出文件的名称，例如可执行文件和调试信息输出文件。
- 调试选项：为调试信息的输出设置偏好。
- 预处理器选项：设置，例如文件位置和定义常量。
- 语言选项：启用或禁用语言扩展。
- 链接选项：启用 `DLL` 输出、线程模型等。
- 预编译头文件选项：包括编译速度。
- 杂项选项：包括帮助、不链接进行编译等。

## 调试

针对 C/C++ 和 Visual Basic 的每个内置 Visual Studio 调试器在 Visual Studio IDE 中都有其自己的窗口。这些窗口中的许多一个可以停靠（即附在主 IDE 窗口的侧边），也可以可以浮动在 IDE 窗口之上。

## 性能调优

Visual Studio 包含了分析应用程序性能的工具，包括：
- `PView`
- `Profiler`
- `Spy++`

`PView` 进程查看器使用对话框来查看和修改运行中的进程及其线程。

`PView` 可以监控：
- 进程、线程以及单个 `DLL` 的内存使用。
- 进程和线程使用的 CPU 时间。
- 应用程序或系统在不同优先级下的运行情况。

> 注意：`PView` 功能提供了强大的工具，开发者可以在不同的优先级下监控应用程序的进程和线程。更改优先级可能会影响运行在同一系统上的其他应用程序。开发者在使用 `PView` 时需要考虑这一点。

`Profiler` 帮助在函数级或单行源代码层级上分析程序执行情况。`Profiler` 可以帮助确定哪些代码部分执行时间较长，哪些部分被执行了多次。

`Profiler` 可用于：
- 统计函数被调用的次数。如果测试数据显示函数调用的次数过多或过少，则应用程序代码可能存在错误。
- 确定函数消耗的时间。如果一个函数的执行时间过长，可能是算法效率低下的问题。
- 通过验证所有函数是否被调用或调用的次数是否正确，来确定测试过程的覆盖率。

`Spy++` (`Spyxx.exe`) 具有系统进程、线程、窗口和窗口消息的图形视图。`Spy++` 具有工具栏、快速导航的超链接、用于轻松选择的窗口查找工具以及用于自定义视图窗口的字体对话框。`Spy++` 还会保存和恢复用户偏好。

## Visual Studio 的第三方扩展

与 Microsoft Studio 集成以检测运行时错误的第三方工具包括来自 Compware 的 `BoundsChecker` 和来自 Rational Software 的 `PurifyPlus`。

`BoundsChecker` 运行时错误检测工具，最初是一个单一产品。它现在是 `DevPartner Studio` 套件的一部分，该套件包含了性能和调试工具。

`BoundsChecker` 可以诊断 C++ 特有的问题，例如栈和堆内存错误，以及内存和资源的泄漏。`BoundsChecker` 通过检查 `Win32`、`ODBC` 和 Internet 等 API 调用，消除了常见的 Windows 参数不匹配问题。

`PurifyPlus` 包含了用于检测错误和内存问题的工具 `Purify`，以及用于分析瓶颈和检测未被发现代码的性能工具。`PurifyPlus` 检查 API 调用中的错误，包括 `Win32`、`ActiveX`、`COM` 对象和 `DLL`。`PurifyPlus` 可检测 C++ 内存问题，如堆和栈错误、指针错误、内存使用错误和句柄错误。`PurifyPlus` 可以在 Visual Studio IDE 之外工作，进行独立调试。

MKS Software 提供了一个 Visual Studio 6.0 的扩展以支持 `lex` 和 `yacc` 实用程序。`lex` 是一种扫描实用程序，用于分析输入文件中是否出现预定义的标记（tokens）。当找到模式时，会运行一组 C 源代码。`lex` 实用从指定的输入文件或标准输入读取输入。输入以对的形式存在，首先是用于扫描的表达式，然后是找到文本表达式后要执行的 C 代码。`lex` 实用产生一个 C 源文件，通过编译来创建扫描程序。

`yacc`（另一个编译器）实用程序是一个解析器，它接收设置的输入标记并对该标记应用一组语法规则。`yacc` 实用根据从输入文件或标准输入的语法规则生成一个 C 程序。

C 程序根据运行 `yacc` 时提供的语法规则解析输入。

`lex` 和 `yacc` 的结合为开发者提供了一种生成编译器、编译器前端处理器、文本处理器和语言翻译器的强大方法。`lex` 实用程序执行基于正则表达式创建标记的功能；`yacc` 则在标记上执行语法规则。

Mks 的 `lex` 和 `yacc` 实用程序作为 Visual Studio 6.0 的插件工作，允许开发者在 Visual Studio 6.0 IDE 内创建扫描器和解析器。这些有助于在 Visual Studio 6.0 内自动化耗时且单调的词法分析和语法匹配任务。

## 源码管理工具

源码管理工具可以集成到 Visual Studio IDE 中，以便开发者修改文件时执行自动检出（checkout）。与 Visual Studio 集成的源码管理工具具有点击式界面，这对于 UNIX 开发者来说可能是新的。

`Visual SourcesSafe` 是 Visual Studio IDE 自带的源码管理工具，它以树形结构创建项目。`Visual SourcesSafe` 为签入（check in）、检出（check out）和差异跟踪提供完整的源码控制。`Visual SourcesSafe` 使用 COM 自动化进行自定义。

自动化模型可以帮助源码从 UNIX 到 Windows 的迁移。与其他源码控制系统一样，提供了功能。

## 打包工具

一旦创建了应用程序，开发者就需要一种方法来分发它。这对于开发者来说是必不可少的。

`Visual SourcesSafe` 是 Visual Studio IDE 自带的源码管理工具，它以树形结构创建项目。`Visual SourcesSafe` 为签入、检出和差异跟踪提供完整的源码控制。`Visual SourcesSafe` 使用 COM 自动化进行自定义。

自动化模型可以帮助源码从 UNIX 到 Windows 的迁移。与其他源码控制系统一样，提供了功能。

## MSI 打包

`MSI` 通过一组编程 API 创建安装包。开发者可以使用 API 与 `MSI` 工作。然而，生成 `MSI` 脚本的工具可以实现这一过程。Microsoft SDK 提供了这样一个工具 - `Orca`。`Orca` 允许开发者直接编辑 `MSI` 数据库的内容。关于 `Orca` 的详细信息可以在 SDK 或 MSDN 网站找到。

第三方 Wise Solutions 和 InstallShield 产品进一步实现了 `MSI` 安装包的创建。这些工具允许开发者创建目标系统的“之前”快照。开发者可以手动安装包并拍摄系统的“之后”快照。差异变成了 `MSI` 包。

有关 `MSI` 的更多详细信息，请参见 Microsoft TechNet 网站。

## 跨平台包和库

从 UNIX 到 Windows 的应用程序迁移都需要 UNIX 开发环境和 Windows 开发环境之间的某些互操作。

重写为 `Win32` 需要的互操作最少。在这种情况下，代码直接移动到原生 Windows 环境，不再需要 UNIX 开发环境。在尺线的另一端，当移植的应用程序需要持续跨平台开发时，UNIX 和 Windows 开发环境必须良好集成。

第三方跨平台环境或工具包是维护多个版本 UNIX 和 Windows 操作系统上代码的流行解决方案。因为抽象层在这种情况下隔离了平台差异，用户在开发应用程序时不需要过多关注特定操作系统的代码。

环境影响对供应商的选择。有关互操作性的更多信息，请参阅第 6 章“UNIX 与 Windows 的互操作性”。

## Interix

`Interix` 是一种运行在运行 Windows 系统的计算机上的多用户 UNIX 环境。`Interix` 子系统及其配套工具提供了一个类似于任何其他 UNIX 系统的环境。它包含区分大小的文件名、作业控制、编译工具，以及 300 多个 UNIX 命令、实用程序和 shell 脚本。由于 `Interix` 子系统层叠在 Windows 内核之上，它在不进行任何仿真的情况下提供了真实的 UNIX 功能。（有关 `Interix` 的更多信息，请参阅第 4 章“评估与分析”。）

本节将讨论 `Interix` API、`Interix` 实用程序以及 `Interix` 的网络和安全问题。

## Interix APIs

`Interix` 包含一个软件开发包（`Interix SDK`），它提供了一套完整的 API（超过 1900 个）以及头文件和库文件，用于创建和迁移 UNIX 。

`Interix SDK` 包含以下类别 API 和服务的文档和头文件：
- `POSIX.1` API
- 加密
- 用户界面服务，包括 `curses`、终端程序和 X-Windows
- 数据库 (`dbm`)
- 远程过程调用 (`RPCs`)
- `Sockets`
- 内存映射通信 (`IPC`) 机制
- System V 进程间通信 (`IPC`)
- Berkeley 软件发行 (`BSD`) 字符串和内存函数
- 伪终端
- 控制终端
- 安全
- 设置与系统管理
- 工具与脚本

`Interix` 环境包含了 Korn shell 和 C shell，并提供了超过 300 多个 UNIX 实用程序。此外，`Interix` 还包含了常用的 UNIX 开发工具，如文本编辑器、`make` 实用程序、编译器、链接器、调试器和 shell 脚本。

### 7.2. Interix 包含的类 UNIX 开发工具

| 类别 | 工具 |
| --- | --- |
