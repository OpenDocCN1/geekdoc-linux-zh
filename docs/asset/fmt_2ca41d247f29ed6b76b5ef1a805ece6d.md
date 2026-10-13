
- Linux 中的一切都可以简化为文件。

- 一如 `pwd` 和 `cd` 的命令可以帮助导航目录。

- 目录路径、`PATH` 和波浪号 (`~`) 等概念可以帮助你理解并在 shell 中使用命令。

- 基础命令允许你找到需要的文件并读取内容。这些命令包括 `ls`、`find` 和 `locate`。

- 创建和删除文件的命令包括 `touch`、`cp`、`ln`、`mv` 和 `rm`；相应的目录创建和删除命令是 `mkdir` 和 `rmdir`。

- 可以 `alias` 命令自定义命令。

https://t.me/CCNA_SECURITY

https://t.me/CCNPSECURITY

## 84 第 2 章 基础命令行技能

### 文件权限

- 标准 Linux 文件权限为读、写、执行、执行，这些可能根据用户所有者、组所有者和其他用户而异。

- 特殊权限包括 SUID、SGID 和粘滞位（sticky bits）。

- 默认用户权限基于 `umask` 的值。

- 所有权和权限可以使用 `chown`、`chgrp` 和 `chmod` 命令进行更改。

- 特殊文件属性可以使用 `lsattr` 命令列出，并通过 `chattr` 命令修改。

### 管理文本文件

- Linux 通过一系列文本配置文件进行管理。

- 文本文件可以使用 `cat`、`less`、`more`、`head` 和 `tail` 等命令作为数据流读取。

- 可以 `touch`、`cp`、`mv`、`ln` 和 `rm` 命令创建、复制、移动、链接和删除新文件。可以使用 `alias` 命令自定义命令。

- 诸如 `sort`、`grep`、`wc`、`sed` 和 `awk` 等文本过滤器支持文本流的处理。

- 理解文本编辑器是一项关键技能。RHCSA 目标的早期版本指定了 Vim 和 emacs 的使用。

### 访问文档

- 如果你需要某个命令的提示，尝试单独运行它；尝试 `-h` 和 `--help` 开关。

- 命令页面通常包含示例：`whatis` 和 `apropos` 可以搜索不同主题的 man 页面。

- 如果命令或文件有对应的 info 手册，你将在 `/usr/share/info` 目录下找到它。

- 许多软件包在 `/usr/share/doc` 目录下包含大量的文档和示例。

## 自测

以下问题将帮助你衡量对本章所介绍材料的理解。由于 Red Hat 考试中没有单选题，因此本书中也没有单选题。这些问题专门测试你对本章的理解。获得结果而非记背琐碎知识，在 Red Hat 考试中才是重要的。

### Shell

1. RHEL 9 默认 shell 的名称是什么？

2. 从 GUI 中，什么键命令可以移动到虚拟控制台 3？

### 标准命令行工具

3. 哪一个单一命令创建 `/abc/def/ghi/jkl` 系列目录？

4. 哪个符号代表家目录？

5. 什么命令列出所有以 ab 开头、包含一个额外字符、并且后面跟着数字 1、2 或 3 之一的文件？

6. 什么命令列出 `/etc` 目录下所有以 `.conf` 结尾的文件？

### 文件权限

7. 什么单一命令将本地文件 `question2.txt` 的用户改为 `professor`，组所有者改为 `assistants`？

### 管理文本文件

8. 什么命令列出 `/var/log/messages` 的最后 10 行？

9. 什么命令返回 `/var/log/messages` 中包含 Linux 的行？

10. 什么命令序列提取 `/etc/passwd` 中包含字符串 `/bin/bash` 的行并进行排序？

11. 什么命令序列返回默认 shell 为 bash 的用户？

## 86 第 2 章 基础命令行技能

### 访问文档

12. 什么命令搜索 man 页面数据库中引用 password 命令和配置文件的手册？

13. 如果假设 `abcde` 命令和文件有 man 页面（第 5 和 8 节），使用什么命令调用 man 页面？

## 实验问题

Red Hat 以电子化方式考试。因此，本章的实验可以在随书网站获取。如果你尚未在系统中设置 RHEL 9，请参考第 1 章的安装说明。每个实验的答案在自测答案之后。

