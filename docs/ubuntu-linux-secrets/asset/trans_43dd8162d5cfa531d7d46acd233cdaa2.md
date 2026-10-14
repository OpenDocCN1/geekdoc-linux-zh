

## 表 28-1：（续）

| 程序 | 描述 |
|---|---|
| apt | 用于记录 Java 类方法的 Java 代码注释处理器 |
| jar | 将多个 Java 类合并为单个应用程序文件 |
| jarsigner | 签署 jar 文件 |
| java | 运行 Java 类文件 |
| javac | 将 Java 代码文件编译为可执行的 Java 类文件 |
| javadoc | 通过生成有关代码文件中使用 Java 函数的 HTML 格式页面来记录 Java 代码文件 |
| javah | 从 Java 代码生成 C 头文件和源文件 |
| javap | 将 Java 类文件反汇编为 Java 代码 |
| jconsole | 监控和管理正在运行的 Java 虚拟机实例 |
| jdb | Java 调试器 |
| jhat | 堆分析工具 |
| jmap | Java 内存映射器 |
| jps | Java 虚拟机进程状态工具 |
| jstat | 显示 Java 虚拟机统计信息 |

这些程序可以直接从命令行运行，但有几个图形化 Java 集成开发环境（IDE）包提供了对 OpenJDK 程序的图形前端（请参阅本章后面的“Eclipse”和“NetBeans”部分）。下一节将展示如何从基于文本和图形的环境中使用 OpenJDK 开发环境。

## Java 开发环境

Ubuntu 提供了多种帮助您开发 Java 应用程序的选项。最基本的是 OpenJDK 中的命令行 javac Java 编译器，它允许您直接在命令行上编译 Java 应用程序和小程序。Ubuntu 还提供了两个流行的 Java 图形 IDE 环境的访问权限，它们为编译、测试和调试 Java 程序提供图形界面：

- Sun Microsystems NetBeans IDE 包
- 开源 Eclipse IDE 包

每个包都为 OpenJDK Java 程序提供了一个图形化、基于窗口的前端。本节将介绍在 Ubuntu 工作站上使用 OpenJDK 命令行程序以及两个图形 IDE 包创建 Java 应用程序的基础知识。

## 命令行工具

Java 开发环境的核心是命令行。OpenJDK 包提供了多个命令行程序，用于直接从命令行处理 Java 程序。命令行 Java 工具最好的地方在于，您可以在几乎任何环境中使用它们，甚至在仅提供命令行界面的 Ubuntu 服务器上也是如此。本节将介绍您在 Ubuntu 中开发、运行和测试 Java 应用程序时将使用的基本工具。

### javac 程序

OpenJDK 提供的命令行 Java 编译器程序是 javac。它将 Java 源代码文件编译为可在任何平台的 JVM 上运行的 Java 类文件。您可以使用 javac 编译器创建 Java 应用程序和小程序。

javac 程序的格式为

```
javac [options] [sourcefiles] [@argfiles]
```

sourcefiles 参数是 javac 程序要编译的 Java 代码文件列表。（Java 程序通常由多个文件组成，需要编译成一个类文件。）

> Java 对源文件名格式要求非常严格。每个 Java 源文件必须以 .java 文件扩展名结尾，并且文件名必须与其中包含代码的 Java 类相匹配。
> 
> 更糟糕的是，Java 区分大小写，因此文件名的大小写必须与 Java 类的大小写相匹配。例如，如果代码文件包含 MyTestClass Java 类的代码，则文件必须命名为 MyTestClass.java。

argfiles 部分允许您列出一个或多个包含选项和源文件名的列表的文件。由于您必须根据 Java 类为源代码文件命名，因此 Java 项目通常会变得复杂，并且对于应用程序中使用的不同 Java 类有许多代码文件。每次编译项目时不必列出创建单个应用程序所需的所有代码文件，您可以创建一个文本文件，其中列出源文件名以及编译应用程序所需的任何选项。然后，您只需在 javac 编译器命令行中包含 argfile 名称，使用 @ 符号作为 argfile 名称的前缀即可。编译器会自动从 argfile 中提取选项和源文件名，并像您在命令行上输入信息一样处理它们。

javac 程序的 options 部分是可选的。提供了各种选项供您修改编译器的行为。选项分为两组：

- 标准选项：Java 语言通用的选项，并在所有 JVM 环境中使用
- 非标准选项：特定于特定 JVM 环境且在 Java 中不标准的选项

