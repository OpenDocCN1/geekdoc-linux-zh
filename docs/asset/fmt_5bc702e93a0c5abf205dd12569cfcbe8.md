
```
$ grep bash /etc/passwd
root:x:0:0:root:/bin/bash
user:x:1001:1001:User,,,/home/user:/bin/bash
```

### -i

搜索不区分大小写

### -r

递归搜索（它搜索给定目录及其子目录中的所有文件）

### -c

统计匹配项的数量

### -V

反转匹配，打印不匹配搜索词的行

### -E

开启扩展正则表达式（某些更高级的元字符如 `|`, `*`, `+`, `?` 需要它）

`grep` 有许多其他实用的选项。请查看 `man page`（帮助手册）以获取更多信息。

### 正则表达式

第二个工具非常强大。它被用于描述文件中的文本，也称为正则表达式。正则表达式通过构建模式，从文本文件中提取数据非常有用。它们通常在脚本中，或者在用高级级语言（如 `Perl` 或 `Python`）进行编程时使用。

在使用正则表达式时，记住每个字符都至关重要，模式的编写目的是匹配特定的字符序列，这被称为字符串。模式使用普通的 ASCII 符号，如字母、数字、标点符号或其他符号，但也可以使用 Unicode 字符来匹配任何其他类型的文本。

以下列表解释了形成模式的正则表达式元字符。

- `.` 匹配任意单个字符（换行符除外）

- `[abc]` 匹配括号内的任意一个字符

- `[^abcABC]` 匹配括号内之外的任意一个字符

- `[a-z]` 匹配范围内的任意字符

- `[a-z]` 匹配范围之外的任意字符

- `sun |moon` 匹配列出的字符串中的任意一个

- `^` 行首

- `$` 行尾

正则表达式的所有功能也可以通过 `grep` 实现。你可以从上面的示例中看到，单词没有被双引号包围。为了防止 shell 解析元字符本身，建议将更复杂的模式放在双引号（`""`）之间。为了练习，我们在实现正则表达式时将使用双引号。其他的引号将保持其正常功能，正如在之前的课程中讨论过的样。

以下示例强调了正则表达式的功能。我们需要文件中的数据，因此接下来的一组命令将向 `.txt` 文件中追加不同的字符串。

```
$ echo "aaabb1" > text.txt
$ echo "abab2" >> text.txt
$ echo "noone2" >> text.txt
$ echo "class1" >> text.txt
$ echo "alien2" >> text.txt
$ cat text.txt
aaabbb1
abab2
noone2
class1
alien2
```

第一个示例是搜索文件和正则表达式的结合。为了完全理解正则表达式，显示它们的区别是非常重要的。第一条命令在行任意任何位置搜索精确字符串，而第二条命令搜索包含括号内任意字符的字符集。因此，命令的结果是不同的。

```
$ grep "ab" text.txt
aaabb1
abab2
$ grep "[ab]" text.txt
aaabb1
abab2
class1
alien2
```

第二组示例显示了行首和行尾元字符的应用。在表达式中指定将这 2 个字符放在正确的位置是非常重要的。当指定行首时，元字符需要放在表达式之前；而指定行尾时，元字符需要放在表达式之后。

```
$ grep "^a" text.txt
aaabb1
abab2
alien2
$ grep "2$" text.txt
abab2
noone2
alien2
```

在上述已解释的元字符之上，正则表达式还具有允许对之前指定的模式进行倍数匹配的元字符：

- `*` 前一个模式的零次或多次

- `+` 前一个模式的一次或多次

## Linux 基础（版本 1.6） | 主题 3：命令行的力量

- `?` 前一个模式的零次或一次

对于倍数元字符，下面的命令搜索一个包含 `ab`、单个字符以及之前发现的一个或多个字符的字符串。结果显示 `grep` 找到了 `aaaabb` 字符串，匹配了 `abbb` 部分以及 `abab2`。由于 `+` 字符是扩展正则表达式字符，我们需要向 `grep` 命令传递 `-E` 选项。

