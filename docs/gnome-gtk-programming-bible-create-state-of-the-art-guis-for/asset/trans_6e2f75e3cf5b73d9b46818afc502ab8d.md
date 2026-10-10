
### 代码示例

```c
widget = gnome_stock_or_ordinary_button("Scores");
gtk_box_pack_start(GTK_BOX(box),widget,FALSE,FALSE,0);

widget = gnome_stock_or_ordinary_button("High Scores");
gtk_box_pack_start(GTK_BOX(box),widget,FALSE,FALSE,0);

widget = gnome_stock_new_with_icon(
    GNOME_STOCK_PIXMAP_OPEN);
gtk_box_pack_start(GTK_BOX(box),widget,FALSE,FALSE,0);
return(box);
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_722_0.png)

**图 22-26**：由 GnomeStock 控件生成的一组控件

所涉及的功能调用并不要求您创建自己的 GnomeStock 控件版本，因为内部已经创建了一个。实际上，您在应用程序中创建 GnomeStock 控件的唯一原因可能是您想要向可用的库存控件列表中添加内容。

创建的第一个控件是一个包含文本和像素图的按钮。GnomeStock 负责创建两个像素图：一个用于按钮的正常外观，另一个用于鼠标选中时的外观。这需要使用不同的背景颜色并更改边框颜色，使按钮看起来像是凸起或凹陷的。

库存像素图名称是字符串。例如，名称 GNOME_STOCK_PIXMAP_REVERT 被定义为 “Revert”。使用 “Scores” 调用 gnome_stock_or_ordinary_button() 的效果与参数为 GNOME_STOCK_PIXMAP_SCORES 相同。这会生成一个同时包含命名像素图和字符串的按钮。然而，使用参数 “High Scores” 调用同一函数时，由于不匹配任何库存像素图，因此仅显示文本。

框中的最后一个条目是 GnomeStock 控件本身。它可以以这种方式显示，因为它是一个控件，其唯一的可显示内容是像素图。

## GnomeStockPixmapWidget

GnomeStockPixmapWidget 是一个用于 GnomeStock 控件操作的实用控件。

### 继承关系
GnomeStockPixmapWidget --> GtkVBox --> GtkBox --> GtkContainer --> GtkWidget --> GtkObject

### 函数
```c
GtkWidget *gnome_stock_pixmap_widget(GtkWidget *window, const char *icon)
GtkWidget *gnome_stock_pixmap_widget_at_size(GtkWidget *window, const char *icon, guint width, guint height)
guint gnome_stock_pixmap_widget_get_type(void)
GtkWidget *gnome_stock_pixmap_widget_new(GtkWidget *window, const char *icon)
void gnome_stock_pixmap_widget_set_icon(GnomeStock *widget, const char *icon)
```

您的应用程序可以使用 GnomeStockPixmapWidget 来显示任意一个库存像素图。以下示例显示了图 22-27 中的窗口，其中包含名为 GNOME_STOCK_PIXMAP_REVERT 的库存像素图。

```c
static GtkWidget *makeWidget()
{
    GtkWidget *widget;

    widget = gnome_stock_pixmap_widget_new(NULL, GNOME_STOCK_PIXMAP_REVERT);
    return(widget);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_723_0.png)

## 摘要

本章提供了所有 Gnome 控件的字母顺序列表，以及可用于构建应用程序的其他一些 Gnome 对象。每个类都列出了以下内容：

- 为对象定义的信号、枚举类型和函数
- 每个对象的继承关系，以便您可以查找为任何特定控件定义的所有信号和函数
- 可显示控件和容器控件的示例，以及指向书中其他章节的引用，这些章节中包含相关示例

即使是 GNOME 应用程序也必须使用操作系统的一些设施。下一章将介绍 Linux 中内置的一些更常用设施。

## 一些 Linux 机制

编写应用程序的大部分工作涉及管理窗口，以及管理窗口显示和接收的数据。本章不涉及窗口和 GUI 界面——而是描述了一些提供对操作系统及某些特殊功能访问的函数调用。这里关于标准 C 库的内容很少（尽管由于 C 语言诞生于 UNIX 环境，某些标准 C 内容源自 UNIX 系统调用）。

本章介绍的函数仅代表可用函数的一小部分。我选择了一些多年来被证明对程序员（包括我）最实用的函数。解释较为简短，但本章的目的是让您知道它们的存在，并让您了解它们是如何工作的。有关每个函数的更多信息，请使用 man 页。

### 本章内容

- 解读 Linux 状态和错误代码
- 从进程内部生成新进程
- 从进程内部执行命令行
- 使用管道进行通信
- 访问当前系统日期和时间
- 处理文件

