
### 示例会话

```
[root@server1 root]### pwd
/home/bob
[root@server1 root]### ls /home/bob
assignment file letter letter2 project
[root@server1 root]#_
```

在运行 `ls` 命令时，注意不同类型的文件通常以不同的颜色显示；然而，如果不需要当前目录列表，你可以向 `ls` 命令传递参数来指定要列出的目录。在下面的示例中，文件被列在 `/home/bob` 目录下方，而没有更改当前目录。

### 注意

注意：使用 `ls` 命令可以以颜色显示类型类型

表 4-1 常见文件名扩展名

| 元字符 | 描述 |
| :--- | :--- |
| `.c` | C 编程语言源文件 |
| `.cc`, `.cpp` | C++ 编程语言源文件 |
| `.html`, `.htm` | HTML（超文本标记语言）文件 |
| `.ps` | 使用 postscript 格式化以用于打印的文件 |
| `.txt` | 文本文件 |
| `.tar` | 归档文件（内部包含其他文件） |
| 表 4-1 常见文件名扩展名（续） |
| 元字符 | 描述 |
| :--- | :--- |
| `.gz`, `.bz2`, `.Z` | 压缩文件 |
| `.tar.gz`, `.tgz`, `.tar.bz2`, `.tar.Z` | 压缩归档文件 |
| `.conf`, `.cfg` | 配置文件（包含文本） |
| `.so` | 共享对象（编程库）文件 |
| `.o` | 编译对象文件 |
| `.pl` | PERL（实用提取和报告语言）程序 |
| `.tcl` | Tcl（工具命令语言）程序 |
| `.jpg`, `.jpeg`, `.png`, `.tiff`, `.xpm`, `.gif` | 包含图形的二进制文件 |
| `.sh` | Shell 脚本（包含由 shell 执行的文本） |

### 列出文件

Linux 提供了各种命令，可用于显示硬盘分区上各种目录中的文件及其类型。到为止，显示文件最常用的方法是使用 `ls` 命令。以下是 root 用户家目录中文件列表的示例：

```
[root@server1 root]# pwd
/root/
[root@server1 root]# ls
current myprogram project project12 project2 project4
Desktop myscript project1 project13 project3 project5
[root@server1 root]#_
```

> 注意：之前列出并在本章中讨论的文件仅用于示例。

`ls` 命令以列格式显示当前目录下的所有文件；然而，如果不需要当前目录列表，你也可以向 `ls` 命令传递参数来指定要列出的目录。在下面的示例中，文件被列在 `/home/bob` 目录下方，而没有更改当前目录。

```
[root@server1 root]### pwd
/root
[root@server1 root]### ls /home/bob
assignment file letter letter2 project
[root@server1 root]#_
```

### 提示

在运行 `ls` 命令时，注意不同类型的文件通常以不同的颜色显示；然而，如果不需要当前目录列表，你可以向 `ls` 命令传递参数来指定要列出的目录。在下面的示例中，文件被列在 `/home/bob` 目录下方，而没有更改当前目录。

### 注意

使用 `ls` 命令可以以颜色显示类型类型

在上述示例中列出的每个文件都有八个信息组件，从左到右列出：

+ 1. 一个文件类型字符
    `d` 字符表示目录。
    `l` 字符表示符号链接文件（在第 5 章“Linux 文件系统管理”中讨论）。
    `b` 或 `c` 字符表示特殊设备文件。
    `n` 字符表示命名管道。
    `s` 字符表示套接字。
    `--` 字符表示所有其他文件类型（文本文件、二进制数据文件）。

### 查看文件和目录

第 4 章

- 2. 文件的权限列表（称为文件的模式）
- 3. 硬链接数（在第 5 章中讨论）
- 4. 文件的所有者（在第 5 章讨论）
- 5. 文件的组所有者（在第 5 章讨论）
- 6. 文件大小
- 7. 文件的最后修改时间
- 8. 文件名（某些是快捷方式或指向其他文件的指针，用箭头 `->` 表示，如前述输出中名为 `current` 的文件所示；这些被称为符号链接，将在第 5 章中讨论）

