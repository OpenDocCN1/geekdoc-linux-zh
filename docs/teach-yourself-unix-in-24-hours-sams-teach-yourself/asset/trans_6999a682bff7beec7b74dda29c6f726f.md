

# 第 9 小

4. 我可以修改我的别名（alias），但要让引号正确显示简直是一场噩梦。
直接编写这个简单的 shell 脚本会容易得多：

```
% cat bin/wrongs
# wrongs - 显示文件中常见误用单词的列表

cat $* | \
awk '{for (i=1;i<=NF; i++) print $i}' | \
fgrep -F ".wrongs"
```

为了让它生效，我需要使用 C shell 别名删除现有的 `wrongwords` 别名，为 shell 脚本添加执行权限，然后执行 `rehash` 以确保 C shell 在被请求时能找到该命令：

```
% alias wrongwords
% chmod +x bin/wrongwords
% rehash
```

现在已经可以使用了：

```
% wrongwords sample3
insure
afect
```

5. `fgrep` 命令还可以从列表中排除单词。如果你一直在使用 `myspell` 命令，你会很地发现该程序对缩写词或你在写作中使用的某些其他拼写正确的单词一无所知。这时 `grep` 就能成为一个得力的爱国者了。列出一个你常用的、没有拼写错误但被报告为错误的单词列表：

```
% alias myspell '*spell\* | fgrep -v -f $HOME/.dictionary'
% cat $HOME/.dictionary
BBS:
FAX
Taylor
Utech
ygote
```

现在 `spell` 变得更有帮助了：

```
% spell newsample
FAX
illiterate
Literacy
letteracy
illiterate
Papert
pre
rithmetic
Rs
Taylor
Utech
ygote
% myspell newsample
illiterate
Literacy
```

# 通配符与正则表达式

letteracy
letterate
Papert
pre
rithmetic
Rs

你现在已经认识了整个 `grep` 命令家族。对于大多数信息搜索任务，你可以直接使用 `grep` 命令本身。不过，有时拥有选项会很棒，特别是当你决定像本节所解释的脚本和别名那样来自自定义某些命令时。

# 任务 9.7：使用 sed 在途中更改内容

我敢打赌，当你读到要学习某些 UNIX 编程工具时，你感到焦虑，手心出汗，也许手指在发抖，脑子里的小声音开始响道：“太晚了！我们可以用管道和纸笔！我们根本不需要电脑！”

不要慌。

如果你仔细想想，你所有的编程都在 UNIX 中完成。当你向 shell 输入命令时，你其实是在编写程序让 shell 立即执行指定的任务。当你指定文件重定向或构建管道（pipe）时，你实际上在编写一个小型 UNIX 程序，由 shell 解释并执行。坦率地说，考虑到你现在已经知道了多少命令，以及每个命令有多少种标志（flags），你已经拥有一套相当不错的编程工具了，所以继续前进吧！

由于 `|` 符号被称为管道（pipe），而连接的命令被称为流水线（pipelines），流经管道的信息是一个流（stream）也不奇怪了。例如，命令 `cat test | wc` 意味着 `cat` 打开文件 test 并将其流给 `wc`，后者计算行数、单词和字符数。

为了编辑、修改管道中的信息，使用一个流编辑器（stream editor）似乎是合理的，而这正是 `sed` 命令的作用！事实上，它的名字源于它的功能：s 代表 stream（流），ed 代表 editor（编辑器）。

以下是 `sed` 命令如何构建在旧编辑器 `ed` 之上的，就是那个负责 `grep` 命令的编辑器，记得吗？`global/regular expression/` 打印的内容正是 grep。它是 unix 自身的微模型，`sed` 命令之间用分号分隔。

有很多不同的 `sed` 命令，但为了遵守承诺不让你被没帮助的选项和变体淹没，我将专注于使用 `sed` 将一种模式替换为另一种，以及从文件中提取行范围。替换命令的通用格式为：`s/old/new/flags`，其中 `old` 和 `new` 是你要处理的模式，`s` 是 substitute（替换）命令的缩写，两个最有用的标志是 `g`（全局替换每行中的所有出现处）和 `n`（告诉 sed 替换模式的前 n 次出现）。默认情况下，行会列在屏幕上，因此像 `10q` 这样的 `sed` 表达式会导致程序列出前 10 行并退出（作为命令 `head -10` 的替代方案）。删除则是：命令前有一个或两个文件地址，反映了删除匹配特定地址的行或从第一到最后范围内的所有行的请求。

`sed` 命令的格式是 `sed`，后跟引号内的表达式，然后是可选用于读取输入的文件。

这里有一些示例：

- 1. 我将从一个示例开始。我将使用 `sed` 从 `/etc/passwd` 文件中提取一些行，然后将冒号替换为空格。此命令的格式是将每个出现的 `:` 替换为空格，即 `s/: / /`
% sed tailor :/etc/passwd | sed -e "s/: /g"
tailor?: 1048:1375:Mary Tailor:/users/tailor:/bin/csh
tailor?: 769:1375:Mary Tailor:/users/tailor:/usr/local/lib/tcsh
tailor?: 375:3518:David Tailor:/users/tailor:/usr/local/lib/tcsh
tailor?: 203:1022:James Tailor:/users/tailor:/bin/csh
tailor?: 662:1042:Robert Tailor:/users/tailor:/bin/csh
tailor?: 869:1508:Melanie Tailor:/users/tailor:/bin/csh
tailor?: 1989:1412:David Tailor:/users/tailor:/bin/csh

这并没有达到我的效果，因为我需要为 `sed` 命令添加全局指令以确保替换每行的所有出现处。我这次尝试在指令中添加一个 `g`。

```
% sed tailor :/etc/passwd | sed -e "s/: /g"
tailor?: 1048:1375:Mary Tailor:/users/tailor:/bin/csh
tailor?: 769:1375:Mary Tailor:/users/tailor:/usr/local/lib/tcsh
tailor?: 375:3518:David Tailor:/users/tailor:/usr/local/lib/tcsh
tailor?: 203:1022:James Tailor:/users/tailor:/bin/csh
tailor?: 662:1042:Robert Tailor:/users/tailor:/bin/csh
tailor?: 869:1508:Melanie Tailor:/users/tailor:/bin/csh
tailor?: 1989:1412:David Tailor:/users/tailor:/bin/csh
```

- 2. 替换的一个更复杂的示例是将所有的 `Tailor` 替换为 `Taylor`：

```
% sed tailor :/etc/passwd | sed -e "s/Tailor:/g"
tailor?: 1048:1375:James:/users/tailor:/bin/csh
tailor?: 769:1375:Mary:/users/tailor:/usr/local/lib/tcsh
tailor?: 375:3518:David:/users/tailor:/usr/local/lib/msh
tailor?: 203:1022:James:/users/tailor:/bin/csh
tailor?: 662:1042:Robert:/users/tailor:/bin/csh
tailor?: 869:1508:Melanie:/users/tailor:/bin/csh
tailor?: 1989:1412:David:/users/tailor:/bin/csh
```