## Linux 错误代码

每当系统调用遇到错误时，错误编号会存储在一个名为 `errno` 的全局变量中。每个系统调用都可能修改此值；如果您需要该编号，必须在错误发生后立即读取它。您可以做三件事。最简单的方法是记录或显示该编号，但某些函数会将其翻译为描述性字符串供您使用。

```c
/* error.c */
#include <sys/types.h>
#include <sys/stat.h>
#include <stdio.h>
#include <fcntl.h>
#include <errno.h>

int main(int argc, char *argv[])
{
    int fd;
    char *filename = "/invalid/path/name";

    fd = creat(filename, S_IRWXU | S_IRWXG);
    if (fd < 0) {
        fprintf(stderr, "Error code: %d\n", errno);
        perror("Unable to create file");
        fprintf(stderr, "Unable to create %s: %s\n",
                filename, strerror(errno));
    }
}
```

对 `creat()` 的调用尝试创建一个新文件（授予用户和组所有权限），但由于路径无效，该尝试失败。错误代码以三种不同的方式显示在标准错误输出上。输出如下所示：

```
Error code: 2
Unable to create file: No such file or directory
Unable to create /invalid/path/name: No such file or directory
```

函数 *perror()* 将您提供的字符串与 *errno* 的**当前**值结合，以创建错误描述。然后它将字符串写入 *stderr*。函数 *strerror()* 仅将错误代码转换为字符串。函数 *perror()* 的优点是简洁，而函数 *strerror()* 的优点是提供最大的灵活性。

## 生成进程

Linux 中让一个进程生成另一个进程的方法是称为 *fork* 和 *exec* 的两步过程。

第一步是您的程序进行 fork 以创建自身的副本。对函数 *fork()* 的调用会创建两个完全独立的相同程序副本在运行，每个都有自己唯一的进程 ID 号。由于可执行代码可以在程序之间共享，因此如果存储在内存中，forking 只会产生一个副本。每个进程特有的内容——例如数据、当前程序位置、某些 CPU 寄存器值和栈——会被复制。Forking 进程是 Linux 操作系统如此基础的一部分，以至于尽管它可以是一个复杂的程序，但它非常快。一旦进程被 fork，原始进程被称为 *父* 进程，而新的进程被称为 *子* 进程。

第二步是子进程用新进程替换自身。也就是说，新程序从磁盘加载并作为子进程开始运行。您可以通过调用 *exec*() 系列函数之一来实现这一点。所有 *exec*() 函数执行相同的功能——唯一的区别是通过命令行传递给新程序的参数组织方式。

以下程序进行 fork，然后由 fork 产生的子进程 exec 一个新程序：

```c
/* Forkexec.c */
#include <unistd.h>

int main(int argc, char *argv[])
{
    int pid;
    int childpid;
    int status;

    if ((pid = fork()) == 0) {
        printf("Child: pid=%d parentpid=%d\n", getpid(), getppid());
        execvp("showargs", 
            "first",
            "second",
            "third",
            NULL);
        printf("Child: This should never print\n");
    }
    printf("Parent: pid=%d childpid=%d\n", getpid(), pid);
    childpid = wait(&status);
    printf("Parent: child %d died\n", childpid);
    exit(0);
}
```

Fork 在第 10 行对 `fork()` 的调用中发生。在函数执行期间，正在运行的程序被分为两部分，实际上有两个从函数返回：一个用于父进程，一个用于子进程。返回的进程 ID 号用于确定哪个是子进程，哪个是父进程；父进程返回子进程的进程 ID，而子进程返回零进程 ID。这意味着第 11 行至第 14 行的语句仅由子进程执行。并且，由于对 `execvp()` 在第 13 行的调用永远不会返回，只有父进程执行第 16 行至第 20 行。

在第 11 行，子进程显示其进程 ID 及其父进程的进程 ID。这两个 ID 都没有从 `fork()` 调用中返回，因此有必要调用 `getpid()` 和 `getppid()` 来获取它们。

在第 12 行，调用 `execvp()` 以启动一个新进程来取代当前进程（子进程），并采用相同的进程 ID 号。该程序立即停止运行，新程序开始。如果 `execvp()` 函数返回，则意味着它失败了。`execvp()` 的第一个参数是要运行的程序名称。其他参数是您应包含在子程序命令行中的内容。`exec()` 函数有几个版本——以不同的方式传递参数——您可以通过输入 `man exec` 获取详细信息。

在第 16 行，父进程显示其自身的进程 ID 和新子进程的进程 ID。对 `getpid()` 的调用用于父进程获取其自身的 ID 号，但子进程的 ID 是从 `fork()` 调用中返回的那个。

