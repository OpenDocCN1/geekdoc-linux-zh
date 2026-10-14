

你需要。Erector Set 呈现出你想象的形状。
它做你想要的事情。

玩具的选择当然是个人化的，那么你会觉得哪种玩具更令人满意？

## 7

## 从 Shell 的视角看世界

![](img/314a0280bc10c5c0d45be132de172677_111_0.png)

在本章中，我们将观察按下 ENTER 键时在命令行上发生的“魔法”。虽然我们将研究 shell 的几个有趣且复杂的特性，但我们只会使用一个新命令来完成：

echo 显示一行文本

### 展开

每次我们输入命令并按下 ENTER 键时，bash 在执行我们的命令之前会对文本进行多次替换。我们已经见过一些简单字符序列，例如 *，对 shell 来说可以有很大意义的情况。使这种现象发生的处理过程称为展开。通过展开，我们输入的内容在 shell 作用于它之前会被展开为其他内容。为了演示我们所说的含义，让我们来看看 echo 命令。echo 是一个 shell 内建命令，执行非常简单的任务。它将文本参数打印到标准输出。

```
[me@linuxbox ~]$ echo this is a test
this is a test
```

这很直接。传递给 echo 的任何参数都会被显示。让我们再试一个例子。

```
[me@linuxbox ~]$ echo *
Desktop Documents ls-output.txt Music Pictures Public Templates Videos
```

发生了什么？为什么 echo 没有打印 *？正如我们从通配符的工作中回忆的那样，* 字符表示匹配文件名中的任意字符，但我们在最初的讨论中没有看到 shell 是如何做到这一点的。简单的答案是 shell 在 echo 命令执行之前将 * 展开为其他内容（在本例中为当前工作目录中的文件名）。当按下 ENTER 键时，shell 会在命令执行前自动展开命令行上的任何符合条件的字符，因此 echo 命令从未看到 *，只看到了其展开后的结果。知道这一点后，我们可以看到 echo 的行为符合预期。

### 路径名展开

通配符工作的机制称为路径名展开。如果我们尝试在前几章中使用的一些技术，我们会发现它们实际上是展开。给定如下的 home 目录：

```
[me@linuxbox ~]$ ls
Desktop   ls-output.txt   Pictures   Templates
Documents Music           Public     Videos
```

我们可以执行以下展开：

```
[me@linuxbox ~]$ echo D*
Desktop Documents
```

以及这个：

```
[me@linuxbox ~]$ echo *s
Documents Pictures Templates Videos
```

甚至这个：

```
[me@linuxbox ~]$ echo [[:upper:]]*
Desktop Documents Music Pictures Public Templates Videos
```

并且在 home 目录之外，我们可以这样做：

```
[me@linuxbox ~]$ echo /usr/*/share
/usr/kerberos/share /usr/local/share
```

### 隐藏文件的路径名展开

正如我们所知，以句点字符开头的文件名是隐藏的。路径名展开也尊重这种行为。如下的展开不会显示隐藏文件：

```
echo *
```

乍一看，我们似乎可以通过在模式前加上前导句点来将隐藏文件包含在展开中，像这样：

```
echo .*
```

它几乎可行。然而，如果我们仔细检查结果，就会看到名称 . 和 .. 也会出现在结果中。因为这些名称指的是当前工作目录及其父目录，使用此模式很可能会产生错误的结果。我们可以通过尝试以下命令来看到这一点：

```
ls -d .* | less
```

为了更好地在这种情况下执行路径名展开，我们必须采用更具体的模式。

```
echo .[!.]*
```

此模式展开为以一个句点开头后跟任意其他字符的每个文件名。这将与大多数隐藏文件正确配合（尽管它仍然不会包含具有多个前导句点的文件名）。带有 -A 选项的 ls 命令（“几乎全部”）将提供隐藏文件的正确列表。

```
ls -A
```

### 波浪号展开

正如我们从对 cd 命令的介绍中可能回忆的那样，波浪号字符（~）具有特殊含义。当用作单词开头时，它会展开为指定用户的主目录名称，或者如果未指定用户，则展开为当前用户的主目录。

```
[me@linuxbox ~]$ echo ~
/home/me
```

如果用户“foo”有账户，则会展开为：

```
[me@linuxbox ~]$ echo ~foo
/home/foo
```

### 算术展开

shell 允许通过展开来执行算术运算。这使我们能够将 shell 提示用作计算器。

```
[me@linuxbox ~]$ echo $((2 + 2))
4
```

算术展开使用以下形式：

```
$((expression))
```

其中 expression 是由值和算术运算符组成的一个算术表达式。

