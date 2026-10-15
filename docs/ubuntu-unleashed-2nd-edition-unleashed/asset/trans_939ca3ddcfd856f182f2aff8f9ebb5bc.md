

```
[paul@caitlin bin]$ cd -
/usr/local
[paul@caitlin local]$ cd -
[paul@caitlin ~]$
```

第一行中，我们切换到 /usr/local 且命令没有输出。在第二行，我们切换到 bin，它是 /usr/local 的一个子目录。接下来使用 cd - 来切换回上一个目录。这次 Bash 打印了上一个目录的名称，以便我们知道自己所在的位置。最后，使用 cd - 切换回我们的主目录，虽然如果你想节省几个按键，只输入 cd 本身就等同于 cd ~。

cd 的第二个神奇之处在于它能够在预定义的位置查找目录。当你指定目录的绝对路径（即以 / 开头的路径）时，cd 总是切换到那个确切位置。然而，如果你指定一个相对子目录——例如 cd subdir——你可以告诉 cd 相对于何处进行查找。这是通过 CDPATH 环境变量实现的。如果该变量未设置，cd 总是以当前目录作为基准；不过，你可以将其设置为任意多个其他目录。

下面的示例展示了对此的测试。它从 /home/paul/empty 开始，这是一个空目录，并且行号已标注以便后续引用：

```
1 [paul@caitlin empty]$ pwd
2 /home/paul/empty
3 [paul@caitlin empty]$ ls
4 [paul@caitlin empty]$ mkdir local
5 [paul@caitlin empty]$ ls
6 local
7 [paul@caitlin empty]$ cd local
8 [paul@caitlin local]$ cd ..
9 [paul@caitlin empty]$ export CDPATH=/usr
10 [paul@caitlin empty]$ cd local
11 /usr/local
12 [paul@caitlin empty]$ cd -
13 /home/paul/empty
14 [paul@caitlin empty]$ export CDPATH=.:/usr
15 [paul@caitlin empty]$ cd local
16 /home/paul/empty/local
17 [paul@caitlin local]$
```

第 1–3 行显示我们位于 /home/paul/empty 且它确实是空的——ls 没有输出。第 4–6 行显示 local 子目录被创建，因此 /home/paul/empty/local 存在。第 7 和 8 行显示你可以 cd 进入 /home/paul/empty/local 再返回。

第 9 行中，CDPATH 被设置为 /usr。之所以选择它是因为 Ubuntu 有 /usr/local 目录，这意味着我们的当前目录 (/home/paul/empty) 和 CDPATH 目录 (/usr) 都存在一个 local 子目录。第 10 行中，在 /home/paul/empty 目录下，我们使用 cd local。这次 Bash 将我们切换到 /usr/local 甚至打印新目录以确保我们知道它做了什么。

第 12 和 13 行将我们移回上一个目录 /home/paul/empty。第 14 行中，CDPATH 被设置为 .:/usr。 : 是目录分隔符，这意味着 Bash 应该先在当前目录 . 中查找，然后在 /usr 目录中查找。第 15 行再次发出 cd local，这次移动到 /home/paul/empty/local。请注意 Bash 仍然打印了新目录——只要它在 CDPATH 中查找目录就会这样做。

## 使用 chmod 修改文件访问权限

你在第 5 章学到的关于 chmod 的知识可以通过一个简单的参数大大扩展：-c。该参数指示 chmod 在操作过程中打印它所做的所有更改的列表，这意味着我们可以捕获输出并将其用于其他目的。例如：

```
[paul@caitlin tmp]$ chmod -c 600 *
mode of '1.txt' changed to 0600 (rw-------)
mode of '2.txt' changed to 0600 (rw-------)
mode of '3.txt' changed to 0600 (rw-------)
[paul@caitlin tmp]$ chmod -c 600 *
[paul@caitlin tmp]$
```

这里 chmod 命令带 -c 发出，你可以看到它输出了操作结果：三个文件被更改为 rw-------（仅用户可读可写）。然而再次发出该命令时，没有输出返回。这是因为 -c 只打印它所做的更改。权限已与你要设置的权限匹配的文件保持不变，因此不会被打印。

还有两个其他参数值得关注：--reference 和 -R。第一个允许你指定一个文件作为权限模板，而不是自己指定权限。例如，如果你希望当前目录中的所有文件都具有与文件 /home/paul/myfile.txt 相同的权限，你会使用：

```
chmod --reference /home/paul/myfile.txt *
```

你可以使用 -R 来启用递归操作，这意味着你可以用它来 chmod 一个目录，它将更改该目录以及该目录下所有文件和子目录的权限。你可以使用 chmod -R 600 /home 将 /home 下的每个文件和目录都更改为仅其所有者可读/写。

## 使用 cp 复制文件

与稍后介绍的 mv 类似，cp 也是一个易于使用和掌握的命令。然而，两个很棒的参数很少被使用（这很遗憾！）尽管它们

