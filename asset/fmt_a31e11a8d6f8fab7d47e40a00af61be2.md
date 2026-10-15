
Java 1.2 最大的增加是引入 JFC（Java 基础类）作为 Base API 的一部分。新的 JFC 功能包括 Swing GUI 工具包、Java 2D API、应用程序服务（Application Services）、辅助功能（Accessibility）以及拖放功能。其他增强特性还包括基于策略的安全性、弱引用、Java IDL API 以及一系列性能增强。

# 软件开发工具包（Java 开发工具包）

每个 Java 开发者的良好起点是 Sun 的 Java 开发工具包。这是你开始 Java 开发的基础工具包，几乎可以在每个平台上运行。JDK 包含了开发者编译、调试和运行使用 Java 编写的 applet 所需的软件和工具。JDK 还包含文档和示例帮助你入门。Linux 移植由 Blackdown 团队完成。在他们的网站上可以找到大量信息，包括最新版本的移植版，你可以下载：http://www.blackdown.org。

与其他平台相比，Linux 平台上的 Java 开发工具仍然比较简陋，但 Linux 操作系统正在迅速发展，每天都有新的开发工具涌现。Sun 麦基系统公司有自己的 Java IDE —— Java Workshop，它可以通过补丁在 Linux 下运行。IBM 正在处理将其的 IBM Visual Age for IDE 移植到 Linux。

IBM 研究还将其开源 Java 代码编译器（Jikes）移植到了 Linux。Sun 的 JDK 代码编译器 `javac` 是是用 Java 语言本身编写的。相比之下，Jikes 用原生 C++ 编写的。根据 Java 语言规范，Jikes 承诺将是一个速度快得多且更准确的编译器。关于该项目的更多信息可以在 http://www.ibm.com/research/jikes/ 找到。

## SuSE Linux 编程工具

你也可以在 http://www.alphaWorks.ibm.com/tech/linux.JVM 获取 IBM 移植版的 JDK 早期版本。

## Java 解释器

Blackdown 移植的 Java 开发工具包还包含了 Sun 麦基系统公司 Java 字节码解释器的移植。Blackdown 移植版还有几个 JIT 可用。较新的 JDK 1.2 版本将包含 JIT。即时编译（Just In Time compilation）是一种用于加速虚拟机字节码执行的技术。JIT 不再解释 Java 字节码，而是直接将字节码翻译成原生代码，使代码执行运行快得多。

TYA 即时编译器是 JDK Linux 移植版的 100% 非官方 JIT，可以与 Blackdown 移植版的 JDK 1.1 使用。可以在 Blackdown 网站上找到 TYA JIT。

还存在几个从头开始的包含 JIT 技术的开源 Java 虚拟机。其中一个实现是 Kaffe。更多信息位于 http://www.kaffe.org。

## Java 语言概览

根据 Sun 麦基系统公司 Inc. 的一份早期白皮书《Java 语言：概述》，Java 语言是“一种简单的、面向对象的、精通网络的、解释型的、健壮的、安全的、架构中性的、可移植的、高性能的、多线程的动态语言”。这里有很多术语，但这是一个很好的描述。

Java 是简单的。它在语法上与 C++ 非常相似，但省略了许多很少使用或似乎没有用的特性。

Java 是面向对象的。Java 允许通过类来编写代码。

Java 是面向对象的。Java 使用封装技术来隐藏细节。

Java 是精通网络的。Java 设计用于网络环境，如 TCP/IP 和 HTTP。

Java 是健壮的。Java 在编译时进行强类型检查。Java 具有自动垃圾回收机制。

Java 是安全的。Java 可以在沙箱中运行以保护工作。

Java 是架构中性的。Java 程序被编译成与平台无关的字节码。Java 是多线程。允许同时处理多个任务。

## 编写 Java 程序

你可以编写的最简单程序可能是 Hello World。Java 程序需要一个入口，因此你必须定义 `main` 方法。

```
class HelloWorld {
    public static void main(String args[]) {
        System.out.println("Hello World!");
    }
}
```

为了让你的代码更易编写，Java 允许在源码中使用注释（见表 25.3）。

### 编辑

