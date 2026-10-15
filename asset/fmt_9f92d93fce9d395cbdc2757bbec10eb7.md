
`matthew@semour:-$ cat myfile.txt`

```
```

这打印了 `myfile.txt` 的内容。对于这种用法，有两个经常使用的额外参数：`-n` 在输出中显示行号，`-s`（“压缩”）一次最多打印一个空行。这意味着，如果你的文件有 1 行文本、10 个空行、1 行文本、10 个空行，以此类推，`-s` 会显示第一行文本、一个空行、下一行文本、一个空行，以此此类推。当你结合 `-s` 和 `-n` 使用时，`cat` 只对打印的行进行编号——显示的 10 个空行被视为一个计数行。

此命令打印关于你的 CPU 的信息，删掉多个空行并对输出进行编号：

```
matthew@semour:-$ cat -sn /proc/cpuinfo
```

你也可以使用 `cat` 一次打印多个文件的内容，如下：

```
matthew@semour:-$ cat -s myfile.txt mymyfile.txt
```

在命令中，`cat` 在输出时合并了 `myfile.txt` 和 `mymyfile.txt`，并删除了多个空行。重要的是，`cat` 在输出中不区分这些文件；没有打印文件名，两个文件之间没有额外的间隔符。这允许你将这 2 个文件视为 1 个，或者通过在命令行中添加更多文件，将 20 个文件视为 1 个。

## 使用 cd 切换目录

切换目录显然没有任何选项，对吧？事实并非如此，`cd` 实际上比大多数人想象的要灵活。与这里的大多数其他命令不同，`cd` 本身并不是一个命令——它是内置在 `bash`（或你使用的任何 shell 解释器）中的，但它仍然像命令一样使用。

`cd` 最基本的用法是这样的：

```
matthew@semour:-$ cd somedir
```

这在当前目录中查找 `somedir` 子目录然后进入该目录。你也可以为目录指定精确的位置，如下：

```
matthew@semour:-$ cd /home/matthew/stuff/somedir
```

## 命令行大师课

`cd` 魔法的第一部分在于字符（`-` 和 `~`，一个破折号和一个波浪号）。第一个表示“切换到上一个目录”，第二个表示“切换到主目录”。与 `cd` 的这段对话展示了这种用法：

```
matthew@semour:-$ cd /usr/local
matthew@semour:/local$ cd bin
matthew@semour:/local/bin$ cd -
matthew@semour:/local$ cd -
```

在第一行中，我们切换到 `/usr/local`；在第二行，我们从 `/local` 进入 `bin`；在第三行，我们在 `/local/bin` 输入 `cd -`；在第四行，我们从 `/local` 输入 `cd -`。

`cd` 魔法的第二部分是它的能力。`cd` 魔法的第二部分是它的能力。`cd` 魔法的第二部分是它的能力。`cd` 魔法的第二部分是它的能力。`cd` 魔法的第二部分是它的能力。`cd` 魔法的第二部分是它的能力。

```
matthew@semour:-$ cd /usr/local
matthew@semour:/local$ cd bin
matthew@semour:/local/bin$ cd -
matthew@semour:/local$ cd -
```

```
matthew@semour:-$ cd /usr/local
matthew@semour:/local$ cd bin
matthew@semour:/local/bin$ cd -
matthew@semour:/local$ cd -
```

在第一行中，我们切换到 `/usr/local`；在第二行中，我们从 `/local` 进入 `bin`；在第三行，我们在 `/local/bin` 输入 `cd -`；在第四行中，我们从 `/local` 输入 `cd -`。

`cd` 魔法的第一部分在于字符（`-` 和 `~`，一个破折号和一个波浪号）。第一个表示“切换到上一个目录”，第二个表示“切换到主目录”。与 `cd` 的这段对话展示了这种用法：

```
matthew@semour:-$ cd /usr/local
matthew@semour:/local$ cd bin
matthew@semour:/local/bin$ cd -
matthew@semour:/local$ cd -
```

在第一行中，我们切换到 `/usr/local`；在第二行中，我们从 `/local` 进入 `bin`；在第三行，我们在 `/local/bin` 输入 `cd -`；在第四行中，我们从 `/local` 输入 `cd -`。

`cd` 魔法的第二部分是它的能力。`cd` 魔法的第二部分是它的能力。`cd` 魔法的第二部分是它的能力。`cd` 魔法的第二部分是它的能力。`cd` 魔法的第二部分是它的能力。`cd` 魔法的第二部分是它的能力。

- `ls`—列出当前目录下的文件。
- `make`—编译并安装程序。
- `man`—显示用于阅读的手页（帮助文档）。
- `mkdir`—创建目录。
