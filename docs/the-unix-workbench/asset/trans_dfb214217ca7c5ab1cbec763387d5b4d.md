

## 练习

- 1. 在你的主目录下创建一个名为 `message.txt` 的文件，并将其移动到另一个目录中。
- 2. 将你刚移动的 `message.txt` 复制到你的主目录中。
- 3. 删除两个 `message.txt` 副本。尝试不要使用 `rm`。

## 使用 Unix

知之非难，行之惟难。——中国谚语

### 自学

到目前为止，我们讨论过的每个命令都有详尽的文档，你可以使用 `man` 命令查看它们的文档，`man` 的第一个参数是你想了解的命令。让我们来看看 `ls` 的文档：

```
man ls
```

```
LS(1)                 BSD General Commands Manual

LS(1)

NAME
    ls -- list directory contents

SYNOPSIS
    ls [-ABCFGHLOPRSTUW@abcdefghiklmopqrstuwx1] [file ...]

DESCRIPTION
    For each operand that names a file of a type other than directory, ls
    displays its name as well as any requested, associated information.
    For each operand that names a file of type directory, ls displays the
    names of files contained within that directory as well as any requested,
    associated information.
```

浏览 man 页面的操作与 `less` 相同。我经常使用 man 页面来快速搜索我忘记的选项。假设我忘记了如何让 `ls` 打印长列表。在输入 `man ls` 打开页面后，键入 `/` 开始搜索。然后输入你要搜索的单词或短语；本例中，输入 `long list`，然后按回车。页面跳转到该条目：

```
-l      (The lowercase letter `ell'.)  List in long format. (See below.)
        If the output is to a terminal, a total sum for all the file sizes is
        output on a line before the long listing.
```

按下 `n` 键搜索下一个匹配项，如果要跳到上一个匹配项，输入 Shift + n。这种搜索方法也适用于 `less`。当你看完一个 man 页面后，输入 `q` 返回提示符。

当你知道要查找哪个命令时，`man` 命令非常好用，但如果你忘记了要找的命令名怎么办？你可以使用 `apropos` 搜索所有可用的命令及其描述。例如，假设我忘记了我最喜欢的命令行文本编辑器的名字。你可以在命令行中输入 `apropos editor`，它会打印一份结果列表：

```
apropos editor

ed(1), red(1)              - text editor
nano(1)                    - Nano's ANOther editor, an enhanced free Pico clone
sed(1)                     - stream editor
vim(1)                     - Vi IMproved, a programmers text editor
```

第二个结果是 `nano`，这个名字刚才就在我嘴边！当只需按几下键盘就能完成搜索时，`man` 和 `apropos` 都很有用，但如果你需要查找详细的示例和解释，在可以访问网页浏览器的情况下，最好使用搜索引擎。

### 小结

- 使用 `man` 查看命令的文档。
- 如果你想不起命令的名称，使用 `apropos` 搜索与该命令相关的单词。
- 如果你可以访问网页浏览器，使用搜索引擎可能比 `man` 或 `apropos` 更好。

### 练习

- 1. 使用 `man` 查找 `ls` 中用于人类可读输出的选项。

```
2017-01-02-hiking01.jpg
2017-01-02-hiking02.jpg
2017-02-10-hiking01.jpg
2017-02-10-hiking02.jpg
```

只列出了以 “2017” 开头的文件！命令 `ls 2017*` 的字面意思是：列出以 “2017” 开头后跟零个或任意多个字符的文件。可以想见，使用通配符是处理名称相似文件组的强大工具。

让我们再看几个使用星号通配符的例子。我们可以只列出以 “2016” 开头的照片：

```
ls 2016*
```

```
2016-06-20-datasci01.png
2016-06-20-datasci02.png
2016-06-20-datasci03.png
2016-06-21-lab01.jpg
2016-06-21-lab02.jpg
```

我们可以只列出文件名以 `.jpg` 结尾的文件：

```
ls *.jpg
```

