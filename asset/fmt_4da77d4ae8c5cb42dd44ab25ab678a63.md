
正因如此，Kylix 提供了 Web 服务导入器（Web Services Importer）。Web 服务导入器连接到 WSDL 文件，并根据 WSDL 文件生成 Kylix 接口和类型。一旦声明了接口，Kylix 就可以将任何客户端应用程序绑定到该服务，仿佛它是在 Kylix 环境中创建的一样。

![](img/d784fa8294cae585d61ec86b987ea212_606_0.png)

图 24-4：

导入外部 Web 服务

下面列出了 Web 服务导入器生成的 Kylix 代码。此功能对于开发者来说是巨大的帮助，否则他们将被迫自己解析 WSDL 并自行生成 Kylix 接口。

> 提示：除了从现有 WSDL 生成接口外，Web 服务导入器还会为 WSDL 中声明的任何类型生成类型声明。它们作为远程对象（`TRemotal` objects）创建，并可以在任何客户端中使用，即使它们最初不是在 Kylix 中创建的。

`Unit FedExClient;`

`interface uses Types, XSBuiltIns;`

```
type
FedTrackerTrackerType = interface(IIInvokable)
['1A17689B-D033-40E6-A39A-4DEEE9F65875']
function getStatus(const trackingNumber: WideString): WideString;stdcall;
```

`implementation`

`uses InvokeRegistry;`

`initialization`

`InvRegistry.RegisterInterface(TypeInfo(FedTrackerPortType), '', '');`

`end.`

一旦生成了接口，只需在客户端中使用它并像以前一样构建客户端即可。因此，即使 Web 服务应用程序不是用 Kylix 编写的（FedEx 服务并非如此），

```
procedure TfmTracker.BtnStatusClick(Sender:Object);
begin
edtStatus.Text := InvRegistry.getStatus(Pkg);
end;
```

## 总结

虽然本章涵盖了 Web 服务的各种用法，但这只是开始。分布式计算允许应用程序跨计算机运行。Kylix 通过让网络透明化，使得 Web 服务的调用变得快速且简单。Web 服务在技术上实际上是中间件。解决这些问题的解决方案之一（与所有解决方案一样）被称为通用对象架构。换句话说，CORBA 是中间件。

# 第 25 章 使用 VisiBroker 进行 CORBA 开发

## 引言

### 应用程序开发

在不同平台上的许多应用程序不断交互。例如，CORBA 架构。在理想世界中，这些应用程序不再是孤立的。在现实生活中，企业没有资源重写所有系统。

## 分布式计算背景

分布式计算的基本思想是将应用程序划分到多个计算机。从客户端的角度来看，程序似乎是在本地执行的。网络上服务器的实际执行通常通过以下步骤完成：

- 客户端封装程序和任何参数。
- 客户端将包发送到服务器。
- 服务器解码包。
- 服务器执行请求的程序。
- 服务器封装任何返回信息。
- 服务器将包发送给客户端。
- 客户端解码包。

应用程序最初通信的方法是使用 TCP/IP Socket。Socket 提供了系统之间发送信息的快速方法，但它们需要应用程序理解、解码并解释传递的消息。在处理如 Intel 和 Motorola 等架构时，字节序问题会变得棘手。远程过程调用（RPC）构建在 Socket 之上提供了一个名为外部数据表示（XRD）的架构层。该层处理数据的传输（打包），采用 Intel 和 Motorola 以及其他系统可以正确解释的格式。

Socket 和 RPC 在今天被广泛使用。然而，它们都采用过程方法而非面向对象的方法。此外，负载均衡和故障转移等企业功能需要额外的代码。

解决这些问题的解决方案之一（与所有一样）是通用对象架构（CORBA）。CORBA 是由对象管理组（OMG）管理的分布式架构。CORBA 的主要目的是为允许应用程序在网络上运行提供供应商、平台和语言无关的架构和基础设施。句话之，CORBA 是中间件。

> 注意：中间件是一个通用术语，指位于应用程序和网络之间的软件层，为不同平台上的许多应用程序提供交互。其他形式的中间件包括 Enterprise JavaBeans、RPC、面向消息的中间件（MOM）和分布式组件模型（DCOM）。

Kylix 为快速方便创建分布式应用程序所需的工具。虽然 Kylix 可以与 RPC 和 Socket 使用，但本章重点是 CORBA。

