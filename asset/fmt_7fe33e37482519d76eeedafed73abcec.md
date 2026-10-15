
### EXPLANATION

`quiet`选项会抑制`grep`的任何输出。它在仅需要退出状态时使用。如果退出状态为零，则表示`grep`找到了该模式。

# LAB 1: grep 练习

（请参考 CD 上的名为`datebook`的文件。）

```
Steve Blenheim:238-923-7366:95 Latham Lane, Easton, PA 83755:11/12/56:20300
Betty Boop:245-836-8537:635 Cutsey Lane, Hollywood, CA 91464:6/23/23:14500
Igor Chevsky:383-735-3995:3567 Populus Place, Caldwell, NJ 23887:5/16/68:23400
Norma Corder:397-857-2735:74 Pine Street, Dearborn, MI 23874:3/28/45:245700
Jennifer Cowan:548-834-2348:583 Laurel Ave., Kingsville, TX 83745:10/1/35:38900
Jon DeLoach:408-253-3122:123 Park St., San Jose, CA 04086:7/25/53:85100
Karen Evich:284-758-2857:23 Edgecliff Place, Lincoln, NB 92743:7/25/53:85100
Karen Evich:284-758-2867:23 Edgecliff Place, Lincoln, NB 92743:11/3/35:58200
Karen Evich:284-758-2867:23 Edgecliff Place, Lincoln, NB 92743:11/3/35:58200
Fred Fardbarkle:674-843-1385:20 Parak Lane, Duluth, MN 23850:4/12/23:780900
Fred Fardbarkle:674-843-1385:20 Parak Lane, Duluth, MN 23850:4/12/23:780900
Lori Gortz:327-832-5728:3465 Mirlo Street, Peabody, MA 34756:10/2/65:35200
Paco Gutierrez:835-365-1284:454 Easy Street, Decatur, IL 75732:2/28/53:123500
Ephram Hardy:293-259-5395:235 Carlton Lane, Joliet, IL 73858:8/12/20:56700
James Ikeda:834-938-8376:23445 Aster Ave., Allentown, NJ 83745:1/21/38:45000
Barbara Kertz:385-753-8726:832 Ponce Drive, Gary, IN 83756:1/21/46:268500
Lesley Kirstin:408-456-1234:4 Harvard Square, Boston, MA 02333:4/22/62:32600
William Kopt:846-836-2837:6937 Ware Road, Milton, PA 9376:9/21/46:43300
Sir Lancelot:837-835-8274:474 Camelot Boulevard, Bath, WY 28356:5/13/69:24500
Jesse Neal:408-233-8971:45 Rose Terrace, San Francisco, CA 92303:2/3/36:25000
Zippy Pinhand:834-823-8319:2356 Bizarro Ave., Farmount, IL 84837:1/1/67:89500
Arthur Putic:923-835-8745:23 Wimp Lane, Kensington, DL 38758:8/31/69:126000
Popeye Sailor:156-454-3322:945 Wluto Street, Anywhere, USA 29338:3/19/35:22350
Jose Santiago:385-898-8357:38 File Way, Abilene, TX 39673:1/5/58:95600
Tommy Savage:408-724-0140:1222 Oxbow Court, Sunnyvale, CA 94087:5/19/66:34200
Yukio Takeshiba:387-827-1095:13 Uno Lane, Asheville, NC 23566:7/1/29:57000
Vinh Tranh:438-910-7449:8235 Maple Street, Wilmington, VM 29085:9/23/63:68900
```

- 1. 打印包含字符串`San`的所有行。
- 2. 打印人名名字以`J`开头的所有行。
- 3. 打印以`700`结尾的所有行。
- 4. 打印不包含`834`的所有行。
- 5. 打印生日在十二月的所有行。
- 6. 打印电话号码为`408`区号的所有行。
- 7. 打印包含一个大写字母、后跟四个小写字母、一个逗号、一个空格和一个大写字母的所有行。
- 8. 打印姓氏以`K`或`k`开头的行。
- 9. 打印行号前一行薪水为六位数的行。
- 10. 打印包含`Lincoln`或`lincoln`的行（请记住`grep`对大小写不敏感）。

# chapter 5

![](img/60a0b5d254bd6007403850f972cbfad8_162_0.png)

# sed, 流线型编辑器

### 5.1 什么是 sed？

`Sed`是一个流线型、非交互式编辑器。它允许你执行与`vi`和`ex`编辑器中使用的相同类型的编辑任务。与交互式使用编辑器不同，`sed`程序让你在命令行输入编辑命令，指定文件，然后在屏幕上查看编辑命令的输出。`sed`编辑器是非破坏性的。除非你使用`shell`重定向保存输出，否则它不会更改你的文件。默认情况下，所有行都会打印到屏幕上。

`sed`编辑器在`shell`脚本中很有用，因为使用`vi`或`ex`等交互式编辑器会要求脚本用户熟悉该编辑器，并会使用户面临对打开文件进行不想要的修改的风险。你也可以将`sed`命令放在名为`sed`脚本的文件中，如果你需要执行多次编辑或不喜欢在`shell`命令行上担心`sed`命令的引号问题。¹

### 5.2 sed 的版本

Linux 使用 GNU 版本的`sed`，由自由软件基金会版权所有。此版本几乎与标准 UNIX 发行版提供的`sed`相同。

> 1. 请记住，`shell`会尝试在命令行输入命令时评估任何元字符或空白；`sed`命令中可能被`shell`解释的任何字符都必须加引号。

# 示例 5.1

```
% sed -V or sed --version

GNU sed version 3.02

Copyright (C) 1998 Free Software Foundation, Inc.

This is free software; see the source for copying conditions.

There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE, to the extent permitted by law.
```

### 5.3 sed 如何工作？

`sed`编辑器一次处理一个文件（或输入）的一行，并将其输出发送到屏幕。其命令是你可能从`vi`和`ed/ex`编辑器中认识到的。`Sed`将其当前处理的行存储在一个临时缓冲区中，称为模式空间或临时缓冲区。一旦`sed`完成对模式空间中行的处理（即在该行上执行`sed`命令），模式空间中的行就会被发送到屏幕（除非命令是删除该行或抑制其打印）。处理完该行后，它会从模式空间中移除，然后下一行会被读入模式空间、处理并显示。`Sed`在处理完输入文件的最后一行后结束。通过将每一行存储在临时缓冲区中并对该行进行编辑，原文件永远不会被更改或破坏。

![](img/60a0b5d254bd6007403850f972cbfad8_163_0.png)

### 5.4 正则表达式

`Sed`与`grep`类似，使用正则表达式（`REs`）和表 5.3 第 132 页所示的各种元字符在文件中搜索模式。正则表达式是用于搜索和替换而用正斜杠括起来的字符模式。

```
sed -n '/RE/p' filename
```

```
sed -n '/love/p' filename
```

```
sed -n 's/RE/replacement string/' filename
```

```
sed -n 's/love/like/' filename
```

要更改正则表达式分隔符，需在某个字符，例如`c`前加上反斜杠，后跟正则表达式，再加上该字符；例如，
