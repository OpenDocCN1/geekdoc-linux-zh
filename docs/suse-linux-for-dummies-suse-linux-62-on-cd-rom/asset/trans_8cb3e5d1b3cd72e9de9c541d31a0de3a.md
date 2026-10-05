
# 140 第三部分：使用 SuSE Linux

现在所有内容不再输出到屏幕上，而是输出到名为 `dogfile` 的文件中，这是 Linux 为我们创建的，因为该文件名之前并不存在。

+ 2. 尽情输入吧。
3. 完成后，只需在空行上按 `^D`。
你就回到了 Linux 提示符。

你是否在想 `cat` 命令是否执行了你想要的操作？你可以再次使用 `cat` 命令和文件名来检查：

```
maddog@shame:- > cat dogfile
Hi again
Dogfish. Dogleg. Dog days.
Doghouse. Dogfight. Doggone.
maddog@shame:- >
```

这一次，`cat` 命令将文件从磁盘中读取，并将输出置到标准输出（也称为标准输出），在本例中，输出就是你的电脑屏幕。

如果你想出其他想添加到文件中的内容，可以使用文件名配合追加符号（`>>`）。你输入的任何内容都会被添加到文件的末尾。回到 `dogfile`：

```
maddog@shame:- > cat dogfile
Dog-eared. Doggerel.
```

![](img/96a9ce6a13d8d15ed05f867f41574278_167_0.png)

我们让你困惑了吗？你使用 `cat` 命令是为了合并文件，或者将输入连接到文件的开头或末尾。它是唯一为此目的创建的命令。你也可以使用 `>>` 符号将数据添加到文件末尾。

`>>` 符号可以用于许多 Linux 命令。例如：

```
cat file2 file3 file4 >>fileout
```

将 `file1`、`file2`、`file3` 和 `file4` 合并，并将结果放入 `fileout`。在接下来：

```
sort file1 >>file2
```

`sort` 命令对 `file1` 的内容进行排序并将其追加到（可能已经存在的）`file2`。如果 `file2` 不存在，系统将创建 `file2` 并排序后的输出放入其中。

完成后，确保使用 `^D` 结束会话。

## 操作文件和目录

Linux 有许多方法来创建、移动、复制和删除文件及目录。其中某些方法非常简单用，以至于你必须小心：与其他操作系统不同，Linux 不会提醒你正要覆盖一个文件——它只会遵循你的指令并直接覆盖！

我们说过一次了，但还会说一遍：在学习这些章节时，确保你没有以 root 身份登录。

## 创建目录

在 Linux 中创建新目录，你将使用 `mkdir` 命令（就像在 DOS 中一样）。命令格式如下：

```
maddog@shamet:~ mkdir newdirectory
```

这会在你的当前或工作目录下创建一个子目录。如果你想在另一个目录下创建子目录，请先切换到该目录，然后创建新的子目录。

创建一个名为 `santa_cruz` 的新目录。动手吧，执行它：

```
mkdir santa_cruz
```

（你能猜出我们现在更想去哪儿吗？）

现在创建另一个名为 `work` 的目录：

```
mkdir work
```

并切换目录进入 `santa_cruz` 目录：

```
cd santa_cruz
```

现在使用你之前学到的 `cat` 命令在 `santa_cruz` 下创建一个名为 `radman` 的文件：

```
cat >radman
Once upon a time there lived a handsome prince.
^D
```

现在创建另一个文件：

```
cat >jewels
Once upon a time there lived a beautiful princess.
^D
```

## 142 第三部分：使用 SuSE Linux

还有一个：

```
cat >moody
The handsome prince and beautiful princess had a dog named
Moody.
^D
```

现在你有一些文件可以操作了。

## 移动和复制文件及目录

移动和复制目录及文件的命令是 `mv`（移动）和 `cp`（复制）。如果你想重命名文件，可以使用 `move` 命令。不，你并不是真的在移动文件，但在 Linux（以及 UNIX）中，开发者意识到重命名在很大程度上就是移动。`move` 命令的格式为：

```
mv <source> <destination>
```

使用你的示例文件，你可以通过以下命令将名为 `radman` 的文件移动为名为 `bryant` 的文件：

```
mv radman bryant
```

这让文件留在了 `santa_cruz` 目录中，但将其名称更改为 `bryant`。所以你看，文件并没有真的移动，只是重命名了。

现在尝试将 `bryant` 文件移动到 `work` 目录。要做到这一点，你必须先将文件向上，然后进入 `work` 目录。你可以用一条命令完成：

```
mv bryant ../work
```

注意目标文件使用了 `..`（或父目录）标识。这告诉 Linux 向上一个目录级别寻找名为 `work` 的目录，然后将文件以 `bryant` 的名称放入该目录，因为你没有指定其他名称。如果你坚持这样做：

```
mv bryant ../work
```

那么 `bryant` 文件将被移动到 `work` 目录并更名为 `supersalesman`。注意，在这两种情况下（文件保留名称 `bryant` 或取新名称 `supersalesman`），你的当前目录仍然 `santa_cruz`，并且所有的文件名都是相对于该目录的。

## 第 8 章：文件操作与命令

## 143

![](img/96a9ce6a13d8d15ed05f867f41574278_170_0.png)

严格来说，文件并没有真正移动。数据位仍然位于它们最初所在的磁盘部分。你用来描述文件的文件规范（目录路径加文件名）变了，所以它看起来像是移动了。

在 UNIX 版本中，你不允许使用 `mv` 将文件从一个分区移动到另一个分区；你只能使用 `cp(1)` 命令进行复制。Linux 允许你使用 `mv` 命令将文件移动到任何地方。通常，`mv` 在原地重命名数据并更改文件名以及名称所在的目录。但当文件跨分区移动时（例如从 Linux 系统的 `/usr` 到 `/home`），数据被复制到新的磁盘分区，新名称被放在该分区的目录结构中，而文件名和数据从旧磁盘分区中移除。

## 删除文件

移除或删除的命令是 `rm`。如果你一直跟着故事学，现在现在 `santa_cruz` 目录下有两个公主（`jewels` 和 `jewels2`）。由于你不需要它们了，让我们把它们删掉：

## 144 第三部分：使用 SuSE Linux

```
rm jewels2
```

你已经从当前目录删除了该文件。要从另一个目录删除文件，你需要提供相对或绝对文件名。例如，如果你想从 `work` 目录剔除 `moody`，请输入：

```
rm ../moody
```

![](img/96a9ce6a13d8d15ed05f867f41574278_171_0.png)

## 删除目录

你不仅可以删除文件，还可以删除目录。如果你还在跟进帅气王子和公主的故事，你现在主目录下有两个占用很小空间的目录。由于你不需要它们了，可以删除它们并收回这些空间。

首先，回到你的主目录：

```
daddog@shamet:~ > cd
```

现在删除 `santa_cruz` 目录：

```
daddog@shamet:~ rm -rf santa_cruz
```

此操作会删除 `santa_cruz` 目录及其所有的文件和目录。注意这是带有递归（recursively）和强制（forcefully）选项的 `rm` 命令。（递归意味着继续向下进入目录结构并删除你发现的所有文件和目录。强制意味着只要可能就应该删除文件；忽略 `rm` 可能会提示用户更多信息的情况）。
