

⇒ 若要输出 marketing 文件的内容，将文本 "television"（无论是否大写）替换为 "Internet"，但不替换包含文本 "radio" 的行，请输入：

```
$ sed '/radio/!s/[Tt]elevision/Internet/g' marketing RET
```

## 14.9 在 Emacs 中搜索文本

以下方法展示了在 Emacs 中搜索文本的各种方式——增量搜索、搜索单词或短语、搜索模式——以及搜索后替换文本。

### 14.9.1 在 Emacs 中增量搜索

输入 CTRL–S 可使用 Emacs 的增量搜索功能。它会在迷你缓冲区中接收文本输入，并从当前点向当前缓冲区末尾搜索该文本。再次输入 CTRL–S 可搜索你要查找的文本的下一次出现位置；此操作可持续到不再有匹配项为止。然后 Emacs 会在迷你缓冲区中报告 "Failing I-search"；再次输入 CTRL–S 可回绕到缓冲区开头并从那里继续搜索。

它之所以被称为"增量"搜索，是因为你一开始输入文本它就会立即开始搜索，因此搜索字符串是逐步构建的。例如，如果你想在当前缓冲区中搜索单词 "sunflower"，你可以开始输入：

```
CTRL–S s
```

此时，Emacs 会从点开始向前搜索缓冲区，直到第一个 "s" 字符并将其高亮显示。然后，当你输入 u 时，它会向前搜索缓冲区中第一个 "su" 并将其高亮显示（如果 "u" 紧跟在它第一次停下的 "s" 之后，它会停在那里并高亮显示 "s" 和 "u"）。只要你继续输入，并且当前缓冲区中存在匹配项，它就会一直这样进行下去。一旦你输入的内容在缓冲区中不存在，Emacs 就会发出蜂鸣声，并在迷你缓冲区中出现一条消息，说明搜索失败。

要搜索你上次输入的字符串的下一个实例，请再次输入 CTRL–S；如果你一直按住 CTRL，那么每次按下 S 键，Emacs 都会前进到缓冲区中的下一个匹配项。

⇒ 若要搜索当前缓冲区中从点反向到缓冲区开头的文本 "moon"，请输入：
CTRL-(R) moon

### 14.9.2 在 Emacs 中搜索短语

与 grep 一样，Emacs 的增量搜索只能作用于文本行，因此它只能找到同一行中的短语。如果你使用增量搜索搜索 "hello, world"，而文本 "hello," 出现在一行的末尾，"world" 出现在下一行的开头，它将无法找到。

要跨换行符查找多词短语，请使用 word-search-forward 函数。无论标点或空格如何，它都能搜索到短语或单词。

⇒ 若要在当前缓冲区中向前搜索短语 "join me"，请输入：
ALT-(X) word-search-forward RET join me RET

注意：word-search-backward 函数与 word-search-forward 功能相同，只是它会从点开始向缓冲区开头反向搜索。

### 14.9.3 在 Emacs 中搜索正则表达式

使用 search-forward-regexp 函数可从当前点向当前缓冲区末尾搜索正则表达式。

⇒ 若要在当前缓冲区中向前搜索正则表达式 "@.*\.org"，请输入：
ALT-(X) search-forward-regexp RET @.*\.org RET

此命令的键盘快捷键是 ALT-(CTRL)-(S)。要重复你上次进行的正则表达式搜索，请输入 ALT-(CTRL)-(S) CTRL-(S)；然后，只要你按住 CTRL，就可以持续输入 s 前进到下一个匹配项，就像增量搜索一样。

注意：还有一个 search-backward-regexp 函数，功能完全相同，但会从点向缓冲区顶部反向搜索。

### 14.9.4 在 Emacs 中搜索并替换

你也可以在 Emacs 缓冲区中搜索并替换文本；为此，请使用 replace-regexp 函数，并同时提供要搜索的表达式和要替换成的表达式。正则表达式会从点向缓冲区末尾进行匹配；要搜索并替换缓冲区中所有匹配项，请在点位于缓冲区开头时运行此函数。

⇒ 若要将当前缓冲区中的文本 "day" 替换为文本 "night"，请输入：

```
ALT - X replace-regexp RET
Replace regexp: day RET
Replace regexp day with: night RET
Replaced 7 occurrences
```

在上面的示例中，正则表达式 "day" 从点向缓冲区末尾被找到了七次（并被替换为正则表达式 "night"）。

此函数特别适用于将控制字符替换为文本，或将文本替换为控制字符。你可以使用 CTRL - Q（即 quoted-insert 函数）来指定这些控制字符（参见方法 10.1.4 [在 Emacs 中插入特殊字符]，第 239 页）。

⇒ 若要将当前缓冲区中的所有 "Control-M" 字符替换为普通换行符，请输入：

```
ALT - X replace-regexp RET
Replace regexp: CTRL - Q CTRL - M RET
Replace regexp "M" with: CTRL - Q 012 RET RET
Replaced 101 occurrences
```

在此示例中，从点向缓冲区末尾共找到（并替换了）101 个 "Control-M" 字符。

## 14.10 在 Vi 中搜索文本

要在 Vi 中搜索文本，请使用与 less 中搜索文本相同的方法，该方法在下一个方法中给出。

## 14.11 搜索正在阅读的文本

使用 less 浏览文本时，你可以搜索文本。less 中有两个用于搜索文本的有用命令：/ 和 ?。要向前搜索

