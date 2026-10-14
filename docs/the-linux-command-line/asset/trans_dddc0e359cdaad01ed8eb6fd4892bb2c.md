

```
[me@linuxbox playground]$ rm -i fun
rm: remove regular file `fun'?
```

在提示符后输入“y”，文件就会被删除。不过，我们再看一下 ls 的输出。注意 fun-sym 发生了什么变化？由于它是一个指向现已不存在文件的符号链接，因此该链接是断开的：

```
[me@linuxbox playground]$ ls -l
total 8
drwxrwxr-x 2 me me 4096 2008-01-15 15:17 dir1
lrwxrwxrwx 1 me me 4 2008-01-16 14:45 dir1-sym -> dir1
drwxrwxr-x 2 me me 4096 2008-01-15 15:17 dir2
lrwxrwxrwx 1 me me 3 2008-01-15 15:15 fun-sym -> fun
```

大多数 Linux 发行版都会配置 ls 以显示断开的链接。在 Fedora 系统上，断开的链接会以闪烁的红色文本显示！存在断开的链接本身并不危险，但确实相当凌乱。如果我们尝试使用断开的链接，就会看到这样的信息：

```
[me@linuxbox playground]$ less fun-sym
fun-sym: No such file or directory
```

我们来做一点清理。删除这些符号链接：

```
[me@linuxbox playground]$ rm fun-sym dir1-sym
[me@linuxbox playground]$ ls -l
total 8
drwxrwxr-x 2 me me 4096 2008-01-15 15:17 dir1
drwxrwxr-x 2 me me 4096 2008-01-15 15:17 dir2
```

关于符号链接需要记住的一点是：大多数文件操作都是针对链接的目标进行的，而不是对链接本身。rm 是个例外。当你删除一个链接时，被删除的是链接本身，而不是目标。

最后，我们要删除我们的 playground。为此，我们返回主目录，并使用带递归选项（-r）的 rm 删除 playground 及其所有内容，包括它的子目录：

```
[me@linuxbox playground]$ cd
```
```
[me@linuxbox ~]$ rm -r playground
```

## 使用 GUI 创建符号链接

GNOME 和 KDE 中的文件管理器都提供了一种简单而自动的创建符号链接的方法。在 GNOME 中，拖动文件时按住 Ctrl+Shift 键将创建链接，而不是复制（或移动）文件。在 KDE 中，每当放下文件时都会出现一个小菜单，提供复制、移动或链接文件的选项。

## 总结

我们在这里涵盖了大量内容，需要一段时间才能完全消化。反复执行 playground 练习，直到理解它为止。充分理解基本的文件操作命令和通配符非常重要。请随意扩展 playground 练习，添加更多文件和目录，并使用通配符来指定用于各种操作的文件。链接的概念起初有些令人困惑，但请花时间学习它们的工作原理。它们在关键时刻真的能派上大用场。

## 识别命令

通常，确切知道正在使用的是四种命令中的哪一种很有用，Linux 提供了几种方法来确定这一点。

## type – 显示命令的类型

type 命令是一个 shell 内建命令，在给定特定命令名的情况下，它会显示 shell 将要执行的命令的种类。它的工作方式如下：

```
type command
```

其中“command”是您想要检查的命令的名称。下面是一些示例：

```
[me@linuxbox ~]$ type type
type is a shell builtin
[me@linuxbox ~]$ type ls
ls is aliased to `ls --color=tty'
[me@linuxbox ~]$ type cp
cp is /bin/cp
```

这里我们看到了三个不同命令的结果。注意关于 ls 的结果（取自 Fedora 系统），以及 ls 命令实际上是一个带有“--color=tty”选项的 ls 命令的别名。现在我们明白了为什么 ls 的输出会以彩色显示了！

## which – 显示可执行程序的位置

有时，系统上安装了不止一个版本的可执行程序。虽然这在桌面系统上并不常见，但在大型服务器上却并不稀奇。要确定某个可执行程序的确切位置，可以使用 which 命令：

```
[me@linuxbox ~]$ which ls
/bin/ls
```

which 只适用于可执行程序，不适用于内建命令，也不适用于作为实际可执行程序替代品的别名。例如，当我们尝试对 shell 内建命令（如 cd）使用 which 时，要么没有响应，要么会出现错误信息：

```
[me@linuxbox ~]$ which cd
/usr/bin/which: no cd in (/opt/jre1.6.0_03/bin:/usr/lib/qt-3.3/bin:/usr/kerberos/bin:/opt/jre1.6.0_03/bin:/usr/lib/ccache:/usr/local/bin:/usr/bin:/bin:/home/me/bin)
```

which 是“找不到命令”的一种婉转说法。

## 获取命令的文档

了解了命令是什么之后，我们现在可以为每种命令查找可用的文档了。

## help – 获取 shell 内建命令的帮助

bash 为每个 shell 内建命令都提供了一个内建的帮助功能。要使用它，输入“help”，后跟 shell 内建命令的名称。例如：

```
[me@linuxbox ~]$ help cd
cd: cd [-L|-P] [dir]
Change the current directory to DIR. The variable $HOME is the default DIR. The variable CDPATH defines the search path for the directory containing DIR. Alternative directory names in CDPATH are separated by a colon (:). A null directory name is the same as the current directory, i.e. ‘..’. If DIR begins with a slash (/), then CDPATH is not used. If the directory is not found, and the shell option ‘cdable_vars’ is set, then try the word as a variable name. If that variable has a value, then cd to the value of that variable. The -P option says to use the physical directory structure instead of following symbolic links; the -L option forces symbolic links to be followed.
```

关于记法的一点说明：当命令语法描述中出现方括号时，它们表示可选项。竖线字符表示互斥的选项。以上面的 cd 命令为例：

cd [-L|-P] [dir]

这种记法表示 cd 命令后面可以可选地跟“-L”或“-P”，并且还可以可选地跟参数“dir”。

虽然 help 对 cd 命令的输出简洁而准确，但它绝

