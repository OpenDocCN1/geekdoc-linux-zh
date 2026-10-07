

## 2.3.2 答案

运行以下命令：

```
set -o noclobber
touch out out1
cat out > out1
```

- a) 错误信息意味着什么？
答案：你应该得到如下内容：
$ set -o noclobber
$ touch out out1
$ cat out > out1
-ksh: out1: file already exists [文件已存在]

如果 `out` 和 `out1` 不存在，`touch` 命令将创建名为这两个名字的空文件。（如果其中任何一个已经存在，`touch` 会静静地将其最后修改时间设为“现在”，但这与本次练习无关。）

错误信息显示程序 `ksh` 发现名为 `out1` 的文件已经存在。为什么信息不是来自 `cat` 而是来自 `ksh`？因为是因为 shell（壳）设置了 I/O 重定向并发现了问题。`cat` 命令根本没有执行。

现在运行这些命令：

```
set -o noclobber
touch out out1
cp out out1
```

- b) 为什么这次没有错误信息？
答案：尽管设置了 `noclobber` 选项，但没有错误信息（文件 `out` 确实被复制到了文件 `out1`），因为 `noclobber` 是 shell 选项，它只影响 shell 执行，例如输出重定向。

`cp` 命令没有办法知道 shell 中设置了哪些选项；`cp` 和 `ksh` 是完全独立的程序。

## 实验 2.3: 命令语法

- c) `set -o noclobber` 起什么作用？
答案：它防止你使用重定向覆盖现有文件。

`noclobber` 选项可以帮助你避免错误，但设置它并不能保护你，除了 shell 知晓的事项，例如输出重定向。

使用 `set +o noclobber` 关闭 `noclobber` 选项，再次尝试将 `cat` 的输出重定向到现有文件。

- d) `set +o noclobber` 起什么作用？
答案：它关闭 `noclobber` 选项。你应该看到如下内容：

```
$ set +o noclobber
$ touch out1
$ cat out > out1
$ 
```

没问题！使用加号关闭该选项（这是 shell 的默认行为），shell 允许你将输出重定向到现有文件而无抱怨。新文件将覆盖旧文件的任何内容。

- e) `set -o noclobber` 和 `set -C`，或者 `set +o noclobber` 和 `set +C` 之间有区别吗？
答案：如下序列所示，没有区别：

```
$ set -C
$ touch out1
$ cat out > out1
- ksh: out1: file already exists [文件存在]
$ set +C
$ touch out out1
$ cat out > out1
$ 
```

对于 shell 来说，使用哪种形式的 `set` 命令并不重要；它们是相同的。有些 shell 选项只能使用 `-o` 选项形式设置，因为没有短格式可用。请参附录 B“命令总结”获取两种形式的完整列表。

## 第2章：命令语法 103

在脚本和函数中使用 `set -o noclobber` 形式，因为这会让你的程序更易读。在交互式输入命令时，`set -C` 形式可以节省几次击键，但你必须学习哪个字母对应哪个选项名称。

开启 `noclobber` 选项，并使用 `cat` 配合 `>>` 在 `out1` 中创建 `out` 的两个副本。

- f) 你输入了哪些命令？
答案：你可以使用以下命令序列：
$ rm -f out1
$ touch out1
$ set -C
$ cat out out >> out1

前两个命令确保 `out1` 存在但是空的。

即使设置了 `noclobber`，`>>` 重定向也允许你向现有文件的末尾添加内容。

注意 `cat` 命令中文件 `out` 作为参数出现了两次。如果你指定了多个参数，`cat` 会依次从每个参数中读取内容，因此这个 `cat` 命令在 `out1` 中创建了两个 `out` 的副本。

- g) 你如何验证 `out1` 包含两个 `out` 的副本？
答案：因为文件非常小，你可以直接打印出它，如下所示：
$ more out1
hello again
good-bye again
hello again
good-bye again
$

你也可以使用 `ls -1` 查看文件大小，但这无法告诉你它们是否实际上包含相同的信息。

## 实验 2.3: 命令语法

你可以使用 `sdiff` 命令对两个文件进行并排比较。你需要使用 `-w 80` 选项使输出适应 80 字符宽的窗口。如果文件很长，你可能会将输出通过到 `less` 或 `more`。

