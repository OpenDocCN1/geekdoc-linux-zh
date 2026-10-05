
## 标题

| HEADING | 描述 |
| :--- | :--- |
| NAME | 主题名称。通常是命令或文件名。简短的描述。 |
| SYNOPSIS | 命令语法的摘要。 |
| DESCRIPTION | 深入描述，以提供对该主题的基本理解。 |
| OPTIONS | 命令执行选项的说明。 |
| EXAMPLES | 如何使用命令、函数或文件的示例。 |
| FILES | 与 man 页相关的文件和目录列表。 |
| SEE ALSO | 相关信息，通常为其他 man 页。 |
| BUGS | 软件已知的错误。 |
| AUTHOR | 关于对该主题开发做出贡献的人的信息。 |

## 通过关键词搜索 man 页

使用 `man -k keyword` 对 man 页进行关键词搜索，它会显示一个与关键词匹配的 man 页列表，并列出章节。

```bash
$student@Desktop~$ man -k password
checkpasswdAccess (3) - 查询内核中的 SELinux 策略数据库。
passwd (8) - 以批模式更新密码
ckpasswd (8) - nrprpd 密码验证器
ckpasswd (8) - 重入式获取密码文件项
fgetwent_r (3) - 重入式获取密码文件项
getwent_r (3) - 重入式获取密码文件项
...
passwd (1) - 更新用户的身份令牌
sslpassword (issl) - 计算密码哈值
passwd (5) - 密码文件
passwd.ntp (5) - 连接到远程 NNTP 服务器的密码
passwd2des (3) - RFS 密码加密
```

常用的系统管理主题位于第1节（用户命令）、第5节（文件格式）和第8节（管理命令）。中。某些故障排除工具的管理员还会使用第2节（系统调用）。其余章节通常供程序员参考或高级管理使用。

> 注意
> 关键词搜索仅针对 `mandb(8)` 命令生成的索引进行，该命令必须以 root 身份运行。该命令通过 `cron.daily` 每日运行，或者在启动后一小时内过期通过 `anacrontab` 运行。

## 重要提示

**man 命令 -K**（大写）选项执行全文页面搜索，而不像 **-k** 选项那样只搜索标题和描述。全文搜索使用更多的系统资源并花费更多时间。

## 参考文献

- man(1), mandb(8), man-pages(7), less(1), intro(1), intro(2), intro(5), intro(7), intro(8) man 页

## 引导练习

## 阅读 man 页

在此练习中，你将练习使用 man 选项和参数查找相关信息。

## 结果

你应该能够使用 Linux 手册系统，并通过搜索和浏览找到有用信息。

## 开始之前

以用户 `student` 密码登录工作站。（注意：原文写为 "student student"，可能是对 "student" 或用户名/密码的笔误）。

在工作站上，运行 `lab help-manual start` 命令。它还会创建一个名为 `manual` 的文件。

```bash
[student@workstation ~]$ lab help-manual start
```

- 1. 在工作站上查看 gedit man 页。查看从命令行使用 gedit 编辑特定文件的选项。

使用 gedit man 页中的一个选项，使用文件末尾的光标打开 `/home/student/manual` 文件。

- 1.1. 查看 gedit man 页。

```bash
[student@workstation ~]$ gedit
```

| GEDIT(1) | 普通命令手册 | GEDIT(1) |
| :--- | :--- | :--- |
| gedit - 用于 GNOME 桌面的文本编辑器 | | |

**SYNOPSIS**
`gedit [OPTION...] [FILE...] [+LINE:COLUMN]`
`gedit [OPTION...]`

- 1.2. 在 gedit man 页中，学习从命令行编辑特定文件的选项。

```
...output omitted...
FILE 指定 gedit 启动时要打开的文件。
...output omitted...
+LINE 对于第一个文件，跳转到 LINE 指定的行（不要在 "+" 号和数字之间插入空格）。如果缺少 LINE，则跳转到最后一行。
```

...output omitted...

按 `q` 退出 man 页。

1.3. 使用 `gedit +` 命令打开手册文件。在 `+` 选项旁缺失的行将作为参数传递，在最后一行打开文件。

```bash
[student@workstation ~]$ gedit + manual
```

那只敏捷的棕色狐狸刚过来向那只懒贵狗打招呼！

确认文件已打开，且光标位于文件最后一行的结尾。按 `Ctrl+Q` 关闭应用程序。

