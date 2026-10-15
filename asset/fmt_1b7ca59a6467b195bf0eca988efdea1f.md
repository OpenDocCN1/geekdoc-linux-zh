
- 不是任何语言任何词典中的单词或姓名
- 大写和小写字母、数字和符号的组合
- 与你的用户名不相似
- 与你最近使用过的密码不相同或不相似
- 不是你的电话号码、出生日期、孩子的出生日期、周年纪念日（即使你能记住）、母亲的娘家姓，或任何可能与你相关联的东西

# Listing Directories and Files with ls

你的 Unix 系统由存储各种信息的目录和文件组成，包括设置信息、配置设置、程序和选项，以及其他文件和目录。你可以把你的 Unix 系统想象成一棵树（实际上是树根），子目录从更高级别的目录中延伸出来。如图 1.6 所示，所有这些文件和目录都位于根目录内，根目录包含系统中的所有内容。

使用 `ls` 命令，你可以准确地了解 Unix 系统中的内容，从而了解你可以使用的资源。你可以列出你当前所在的目录或你指定的目录中的文件和目录。

## To list the files and directories of the directory you're in:

- `ls`

在 shell 提示符下，输入 `ls` 以列出当前目录中的文件和目录，在本例中是我们的主目录（代码清单 1.2）。

Figure 1.6 All files and directories are nested within the root directory, which serves to contain everything in the system.

```
[jdoe@frazZ jdoe]$ ls
limerick mail/ Project/ public_html/
* testfile testlink@ tmp/
[jdoe@frazZ jdoe]$
```

Code Listing 1.2 Use `ls` by itself to list the files and directories of the directory you're in.

## To list the files and directories of a specified directory:

- `ls /bin`

在这里，你输入 `ls` 命令加上目录名。如代码清单 1.3 所示，此命令列出 `/bin` 目录中的文件和目录，在其中你会找到系统命令和程序。

### Tips

- 你可以随时在任何地方通过输入 `ls /` 来列出根目录中的文件和目录。
- 想不起来那个讨厌的文件名？只需使用 `ls` 来帮助你回忆。或者，参考第 2 章中的 Finding Forgotten Files with `find`，它也可以帮助你记住文件名。
- 还有许多其他 `ls` 选项可用于控制你看到的文件信息的数量以及它们在屏幕上出现的格式。有关详细信息，请参阅第 2 章的 Listing Files and Directories with `ls` (More Goodies) 部分。

```
[jdoe@frazZ jdoe]$ ls /bin
arch*    domainname@  ipcalc*    open*    tar*
awk@     echo*        ipv6c     eys*     red@     unlink*
chmod*   fbresolution* login*    rm*      usleep*
chown*   fgrep@       ls*       rmdir*   vi@
consolechars* find*   lsb_release* rpm*     vim@
cp*      gawk*        mail*     rvi@     vim@
cpio*    gawk-3.1.6@  mkdir*    rview@
date*    gtar@        more*     sleep*   zcat*
dd*      gunzip*      mount*    sort*    zsh*
df*      gzip*        mv*       stat* 
dmesg*   hostname*    netstat*  stty*
dnsdomainname@ id@      nice*     su*
doexec*  gawk*        nisdomainname@ sync*
[jdoe@frazZ jdoe]$
```

Code Listing 1.3 Use `ls` with the name of a directory to list the contents of that directory (`/bin`, in this case).

```
[jdoe@frazzi jdoe]$ cd /
[jdoe@frazzi /]$ cd
[jdoe@frazzi jdoe]$ cd ~/home/jdoe/Project/
[jdoe@frazzi Project]$ cd /etc
[jdoe@frazzi etc]$ cd /home/jdoe/
[jdoe@frazzi jdoe]$ cd /home/jdoe/mail/
[jdoe@frazzi mail]$ cd ..
[jdoe@frazzi jdoe]$
```

代码清单 1.4 使用 `cd`，你可以更改目录并在系统中移动。注意本代码清单中的提示显示了当前目录的名称，这非常方便。

# 使用 cd 更改目录

要探索 Unix 及其功能，你需要在目录之间移动。你使用 `cd` 命令来实现这一点，它会将你从当前所在的目录带到你指定的目录。代码清单 1.4 说明了如何使用 `cd` 更改目录。

## 更改目录的方法：

- 1. `cd Projects`

  要移动到特定目录，输入 `cd` 加上目录名称。在此示例中，我们在目录树中向下移动到名为 `Projects` 的子目录。 （请参阅“向上和向下移动”侧边栏，了解 Unix 术语中“向上”和“向下”的含义。）

- 2. `cd ..`

  输入 `cd ..` 可向上移动一级目录树。

- 3. `cd /etc`

  这里，`/etc` 告诉系统查找位于系统根目录的 `etc` 目录。

### 向上和向下移动

在本书中，我们将讨论在 Unix 文件系统中“向上”和“向下”移动。向上移动意味着进入包含当前目录的目录——也就是说，更接近根目录。向下移动意味着进入由当前目录包含的子目录——也就是说，远离根目录。

### ✓ 提示

- 如果你不记得要更改到的目录名称，可以使用 `ls` 列出当前目录中的目录和文件，然后按上述方式使用 `cd`。 有关更多信息，请参阅上一节 *使用 ls 列出目录和文件*。
- 你可以从 Unix 系统中的任何位置返回到主目录，只需输入 `cd` 而不指定目录即可。
- 你通常可以使用波浪号 (`~`) 作为主目录的便捷快捷方式。 例如，如果你想更改到主目录中 `Projects` 目录下的 `Urgent` 目录，你可以使用类似 `cd /home/users/y/yourid/Projects/Urgent` 的命令，或者直接使用快捷方式 `cd ~/Projects/Urgent`。
- 请记住，你的主目录与系统根目录不同。 你可以把你的主目录想象成“我可以称之为自己的 Unix 系统的很小一部分”。 使用 Unix 系统的每个人都有自己的小个人区域。
- 当前目录始终用 `.` 表示，而下一个更高一级的目录（包含当前目录的目录）用 `..` 表示。 这就是为什么你使用 `cd ..` 来向上移动一个目录。 在第 10 章中，你将看到使用 `.` 指定运行脚本或程序时的当前目录的具体用法。
- 请访问第 2 章，了解有关目录和文件的更多信息。

```
[jdoe@frazzi jdoe]$ pwd
/home/jdoe
[jdoe@frazzi jdoe]$ ls ; pwd
codelisting1.2  codelisting1.4  mail/
public_html/  testlink#
codelisting1.3  limerick  Project/  testfile
tmp/
/home/jdoe
[jdoe@frazzi jdoe]$ cd
[jdoe@frazzi jdoe]$ cd /
[jdoe@frazzi /]$ pwd
/
[jdoe@frazzi /]$
```

代码清单 1.5 `pwd` 显示当前目录的名称，如果你一直在探索系统，这特别方便。 通过组合命令，你可以同时请求目录的名称和内容。

# 使用 pwd 找到自己的位置

当你开始使用 Unix 并在目录和文件中移动时，你可能会有点迷路——也就是说，忘记你所在的目录或子目录。 你可以使用 `pwd` 命令来提醒你所在的位置，如代码清单 1.5 所示。

你可以只请求目录名称，也可以更灵活地请求目录的名称及其内容，这要归功于 `ls`。

## 查找当前目录名称的方法：

- `pwd`

此命令显示你当前所在的目录的路径和名称。 路径列出了当前目录“上方”的每个目录，让你全面了解你相对于系统根目录的位置。

## 查找当前目录名称及其内容的方法：

- `ls ; pwd`
