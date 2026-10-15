
这就是 -i（忽略大小写）选项能派上用场的地方：

点击此处查看代码图片

```
% grep -i owl testme
Archives/               OWL/                keylime.pie
```

3. 在接下来的几个示例中，我将进入 /etc 目录，因为那里的文件有很多行。在我使用的一个系统上，/etc/passwd 文件有将近 4,000 行：

```
% cd /etc
% wc -l /etc/passwd
3877
```

我的账户是 taylor。我将使用 grep 查看密码文件中我的账户条目：

点击此处查看代码图片

```
% grep taylor /etc/passwd
taylorj::?1048:1375:James Taylor:/users/taylorj:/bin/csh
mtaylor::?760:1375:Mary Taylor:/users/mtaylor:/usr/local/bin/tcsh
dataylor::?375:518:David Taylor:/users/dataylor:/usr/local/lib/msh
taylorjr::?203:1022:James Taylor:/users/taylorjr:/bin/csh
taylorrj::?668:1042:Robert Taylor:/users/taylorrj:/bin/csh
taylorm::?862:1508:Melanie Taylor:/users/taylormx:/bin/csh
taylor::?1989:1412:Dave Taylor:/users/taylor:/bin/csh
```

4. 如你所见，许多账户都包含 taylor 模式。

你可以使用管道命令 grep taylor /etc/passwd | wc -l 算出有多少账户，对吧？

一种更聪明的做法是使用 grep 的 -c 选项来查看 taylor 模式出现的频率，它会告诉你文件中有多少处匹配：

```
% grep -c taylor /etc/passwd
7
```

该命令找到了七处匹配。数一下第3步输出列表中的匹配项来确认这一点。

5. 密码文件是一个记录 Unix 系统上每个用户基本账户信息的管理文件，其中有 3,877 行。看看所有 Taylor 账户是否大约同时开设会很有趣。（这大概意味着它们都出现在文件中大致相同的位置。）为此，我将使用 -n 选项为输出行编号：

点击此处查看代码图片

```
% grep -n taylor /etc/passwd
319:taylorj::?1048:1375:James Taylor:/users/taylorj:/bin/csh
1314:mtaylor::?760:1375:Mary Taylor:/users/mtaylor:/usr/local/bin/tcsh
1419:dataylor::?375:518:David Taylor:/users/dataylor:/usr/local/lib/msh
1547:taylorjr::?203:1022:James Taylor:/users/taylorjr:/bin/csh
1988:taylorrj::?668:1042:Robert Taylor:/users/taylorrj:/bin/csh
2133:taylorm::?8692:1508:Melanie Taylor:/users/taylormx:/bin/csh
3405:taylor::?1989:1412:Dave Taylor:/users/taylor:/bin/csh
```

grep 命令会添加行号、冒号以及该行的实际内容，在本例中这相当令人困惑，因为匹配的行也使用冒号来分隔行内的信息。通常，行号后跟冒号没问题，但在 passwd 文件中（已经满是冒号），这就让人摸不着头脑了。

你可以看出，我关于 Taylor 们何时开设账户的理论是错误的。如果账户在 passwd 文件中的位置接近意味着它们是在相近时间分配的，那么没有任何 Taylor 账户是在同一周内开设的。

这些有关如何使用 grep 的例子，只是触及了这个强大而精妙的命令所能做的事情的皮毛。使用 grep 在自己的文件系统中搜索特定模式，探索一下吧。

# 注意

掌握了通配符之后，你现在可以试试 grep 的 -l 选项。还记得吗，这个选项会列出包含指定模式的文件名，而不是打印匹配的行。如果我进入我的电子邮件归档目录——Mail——我可以很容易地使用命令 grep -l -i chicago Mail/* 生成一个文件夹列表，这些文件夹包含不区分大小写的模式 chicago。试试使用 grep -l 搜索你主目录中的所有文件，查找单词或模式。

# 任务8.6：创建正则表达式

正则表达式可以简单到像 acme 这样一个字母一个字母地匹配的单词，也可以复杂到像 (^ [a-zA-Z] | :wi) 这样，它匹配所有以大写或小写字母开头的行，或者包含 :wi 的行。

正则表达式的语言充满了以非常规方式使用的标点符号和字母。重要的是要记住，正则表达式不同于 shell 通配符模式。遗憾的是，事实确实如此。例如，在 C shell 中，a * 会列出所有以字母 a 开头的文件。正则表达式不是左锚定的，这意味着如果你只想匹配以字母 a 开头的行，就需要指定 ^a。shell 模式 a * 只匹配以字母 a 开头的文件名，而 * 在作为正则表达式的一部分时有着完全不同的解释：a * 是匹配字母 a 出现零次或多次的模式。正则表达式的符号如表8.3所示。egrep 命令还有额外的符号，你很快将学到。
