
## 使用 cat 打印文件内容

许多 Ubuntu 的 shell 命令处理文本，因此如果你想让它们处理文件内容，你需要输出文件。输入`cat`命令，它可以打印传递给它的任何文件的内容。

最基本的用法如下：

```bash
matthew@scour:-$ cat myfile.txt
```

这打印了`myfile.txt`的内容。对于这种用法，有两个常用的额外参数：`-n`对输出中的行进行编号，`-s`（“压缩”）每次最多打印一个空行。如果你的文件有 1 行文本、10 行空行、1 行文本、10 行空行，那么`-s`会显示第一行文本、单个空行、下一行文本、单个空行，以此此类推。当你结合`-s`和`-n`时，`cat`只对打印出的行编号——显示为一个 10 行空行将计为一行。

此命令打印关于你的 CPU 的信息，过滤多个空行并对输出编号：

```bash
matthew@scour:-$ cat -sn /proc/cpuinfo
```

你也可以用`cat`一次打印多个文件的内容，如下：

```bash
matthew@scour:-$ cat -s myfile.txt myfile.txt
```

## 使用 cd 切换目录

切换目录显然是一个没有任何选项的操作，对吧？事实并非如此。`cd`的灵活性比大多数人想象的要得多。与其他大多数命令不同，`cd`本身并不是一个命令——它是`bash`（或你正在使用的任何 shell 解释器）内置的，但它仍然像命令一样使用。

`cd`最基本的用法是：

```bash
matthew@semour:-$ cd somdir
```

这会在当前目录下查找`somdir`子目录，然后进入该目录。你也可以为目录指定精确的位置，如下所示：

```bash
matthew@semour:-$ cd /home/matthew/stuff/somdir
```

`cd`的第一个魔力在于这两个字符（– 和 `~`，即一个连字符和一个波浪号）。第一个表示“切换到我的上一个目录”，第二个表示“切换到我的主目录”。与`cd`的对话展示了这些用法：

```bash
matthew@semour:-$ cd /usr/local
matthew@semour/usr/local$ cd bin
matthew@semour/usr/local/bin$ cd -
/usr/local
matthew@semour/usr/local$ cd ~
matthew@semour:-$
```

在第一行中，我们切换到`/usr/local`，命令没有产生输出。在第二行中，我们切换到`bin`，它是`/usr/local`的子目录。接下来，使用`cd -`回到上一个目录。这次`bash`打印了上一个目录的名字，让我们知道自己现在在哪里。最后，使用`cd ~`回到我们的`/home`目录，尽管如果你想少按几次击键，直接输入`cd`等同于`cd ~`。

`cd`的第二个魔力在于它在预定义的位置查找目录的能力。当你为目录指定一个绝对路径（即以`/`开头的路径）时，`cd`总是会切换到该精确位置。然而，如果你指定一个相对子目录——例如`cd subdir`——你可以告诉`cd`你想相对于该位置去哪里。这是通过`CDPATH`环境变量实现的。如果未设置此变量，`cd`始终使用当前目录作为基准；但你可以将其设置为任何数量的其他目录。

接下来的示例展示了这一测试。它从`/home/matthew/empty`（一个空目录）开始，并对行进行了编号以备后参考：

```bash
1 matthew@semour:~/empty$ pwd
2 /home/matthew/empty
3 matthew@semour:~/empty$ ls
4 matthew@semour:~/empty$ mkdir local
5 matthew@semour:~/empty$ ls
6 local
7 matthew@semour:~/empty$ cd local
8 matthew@semour/empty/local$ cd ..
9 matthew@semour:~/empty$ export CDPATH=/usr
10 matthew@semour:~/empty$ cd local
11 /usr/local
12 matthew@semour:~/usr/local$ cd -
13 /home/matthew/empty
14 matthew@semour:~/empty$ export CDPATH=./usr
15 matthew@semour:~/empty$ cd local
16 /home/matthew/empty/local
17 matthew@semour:~/empty/local$
```

第 1-3 行显示我们处于`/home/matthew/empty`且它确实是空的；`ls`没有输出。第 4-6 行显示创建了`local`子目录，因此`/home/matthew/empty/local`存在。第 7 和 8 行显示你可以进入`/home/matthew/empty/local`再退出。

在第 9 行中，`CDPATH`被设置为`/usr`。选择它是因为 Ubuntu 的目录 (`/home/matthew/empty`) 和我们的`CDPATH`目录 (`/usr`) 都包含一个`local`子目录。在第 10 行中，位于`/home/matthew/empty`目录时，我们使用`cd local`。这次，`bash`切换到了`/usr/local`并打印了新目录以确保我们知道它做了什么。

第 12 和 13 行让我们回到上一个目录`/home/matthew/empty`。在第 14 行中，`CDPATH`设置为`:./usr`。冒号是分隔符，这意味着`bash`应该先查找当前目录`.`，然后在`/usr`目录中查找。在第 15 行执行了`cd local`，这次移动到了`/home/matthew/empty/local`。

注意，`bash`仍然打印了新目录；每当它在`CDPATH`中查找目录时，它都会这样做。

## 使用 chmod 更改文件访问权限

你对`chmod`的用法可以通过一个简单的参数极大扩展：`-c`。它指示`chmod`打印其操作过程中所做的所有更改列表，我们可以捕获输出并用于其他用途。例如：

```bash
mathew@seymour:$ chmod -c 600 *
mode of '1.txt' changed to 0600 (rw------)
mode of '2.txt' changed to 0600 (rw------)
mode of '3.txt' changed to 0600 (rw------)
mathew@seymour:$ chmod -c 600 *
mathew@seymour:$$
```

如果你想知道系统变量的值，例如`TERM`，输入变量名即可输出其值，如下：

```bash
matthew@seymour:~$ echo $TERM
```

你可以将`echo`的输出重定向到文本文件中，例如当我想向`PATH`中添加一个新目录时，如下：

```bash
matthew@seymour:~$ echo export
PATH=$PATH:/usr/local/bin/ >> ~/.bashrc
```

你可以在`/proc`中更改或设置内核设置（1=开启，0=关闭），如下：

```bash
matthew@seymour:~$ sudo -c 'echo "1"
>/proc/sys/location/of/setting'
```

注意，你可以使用`cat`命令读取`/proc`中内核值的设置。

## 使用 find 查找文件

`find`命令是 Linux 中领域最晦涩且最不为人理解的领域之一，但它也是最强大的工具之一。诚实地说，`find`命令本身并没有通过使用 X 风格的参数来利于自身。UNIX 标准是使用`-c`、`-s`等，而 GNU 标准是使用`--dosomthing`、`--mooby`等。X 风格参数通过在单横线前加节点来合并两者。

然而，`find`最大的问题是它的选项比大多数人能记住的多得多；它确实能够完成你想要的大多数任务。最基本的用法如下：

```bash
matthew@seymour:~$ find -name "*.txt"
```
