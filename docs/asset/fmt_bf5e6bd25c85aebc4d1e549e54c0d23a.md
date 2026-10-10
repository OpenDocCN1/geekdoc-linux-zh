
# cd /usr/local

# tar xvfz /tmp/jdk_1.1.7-v1a-glibc-x86.tar.gz

现在，你必须将 JDK 的 `bin` 目录添加到可执行搜索路径。如果你使用 `bash`，将此加入 `.bash_profile`：

```
export PATH=$usr/local/jdk117_v1a/bin
```

（你需要将 `jdk117_v1a` 更改为 `/usr/local` 创建的目录名称。）

## JDK 版本

三个版本的 JDK：`1.0`、`1.1` 和 `1.2`。

`JDK 1.0` 是原始版本；它现在已经过时，除非你对考古学感兴趣，否则你不需要在上面浪费时间。

`JDK 1.1` 是最广泛使用的。它经过了良好的测试和调试，极其稳定。

`JDK 1.2` 是最新版本。它相对于 `JDK 1.1` 的主要优势是更优化的 JVM 和更广泛的库。Sun 现在将 `JDK 1.2` 称为 Java 2 平台，并且在不久的将来，它将取代 `JDK 1.1` 成为最广泛使用的版本。

这个解释可能会给你留下一种印象，认为 Java 有许多互不兼容的版本，但事实并非如此。`JDK 1.0`、`JDK 1.1` 和 `JDK 1.2` 之间的大多数变化只是实现上的改进以及标准库的增加。几乎所有为 `JDK 1.0` 编写的代码在 `JDK 1.2` 上仍然可以运行。你甚至不需要重新编译它。

## 开发环境

第四部分
PART IV

一旦你解压了压缩文件并更新了可执行文件搜索路径，就可以执行此命令来测试一切是否正常：

当然，显示的版本应该与你下载的版本对应。

## 编译和运行程序

使用你最喜欢的文本编辑器（如果你还没有喜爱的编辑器，`emacs` 是一个不错的选择），输入以下程序并将其保存为名为 `Example1.java` 的文件。该程序将在屏幕上显示一条简单的消息。

```java
public class Example1 {
    public static void main(String[] args[]) {
        System.out.println("Hello World!");
    }
}
```

现在，在命令行提示符上输入以下命令进行编译：

```bash
$ javac Example1.java
$
```

如果你没有犯任何输入错误，编译器会创建一个 `Example1.class` 文件，其中包含你程序的 Java 字节码。要执行它，你只需要调用 JVM，如下：

```
$ java Example1
Hello World!
$
```

现在，使用 JVM 的详细选项 `-v` 来查看它如何在运行时动态加载类。在命令行提示符上输入：

```bash
$ java -v Example1
[Loaded java/lang/Thread.class from /usr/java/bin../lib/classes.zip]
[Loaded java/lang/Object.class from /usr/java/bin../lib/classes.zip]
[Loaded java/lang/Class.class from /usr/java/bin../lib/classes.zip]
....（为了简洁省略了一些行）
[Loaded java/io/BufferedWriter.class from /usr/java/bin../lib/classes.zip]
[Loaded java/lang/Compiler.class from /usr/java/bin../lib/classes.zip]
[Loaded ./Example1.class]
Hello World!
```

## Java 编程

第 25 章

你在输入命令的窗口中看到的滚动内容是 JVM 为了运行你的程序需要加载的 Java 运行时类列表。你会最后加载的一个类是 `Example1.class`，它在显示“Hello World!”消息之前。

我们对 `Example1.java` 做了微小的修改，以查看动态加载的一个更有趣的示例。通过在打印问候语句的行之后添加新行来修改 `Example1.java`。修改后，程序应该像这样：

```java
public class Example1 {
    public static void main(String args[]) {
        System.out.println("Hello World!");
        System.out.println(2000.0);
    }
}
```

确保你没有将数字放在引号之间。

现在，使用 `-v` 选项编译并执行它：

```bash
$ java -v Example1
[Loaded java/lang/Thread.class from /usr/java/bin/../lib/classes.zip]
[Loaded java/lang/Object.class from /usr/java/bin/../lib/classes.zip]
[Loaded java/lang/Class.class from /usr/java/bin/../lib/classes.zip]
...（为了简洁省略了一些行）
[Loaded java/io/BufferedWriter.class from /usr/java/bin/../lib/classes.zip]
[Loaded java/lang/Compiler.class from /usr/java/bin/../lib/classes.zip]
[Loaded Example1.class]
Hello World!
[Loaded java/lang/FloatingDecimal.class from /usr/java/bin/../lib/classes.zip]
[Loaded java/lang/Double.class from /usr/java/bin/../lib/classes.zip]
2000.0
```
