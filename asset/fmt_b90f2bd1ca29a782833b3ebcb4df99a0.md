
# 查看文件结尾：`tail` 命令

就像 `head` 命令显示文本文件的开头一样，`tail` 命令可用于显示文本文件的结尾。默认情况下，`tail` 命令显示文件的最后 10 行，但它还可以接受一个数字选项，指定要在终端屏幕上显示的行数。

以下示例展示了在 `project4` 文件上使用 `tail` 命令：

```
[root@server1 ~]# tail project4
I have been reading on the history of Algonquin Park but
no where could I find a description of where the Highland
Inn was originally located on Cache lake.

If it is no trouble, could you kindly let me know such that
I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth
[root@server1 ~]# tail -2 project4
Regards,
Mackenzie Elizabeth
[root@server1 ~]#
```

# 分页显示大文件：`more` 和 `less`

虽然有些文本文件足够小，可以完全显示在终端屏幕上，但你也可能会遇到太大而无法在一屏内适配的文本文件。在这种情况下，`cat` 命令会将整个文件内容发送到终端屏幕；然而，屏幕只显示其容纳得下的文本量。要以分页方式显示大型文本文件，你需要使用 `more` 和 `less` 命令。

## `more` 命令

`more` 命令的名字源于曾经用于 UNIX 系统的 `pg` 命令。`pg` 命令在终端屏幕上分页显示文本文件，从文件开头开始；按下空格键或 `Enter` 键显示下一页，以此类推。`more` 命令比 `pg` 做的更多，因为如果按下空格键，它会显示文本文件的下一个完整页面；但如果按下 `Enter` 键，它只显示文本文件的下一行。这样，你可以逐页或逐行浏览文本文件的内容。

虚拟文件 `project5` 摘录自莎士比亚的悲剧《麦克白》，对于使用 `cat` 命令在终端屏幕上完整显示来说，它太大了。使用 `more` 命令查看其内容，结果如下：

```
[root@server1 ~]# more project5
Go bid thy mistress, when my drink is ready,
She strike upon the bell. Get thee to bed.
Is this a dagger which I see before me,
The handle toward my hand? Come, let me clutch thee.
I have thee not, and yet I see thee still.
Art thou not, fatal vision, sensible
To feeling as to sight? or art thou but
A dagger of the mind, a false creation,
Proceeding from the heat-opressed brain?
I see thee yet, in form as palpable
As this which now I draw.
Thou marshal'st me the way that I was going;
And such an instrument I was to use.

Mine eyes are made the fools o' the other senses,

Or else worth all the rest; I see thee still,

And on thy blade and dudgeon gouts of blood,

Which was not so before. There's no such thing;

It is the bloody business which informs

Thus to mine eyes. Now o'er the halfworld

Nature seems dead, and wicked dreams abuse

The curtain'd sleep; witchcraft celebrates

Pale Hecate's offerings, and wither'd murder,

Alarum'd by his sentinel, the wolf,

--More-- (71%)
```

如前文输出所示，`more` 命令显示第一页时，并不会返回 shell 提示符。相反，`more` 命令在终端屏幕底部显示一个提示符，指示屏幕上显示的文件占总文件大小的百分比。在前面的示例中，`project5` 文件的 71% 被显示。在此提示符下，你可以按空格键前进一整页，或者按 `Enter` 键前进到下一行。此外，`more` 命令允许在此提示符下与其他用户交互。在提示符处按下 `h` 字符会显示帮助屏幕，如下所示，而按下 `q` 字符则会完全退出 `more` 命令，而不会查看文件的剩余部分。

### `more` 命令快捷键参考

大多数命令可选地由整数参数 `k` 前导。括号内为默认值。星号（`*`）表示参数成为新的默认值。

- `<space>` 显示接下来 `k` 行文本 [当前屏幕大小]
- `z` 显示接下来 `k` 行文本 [当前屏幕大小]
- `<return>` 显示接下来 `k` 行文本 [1]
- `d` 或 `Ctrl-D` 滚动 `k` 行 [当前滚动大小，初始为 11]
- `q` 或 `Q` 或 `<interrupt>` 退出 `more`
- `s` 跳过 `k` 行文本 [1]
- `f` 跳过 `k` 屏文本 [1]
- `b` 或 `Ctrl-B` 向后跳过 `k` 屏文本 [1]
- `/` 转到上一次搜索开始的位置
- `=` 显示当前行号
- `/regular expression>` 搜索正则表达式的第 `k` 个出现位置 [1]
- `n` 搜索最后一个正则表达式的第 `k` 个出现位置 [1]
- `!<cmd>` 或 `:!<cmd>` 在子 shell 中执行 `<cmd>`
- `v` 在当前行启动 `/usr/bin/vi`
- `Ctrl-L` 重绘屏幕
- `:n` 转到下一个文件的第 `k` 个文件 [1]
- `:p` 转到上一个文件的第 `k` 个文件 [1]
- `:f` 显示当前文件名和行号
- `.` 重复上一个命令

