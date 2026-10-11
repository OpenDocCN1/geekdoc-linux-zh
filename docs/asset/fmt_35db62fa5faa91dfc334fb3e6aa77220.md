
```
[root@localhost root]# pwd
/root
[root@localhost root]# ls /home/bob
assignment1 file letter letter2 project1
[root@localhost root]# _
```

> 运行 `ls` 命令时，你会发现不同类型的文件通常被表示为不同的颜色，表示某些类型文件的特定颜色可能随终端和发行版的不同而异。因此，不要使用颜色来判断文件类型。

![](img/6148a12ef656b46c092b21c2e023d928_149_1.png)

> `Windows` 使用 `cmd` 来列出文件和目录；为了方便 `Windows` 用户学习 `Linux`，`Linux` 中有一个 `dir` 命令，它只是 `ls` 命令的指针或快捷方式。

![](img/6148a12ef656b46c092b21c2e023d928_149_2.png)

回想上一章，你可以使用开关（switches）来改变命令的行为。要文件列表及其类型，请在命令中使用 `-F` 开关：

```
[root@localhost root]# pwd
/root
[root@localhost root]# ls -F
current@ myprogram* project project12 project2 project4
Desktop/ myscript* project1 project13 project3 project5
[root@localhost root]# _
```

## 查看文件和目录

`ls -F` 命令在每个文件名末尾附加一个特殊字符以指示文件类型。在上面的输出中，注意文件名 `current`、`Desktop`、`myprogram` 和 `myscript` 名字后面都附加了特殊字符。`@` 符号表示链接文件，`*` 符号表示执行文件，`/` 表示子目录。还有两个特殊字符在上面未显示：`=` 表示套接字（socket），`|` 表示管道文件（piped file）。所有其他类型都没有附加特殊字符，可能是文本文件、二进制数据或特殊设备文件。

目录以大写字母开头是一种常见的惯例，如上面输出中 `Desktop` 目录中的 `D`。这确保了目录在执行 `ls` 命令时列在开头，并让你在运行没有指定文件类型的 `ls` 命令时，能够快速判断哪些名称指的是目录。

![](img/6148a12ef656b46c092b21c2e023d928_150_0.png)

`ls -F` 命令是一种以易读格式获取文件类型信息的快速方法，但有时你可能需要关于每个文件的更详细信息。`ls -l` 命令可以为特定目录中的每个文件提供长列表：

```
[root@localhost root]# pwd
/root
[root@localhost root]# ls -l
total 548
drwxr-xr-x 1 root 9 Apr 09:56 current -> project12
-------- 1 root 4096 Mar 29 10:01 Desktop
-rwxr-xr-x 1 root 51964 Apr 09:59 myscript
-rwxr-xr-x 1 root 20 Apr 09:58 project
-rw-r--r 1 root 71 Apr 09:58 project1
-rw-r--r 1 root 71 Apr 09:59 project2
-rw-r--r 1 root 71 Apr 09:59 project3
-rw-r--r 1 root 0 Apr 09:59 project4
-rw-r--r 1 root 71 Apr 09:59 project5
-rw-r--r 1 root 90 Apr 10:01 project6
-rw-r--r 1 root 99 Apr 10:01 project7
-rw-r--r 1 root 108 Apr 10:01 project8
[root@localhost root]#
```

上述示例列出的每个文件从左到右包含八部分信息：

1. 文件类型
   - `d` 字符表示目录
   - `l` 字符表示符号链接文件（第5章讨论）
2. 权限
3. 大小
4. 所有者
5. 组
6. 修改时间
7. 名称
8. 链接

# 第 4 章 探索 Linux 文件系统

如前所述，`.` 字符表示当前工作目录，而 `..` 字符表示相对于你当前目录树的父目录。当使用 `ls -a` 命令时，这些点中的每一个都被视为一个特殊的（虚拟的）文件，因为它们都以点开头。

你还可以在命令行中对大多数命令中同时指定多个选项，并获得所有选项的组合功能。例如，要查看所有隐藏文件及其类型，可以使用：

```
[root@localhost ~]# ls -aF
./gimp-1.2/       project
../gnome/         project1
.bash_history  gnome-desktop/ project2
.bash_logout   gnome_private/ project3
.bash_profile  gtkrc           project2
.bashrc        ICEAuthority project3
.cshr          kde/            project4
current@       mcp/            project5
.DOCOPserver_localhost.localdomain@ mcp-random-seed .sane/
Desktop/        .mcprc .sawfish/
.first_start_kdemozilla/.tcshrc
.galeon        myprogram*     Xauthority
.gconf         myscript       Xresources
.gconfd        .nautilus/      xsession-
errors
[root@localhost root]# _
```

上述 `ls` 命令的选项（`ls -l`、`-F`、`ls -a`）是在 `Linux` 目录树中导航时最常用的选项；然而，`ls` 命令还有许多可用选项可以更改文件系统上文件的列出方式。这些选项及其描述见表 4-2。

## 表 4-2 ls 命令的常用选项

| 选项 | 描述 |
| :--- | :--- |
| `-a` | 列出所有文件名 |
| `--all` | |
| `-A` | 列出大多数文件名（排除 `.` 和 `..` 特殊文件） |
| `--almost-all` | |
| `-C` | 以列格式列出文件名 |
| `--color=n` | 不带颜色地列出文件名 |
| `-f` | 不经排序列出所有文件名 |
| `-F` | 按文件类型分类列出文件名 |
| `--classify` | |
| `--full-time` | 以长格式列出文件名并显示完整的修改时间 |
| `-l` | 以长格式列出文件名 |

## 查看文件和目录

表 4-2 ls 命令的常用选项（续）

| 选项 | 描述 |
| :--- | :--- |
| `-lh` | 以长格式列出文件名，并带有人类可读（易读）的文件大小 |
| `-l --human-readable` | |
| `-l -G` | 以长格式列出文件名，但省略用户组信息 |
| `-l --no-group` | |
| `-0` | |
| `-r` | 反向排序列出文件名 |
| `--reverse` | 列出指定目录及其所有子目录中的文件名 |
| `--recursive` | 列出文件名及其以千字节 (K) 为单位的大小 |
| `-s` | 按文件大小排序列出文件名 |
| `-S` | |
| `-t` | 按修改时间排序列出文件名 |
| `-U` | 不排序出文件名 |
| `-x` | 以行而非列列出文件名 |

## 通配符元字符

在上一节中，你看到 `*` 元字符被用于指示（或“匹配”）当前目录下的所有文件，就像纸牌游戏中的通配符匹配某些卡牌一样。因此，`*` 元字符被称为通配符元字符。通配符元字符可以简化命令行中指定多个文件名的命令。这些通配符元字符由 `shell` 解释，并用于大多数常用的 `Linux` 命令，包括我们已经提到的几个（`ls`、`file` 和 `cd`）。这些元字符包含文件名的某些部分或文件名本身。通配符元字符的列表可以参阅表 4-3 及其描述。

## 表 4-3 通配符元字符

| 元字符 | 描述 |
| :--- | :--- |
| `*` | 匹配文件名中的 0 个或多个字符 |
| `?` | 匹配文件名中的 1 个字符 |
| `[aegh]` | 匹配文件名中的 1 个字符——只要该字符是 `a`、`e`、`g` 或 `h` 之一 |
| `[a-e]` | 匹配文件名中的 1 个字符——只要该字符是 `a`、`b`、`c`、`d` 或 `e` 之一 |
| `[!a-e]` | 匹配文件名中的 1 个字符——只要该字符不是 `a`、`b`、`c`、`d` 或 `e` |
