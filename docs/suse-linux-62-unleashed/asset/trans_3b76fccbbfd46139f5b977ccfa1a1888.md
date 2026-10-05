

```python
#!/usr/bin/python
import os

def printenv(s):
    try:
        x = os.environ[s]
    except KeyError:
        print "No such environment var:", s
    else:
        print "Env var", s, "has value:", x

printenv("SHELL")
printenv("OSTYPE")
printenv("JUNK")
```

> 前述代码必须如所示进行缩进。Python 通过语句的缩进（执行脚本时）或空行（交互式运行时）来决定要执行的代码块的开始和结束。def;、try;、except; 和 else: 语句都有从属的代码块。

在你的系统上尝试这段代码。你几乎肯定拥有 SHELL 和 OSTYPE 环境变量，但可能没有 JUNK。

# Java 编程

本节作为 Java 编程语言和平台的简要介绍。Java 是最初由 Sun Microsystems, Inc. 开发的编程语言。Java 最初被称为 Green，后来改为 Oak，灵感来自其中一位设计者办公室窗外的一棵树。Java 最初的原意是为消费电子产品开发软件。当时的想法是录像机和微波炉使用了许多不同的微处理器和嵌入式操作系统。设计者认为必须有一种更简单的方法为这些设备开发软件，并最终让它们相互通信。

# SuSE Linux 编程工具
第25 章

这种解决方案最终被称为 Java。一旦互联网热潮来临，Java 就找到了新的用途。有人意识到互联网应用程序与消费电器面临相同的问题。许多不同的平台通过互联网和广域网相互连接，而 Java 通过允许它们共享和执行相同的编程指令进一步进一步连接了它们。

HTML 是平台无关的。无论你使用什么机器、操作系统或 Web 浏览器都没有关系。网页的超链接文本不断增长，需要更高级的世界网用户：来交付动态实时数据和应用程序。Java 的设计者决定将 Java 嵌入 Web 浏览器中，Java Applet 诞生了。现在，你可以加载嵌入用 Java 语言编写的小型、平台无关程序的 Java 页面。

# Java 的用途

Java 有许多用途。它提供了其他语言提供的许多功能，还是包含 Java Base API 的平台。Base API 设计为 Java 的一组通用 API。这些 API 由可重用的对象组成，大多数开发者在开发应用程序时都需要这些对象。

这组通用库进一步扩展了 Java 的用途。Java Base API 包含了网络、分发对象和数据库连接的库。Java Base API 还包含一个名为 Java Abstract Windowing Toolkit（AWT）的平台无关窗口工具包，用于编写图形用户界面。

Java 目前最大的动力似乎源于企业级。大公司似乎对其平台独立性和与其他环境的轻松集成感到惊讶。Java 正在快速成为解决复杂业务问题的解决方案。为 Java 开发的一些新 API 和规范使其成为理想选择。Java 可以通过 JDBC（Java 数据库连接）API 轻松地与现有数据库集成，现在像 Enterprise JavaBeans 这样的规范是围绕 CORBA（通用对象体系架构）等标准构建的，这些可以与现有系统集成。Enterprise Java Beans 是 Java 组件架构 Java Beans 的扩展。Enterprise Java Beans 通过使其具有分布式和持久化特性增强了 Java Beans。

# 注意

JavaScript 是由 Netscape 开发的脚本语言。JavaScript 通常用嵌入 HTML 的脚本使用，由 Web 浏览器解释。Java 和 JavaScript 是完全不同的。

![](img/cbac72550c7126a22162e94d91a0c360_842_0.png)

# 图形、多媒体和生产力工具
第四部分

Java 在 Web 应用中也找到了许多用途。Java 最初被宣传为可以在你的 Web 浏览器中运行的小型 applet，但越来越多的人发现 Java 可以通过 servlet 在服务端使用。这些 servlet 正在取代传统用 Perl 和 C/C++ 等语言编写的 Web 服务器 CGI 脚本。

# Java 虚拟机

运行 Java 平台的代码需要一种通常称为 Java 虚拟机（JVM）的软件。这段软件为特定平台的底层操作系统和硬件添加了抽象层。

许多语言被编译成可以直接在机器硬件上执行的机器码。这种编译是特定于平台的，因此结果只能在特定的的硬件上运行。例如，为 Windows 编译的 C 程序只能在 Windows 平台下运行。

# 字节码

让 Java 与许多其他技术区分开来的是？Java 没有编译成特定平台的机器码。Java 被编译成平台无关的字节码，这些是针对物理上不存在计算机的平台的指令。这些字节码被设计为在虚拟机上运行。

# JVM 如何保护底层操作系统环境

每个平台都有不同的 Java 虚拟机实现，所有实现都应该能够根据 Java 规范运行架构中立的字节码。这通过在虚拟机中隐藏底层系统细节，使得 Java 的移植性成为可能，并能够在无需重新编译的情况下在其他平台上运行 Java 应用程序。开发者可以在一个平台上编写并编译 Java 应用程序，然后在完全不同的平台上部署和运行它们。

> 支持 Java 的平台（不完全列表）

- Linux
- UNIX (Solaris, AIX, HP-UX, UNIXWare, IRIX 等等)
- Windows 95/98/NT
- IBM OS/390, OS/400, OS/2
- MacOS

SuSE Linux 编程工具
第25 章

# 应用程序与 Applet

应用程序和 applet 是可以在 Java 中运行的两种基本程序类型。Java 应用程序与用 C++、Visual Basic 或任何语言编写的应用程序非常。应用程序通常安装在你的工作站上并通过命令行执行。

另一方面，Java applet 是设计在 Web 浏览器中运行的小型程序，通过网络动态加载并在你的工作站上执行。Java applet 通常嵌入执行某些微小任务的网页中。

当用户编写 Java applet 时，他或她为 applet 添加了功能。Applet 对象是 Web 浏览器识别的通用 applet。扩展通用 Java applet 为你的 applet 提供了在丰富环境中运行的优势。

applet 的一个使其与应用程序非常重要的特性是其安全性。Java applet 运行在一个限制环境中。该环境防止 applet 在你的工作站上执行任何恶意行为，例如删除硬盘上的所有文件。

# 跨平台开发与专用开发

自从互联网演进以来，跨平台开发比任何时候都重要。我们正处于信息风潮之中。一夜之间，我们有了从家里办理银行业务的能力，这在几年前似乎只有银行家才能可行。我们可以交易股票、查询当前天气，并跟踪我们发出的包裹。

假设你登录网上网银行转账到你的支票账户。银行用于其信息系统的计算机、软件和架构通常与你使用的不同。你能想象为了从储蓄账户转账到支票账户而购买主机吗？你能想象银行必须为每种可用平台编写不同的应用程序以便你这吗？