## CORBA 基础

CORBA 的核心是对象请求代理（ORB）。一个或多个 ORB 位于网络，为应用程序提供服务。ORB 由 Borland（Visigenic）和 IONA（Orbix）等供应商编写。

CORBA 应用程序由一个多个 CORBA 组件组成。这些组件不是拖到表单上的那种。相反，

# Kylix 2 开发第 25 章：使用 VisiBroker 4.5 为 Kylix 5 进行 CORBA 开发

它们是可以在网络上与其它 CORBA 组件通信的代码段。从一个简单的角度来看，客户端请求服务器组件的服务。

在客户端/服务器模型中，客户端直接与服务器通信。CORBA 应用程序并非如此，因为客户端和服务器之间并不直接相互通信。相反，它们通过称为存根（stubs）和骨架（skeletons）的代理对象进行通信。这些对象代表了客户端和服务器对象所暴露的接口。见图 25-1。

![](img/d784fa8294cae585d61ec86b987ea212_611_0.png)

当客户端调用服务器的方法时，看起来客户端正在直接与服务器通信。然而，实际上，客户端调用存根代理，代理与 ORB 通信，调用骨架代理，并调用服务器内部的方法。任何需要返回给客户端的信息都通过反向该过程完成。

## CORBA 独立性

CORBA 最大的优势是独立性。CORBA 不依赖于任何特定平台、供应商或语言。此外，它是分布式对象之间通信的 ISO 标准。

平台和供应商的独立性通过使用名为 `IIOP` 的标准 CORBA 协议在位于网络上的 ORB 之间通信来实现。语言独立性通过使用接口定义语言（IDL）描述 CORBA 对象的接口、类型和其他元素来实现。IDL 存在多种语言如 C、C++、Java、COBOL、Smalltalk、Ada、Lisp、Python 和 IDLscript 的映射。

# 第 25 章：使用 VisiBroker 4.5 为 Kylix 进行 CORBA 开发

Kylix 提供了从 IDL 到 Object Pascal 的映射。事实上，`IDL2Pas` 工具提供了一种简单方便的方法，用于生成编写客户端和服务器应用程序所需的代码。本章稍后部分将详细讨论 `IDL2Pas` 工具。

## IDL 元素

IDL 有许多元素。本节将讨论主要元素以及它们如何映射到 Object Pascal。在本节末尾显示了一个演示每个元素的示例。另一个需要注意的项是，IDL 看起来类似于 C 编程语言。事实上，IDL 也有一个处理器，可以在需要时包含其他 IDL 文件和类型定义（或别名）。

### 注释

可以使用传统的 C 风格 (`/* */`) 或 C++ 风格 (`//`) 在 IDL 文件中放置注释。

### 模块 (Modules)

模块相当于 Object Pascal 中的单元（unit）。对于 IDL 文件中的的每个模块，都会创建一个包含相应映射元素的新单元。

### 接口 (Interface)

接口描述了可调用的操作或服务。相应的，它映射到 Kylix 中的接口。一个模块可以包含零或多个接口。拥有没有接口的 IDL 文件的原因之一是提供 C 编程语言中头文件的等物。

### 常量 (Constants)

常量提供定义不变值的方法。使用关键字 `const` 来表示常量。如所预期，IDL 常量映射到 Pascal 常量，位于单元的接口部分。对于定义在接口内的常量，会在常量名称开头添加下划线 (`_`)。

### 类型 (Types)

类型指的是数据结构。类型有四类——数据类型、构造类型、模板类型和复杂类型。将在接下来的章节中进行解释。

### 基本类型

基本类型或数据类型指的是简单的数据类型，如布尔值、整数、浮点数、字符串和“any”类型。下表列出了基本数据类型。

表 25-1

| IDL 数据类型 | Pascal 映射 |
| :--- | :--- |
| `float` | `Single` |
| `double` | `Double` |
| `long double` | `Extended` |
| `long` | `Integer` |
| `short` | `SmallInt` |
| `long long` | `Int64` |
| `unsigned long` | `Cardinal` |
| `unsigned short` | `Word` |
| `unsigned long long` | `Int64` |
| `char` | `Char` |
| `wchar` | `WideChar` |
| `boolean` | `Boolean` |
