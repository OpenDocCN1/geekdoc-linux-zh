
图 6-23 展示了你正在链接的*目录*的文件模式必须是什么样子的。你只需关注第 4、5 和 6 位。

```
   123 456 789
  d  rwx  r-X  ---
```

![](img/cc8b9fd5970716027fba0d0a45c13900_121_0.png)

如果第 4、5 和 6 位看起来像这样——**rwx**——那就没问题。如果缺少 **r** 或 **x**，目录的所有者必须从*directoryname*的*父目录*中执行以下命令：

- a. 键入 `chmod g+rx directoryname`
- b. 按下 <Enter>

在步骤 a 中，目录的所有者会将*directoryname*替换为目录的实际名称。

图 6-24 展示了你正在链接的*文件*的文件模式必须是什么样子的。同样，你只需关注第 4、5 和 6 位。

```
   123 456 789
  rwx  r--  ---
```

![](img/cc8b9fd5970716027fba0d0a45c13900_121_1.png)

如果第 4、5 和 6 位看起来像这样——**rwx** 或 **rw-**——那就没问题。如果缺少 **r**，目录的所有者必须从*包含 linkfile 的目录*中执行以下命令：

- c. 键入 `chmod g+r linkfile`
- d. 按下 <Enter>

在步骤 c 中，文件的所有者会将*linkfile*替换为文件的实际名称。

请记住，在这种场景中，你既是一个合作伙伴，必须确保她的目录和文件已正确准备就绪，又是创建指向他人文件链接的人。

**44.** 你的*userid*是**ronsm**。创建一个名为*linkfile*的文本文件的链接。你的合作伙伴（*linkfile*的所有者）的*userid*是**sam4**。

- a. 键入 `ln /home/sam4/linked_directory/linkfile`
  - 你需要将*linked_directory*和*linkfile*替换为实际目录和文件的名称。
- b. 按下 <Enter>
- c. 键入 `ls -l /home/sam4/linked_directory`
  - 这将列出合作伙伴账户中包含链接文件的目录。你需要将*linked_directory*替换为实际目录的名称。
- d. 按下 <Enter>

你的屏幕看起来会类似于图 6-25 中的部分目录列表。

```
$ ls -l /home/sam4/linked_directory
-rwxr--r-- 2 sam4 1024... linked_file
$ 
```

### 图 6-25 sam4 目录的列表，显示链接文件

注意，*linked_file*有两个链接。第二个链接代表你刚刚创建的链接。

当你列出你自己（**ronsm**）包含该链接的目录时，你的屏幕看起来会类似于图 6-26 中的部分目录列表。

```
$ ls -l
-rw-r--r---- 1 ronsm 1024......file1
-rw-r--r---- 1 ronsm 1024......file1
-rwxr-r--r-- 2 sam4 1024......linked_file
```

### 图 6-26 你自己（rons m）目录的列表，显示指向合作伙伴（sam4）文件的链接

注意，目录列表表明 linked_file 的所有者是 sam4。

- 45. 读取链接文件。
  - a. 键入 `cat linked_file`
  - b. 按下 <Enter>

请记住，在步骤 a 中，你需要输入链接文件的名称。你将在屏幕上看到链接文件的内容。

## 自我检测

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

### 图 6-27 第 9 和 10 题使用此屏幕

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

### 图 6-28 第 26 题的屏幕

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

### 图 6-29 第 28 和 29 题的屏幕

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
  - a. 正确。
  - b. 错误。 `rm` 仅允许删除单个文件。

