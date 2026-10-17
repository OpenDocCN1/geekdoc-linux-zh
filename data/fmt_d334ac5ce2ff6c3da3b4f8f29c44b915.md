
在命令模式下，`x` 命令删除光标下的字符。如果你连续按五次 `x`，你最终将得到：

```
Now is the time for all good women to come to the aid of the
party.
Afterwards, we'll go out for pizza and _
-
-
-
```

现在按 `a` 插入一些文本，紧接着按 `esc`：

```
Now is the time for all good women to come to the aid of the
party.
Afterwards, we'll go out for pizza and Diet Coke_
-
-
-
```

你可以使用命令 `dd` 删除整行（即，连续按两次 `d`）。如果你的光标在第二行，并且你输入 `dd`，

```
Now is the time for all good women to come to the aid of the
party.
-
-
-
```

要删除光标所在的单词，请使用 `dw` 命令。将光标置于单词 "good" 上，并输入 `dw`。

```
Now is the time for all women to come to the aid of the party.
-
-
-
```

### 3.12.5 修改文本

你可以使用 `R` 命令替换部分文本。将光标置于 "party" 的第一个字母上，并输入单词 "hungry"。

```
+ Now is the time for all women to come to the aid of the hungry_
-
-
-
```

使用 `R` 编辑文本与 `i` 和 `a` 命令非常相似，但 `R` 是覆盖文本而不是插入文本。

`r` 命令替换光标下的单个字符。例如，将光标移动到单词 "Now" 的开头，输入 `r` 后紧跟字母 `C`，你将得到：

```
+ Cow is the time for all women to come to the aid of the hungry.
-
-
-
```

`~` 命令可以将光标下字母的大小写从大写更改为小写，反之亦然。例如，如果你将光标置于上方 "Cow" 中的 "o" 上并反复按 `~`，你将得到：

```
+ COW IS THE TIME FOR ALL WOMEN TO COME TO THE AID OF THE HUNGRY_
-
-
-
```

### 3.12.6 移动命令

你已经知道如何使用方向键在文档中移动。此外，你可以使用 `h`、`j`、`k` 和 `l` 命令分别将光标向左、向下、向上和向右移动。当由于某种原因方向键无法正常工作时这非常方便。

`w` 将光标移动到下一个单词的开头；`b` 将其移动到上一个单词的开头。

`D`（数字零）将光标移动到当前行的开头，`$` 命令将其移动到行尾。

在编辑大文件时，你可能希望一次一屏地向后移动。按 `Ctrl-F` 将光标向前移动一屏，`Ctrl-B` 向后移动一屏。
