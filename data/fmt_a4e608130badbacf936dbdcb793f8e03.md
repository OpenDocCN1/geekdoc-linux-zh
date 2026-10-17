
当你在本章中发现更多可以处理文件的命令时，你将能够利用对路径的知识来引用与当前工作目录不在同一目录下的文件。

注意不要混淆绝对路径和相对路径。特别要注意你使用斜杠 `/` 的位置。如果你打算使用从根目录开始的绝对路径，则应该在路径开头使用 `/`。

![](img/df9a01bf057d58c2401b5edabd6e8829_111_0.png)

如果你想进入某个目录快速查看一眼然后返回，可以使用快捷方式切换回上一个目录：

```
cd -
```

如果你输入这个命令，shell 会向你显示你之前所在的目录，然后将当前工作目录切换到该目录。

你也可以单独使用 `cd` 命令快速回到你的主目录，如下所示：

```
pi@raspberry /boot $ cd
pi@raspberry ~ $
```

## 探索更高级的列出选项

你可以通过指定路径使用 `ls` 查看当前工作目录之外的任何目录，如下：

```
pi@raspberry ~ $ ls /boot
```

尽管你处于主目录，但该命令仍为你提供了 `/boot` 目录的列表。

当我们这样为命令提供需要处理的信息（例如文件名或路径）时，它被称为`argument`。许多 Linux 命令都可以以此方式接受参数（包括 `cd` 和 `file` 命令）。某些命令还可以接受`option`。它们告诉命令如何执行工作，其格式为连字符 `-` 后面跟一个告诉命令使用哪些选项的代码。

有几个选项可以与 `ls` 一起使用来改变其结果，如表 5-1 所示。例如，进入你的主目录并使用

```
pi@raspberry ~ $ ls -R
```

这会列出你主目录下的所有内容，然后是主目录下各个文件夹中的所有内容。你可以使用 shell 右侧的滚动条查看所有内容。

当你同时使用选项和参数时，选项位于参数之前，典型的 Linux 命令格式为：

```
command -options arguments
```

例如，尝试使用 `-X` 选项列出 `python_games` 文件夹的内容。所有 `.png`、`.py` 和 `.wav` 文件将分在一起，这样更容易看到里面有什么。使用的命令是：

```
pi@raspberry ~ $ ls -X ~/python_games
```

你可以通过在单个连字符后添加多个选项代码来组合使用多个选项。例如，如果你想列出当前目录下的所有目录（选项 `R`），并且想按文件类型对结果分组（选项 `X`），并使用符号在文件名旁指示目录和可执行文件（选项 `F`），你将使用：

```
pi@raspberry ~ $ ls -RXF
```

5-2 显示了结果输出。我们向上滚动滚动条，所以你看到的是结果的开头而不是结尾。你可能会注意到的一点是，路径中使用单个点 `.` 来引用当前目录，第一组结果的路径简单的一个点。这个表示当前目录的短代码与用于引用父目录的两个点 `..` 类似。

![](img/df9a01bf057d58c2401b5edabd6e8829_112_0.png)

提示：当你尝试 `ls` 时，如果屏幕变得混乱难以追踪，请使用 `clear` 命令清空屏幕。

## ls 命令的选项

```
File Edit Tabs Help
@raspberrypi: ~ $ ls
Desktop/ Downloads/ Music/ Pictures/ Public/ python_game/ Templates/ Videos/
Desktop/
@Documents/
@aj Projects/ Greenfoot Projects/ Scratch Projects/
@Documents/Subprojects/ LED-Button/ people2/ shapes/
exploit/ license/ THPARTYLICENSE.txt
hello/ picture/ README.txt
@Documents/Subprojects/ Converter.java README.TXT
@Documents/Subprojects/ Game.java README.TXT
@Documents/Subprojects/ file-reader/
@Documents/Subprojects/ Database.java-Database-Test.java README.TXT
@Documents/Subprojects/ hello/
package hello.njava README.txt
@Documents/Subprojects/ LED-Button/
Button.java String.java
LED.java LED.java README.TXT
@Documents/Subprojects/ Class.java Class.class Student.class Person.java Student.java
Database.class Staff.class Database.class Staff.class Student.java README.TXT
@Documents/Subprojects/ Address.java Database.java Person.java Staff.java Student.java README.TXT
@Documents/Subprojects/ Picture.java Picture.java Square.java Triangle.java README.TXT
@Documents/Subprojects/ shapes/
shape.java Square.java Triangle.java README.TXT
@Greenfoot Projects/Tutorials/
@pi/scripts/ GREENFOOT_IMAGES.txt LICENSE README.txt THPARTYLICENSE.txt
```

FIGURE 5-2:

此列表包含了所有

| 选项 | 描述 |
| :--- | :--- |
| `-a` | 显示所有文件，包括隐藏文件。 |
| `-F` | 添加符号以指示类型。 |
| `-h` | 以人类可读的格式显示大小（K, M, G）。 |
| `-l` | 使用长格式，显示权限、链接、所有者、组、大小和修改日期。 |
| `-1` | 以单列（一个）输出结果，而不是行。 |
| `-m` | 在单行内列出条目，用逗号分隔。 |
| `-R` | 递归选项；搜索子目录。 |
| `-r` | 反转选项；按反序显示结果。 |
| `-s` | 按大小对结果排序。 |
| `-t` | 根据最后修改日期时间对结果排序。 |
| `-X` | 按扩展名对结果排序。 |

## 理解长列表格式和权限

`ls` 最实用的选项是长格式，与标准列表相比，它提供了关于文件的额外信息。你通过在 `ls` 命令后使用选项 `-l` 来触发它，如下所示：

```
@raspberry ~ $ ls -l
total 152
-rw-r--r-- 1 pi pi 256 Oct 28 13:53 booknotes.txt
drwx-xr-x 2 pi pi 4096 Oct 28 22:54 Desktop
drwx-xr-x 5 pi pi 4096 Oct 28 22:35 Documents
drwx-xr-x 2 pi pi 4096 Oct 28 22:54 Downloads
drwx-xr-x 2 pi pi 4096 Oct 28 22:54 Music
drwx-xr-x 2 pi pi 4096 Oct 28 22:54 Pictures
drwx-xr-x 2 pi pi 4096 Oct 28 22:54 Public
drwx-xr-x 2 pi pi 4096 Nov 17 22:35 python_games
drwx-xr-x 2 pi pi 4096 Nov 3 17:43 seanwork
-rw-r--r-- 1 pi pi 20855 Nov 12 2010 spacegame.sb
drwx-xr-x 2 pi pi 4096 Oct 28 22:54 Templates
drwx-xr-x 2 pi pi 4096 Oct 28 22:54 Videos
```

行中间的数字是文件大小。有三项（`Desktop`、`python_games` 和 `seanwork`）是目录，它们具有相同的大小（4096 字节），尽管它们的内容截然不同。这是因为目录也是文件，这里的数字告诉你描述该目录的文件有多大，而不是目录内容以字节为单位的实际大小，但你可以添加 `-h` 选项来获得更易易读的数字——例如，将 4096 字节转换为 4K。

其余信息是权限，它们指的是谁被允许使用文件以及他们被允许对文件做什么。Linux 从设计之初就旨在提供一种安全的方式，让多个用户共享同一个系统，因此权限是 Linux 运行至关重要的一部分。
