
现在，你已经把 Robert 的所有供应文件集中在一个地方并进行了备份，他要求你查找文件中的特定信息。例如，哪个文件包含关于文件的信息？文件夹？磁带？为此，你将使用 `grep`，它代表“globally search for a regular expression and print it”（全局搜索正则表达式并打印它）。

### 36. 哪些文件包含关于笔的信息？

- a. 输入 `grep pens *`
- b. 按 <Enter>

`grep` 命令行需要两个参数：(1) 要搜索的文本和 (2) 要搜索的文件。星号意味着“所有文件”。

你的搜索结果应类似于图 6-17。

```
$ grep pens *
supply1:writing -- pens.
supply3:correction pens
$
```

![](img/cc8b9fd5970716027fba0d0a45c13900_116_0.png)

如果你的结果与你在图 6-17 中看到的不匹配，也许你的输入没有你预期的那么仔细。如果图 6-17 中列出的某个文件未出现在你的屏幕上，请使用 `cat` 读取该文件。如果发现错误，请使用 `cat > filename` 重新创建该文件。（你将用文件的实际名称替换 `filename`。）

在某些 shell 中，当你输入 `cat > filename` 时，如果文件名已存在，你会收到错误信息，类似于：`cat > filename: file exists`。系统不会让你覆盖已存在的文件。在这种情况下，你必须先用 `rm` 删除该文件，然后再重新创建它。

### 37. 哪些文件包含关于特殊物品的信息？

- a. 输入 `grep specialty *`
- b. 按 <Enter>

你的搜索结果应类似于图 6-18。

```
$ grep specialty *
supply6:staplers -- specialty
supply7:tape -- specialty
supply9:folders -- specialty file
```

图 6-18 `grep` 搜索 "specialty"

### 38. 哪些文件包含关于 Post-It® 便签的信息？

- a. 输入 `grep post-it *`（是的，小写。）
- b. 按 <Enter>

你的屏幕将类似于图 6-19。

```
$ grep post-it *
$
```

图 6-19 `grep post-it *` 的结果

系统只返回 shell 提示符，这意味着 `grep` 未在任何文件中找到目标文本。但这是预期之中的：Linux 区分大小写，而你在创建该特定文件时使用的是“Post-It”——大写的“P”和大写的“I”。你可以通过在命令行中添加 `-i` 开关来告诉 `grep` 忽略大小写。

### 39. 使用 `grep -i` 搜索 “Post-It”。

- a. 输入 `grep -i post-it *`
- b. 按 <Enter>

你的屏幕将类似于图 6-20。

```
$ grep post-it -i *
supply10:Post-It -- pads
supply10:Post-It -- pop-up
supply10:Post-It -- printed
$
```

图 6-20 不区分大小写的 grep 搜索

### 40. Robert 要求你在 Post-It 文件 supply10 中追加一条注释，提醒他在 2 月 27 日重新订购。你将使用 cat 配合双重重定向符号 >>。

- a. 输入 `cat >> supply10`
- b. 按 <Enter>
- c. 输入 `Reorder 2/27`
- d. 按 <Enter> 将光标移至下一行。
- e. 按 <Enter> 在新文本下方添加一个空行。
- f. 按 <Ctrl-D>

### 41. 现在查看 supply10 的新版本。

- a. 输入 `cat supply10`
- b. 按 <Enter>

你的屏幕应类似于图 6-21。

```
$ cat supply10
Post-It notes -- pads
Post-It notes -- pop-up
Post-It notes -- printed
Reorder 2/27
$
```

图 6-21 添加了追加文本的 supply10

你向 Robert 建议，处理一个稍大一点的文件比处理多个小文件更有效率。Robert 同意了。

### 42. 将六个供应文件合并为一个。

- a. 输入 `cat supply1 supply3 supply6 supply7 supply9 supply10 > supply`

命令行可能会跨越两行。Linux 可以解释跨越多行屏幕的命令行。

- b. 按 <Enter>

现在读取新文件。

- c. 输入 `cat supply`
- d. 按 <Enter>

下一个合乎逻辑的步骤可能是打印该文件。为此，你会使用 `lpr`——例如，`lpr supply`。但由于关于打印机使用的准则因系统而异，我们无法在此处包含打印练习。请咨询你的讲师或系统管理员了解有关你系统上打印机使用的信息。

对于最后一组练习，你将是——而不是 Robert 的实习生。要完成这一系列练习，你需要与另一名学生、朋友或同事合作。

你将创建指向另一个用户账户中文本文件的链接。然后你将读取该文本文件。这将要求你能够列出该账户中的目录，并且知道哪些文件是文本文件。

为了演示，我们将假设另一个用户的 `userid` 是 `sam4`。你的 `userid` 是 `ronsm`。

### 43. 列出 sam4 的主账户。

- a. 输入 `ls -l /home/sam4`
- b. 按 <Enter>

你的屏幕将类似于图 6-22。

```
$ ls -l /home/sam4
drwxr-xr- 1 sam4 users 1024.. accounts
drwxr-xr- 1 sam4 users 1024.. practice
drwxr-xr- 1 sam4 users 1024.. webstuff
$
```

