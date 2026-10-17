
## 显示文本文件的内容 141

```
- <space> 显示下 k 行文本 [当前屏幕大小]
- z 显示下 k 行文本 [当前屏幕大小]* 显示下 k 行文本 [1]*
- <return> d 或 ctrl-D* 滚动 k 行 [当前滚动大小，初始为 11]* 退出 more
- q 或 Q 或 <interrupt> 跳过 k 行文本 [1]
- s 跳过 k 个屏宽 [1]
- b 或 ctrl-B 向后跳 k 个屏宽 [1]
- = 跳到上次搜索开始的地方
  显示当前行号
- /<正则表达式> 搜索正则表达式的第 k 次出现 [1]
- n 搜索上一次正则表达式的第 k 次出现 [1]
- !<cmd> 或 !:<cmd> 在子 shell 中执行 <cmd>
```

```
- v (等待，检查上下文：为 vi)
- ctrl-L 在当前行启动 /usr/bin/vi
- :n 重绘屏幕
- :p 跳转到下一个第 k 个文件 [1]
- :f 跳转到上一个第 k 个文件 [1]
  显示当前文件名和行号
  重复上一个命令
```

--More--(71%)

正如 `more` 命令的命名是因为提供了更多功能，`less` 命令的名字也相似，因为它可以比 `more` 命令做得更多（记住“少即是多”，或 "less is more"）。与 `more` 命令类似，`less` 命令可以通过按下空格键分页、通过按下回车键逐行浏览文本文件的内容；然而，你可以使用光标键进行导航。

## 142 第 4 章 探索 Linux 文件系统

### LESS 摘要

带有 * 标记的命令前面可以加上数字 N。

括号中的注释表示给出 N 时的行为。

- h 显示此帮助。
- q :Q 退出。

### 移动

- + e 向前移动一行（或 N）。
- y k 向后移动一行（或 N）。
- f 向向前一个窗口（或 N）。
- b 向后移动一个窗口（或 N）。
- z 向前移动一个窗口并设置窗口。
- w 向后移动一个窗口并设置窗口。
- d 向向前半个窗口并设置半窗口。
- u 向后移动半个窗口并设置半窗口。
- ESC- 向右移动 8 个字符位置（或 N）。
- ESC-) 向左移动 8 个字符位置（或 N）。
- F 向前；类似于 `tail -f`

HELP 按 RETURN 获取更多信息，完成后按 q

`more` 和 `less` 命令也可以与命令的输出结合使用，如果输出大到无法容纳在终端上。要这样做，请在命令后使用元字符 `|`，随后接 `more` 或 `less` 命令，如下所示：

```
@server1 root]# cd /etc
[@server1 etc]# ls -l | more
total 3688
-rw-xr-- 1 root root 15276 Mar 22 12:20 a2ps.cfg
-rw-xr-- 1 root root 2562 Mar 22 12:20 a2ps-site.cfg
drwxr-xr-x 4 root root 4096 Jun 11 08:45 acqi
-rw-xr-- 1 root root 46 Jun 16 16:42 adtime
drwxr-xr-x 2 root root 4096 Jun 11 08:47 aep
-rw-xr-- 1 root root 668 Feb 17 00:35 aep.conf
-rw-xr-- 1 root root 703 Feb 17 00:35 aeplog.conf
drwxr-xr-x 4 root root 4096 Jun 11 08:47 alchemist
-rw-xr-- 1 root root 1419 Jan 26 10:14 aliases
-rw-r-- 1 - smmssp 12288 Jan 17 13:17 13-aliases.db
```

## 显示二进制文件的内容

| drwxr-xr-x 3 amanda disk 4096 Jun 11 10:16 amanda |

| -rw-xr-r-- 1 amanda disk 0 Mar 22 12:28 amandates |

| -rw------ 1 root root 688 Mar 4 22:34 amd.conf |

