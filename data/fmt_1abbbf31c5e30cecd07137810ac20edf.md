
- 如何查询可用的磁盘空间大小。
- 适用于所有目录的目录简写符号。
- 针对你账户的目录简写符号。

现在，请前往“Linux Made Easy CBT”中的 Linux 目录模块。完成 CBT 中的材料后，请返回本指南。回到这里后，请完成“Try It Live!”中的练习，然后完成“Check Yourself”和“Match”部分的问题。

#### 立即尝试！

1. 登录你的 Linux 系统。使用 `ls` 列出主目录中的文件。
   - a. 输入 `ls`
   - b. 按 <Enter>

```
$ ls
. . . . . . [file list]
$
```

图 5-1 你在系统提示符下输入 `ls`

2. 使用 `ls -a` 列出主目录中的文件。
   - a. 输入 `ls -a`
   - b. 按 <Enter>

`-a` 开关意味着“所有”。正如你所见，`a` 开关会在显示中添加通常被隐藏的文件——以点开头的文件。我们在《*Day to Day with Linux*》中提到过这样一个文件，即 `.profile` 文件，你可以使用它来自定义你的 Linux 账户。图 5-2 显示了你可能会看到的文件列表。这些隐藏文件中可能有一些是由系统创建的房屋管理文件（housekeeping files）。在屏幕显示中，注意简写符号——单点和双点。你记得单点代表当前目录，双点代表父目录。

![](img/cc8b9fd5970716027fba0d0a45c13900_80_0.png)

图 5-2 使用 `ls -a` 显示时你可能会看到的文件简略列表

3. 如果你主目录的内容目前有点寒酸，列出 `/etc` 目录。
   - a. 输入 `ls /etc`
   - b. 按 <Enter>

你很可能在这个目录中找到一长串文件。使用 `ls -a` 列出文件。
   - c. 输入 `ls -a /etc`
   - d. 按 <Enter>

> 请记住，如果 `ls` 或 `ls -a` 产生的文件列表滚出屏幕，你可以使用 <Ctrl-S> 停止滚动，并使用 <Ctrl-Q> 恢复滚动。

4. 你还可以将 `ls` 的结果*管道*传输给 `more`。课程稍后会介绍管道，但这里的操作步骤足够简单，可以直接在此使用。在 shell 提示符下：
   - a. 输入 `ls /etc | more`
   - (确保管道符号 | 的两侧各留有一个空格。)
   - b. 按 <Enter>
   - c. 再次按 <Enter> 向下滚动一行。
   - d. 按 <Space Bar>（空格键）向下滚动一整屏。

5. 使用 `ls -l` 列出主目录中的文件。
   - a. 输入 `ls -l`
   - b. 按 <Enter>

6. 你可以组合开关。使用 `ls -la` 列出主目录中的文件。
   - a. 输入 `ls -la`
   - b. 按 <Enter>

7. `du` 会告诉你文件系统占用了多少空间。从你的主目录，输入以下内容：
   - a. 输入 `du`
   - b. 按 <Enter>

默认情况下，`du` 以*块*为单位报告文件大小。一个块通常是 1024 字节。当你使用适当的开关时，`du` 会以字节为单位报告文件使用情况。下一个练习将告诉你如何识别哪个开关对应哪种功能。

8. 与许多 Linux 命令一样，你可以使用开关来修改命令的输出。如何查找可用的开关及其作用？使用 `man`——即 manual（手册）的缩写。
   - a. 输入 `man du`
   - b. 按 <Enter>
   - c. 再次按 <Enter> 向下滚动一行。
   - d. 按 <Space Bar>（空格键）向下滚动一整屏。
   - e. 要退出 `man` 显示，按 <q>（代表“quit”/退出）。

图 5-3 显示了 `du` 的 `man` 结果的部分屏幕显示。

