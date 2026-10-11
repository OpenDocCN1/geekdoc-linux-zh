
通配符可以通过 `ls` 命令来演示。下面展示了使用通配符元字符来缩小 `ls` 命令输出列表范围的示例。

```
[root@server1 root]$ ls
current  myprogram  project  project12  project2  project4
Desktop  myscript  project1  project13  project3  project5

[root@server1 root]$ ls project*
project  project1  project12  project13  project2  project3  project4  project5

[root@server1 root]$ ls project?
project1  project2  project3  project4  project5

[root@server1 root]$ ls project??
project12  project13

[root@server1 root]$ ls project[135]
project1  project3  project5

[root@server1 root]$ ls project[!135]
project2  project4
```

## 显示文本文件的内容

到目前为止，本章讨论的命令可用于导航 Linux 目录结构并查看文件名和文件类型；现在通常要显示这些文件的内容。迄今为止，用户显示的最常见文件类型是文本文件。这些文件通常较小，包含由 shell 解释的配置信息或指令（称为 shell 脚本），但也可以包含其他形式的文本，如电子邮件信件。要在终端屏幕上（也称为**串联**）查看整个文本文件，可以使用 **cat 命令**。以下是使用 cat 命令显示电子邮件消息（在虚构文件 project4 中）内容的示例：

```
[root@server1 root]$ ls
current  myprogram  project  project12  project2  project4
Desktop  myscript  project1  project13  project3  project5

[root@server1 root]$ cat project4
Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining
room this year while vacationing in Algonquin Park - I
especially wished to see the model of the Highland Inn
and the train station in the dining room.

I have been reading on the history of Algonquin Park but
no where could I find a description of where the Highland
Inn was originally located on Cache lake.

If it is no trouble, could you kindly let me know such that
I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth
[root@server1 root]#_
```

除了显示内容外，你还可以通过向 **cat** 命令传递 `-n` 选项，使用 **cat 命令** 显示文件中每行的行号。在以下示例中，显示了 `project4` 文件中的行数：

```
[root@server1 root]# cat -n project4
     1  Hi there, I hope this day finds you well.
     2
     3  Unfortunately we were not able to make it to your dining
     4  room this year while vacationing in Algonquin Park - I
     5  especially wished to see the model of the Highland Inn
     6  and the train station in the dining room.
     7
     8  I have been reading on the history of Algonquin Park but
     9  no where could I find a description of where the Highland
    10 Inn was originally located on Cache Lake.
    11
    12 If it is no trouble, could you kindly let me know such that
    13 I need not wait until next year when I visit your lodge?
    14
    15 Regards,
    16 Mackenzie Elizabeth
[root@server1 root]#_
```

在某些情况下，你可能希望以反向顺序显示特定文本文件的内容，这在显示由系统服务持续追加文本的文件时很有用。这些文件也称为**日志文件**，其中最近的条目位于文件的底部。要反向显示文件，请使用 **tac 命令**（tac 是 cat 的拼写倒序），如下所示，使用文件 `project4`：

```
[root@server1 root]# tac project4
Mackenzie Elizabeth
Regards,

I need not wait until next year when I visit your lodge?
If it is no trouble, could you kindly let me know such that

Inn was originally located on Cache Lake.
no where could I find a description of where the Highland
I have been reading on the history of Algonquin Park but
and the train station in the dining room.
especially wished to see the model of the Highland Inn
room this year while vacationing in Algonquin Park - I
Unfortunately we were not able to make it to your dining

Hi there, I hope this day finds you well.
[root@server1 root]#
```

如果显示的文件非常大，而你只想查看开头几行，可以使用 **head 命令**。head 命令将文本文件的前 10 行（包括空行）显示到终端屏幕上，但也可以接受一个数字选项，指定要显示的不同行数。以下示例展示了使用 head 命令查看 project4 文件顶部的情况：

```
[root@server1 root]# head project4
Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining
room this year while vacationing in Algonquin Park - I
especially wished to see the model of the Highland Inn
and the train station in the dining room.

I have been reading on the history of Algonquin Park but
no where could I find a description of where the Highland
Inn was originally located on Cache lake.
[root@server1 root]# head -3 project4
Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining
[root@server1 root]#
```

正如 **head 命令** 显示文本文件的开头一样，**tail 命令** 可用于显示文本文件的结尾。默认情况下，tail 命令显示文件的最后 10 行，但也可以接受一个数字选项，指定要显示到终端屏幕上的行数，如下例中针对 project4 文件的示例所示：

```
[root@server1 root]# tail project4

I have been reading on the history of Algonquin Park but
no where could I find a description of where the Highland
Inn was originally located on Cache lake.

If it is no trouble, could you kindly let me know such that
I need not wait until next year when I visit your lodge?

Regards,
MacKenzie Elizabeth
[root@server1 root]# tail -2 project4
Regards,
MacKenzie Elizabeth
[root@server1 root]#_
```

**tail** 命令还接受另一个选项，指定在将文本显示到终端屏幕时开始显示的行号。例如，要从第 10 行开始显示文本文件的结尾并一直持续到文件末尾，只需使用 **tail** 命令的 `-10` 选项，如下所示：

```
[root@server1 root]# tail -10 project4
Inn was originally located on Cache Lake.

If it is no trouble, could you kindly let me know such that
I need not wait until next year when I visit your lodge?

Regards,
MacKenzie Elizabeth
[root@server1 root]#_
```

虽然一些文本文件可以完全在终端屏幕上显示，但你可能遇到太大的文本文件无法显示。在这种情况下，**cat** 命令会按顺序将文件的全部内容显示到终端屏幕上，由于屏幕区域不足，文件的顶部不会显示。因此，使用 **more** 或 **less** 命令逐页显示文本文件是非常有用的。

**more 命令** 得名于曾经在 UN*X 系统上使用的 **pg** 命令。**pg** 命令在终端屏幕上从文件开头开始逐页显示文本文件；按下空格键或 Enter 键会显示下一页，以此类推。**more** 命令比 **pg** 做得更多，因为如果你按下空格键，它会显示文本文件的下一个完整页面，但如果你按下 Enter，它只显示文本文件的下一行。这样，你可以逐页或逐行浏览文本文件的内容。虚构文件 **project5** 是莎士比亚悲剧 ***Macbeth*** 的摘录，太大，无法使用 **cat** 命令在终端屏幕上完全显示。使用 **more** 命令查看其内容的结果如下输出：

```
[root@server1 root]# more project5
Go bid thy mistress, when my drink is ready,
She strike upon the bell. Get thee to bed.
Is this a dagger which I see before me,
The handle toward my hand? Come, let me clutch thee.
I have thee not, and yet I see thee still.
Art thou not, fatal vision, sensible
To feeling as to sight? or art thou but
```

