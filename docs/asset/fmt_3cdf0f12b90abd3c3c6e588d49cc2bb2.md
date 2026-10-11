
`$ cat /etc/passwd | cut -f 5 -d | tr [:lower:] [:upper:] | sort | head -5`

命令管道的第一部分 `cat /etc/passwd` 将 `/etc/passwd` 文件的内容写入标准输出。第二部分 `cut -f 5 -d` 使用冒号（`:`）作为分隔符，从其标准输入（`/etc/passwd` 的内容）中切出第五字段（`/etc/passwd` 的第五字段是 GECO 或名称字段）。

第三部分 `tr [:lower:] [:upper:]` 将标准输入中的所有小写字母转换为大写字母。下一个元素 `sort` 在将排序后的列表发送到标准输出之前，对其输入的第一个字母进行字母排序。最后一个组件 `head -5` 只将其标准输入的前五行显示到标准输出。该管道的输出可能如下：

```
ADM

BIN

DAEMON

GAMES

LP
```

接下来的命令管道将被证明更有用：它将当前的运行时间和平均负载通过电子邮局发送给 root 用户：

```
$ uptime | mailx -s "System Usage" root
```

第三条规则——保持程序自成一体——与第二条规则相关。其背后的概念是，设计用于命令管道的程序不应该对其输入的可能样式做任何假设，也不应该对输出进行任何处理。

考虑在第一个命令管道中显示的 `cut` 命令。它接受任意格式的输入，并允许用户指定在哪些数据上进行操作（示例中的第五字段，该字段由冒号分隔），然后直接在标准输出上显示请求的数据。

# 编程环境与接口

`cut` 不对输出进行任何后处理，允许用户随心所欲地使用另一个工具对其进行处理。

第四条规则实际上更像是一种哲学观察，你无法真正预测你的程序可能被使用的所有方式。事实上，正如 S.C. Johnson 曾经指出的那样，“一个成功的[软件]工具是用来完成作者从未想过的事情的。”

点在于，Linux 工具包（对于开发者和终端用户来说）充满了许多小工具和实用程序。这些是经常用于创建大型程序和工具的构建块，这些工具共同执行那些任何单一程序无法完成或无法高效完成的复杂任务。构建块哲学的另一个特征是，它允许以批处理模式执行任务，不需要用户的活跃执行或参与。这种构建块哲学是 Linux 开发环境的另一个显著特征，一旦你理解了这一点，它就能让你的生活变得简单得多。它还帮助你站在前人的肩膀上，这样你就可以可以在现有构建块的基础上构建，而不是从头开始一切。

## 图形化编程环境

如果你坐在 Linux 系统前，那么很有可能：

- 它正在运行某个版本的 X窗口系统（X Window System）。
- 在 X 图形界面之上运行着几个终端（或 shell）窗口（终端模拟器）。
- 运行着至少一个或多个原生图形化程序，例如 Web 浏览器。

Linux 编程环境可以分为两大大类：图形化 IDE 和离散的命令行工具集。来自主要 Windows 背景的开发者和用户对 IDE 来说很熟悉；Windows 世界中的“巨无霸”是微软的 Visual Studio 产品。

本节介绍了一些功能完备的图形化 IDE，它们在单一的统一界面中收集并合并了开发任务所需的所有组成部分，例如编辑器、编译器、链接器、调试器、类浏览器和项目管理器。文中讨论的示例包括开源环境 Eclipse、KDE 环境和 Code Crusader 环境。

### Eclipse：通型工具平台

Eclipse 是一个大型的基于 Java 的开发平台。在原理和实践中，Eclipse 是一个通用的 IDE，用于创建各种应用程序，如 Web 网站、C、C++ 和 Java 程序，以及扩展 Eclipse 本身的插件。Eclipse 完全有能力以惊人的多种语言处理 Linux 开发的各个方面。图 28.1 显示了屏幕上用 Java 编写的“Hello, World”示例程序的 Eclipse。

## 第六部分 在 Linux 中编程

### 图 28.1 Eclipse IDE

![](img/fa18693414a802b12c8add5f8c4be910_799_0.png)

图 28.1 说明了 IDE 的一些典型特征。屏幕左侧的项目视图提供了一个项目文件浏览器，让你能够一目了然看到项目的内容。你可能会看到默认包 HelloWorld 和一些 JRE（Java 运行时环境）文件。

