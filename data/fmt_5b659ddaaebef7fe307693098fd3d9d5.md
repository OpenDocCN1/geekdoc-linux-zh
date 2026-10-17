
默认情况下，文件安装在`/usr/java/j2sdk1.4.0/`目录下。`/usr/java/j2sdk1.4.0/bin`目录包含了该 SDK 的所有二进制文件。

## 9.4.3 创建 Jar 文件

`jar`工具用于创建 jar 类归档。它可以接受多个类文件，将它们进行压缩并放入单个`.jar`文件中。`jar`工具的语法与 Linux 和其他 UNIX 系统上广泛使用的`tar`程序类似。以下命令从两个类`first.class`和`second.class`创建`myclasses.jar`。

```
jar cvf myclasses.jar first.class second.class
```

你还可以从现有的`.jar`文件中添加或提取类。以下命令将`third.class`添加到`myclasses.jar`归档中。

```
jar uf myclasses.jar third.class
```

以下命令将从`myclasses.jar`文件中提取`second.class`。

```
jar x second.class
```

你也可以在`jar`命令中使用通配符。如果你使用目录名，该目录中的所有文件都将添加到`.jar`文件中。

要列出`.jar`文件中的所有文件，请使用`t`命令行选项。以下命令列出`myclasses.jar`文件中的所有文件。

```
jar tf myclasses.jar *
```

## 构建 Java 应用程序

Java 是一种编译后的 Java 程序，可以使用 Java 虚拟机执行。创建 Java 应用程序有三个基本步骤。这些步骤是：

- 1. 创建源代码。
- 2. 编译它。
- 3. 使用虚拟机运行它。

让我们看看如何完成这些步骤。

### 9.5.1 创建源代码文件

与其他任何编程语言一样，Java 源代码文件是使用编辑器创建的。这些源代码文件包含 Java 指令。简单的源代码文件包含一条打印“Hello World”消息的指令，类似于你的第一个 C 程序。请注意，本章中的 Java 示例仅用于演示如何使用开发工具。下面显示了打印“Hello World”消息的程序：