## 自测答案

### Shell

1. RHEL 9 的默认 shell 是 `bash`，也称为 Bourne-again shell。

2. 从 GUI 中，移动到虚拟控制台的按键组合是 `ctrl-alt-f`。

### 标准命令行工具

3. 创建 `/abc/def/ghi/jkl` 系列目录的单一命令是 `mkdir -p /abc/def/ghi/j`。

4. 代表当前用户家目录的符号是波浪号 (`~`)。

5. 命令 `ab?[123]` 列出所有以 ab 开头、包含一个额外字符、并且后面跟着数字 1、2 或 3 之一的文件。

6. 命令 `find /etc -name *.conf` 列出 `/etc` 目录下所有以 `.conf` 结尾的文件。

### 文件权限

7. 将指定文件的所有者更改为 `professor`、组所有者更改为 `assistants` 的单个命令是：

```bash
# chown professor.assistants question2.txt
```

使用冒号 (`:`) 替换点 (`.`) 是可以接受的。

### 管理文本文件

- 8. 列出 `/var/log/messages` 前 10 行的命令是 `tail -n 10 /var/log/messages`。因为 10 是默认值，`tail /var/log/messages` 也是一个有效的解决方案。

- 9. 从 `/var/log/messages` 中返回包含 Linux 术的命令是 `grep Linux /var/log/messages`。其他变体也是接受的，例如 `cat /var/log/messages | grep Linux`。

- 10. 命令 `grep /bin/bash /etc/passwd` 提取 `/etc/passwd` 中包含字符串 `/bin/bash` 的所有行，并按字母顺序进行排序。

- 11. 回答这个问题有许多方法。一种可能的解决方案是：

```bash
# awk -F: 'print $1}' '$5' /etc/passwd | grep /bin/bash | awk 'print $1'
```

管道中的第一个 `awk` 命令从 `/etc/passwd` 的每行中提取第一字段和第七字段（用户名和 shell）。结果被传递给 `grep`，`grep` 只保留包含 `/bin/bash` 的行。最后，最后一个 `awk` 命令从输出中选择第一个字段（用户名）。结果是该管道返回了所有默认 shell 为 bash 的用户。

### 访问文档

- 12. 在帮助手册页（man pages）数据库中搜索引用密码和配置文件的手册的命令是 `whatis password`。`apropos -man` 命令更进一步，因为它通过在命令或描述中使用带有“password”文本的手册页进行搜索。

- 13. 调用第 5 节中假设的 `abcde` 命令手册的命令是 `man 5 abcde`。

## 实验答案

### 实验 1

- 1. 在你的主目录下创建 `book` 目录：

```bash
# mkdir ~/book
```

https://t.me/CCNA_SECURITY

https://t.me/CCNPSECURITY

## 88 第 2 章 基础命令行技能

确认目录存在：

```bash
$ ls -l ~
```

- 2. 切换到新目录并创建文件：

```bash
$ cd ~/book
$ touch Ch{0,1}{..9}.txt
$ rm -f Ch00.txt
```

前面的 `touch` 命令是用一次操作创建所有请求文件的最快方法。注意，该命令还创建了 `Ch00.txt` 文件，这是未要求的，因此你需要删除它。

- 3. 使用以下命令删除 `book` 目录及其所有内容：

```bash
$ rm -rf ~/book
```

# 实验 2

你可以使用以下命令创建 `rhcsa` 目录和 `lab.txt` 文件：

```bash
$ mkdir ~/rhcsa
$ cd ~/rhcsa
$ echo "Labs for the RHCSA Exam" >> lab.txt
$ date +%F >> lab.txt
```

接下来，显示 `lab.txt` 文件的内容并统计字符数：

```bash
$ cat lab.txt
$ wc -m lab.txt
```

如果你不知道 `-m` 是显示文件字符数的 `wc` 选项，请记住你可以输入 `man wc` 来查找信息。要归档 目录并完成实验中的其他任务，运行：

```bash
$ mkdir archive
$ mv lab.txt archive
$ mv ~/rhcsa /tmp/
```

## 实验 3

首先，创建一个包含 `/etc` 目录中以 "conf" 结尾的文件名的列表：

```bash
# find /etc -name "*conf" > ~/file.txt
```