```
DU(1) DU(1)

名称

du - 估算文件空间使用情况

概要

du [OPTION]... [FILE]...

描述

汇总每个 FILE 的磁盘使用情况，对于目录则递归执行。

- -a, --all

  写入所有文件的计数，而不仅仅是目录

- -block-size=SIZE

  使用 SIZE 字节的块

- -b, --bytes

  以字节为单位打印大小
```

![](img/cc8b9fd5970716027fba0d0a45c13900_82_0.png)

9. 与你的朋友、同事或同学中的几位商量好进行一些互相查看。切换到其中一个人的主目录。使用 `ls` 加上你在这些练习中使用过的数字开关，将他们的目录结构中的文件数量和类型与你自己的目录内容进行比较。

10. 你使用 `du` 来查找你的文件占用了多少磁盘空间。现在使用 `du` 从你预先安排好的窥探小组中一些成员的文件系统获取相同的信息。

11. 请记住，`du` 报告文件使用情况时是从当前目录开始，包括该层级中的所有子目录。在练习 7 中，你使用 `du` 显示了你文件系统的相关信息。将这些结果与以下结果进行比较：
    - a. 输入 `cd /`
    - b. 按 <Enter>
    - c. 输入 `du`
    - d. 按 <Enter>

> 请记住，你可以使用 <Ctrl-C> 中断大多数命令的输出。

12. 与 `du` 不同，`df` 报告整个硬盘的空闲空间。为了确认这一点，请执行以下操作：
    - a. 输入 `cd /`
    - b. 按 <Enter>
    - c. 输入 `df`
    - d. 按 <Enter>
    你在屏幕上看到的是 `df` 从你的主目录提供的显示结果。
    - e. 输入 `cd /`
    - f. 按 <Enter>
    - g. 输入 `df`
    - h. 按 <Enter>
    你在屏幕上看到的是 `df` 从根目录提供的显示结果。你可以看到，无论你执行该命令时身处哪个目录，`df` 命令提供的信息都是相同的。

13. 在这个练习中，你将使用 `cd` 切换到你的主目录。然后，你将创建一个名为 `practice` 的目录。
    - a. 在 shell 提示符下，输入 `cd`
    - b. 按 <Enter>
    - c. 输入 `mkdir practice`
    - d. 按 <Enter>
    - e. 输入 `ls`
    - f. 按 <Enter> 并注意到你刚刚创建的目录。

14. 在这个练习中，你将使用 `cd` 切换到目录 `practice`。接下来，你将创建一个名为 `practice.temp` 的目录，并使用 `ls` 确认目录 `practice.temp` 存在。
    - a. 输入 `cd practice`
    - b. 按 <Enter>
    - c. 使用你在练习 13 中练习的内容创建目录 `practice.temp`，然后使用 `ls` 确认你的成功。

15. 在这个练习中，你将尝试删除目录 `practice`。我们的指导步骤将引导你经历一个会导致系统返回错误信息的过程。在执行此练习时，通过尝试识别错误的指示步骤来测试自己。
    - a. 输入 `cd`
    - b. 按 <Enter>
    - c. 输入 `rmdir practice`
    - d. 按 <Enter>

系统将返回一条类似以下的错误信息：

```
rmdir: practice: Directory not empty.
```

在这个练习中，第一步将你带回主目录。`practice` 是你的目录之一，但它不是空的。你还记得 `rmdir` 不允许你删除非空目录吗？为了能够删除目录 `practice`，你必须先删除其子目录 `practice.temp`。

16. 在这个练习中，你将删除子目录 `practice.temp`。
    - a. 输入 `cd practice`
    - b. 按 <Enter>
    - c. 输入 `rmdir practice.temp`
    - d. 按 <Enter>

17. 让我们来纠正一个打字错误。使用 <Ctrl-H> 将 `ls -z` 更改为 `ls -l`。
    - a. 输入 `ls -z`
    - b. 按 <Ctrl-H> 擦除 "z"。
    - c. 输入 `l`
    - d. 按 <Enter>

