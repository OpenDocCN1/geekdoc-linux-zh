

另一方面，apropos 命令以搜索字符串作为参数，并返回所有匹配搜索的手册页。例如，apropos mixer 给出如下列表：

alsamixer (1) - soundcard mixer for ALSA soundcard driver
mixer (1) - command-line mixer for ALSA soundcard driver
aumix (1) - adjust audio mixer

因此，使用 apropos 来帮助你查找命令，并使用 whatis 来告诉你某个命令的作用。

## 使用 mkdir 创建目录

创建目录就像听起来一样简单，虽然有一个参数你应该注意：-p。如果你位于 /home/paul 且想创建目录 /home/paul/audio/sound，你会得到类似这样的错误：

```
mkdir: cannot create directory `audio/sound': No such file or directory
```

乍一看这似乎不对，因为 mkdir 无法创建目录，因为它不存在。实际上它的意思是它无法创建目录 sound，因为目录 audio 不存在。这就是 -p 参数发挥作用的地方：如果要创建的目录位于另一个不存在的目录内，如上例，-p 也会创建父目录。因此。

```
mkdir -p audio/sound
```

这首先创建 audio 目录，然后在其内部创建 sound 目录。

## 使用 mv 移动文件

这个命令是周围最简单的命令之一。mv 有两个有用的参数：-f，它在不询问的情况下覆盖文件；-u，它仅在源文件比目标文件更新时才移动源文件。就这样！

## 使用 ps 列出进程

这是本文讨论的第三个也是最后一个“本应简单却不简单”的命令。ps 命令列出进程并为其操作提供极大的控制。

首先要知道的是，ps 通常使用所谓的 BSD 风格参数。在“使用 find 搜索查找文件”一节中，我们讨论了 UNIX 风格、GNU 风格和 X 风格参数，分别为 -c、--dosomething 和 -d dosomething，但 BSD 风格参数不同，因为它们使用不带连字符的单个字母。

因此，ps 的默认用法列出你正在运行的、附加到终端的所有进程。然而，你可以通过添加 x 参数来要求它列出附加到任何终端的、甚至不附加终端的所有你的进程：ps x。你可以通过 a 参数要求它列出所有用户的所有进程，或将该参数与 x 结合以列出所有用户的所有进程，无论是否附加到终端：ps ax。

然而，这两者都比全能的 u 选项逊色，后者启用面向用户的输出。实际上，这带来巨大差异，因为你会得到所有者用户名、使用的 CPU 时间和 RAM、进程启动时间等重要字段。这会输出大量信息，因此你可能想尝试添加 f 参数，它通过使用 ASCII 艺术连接父命令与其子进程来创建进程树。你可以将迄今为止的所有选项组合成此命令：ps faux（是的，有点想象力的话，你可以用参数拼出单词！）。

你可以通过使用 --sort 参数来控制数据的返回顺序。它接受 + 或 -（+ 为默认值）后跟你想要排序的字段：command、%cpu、pid 和 user 都是热门选项。如果使用减号，结果会反转。下一个命令按 CPU 使用率降序列出所有进程：

```
ps aux --sort=-%cpu
```

ps 还有许多其他参数，包括大量与其他 UNIX 系统兼容的选项。如果你有时间阅读手册页，你应该试试！

## 使用 `rm` 删除文件和目录

rm 命令只有一个感兴趣的参数：--preserve-root。到目前为止，你应该知道使用 sudo 执行 rm -rf / 会破坏你的 Linux 安装，因为 -r 表示递归，-f 表示强制（删除前不提示确认）。粗心的人可能不小心发出此命令——不是故意输入命令，而是把空格放错位置。例如：

```
rm -rf /home/paul
```

该命令删除用户 paul 的主目录。这不是一个不常见的命令；在删除用户并备份其数据后，你可能想执行类似的操作。然而，如果你在“home”中的 / 和 h 之间不小心加了一个空格，你会得到这个：

```
rm -rf / home/paul
```

这次命令的意思是“从 / 递归删除所有内容，然后删除 home/paul”——结果完全不同！你可以通过使用 --preserve-root 参数来阻止这种情况的发生，它会用以下消息阻止灾难：

```
rm: it is dangerous to operate recursively on /
rm: use --no-preserve-root to override this failsafe.
```