![](img/cc8b9fd5970716027fba0d0a45c13900_120_0.png)

在某些系统中，主账户可能位于 `/home` 以外的某个目录中。例如，在你刚刚完成的链接练习中，你可能需要输入 `/accounts/sam4` 或 `/users/sam4` 以反映你系统上正确的用户目录。

我们目前的关注点是文件模式，由图 6-22 中的这些字符表示：`rwxr-xr-`。我们在 CBT 课程的前一个模块 *Linux Directories*（Linux 目录）中提供了文件模式的概述，并将在名为 *Security*（安全）的模块中详细讲解文件模式。

就我们目前的目的而言，我们要指出，当你创建一个文件的链接时，你正在创建指向*位于*某个目录*内*的文件*的*链接。如果你要能够创建链接*并*读取文件，那么文件和目录都需要特定的权限。我们将向你展示权限必须是什么，以及在必要时如何更改它们。但对于文件模式和权限的详细解释，我们将参考 *Linux Made Easy CBT* 中的 *Security* 模块以及本指南中相应的安全章节。

图 6-23 展示了你正在链接的*目录*的文件模式必须是什么样子的。你只需关注第 4、5 和 6 位。

```
   123 456 789
  d  rwx  r-X  ---
```

![](img/cc8b9fd5970716027fba0d0a45c13900_121_0.png)

如果第 4、5 和 6 位看起来像这样——`rwx`——那就没问题。如果缺少 `r` 或 `x`，目录的所有者必须从 *directoryname* 的*父目录*中执行以下命令：

- a. 键入 `chmod g+rx directoryname`
- b. 按下 <Enter>

在步骤 a 中，目录的所有者会将 *directoryname* 替换为目录的实际名称。

图 6-24 展示了你正在链接的*文件*的文件模式必须是什么样子的。同样，你只需关注第 4、5 和 6 位。

```
   123 456 789
  rwx  r--  ---
```

![](img/cc8b9fd5970716027fba0d0a45c13900_121_1.png)

如果第 4、5 和 6 位看起来像这样——`rwx` 或 `rw-`——那就没问题。如果缺少 `r`，目录的所有者必须从*包含 linkfile 的目录*中执行以下命令：

- c. 键入 `chmod g+r linkfile`
- d. 按下 <Enter>

在步骤 c 中，文件的所有者会将 *linkfile* 替换为文件的实际名称。

请记住，在这种场景中，你既是一个合作伙伴，必须确保她的目录和文件已正确准备就绪，又是创建指向他人文件链接的人。

**44.** 你的 *userid* 是 `ronsm`。创建一个名为 *linkfile* 的文本文件的链接。你的合作伙伴（*linkfile* 的所有者）的 *userid* 是 `sam4`。

- a. 键入 `ln /home/sam4/linked_directory/linkfile`
  - 你需要将 *linked_directory* 和 *linkfile* 替换为实际目录和文件的名称。
- b. 按下 <Enter>
- c. 键入 `ls -l /home/sam4/linked_directory`
  - 这将列出合作伙伴账户中包含链接文件的目录。你需要将 *linked_directory* 替换为实际目录的名称。
- d. 按下 <Enter>

你的屏幕看起来会类似于图 6-25 中的部分目录列表。

```
$ ls -l /home/sam4/linked_directory
-rwxr--r-- 2 sam4 1024... linked_file
$ 
```

##### 图 6-25 sam4 目录的列表，显示链接文件

注意，*linked_file* 有两个链接。第二个链接代表你刚刚创建的链接。

当你列出你自己（`ronsm`）包含该链接的目录时，你的屏幕看起来会类似于图 6-26 中的部分目录列表。

```
$ ls -l
-rw-r--r---- 1 ronsm 1024......file1
-rw-r--r---- 1 ronsm 1024......file1
-rwxr-r--r-- 2 sam4 1024......linked_file
```

##### 图 6-26 你自己（ronsm）目录的列表，显示指向合作伙伴（sam4）文件的链接

注意，目录列表表明 `linked_file` 的所有者是 `sam4`。

- 45. 读取链接文件。
  - a. 键入 `cat linked_file`
  - b. 按下 <Enter>

请记住，在步骤 a 中，你需要输入链接文件的名称。你将在屏幕上看到链接文件的内容。

#### 自我检测

- 1. 目录是以下哪种类型？
  - a. 过滤器。
  - b. 命令。
  - c. 文件。
  - d. 列表。

- 2. 特殊文件和普通文件是同一类型文件的名称不同。
  - a. 正确
  - b. 错误

- 3. 目录不能包含其他目录。
  - a. 正确
  - b. 错误

- 4. 文件名中允许字符数因系统而异。你的系统很可能将上限设置为
  - a. 11 或 255。
  - b. 8 或 14。
  - c. 11 或 14。
  - d. 14 或 255。

- 5. 普通文件包含
  - a. 其他文件。
  - b. 将外设附加到系统的说明。
  - c. 你的数据、文本或程序。
  - d. 仅你的数据。

