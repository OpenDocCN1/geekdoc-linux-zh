
关于 KDevelop 的更多信息（包括下载信息），请访问 KDevelop 首页：`kdevelop.org/`。语言支持页面（`www.kdevelop.org/HEAD/api/html/LangOrderStatus.html`）显示了编程语言的状态。KDevelop 适用于许多 Linux 发行版，包括 KDE 桌面。（例如，在 Fedora 中执行 `yum install kdevelop` 来安装 KDevelop。）

## Anjeta：用于 GTK/GNOME 的 IDE

为了给 GTK/GNOME 桌面环境开发 C 和 C++ 应用程序，你可以使用 Anjeta 集成开发环境（`http://projects.gnome.org/anjeta`）。通过 Anjeta，你可以使用 GtkSource 或 Scaffold 等编辑器管理你的代码。你可以在文档窗口中编辑文件，在项目视图查看树，或打开符号窗口查看符号树。Anjeta 项目插件可以帮助你管理基于 automake 和 autoconf 的多个项目。你可以创建新项目、更改其结构、配置构建标志和其他设置、编译并链接源代码以及运行程序。通过不向项目添加任何 Anjeta 特有的文件，Anjeta 允许你在 Anjeta 之外的环境中使用你的项目。

Anjeta 带有许多 Linux 发行版。在 Fedora 中，你可以以 root 用户身份执行 `install anjeta` 来安装它。要打开 Anjeta 窗口，选择应用程序-编程-Anjeta IDE。图 29-4 显示了 Anjeta 窗口的一个示例。

图 29-4

用于 GTK/GNOME 的 IDE

![](img/8f71f83ce3d8e208bf71b5b6c9a753bd_798_0.png)

767

# 第六部分：在 Linux 中编程

## 代码十字服者 (Code Crusader)

Code Crusader 是一款用 C++ 编写的商业支持型 IDE，专门针对 Linux 开发者；它不支持 Windows 系统。你可以使用 Code Crusader 编写 Java、FORTRAN、C++ 以及其他程序。与目前讨论的 IDE 不同，Code Crusader 没有内置的调试器。相反，Code Crusader 的开发者 New Planet Software 单独提供了其调试器应用程序 Code Medic（尽管你可以将两者作为 IDE 捆包一起购买）。图 29-5 显示了编辑器窗口中带有 `forkec.c` 的 Code Crusader。

## 图 29-5

Code Crusader IDE

```
forkec.c
File Edit Search Commands Windows Preferences Header
* forkec - illustrate simple fork/exec usage
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
    pid_t pid;
    int status;
    pid = fork();
    if (pid == 0) {
        printf("child: %d\n", pid);
        execl("/bin/ls", "ls", NULL);
    } else {
        printf("parent: %d\n", pid);
        wait(&status);
    }
    return 0;
}
```

如你在图 29-5 所示，Code Crusader 的界面比目前提到的其他 IDE 更加简单、简洁。Code Crusader 与 Eclipse 和 KDevelop 等大型 IDE 的另一个显著区别在于，每个 IDE 组件（如项目浏览器、类浏览器、编辑器窗口和日志查看器）都在它们各自独立的窗口中打开，而不是作为单一文档界面 (SDI) 的一部分。

多窗口更符合传统的 Linux 和 UNIX 窗口惯例，但来自 Windows 背景的开发者起初可能会觉得 Code Crusader 的多文档界面 (MDI) 稍微有些不习惯。另一方面，倾向于轻量、简洁界面的程序员可能更偏喜欢 Code Crusader，而不是 Eclipse 和 KDevelop 提供的看起来相当臃肿的界面。

## 第 29 章：编程环境与接口

## 笔记

关于 Code Crusader 的更多信息

