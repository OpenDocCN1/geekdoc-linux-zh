

你的 shell，但现在你知道怎么做了，如果有必要的话。

最后一点说明：C shell 也要求大多数人去调整环境变量。 在 .cshrc 中查找 set history=200 或 set savehist=200（不过更好的替代方案是直接切换到 bash）。

## Task 14.2: Using History to Cut Down on Typing

处理历史列表主要有三种机制。 你可以通过命令编号、命令的前几个字符来指定之前的命令，或者，如果你设置了命令编辑参数，可以在命令行上交互式地操作。

非交互式历史命令以感叹号开头。 例如，如果你输入的第 33 个命令是 who 命令，你就可以通过其命令编号来执行它：在命令提示符下输入 !33。 你也可以通过输入命令的一个或多个字符来执行它：!w、!wh 或 !who。 不过要小心：最近的匹配项会在没有确认的情况下被调用，所以如果你输入了 who，但在之后输入了一个名为 wipeout 的 rm 命令别名，那么 !w 序列匹配到的会是后者，而 !wh 或 !who 匹配到的才是前者。

一个非常有用的简写是 !!，它会重复最近执行的命令。 还有两个有价值的历史引用需要了解：!$ 扩展为前一个命令的最后一个词（这很有意义，因为 $ 总是指向某物的末尾，无论是行、文件还是在这种情况下的命令），而 !* 扩展为前一个命令中除第一个词之外的所有词。 所以，例如，如果我输入命令 ls /usr /etc /dev，然后立即输入 echo !*，它会自动扩展为 echo /usr /etc /dev。

- 1. 首先，我需要花几分钟时间通过运行各种命令来建立一个历史列表：

Click here to view code image

```
$ cat buckaroo
I found myself stealing a peek at my own watch and overhead
General Catbird’s
aide give him the latest.
“He’s not even here,” went the conversation.
“Who?”
“Banzai.”
“Where the hell is he?”
“At the hospital in El Paso.”
“What? Why weren’t we informed? What’s wrong with him?”
$ who
taylor     tty p0  May  1 11:50  (198.76.82.151)
$ date
Sat Mar  7 13:26:26 MST 2015
$ echo $HISTSIZE $HOME
500 /home/taylor
$
```

- 2. 现在我将检查我的历史列表，看看有哪些命令被保存起来以备后用：

```
% history 10
```

```
310 echo $HISTFILESIZE
311 who
312 ls
313 vi buckaroo
314 cat buckaroo
315 who
316 date
317 echo $HISTSIZE $HOME
318 history 10
```

### 3. 要重复 date 命令，我可以指定其命令编号：

Click here to view code image

```
% !316
date
Sat Mar  7 13:26:38 MST 2015
```

注意 shell 显示了我输入的命令为命令编号 316（date），然后执行了它。 这里的 ksh 等价写法是 r 316。

### 4. 重复的第二种方法——一种更简单的方法——是指定命令的第一个字母：

Click here to view code image

```
% !w
who
taylor  tty p0  Feb  1 11:50  (198.76.82.151)
```

### 5. 现在看一下历史列表：

```
% history 10
314 cat buckaroo
315 who
316 date
317 echo $HISTSIZE $HOME
318 history 10
319 cat buckaroo
320 date
321 who
322 history 10
```

通过历史机制扩展的命令会以扩展后的命令形式存储，而不是实际输入的历史重复序列。 因此，这就违背了历史机制总是显示之前输入内容的 earlier 规则。 然而这是一个非常有帮助的例外！

历史命令对于从事软件程序开发的人来说非常有帮助。 程序员重复的最常见循环是编辑-编译-运行，反复进行。 Unix 程序员最常使用的命令可能看起来像 vi test.c、cc -o test test.c 和 ./test，分别用于编辑、编译和运行程序。 使用 shell 历史机制，程序员可以轻松输入 !v 来编辑文件，!c 来编译它，然后 !. 来测试它。 随着命令变得越来越长和复杂，这个功能就越发有用。

- 6. 是时候稍微试验一下文件通配符了：

Click here to view code image

