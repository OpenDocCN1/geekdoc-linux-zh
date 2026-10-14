
| WWW | http://www.gnu.org/software/m4/m4.html |
| Key | Value |
| :--- | :--- |
| DEB | m4 |
| RPM | m4 |
| WWW | http://www.gnu.org/software/m4/m4.html |

268 Linux 编译指南，第 2 版

# JOE

- DEB: joe
- RPM: joe
- WWW: http://sourceforge.net/projects/joe-editor/

![](img/87037a08576dd88b212b2f4a41577fd3_303_0.png)

图 10-22. Joe 自己的编辑器。

# Le

一种用于终端的多语言编辑器，支持矩形文本块。

- DEB: 1le
- RPM: 1le
- WWW: http://tinyurl.com/23325

![](img/87037a08576dd88b212b2f4a41577fd3_303_1.png)

图 10-23. Le。

# 第 10 章：编辑文本

### MCedit

这是随 Midnight Commander 附带的全屏终端编辑器

```
DEB: mc-common
RPM: mc
WWW: http://www.ibiblio.org/mc/
```

![](img/87037a08576dd88b212b2f4a41577fd3_304_0.png)

图 10-24. Midnight Commander。

### Nano

GNU Nano 是一个受 PICO 启发的免费软件编辑器，PICO 是华盛顿大学专用 PINE 邮件程序中包含的编辑器。它比 PICO更快，并且带有更多功能。

```
DEB: nano
RPM: nano
WWW: http://www.nano-editor.org/
```

![](img/87037a08576dd88b212b2f4a41577fd3_304_1.png)

图 10-25. Nano。

# Linux 编译指南，第 2 版

### Ted

Ted 是一个用于 X 的所见即所得（WYSIWYG）、类打字机的文本编辑器。它可以读写 RTF 文件（微软的“富文本格式”）。

- DEB: ted
- RPM: Ted
- WWW: http://www.nllgg.nl/Ted/

![](img/87037a08576dd88b212b2f4a41577fd3_305_0.png)

图 10-26. Ted。

### The Hessling 编辑器 (THE)

THE 是一个使用 Rexx 宏语言的可配置编辑器。它的灵感来自用于 VM/CMS 的 XEDIT 编辑器和用于 DOS 的 Kedit 编辑器。

- DEB: the
the-doc
- RPM: THE
- WWW: http://hessling-editor.sourceforge.net/

![](img/87037a08576dd88b212b2f4a41577fd3_305_1.png)

图 10-27. The Hessling 编辑器。

# 第 10 章：编辑文本

### 271 Vi

Vi 是一个可视化或全屏编辑器。它可能是 Linux 上以及大多数基于 UNIX 的系统中最流行的编辑器。盲打字通常发现它的按键命令可以实现非常快速的编辑。本章前面的部分有一个关于它的介绍（参见菜谱 10.2 [使用 Vi]，第 244 页）。

Vi

- DEB: nvi
- RPM: nvi
- WWW: http://www.bostic.com/vi/

![](img/87037a08576dd88b212b2f4a41577fd3_306_0.png)

图 10-28. Vi。

与 Elvis 编辑器一样，Vi（“改进版 Vi”）是 Vi 的现代实现；它有更多的命令和功能性，新功能包括语法高亮、滚动条和菜单、鼠标支持以及内置帮助。

Vim

- DEB: vim
- RPM: vim
- WWW: http://www.vim.org/

![](img/87037a08576dd88b212b2f4a41577fd3_306_1.png)

图 10-29. Vim。

### 272 Linux 编译指南，第 2 版

Wily 是一个有趣的以鼠标为中心的编辑器，其灵感来自 AT&T Plan 9 实验操作系统的 Acme 编辑器。Wily 的命令由三个鼠标键的各种组合组成，被称为“和”（chords）。

- DEB: wily
- WWW: http://www.cs.yorku.ca/~oz/wily/

![](img/87037a08576dd88b212b2f4a41577fd3_307_0.png)

Xcoral

一个用于 X 的多窗口以鼠标为中心的文本编辑器。

- DEB: xcoral
- RPM: xcoral
- WWW: http://xcoral.free.fr/

![](img/87037a08576dd88b212b2f4a41577fd3_307_1.png)

# 第 10 章：编辑文本

### Xedit

Xedit 是一个随 X 并在 X 中的简单文本编辑器。它允许你插入、删除、复制和粘贴文本，以及打开和保存文件——这些都是基础操作。

- DEB: xbase-clients
- RPM: XFree86
- WWW: http://www.xfree86.org/

![](img/87037a08576dd88b212b2f4a41577fd3_308_0.png)

图 10-32. Xedit。

### Emacs

Emacs 是一个具有高级功能的 Emacs 版本，用于 X 并显示图像。

- DEB: emacs-common
- RPM: emacs
- WWW: http://www.emacs.org/

![](img/a088b212b2f4a41577fd3_308_1.png)

图 10-33. Emacs。

# 第 11 章：语法与参考

在 Linux 上进行写作和编辑的工具和资源包括拼写检查器、字典和参考文件。本章展示了如何使用它们。

## 11.1 拼写检查

在 Linux 上对文本和文件进行拼写检查有多种方法；以下展示了如何查找特定单词的正确拼写以及如何进行批量、交互和基于 Emacs 的检查。

系统字典文件 `/dict/words` 仅仅是一个单词列表（尽管很大），按字母顺序排序，每行一个单词。无论大小写，正确的单词以全小写形式出现，某些依赖大写（如专有名词）。所有的 Linux 拼写工具都使用此文件进行检查；如果一个单词没有出现在字典中，则被认为拼写错误。

要查看字典中有多少单词，输入：

```
$ wc -l /dict/words
```

注意：计算机拼写检查工具会纠正这种错误——例如，如果你把 "there" 写成了 "their"，计算机无法检测到！

### 11.1.1 查找单词的正确拼写

如果你不确定单词的拼写是否正确，请使用 `spell` 来查找。`spell` 从标准输入读取并输出字典中未找到的——因此如果单词拼写错误，它会在屏幕上显示。

在越来越多的系统中，此文件被较新的名称 `/usr/share/dict/words` 替换；管理员应该创建一个较短的符号链接。

换句话说，无论它们是全小写、首字母大写还是全大写都是正确的。

例如，检查单词 "occurrence" 是否拼写错误，输入：

```
$ spell
occurrence
CTRL-D
```

在例示中，`spell` 输出了单词 "occurrence"，这意味着该单词不在字典中，因此很可能是拼写错误。然后输入 CTRL-D 退出 `spell`。

### 11.1.2 列出文本中的拼写错误

要输出文件中的拼写错误列表，将检查的文件作为 `spell` 的参数。文件中的任何拼写错误都会输出，每个单词占一行，并按照它们在文件中出现的顺序。

检查文件 lecture.draft，输入：

```
$ spell lecture.draft
occurrence
will
occurrence
```

在示例中，输出了三个单词："occurrence"、will" 和再次 "occurrence"，这意味着这三个单词在 lecture.draft 中按该顺序找到，且不在系统字典中（因此可能拼写错误）。注意，错误的 "occurrence" 在文件中出现了两次。

要纠正拼写错误，你可以用偏好的文本编辑器打开文件并进行编辑。在本节的后面，我将描述一种允许你在发现拼写错误时立即进行纠正的交互式拼写检查器。另一种选择是使用带有内置拼写检查功能的文本编辑器，例如 Emacs。

检查文件 lecture.draft 并任何可能的拼写错误的单词输出到文件 lecture.spelling，输入：

```
$ spell lecture.draft > lecture.spelling
```

# 第 11 章：语法与参考
