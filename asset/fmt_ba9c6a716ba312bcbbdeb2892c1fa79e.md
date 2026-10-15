
5. 如果你想在同一条命令行上使用多个选项，请在单个连字符后输入所有选项。例如，输入 `who -uH` 并按 `Enter` 以查看带有空闲时间和列标题的用户列表。

6. 输入 `who -q` 并按 `Enter` 查看当前用户的快速列表。你将看到一个类似下面的列表，它只显示登录名和系统上的用户总数。

```
mpaler sjones
## users=3
```

7. 要确定你正在使用哪个终端或登录时间，请在命令行中输入 `who am` 并按 `Enter`（见图 1-15）。出现了什么信息？如果你不确定，输入 `who am i -H` 并按 `Enter` 查看列标题。（另一个选项是输入 `whoamni` 写成一个单词，它只显示你的账户名或用户 ID，以防你不确定当前正在使用哪个账户；此选项供系统管理员使用。还请尝试输入 `who mom` 看看你发现了什么。）

![](img/0a988e998d76ede7c21a57edbc89e490_62_0.png)

如果你为命令提供两个参数，你将看到第 7 步描述的输出。例如，你可以输入 `who are` 或 `who x x x` 来查看相同的信息。传统上，UNIX/Linux 用户输入 `who am i` 来查看描述会话的信息。

![](img/0a988e998d76ede7c21a57edbc89e490_62_1.png)

另一个与 who is 类似的命令是 `w` 命令。系统管理员使用 `w` 命令不仅查看谁已登录，还查看在使用哪些系统资源（如 CPU 资源）。

## 实践项目

![](img/0a988e998d76ede7c21a57edbc89e490_63_0.png)

**图 1-15** 使用 who am i

## 项目 1-6

此时，你的屏幕可能看起来满了命令及其结果。每当你想要一个空白的屏幕时，都可以随时使用 `clear` 命令。这个项目将使你现在能够清除屏幕。

**清除屏幕：**
- 1. 在命令行上输入 `clear` 并按 `Enter`。命令行提示符现在位于屏幕的左上角。

## 项目 1-7

你可以使用手册页（manual pages）学习更多关于命令或程序的信息（如果该程序在手册页中有记录）。此外，`whatis` 提供特定命令和程序的快速摘要。在这个项目中，你将同时使用 `man` 和 `whatis` 命令。在使用 `whatis` 命令之前，应该已经创建了数据库。

**使用 man 显示在线帮助：**
- 1. 在命令行中输入 `man who` 并按 `Enter`。你将看到图 1-16 所示的 `who` 命令的解释。
- 2. 按一次或多次 `Enter` 以查看更多行文本。接着按 `Spacebar`（空格键）查看更多文档页。
- 3. 输入 `q` 退出 man 程序。

# 第 1 章 UNIX 和 Linux 的本质

```
mpalmer@localhost:~
File Edit View Terminal Tabs Help
WHO(1)                               User Commands                               WHO(1)
NAME
who - 显示谁已登录
SYNOPSIS
who [OPTION]... [ FILE | ARG1 ARG2]
DESCRIPTION
-a, --all
    同于 -b -d --login -p -r -t -u
-b, --boot
    上一次系统启动的时间
-d, --dead
    打印死进程
-H, --heading
    打印列标题行
-l, --login
    打印系统登录进程
```

图 1-16 使用 man 查找更多关于 who 命令的信息

- 4. 输入 `man` 并按 `Enter`。你将看到描述 `man` 命令的页面。`-M` 选项的目的是什么？
- 5. 输入 `q` 退出 `man` 程序。

**使用 whatis 命令显示命令的简要描述：**
- 1. 输入 `whatis` 并按 `Enter`。
- 2. 你看到 `who` 命令的摘要如下：

who (1) - 显示谁在系统上

who (1) - 显示谁已登录

## 项目 1-8