`--More-- (71%)`

## `less` 命令

正如 `more` 命令因允许更多用户功能而得名，`less` 命令因比 `more` 命令做的更多而得名（记住“less is more”，或多或少）。与 `more` 命令类似，`less` 命令可以通过按空格键逐页浏览文本文件内容，通过按 `Enter` 键逐行浏览；然而，你还可以使用键盘上的光标键向上和向下滚动文件内容。使用 `less` 命令查看 `project5` 文件时的输出如下：

```
[root@server1 ~]# less project5
Go bid thy mistress, when my drink is ready,
She strike upon the bell. Get thee to bed.
Is this a dagger which I see before me,
The handle toward my hand? Come, let me clutch thee.
I have thee not, and yet I see thee still.
Art thou not, fatal vision, sensible
To feeling as to sight? or art thou but
A dagger of the mind, a false creation,
Proceeding from the heat-opressed brain?
I see thee yet, in form as palpable
As this which now I draw.
Thou marshall'st me the way that I was going;
And such an instrument I was to use.
Mine eyes are made the fools o’ the other senses,
Or else worth all the rest; I see thee still,
And on thy blade and dudgeon gouts of blood,
Which was not so before. There’s no such thing:
It is the bloody business which informs
Thus to mine eyes. Now o’er the one half world
Nature seems dead, and wicked dreams abuse
The curtain’d sleep; witchcraft celebrates
Pale Hecate’s off’rings, and wither’d murder,
Alarum’d by his sentinel, the wolf,
Whose howl’s his watch, thus with his stealthy pace.
project5
```

与 `more` 命令类似，`less` 命令使用 `:` 字符或正在查看的文件名（在我们的示例中为 `project5`）在文件底部显示提示符，但 `less` 命令包含更多的键盘快捷键，用于在文件中搜索文本。在提示符处，你可以按 `h` 键获取帮助屏幕，或按 `q` 键退出。`less` 命令的第一个帮助屏幕如下所示：

```
SUMMARY OF LESS COMMANDS
Commands marked with * may be preceded by a number, N.
Notes in parentheses indicate the behavior if N is given.
A key preceded by a caret indicates the Ctrl key; thus ^k is ctrl-K.
 h H Display this help.
 q :q Q :Q ZZ Exit.
```

### 移动

- `e` `^E` `j` `^N` `CR` `*` 向前一行（或 `N` 行）
- `y` `^Y` `k` `^K` `^P` `*` 向后退一行（或 `N` 行）
- `f` `^F` `^V` `SPACE` `*` 向前一屏（或 `N` 行）
- `b` `^B` `ESC-[` `*` 向后退一屏（或 `N` 行）
- `z` `*` 向前一屏（并将窗口设置为 `N`）
- `w` `*` 向后退一屏（并将窗口设置为 `N`）
- `ESC-SPACE` `*` 向前一屏，但在文件末尾不停止
- `d` `^D` `*` 向前半屏（并将半屏设置为 `N`）
- `u` `^U` `*` 向后退半屏（并将半屏设置为 `N`）
- `ESC-(` `RightArrow` `*` 向左 `8` 个字符位置（或 `N` 个位置）
- `ESC-)` `LeftArrow` `*` 向右 `8` 个字符位置（或 `N` 个位置）
- `F` `*` 永久向前；类似于 `tail -f`

`HELP -- Press RETURN for more, or q when done`

`more` 和 `less` 命令也可以与命令的输出配合使用，如果该输出太大而无法适配终端屏幕。为此，只需在命令后使用 `|` 元字符，然后跟着 `more` 或 `less` 命令，如下所示：

