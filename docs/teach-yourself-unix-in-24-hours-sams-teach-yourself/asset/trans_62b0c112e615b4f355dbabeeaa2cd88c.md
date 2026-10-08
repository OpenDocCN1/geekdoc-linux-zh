

# 274

# 第 12 小时

学会这个新命令后，你可以尝试它的另一种变体，这次是将整个段落传递给 `fmt` 命令。我仍然处于文本中 "When" 词的开头。所以，当我输入命令 `itfmt` 时，整个段落被清理了，屏幕变成了这样：

# 双城记
 序言

Chuck，这是我目前的文件：

当我与孩子们和朋友一起表演威尔基·柯林斯先生（Mr. Wilkie Collins）的戏剧《冰封》（The Frozen Deep）时，我首次构思了这个故事的核心思想。一种强烈的欲望驱使着我，将其化化到我身上；我在脑海中勾勒出，这种状态需要我作为一个敏锐的观察者，带着特殊的关注和兴趣来呈现它。

随着这个想法变得对我越来越熟悉，它逐渐形成了现在的形状。在执行它的过程中，它完全占据了我；到目前为止，我所证实的这些页中所做、所经历的，正如我亲自所经历的那样。

每当这里（无论多微小）提到革命前或革命期间法国人的状况时，都是基于最可靠的证人的信言。我的愿望之一是尽可能少增加几行。

再次，`vi` 告诉我们文件中的行数由于命令而发生了变化。在这种情况下，收紧段落实际上也减少了两个行。

这个命令非常有用，以至于我经常不得不用 `map` 命令将其绑定到特定的键。在像这样的 `.exrc` 文件中实现此点的典型方法是：
`map ^P it()fmt^M`

`^` 是 `vi` 用于记录回车键（Return）的符号。（记得你需要先使用 `^v`。）在我的 `.exrc` 中定义此内容后，我可以按 `^p` 来格式化当前段落。

- 5. 在结束这一小时的内容之前，我将再提供一个该命令的示例。还记得第 10 小时引入的 `awk` 命令吗？记得它如何轻松地用于提取特定字段的信息吗？这在 `vi` 中非常有帮助。不过，我不再继续处理 `dickens.intro` 文件，而是退出创建一个新文件，其中包含来自 `is` 命令的一些输出：

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_283_0.png)

# 高级 vi 技巧、工具与技术

% ls -CF
Archives/ big-output dickens.note src/
InfoWorld/ bigfiles keyline.pie temp/
Mast/ bin/ newfile
News/ buckaroo owl/
OWL/ buckaroo.confused sample
% ls -l a* > listing

现在我使用 `vi listing` 来从 `ls` 命令的输出开始开始工作：

```
-rw-rw---- 1 taylor 126 Dec 16:34 awkscript
-rw-rw---- 1 taylor 1659 Dec 3 23:26 big.output
-rw-rw---- 1 taylor 165 Dec 3 16:42 bigfiles
-rw-rw---- 1 taylor 270 Dec 4 15:09 buckaroo
-rw-rw---- 1 taylor 458 Dec 4 23:22 buckaroo.confused
```

"listing" 5 行，282 个字符

如果以此为基础创建一个 shell 脚本（它只是系列你可能直接输入到 shell 的命令，都整齐地保在一个文件中），那就太好了。一个 shell 脚本可以显示每个文件的第一行和最后一行，并去掉中间部分。条目如下：

```
echo filename=
head -5 filename; tail -5 filename
```

我将结合 `vi` 中的 `!` 命令和 `awk` 命令来实现此：

```
awk "{ print \"echo \"$0;\"$4 bytes... tail $8\" }"
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_284_0.png)

当光标位于此文件的最顶部时，我现在可以输入 `|` 将整个文件通过管道。光标掉到底部，然后我输入之前的 `awk` 脚本并按回车。结果如下：

```
echo awkscript
head -5 script; echo 126 bytes...
echo big.output
head -5 output; echo 1659 bytes...
echo bigfiles
head -5 bigfiles; echo 125 bytes...
echo buckaroo
head -5 buckaroo; echo 270 bytes...
echo buckaroo.confused
head -5 buckaroo.confused; echo 458 bytes...
```
```awk '{ (print \"echo \"$8\"; print \"head \"$8\"; echo \"$4 bytes... tail $8\") }'
```

如果我现在退出并要求解释内容，会发生这些：

```
echo awkscript
head -5 script; echo 126 bytes...
echo big.output
head -5 output; echo 1659 bytes...
echo bigfiles
head -5 bigfiles; echo 125 bytes...
echo buckaroo
head -5 buckaroo; echo 270 bytes...
echo buckaroo.confused
head -5 buckaroo.confused; echo 458 bytes...
```

