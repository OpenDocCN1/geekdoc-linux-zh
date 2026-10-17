
1 Merge branch 'master' of https://github.com/

bobk48/unixthetextbook3

2

# Please enter a commit message to explain why

this merge is necessary,

4 # especially if it merges an updated upstream into

a topic branch.

5 #

6 # Lines starting with '#' will be ignored, and an

empty message aborts

7 # the commit.

`/usr/home/bob/unixthetextbook3/.git/MERGE_MSG`: 7 lines, 295 characters.

Merge made by the 'recursive' strategy.

`.gitattributes` | 22

++++++

`.gitignore` | 43

++++++++++++++

`README.md` | 4 ++

`chap22_code/xlib_xcb_programs/1stxcbdraw.c` | 115

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

`chap22_code/xlib_xcb_programs/2ndxcb_events.c` | 102

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

`chap22_code/xlib_xcb_programs/test1.c` | 59

++++++++++++++++++++++++++++++++++++++++++++

`chap22_code/xlib_xcb_programs/test2.c` | 21

++++++

`chap22_code/xlib_xcb_programs/test3.c` | 53

++++++++++++++++++++++

`chap22_code/xlib_xcb_programs/test4.c` | 99

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

`chap22_code/xlib_xcb_programs/test7.c` | 98

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

`chap22_code/xlib_xcb_programs/test8.c` | 132

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

`chap22_code/xlib_xcb_programs/xcb_events.c` | 146

++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

...

create mode 100644 `qt/qt_progs3/qt_progs3`

create mode 100644 `qt/qt_progs3/qt_progs3.pro`

create mode 100644 `qt/qt_progs4/Makefile`

create mode 100644 `qt/qt_progs4/qt4.cpp`

create mode 100644 `qt/qt_progs4/qt4.o`

create mode 100644 `qt/qt_progs4/qt_progs4`

create mode 100644 `qt/qt_progs4/qt_progs4.pro`

<Output Truncated>

6. 检查工作目录的内容。

```
% ls
The current contents of the unixthetextbook3 repository
%
```

> 结论：使用 `git pull` 命令，你可以将内容从 GitHub 仓库分支获取并放到本地仓库分支上。

## EXERCISE 17.20

对于仓库 `unixthetextbook3` 列出了哪些 refspec URL 和 fetch 赋值？你是如何得知的？

## 17.5.7.9 Solaris Git 安装附录

以下步骤将允许你在 Solaris 系统上安装 Git：

- 1. 成为超级用户。

+ `bob@solaris:~$ su`

+ `Password: xxxxxx`

- 2. 使用 `pkg info` 命令检查在你的 Solaris 默认在线仓库中有哪些 Git 可用。注意其名称为 `/developer/versioning/git`。

+ `root@solaris:~# pkg info -r git`

+ Name: `developer/versioning/git`

+ Summary: `git` - Fast Version Control System

+ Description: `Git` is a free & open source, distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

+ Category: Development/Source Code Management

+ State: Not installed

+ Publisher: `solaris`

+ Version: 1.7.9.2

+ Build Release: 5.11

+ Branch: 0.175.2.0.0.42.1

+ Packaging Date: June 23, 2014 01:29:36 AM

+ Size: 22.91 MB

+ FMRI: `pkg://solaris/developer/versioning/git@1.7.9.2,5.11-0.175.2.0.0.42.1:20140623T012936Z`

+ `root@solaris:~#`

- 3. 使用 `pkg install` 安装 Git。

+ `root@solaris:~# pkg install developer/versioning/git`

+ Packages to install: 1

```
Create boot environment: No
Create backup environment: No
Services to change: 1
DOWNLOAD          PKGS      FILES      XFER (MB)   SPEED
Completed         1/1       334/334    8.5/8.5     454k/s
PHASE             ITEMS
Installing new actions            496/496
Updating package state database   Done
Updating image state              Done
Creating fast lookup database     Done
root@solaris:~#
```

4. 你现在已在 Solaris 系统上拥有 Git。

## 17.6 静态分析工具

对程序进行静态分析涉及在不执行程序的情况下分析程序的结构和属性。这些分析通常旨在确定代码在多个平台上的可移植性水平、代码行数（LOC）、程序中函数调用/点（FPs）的数量以及代码中每个函数所占时间的百分比。在软件项目的规划阶段，LOC 和 FPs 等参数通常用于软件成本模型中，用于估算完成软件项目所需的个人月数，从而估算软件成本。

静态分析工具允许你衡量这些参数。在以下各节中，我们讨论了一些有用的 UNIX 工具，这些工具允许你执行这些分析。我们的重点是 `lint` 实用程序，但我们也简要描述了 `prof` 实用程序。

### 17.6.1 验证代码的可移植性

大多数 C 编译器在检查类型不匹配方面做得相当好，但很少处理可移植性。你可以使用 `lint` 实用程序检查你的 C 软件的可移植性。它是 UNIX 中用于开发高质量、干净且可移植的 C 软件的最有用工具之一，但也是最不被理解和使用的工具之一。它检测可能成为错误、不可移植或浪费系统资源的程序特性。虽然 `lint` 可以与许多类型的文件一起使用，包括 C 程序、汇编和预处理器文件，但此处的讨论仅限于其与 C 程序文件一起使用。它在 Solaris 中不可用。因此，我们在 PC-BSD 下展示此工具的使用。

你只需学会忽略此类信息。下面是对 `lint` 实用程序的简要描述。