- 读取 su(1) man 页。
注意，当用户使用 `su` 命令时假设用户是 root。如果 `su` 命令后跟着一个连字符 (`-`)，它将启动一个子 shell。如果没有连字符，则会创建一个与用户当前环境匹配的非登录子 shell。

```bash
[student@workstation ~]$ man 1 su
```

SU(1) 用户命令 SU(1)
**NAME**
su - 使用替换用户和组 ID 运行命令
**SYNOPSIS**
su [options] [-] [user [argument...]]]]

**DESCRIPTION**
允许使用替换用户和组 ID 运行命令。
在不带参数调用时，默认作为 root 运行交互式 shell。
...output omitted...
**OPTIONS**
...output omitted...
-, -1, --login
以登录 shell 启动 shell，其环境与真实登录相似
...output omitted...

> 注意
> 注意用户使用 `su` 命令时假设用户是 root。如果 `su` 命令后跟着一个连字符 (`-`)，它将启动一个子 shell。如果没有连字符，则会创建一个与用户当前环境匹配的非登录子 shell。

SU(1) 用户命令 SU(1)
**NAME**
su - 使用替换用户和组 ID 运行命令
**SYNOPSIS**
su [options] [-] [user [argument...]]]]

**DESCRIPTION**
允许使用替换用户和组 ID 运行命令。
在不带参数调用时，默认作为 root 运行交互式 shell。
...output omitted...
**OPTIONS**
...output omitted...
-, -1, --login
以登录 shell 启动 shell，其环境与真实登录相似
...output omitted...

（等待，OCR 文本这些乱了，让我们重新对齐）。

（此处重复内容略）

## 阅读 man 页

在此练习中，你将练习使用 man 选项和参数查找相关信息。

## 结果

你应该能够使用 Linux 手册系统，并通过搜索和浏览找到有用信息。

## 开始之前

以用户 `student` 密码登录工作站。

在工作站上，运行 `lab help-manual start` 命令。它还会创建一个名为 `manual` 的文件。

```bash
[student@workstation ~]$ lab help-manual
```

- 1. 在工作站上查看 gedit man 页。查看从命令行使用 gedit 编辑特定文件的选项。

使用 gedit man 页中的一个选项，使用文件末尾的光标打开 `/home/student/manual` 文件。

- 1.1. 查看 gedit man 页。

```bash
[student@workstation ~]$ gedit
```

| GEDIT(1) | 普通命令手册 | GEDIT(1) |
| :--- | :--- | :--- |
| gedit - 用于 GNOME 桌面的文本编辑器 | | |

**SYNOPSIS**
`gedit [OPTION...] [FILE...] [+LINE:COLUMN]`
`gedit [OPTION...]`

- 1.2. 在 gedit man 页中，学习从命令行编辑特定文件的选项。

```
...output omitted...
FILE 指定 gedit 启动时要打开的文件。
...output omitted...
+LINE 对于第一个文件，跳转到 LINE 指定的行（不要在 "+" 号和数字之间插入空格）。如果缺少 LINE，则跳转到最后一行。
```

...output omitted...

按 `q` 退出 man 页。

1.3. 使用 `gedit +` 命令打开手册文件。在 `+` 选项旁缺失的行将作为参数传递，在最后一行打开文件。

```bash
[student@workstation ~]$ gedit + manual
```

那只敏捷的棕色狐狸刚过来向那只懒贵狗打招呼！

确认文件已打开，且光标位于文件最后一行的结尾。按 `Ctrl+Q` 关闭应用程序。

- 读取 su(1) man 页。
注意，当用户使用 `su` 命令时假设用户是 root。如果 `su` 命令后跟着一个连字符 (`-`)，它将启动一个子 shell。如果没有连字符，则会创建一个与用户当前环境匹配的非登录子 shell。

```bash
[student@workstation ~]$ man 1 su
```

SU(1) 用户命令 SU(1)
**NAME**
su - 使用替换用户和组 ID 运行命令
**SYNOPSIS**
su [options] [-] [user [argument...]]]]

**DESCRIPTION**
允许使用替换用户和组 ID 运行命令。
在不带参数调用时，默认作为 root 运行交互式 shell。
...output omitted...
**OPTIONS**
...output omitted...
-, -1, --login
以登录 shell 启动 shell，其环境与真实登录相似
...output omitted...

（注：提供的 OCR 文本包含大量重复和碎片。我已根据提供的内容合并了逻辑流。）