屏幕中心的代码编辑器显示 Java 程序的代码。代码编辑器使用颜色进行实时语法高亮。Java 关键字是紫色的；普通注释显示为绿色；Javadoc 风格的注释显示为浅蓝色；字符串为蓝色；普通代码为黑色。都可以根据你的喜好进行自定义。

Eclipse 的右侧显示了 IDE 中常见的另一个功能：类浏览器（class browser）。类浏览器允许开发者从代码模块的角度而非仅仅是目录中文件的角度来查看程序的结构。对于像 HelloWorld 这样的小程序，这个功能并不是特别有用，但对于由几十个类或代码模块组成的大型程序，使用类浏览器导航要容易得多。

屏幕底部显示了各种信息和状态窗口。例如，“问题”（Problems）视图显示了在编译程序时可能出现的问题。Eclipse 允许你双击问题视图中的错误，以直接跳转到相关代码文件中的错误（见图 28.2）。

### 图 28.2 Eclipse 的问题视图

![](img/fa18693414a802b12c8add5f8c4be910_800_0.png)

Javadoc 视图是 Eclipse Java 开发插件特有的，允许你查看 Javadoc 的输出，Javadoc 是一种从特殊格式的 Java 源码注释创建文档的工具。声明（Declaration）视图与类浏览器配合使用，显示方法和数据类型的完整声明。控制台（Console）视图显示程序的实际输出。

> 注意 欲了解有关 Eclipse 的更多信息（包括下载信息），请访问 www.eclipse.org。

### KDevelop：KDE 的 IDE

KDevelop 是一个根据 GPL 许可的开源 IDE，最初是为了提供一个与 KDE 以及基于 KDE 的 Qt 框架（大型 C++ 应用程序框架）无缝协作的 IDE。然而，多年来，KDevelop 已演变成一个吸引人的、功能丰富的开发环境，支持除 C++ 之外的多种语言。今天，KDevelop 是一个通用 IDE，用于创建用 C++ 编写的 Qt 应用程序效果最好。图 28.3 显示了 KDevelop 的代表性截图。

### 图 28.3 KDevelop IDE

![](img/fa18693414a802b12c8add5f8c4be910_801_0.png)

如果你将 KDevelop 与 Eclipse 的外观进行比较，你会发现它们具有相同类型的组件。在图 28.3 中，类浏览器位于屏幕左侧，项目窗口位于屏幕右上角，而 KDevelop 的声明视图显示在屏幕右下角。

图 28.3 中占据 KDevelop 界面底日志视图显示了编译过程。与 Eclipse 相比，KDevelop 的工具栏和菜单挤满了满足开发者需求的按钮和菜单项，就像文字处理器会针对编写和格式化文档的任务定制特定的按钮和菜单项一样。

> 欲了解更多关于 KDevelop 的信息（包括下载信息），请访问 KDevelop 主页 http://kdevelop.kde.org/。语言状态支持页（www.kdevelop.org/HEAD/api/html/LangSupportStatus.html）显示了当前支持的编程语言列表。

### Code Crusader

Code Crusader 是一款商用且支持的 C++ IDE，专门为 Linux 开发者量身定制；它不适用于 Windows。你可以使用 Code Crusader 编写

Java、FORTRAN、C++ 以及 语言程序。与到目前讨论的 IDE 不同，Code Crusader 不包含内置调试器。相反，Code Crusader 的开发者 New Planet Software 单独提供其调试器应用程序 Code Medic（尽管你可以将两者作为 IDE 捆绑购买）。图 28.4 显示了打开了窗口并运行列表 28-1 中 `forkexec.c` 程序的 Code Crusader。

### 图 28.4 Code Crusader IDE

```
forkexec.c - 演示简单的 fork/exec 用法

#include <stdio.h>

#include <stdlib.h>

#include <sys/types.h>

#include <sys/wait.h>

int main(int argc, char *argv[]) {

    pid_t pid;

    int status;

    pid = fork();

    if (pid == 0) {

        printf("child: %d\n", getpid());

        execcl("/bin/ls", "ls", NULL);

    } else {

        printf("parent: %d\n", getpid());
```
