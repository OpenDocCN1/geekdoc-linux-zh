
Crunch 的 `Charset.lst` 文件包含预定义为字母数字或符号字符串的关键字列表。我们可以使用这些关键字，这样就不必手动输入我们要使用的字符。该文件位于 `/usr/share/crunch` 目录中。如果我们查看该文件，我们可以看到可用的关键字集：

- ➤ `cd /usr/share/crunch`
- ➤ `cat charset.lst`

![](img/4a03f08556c51a14a3b88fe549a54ca8_60_0.png)

我们可以使用任何已定义的集合，例如：

- ➤ `sudo crunch 2 4 -f charset.lst mixalpha-numeric-all -o mixedall.txt`

`kali@kali:-/usr/share/crunch]`

```
$ sudo crunch 2 4 -f charset.lst minalpha-numeric-all -0 mixedall.txt
```

Crunch 将生成以下数据量：393732324 字节

375 MB

0 GB

0 TB

0 PB

Crunch 将生成以下行数：78914316

crunch: 输出生成进度 98%

crunch: 输出生成进度 100%

该命令创建了一个单词列表，该列表遍历包含所有字母、数字和符号的两到四个字符的单词。大多数网站要求新账户使用至少包含字母和数字组合的密码。因此，拥有包含这些组合的单词列表是一个良好的起点。

密码中出现数字串也是非常常见的。我经常看到长达 16 位数字的组合，与人物、地点或事物结合使用。你可以使用 crunch 生成一个数字范围的单词列表，如下所示：

```
sudo crunch 1 5 -f charset.lst numeric -o 1to5numbers.txt
```

Crunch 将生成以下数据量：654320

0 MB

0 GB

0 TB

0 PB

Crunch 将生成以下行数：111110

crunch: 输出生成进度 100%

这将创建一个包含一到五位数字的单词列表。单独使用它效果并不显著，但结合 Hashcat 的 Al 组合器攻击以及“Rock You”或 Ignis 列表使用时效果非常好。这会从单词列表中取一个词，并加入我们新生成的数字列表中的数字。

### CRUNCH：创建 Unicode 单词列表

许多语言包含扩展字符或 Unicode 字符。我们可以使用 Crunch 创建包含“Unicode”字符的单词列表。“mixalpha-space-sv”字符集包含其中一些字符。

如下所示：

`mixalpha-space-sv =`

`[abcdefghijklmnopqrstuvwxyzäöäABCDEFGH IJKLMNOPQRSTUVWXYZ`

`ÄÖ]`

我们可以使用此字符集来构建单词列表。

```
sudo crunch 3 5 -f charset.lst mixalpha-space-sv -o mixedall.txt
```

![](img/4a03f08556c51a14a3b88fe549a54ca8_62_0.png)

我们现在有了一个用于密码破解的混合字符列表。我们可以将此列表与之前的“1 到 5 位数字”列表结合，形成非常实用的组合。或者，我们可以在混合攻击中使用它，让 Hashcat 添加数字。

如下所示：

```
hashcat --remove -m 0 uncracked.txt -o cracked.txt -i -a6 mixedall.txt ?d?d?d?d -O
```

我们将在后续章节中深入介绍 Hashcat。目前，只需知道上述命令会取我们新创建的单词列表，并逐个在单词列表末尾添加一位十进制数字，依次递增。因此，第一次攻击路径会在单词末尾添加一个数字，第二次路径会在单词末尾添加两个数字，依此类推。

使用这种简单技术，我成功破解了未破解列表中大量的密码哈希。它破解了如下密码：

- NMWTÄ,,48
- hÅ«LlLo1995
- ËŸminÄY1311
- NickÅ«2501

我知道这些字母看起来有点不同，但这就是 Hashcat 显示 Unicode 字符的方式。在某些情况下这会很方便，但你可以使用破解程序中的规则和组合攻击来达到类似的效果。

### CRUNCH - 创建更高级的单词列表

