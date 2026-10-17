
![](img/03e4d38bded7def6bb51288422c4f89d_47_0.png)

## `sed /[0-9]/no/g digits.txt`

![](img/03e4d38bded7def6bb51288422c4f89d_48_0.png)

`sed -n 7p sed_sample.txt`

`sed -n 5,12p sed_sample.txt`

对于一个只有几十行的文件，这个命令似乎毫无意义。但当你拥有一个例如包含数千万行的 CSV 文件，且 Excel 拒绝打开它，而你需要查看第 108100、999588、10009898 行的内容以确保数据格式正确时，它的真正威力就会显现出来。

你也可以将此结合起来，在给定的字符串范围内查找并替换单词或正则表达式：

## 问题 输出 端口 调试 控制台 终端

```
## And a Happy NewYeargit/Linux-for-OSINT-21-day/Day_7 (main) $ sed '1,30 s/Happy/Merry/g' sed_sample.txt
We wish you a Merry Christmas
We wish you a Merry Christmas
We wish you a Merry Christmas
And a Merry New Year!

Good tidings we bring to you and your kin,
We wish you a Merry Christmas
And a Merry New Year!

Oh, bring us some figgy pudding
Oh, bring us some figgy pudding
Oh, bring us some figgy pudding
And bring it right here!

Good tidings we bring to you and your kin,
We wish you a Merry Christmas
And a Merry New Year!

We won't go until we get some
We won't go until we get some
We won't go until we get some
So bring it right here!

Good tidings we bring to you and your kin,
We wish you a Merry Christmas
And a Merry New Year!

We all like-like our figgy pudding
```

![](img/03e4d38bded7def6bb51288422c4f89d_49_0.png)

更多示例可以在“Useful sed” Github 仓库（`https://github.com/adrianlarion/useful-sed`）中找到。

```
使用此工具生成 sed 命令，你可以在 Linux 或 Unix 机器上运行它。
```

![](img/03e4d38bded7def6bb51288422c4f89d_50_0.png)

不要试图记忆组合 Sed 命令的语法规则。你始终可以在 StackOverflow 上找到示例，向某些 AI 助手寻求帮助，或者使用特殊的在线服务如 Sed 命令生成器（`https://www.jamiebalafour/scot/devkit/sed/`）。

# AWK

`Awk` (`https://www.gnu.org/software/gawk/manual/gawk.html`) 是一种用于文本处理的脚本语言。有趣的事实是：`Awk` 并不是技术缩写，而是该语言三位开发者的字母组合：Alfred V. Aho, Peter J. Weiner 和 Brian W. Kernighan。

`Awk` 像 `Sed` 一样不需要安装，因为 Linux 默认包含它。

首先，让我们尝试显示文件的整个文本。使用 `Cat` 会更容易，但这个示例对于理解 `awk` 语法是必要的：

```
PROBLEMS OUTPUT PORTS DEBUG TERMINAL # zsh - dev_7
$home/mary/linux/08-21-day.php $1 '{print $1}'
$home/mary/linux/08-21-day.php $1 '{print $2}'
$home/mary/linux/08-21-day.php $1 '{print $3}'
$home/mary/linux/08-21-day.php $1 '{print $4}'
Title of the book: The British Edition,Gift of So,2016,1
Another title (1986,1880): The British Invention, Mary, eloquently written curatorial descriptions,John Doe,Gift of So,2016,1,repr
First image (2014): Terry, Mary,some other 2015,3
$home/mary/linux/08-21-day.php $1
awk '{print $0}' sample.txt
```

现在让我们做相同的操作，但带有行号：

![](img/03e4d38bded7def6bb51288422c4f89d_51_0.png)

```
awk '{print NR,$0}' sample.txt
```

让我们只显示文档的第一列和第三列（使用标志 `-F` 指明分隔符为逗号）：

![](img/03e4d38bded7def6bb51288422c4f89d_51_1.png)

```
awk -F, '{print $1,$3}' sample.txt
```

现在只输出以特定字符开头的字符串：

`example.csv | awk_sample.txt`

```
+,2016,1
1 Title,Identifier
Title of the book: The British Edition,Gift of So,2016,1
Another title (1986,1880): The British Invention, Mary, eloquently written curatorial descriptions,John Doe,Gift of So,2016,1,repr
First image (2014): Terry, Mary,some other 2015,3
```

# 第 8 天 Vim 文本编辑器

一个有趣的事实，如果你在 Google 中输入 "emacs"，搜索引擎会问你：“你是指 vi 吗？”（`vim` 是 `vi` 文本编辑器的改进版本，于 1976 年引入）。全球许多开发者都热爱 Vim，他们已经使用了几十年，并不断发现这个文本编辑器的某些惊人功能。

![](img/03e4d38bded7def6bb51288422c4f89d_54_0.png)

`Vim` (`https://www.vim.org`) - 是一款通用且高度可配置的命令行文本编辑器。它的第一个版本出现在 1991 年，尽管有许多其他文本编辑器和 IDE（集成开发环境）作为竞争对手，但它一直保持流行。让我们运行它，看看它擅长什么。

![](img/03e4d38bded7def6bb51288422c4f89d_55_0.png)

让我们来安装：

## `sudo apt update`

## `sudo apt install vim`
