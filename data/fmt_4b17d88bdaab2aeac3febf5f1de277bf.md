
当你使用重定向输入符号 `<` 并在后跟一个文件名时，你是在告诉 shell 你想将一个文件作为命令的输入。

现在，使用你已经创建的文件来演示这个概念。只需输入以下内容：

```
[carlotta@toluca carlotta]$ cat < sneakers.txt
```

因为你使用了小于符号 (`<`) 将 `cat` 命令与文件分隔

## 管道与分页器

管道是 `|` 符号，它位于键盘上与反斜杠相同的按键上。在 Linux 中，管道将一个命令的输出重定向到另一个命令的输入。考虑一下本章之前讨论过的 `ls` 命令。使用 `|` 有许多可用选项，但如果目录的内容滚动得太快，导致你无法查看怎么办？

## 第 9 章 ♦ 命令行威力：Shell 提示符基础 167

例如，查看 `/etc` 目录的内容：

```
$carlotta@toluca carlotta$ ls -al /etc
```

在输出离开屏幕之前，你如何更仔细地查看输出呢？

### 通过 less 管道输出

使长输出易于浏览的一种方法是通过名为 `less` 的工具进行管道输出。`less` 是一个分页工具，之所以这样命名是因为允许你每次查看一页（或一个屏幕）信息：

```
$carlotta@toluca carlotta$ ls -al /etc | less
```

现在你可以一次一个屏幕地查看 `/etc` 的内容。要向前移动一屏幕，按空格键或 Page Down 键；要向后移动一屏幕，按 `b` 或 Page Up 键。你可以使用箭头键逐行上下导航文件。当你完成操作并想退出 `less` 时，按 `q`。

为了更仔细地阅读启动信息，在提示符处，输入 `dmesg | less`。你将能够一次一个屏幕地阅读文件。使用箭头键导航文件。

![](img/67d9607982940021da1fe4247b9b224c_188_0.png)

### 在管道中使用 grep

这是你通过命令和管道可以执行的另一个技巧。你可以使用 `grep` 命令在 `sneakers.txt` 文件中搜索单词 `coffee`，它只会输出它找到 `coffee` 单词的行：

```
$carlotta@toluca carlotta$ grep coffee sneakers.txt
bring the coffee home
make some coffee
bring the coffee home
make some coffee
```

现在将输出通过打印机 `lpr` 将信息发送到打印机（显然，如果你安装并配置了默认打印机，这对你来说有效）。输入以下内容：

```
grep coffee sneakers.txt | lpr
```

这会将 `sneakers.txt` 文件中提到单词 `coffee` 的每一行发送到打印机（在本章后面的“grep 命令”部分更多关于 grep 的信息）。

### more 命令

`more` 命令是 `less` 命令的一个原始且基本上过时的版本，但它值得提到，因为你可能会看到或听到有人提到这个命令。`more` 和 `less` 的区别在于 `less` 允许你使用箭头键向前后移动，而人们通常只使用空格键向前翻页输出。使用 `less` 时，你可以按 `q` 退出 `more`。

使用 `ls` 和 `more` 列出 `/etc` 目录的内容（见图 9-7）。

```
$carlotta@toluca carlotta$ ls -al /etc | more
```

## 168 Fedora 官方伴侣

```
File Edit View Terminal Go Help | more
carlotta@toluca carlotta]$ ls -l /etc
total 2000
-rwxr root root 15228 Jun 05 18 a2ps.cfg
-rw root root 2562 Jun 05 18 a2ps-site.cfg
-rw root root 44 Aug 24 16:10 adwm
-rwx root root 4096 Jul 24 21:42 alchemist
-rw root root 217 Jul 23 17:35 aliases
-rw- root root 2194 Jul 24 21:53 be-activation
-rw- root root 12288 Jan 25 08:41 aliases.db
-rwx root root 4096 Jul 24 20:43 alternatives
-rw root root 3167 Jul 10 13:54 amessage
-rw root root 512 Jun 07 02:45 at.dump
-rw root root 575 Jun 09 17:55 auto.misc
-rw root root 1487 Aug 29 20:02 backup
-rw root root 2176 Jul 23 23:38 blind.tab
-rwx root root 4096 Jul 24 21:46 de-activation
-rw root root 1000 Jun 27 07:55 drecord.conf
-rw- root root 1767 Jun 16 16:33 cookies.txt
-rw root root 4096 Jul 15 15:58 CODBA
-rw root root 4096 Jul 23 23:38 cron.d
-rw root root 4096 Jul 24 21:57 cron.daily
-rw root root 4096 Feb 07 20:03 cron.hourly
-rw root root 4096 Jul 24 21:57 cron.daily
```

图 9-7：通过 less 管道输出

假设你正在寻找一个之前使用过的、类似于 `cat something` 的命令。同时，假设你最近用过这个命令，并且你认为它可能在你的历史文件中。在 shell 提示符下，输入以下内容：

```bash
[carlotta@toluca carlotta]$ history | grep sneak
```

### Tab 键补全 (Tab Completion)

另一个节省时间的工具被称为命令补全。如果你输入文件、命令或路径的一部分，然后按 Tab 键，bash 就会为你展示该文件/路径的剩余部分，或者发出“哔”声（如果你的系统开启了提示音）。如果你听到了“哔”声，再次按 Tab 键即可获取与目前输入匹配的文件/路径列表。

例如，如果你忘记了 `updatedb` 命令，但记得该命令的一部分，你可以 `su` 切换到 root 用户，然后在 shell 提示符下输入 `up`；按两次 Tab 键，你将看到包括 `updatedb` 在内的可能的命令列表。通过输入部分命令 `upd` 并再次按 Tab 键，你的命令就会为你自动完成。

### 所有权与权限 (Ownership and Permissions)

在本章前面的部分，当你尝试 `cd` 进入 root 的登录目录时，你收到了以下消息：

```
[carlotta@toluca carlotta]$ cd /root
bash:/root: Permission denied
[carlotta@toluca carlotta]$
```

这是 Linux 安全功能的一个演示。与 Unix 不同，Linux 是一个多用户系统，文件权限是系统防止意外或恶意篡改的一种方式。

当你被拒绝权限时，进入的一种方法是 `su` 切换到 root，正如你在本章之前学的那样。这是因为任何知道 root 密码的人对系统都有完全访问权限。

```
[carlotta@toluca carlotta]$ su
Password:your_root_password
[root@localhost carlotta]$# cd /root
[root@localhost /root]$
```

但切换到 root 用户并不总是方便或推荐的，因为作为 root 身份很容易犯错并修改重要的配置文件。

所有文件和目录都由创建它们的人“所有”。例如，如果你在登录目录中创建了 `sneakers.txt` 文件，那么 `sneakers.txt` 就属于你。这意味着你可以指定谁允许读取文件、写入文件，或（如果它是应用程序而不是文本文件）谁可以执行该文件。

读取、写入和执行是权限三个主要设置。由于用户被分配到创建账户时所在的组中，你还可以指定某些组是否可以读取、写入或执行文件。

使用 `ls` 命令的 `-l`（长格式）选项仔细查看 `sneakers.txt`（见图 9-8）：

```
[carlotta@toluca carlotta]$ls -l sneakers.txt
-rw-rw-r-- 1 carlotta carlotta 150 Mar 19 08:08 sneakers.txt
```