![](img/4a03f08556c51a14a3b88fe549a54ca8_64_0.png)

在使用 crunch 创建单词时，我们可以使用多个字符集。人类是习惯和模式的生物，因此你在破解密码时会发现模式。你可以使用任何模式，通过 crunch 创建自定义单词列表。

简单来说，列出你想使用的每个字符集，然后使用“@ , % ^”字符创建掩码，就像在 Hashcat 中做的那样。“@”符号代表第一个字符集中的字符。“,”代表第二个，“%”代表第三个字符集，依此类推。然后使用“-t”模式开关来构建你的模式。

#### 警告：这可能会快速填满硬盘 – 你已被警告

是不是很困惑？让我们看一个例子：

```
sudo crunch 10 10 -f charset.lst mixalpha-space-sv symbols14-space ualpha -o mixedsymupper.txt -t @@,%%%
```

不要让这个命令运行超过几秒钟！它可能会生成一个巨大的文件。按"Ctrl-C"并查找"START"文件。

你应该会看到这样的单词：

aaa!!!#VVR

baa!!$#WUS

aba!*!#KTT

cab&!!)SSU

你应该能看到我们构建的模式：

- 3 个来自 `mixalpha-space-sv` 字符集的字母 (`@@@`)
- 4 个来自 `symbols14-space` 字符集的符号 (`,,,,`)
- 3 个来自大写字母字符集 (`%%%`)

很多时候，你会发现某个单词在密码哈希中被反复使用，比如公司名称。假设我们发现一串密码，包含虚构的公司缩写"WOW"，随后是 3 个符号、2 个大写字母和 5 个数字。

我们可以使用以下 Crunch 命令：

```
sudo crunch 13 13 -f charset.lst symbols14-space ualpha numeric -o special.txt -t WOW@@,,%%%%
```

再次，不要让它运行超过几秒钟，然后查看"START"输出文件。

- WOW!!!AB11910
- WOW!!!AB11911
- WOW!!!AB11912
- WOW!!!AB11913

Crunch 是一个功能强大的工具，拥有许多选项。如果你找不到满足需求的单词列表，就用 Crunch 构建它！我们只涉及了该工具的几个功能。还有额外的功能以及存储输出文件的不同方式 - 请参阅 crunch 手册以获取有用的示例。

### HASHCAT - 使用 HASHCAT 创建单词列表

许多 Hashcat 用户不知道，实际上可以使用 Hashcat 工具本身来创建单词列表。你可以使用任何标准的 Hashcat "-a" 攻击命令来生成单词列表。我们将在后续章节中介绍几种 Hashcat 攻击模式。因此，而不是逐步讲解这些步骤，我制作了一个图表，展示了一些常见用法：

| 命令 | 描述 | 示例输出 |
| :--- | :--- | :--- |
| `hashcat64 -a 3 -i ?d?d?d?d --stdout > numbers1-4.txt` | 创建如下单词： | 1111<br>1112<br>1123<br>1234 |
| `hashcat64 -i -a 6 FrenchWordlist.txt ?d?d?d?d --stdout > FrenchNumbers1-4.txt` | 创建如下单词： | chat1111<br>chat2222<br>chien1111<br>chien2222 |
| `hashcat64 --stdout wordlist.txt -r rules/toggles3.rule -o WordlistRules.txt` | 创建如下单词： | Admin<br>aDmin<br>adMin<br>admiN<br>admin |

再次强调，你可以使用任何你希望的 `"-a"` 攻击模式，只需确保使用 `"--stdout"` 开关。然后你可以使用 `"-o"` 指定输出文件，或者直接使用 `">"` 文件重定向命令。

### HASHCAT 工具

工具 GitHub：[https://github.com/hashcat/hashcat-utils](https://github.com/hashcat/hashcat-utils)

工具发布页：[https://github.com/hashcat/hashcat-utils/releases](https://github.com/hashcat/hashcat-utils/releases)