如果在步骤 a 中按 <Ctrl-H> 删除了你输入的所有字符，那么在步骤 c 中你需要输入 `ls -l`。

#### 自我检测

当 Diamond Office Supply 雇用 Sallie 时，她丰富的市场营销背景给公司留下了深刻印象。虽然她对 Windows 环境的熟悉程度帮助她高效地学习使用 Linux，但她在文件系统方面仍然有些吃不准。

1. Sallie 决定她的第一项任务应该是创建她用来管理电脑文件的目录结构。Sallie 坐在终端前，看到了图 5-4 中所示的屏幕。

```
.calendar
phone_list
sacr.feb99
to_do
$ _
```

![](img/cc8b9fd5970716027fba0d0a45c13900_85_0.png)

Sallie 应该从这个屏幕开始创建她的第一个新子目录吗？

a. 是的。这个子目录中文件很少，表明还有很多空间。
b. 否。名为 `.calendar` 的文件是一个通常隐藏的文件，你不应该在包含隐藏文件的目录中创建子目录。
c. 否。这个屏幕没有向 Sallie 表明她在文件系统中的位置。
d. 是的。子目录放在哪里其实并不重要。

2. 哪个命令可以告诉 Sallie 当前打开的是哪个目录？

a. `cd`
b. `ls`
c. `mkdir`
d. `pwd`

3. Sallie 应该在哪里创建她的目录结构？

a. 在她的家目录中
b. 没关系，只要她记得住就行。
c. 在 `/home` 之下
d. 在文件系统中任何没有很多子目录的地方

4. Sallie 应该使用哪个命令切换到她的家目录？

a. `cd`
b. `ls`
c. `mkdir`
d. `pwd`

5. Sallie 的用户 ID 是 Salrb。以下哪项代表 Sallie 的家目录？

a. `/etc/Salrb`
b. `/home/Salrb`
c. `/usr/Salrb`
d. `/home/Salrb`

6. Sallie 记得她的家目录有一个简写名称。它是什么？

a. `home`
b. `$HOME`
c. `HOME`
d. `home/$HOME`

7. Sallie 知道她将积累大量关于销售联系人的信息。她决定创建一个名为 `contacts` 的目录。Sallie 将使用什么命令来创建这个新目录？

a. `make contacts`
b. `newdir contacts`
c. `makedir contacts`
d. `mkdir contacts`

8. Sallie 想在 `contacts` 下创建独立的子目录：一个用于当前客户的联系人，另一个用于潜在客户的联系人。图 5-5 展示了 Sallie 在该过程中的第一步。

```
S pwd
/home/Sal/rb
S |
```

#### 图 5-5 Sallie 准备创建新目录时的第一步

Sallie 的下一步应该是什么？

a. `mkdir current`
b. `mkdir prospective`
c. `cd contacts`
d. `cd`

9. 一贯乐观的 Sara 建议 Sallie 将目录名称从 “prospective” 改为 “future”。Sallie 将使用哪个命令？

a. `mv prospective future`
b. `rename prospective future`
c. `mv future prospective`
d. 以上都不是

10. Sallie 使用了哪个命令生成了图 5-6 中的文件列表？

a. `ls`
b. `ls -l`
c. `ls -v`
d. `ls -r`

```
assessment
biannual
contacts
floppy
letters
salesrepts
suppliers
Temp
$ |
```

图 5-6 Sallie 的文件显示

11. 图 5-7 中的图片有什么问题？

```
$ ls
drwx------ 1 Salrb sales 64 May 1 8:23 Temp
-rw-rw-- 2 Salrb sales 2309 May 8 13:13 assessment
drwrx-xF-- 8 sara admin 11489 May 12 9:12 biannual
drwxr-x--- 1 Salrb sales 1632 Feb 22 10:30 contacts
drwx------- 1 Salrb sales 64 Jun 1 4:12 floppy
drw-r----- 1 Salrb sales 23259 Mar 4 12:31 letters
drwrx-r-x 9 Salrb sales 66279 May 15 15:58 sales.repts
drwxr-x--- 4 Salrb sales 1243 Dec 2 11:47 suppliers
$ |
```

