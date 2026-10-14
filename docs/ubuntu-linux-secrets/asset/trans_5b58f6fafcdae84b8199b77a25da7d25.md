

## 第 5 部分：在 Ubuntu 中编程

on inside the program as the program runs. 要正确调试 Java 应用程序，您需要使用 -g 选项编译它。然后您可以在调试器中启动类文件：

```
$ javac -g MyTestClass.java
$ jdb MyTestClass
Initializing jdb...
>
```

jdb 调试器现在已准备就绪。您可以使用多个命令来控制调试器的操作，如表 28-4 所示。

**表 28-4：jdb 调试器命令**

| 命令 | 描述 |
|---|---|
| `connectors` | 列出 JVM 中可用的连接器和传输 |
| `run` | 启动主类的执行 |
| `threads` | 列出线程 |
| `thread` | 设置默认线程 |
| `suspend` | 挂起指定的线程 ID |
| `resume` | 恢复指定的线程 ID |
| `where` | 转储指定线程的栈 |
| `wherei` | 转储指定线程的栈并附带 pc 信息 |
| `up` | 向上移动线程的栈 |
| `down` | 向下移动线程的栈 |
| `kill` | 终止指定的线程 |
| `interrupt` | 中断指定的线程 |
| `print` | 显示指定表达式的值 |
| `dump` | 显示所有对象信息 |
| `eval` | 计算指定的表达式 |
| `set` | 为变量分配新值 |
| `locals` | 显示所有局部变量 |
| `classes` | 列出当前已知的类 |
| `class` | 显示指定类的详细信息 |
| `methods` | 显示指定类的方法 |
| `fields` | 显示指定类的字段 |
| `threadgroups` | 列出线程组 |
| `threadgroup` | 将当前线程组设置为指定的线程组 |
| `stop in` | 在指定的类方法或行设置断点 |

正如您所见，有许多命令可用于检查正在运行的 Java 应用程序。以下是使用示例 Java 代码启动调试器并设置断点以停止程序的一个小示例：

```
$ jdb MyTestClass
Initializing jdb...
> stop in MyTestClass.main
Deferring breakpoint MyTestClass.main.
It will be set after the class is loaded.
> run
run MyTestClass
Set uncaught java.lang.Throwable
Set deferred uncaught java.lang.Throwable

VM Started: > Set deferred breakpoint MyTestClass.main

Breakpoint hit: "thread-main,", MyTestClass.main(), line=3 bc1=0
3 int number = 5;

main[1]
```

启动调试器后，我使用 stop in 命令在 MyTestClass 类的 main 方法处设置了断点。设置断点后，我使用 run 命令执行程序。

调试器启动了程序，然后在 main 方法的第一行停止。此时您可以使用 list 命令来显示代码中的位置：

```
main[1] list
1 class MyTestClass {
2 public static void main(String[] arg) {
3 -> int number = (int)(Math.random() * 10);
4 int factorial = 1;
5 int counter;
6 for(counter = 1; counter <= number; counter++) {
7 factorial = factorial * counter;
8 }
9 System.out.println("The factorial of "
10 + number
main[1]
```

调试器知道源代码并指示程序停止的源代码行。然后您可以使用 step 命令逐行逐步执行代码，然后使用 print 命令检查变量值：

```
main[1] step
>
Step completed: "thread-main,", MyTestClass.main(), line=4 bc1=2
4 int factorial = 1;

main[1] step
>
Step completed: "thread-main,", MyTestClass.main(), line=6 bc1=4
6 for(counter = 1; counter <= number; counter++) {
```

```
main[] print number
number - 5
main[]
```

您可以逐步执行 for 循环并观察每次迭代中 factorial 变量值的变化。在 for 循环结束时，factorial 值将包含最终值：

```
main[] step
> 
Step completed: "thread-main", MyTestClass.main(), line=9 bci=21
9 System.out.println("The factorial of "
```

```
main[] print factorial
factorial = 120
main[]
```

您可以使用 cont 命令释放程序以完成：

```
main[] cont
The factorial of 5 is 120
> 
The application exited
$
```

程序完成后，调试器会自动退出并返回到命令行提示符。调试器是排查 Java 程序的绝佳工具。

> 大多数图形化 IDE 包都提供图形化调试环境，这使得它们比命令行 jdb 调试器更容易使用。如果您有访问图形化 IDE 包来开发 Java 应用程序，请使用该软件中的调试器而不是 jdb 程序。但是，如果您处于命令行环境中，例如 Ubuntu 服务器，并且需要调试 Java 应用程序，jdb 可以成为救命稻草！

## jar 程序

Java 的一个缺点是，您通常会因编译单个应用程序的多个 Java 程序而产生多个 .class 文件。分发需要多个类文件的应用程序可能存在问题。

为了解决这个问题，Java 使用 jar 程序。jar 程序创建一个包含应用程序所需所有类文件单个库文件。

jar 程序的格式会根据您尝试执行的功能而变化。要创建新的 jar 文件，您将使用以下格式：

```
$ jar cf myjar.jar MyTestClass.class
```

此命令将类文件 MyTestClass.class 添加到名为 myjar.jar 的 jar 文件中。如果您需要向 jar 文件添加多个文件，只需将它们添加到命令行即可。您也可以使用 uf 参数更新现有 jar 文件。例如，如果您还有另一个