可以使用任何编辑器编辑 Java 代码，就像 C 或 C++ 一样。在 Unix 类平台上常用的编辑器是 `vi` 编辑器。`Emacs` 是另一个流行的编辑器。`Emacs` 的一个精彩功能是 Java 模式，可以格式化你的代码。

Java 编译器通过扩展名 `.java` 识别 Java 源文件。多个 Java 类可以放入一个 `.java` 文件，但每个文件只能包含一个公共类。文件名必须与文件中的公共类相同。

### 表 25.3 注释

| 注释类型 | 描述 |
| --- | --- |
| /* */ | C 风格注释。/* 和 */ 之间的内容会被编译器忽略。 |
| // | C++ 风格注释。// 之后到行尾的内容会被编译器忽略。 |
| /** */ | 与 C 风格注释相同，但可以使用 JDK 提供的 `javadoc` 工具从源码中创建实用的文档。 |

你不需要为构造函数指定返回类型，因为返回类型始终被理解为该类实例的引用。此外，构造函数的名称与类名相同。

### 编译 Java 源代码

Java 源代码是针对 Java 编译的。源代码需要通过 Java 字节码编译器翻译成字节码。这最常见的是使用 Sun JDK 字节码编译器完成。其他可用工具，例如 Likes。IDE 的 Java Workshop 也会为你进行字节码编译。

JDK 中包含的 `javac` 字节码编译器接受扩展名为 `*.java*` 的输入文件。要编译 HelloWorld 示例，你可以在 Linux shell 命令行中输入：

```bash
# javac HelloWorld.java
```

> 注意

在为 SuSE Linux 安装 Java 之后，`javac` 编译器位于 `/usr/lib/jdk1.7/bin` 目录下。

编译器会在 `HelloWorld.java` 文件相同的目录下生成一个名为 `HelloWorld.class` 的文件。这些是编译后的字节码类。即使一个文件包含多个类或内部类，Java 也会为每个类创建一个 `.class` 文件。你可以在 Linux 命令行 shell 中输入以下命令来快速获取 `javac` 编译器的帮助：

```bash
# javac -h
```

### 创建和运行应用程序

Java 应用需要一个特殊的类入口点。这个入口点是 `main` 方法。Java 解释器会调用此方法并传递一个命令行参数数组。

```java
public static void main(String args[]) {
  ...
}
```

Java 解释器 (`java`) 运行独立的 Java 可执行程序。应用程序通常从命令行运行：

```bash
# java Options Classname
```

要运行 HelloWorld 类，请运行 Java 解释器并指定你想让运行的程序类名。Linux 内核也可以配置为自动运行解释器。

```bash
# java HelloWorld
```

> 注意

Java 解释器要求定义了 `main` 方法的类。任何类必须包含一个 `main` 方法。

#### 总结

本章介绍了 Linux 上最流行的编程工具的一些基本功能。每个软件工具都有特定的优缺点，但几乎所有工具都是健壮且成熟的。正如你所看到的，你将拥有丰富的软件用于开发程序或管理系统。

# 第 26 章

## Linux 图形应用程序

本章内容

- Linux 图形应用程序 818
- 图形文件格式 818
- 转换图形 819
- 编辑图形 820
- 创建图形 827
- 显示和打印图形 835

图形有趣之处在于，它的市场比许多其他 Linux 应用更广泛。图形工具涵盖了从简单的画图程序到高度复杂的图形程序，后者可以与甚至超过其他操作系统上的商业软件包相媲美。

这意味着 Linux 图形环境可以帮助：

- 孩子们学习颜色以及如何使用简单的绘图工具
- 需要工具制作图形布局和宣传册的小型企业
- 严谨的图形艺术家，他们需要最先进的工具来创作复杂作品，且不会在质量上做出妥协

本章涵盖了如何使用 Linux 下可用的流行工具进行图形的转换、编辑和创建。其他工具（如办公套件）仅从生成演示文稿或幻灯片的角度进行了介绍。关于办公套件的完整覆盖请参阅第 28 章“Linux 生产力客户端和套件”。本章提到的大多数图形软件包都是 SuSE Linux 6.2 的六张光盘套装，可以使用 YaST 工具或 RPM 包管理器进行安装。

## Linux 图形应用程序