```
class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

程序必须有一个`main()`函数，就像 C 程序一样。程序可以保存为`HelloWorld.java`文本文件。

注意，你可以使用任何编辑器创建源代码文件。我建议使用你在第 2 章已经学过的 Emacs。Emacs 理解 Java 编程语言语法。你还可以使用其他 GUI 编辑器和集成开发环境`IDE`包来创建源代码。

### 9.5.2 编译 Java 代码

Java 编译器将把 Java 代码编译为可执行文件。以下命令从源代码文件`HelloWorld.java`创建输出文件`HelloWorld.class`。

```
/usr/java/j2sdk1.4.0/bin/javac HelloWorld.java
```

注意，输出文件名与包含`main()`函数的类相同。你可以使用`file`命令检查输出文件的类型。以下命令显示输出文件的类型为编译后的类数据。

```
[root@desktop /root]# file HelloWorld.class
HelloWorldorld.class: compiled Java class data, version 46.0
[root@desktop /root]#
```

## 构建 Applet

注意，在大型项目中，可能会有很多源代码文件、类文件和其他对象代码文件来生成输出的可执行文件。在这种情况下，你通常不使用 Java 编译器编译单个文件。执行此类任务的最佳方法是使用你在书中之前已经学过的`make`工具。

### 9.5.3 运行 Java 应用程序

Java 应用程序运行在 Java 虚拟机之上。你在上一节中创建的“Hello World”应用程序可以使用 Java 虚拟机执行。

```
[root@desktop /root]# Java HelloWorld
Hello World!
[root@desktop /root]#
```

注意，当你运行此应用程序时，不要在命令行中使用`HelloWorld.class`。如果你 true这样做，Java 虚拟机将无法执行该命令。我在邮件列表和新闻组中见过许多人犯这个错误，并纳闷他们为什么会收到错误消息。

### 9.5.4 使用 gcj 构建 Java 应用程序

`gcj`编译器是 GCC 编译器套的一部分。它能够编译 Java 语言程序。使用`gcj`编译 Java 程序的一个优点是，你可以创建可执行的应用程序，而不是 Java 字节码。这些应用程序可以在 Linux 上执行，而不需要 Java 虚拟机。缺点是，你只能在你编译的平台上执行此类构建的应用程序。这与 Java 基本的一次编译，处处运行的理念相反。关于使用`gcj`的详细信息请见其网站 http://gcc.gnu.org/java/。

你可以对使用`gcj`的程序使用 Gnu 调试器，这对许多熟悉`gcj`的程序员来说是一个巨大的优势。要能够用`gcj`编译程序，你的系统中必须可用`libgcj`。`libgcj`提供了类库，但在运行时提供代码解释器和垃圾回收器。可以使用最新版本的`libgcj`。

# Java 的 Jikes

Jikes 常见问题解答（FAQ）也可以在上述网站找到。由于 Jikes 是一个命令行编译器，它可以用于大型项目的 Makefile 中。可以使用以下命令调用编译器，以及 Jikes 的可用选项：

```
[root@conformix jikes-1.15]# jikes
```

Jikes 编译器

(C) 版所有 IBM Corp. 1997, 2001.

- 许可材料 - IBM 软件财产 - 版权所有。

```
use: jikes [-classpath path] [-classpath path][-d dir][-
debug][-depend][-Xdepend][-deprecation][-encoding encoding][-
extdirs path] [-g][-nowarn][-nowwrite][-O][-sourcepath path][-
verse]-
Xdout][+][+][B][C+][OLDCSO][-D][+DR=filename][+E][+F][+Name=TypeKeyword]+M][P][Td..d][+U][Z] file.java...
```

- `-bootstrap path` 将路径前置于 CLASSPATH 之前
- `-classpath path` 使用路径作为 CLASSPATH
- `-d dir` 在目录 dir 中写入类文件
- `-debug` 无影响（为了兼容性而识别）
- `-depend -Xdepend` 编译所有使用的类
- `-deprecation` 报告已弃功能的使用；使用指定的编码读取源文件
- `-extdirs path` 将路径中所有 zip 文件前置于 CLASSPATH 之前
- `-g` 调试（生成 LocalVariableTable）
- `-nowarn` 不发布警告信息
- `-nowwrite` 不写入任何类文件
- `-O` 不写入 LineNumberTable
- `-sourcepath` 同时在路径列表中搜索源文件；列出读取和写入的文件
- `-verbose` 将输出列表重定向到 stdout
- `-++` 在增量模式下编译
- `+-B` 不调用字节码生成器
- `+-C` 不丢弃词法器输出的 own
- `+-OLDCSO` 为了兼容性执行原始的 Jikes 类顺序
- `+-D` 立即以 emacs 格式报告错误，不进行缓冲处理
- `+-DR=filename` 在文件名中生成依赖报告
- `+-E` 以 emacs 格式列出错误
- `+-P` 除 Zip 和 Jar 文件外，进行完整的依赖检查
+ `-Kname=TypeKeyWord` 将名称映射到类型关键字
+ `-M` 生成 makefile 依赖关系
+ `-P` 严谨编译 - 会产生大量警告
+ `-Td..d` 设置制表 d...d 个空格的值；每个 d 是一个十进制
+ `-U` 进行包括 Zip 和 Jar 文件在依赖检查
+ `-Z` 将警告视为错误

版本 1.15 - 2001年9月26日

Jikes 最初由 IBM 研究的 Philippe Charles 和 David Shields 编写，现在由 Jikes 项目进行更频繁的维护和完善：

http://ibm.com/developerworks/opensource/jikes

请咨询此 URL 以获取更多信息并学习如何报告问题。

```
[root@conformix jikes-1.15]##
```

以下命令将编译 hello.java 程序以创建 hello.class 输出。

```
jikes hello.java -classpath /usr/java/j2sdk1.4.0/jre/lib/rt.jar
```

请注意，您的系统中可能安装了某些类以使用编译器。在上面的示例中，在命令行中提到了 classpath。

## 9.9 杂项

本节包含了与 Java 相关的其他领域的简要摘要和链接。在 Sun 和 IBM 等行业巨头的推动下，Java 技术正在向许多不同领域不断进。

### 9.9.1 嵌入式 Java

Sun 引入了 Java Embedded Server，它允许开发者基于 Java 平台构建嵌入式应用。除了其他内容外，它还包含了 SSL 的 Java 实现。关于嵌入式 Java 信息可以在 http://java.sun.com/prod/embeddedjava/ 获取。

### 9.9.2 实时 Java

人们正在努力实现 Java 虚拟机。实时 Java 的规范可以在 http://www.rtj.org/ 找到。规范包含了如何管理内存、中断、调度、垃圾回收等信息。

### 9.9.3 无线应用

Sun Microsystems 的 Java 2 微型版（J2ME）引入了无线 Java 技术。关于在无线应用中使用 Java 技术的信息，可以在 http://java.sun.com/products/embeddedjava/ 找到。

## 9.10 参考文献

- 1. Kaffe 可通过其网站 http://www.kaffe.org 获取
- 2. 大多数 Sun Java 信息可以通过 http://java.sun.com 获取
- 3. 非阻塞库位于 http://www.cs.berkeley.edu/~mdw/proj/java-nbio/
- 4. Jboss 可通过其网站 http://www.jboss.org/ 获取
- 5. sourceforge.net 上的 Jboss 信息 http://sourceforge.net/projects/jboss/
- 6. Java 语言规范位于 http://java.sun.com/docs/books/jlis/
- 7. Jikes 编译器位于 http://oss.software.ibm.com/developerworks/opensource/jikes/
- 8. gej 编译器信息位于 http://gcc.gnu.org/java/
- 9. libgcj 库来自 ftp://sourceware.cygnus.org/pub/java/
- 10. 实时 Java 规范位于 http://www.rtj.org/
- 11. 嵌入式 Java位于 http://java.sun.com/products/embeddedjava/

## Linux 开发工作站的典型硬件要求

选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux

## 附录 A Linux 开发工作站的典型硬件要求

### A.2 第 1 节：处理器与内存

有 Linux工作因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多因素。选择 Linux 开发工作站有许多

### A.3 第 2 节：磁盘驱动器

目前，个人电脑市场上有两种类型的驱动器：IDE 和 SCSI（读作 "scuzzy"）。第一种最常见的是 IDE 驱动器。这是大多数现成工作站配备的类型。标准计算机一次可以支持多四个 IDE 驱动器。这些驱动器可以是硬盘、CD-ROM、DVD 驱动器或磁带驱动器。一旦计算机中安装了最多四个设备，在移除其中一个之前就无法再添加。这以及由于 IDE 驱动器传统上比

## 任务规模评估

SCSI 驱动器是使用此类设备的主要限制。然而，它们比 SCSI 驱动器便宜，且安装也相对简单。

SCSI 设备也可用于大规模存储。除了 CD-ROM 和 DVD 驱动器，SCSI 设备还可以包括扫描仪、打印机和其他设备。

计算机内部的单个 SCSI 接口卡最多可以连接七个设备，且一台计算机可以拥有多个接口卡。一台计算机上安装的 SCSI 设备总数限于主板上可用接口槽的数量乘以七。在大多数现代工作站和服务器上，这将允许 SCSI 设备总数达到七个到三十多个不等。新的 SCSI 标准允许更多设备连接到单个 SCSI 适配器上。
