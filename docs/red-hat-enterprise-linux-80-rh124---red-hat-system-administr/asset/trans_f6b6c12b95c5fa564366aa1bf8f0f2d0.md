

exec gzip -cd "$@"

+   8. 重复上一个命令，使用 -n 20 选项显示文件的最后 20 行。使用命令行编辑以最少的按键次数完成此操作。

向上方向键（UpArrow）显示上一个命令。Ctrl+A 将光标移到行首。Ctrl+右方向键跳到到下一个单词，然后添加 -n 20 选项并按回车执行命令。

```
student@workstation ~$ tail -n 20 zcat
-l, -list 列出压缩文件内容
-q, -quiet 抑制警告
-r, -recursive 对目录进行操作
-S, -suffix=SUF 在压缩文件上使用 SUF
--synchronous 同步输出（系统崩溃时更安全，但速度较慢）
-t, -test 测试压缩文件的完整性
--verbose 详细模式
--help 显示此帮助信息并退出
--version 显示版本信息并退出
```

在没有指定文件（FILE）或当 FILE 为 - 时，从标准输入读取。

将日志报告至 <bug-gzip@gnu.org>。

```
case $1 in
  --help) printf "%%s\n" "Usage" || exit;
  --version) printf "%%s\n" "Version" || exit;
esac
```

```
exec gzip -cd "$@"
```

+   9. 使用 shell 历史记录再次运行 date +r 命令。
使用 history 命令显示之前的命令列表并识别要执行的特定日期。使用 !number 运行命令，其中 number 是从 history 命令输出使用的使用的编号。
注意，你的 shell 历史记录可能与以下示例不同。请根据你自己的 history 命令的输出确定要使用的命令编号。

```
student@workstation ~]$ history
date
date +r
file zcat
wc zcat
head zcat
tail zcat
tail -n 20 zcat
history
[student@workstation ~]$ ! 2
date +r
```

# 评估

在工作站上运行 lab cli-review grade 脚本以确认此练习是否成功。

```
[student@workstation ~]$ lab cli-review grade
```

# 完成

在工作站上运行 lab cli-review finish 脚本以完成实验。

```
[student@workstation ~]$ lab cli-review finish
```

实验结束。

# 总结

在本章中，你学习了：

-   - Bash shell 是一个命令解释器，提示交互式用户指定 Linux 命令。
- 许多命令都有 ---help 选项，可以显示用法信息或屏幕。
-   使用工作空间（workspaces）更容易组织多个应用程序窗口。
-   位于顶部栏左角的活动（Activities）按钮提供了概述模式，帮助用户组织窗口并启动应用程序。
-   file 命令扫描文件的开头并显示其类型。
-   head 和 tail 命令分别显示文件的开头和结尾。
-   在将文件名作为命令参数输入时，可以使用 Tab 补全来完成文件名。

# 第 3 章

# 从命令行管理文件

# 目标

在 Bash shell 中工作时复制、移动、创建、删除和组织文件。

# 学习目标

+   - 描述 Linux 如何组织文件，以及文件系统层次结构中各种目录的用途。
-   指定文件相对于当前工作目录和绝对位置的位置，确定并更改你的工作目录，并列出目录内容。
-   创建、复制、移动和删除文件及目录。
-   使用硬链接（hard links）和符号链接（或“软链接”）让多个文件名引用同一个文件。
-   使用 Bash shell 的模式匹配功能高效运行影响许多文件的命令。

# 章节

+   - 描述 Linux 文件系统层次结构概念（及测验）
-   按名称指定文件（及测验）
-   使用命令行工具管理文件（及引导性练习）
-   建立文件建立链接（及引导性练习）
-   使用 Shell 扩展匹配文件名（及测验）

# 实验

从命令行管理文件

![](img/59afb92e10b67a9cecc358a2c65e93b5_66_0.png)

# 描述 Linux 文件系统层次结构概念

# 学习目标

完成本节后，你应该能够描述 Linux 如何组织文件，以及文件系统层次结构中各种目录的用途。

# 文件系统层次结构

Linux 系统上的所有文件都存储在文件系统中，文件系统被组织成单一的倒立目录树，称为文件系统层次结构。这棵树之所以倒立，是因为树的根被认为位于层次结构的*顶部*，而目录和子目录的分支延伸到根的*下方*。

![](img/59afb92e10b67a9cecc358a2c65e93b5_67_0.png)

**图 3.1：Red Hat Enterprise Linux 8 中重要的文件系统目录**

/ 目录是文件系统层次结构顶部的根目录。/ 字符也用作文件名中的*目录分隔符*。例如，如果 **etc** 是 / 目录的子目录，你可以引用该目录为 /etc。同样，如果 /etc 目录包含一个名为 **issue** 的文件，你可以将该文件引用为 /etc/issue。

/ 的子目录用于标准化的用途，按类型和目的组织文件。这使得更容易找到文件。例如，在根目录中，子目录 /boot 用于存储启动系统的文件。

> 注意
/ 的子目录用于按类型和目的组织文件的标准化。这使得更容易找到文件。
* 静态内容在重启后保持不变。
* 动态或变量内容可能会被修改。
* 持久性内容在重启后保留。
* 运行时内容自上次启动以来产生。
/ 目录的内容包括：

# 重要的 Red Hat Linux 目录

下表列出了系统中重要目录的名称和用途。

| 位置 | 用途 |
| --- | --- |
| /usr | 用户命令。<br>* /sbin: 系统管理命令。<br>* /local: 本地自定义软件。 |
| /etc | 系统特定的配置文件。 |
| /var | 系统动态数据，如数据库、日志文件等。 |
| /run | 自上次启动以来的运行时数据。 |
| /home | 普通用户存储个人数据的目录。 |
| /root | 管理员的主目录。 |
| /tmp | 临时文件的写入空间。超过30天未访问、更改或修改的文件会被删除。 |
| /boot | 用于启动系统的文件。 |
| /dev | 用于访问硬件的特殊文件。 |

# 重要

在 Red Hat Enterprise 7 及更高版本中，/ 中的目录与 /usr 中的对应目录内容相同：

- /bin 和 /usr/bin
- /sbin 和 /usr/sbin
- /lib 和 /usr/lib
- /lib64 和 /usr/lib4

在旧版本的 Red Hat 中，这些是包含不同文件的独立目录。

在 Red Hat Enterprise 7 及更高版本中，/ 中的目录是指向 /usr 的符号链接。

# 参考

hier(7) 手页

来自 Fedora 17 的 UsMove
https://fedoraproject.org/wiki/Features/UsMove

# 测验

# 描述 Linux 文件系统层次概念

选择以下问题的正确答案：

+   1. 哪个目录包含持久的、系统特定的配置数据？
   a. /etc
   b. /root
   c. /run
   d. /usr

+   2. 哪个目录是文件系统层次结构的顶部？
   a. /etc
   b. /
   c. /home/root
   d. /root

+   3. 哪个目录包含用户主目录？
   a. /
   b. /home
   c. /root
   d. /user

+   4. 哪个目录包含临时文件？
   a. /tmp
   b. /trash
   c. /run
   d. /var

+   5. 哪个目录包含动态数据，如数据库和网站？
   a. /etc
   b. /run
   c. /usr
   d. /var

+   6. 哪个目录是管理员用户的主目录？
   a. /etc
   b. /
   c. /home/root
   d. /root