对于上一个示例中名为 `project` 的文件，你可以看到这是一个普通文件，因为它的长列表显示以 `-` 字符开头，文件权限为 `rw-r-r--`，硬链接数为 1，文件所有者为 `root` 用户，文件组所有者为 `root` 组，文件大小为 71 字节，文件最后修改时间为 4 月 7 日上午 9:58。

> 在大多数 Linux 系统上，可以使用 `ls` 命令的快捷方式来显示与 `ls -l` 命令相同的列信息。某些用户倾向于使用这种快捷方式，通常称为别名（alias），当用户在命令提示符处输入 `ll` 时就会调用。这被称为 **ll** 命令。

`ls -F` 和 `ls -l` 命令对于想要显示文件类型的用户非常有价值；然而，这些命令无一个能使用特殊字符显示所有文件类型。要显示任何文件的类型，你可以使用 `file` 命令；只需向 `file` 命令提供参数指定要分析的文件即可。你也可以传递多个文件作为参数，或使用通配符 `*` 来引用当前目录下的文件。在 root 的主目录下使用 `file` 命令的示例如下：

```
[root@server1 root]# pwd
/root
[root@server1 root]# ls
current myprogram project2 project2 project4
Desktop myscript project1 project13 project3 project5
[root@server1 root]# file Desktop
Desktop: directory
[root@server1 root]# file project Desktop
project: ASCII text
Desktop: directory
[root@server1 root]# file *
Desktop: directory
Desktop:
```

# 第 4 章 探索 Linux 文件系统

```
current: 指 project12 的符号链接
myprogram: ELF 32-bit LSB 可执行文件, Intel 8036, version 1, 动态链接 (使用共享库), stripped
myscript: Bourne-ne shell脚本文本可执行文件
project: ASCII text
project1: ASCII text
project12: ASCII text
project13: empty
project2: ASCII text
project3: ASCII text
project4: ASCII text
project5: ASCII text
[root@server1]#
```

如上例所示，`file` 命令还可以识别不同类型可执行文件之间的差异。`myscript` 文件是一个包含执行命令的文本文件（也称为 shell 脚本），而 `myprogram` 是一个 32 位可执行程序。`file` 命令还能识别如上例中 `project13` 这样的空文件。

每个用户主目录下的某些文件名代表重要的配置文件或程序目录。因为这些文件很少由用户编辑，且会弄乱文件列表，在使用 `ls` 和 `file` 命令时它们通常是隐藏的。记住，隐藏文件名以点字符（`.`）开头。要查看它们，请向命令传递 `-a` 。以下是 root 用户主目录中常见的隐藏文件：

```
[root@server root]# ls
current myprogram project12 project2 project4
Desktop myscript project1 project13 project3 project5
[root@server root]# ls -a
.gimp-1.2 project
.gnome project1
.bash_history .gnome-desktop project12
.bash_logout .gnome_private project13
.bash_profile .gtckrc project2
.bashrc .ICEAuthority project3
.cshrc .kde project4
current .mcpop project5
.DCOPServer_server1_0 .MCOP-random-seed .sane
Desktop .mocprc .sawfish
.first_start_kde .mozilla .tcshrc
.galeon myprogram .Xauthority
.gconf myscript .Xresources
.gconfd .nautilus
.nautilus .xsession-errors
[root@server root]#
```

### 查看文件和目录

如前所述，`.` 字符引用当前工作目录，`..` 字符引用相对于你在目录树中当前位置的父目录。在使用 `ls -a` 命令时，这些指针都是特殊或（虚拟的）文件，因为它们都以点开头。

你还可以同时为命令行上的大多数命令指定多个选项，并获得所有选项组合的功能。例如，要查看所有隐藏文件及其类型，你可以输入：

