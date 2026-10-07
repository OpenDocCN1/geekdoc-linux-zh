

## 表 14.1 次级 jar 选项

| 选项 | 需要文件名 | 功能 |
| --- | --- | --- |
| -v |否 | 详细模式 |
| -0 (零) |否 | 不压缩 |
| -M |否 | 不创建清单文件 |
| -f | 是 | 指定要创建、提取等的 jar 文件 |
| -m | | 指定清单文件 |

次级选项所需的最后一个 jar 或清单文件名之后，命令行以一系列内容文件名列表 (*) 结束（例如我们示例中的 java in our example)）。这些是将被插入到归包中或从归包中提取的文件。如果你正在执行列出或提取操作，则不需要指定它们；如果没有出现文件名，则 jar 将列出或提取归包中的所有内容。如果你正在执行创建（create），列出的文件将被复制到新的归包中。如果你正在执行更新（update），列出的文件将被复制到现有的归包中。如果目录的内容将进行递归处理。

jar 文件可以出现在类路径中，代替目录名。因此，如果你创建了几个包含大量类文件的包，可以将它们作为一个单一 jar 归包发送给你的客户。客户可以在不提取归包的情况下使用它们，这比将所有内容保留在 jar 内部的替代方案要得多。将类留在 jar 中比提取它们的效率略低，因为 JVM 在加载它们之前必须先提取并解压它们。然而，这种效率的降低是非常微道的，且每个文件仅发生一次；类被加载后，其描述就在 JVM 内部，文件将不会被再次访问。

如果 jar 文件包含应用程序的名称，你可以使 jar 变得可执行。这对你的用户来说是一个很好的便利之处，因为有了可执行 jar，他们不需要记住主类的名称。要运行可执行 jar 文件，只需使用 -jar 选项并在 java 命令行上指定文件名，如下：

```
java -jar the_executable_archive.jar
```

要创建一个可执行 jar，首先要创建一个清单，告知哪个类文件是主类。要做到这一点，创建一个包含如下内容的行的文本文件：

Main-Class: x.y.MyMainClass

# 第 14 章 · 整合一切

注意你指定的是类名，而不是类文件名，所以没有 .class 后缀。要指定整个类名，包括包前缀（在本例中为 x.y）。该文本文件可以是任何名称。它不会被插入到 jar 文件中。相反，jar 程序读取并将其信息复制到清单文件中，该文件由 jar 程序创建。

现在使用 -m 选项构建 jar 文件，告诉 jar 文件查找清单信息。例如，如果你的 Main-Class 行在一个名为 many.txt 的文件中，你的命令将是

```
jar -cvfm my_archive.jar many.txt .class
```

jar 程序读取 many.txt 中的主类声明并在 jar 内部构建清单，包含主类声明和一些额外信息。jar 内部创建一个名为 META-INF 的目录，在 META-INF 中创建一个名为 MANIFEST.MF 的纯文本文件。这里是示例中 MANIFEST.MF 的样子：

```
Manifest-Version: 1.0
Created-By: 1.5.0 (Sun Microsystems Inc.)
Main-Class: MyMainClass
```

易用性是软件质量的重要部分。对 jar 程序稍微熟悉可以显著提高你项目的易用性。

# 总结

在之前的章节中，你已经阅读了完成项目所需的 GUI、I/O 和通信技术。本章复习了你读过的一些较小的杂杂概念，包括 Javadoc、线程、额外积分、对象流与 RMI、常识 GUI 设计以及 jar 工具。

这就是你需要的全部！到此时你已经准备好下载作业并开始工作了。
祝你好运！

# 附录 A 练习题

![](img/09f8389b7ae2705d1ab14be2d5e857e3_509_0.png)

# 问题

- 1. 给定：
```java
public enum Wallpaper {
BROWN, BLUE, YELLOW;
}
```

- 2. 下列哪些是合法的？
A. enum PatternedWallpaper extends Wallpaper {
STRIPES, DOTS, PLAIN;
B. Wallpaper wp = Wallpaper.BLUE;
C. Wallpaper wp = 
ew Wallpaper(Wallpaper.BLUE);
D. void aMethod(Wallpaper wp) {
System.out.println(wp);
E. int hcode = Wallpaper.BLUE.hashCode();

- 3. 给定以下：
```java
package pack;

class Sploo {
public int a;
public static int b;
int c;
static int d;
```

```java
public void eee() {}
public static void fff() {}
}
```

由于以下导入，包 pack 中的类可以访问 Sploo 的哪些功能？

```
import static pack.Sploo;
```

- A. a
B. b
C. c
D. d
E. eee()
F. fff()

- 4. 给定以下：
```java
public abstract class Abby {
    abstract provideMe();
}
public class SubAbby extends Abby { }
```

以下哪些陈述是正确的？

- A. Abby 生成了一个方法。
B. SubAbby 产生了一个错误。
C. 如果 SubAbby 是抽象的，它将通过编译。
D. 可以实例化 SubAbby。

- 5. 给定以下：
```java
class Xxx {
    int[] ages;
    int[] heights = new int[10];
}
```

哪些语句是正确的？

- A. ages 初始化为 null。
B. 这里的 初始化为 0。
C. heights 初始化为 10 个元素。
D. heights 初始化为数组。

- 6. 给定具有 public 变量 tint，以下哪些方法符合 JavaBeans 命名规范？
A. getColor()
B. getColor()
C. getTint()
D. getTint()
E. tint()

- 7. 关于以下方法，哪些是正确的？
```java
void callMe(String... names) {
```
A. 无法编译。
B. 在方法内部 names 是一个数组。
C. 在方法内部 names 是一个列表。
D. 方法只能从内部类调用。

- 8. 给定以下：
```java
class Food { }
class Fruit extends Food { }
class Citrus extends Fruit {
public feedMe() { return new(); }
```

对于 Subby，哪些返回类型是合法的？
A. Object
B. Food
C. Fruit
D. Citrus
E. Pomelo

- 9. 给定以下：
```java
class A extends java.Vector {
private A(int x) { super(x); }
}
```

哪些语句是正确的？

A. 创建了 public 访问的默认构造函数。
B. 创建了 protected 访问的默认构造函数。
C. 创建了默认访问的默认构造函数。
D. 创建了 private 访问的默认构造函数。
E. 没有创建默认构造函数。

- 10. 以下哪些类型是 switch 语句的合法参数？
A. enums
B. bytes
C. longs
D. floats
E. strings

- 11. 给定：
```java
int[] ages = { 9, 41, 49 };
int sum = 0;
```

以下哪些是添加数组元素的合法方式？
A. for (int i=0; i<ages.length; i++)
sum += ages[i];
B. for (int i=0; i<=ages.length; i++)
sum += ages[i];
C. for (int i:ages)
sum += i;
D. sum += ages[int:ages];

- 12. 哪些行检查 x 是否等于四？假设编译和运行时启用了断言。
A. assert x == 4;
B. assert x != 4;
C. assert x == 4 : "x is not 4";
D. assert x != 4 : "x is not 4";

- 13. 哪些是断言的适当用法？
A. 在私有方法中检查前提条件
B. 在私有方法中检查后置条件
C. 在公共方法中检查前提条件
D. 在公共方法中检查后置条件

- 14. 假设 A 类有一个方法，声明如下：
```
void callMe() throws ObjectStreamException
```

以下哪些可能出现在 A 的子类中？
A. void callMe()
B. void callMe() throws IOException
C. void callMe() throws NotSerializableException
D. void callMe() throws ObjectStreamException, AWTException