```
$ grep -E "ab.+\+" text.txt
aaabb1
abab2
```

大多数元字符都是自言自明的，但在第一次使用时可能会变得复杂。之前的示例仅代表了正则表达式功能的一小部分。尝试上表中的所有元字符以了解更多关于它们如何工作的知识。

### 引导练习

使用 `grep` 和 `/usr/share/hunspell/en_US.dic` 文件，找到符合以下标准的行：

- 1. 行中任意位置包含单词 `cat` 的所有行。

- 2. 不包含以下任何字符的全部行：`sawgt fixk`。

- 3. 所有以任意 3 个字母和单词 `dig` 开头的行。

- 4. 所有以至少一个 `e` 结尾的行。

- 5. 所有包含以下单词之一的行：`org`, `kay` 或 `tuna`。

- 6. 所有以一个或没有 `c` `ati` 开头的行。

### 探索练习

- 1. 找到匹配“Include”行中单词但不匹配“Exclude”行中单词的正则表达式：

    - Include: pot, spot, apot

    - Exclude: potic, spots, potato

    - Include: arp99, apple, zipper

    - Exclude: zoo, arive, attack

    - Include: arcane, capper, zoology

    - Exclude: air, coper, zoloc

    - Include: 0th/pt, 3th/tc, 9th/pt

    - Exclude: 0/nm, 3/nm, 9/nm

    - Include: Hawaii, Dario, Ramiro

    - Exclude: hawaii, Ian, Alice

    - 2. 还有其他哪些用于搜索文件的实用命令？

    - 3. 结合之前的课程，使用示例中的一个并尝试在 `grep` 的帮助下在输出中搜索特定模式。

### 总结

在本实验中你学习了：

- 正则表达式元字符

- 如何用正则表达式创建模式

- 如何在文件中搜索

- `grep`

## 引导练习答案

使用 `grep` 和 `/usr/share/hunspell/en_US.dic` 文件，找到符合以下标准的行：

- 1. 行中任意位置包含单词 `cat` 的所有行。

```
$ grep "cat" /usr/share/hunspell/en_US.dic
catraz
Decate
```

- 2. 不包含以下任何字符的全部行：`sawgt fixk`。

```
$ grep -v "[sawgt fixk]" /usr/share/hunspell/en_US.dic
496
```

- 3. 所有以任意 3 个字母和单词 `dig` 开头的行。

```
$ grep "^.{3}dig" /usr/share/hunspell/en_US.dic
cardigan
condign
predigest
```

- 4. 所有以至少一个 `e` 结尾的行。

```
$ grep -E "e+" /usr/share/hunspell/en_US.dic
Anglicize
Anglophobe
Anthropocene
```

- 5. 所有包含以下单词之一的行：`org`, `kay` 或 `tuna`。

```
$ grep -E "org|kay|tuna" /usr/share/hunspell/en_US.dic
Borg
George
Tokay
fortunate
```

- 6. 所有以一个或没有 `c` `ati` 开头的行。

```
$ grep "c?ati" /usr/share/hunspell/en_US.dic
3
```

## 探索练习答案

1. 找到匹配“Include”行中单词但不匹配“Exclude”行中单词的正则表达式：

    - Include: pot, spot, apot

    - Exclude: potic, spots, potato

    答案：`pot$`

    - Include: arp99, apple, zipper

    - Exclude: zoo, arive, attack

    答案：`p+`

    - Include: arcane, capper, zoology

    - Exclude: air, coper, zoloc

    答案：`arc|cap|zoo`

    - Include: 0th/pt, 3th/tc, 9th/pt

    - Exclude: 0/nm, 3/nm, 9/nm

    答案：`[0-9]th.+`

    - Include: Hawaii, Dario, Ramiro

    - Exclude: hawaii, Ian, Alice

    答案：`^[A-Z]a.*+$`

2. 还有其他哪些用于搜索文件的实用命令？它有哪些额外功能？

`sed` 命令。该命令可以查找并替换文件中的字符或字符集。
