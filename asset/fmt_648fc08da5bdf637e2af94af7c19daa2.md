
### Shell - Console

```
Session Edit View Bookmarks
user> who
mike tty1 2005-10-06 12:01
mike tty2 2005-10-06 12:01
mike tty3 2005-10-06 12:02
mike :0 2005-10-06 12:00 (console)
mike pts/1 2005-10-06 12:00
user>
```

按 `Ctrl+Alt+F1` 打开虚拟终端 1，例如，`vi` 编辑器正在运行：这是在 Linux shell 中使用 `vi` 编辑器写入的简单文本。

按 `Ctrl+Alt+F2` 打开虚拟终端 2，例如，用户可能有 `man` 手页参考：

## 名称

`vim` - Vi 文本编辑器

## 用法

```
vim [options] [file]
Manual page vi(1) line 5
```

按 `Ctrl+Alt+F3` 打开虚拟终端 3，例如，用户可能运行着一个纯文本浏览器来搜索互联网上的信息：

| Java 快速上手 |
|---|
| Linux 快速上手 |
|---|
| 选择 按回车并使用方向键返回。 |
|---|

![](img/0494b98ec9ddc4515587e9808d73902e_174_0.png)

![](img/0494b98ec9ddc4515587e9808d73902e_174_1.png)

## 文本处理

shell 中的 `cut` 和 `paste` 命令可能与你预期的不同。它们用于处理以制表符分隔按列排列的文本。每一列文本被称为“字段”（field），`cut` 命令可以指定一个选项来确定哪个字段——例如，选项 `-f3` 选择第三列。

要选择多个字段，请指定逗号分隔的列表。例如 `-f1,3`，或选择一个字段范围 `-2-4`。

![](img/0494b98ec9ddc4515587e9808d73902e_175_0.png)

| 命令 | 说明 |
|---|---|
| `cut` | 显示文本文件的指定列 |
| `paste` | 显示合并列的文本文件 |
| `tr` | 转换文本 |
| `sort` | 按字母顺序排列行 |
| `tee` | 将文本流写入文件然后显示为输出 |

`paste` 命令是 `cut` 命令的相反操作，将多个文件的列合并显示：注意这里使用了 `-t` 选项，让命令将制表符显示为 `^`。可以使用其他分隔符，但默认是制表符。

![](img/0494b98ec9ddc4515587e9808d73902e_175_1.png)

```
Shell - Console
Session Edit View Bookmark Settings
user> cat -T columns.txt
Apple Alpha
Banana Bravo
Cherry Charlie
user> cut -f2 columns.txt
Anthem
Bloom
Cheer
user> cat -T lists.txt
Sun Tough
Sea Today
Sand Trend
user> paste columns.txt lists.txt
Anthem Alpha Sun Tough
Banana Bloom Sea Today
Cherry Charlie Sand Trend
user>>
```

# ...续上

通过将文本流传递到 `tr` 命令可以轻松进行简单的文本转换。这需要两个参数来指定更改什么以及如何更改。例如，命令 `*` 将改变字母 `a` 的出现，将每个一个替换为星号。通常它用于转换大小写，如示例所示：

![](img/0494b98ec9ddc4515587e9808d73902e_176_0.png)

`who` 命令显示了谁登录了系统。对于大型多用户 Linux 系统，如果命令结果按字母排序，查找特定用户是否登录会容易得多。

| Session | Edit | View | Bookmarks | Settings | Help |
|---|---|---|---|---|---|
| user> cat quote0.txt | | | | | |
| I can resist everything except temptation. | | | | | |
| user> cat quote0.txt | tr "a-z" "A-Z" | | | | |
| I CAN RESIST EVERYTHING EXCEPT TEMPTATION. | | | | | |
| user> sort lists.txt | | | | | | |
| Sand Trend | | | | | | |
| Sea Today | | | | | | |
| Sun Tough | | | | | | |
| user> | tee unsorted.who | sort | | | | |
| andrew tty2 | 2005-10-06 13:39 | | | | | |
| david tty3 | 2005-10-06 13:39 | | | | | |
| linda tty1 | 2005-10-06 13:37 | | | | | |
| mike :0 | 2005-10-06 12:00 (console) | | | | | |
| mike pts/1 | 2005-10-06 12:00 | | | | | |

# 匹配文本模式

`grep` 命令是所有命令中最有用的之一。它有很多可能的选项，但其目的仅仅是显示文本文件中所有包含指定字符串或模式的行。

| 命令 | 说明 |
| --- | --- |
| `grep` | 显示所有包含指定模式的行 |
| `uniq` | 忽略连续的重复文本行 |

一个简单的 `grep` 命令可以将要查找的字符串作为第一个参数，将文件名作为第二个参数——按下回车键，它将显示所有包含该字符串的行。

可以使用 `uniq` 命令删除连续的重复行。首先通过管道将 `grep` 的文本流输传给 `sort` —— 以将重复的行连续排列。然后将这些行通过 `uniq` 进行处理，以便只剩下唯一的行：

![](img/0494b98ec9ddc4515587e9808d73902e_177_0.png)

正则表达式的主题本身就可以写满一本书了——更多详情请参阅 `grep`。

```
Shell - Konsole
Session Edit View Bookmarks Settings Help
user> grep sword reading-gaol.txt
The brave man with a sword!
For, right within, the sword of Sin
The brave man with a sword!
user> grep sword reading-gaol.txt | sort | uniq
For, right within, the sword of Sin
The brave man with a sword!
user> cat quotel.txt
[at the New York Custom House]
I have nothing to declare except my genius.
user> grep [Y] quotel.txt
[at the New York Custom House]
user>|
```

上面的截图包含一个使用 `grep` 显示包含大写“Y”的行的示例——这是一个基础的模式匹配。可以使用“正则表达式”搜索更复杂的模式。

## Linux 入门

# 检查拼写

`look` 命令是一个实用的小程序，用于显示以你提供的参数作为字符串开头的单词列表。这些单词从字典文件中检索，通常位于 `/usr/share/dict/words`，你可以对其进行编辑或替换。

| 命令 | 说明 |
| --- | --- |
| `ispell` | 显示当前有效用户名 |
| `look` | 显示主机域名 |

按 `Ctrl+C` 键可以退出交互式拼写检查并返回正常的 shell 提示符。

使用 `ispell` 命令进行更全面的拼写检查。使用此命令并按回车，程序会提示你输入一个要检查的单词。如果拼写正确，将报告 `OK`；如果错误，则会建议替代方案。

提供文件名作为 `ispell` 命令的参数，开始对其整个内容进行交互式拼写检查。

![](img/0494b98ec9ddc4515587e9808d73902e_178_0.png)

```
Shell - Konsole
Session Edit View Bookmarks Settings Help
user> look genius
genius geniuses's
user> ispell
(@) International Ispell Version 3.2.06
word: freind
how about: friend
user> ispell reading-gaol.txt
```
