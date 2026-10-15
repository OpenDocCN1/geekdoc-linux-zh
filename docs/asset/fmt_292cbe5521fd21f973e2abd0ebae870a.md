
Finally, the `-R` parameter recurses through subdirectories. For example, typing `ls /etc` lists all the files and subdirectories in `/etc`, but `ls -R /etc` lists all the files in and subdirectories in `/etc`, all the files and subdirectories in `/etc/acpi`, all the files and subdirectories in `/etc/acpi/actions`, and so on until every subdirectory has been listed.

## Reading Manual Pages with man

Time for a much-needed mental break: The `man` command is easy to use. Most people use only the topic argument, like this: `man gcc`. However, two other commands work closely with `man` that are very useful—`whatis` and `apropos`.

The `whatis` command returns a one-line description of another command, which is the same text you get at the top of that command's man page. For example:

```
[paul@caitlin ~]$ whatis ls

ls (1) - list directory contents
```

The output there explains what `ls` does but also provides the man page section number for the command so you can query it further.

On the other hand, the `apropos` command takes a search string as its parameter and returns all man pages that match the search. For example, `apropos mixer` gives this list:

```
alsamixer (1) - soundcard mixer for ALSA soundcard driver

mixer (1) - command-line mixer for ALSA soundcard driver

aumix (1) - adjust audio mixer
```

So, use `apropos` to help you find commands and use `whatis` to tell you what a command does.

## Making Directories with mkdir

Making directories is as easy as it sounds, although there is one parameter you should be aware of: `-p`. If you are in `/home/paul` and you want to create the directory `/home/paul/audio/sound`, you will get an error like this:

```
mkdir: cannot create directory 'audio/sound': No such file or directory
```

At first glance this seems wrong because `mkdir` cannot create the directory because it does not exist. What it actually means is that it cannot create the directory `sound` because the directory `audio` does not exist. This is where the `-p` parameter comes in: If you try to make a directory within another directory that does not exist, like the previous, `-p` creates the parent directories, too. So:

```
mkdir -p audio/sound
```

That first creates the `audio` directory and then creates the `sound` directory inside it.

## Moving Files with mv

This command is one of the easiest around. There are two helpful parameters to `mv`: `-f`, which overwrites files without asking, and `-u`, which moves the source file only if it is newer than the destination file. That is it!

## Listing Processes with ps

This is the third and last “command that should be simple, but isn’t” that is discussed here. The `ps` command lists processes and gives you an extraordinary amount of control over its operation.

The first thing to know is that `ps` is typically used with what are known as BSD-style parameters. Back in the section “Finding Files by Searching with find,” we discussed UNIX-STYLE, GNU-style, and X-style parameters (`-c`, `- -dosomething`, and `.dosomething`, respectively), but BSD-style parameters are different because they use single letters without a dash.

So, the default use of `ps` lists all processes that you are running that are attached to the terminal. However, you can ask it to list all your processes attached to any terminal (or

确实没有终端）通过添加 `x` 参数：`ps x`。你可以用 `a` 参数要求它列出所有用户的所有进程，或将该参数与 `x` 结合起来列出所有用户的所有进程，无论是否附加到终端：`ps ax`。

然而，这两者都比全能的 `u` 选项逊色，后者启用了面向用户的输出。实际上，这带来了巨大的不同，因为你会得到重要的字段，如所有者的用户名、使用的 CPU 时间和 RAM、进程启动时间等。这会输出大量信息，因此你可能想尝试添加 `f` 参数，它通过使用 ASCII 艺术连接父命令与其子进程来创建进程树。你可以将迄今为止的所有选项与此命令结合：`ps faux`（是的，只要有点想象力，你就可以用参数拼出单词！）。

你可以通过使用 `--sort` 参数来控制数据的返回顺序。它接受 `+` 或 `-`（`+` 为默认值）后跟你想要排序的字段：`command`、`%cpu`、`pid` 和 `user` 都是热门选项。如果你使用减号，结果会被反转。下面的命令按 CPU 使用率降序列出所有进程：

```
ps aux --sort=-%cpu
```

`ps` 还有许多其他参数，包括大量用于与其他 UNIX 系统兼容的选项。如果你有时间阅读 man 手册，你应该试试！

## 使用 rm 删除文件和目录

`rm` 命令只有一个感兴趣的参数：`--preserve-root`。到目前为止，你应该知道使用 `sudo` 执行 `rm -rf /` 会破坏你的 Linux 安装，因为 `-r` 表示递归，`-f` 表示强制（删除前不提示确认）。粗心的人可能会不小心发出此命令——不是故意输入命令，而是把空格放错了位置。例如：

```
rm -rf /home/paul
```
