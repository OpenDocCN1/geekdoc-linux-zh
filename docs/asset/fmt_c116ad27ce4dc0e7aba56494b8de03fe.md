
选项 `x` 将从 `tar` 归档中提取文件。它会将内容提取到执行命令的当前目录。

```
# tar xvf /tmp/my_home_directory.tar
```

## 我如何将 `tar.gz` 文件提取到特定目录？

```
# tar xvfz /tmp/my_home_directory.tar.gz -C /home/ramesh
```

# 破解 49. 将 `gzip`、`bzip2` 与 `tar` 结合

## 如何配合 `tar` 使用 `gzip`？

处理 `tar.gz` 压缩文件时，在 `tar` 命令中添加选项 `z`。

```
# tar cvfz /tmp/my_home_directory.tar.gz /home/jsmith
# tar xvfz /tmp/my_home_directory.tar.gz
# tar tvfz /tmp/my_home_directory.tar.gz
```

> 注意：与 `bzip2` 相比，使用 `gzip` 更快。

## 如何配合 `tar` 使用 `bzip2`？

处理 `tar.bz2` 压缩文件时，在 `tar` 命令中添加选项 `j`。

```
# tar cvfj /tmp/my_home_directory.tar.bz2 /home/jsmith
# tar xvfj /tmp/my_home_directory.tar.bz2
# tar tvjf /tmp/my_home_directory.tar.bz2
```

注意：与 `gzip` 相比，使用 `bzip2` 提供更高的压缩率。

# 第 8 章：命令行历史

当你频繁使用 Linux 命令行时，有效使用 `history` 可以极大提高效率。事实上，一旦你掌握了我这里提供的 15 个示例，你就会发现命令行变得更加有趣享受。

## 破解 50. 使用 `HISTTIMEFORMAT` 在历史中显示时间戳

通常当你从命令行输入 `history` 时，它会显示命令和命令。为了审计目的，如下所示与命令一起显示时间戳可能会很有帮助。

```
# export HISTTIMEFORMAT="%F %T "
# history
1
2
3
4
| more
2008-08-05
2008-08-05
2008-08-05
19:02:39
19:02:39
19:02:39
service network restart
exit
id
cat /etc/redhat-release
```

注意：你也可以设置以下别名来查看最近的历史命令。

`alias h1='history 10'`

`alias h2='history 20'`

`alias h3='history 30'`

## 破解 51. 使用 `Control+R` 搜索历史

我坚信这可能是你 `history` 中最高频繁的功能。当你已经执行了一个非常长的命令时，只需使用关键字搜索历史并重新执行相同的命令，而无需完整输入。按下 `Control+R` 并输入关键字。

在下面的示例中，我搜索了 `red`，这在历史中显示了包含该词之前的命令 `"cat /etc/redhat-release"`。

`# [注意：从命令行提示符按下 Ctrl+R，将显示如下所示的反向搜索提示符]`

`(reverse-i-search)'red': cat /etc/redhat-release`

`# [注意：当你看到你的命令时按回车，将从历史中执行该命令]`

`# cat /etc/redhat-release`

`Fedora release 9 (Sulphur)`

有时你想在执行历史记录中的命令之前对其进行编辑。例如，你可以搜索 `httpd`，它将在命令历史中显示 `service httpd stop`，选择此命令并将 `stop` 改为 `start` 然后再次重新执行，如下所示。

`# [注意：从命令行提示符按下 Ctrl+R，将显示如下所示的反向搜索提示符]`

`(reverse-i-search)'httpd': service httpd stop`

`[注意：当你看到你的命令时按回车，将从历史中执行该命令]`

`service httpd start`

## 破解 52. 从历史中重复上一个命令

有时你会重复命令。以下是重复上一个命令的四种方法：

1. 使用向上箭头

2. 输入 `!` 并回车

3. 输入 `!!` 并回车

4. 按 `Ctrl+P`

在下面的示例中，如果你想重复以 `ps` 开头的命令，输入 `!ps` 并回车。

## 破解 53. 执行以单词开头的命令