| -rw-xr-r-- 1 root root 105 Mar 4 22:34 amd.net |

| -rw-xr-r-- 1 root root 317 Feb 15 14:33 anacontrab |

| -rw-xr-r-- 1 root root 331 May 5 08:07 ant.conf |

| -rw-xr-x-- 1 root root 6200 Jun 16 16:42 asound.state |

| drwxr-xr-x 3 root root 4096 Jun 11 10:37 atalk |

| -rw-xr-r-- 1 root root 1 May 5 13:39 at.den |

| -rw-xr-r-- 1 root root 325 Apr 14 13:39 auto.master |

| -rw-xr-r-- 1 root root 581 Apr 14 13:39 auto.misc |

在前面的示例中，`ls -l` 命令的输出被重定向到 `more` 命令，它在终端上显示输出的第一页。然后你可以逐页、逐行地翻页输出内容。这种类型的重定向将在第 8 章“与 BASH Shell 交互”中进行讨论。

## 显示二进制文件的内容

在包含文本的文件上使用如 `cat`、`tac`、`head`、`tail`、`more` 和 `less` 等文件命令是非常重要的；否则，你可能会发现终端屏幕上出现随机的输出，甚至导致终端无法工作。要查看二进制文件的内容，你通常使用创建该文件的程序；但是，某些命令可以显示大多数二进制文件的内容。`strings` 命令在二进制文件中搜索文本字符并输出该文件的用途。例如，这些文本字符可能指示该二进制文件的用途。要逐页查找 `/bin/echo` 二进制执行文件内部的文本字符，可以使用以下命令：

```
[server1 root]# strings /bin/echo | more
/lib/ld-linux.so2
PTRh|
<nt7<e
[^\]
Try %s --help for more information.
Usage: %s [OPTION]... [STRING]...
Echo the STRING(s) to standard output.
-n 不输出末尾换行
-e 启用解释下面列出的斜杠转义字符，这些序列的解释在
-E 禁用这些序列的解释
STRINGS --help 显示此帮助并退出
```

--version 输出版本信息并退出

在没有 -E 的情况下，以下序列会被识别并插值：

- \NNN ASCII 码为 NNN（八进制）的字符
- \\ 反斜杠
- \a 警报（BEL）
- \b 退格格
- \c 抑制末尾换行
- \f 换页
- \n 换行

--More--

虽然此输出可能并不易读，但它确实包含了一些文本，可以引导用户找到正确的方向来了解 `/bin/echo` 命令。另一个可以安全用于二进制文件和文本文件的命令是 `od`，八进制格式（数值基 8）。使用 `od` 命令显示 `project4` 文件前五行的示例如下：

```
[root@server1]# od project4 | head -5
000000 64510 072040 062550 020054 020111 067550 062560
000020 072040 064550 020163 065044 020171 064546 062156 020163
000040 067571 062510 062567 066154 006456 006412 064212 063156
000060 071157 072564 065056 062564 074554 073440 020145 062567
000100 062562 067040 072157 060440 066142 020145 067566 066440
[root@server1]#
```

你可以使用 `od` 命令的 `-x` 选项以十六进制格式（数值基 16）显示文件。

## 在文件中搜索文本

回想 Linux 是模仿 UNIX 操作系统建模的。UNIX 系统通常被称为所有操作系统的“祖父”，因为它已经有 30 多年的历史了。UNIX 操作系统经常被提及为所有操作系统的“祖父”，因为它已经有 30 多年的历史了。Linux 许多工具都源于此：

- grep
- awk
- sed
- vi
- Emacs
- ed
- PERL
- Tcl

正如前面提到的，正则表达式（regexp）允许你以特定的方式搜索文本。

## 正则表达式

正如前面提到的，正则表达式（regexp）允许你以特定的方式搜索文本。常见的通配符分为两类：普通正则表达式和扩展正则表达式。

| 正则表达式 | 说明 | 类型 |
