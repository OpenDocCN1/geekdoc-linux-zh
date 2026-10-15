

## 注意

前面示例中的缩进行使用制表符缩进，而非空格。这一点务必牢记！人眼很难看出区别，但 make 可以分辨。如果你在 Linux 下开始构建程序时 make 报出令人困惑的错误，请检查项目 makefile 中是否正确使用了制表符及其他格式。

使用前面示例中的 makefile，你可以这样构建程序：

```
# make
```

要构建 makefile 中的特定组件，可以在命令行中使用目标定义。仅构建程序时，可将 make 与 skele 目标一起使用，如下所示：

```
# make skele
```

如果你对目标对象的任何元素（如源代码文件）进行了更改，make 会自动重新构建该目标。这一特性是使用 make 管理开发项目的便利性之一。若要在一步内构建并安装程序，可以指定 install 目标，如下所示：

```
# make install
```

较大的软件项目在 makefile 中可能包含许多传统目标，例如：

- test—在最终软件上运行特定测试
- man—使用 man 宏处理并包含 troff 文档
- clean—删除所有剩余的目标文件
- archive—清理、归档并压缩整个源代码树
- bugreport—自动收集构建或错误日志，然后通过邮件发送副本

大型应用程序可能需要数百个源文件。编译和链接这些应用程序可能是一项复杂且容易出错的任务。make 工具帮助你组织从许多源文件构建复杂应用程序可执行形式的过程。

## 使用 autoconf 工具配置代码

make 命令只是 Ubuntu 附带的几个编程自动化工具之一。还有其他工具，如 pmake（用于并行 make）、imake（一种依赖驱动的 makefile 生成器，用于构建 X11 客户端）、automake，以及一个较新的工具 autoconf，它构建可用于配置程序源代码包的 shell 脚本。

为 Linux 构建许多以源代码形式分发的软件包需要使用 GNU 的 autoconf 工具。该程序构建一个名为 configure 的可执行 shell 脚本，该脚本在执行时，会根据目标主机（你的 Linux 系统）上安装的软件资源或依赖项（如编程工具、库和相关实用程序），自动检查并调整客户端基于源代码的构建。

许多以源代码形式下载的 Linux 命令和 X 图形客户端都包含 configure 脚本。要配置源代码包、构建软件并安装新程序，root 用户可能会这样使用该脚本（解压源代码并进入生成的构建目录之后）：

```
$ ./configure ; make ; sudo make install
```

autoconf 程序使用名为 configure.in 的文件，其中包含基本规则集或宏集合。configure.in 文件是使用 autoscan 命令创建的。构建一个正确执行的 configure 脚本还需要一个名为 Makefile.in 的 makefile 模板。虽然可以手动创建检查依赖关系的 configure 脚本，但使用图形化项目开发工具（如 KDE 的 KDevelop 或 GNOME 的 Glade）可以轻松处理任何复杂的依赖关系。（更多信息请参阅本章后面的“图形化开发工具”一节。）

## 使用 CVS 和 Subversion 管理软件项目

虽然你可以使用 make 来管理软件项目，但较大的软件项目需要文档管理、源代码控制、安全性和版本跟踪，因为源代码在开发过程中会经历一系列变更。CVS 和 Subversion 为此类大型软件项目管理提供了源代码版本控制工具。你可以在 Ubuntu DVD 上的 APT 软件包中找到这些工具。

CVS 和 Subversion 都用于跟踪文件多个版本的变更，并可用于在项目范围内回溯或分支文档版本。它们还可用于防止或解决多个开发人员对源代码文件所做的冲突条目或更改。Subversion 比 CVS 更新，许多项目正在从 CVS 迁移到 Subversion。尽管 Subversion 引入了许多受欢迎的功能，例如离线工作的能力，但它使用了与 CVS 非常相似的命令行语法，因此 CVS 用户会感到熟悉。

使用 CVS 和 Subversion 进行源代码控制，至少需要在 cvs 或 svn 命令行中使用以下六个命令选项：

- checkout—检出修订版本
- update—用其他开发人员所做的更改更新你的源代码
- add—在 cvs 记录中添加新文件
- import—向仓库添加新源代码
- remove—从仓库中删除文件（注意：Subversion 使用 delete 来执行此操作）
- commit—将更改发布给仓库的其他开发人员