![](img/694fa9f0320e707804a4c650b96a09b4_123_0.png)

在 `noclobber` 选项仍然开启的情况下，使用 `>/` 用单个 `out` 副本覆盖 `out1`，并验证 `out1` 已被覆盖。

- h) 你使用了哪些命令？
```
答案：以下命令序列可以完成要求的操作：
$ rm -f out1
$ touch out1
$ set -o noclobber
$ cat out >| out1
$ sdiff -w80 out1
hello again
good-bye again
$
```

你可以使用 `diff` 命令来确保文件相同，但 `sdiff` 让你查看内容。

> 一些其他的 shell 使用 `>!` 的方式就像 KornShell 使用 `>|` 一样。也就是说，它使用感叹号而不是竖线来覆盖 `noclobber` 选项。不要混淆这两个符号。KornShell 不会在任何与重定向相关的操作中使用感叹号。

![](img/694fa9f0320e707804a4c650b96a09b4_123_1.png)

- i) 你是如何验证文件被覆盖的？
答案：`rm` 和 `touch` 命令保证了 `out1` 存在但字节为零。

逻辑上讲，给出的解决方案并没有证明 `out1` 是被追加而不是覆盖的。如果你不确定是被覆盖还是追加的，可以 cat 另一个文件覆盖它。

## 第2章：命令语法 105

## 2.3.3 答案

尝试使用 `cat` 将输出重定向到 stdout（标准输出）。

- a) 你看到了什么错误信息？
答案：这里有一个使用该文件的交互：
$ rm -f out1
$ cat out1
-ksh: out1: cannot open [没有文件]

错误信息显示程序 `ksh` 发现名为 `out1` 的文件已经存在。为什么信息不是来自 `cat` 而是来自 `ksh`？因为是因为 shell 设置了 I/O 重定向并发现了问题。`cat` 命令根本没有执行。

- b) 你使用了哪些命令？
答案：以下命令序列可以完成要求：
$ rm -f out1
$ touch out1
$ set -o noclobber
$ cat out >| out1
$ sdiff -w80 out1
hello again
good-bye again
$

- c) 你在 errorlog 中看到了两个消息吗？
答案：如预期，errorlog 包含了两个消息。

- d) 如果 `2>` 表示重定向 stderr（标准错误），那么 `0<` 和 `1>` 代表什么？
答案：分别重定向 stdin 和 stdout。

## 实验 2.3: 命令语法 106

三个标准描述符数字分别是：0 代表 stdin，1 代表 stdout，2 代表 stderr。

- e) 写一个 `cat` 命令，使用描述符将文件 `out` 复制到 `out1`。
答案：以下交互显示了 `cat` 命令并验证了它的有效性。

```
$ cat 0<out >|out1
$ more out1
hello again
good-bye again
$
```

注意输出重定向使用了 `1>`。如果你知道文件不存在或者知道 shell 的 `noclobber` 选项未设置，你可以直接使用 1。

- f) 记得 `out1 > out2` 表示将 stdout 重定向到 `out2`（正如你之前看到的），你认为 `out>3 2>3` 表示什么？
答案：这意味着 stdin 和 stderr 都重定向到了同一个文件，但它行不通，如下交互所示：

```
$ rm -f out3
$ set -o noclobber
$ cat out1>out3 2>out3
-ksh: out3: file already exists [文件存在]
$
```

问题在于 shell 看到了两个独立的输出重定向。当它看到 `1>out3` 时，它创建了一个字节为零的文件 `out3`。然后当它看到 `2>out3` 时，文件 `out3` 已经存在，且由于设置了 `noclobber` 而没有使用 `>|`，重定向失败。`cat` 命令从未运行，因为问题被 shell 检测到了。

如果没有设置 `noclobber`，shell 会运行 `cat` 命令，但这里还有另一个微妙的问题是你在你使用 `cat` 时无法看到的，即一个向 stdout 和 stderr 写入内容的程序在使用这种重定向形式时，产生的输出行顺序可能与链接 fd 不同，这将在下一个练习中涵盖。该问题基于操作系统对写入 stdout 的输出进行缓存，但对 stderr 则不缓存。

