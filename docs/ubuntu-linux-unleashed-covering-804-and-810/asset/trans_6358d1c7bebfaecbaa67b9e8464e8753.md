

将多个源文件构建成复杂应用程序的可执行形式的过程。

## 使用 autoconf 实用程序配置代码

make 命令只是 Ubuntu 随附的多个编程自动化实用程序之一。还有其他工具，例如 pmake（可并行执行 make），imake（用于构建 X11 客户端的依赖驱动 makefile 生成器），automake，以及较新的工具之一 autoconf，它构建可用于配置程序源代码包的 shell 脚本。

构建以源代码形式分发的许多 Linux 软件包需要使用 GNU 的 autoconf 实用程序。该程序构建一个名为 configure 的可执行 shell 脚本，执行时会自动检查并根据安装在目标主机（你的 Linux 系统）上的软件资源或依赖项（例如编程工具、库和相关实用程序）来定制从源代码构建。

许多以源代码形式下载的 Linux 命令和 X 的图形客户端都包含 configure 脚本。要配置源代码包、构建软件，然后安装新程序，root 用户可能会像这样使用脚本（在解压缩源代码并进入生成的构建目录之后）：

```
$ ./configure ; make ; sudo make install
```

autoconf 程序使用一个名为 configure.in 的文件，其中包含基本规则集或宏集合。configure.in 文件是用 autoscan 命令创建的。构建一个能正确执行的 configure 脚本还需要一个 makefile 模板，名为 Makefile.in。尽管可以手动创建依赖检查的 configure 脚本，但你可以通过使用 KDE 的 KDevelop 或 GNOME 的 Glade 等图形化项目开发工具轻松克服任何复杂依赖关系。（有关更多信息，请参阅本章后面的“图形化开发工具”部分。）

## 使用 Subversion 管理软件项目

尽管 make 可用于管理软件项目，但较大的软件项目需要文档管理、源代码控制、安全性和修订跟踪，因为源代码在开发过程中会经历一系列更改。Subversion 为这种大型软件项目管理提供了源代码版本控制实用程序。

Subversion 系统用于跟踪文件的多个版本更改，并且可用于回溯或在项目范围内对文档版本进行分支。它还可用于防止或解决多个开发人员对源代码文件所做的冲突条目或更改。使用 Subversion 进行源代码控制需要在 svn 命令行上至少使用以下五个命令选项：

- ► checkout—检出修订版本
- ► update—使用其他开发人员所做的更改更新你的源代码
- ► add—向仓库添加新文件
- ► delete—从仓库中删除文件
- ► commit—向其他仓库开发人员发布更改

请注意，其中一些命令要求你使用额外的字段，例如文件名。使用 commit 命令时，你应始终尝试传递 -m 参数（让你提供描述更改的消息），后跟有关更改的一些信息。例如：

```
svn commit -m "This fixes bug 204982."
```

Subversion 最令人印象深刻的功能之一是其能够离线工作——任何本地 Subversion 检出都会自动隐藏一个 .svn 目录，其中包含所有已检出文件的副本。得益于此，你可以在不联系服务器的情况下将当前文件与已检出的文件进行比较——所有操作都在本地运行。

## 调试工具

调试既是一门科学，也是一门艺术。有时，最简单的工具——代码清单——就是最好的调试工具。然而在其他时候，你需要使用其他调试工具。其中三种工具是 splint、gprof 和 gdb。

### 使用 splint 检查源代码

splint 命令类似于传统的 Unix lint 命令：它静态检查源代码是否存在可能的问题，并且还具有许多附加功能。即使你的 C 代码符合 C 标准并且编译干净，也可能仍包含错误。例如，这个简单程序可能编译干净甚至可以运行：

```
$ gcc -o tux tux.c
$ ./tux
```

但 splint 命令可能会指出源代码中的一些严重问题：

```
$ splint tux.c
Splint 3.1.1 --- 17 Feb 2004

tux.c: [in function main]
tux.c:2:19: Return value (type int) ignored: putchar(t[i+j]) ....
    Result returned by function call is not used. If this is intended, can cast
    result to (void) to eliminate message. (Use -retvalint to inhibit warning)
Finished checking --- 1 code warning
```

你可以使用 splint 命令的 -strict 选项，像这样获取更详细的报告：

```
$ splint -strict tux.c
```

GCC 也通过使用广泛的警告（通过 -Wall 和 -pedantic 选项）支持诊断：