- 6. 文件名中的前导点表示该文件是
  - a. 受保护的。
  - b. 特殊的。
  - c. 隐藏的。
  - d. 一个目录。

- 7. 文件名只能包含字母和数字。
  - a. 正确
  - b. 错误

- 8. 文件名可以包含多个点。
  - a. 正确
  - b. 错误

使用图 6-27 回答第 9 和 10 题。

```
$ ls
chap chap1 chap12 chap2 chapter3
```

##### 图 6-27 第 9 和 10 题使用此屏幕

- 9. 当你使用 `ls chap*` 时，哪些文件将被列出？
  - a. chap1 和 chap2
  - b. chap, chap1, chap12, 和 chap2
  - c. chapter3
  - d. 全部

- 10. 当你使用 `ls chap?` 时，哪些文件将被列出？
  - a. chap1 和 chap2
  - b. chap, chap1, chap12, 和 chap2
  - c. chapter3
  - d. 全部

- 11. 你使用此命令来复制文件：
  - a. find
  - b. mv
  - c. cp
  - d. ln

- 12. 你使用此命令来删除文件：
  - a. tar
  - b. grep
  - c. sync
  - d. rm

- 13. 你使用此命令来重命名文件：
  - a. lp
  - b. cp
  - c. mv
  - d. cat

- 14. 你使用此命令来移动文件：
  - a. rm
  - b. mv
  - c. cp
  - d. find

- 15. 你使用此命令来读取文本文件：
  - a. ln
  - b. grep
  - c. lp
  - d. cat

- 16. 你使用此命令来创建文件的链接：
  - a. lp
  - b. cp
  - c. ln
  - d. cat

- 17. 你使用此命令来查找文件：
  - a. grep
  - b. cp
  - c. sync
  - d. find

- 18. 你使用此命令来在文件中查找文本：
  - a. find
  - b. grep
  - c. cp
  - d. cpio

- 19. 你使用此命令来打印文件：
  - a. cp
  - b. pr
  - c. cpr
  - d. lpr

- 20. 你使用此命令来确保你的文件已写入磁盘：
  - a. tar
  - b. wrd
  - c. sync
  - d. cat

- 21. 这两个命令用于备份你的文件：
  - a. tar, bk
  - b. bk, cpio
  - c. tar, cpio
  - d. cpio, sync

- 22. 复制文件并将复制的文件重命名的最有效方法是使用
  - a. cp
  - b. cp 和 mv
  - c. cp 和 cat
  - d. cat 和 mv

- 23. 复制文件并将该复制的文件放在不同目录中的最有效方法是使用
  - a. cp
  - b. cp 和 mv
  - c. cp 和 cat
  - d. cat 和 mv

- 24. directory1 是一个目录。此命令的结果是什么？ `cp file1 directory1/file2`
  - a. 系统会给你一个错误消息，大意是你不能复制名称不同的文件。
  - b. 系统会将 file1 复制到 directory1 并将复制的文件命名为 file2。
  - c. 系统会将 file1 复制到 directory1 并将复制的文件命名为 file1。
  - d. 系统会将 file1 追加到 directory1 中的 file2。

- 25. 你可以用一个命令将四个文件从一个目录复制到另一个目录。
  - a. 正确
  - b. 错误

- 26. 查看图 6-28。当你发出以下命令时，系统如何响应？ `cp thisfile directory1`

![](img/cc8b9fd5970716027fba0d0a45c13900_128_0.png)

##### 图 6-28 第 26 题的屏幕

- a. 系统将不允许你复制文件。
- b. 系统将警告你即将覆盖现有文件，但仍然允许你复制文件。
- c. 系统将复制文件并将新文件命名为 thisfile(1)。
- d. 系统将复制文件并覆盖现有文件，且没有警告。

- 27. directory1 是一个目录。此命令的结果是什么？ `mv newfile directory1/oldfile`
  - a. newfile 将从当前位置删除。
  - b. newfile 将移动到 directory1。
  - c. newfile 将移动到 directory1 并更名为 old-file。
  - d. 系统会给你一个错误消息，大意是你不能在同一个操作中移动文件并重命名。

使用图 6-29 中的部分目录列表回答第 28 和 29 题。

```
$ ls -1
drwxr-xr-x directory1
-rw-rw-r-- newfile
-rw-rw-r-- oldfile
-rw-rw-r-- thisfile
$ 
```

##### 图 6-29 第 28 和 29 题的屏幕

- 28. 此命令的结果是什么？ `mv newfile oldfile this-file directory2`
  - a. 系统会给你一个错误消息，大意是你不能同时移动三个文件。
  - b. 系统将复制文件。
  - c. 系统将移动文件。
  - d. 系统会给你一个类似“directory2: 没有那个文件或目录”的错误消息。

- 29. 此命令的结果是什么？ `mv newfile oldfile thisfile directory1`
  - a. 系统会给你一个错误消息，大意是你不能同时移动三个文件。
  - b. 系统将复制文件。
  - c. 系统将移动文件。
  - d. 系统将移动文件，但要求你确认每个文件的移动。

- 30. 命令 `rm file1 file2 file3` 将删除所有三个文件。
