
`% grep 'z*' /etc/passwd | head -5`

root:? :0:0:/:/bin/csh

news:? :6:11:USENET News:/usr/spool/news:/bin/ksh

ingres:*? :7:519:INGRES Manager:/usr/ingres:/bin/csh

usrlimit:? :8:800:(1000 user system):/mnt:/bin/false

vanilla:*? :20:805:Vanilla Account:/mnt:/bin/sh

结果与前一个命令的结果相同，但这并不奇怪。指定匹配零次或多次出现的模式将匹配每一行！指定只有包含一个或多个 `z` 的行是通过这种看起来奇怪的模式实现的：

```
% grep 'z*z*' /etc/passwd | head -5
```

marg:? :724:1233:Guyzee:/users/marg:/bin/ksh

ayy:? :1272:1224:martine:/users/ayy:/bin/csh

wizardz:? :1560:1375:Cz:/users/wizardz:/bin/ksh

zhq:? :2377:1318:Zihong:/users/zhq:/bin/csh

mmm:? :1527:133:Michael Kenzel:/users/mmm:/bin/ksh

### 5.
之前我发现 `/etc/passwd` 文件中有几行是未指定登录 shell 的账户。每行密码文件必须有一定数量的冒号，对于这些账户，行上的最后一个字符将是冒号，这是一个容易的 `grep` 模式，只要记住作为模式中的最后一个字符，`$` 表示行尾。并且不要忘记 `^` 作为模式中的第一个字符表示行的开头（与在集合记号中表示“非”或反转随后指定的模式的情况不同）。

以下是 `$` 记号在此上下文中的可能外观：

```
% grep ':$' /etc/passwd
```

charon:? :21:807:The Ferryman:/users/tomb:

lp:*? :70:10:System V LP Administration:/var/spool/lp:

### 6.
假设我接到会计的电话，需要找到一个包含关于花费 100 美元购买某款软件的消息的文件。结果发现，要找到该消息，我可以使用 `grep` 搜索所有包含美元符号、后跟 1、后跟一个或多个 0 的文件：

```
% grep '$100*' * /* 
```

Mail/bob_gale:      Unfortunately, our fees are currently $100 per test drive, budgets

Mail/dan_sommer:We also pay $100 for Test Drives, our very short "First Looks" section. We often

Mail/james:has been dropped, so if I ask for $1000 is that way outta line

Mail/john_spragens:time testing things since it's a $100 test drive: I'm willing to

Mail/john_spragens:      Finally, I'd like to request $200 rather than $100 for

Mail/mac:again: expected pricing will be $10,000 - $16,000 and the BriteLite LX with

Mail/mark:I'm promised $1000 / month for a first

Mail/netnews.postings: Win Lose or Die, John Gardner (hardback) $10

Mail/netnews.postings:I'd be willing to pay, I dunno, $100 / year for the space? I would

Mail/sent:to panic that they'd want their $10K advance back, but the good news is

Mail/sent:That would be fine. How about $100 USD for both, to include any

Mail/sent:      Amount: $100.00

匹配项相当多。请注意，在匹配项中包括了 `$1000`、`$10K` 和 `$10`。要匹配特定的值 `$100`，当然，我可以将 `$100` 作为搜索模式，后跟一个排除集：`$100[^0]`。

### Note

你可以使用 shell 不仅在当前目录中展开文件，还可以展开到子目录中更深一层：`*` 将你的搜索扩展到当前目录中的文件之外，而 `* /*` 将你的搜索扩展到当前点下方一层目录中的所有文件。如果你有大量文件，你有时可能会看到错误 `arg list too long`；这就是通配符达到其有用性极限的地方，而 `find` 命令（在第 22 小时“搜索信息和文件”中介绍）接管了。

该模式展示了 Unix 正则表达式的复杂性和潜在的混淆。例如，`$` 是一个特殊字符，可用于表示行的结尾，但只有在将其放在模式末尾时才有效。因为我没有将其放在模式末尾，所以 `grep` 程序正确地将其解释为 `$` 字符本身。

在正则表达式中可用的相对较少的记法下，你可以创建相当多样的复杂模式来在文件中查找信息。使用 `man grep` 了解更多信息。

## Task 8.7: The Rest of the grep Family

有时单个正则表达式无法定位你所寻找的内容。例如，也许你正在寻找匹配两种模式之一的行。这时 `egrep` 命令就派上用场了。该命令的名称源自“expression grep”，并且其记法比 `grep` 更强大，如表 8.4 所示。

| Notation | Meaning |
|---|---|
| c | Match the character c |
| \c | Force c to be read as the letter c, not as another meaning the character might have |
| ^ | Beginning of the line |
| $ | End of the line |
| . | Any single character |
| [xy] | Any single character in the set specified |
| [^xy] | Any single character not in the set specified |
| c* | Zero or more occurrences of character c |
| c+ | One or more occurrences of character c |

# TABLE 8.4 Regular Expression Notation for egrep

例如，你可能想要一个模式文件并调用一个 Unix 命令来搜索包含该文件中任何模式的行。这时 `fgrep`，或基于文件的 `grep`，命令就派上用场了。模式文件可以包含 `grep` 会理解的任何模式（这意味着不幸的是，你不能使用 `egrep` 中可用的额外记法），并通过 `-f file` 选项指定。

### 1.
我将搜索密码文件来演示 `egrep`。我之前用 `grep` 搜索包含一个或多个字母 `z` 的行的模式看起来有点奇怪：`\zz*`。使用 `egrep`，此搜索要容易得多：

```
% egrep 'z+' /etc/passwd | head -5
```

marg:? :724:1233:Guyzee:/users/marg:/bin/ksh

axy:? :1272:1233:martinez:/users/axy:/bin/csh

wizard:? :1560:1375:Oz:/users/wizard:/bin/ksh

zhq:? :2377:1318:Zihong:/users/zhq:/bin/csh

mm:? :7152:1233:Michael Kenzie:/users/mm:/bin/ksh

Broken pipe

### 2.
要搜索包含 `z` 或 `q` 的行，我可以使用以下命令：

```
% egrep '(z|q)' /etc/passwd | head -5
```

aaq:? :528:1233:Don Kid:/users/aaq:/bin/csh

abq:? :560:1233:K Laws:/users/abq:/bin/csh

marg:? :724:1233:Guyzee:/users/marg:/bin/ksh
