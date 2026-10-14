
这会在当前目录和所有子目录中搜索以 `.txt` 结尾的文件。之前的搜索找到以 `.txt` 结尾的项，但不包括 `.TXT` 或其他变体。要进行不区分大小写的搜索，请使用 `-iname` 而不是 `-name`。你可以可选地在 `-name` 参数之前指定搜索起点，如下：

```
matthew@seymour$: find -iname "*.txt"
```

另一个实用的参数是 `-size`，它允许你指定文件的大小。你可以使用 `+` 表示大于或使用 `-` 表示小于。例如：

```
matthew@seymour$: find -size +10M
```

`-perm` 参数允许你搜索具有特定权限的文件。你可以使用与 `chmod` 相同的表示法。例如：

```
matthew@seymour$: find -perm 644
```

`-user` 参数允许你搜索由特定用户所有的文件。例如：

```
matthew@seymour$: find -user matthew
```

`-group` 参数允许你搜索由特定组所有的文件。例如：

```
matthew@seymour$: find -group staff
```

`-type` 参数允许你搜索特定类型的文件，例如目录或文件。例如：

```
matthew@seymour$: find -type d
```

`-maxdepth` 参数允许你限制搜索递归的深度。例如：

```
matthew@seymour$: find -maxdepth 1
```

`-exec` 参数允许你对找到的每个文件执行命令。例如：

```
matthew@seymour$: find . -name "*.txt" -exec rm {} \;
```

`-name` 参数允许你根据文件名搜索文件。例如：

```
matthew@seymour$: find -name "*.txt"
```

`-iname` 参数允许你根据文件名搜索文件（不区分大小写）。例如：

```
matthew@seymour$: find -iname "*.txt"
```

`-mtime` 参数允许你搜索最近修改的文件。例如：

```
matthew@seymour$: find -mtime -7
```

`-atime` 参数允许你搜索最近访问的文件。例如：

```
matthew@seymour$: find -atime -1
```

`-ctime` 参数允许你搜索最近更改过状态的文件。例如：

```
matthew@seymour$: find -ctime -1
```

`-content` 参数允许你搜索包含特定字符串的文件。例如：

```
matthew@seymour$: find -content "search"
```

要查找其他用户不可读的文件，可以使用 `-not` 条件，如下：

```
mathew@semour:-$ find /home -not -perm +o=r
```

现在，我们来看 `find` 命令最高级的：`-exec` 参数。它允许你在每次匹配到项时执行一个外部程序，并在你任何需要的地方传递匹配到的文件名。你的命令及其参数应该紧跟在 `-exec` 之后，并以 `\;` 结束。你可以使用 `{}`（一对并排的左括号和右括号）在任何位置插入文件名。

因此，你可以匹配系统中所有的文本文件（即在我们之前的示例中是递归的 `/` 而不是 `/home`）、大于 10KB、由 mathew 所有且其他用户不可读的文件，并使用 `chmod` 启用读取权限，如下：

```
mathew@semour:-$ find -name "*.txt" -size +10k -user mathew -not \
+ -exec chmod r {} \;
```

当你输入自己的 `-exec` 参数时，请务必在 `\;` 之前包含一个空格。否则，你可能会看到错误，提示 `'.exec'` 缺少参数。

你现在知道为什么有些人认为 `find` 命令很智能了吗？很多人只学会了 `find` 的基础用法并进行简单的操作，但希望如果你给它一个机会，你会发现它能做很多事情。

## 使用 grep 在输入中搜索字符串

`grep` 命令和 `find` 一样，用得当就是极其强大的搜索工具。不过，`grep` 处理任何文本，无论是文件内容还是标准输入。

`grep` 的基本用法是：

```
mathew@semour:-$ grep "some text" *
```

这会在当前目录（但不包括子目录）的所有文件中搜索该字符串，并打印文件名以及匹配的行。要在子目录中启用递归搜索，使用 `-r` 参数，如下：

```
mathew@semour:-$ grep -r "some text" *
```

文件中的每个字符串匹配项都会打印出文件名和匹配内容。如果一个文件包含多个匹配项，每个匹配项都会被打印。你可以通过 `-l` 参数（小写 L）更改这种行为，它会强制 `grep` 只打印包含至少一个匹配项的文件名，而不打印匹配的文本。如果一个文件包含多个匹配项，它也只显示一次。或者，`-c` 参数会打印每个被搜索的文件名并在结尾包含匹配项的数量，即使没有匹配项也是如此。

在指定要搜索的模式时，你有很大的控制权。你可以像之前那样指定一个简单的字符串（如 `some text`），也可以通过指定 `-v` 参数来反转匹配。例如，这会返回 `myfile.txt` 中不包含 `hello` 单词的所有行：

```
mathew@semour:-$ grep -v "hello" myfile.txt
```

你还可以使用正则表达式作为搜索词。例如，你可以使用此命令搜索 `myfile.txt` 中对 `cat`、`sat` 或 `mat` 的所有引用：

```
mathew@semour:- grep "[cmas]" myfile.txt
```

添加 `-i` 参数来忽略大小写，匹配 `Cat`、`CAT`、`MaT` 等：

```
mathew@semour:-$ grep -i [cmas] myfile.txt
```

输出也可以通过 `-n` 和 `--color` 参数在一定程度上得到控制。第一个告诉 `grep` 为每个匹配项打印行号，即它在源文件中的位置。`--color` 参数告诉 `grep` 在输出中为搜索词着色，帮助它们在行的所有其他文本中脱颖而出。你可以使用 `GREP_COLOR` 环境变量来选择所需的颜色：`export GREP_COLOR=36` 提供青色，`export GREP_COLOR=32` 提供柠檬绿。

下一个示例使用这两个参数对上一个命令的所有匹配项进行编号和上色：

```
mathew@semour:-$ grep -in --color [cmas] myfile.txt
```