如果你想执行以特定单词开头的命令，输入 `!` 后跟单词的字母。例如，如果你想执行以 `cat` 开头的命令，输入 `!cat` 并回车。

## 破解 54. 使用 `HISTSIZE` 控制历史中的总行数

`HISTSIZE` 变量限制了存储在历史列表中的命令数量。要增加此限制，请在你的 `bash` profile 中设置：

```bash
export HISTSIZE=1000
```

## 破解 55. 使用 `HISTFILE` 修改历史文件名

默认情况下，历史存储在 `~/.bash_history`。为了跟踪从不同终端执行的命令，请在你的 `bash` profile 中设置 `HISTFILE` 变量：

```bash
export HISTFILE=~/.commandline_warrior
```

# Linux 技巧

Ajay Kumar Tiwari

# 技巧 59. 使用 `HISTCONTROL` 强制历史记录不记录特定命令

当你执行命令时，你可以通过将 `HISTCONTROL` 设置为 `ignorespace` 并在命令前输入一个空格（如下所示）来指示历史记录忽略该命令。我看到很多许多初级系统管理员对此感到非常兴奋，因为他们可以从历史记录中隐藏某些命令。

了解 `ignorespace` 的工作原理很有帮助。但作为最佳实践，请不要这样做：

```bash
# export HISTCONTROL=ignorespace
# ls -ltr
# pwd
# service httpd stop
[注意：service 开头有一个空格，以便在历史记录中忽略此命令]
# history | tail -3
67 ls -ltr
68 pwd
69 history | tail -3
```

# 技巧 60. 使用选项 `-c` 清除所有之前的历史记录

有时你可能想要清除所有之前的历史记录。然而，你可能仍然想让历史记录继续进行。

```bash
# history -c
76
```

# 技巧 61. 替换历史命令中的单词

当你搜索历史记录时，你可能想要执行一个不同的命令，但使用刚刚搜索的命令中的相同参数。

在下面的示例中，`vi` 命令旁的 `!!$` 会将上一个命令的参数传递给当前命令。

```bash
# ls anaconda-ks.cfg
anaconda-ks.cfg
# vi !!:
vi anaconda-ks.cfg
```

在下面的示例中，`vi` 命令旁的 `!^` 会将上一个命令的第一个参数（即 `cp` 命令）传递给当前命令（即 `vi` 命令）。

```bash
# cp anaconda-ks.cfg anaconda-ks.cfg.bak
anaconda-ks.cfg
# vi ^^
vi anaconda-ks.cfg
```

# 技巧 62. 为特定命令替换特定参数

在下面的示例中，`!cp:2` 会在历史记录中搜索以 `cp` 开头的之前的命令，取 `cp` 的第二个参数并将其替换为 `ls -l` 命令如下所示：

```bash
# cp ~/longname.txt /real/a/very/long/path/long-filename.txt
# ls -l !cp:2
ls -l /real/a/very/long/path/long-filename.txt
```

在下面的示例中，`!cp$` 会在历史记录中搜索以 `cp` 开头的之前的命令，取 `cp` 的最后一个参数（在本例中也是上所述的第二个参数）并将其替换为 `ls -l`。

```bash
# ls -l !cp$
ls -l /real/a/very/long/path/long-filename.txt
```

# 技巧 63. 使用 `HISTSIZE` 禁用历史记录

如果你想完全禁用历史记录，不想让 `bash` shell 记住你输入的命令，如下所示将 `HISTSIZE` 设置为 0。

```bash
# export HISTSIZE=0
# history
# [注意]:
历史记录没有显示任何内容
```

# 技巧 64. 使用 `HISTIGNORE` 忽略历史记录中的特定命令

有时你可能不希望 `pwd` 和 `ls` 等基础命令弄乱你的历史记录。使用 `HISTIGNORE` 指定所有你想从历史记录中忽略的命令。

请注意，将 `ls` 添加到 `HISTIGNORE` 中仅忽略 `ls` 而不是 `ls -l`。因此，你必须提供你想从历史记录中忽略的精确命令。
