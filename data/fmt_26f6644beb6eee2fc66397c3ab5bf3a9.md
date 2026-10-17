
I think the new neighbors are getting a new heat pump

字符串 `"air"` 被字符串 `"heat"` 替换。文本替换是 `sed` 最简单的功能之一，也是它大部分时间的使用用途，因为它的力量和特性在这里真正脱颖而出。

## 基础 GNU 和 Unix 命令

> 重要的是要意识到 `sed` 不是交互式编辑器。当你给它命令时，它通过扫描每一行来工作。如果发现匹配项，它就会进行更改。例如，假设你想将 `"new"` 更改为 `"old"`：

```bash
$ echo I think the new neighbors are getting a new air pump | 
  sed 's/new/old/'
```

输出变为：

I think the old neighbors are getting an old air pump

搜索短语的第二次出现没有更改，因为 `sed` 已完成处理。如果你想更改行中的所有出现项，必须在命令末尾使用 `"g"` 使其全局：

```bash
$ echo I think the new neighbors are getting a new air pump | 
  sed 's/new/old/g'
```

输出变为：

I think the old neighbors are getting an old air pump

全局参数使 `sed` 继续搜索剩余行，直到到达行尾。这处理了同一短语的多次出现。如果你想更改多个值，可以在命令行上通过 `-e` 选项来标记每个命令。例如：

```bash
$ echo I think the new neighbors are getting a new air pump | 
  sed -e 's/new/old/' -e 's/air/heat/'
```

输出变为：

I think the old neighbors are getting an old heat pump

第二种方法是将所有的替换标准放在文件中，然后使用 `-f` 选项调用该文件。以下示例假设 `wishlist2` 存在：

```bash
$ cat wishlist2
s/line/phrase/
s/short/long/
```

```bash
$ echo this line is shorter | sed -f wishlist2
this phrase is longer
```

产生相同的结果，但使用文件存储命令使得在需要更改标准时变得容易得多，便于跟踪你正在执行的操作并在稍后重新运行这些命令。

### 限制行

如果你有一个大文件，你可能不想编辑整个文件，而是只编辑某些行。和其他所有事情一样，你有多种方法可以解决这个问题。第一种方法是指定一个搜索子句，仅在找到搜索短语时进行替换。搜索短语必须在操作之前并括在斜杠之间：`/search phrase/` `{operation}`

#### 基础 GNU 和 Unix 命令 第 3 章

例如，假设你有一个名为 `tuesday` 的文件：

- one 1
- two 1
- three 1
- three 1
- two 1
- one 1

你希望显示的最终结果为

- one 1
- two 2
- three 3
- three 3
- two 2
- one 1

在这种情况下，搜索的应该是单词 `two`。如果找到了，则将任何 `1s` 转换为 `2`。同样，还应该搜索单词 `three`，并将任何 `1s` 转换为 `3`：

```
$ cat wishlist3
/two/ -s/1/2/
/three/ -s/1/3/
$
$ sed -f wishlist3 tuesday
one 1
two 2
three 3
three 3
two 2
one 1
$
```

> 从设计上讲，`sed` 仅更改显示的值，而不更改原始文件中的值。为了保留更改结果，你必须将输出重定向到文件，如下所示：

```
sed -f wishlist3 tuesday > wednesday
```

有时，指定的动作不应基于搜索，而是纯粹基于行号。例如，你可能只想更改文件的第一行、前 10 行或任何组合。在这种情况下，你可以使用此语法指定行范围：

### 第一行，最后一行

要将前五行中的所有非“one”的内容更改为该值，请使用此示例：

```
$ cat wishlist4
1,5 s/two/one/
1,5 s/three/one
$
$ sed -f wishlist4 tuesday
one 1
one 1
one 1
one 1
one 1
one 1
$
```

### 打印

`sed` 的默认选项仅是打印。如果你没有提供任何参数，整个文件将显示出来，而不会发生任何真正的编辑。唯一的例外是 `sed` 必须始终有一个选项或命令。如果你只是在 `sed` 之后提供一个文件名而什么都不加，它会将其误解为命令。

你可以给它一个要显示的行数，后面跟 `q` 命令（代表退出），并查看任何文件的内容。例如 `sed 75000q /usr/share/dict/words` 将显示所有的单词文件，因为文件中的行数远少 75,000。如果你只想看前 60q，可以使用 `sed 60q /usr/share/dict/words`。

默认操作的反面或相反对的操作是 `-n` 选项。它可以防止正常工作的行被显示。例如 `sed -n 75000q /usr/share/dict/words` 将什么都不显示。尽管对于一个旨在显示数据的工具来说，防止显示数据的选项似乎很愚蠢，但它实际上是一件很妙的事情。不过，为了方便理解，你必须知道 `p` 命令的存在，它被用于强制打印（默认选项）。

#### 第 3 章

在较早的示例中，`tuesday` 文件中的数字更改以匹配它们的字母对应项。文件中的某些行已经是正确的，不需要更改。如果行没有被更改，你真的需要看到它们的输出吗——或者你只对被更改的行感兴趣？如果是后者，以下内容将显示那些条目：

```
$ cat wishlist5
/two s/1/2/p
/three/ s/1/3/p
$
sed -nf wishlist5 tuesday
two 2
three 3
three 3
two 2
$
```

要只打印文件的第 200 到 300 行（不发生实际编辑），命令变为 `sed -n '200,300p' /usr/share/dict/words`。

### 删除

`d` 命令用于指定删除。与所有的 `sed` 操作一样，行仅从显示中删除，而不从原始文件中删除。语法始终是：

> `{specification}` `d`

使用此示例删除所有包含 `"three"` 的行：

```
$ sed '/three/ d' tuesday
one 1
two 1
one 1
$
```

删除第 1 到 3 行，尝试这个：

```
$ sed '1,3 d' tuesday
three 1
two 1
one 1
$
```

> 在所有情况下，`d` 命令强制删除整行。你不能使用此命令删除行的一部分或一个单词。如果你想删除一个单词，将其替换为空：

```
sed 's/word//'
```

### 追加文本

可以使用命令将字符串追加到显示中。追加总是将字符串放在指定行的末尾——其他行之后。例如，为了将“The End”作为显示的最后一行，命令将是：

```
$ '$a\
The End\' tuesday
one 1
two 1
three 1
two 1
one 1
The End
$
```

美元符号 (`$`) 用于指定文件的结束，而反斜杠 (`\`) 用于换行。如果命令中缺少美元符号，文本将追加到每行之后：

```
$ 'a\
The End\' tuesday
one 1
The End
two 1
The End
three 1
The End
two 1
The End
one 1
The End
```

如果你想在特定行之后追加字符串，在命令中添加行号：

## 基础 GNU 和 Unix 命令 第 3

## 给智者的建议

在使用 `sed` 并执行多个更改、替换或删除操作时，必须小心指定执行操作的顺序。使用使用的 `tuesday` 文件示例，假设编号有误。你想将所有的 `ones` 变成 `twos`，所有的 `twos` 变成 `threes`，所有的 `threes` 变成 `fours`。这里有一种处理方法以及它生成的结果：

```
$ cat wishlist7
s/one/two/
s/two/three/
s/three/four/
$
sed -f wishlist7 tuesday
four 1
```

#### 第 3 章

基础 GNU 和 Unix 命令

four 1

four 1

four 1

four 1

结果既不是预期的，也不是想要的。因为 `sed` 会遍历整个文件并执行第一个操作，它会将文件更改为 `two 1-three 1-three 1-two 1-two`。之后，`sed` 会再次遍历文件以执行第二个操作。这导致文件变为 `three 1-three 1-three 1-three`。