```
[root@server1 root]# ls -aF
./ gimp-1.2/ project
../ .gn/ project1
.bash_history .gn_desktop/ project12
.bash_logout .gn_private/ project13
.bash_profile .gtckrc project2
 .ICEAuthority project3
current .mcpop project5
.DCOPServer_server1_0 .MCOP-random-seed .sane
Desktop .mocprc .sawfish
.first_start_kde .mozilla .tcshrc
.galeon myprogram .Xauthority
.gconf myscript .Xresources
.gconfd .nautilus
.nautilus .xsession-errors
[root@server1]#
```

你也可以通过向 `cat` 命令传递 `-n` 选项，在显示文件内容的同时显示文件中每一行的行号。在接下来的示例中，显示了 `project4` 文件的行数：

```
[root@server root]# cat -n project4
1 你好，希望你今天一切都好。
2
3 遗憾的是，今年我们在阿尔冈昆国家公园度假期间，
4 没能进入您的餐厅 - 我
5 特别想看到餐厅里 Highland Inn 的模型
6 以及火车站的模型。
7
8 我一直在阅读关于阿尔冈昆国家公园的历史，但
9 在哪里都找不到关于 Highland 
10 Inn 原地位于 Cache 湖何的描述。
11
12 如果不麻烦的话，您能否告知我，这样
13 我就不必等到明年访问您的旅馆了？
14
15 顺颂商祺，
16 Mackenzie Elizabeth
[root@server root]#_
```

在某些情况下，我们可能想要反序显示某个文本文件的内容，这在显示由系统服务持续追加文本的文件时非常有用。这些文件称为日志文件，其最新条目位于文件底部。要反序显示文件，请使用 `tac` 命令（`tac` 是 `cat` 的反向拼写），如下所示 `project4` 文件所示：

```
[root@server root]# tac project4
Mackenzie Elizabeth
顺颂商祺。
```

### 显示文本文件的内容

第 4 章 129

如果显示的文件很大，你只想查看它的前几行，可以使用 `head` 命令。`head` 命令将文本文件的前 10 行（包括空行）显示到终端屏幕，但也可以接受一个数字选项来指定不同的显示行数。以下显示了使用 `head` 命令查看 `project4` 顶部的示例：

```
root@server1]# head project4
你好，希望你今天一切都好。
```

```
root@server1]# head -3 project4
你好，希望你今天一切都好。
```

正如 `head` 命令显示文本文件的开头一样，`tail` 命令可以用于显示文本文件的末尾。默认情况下，`tail` 命令显示文件的最后 10 行，但也可以接受一个数字选项来指定显示到终端屏幕的行数，如下面的 `project4` 文件示例所示：

```
root@server1]# tail project4
```

```
[root@server1] tail -2 project4
```

```
[root@server1 root]#_
```

`tail` 命令还接受另一个选项，用于指定在向终端显示文本时从哪一行开始。例如，要从第 10 行开始一直到文件末尾显示文本文件的结束，只需对 `tail` 命令使用 `+10` 选项，如下所示：

```
[root@server1] tail +10 project4
```

虽然文本文件可以在终端屏幕上完整显示，但你可能会遇到大到无法显示的文本文件。在这种情况下，`cat` 命令会在终端屏幕上显示整个文件内容，由于屏幕空间不足，文件顶部不会显示。因此，使用 `more` 或 `less` 命令以逐页的方式显示文本文件是有用的。

`more` 命令的名字源于 UNIX 系统上使用的 `pg` 命令。`pg` 命令从文件开头开始逐页显示文本文件；按下空格键或回车键显示下一页，依此类推。`more` 命令的功能比 `pg` 更多，因为当你按下空格键时它会显示下一个完整页，但按下回车键时它只显示下一行。通过这种方式，你可以逐页或逐行地缓冲文件内容。虚拟文件 `project` 是莎士比亚悲剧的一个片段，大到无法在终端上完全显示。使用 `more` 命令查看其内容，输出如下：

```
[root@server1] more project5
```

去告诉我的夫人，当你的酒准备好时，

敲一下。

我看到的这把刀吗？

来，抓住它。

### 显示文本文件的内容

# 第 4 章 131