图 5-7 问题 11 的文件显示

a. Sara 不是管理员。
b. `ls -l` 命令不会生成此列表。
c. `ls` 命令不会生成此列表。
d. 没有问题

12. 图 5-8 中箭头所指的列表示该条目是

a. 隐藏的
b. 普通文件或目录
c. 受删除保护
d. 设备文件

![](img/cc8b9fd5970716027fba0d0a45c13900_89_0.png)

问题 12 的文件显示

13. 在图 5-9 中，大括号括起的列表示文件的

a. 权限
b. 所有者
c. 组
d. 模式

![](img/cc8b9fd5970716027fba0d0a45c13900_89_1.png)

问题 13 的文件显示

14. 在图 5-10 中，箭头所指的列表示文件的

a. 权限
b. 所有者
c. 组
d. 模式

![](img/cc8b9fd5970716027fba0d0a45c13900_90_0.png)

图 5-10 问题 14 的文件显示

15. 在图 5-11 中，箭头所指的列表示文件的

a. 权限
b. 所有者
c. 组
d. 模式

![](img/cc8b9fd5970716027fba0d0a45c13900_90_1.png)

图 5-11 问题 15 的文件显示

16. Sallie 已经将目录 `letters` 复制到了 `contacts` 下的一个子目录中。她想从她的家目录中删除目录 `letters`。她将使用哪个命令？

a. `rmdir`
b. `deldir`
c. `remdir`
d. `mvdir`

17. 在使用命令删除目录 `letters` 之前，Sallie 应该做什么？

a. 阅读所有信件，以确保她不需要保留其中一些。
b. 与系统管理员沟通，以确保删除目录是可以的。
c. 别再担心了，直接删除目录。
d. 确保目录为空。

18. 如果 `letters` 中包含文件，当 Sallie 使用命令删除该目录时会发生什么？

a. 目录将被删除，所有文件也会丢失。
b. 系统将返回一条错误消息，并且不会删除该目录。
c. 在删除目录之前，系统将返回一个提示，类似于“你确定吗？”。这给 Sallie 一个改变主意的机会。
d. 文件将被复制到临时目录 `temp`，并且目录 `letters` 将被删除。

19. Sallie 正在她的家目录中工作。Robert 的用户 ID 是 Roband。她将使用哪个命令切换到 Robert 的家目录？

a. `cd /home/Roband`
b. `cd \home\Roband`
c. `cd /Roband`
d. `cd \Roband`

20. 系统策略规定了任何个人在文件系统中可以使用的空间限制。Sallie 应该使用哪个命令来查看她的文件已经占用了多少空间？

a. `df`
b. `du`
c. `ds`
d. `do`

21. Sallie 正在查看图 5-12 中的屏幕。如果她从这个文件系统位置使用 `du`，她能否得到关于她的账户占用空间准确度的画面？

![](img/cc8b9fd5970716027fba0d0a45c13900_92_0.png)

图 5-12 问题 21 的文件显示

a. 否。她应该先使用 `cd /`，这样她获得的信息将关于她的完整账户。
b. 当然，如果她想要这些信息的话。
c. 是的，前提是她首先获得了系统管理员的批准。
d. 否。她应该先使用 `cd`，这样她获得的信息将关于她的完整账户。

> 请记住，`du` 提供的报告包括当前目录及其子目录的信息。

22. 给定问题 21 中的屏幕（图 5-12），Sallie 可以使用 `cd` 或 `cd ..` 返回她的家目录。

a. 正确
b. 错误

23. 命令 `ls` 和 `ls -l` 将产生不同的结果。

a. 正确
b. 错误

24. Sallie 正在查看图 5-13 中的屏幕，然后执行了图 5-14 中所示的操作。请解释错误消息。
