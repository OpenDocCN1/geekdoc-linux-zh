
# 修改行

正如你所记得的，`sed` 中有五种修改命令（`i`, `a`, `c`, `d`, `D`）。我们将向你展示如何在 `awk` 中模拟其中一些命令，并将其余下部分留作练习题。

# 插入行

插入命令（`i`）可以很容易地使用 `print` 语句来模拟，在打印特定的某行或一组行之前打印文本。当定位到地址时，就会执行操作并插入行。代码位于第 12.50 节。

## 第 12.50 节 使用 sed 和 awk 插入文本

| sed |
| :--- |
| $ `sed -f addLines.sed 5lines.dat` |
| `3i\` |
| This is text! |
| to be added |
| 输入: | 输出 |
| line 1 | line 1 |
| line 2 | line 2 |
| line 3 | This is text |
| line 4 | to be added |
| line 5 | line 3 |
| | line 6 |
| | line 5 |
| awk |
| `awk -f addLines.awk 5lines.dat` |
| `#addLines.awk` |
| `NR = 3 (print $0)` |
| `NR == 3 (print "This is text"; print "to be added"; print $0)` |
| 输入: | 输出 |
| line 1 | line 1 |
| line 2 | line 2 |
| | This is text |
| | to be added |
| | line 3 |
| | line 4 |
| | line 5 |

# 删除行

我们可以很容易地使用 `awk` 脚本模拟 `sed` 的删除命令（`d`）。注意，`awk` 脚本的逻辑要求我们指定想要保留的行（`print`），而不是想要删除的行。代码位于第 12.51 节。

## 第 12.51 节 使用 sed 和 awk 删除文本

| sed |
| :--- |
| `sed '2,4d' 5lines.dat` |
| 输入: | 输出 |
| line 1 | line 1 |
| line 2 | line 5 |
| line 3 | |
| line 4 | |
| line 5 | |
| awk |
| $ `awk 'NR < 2 || NR > 4 ( print $0)' lines.dat` |
| 输入: | 输出: |
| line 1 | line 1 |
| line 2 | line 2 |
| line 3 | |
| line 4 | |
| line 5 | line 5 |

# 替换

要替换文本，`sed` 使用替换命令（`s`）；而 `awk` 使用函数。我们可以很容易地使用 `awk` 中的 `sub` 函数来进行替换。该概念在第 12.52 节。

## 第 12.52 节 使用 sed 和 awk 替换文本

| sed |
| :--- |
| $ `sed '3s/line/order/' 5lines.dat` |
| 输入: | 输出: |
| line 1 | line 1 |
| line 2 | line 2 |
| line 3 | order 3 |
| line 4 | line 4 |
| line 5 | line 5 |

```
$ awk -f sub.awk 5lines.dat

# sub.awk 脚本

{

  if (NR == 3)

    sub (/line/, "order")

  print $0

}
```

| 输入: | 输出: |
| line 1 | line 1 |
| line 2 | line 2 |
| line 3 | order 3 |
| line 4 | line 4 |
| line 5 | line 5 |

# 转换

`sed` 转换命令（`y`）在 `awk` 中没有直接实现。

# 下一个命令

`sed` `next`（`n`）可以使用 `getline` 操作直接模拟（详见第 446 页的 Next）。`sed` `append next` 命令（`N`）在 `awk` 中是不被支持的，因为它不支持多行缓冲区。

# 打印命令

`sed` `print` 命令（`p`）可以直接使用 `awk` `print` 命令重写。然而，`sed` 打印第一行命令（`P`）无法直接模拟，因为 `awk` 不支持多行缓冲区。

# 列表命令

`list` 命令（`l`）无法通过 `awk` 模拟。

# 文件

# 读取命令

`sed` `read` 命令（`r`）可以使用 `awk` `getline` 操作直接模拟。但记住，使用 `getline` 读取文件只会读取文件的下一行。要读取多行，必须使用循环。

# 写入命令

`sed` `write` 命令（`w`）可以使用 `awk` `print` 命令直接模拟。

# 分支

`awk` 工具没有与 `sed` 分支（`b`, `t`）和标签（`:`）命令对应的命令。

# 退出

`sed` 退出命令的 `awk` 等命令是 `exit`。第 12.53 节演示了如何在这两个工具中单步执行脚本。

```
$ sed '4q' 71lines.dat
```
| 输入: | 输出: |
| line A | line A |
| line B | line B |
| line C | line C |
| line D | line D |
| line E | | |
| line F | | |
| line G | | |

```
$ awk '{ if (NR > 4) exit; else print $0}' 71lines.dat
```