```
[root@server1 ~]# cd /etc
[root@server1 etc]# ls -1 | more
total 3680
-rw-r-r-- 1 root  root  15276 Mar 22 12:20 a2ps.cfg
-rw-r-r-- 1 root  root  2562 Mar 22 12:20 a2ps-site.cfg
drwxr-xr-x 4 root  root  4096 Jun 11 08:45 acpi
-rw-r-r-- 1 root  root  46 Jun 16 16:42 adjtime
drwxr-xr-x 2 root  root  4096 Jun 11 08:47 aep
-rw-r-r-- 1 root  root  688 Feb 17 00:35 aep.conf
-rw-r-r-- 1 root  root  703 Feb 17 00:35 aeplog.conf
drwxr-xr-x 4 root  root  4096 Jun 11 08:47 alchemist
-rw-r-r-- 1 root  root  1419 Jan 26 10:14 aliases
-rw-r-r-- 1 root  smmsp 12288 Jun 17 13:17 aliases.db
drwxr-xr-x 2 root  root  4096 Jun 11 11:11 alternatives
drwxr-xr-x 3 amanda disk 4096 Jun 11 10:16 amanda
-rw-r-r-- 1 amanda disk  0 Mar 22 12:28 amandates
-rw------- 1 root  root  688 Mar 4 22:28 amd.conf
-rw-r-r--- 1 root  root  105 Mar 4 22:34 amd.net
-rw-r-r-- 1 root  root  317 Feb 15 14:33 anacrontab
-rw-r-r-- 1 root  root  331 May 5 08:07 ant.conf
-rw-r-r-- 1 root  root  6200 Jun 16 16:42 aouned.state
drwxr-xr-x 3 root  root  4096 Jun 11 10:37 atalk
-rw----- 1 root  root  1 May 5 13:39 at.deny
-rw-r-r-- 1 root  root  325 Apr 14 13:39 auto.master
-rw-r-r-- 1 root  root  581 Apr 14 13:39 auto.misc
--More--
```

在前面的示例中，`ls -l` 命令的输出被重定向到 `more` 命令，该命令在终端上显示输出的第一页。然后你可以前进通过分页或逐行输出的方式。这种重定向方法在第 7 章中进行了讨论。

## 显示二进制文件的内容

仅对包含文本的文件使用文本文件命令（例如 `cat`、`tac`、`head`、`tail`、`more` 和 `less`）非常重要；否则，你可能会在终端屏幕上看到随机输出，甚至导致终端功能失效。要查看二进制文件的内容，通常使用创建该文件的程序。但是，某些命令可以安全地显示大多数二进制文件的内容。

`strings` 命令在二进制文件中搜索文本字符并将其输出到屏幕上。在许多情况下，这些文本字符可能表明该二进制文件的用途。例如，要分页查找 `/bin/echo` 二进制可执行程序内部的文本字符，可以使用以下命令：

```bash
[root@server1 ~]# strings /bin/echo | more
/lib/ld-linux.so.2
PTRH
<t<t<e
[\*_
[\*_
Try '\$s --help' for more information.
Usage: \$s [OPTION]... [STRING]...
Echo the STRING(s) to standard output.
  -n        do not output the trailing newline
  -e        enable interpretation of the backslash-
            escaped characters listed below
  -E        disable interpretation of those sequences in STRINGS
  --help    display this help and exit
  --version output version information and exit
Without -E, the following sequences are recognized and interpolated:
  \\NNN  the character whose ASCII code is NNN (octal)
  \\\      backslash
  \\a      alert (BEL)
  \\b      backspace
  \\c      suppress trailing newline
  \\f      form feed
  \\n      new line
--More--
```

虽然此输出可能不容易阅读，但它确实包含了一些文本片段，可以引导用户朝正确方向查找有关 `/bin/echo` 命令的更多信息。另一个可以安全用于二进制文件和文本文件的命令是 `od` 命令，它以八进制格式（数字基数 8 格式）显示文件内容。以下示例展示了使用 `od` 命令显示文件 `project4` 的前五行：

```bash
[root@server1 ~]# od project4 | head -5
0000000 064510 072040 062550 062562 020054 020111 067550 062560
0000020 072040 064550 020163 060544 020171 064546 062156 020163
0000040 067571 020165 062567 066154 006456 006412 052412 063156
0000060 071157 072564 060556 062564 074554 073440 020145 062567
0000100 062562 067040 072157 060440 066142 020145 067564 066440
[root@server1 ~]#
```

![](img/c27875544958897d817484d558c208c8_132_0.png)