在本节讨论的三个 IDE 之外，还有许多其他的 IDE。有些成熟度不高或仍处于测试阶段。另一些是特殊用途 IDE，例如 Quanta HTML 编辑器，或用于 GNOME 的 GLADE 界面设计器。如果 Eclipse、KDE 和 Code Crusader不能吸引你，快速搜索 Freshmeat（`http://freshmeat.net/tags/integrated-development-environments` 以直接进入 IDE 类别）或 SourceForge（`http://sourceforge.net/software/tree_list.php?form_cat=65` 以直接进入 IDE 类别）会提供很多选项供你选择。每个人都能找到适合自己的。毕竟这是 Linux，所以你可以自由选择最吸引你的 IDE。不过，在下一个小节中你将了解到，并不是所有人（或都需要）一个 GUI IDE。

## 命令行编程环境

Linux 命令行编程环境或 CLI（命令行界面）与上一节描述的 GUI 形成了鲜明对比。这让那些只有 Windows 开发背景且不习惯使用 CLI 的开发者感到震惊。

公平地说，发现自己面对一个命令行提示符，没有任何双击操作可以启动，也没有关于如何继续的任何线索，这可能会令人感到畏惧。尽管如此，虽然对于新手来说 CLI 也许看起来很简陋，但在命令行进行编程是惊地强大，它允许你以大多数 IDE 无法比拟的方式混合使用最顶级的工具。CLI 编程环境在功能上可以与 GUI 提供的环境匹配，唯一的例外是图形界面本身。

不方便（如果算是不方便的话）源于 CLI 编程环境依赖于独立的工具。例如，假设你在 Windows 系统中工作，你可能在每个终端窗口中运行一个或多个文本编辑器，如 `vi`、`nano`、`joe` 或 `emacs`。你可能使用另一个终端窗口来编译程序，直接调用编译器 `gcc`（GNU 编译器）或使用 `make` 工具。在另一个窗口中，你可能正在运行调试器，如 `gdb`（GNU 调试器）。如果你不熟悉使用的库，可以使用 Web 浏览器查看某些在线文档，或者使用一个以图形化格式显示 Linux 手册 (man) 页的程序。

然而，图形 IDE 并不比使用离散工具更好。这取决于开发者觉得使用哪种工具最舒服，哪种方法让开发者效率最高，以及哪种方法符合每个开发者的个人工作风格。许多长期 UNIX 和 Linux 开发者觉得使用命令行工具最舒服且工作效率更高：使用 `vi` 或 `emacs` 编写和编辑代码，使用 `gcc` 和 `make` 进行编译，使用 `gdb` 和 `kgdb` 进行调试。

# 第六部分：在 Linux 中编程

无论如何，这些界限并不那么明显。例如，Emacs 具有调用（编译和调试设施的功能，拥有极其丰富的代码编辑界面（例如语法高亮和自动缩进），并支持其他代码开发功能。Emacs 还包括源码控制、符号和类浏览，以及对至少三种不同在线帮助设施的内置支持。

如果你更偏于 `vi`，它也可以配置为使用 `ctags` 程序支持符号和类，它具有基础的语法高亮（取决于实现方式），并且可以与其他协作。

## Linux 接口

正如章节开头定义的，编程接口指的是规则或方法。图形界面使用窗口系统来接收输入。命令行接口（有时称为 TUI）是严格基于文本的。正如章节开头提到的，还有第三种接口：应用程序编程接口，或 API。本节将介绍用于创建接口的库，检查一些流行的图形界面，并描述程序员使用最常用的 API。

## 创建命令行接口

在命令行创建与用户交互的程序有两种主要方法。两种使用屏幕操作库（S-Lang 和 curses）来创建 TUI，而第三种使用标准输入和输出（传统称为 stdin 和 stdout）。使用 stdin 和 stdout 非常简单。输入和输出按行进行；用户通过键盘输入或从文件管道输入，输出显示在屏幕上或重定向到文件。列表 29-2 显示这样一个程序 `readkey.c`。

### 列表 29-2

读写 `stdin` 和 `stdout`
