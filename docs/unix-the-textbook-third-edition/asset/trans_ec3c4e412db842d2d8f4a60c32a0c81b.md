

## 表 17.7 最常用的编程语言的网络资源，以及程序开发的 UNIX 命令和工具

### 通用页面：Shell 命令、Shell 编程、高级 UNIX 和程序开发工具

www.tutorialspoint.com/unix/unix-manpage-help.htm
一个关于 UNIX shell 命令、UNIX shell 编程、高级 UNIX 以及许多重要 UNIX 工具和资源的网页

tacpa.org/notes/linux/devTools.html
一个关于 UNIX/Linux 开发工具的网页

### 编程语言

www.perl.com
Perl 语言主页

http://www.bell-labs.com/usr/dmr/www/chist.html
C 语言历史，由 Dennis Ritchie 撰写

www.stroustrup.com/C++.html
C++ 语言页面，由语言设计者 Bjarne Stroustrup 维护

www.oracle.com/java/index.html
Java 的主页

www.oracle.com/technetwork/java/index.html
Java 编程语言精要

www.gnu.org/software/java/java.html
GNU 与 Java 语言

www.haskell.org/haskellwiki/Haskell
Haskell 编程语言

www.eiffel.com
Eiffel 编程语言主页

www.smalltalk.org
Smalltalk 编程语言主页

www.visualbasic.org
Visual BASIC 专业人士协会页面

gcc.gnu.org/fortran
GNU FORTRAN 主页

www.sigapl.org
ACM SIGPLAN APL 分会

en.wikipedia.org/wiki/AWK
AWK 的维基百科

www.grymoire.com/Unix/Awk.html
一个关于 AWK 的不错教程

### HTML 活动

### 编译器

### Make 和库工具

## 表 17.7 （续）最常用的编程语言的网络资源，以及程序开发的 UNIX 命令和工具

### 通用页面：Shell 命令、Shell 编程、高级 UNIX 和程序开发工具

| capone.mtsu.edu/csdept/FacilitiesAndResources/make.htm | 关于 make 实用程序的一个小型教程 |
| heather.cs.ucdavis.edu/~matloff/UnixAndC/CLanguage/Make.html | 关于 makefile 和库的非常好的教程 |

### gdb 和 GNU 软件测试工具

| http://www.gnu.org/software/gdb/gdb.html | gdb 的主页，GNU 项目调试器 |
| http://www.gnu.org/manual/ | GNU 软件包的在线文档 |

### 使用 Git/GitHub 进行版本控制

| http://gitref.org/ | Git 的综合参考网站 |
| http://git-scm.com/ | Git 的开源网站托管在 GitHub 上 |
| https://github.com/ | GitHub 托管网站 |
| en.wikipedia.org/wiki/GitHub | GitHub 的维基百科网站 |

- 将项目开发拆分为多个独立的分支，称为分支，可以单独演进
- 通过合并，或协调，在两个或多个分支中进行的内容更改，定期重新组合分支内容
- 允许许多人同时在项目上工作，根据需要随时在方便的时间共享和组合他们的工作

Git 和 GitHub 是原子级、分布式、面向内容的版本控制系统。原子级意味着当你对软件进行快照时，其中的所有内容都在同一时刻被捕获在快照中。分布式意味着你正在处理的整个软件包始终在本地对所有协作者可用。面向内容意味着当你将软件工作的不同分支合并时，只考虑你正在合并的分支中文件中的行内容。Git 使用几种有用的策略和机制来指示合并内容冲突，并使用作为 Git 插件的几种工具来解决它们。但只有编写、构建和测试软件如何工作的人，以及管理该过程的人，才负责解决合并上下文冲突。

静态分析阶段的目的是识别软件中可能存在的错误或不可移植的特征，并测量诸如代码行数（LOC）、功能点（FPs）和函数重复次数等指标。可用于此目的的 UNIX 工具包括 lint、prof 和 dprof。

动态分析阶段的目的是在程序执行期间分析程序。此阶段使用的工具旨在跟踪程序执行以调试它们并衡量其运行时间性能，即执行时间。软件生命周期此阶段常用的 UNIX 工具是调试器（gdb 等）和用于测量程序运行时间的工具（time）。

