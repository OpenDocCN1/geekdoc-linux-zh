
第一个 `find` 命令在当前 Downloads 目录内搜索，而第二个则在用户主目录下搜索。

`find` 命令非常复杂，因此它不会包含在 Linux Essentials 考试中。然而，它是一个强大的工具，在实践中特别有用。

### 引导性练习

1. 使用 `man` 命令查找每个命令的作用：

| 命令 | 描述 |
| --- | --- |
| ls | 显示目录内容。 |
| cat | |
| cut | |
| cd | |
| cp | |
| mv | |
| mkdir | |
| touch | |
| wc | |
| passwd | |
| rm | |
| rmdir | |
| more | |
| less | |
| whereis | |
| head | |
| tail | |
| sort | |
| tr | |
| chmod | |
| grep | |

2. 打开 `ls` 的 info 页面并识别 MENU（菜单）部分。

- 你有哪些可用选项？

- 找到允许你按修改时间对输出进行排序的选项。

3. 显示前 3 个 README 文件的路径。使用 `man` 命令识别 `locate` 的正确选项。

4. 在你的主目录下创建一个名为 `test` 的文件。使用 `locate` 命令找到它的绝对路径。

5. 你立即找到它了吗？为了让 `locate` 找到它，你必须执行什么？

6. 使用 `find` 命令搜索你之前创建的 test 文件。你使用了什么语法？绝对路径是什么？

### 探索性练习

- 1. 上表中有一个命令没有 man page（帮助手册）。它是哪一个？你认为为什么该命令没有 man page？

- 2. 使用上表中的命令创建以下文件树。以大写字母开头的名字是目录，小写字母的是文件。

```
User

| Documents

| | Hello

| | | hey2

| | | helloa

| | | ola5

| | | World

| | | earth9

| Downloads

| | Music

| | Songs

| | | collection1

| | | collection2

| Test

| | passa

test
```

- 3. 在屏幕上显示当前工作目录，包括子文件夹。

- 4. 在树中搜索所有以数字结尾的文件。

- 5. 使用单个命令删除整个目录树。

### 总结

在本节中，你学习了：

- 如何获取帮助
- 如何使用 `man` 命令
- 如何在 man page 中导航
- man page 的不同部分
- 如何使用 `info` 命令
- 如何在不同节点之间导航
- 如何在系统中搜索文件

练习中使用的命令：

`man`
显示 man page。

`info`
显示 info 页面。

`locate`
在 locate 数据库中搜索特定名称的文件。

`find`
在文件系统中搜索符合一组选择标准的文件。

`updatedb`
更新 locate 数据库。

### 引导性练习答案

1. 使用 `man` 命令查找每个命令的作用：

| 命令 | 描述 |
|---|---|
| ls | 显示目录内容。 |
| cat | 合并或查看文本文件 |
| cut | 从文本文件中删除某些部分 |
| cd | 切换到不同的目录 |
| cp | 复制文件 |
| mv | 移动文件（也可用于重命名） |
| mkdir | 创建新目录 |
| touch | 创建文件或修改现有文件的最后修改时间和日期 |
| wc | 统计文件的字数、行数或字节数 |
| password | 修改用户密码 | || rm | 删除文件 |
| rmdir | 删除目录 |
| more | 一页一次地查看文本文件 |
| less | 查看文本文件，允许逐行或逐页向上向下滚动 |
| whereis | 显示程序所在的路径 |
| head | 显示文件的前几行 |
| tail | 显示文件的后几行 |
| sort | 对文件进行排序 |
| tr | 翻译或转换字符 |
| chmod | 修改权限 |
| grep | 在文件中搜索 |

2. 打开 `ls` 的 info 页面并识别 MENU。

- 你有哪些可用选项？

- 哪些文件出了
- 关于输出的信息
- 关于版本
- 输出格式
- 输出文件名

3. 显示前 3 个 README 文件的路径。使用 `man` 命令识别 `locate` 的正确选项。

```
$ locate -l 3 README

/etc/alternatives/README

/etc/init.d/README

/etc/rc0.d/README
```

4. 在你的主目录下创建一个名为 `test` 的文件。使用 `locate` 命令找到它的绝对路径。

```
$ touch test

$ locate test

/home/user/test
```

5. 你立即找到它了吗？为了让 `locate` 找到它，你必须执行什么？

```
$ sudo updatedb
```

文件是新创建的，因此数据库中没有它的记录。

6. 使用 `find` 命令搜索你之前创建的 test 文件。你使用了什么语法？绝对路径是什么？

```
$ find ~ -name test
```

或者

```
$ find . -name test
/home/user/test
```

### 探索性练习答案

- 1. 上表中有一个命令没有 man page。它是哪一个？你认为为什么该命令没有 man page？

`cd` 命令。它是 shell 的内置命令。

- 2. 使用上表中的命令创建以下文件树。以大写字母开头的名字是目录，小写字母的是文件。

解决方案是 `mkdir` 和 `touch`。

- 3. 在屏幕上显示当前工作目录，包括子文件夹。

```
$ ls -R
```

- 4. 在树中搜索所有以数字结尾的文件。

```
$ find ~ -name "*0-9]"
```

- 5. 使用单个命令删除整个目录树。

```
$ rm -rf Documents
```

目录之间的关系用正斜杠（`/`）表示。我们知道 Reports 是 Documents 的子目录，而 Documents 是 user 的子目录，user 位于一个名为 home 的目录中。home 似乎没有父目录，但事实并非如此。home 的父目录称为 root，由第一个斜杠（`/`）表示。我们将在后面的章节中讨论根目录。

请注意，`pwd` 命令的输出与命令行提示符给出的路径略有不同。命令行提示符不是 `/home/user`，而是包含一个波浪号（`~`）。这是一个代表用户家目录的特殊字符。我们将在下一节中详细介绍这一点。

## 列出目录内容

使用 `ls` 命令列出当前目录的内容：

```
user@hostname ~/Documents/Reports $ ls

report2018.txt
```

注意，`ls` 不提供任何关于父目录的信息。同样，默认情况下，`ls` 不显示任何关于子目录内容的信息。`ls` 只能“看到”当前目录中的内容。

## 更改当前目录

Linux 中的导航主要通过 `cd` 命令完成。该命令用于更改目录。通过之前的之前的 `pwd` 命令，我们知道当前目录是 `/home/user/Documents/Reports`。我们可以通过输入新路径来更改当前目录：

```
user@hostname ~ cd /home/user/Documents

user@hostname ~/Documents $ pwd

/home/user/Documents

user@hostname ~/Documents $ ls

Mission-Statement.txt Reports
```

从新位置开始，我们可以“看到”Mission-Statement.txt 和我们的子目录 Reports，但无法看到子目录的内容。我们可以这样返回 Reports：

```
user@hostname ~/Documents cd Reports

user@hostname ~/Documents/Reports $ pwd

/home/user/Documents/Reports
```

```
user@hostname ~/Documents/Reports $ ls -l

report2018.txt
```

我们现在已经回到了起点。

## 绝对路径与相对路径

`pwd` 命令始终打印**绝对路径**。这意味着路径包含了路径中的每一个步阶，从文件系统的顶端（`/`）到终端（Reports）。绝对路径始终以 `/` 开头。

```
/

home

  user

    Documents

      Reports