当你输入命令出错时，不需要重新输入整个命令。你可以使用命令行编辑功能。在这个项目中你将练习这些功能。

**在行上编辑命令：**
- 1. 首先确定你正在使用的 shell。输入 `echo SHELL` 并按 `Enter`。如果你使用的是 Bash shell，你会看到：

```
/bin/bash
```

如果你没有使用 Bash shell，输入 `bash` 并按 `Enter`。
- 2. 输入 `who am i` 但不要按 `Enter`。

![](img/0a988e998d76ede7c21a57edbc89e490_64_0.png)
- 3. 按左方向键将光标移动到单词 "am"。
- 4. 按 `Alt+d` 删除 "am。"
- 5. 按 `Ctrl+k` 删除当前位置的命令行。
- 6. 按 `Ctrl+a` 将光标移动到行首。
- 7. 再次按 `Ctrl+k` 删除。
- 8. 重输命令 `who am i` 但不要按 `Enter`。
- 9. 按八次 `Ctrl+b` 直到光标位于开头。
- 10. 按三次 `Alt+l`。每按一次，光标移动到下一个单词的字符之前。
- 11. 按 `Ctrl+a`，然后按 `Ctrl+k` 清除命令行。

![](img/0a988e998d76ede7c21a57edbc89e490_65_0.png)

## 项目 1-9

你可以在命令之间使用分号在同一行执行多个命令。在这个项目中练习运行命令。

**在行上输入多个命令：**
- 1. 输入 `date; cal` 并按 `Enter` 查看当前日期和本月日历。在分号前后加空格是有效的。例如，你可以输入 `date; cal`。
- 2. 输入 `who -u` 并按 `Enter`（见图 1-17）。date 命令产生第一行；剩余部分是 who 命令的结果。

![](img/0a988e998d76ede7c21a57edbc89e490_65_1.png)

## 项目 1-10

在这个项目中，使用 Bash shell 的历史功能调用你之前使用的命令。你会发现，越使用 UNIX/Linux，这个命令行功能就能节省大量的重复输入时间。

**使用命令行历史：**
- 1. 输入 `date` 并按 `Enter`。
- 2. 输入 `who` 并按 `Enter`。
- 3. 输入 `who -u` 并按 `Enter`。
- 4. 输入 `clear` 并按 `Enter`。
- 5. 按四次上方向键。date 命令被调到了命令行。不要按 `Enter`。
- 6. 按两次下方向键。你看到了什么命令？按 `Enter` 执行该命令。

![](img/0a988e998d76ede7c21a57edbc89e490_66_0.png)

```
mpalmer@localhost:~
File Edit View Terminal Tabs Help
[mpalmer@localhost~]$ date ; cal
Sat Nov 21 10:57:22 MST 2009
November 2009
Su Mo We Th Fr Sa
1 2 3 4 5 6 7
8 9 10 11 12 13 14
15 16 17 18 19 20 21
22 23 24 25 26 27 28
29 30

[mpalmer@localhost~]$ date ; -uH
Sat Nov 21 10:57:56 MST 2009
NAME LINE TIME IDLE PID COMMAND
mpalmer pts/1 2009-11-21 10:57 . 2978 (:0.0)
[mpalmer@localhost~]$ 
```

**图 1-17** 在一条命令行上执行多个命令

## 项目 1-11

密码是你保护用户账户免受可能尝试未经授权访问的手段。计划经常更改密码以保持账户安全。在这个项目中，你将学习如何更改密码。

**更改密码：**
- 1. 在命令行提示符后输入 `passwd` 并按 `Enter`。
- 2. 输入你的当前密码并按 `Enter`。（在某些系统中，如果你登录的是 root 账户，则跳过此步直接进入第 3 步。）
- 3. 输入你的新密码并按 `Enter`。在输入时，屏幕上不会显示新密码。
- 4. 再次输入新密码并按 `Enter`，以便 UNIX/Linux 确认你的新密码。
