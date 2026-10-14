
### 在 WordNet 词典中搜索以 “homew” 开头的名词

要在 WordNet 词典中搜索以 “homew” 开头的名词，请输入：

```
$ wn homew -grepn [RET]
```

### 在 WordNet 词典中搜索以 “homew” 开头的名词和形容词

要在 WordNet 词典中搜索以 “homew” 开头的名词和形容词，请输入：

```
$ wn homew -grepn -grepa [RET]
```

## 11.2.2 列出单词的释义

要列出单词的释义，请将单词作为参数传递给 `wn`，后跟 `-over` 选项。

⇒ 要列出单词 “slope” 的释义，请输入：

```
$ wn slope -over [RET]
```

NOTES: 如果您经常查找词典释义，将 `def` 定义为 `wn $1 -over` 的别名会很方便（请参阅配方 3.6.1 [使用其他名称调用命令]，第 83 页）。

### 11.2.3 列出单词的同义词

单词的同义词是指在某些上下文中可以替代第一个单词的含义相似的不同单词。要使用 `wn` 输出单词的同义词，请将单词作为参数给出，后跟以下选项之一：`-synsn` 表示名词，`-synsv` 表示动词，`-synsa` 表示形容词，或 `-synsr` 表示副词。

⇒ 这里有两种使用方法。

- 要输出名词“break”的所有同义词，输入：

```
$ wn break -synsn [RET]
```

- 要输出动词“break”的所有同义词，输入：

```
$ wn break -synsv [RET]
```

### 11.2.4 列出单词的反义词

一个词的反义词是在某些上下文中含义相反的另一个词。要使用 `wn` 输出某个词的反义词，将该词作为参数给出，然后加上以下选项之一：动词用 `-antsv`，形容词用 `-antsa`，或副词用 `-antar`。

⇒ 要输出形容词“sad”的所有反义词，输入：

```
$ wn sad -antsa [RET]
```

### 11.2.5 列出单词的上位词

一个词的上位词是一个相关术语，其含义比给定词更通用。例如，单词“mammal”和“animal”都是单词“cat”的上位词。

要使用 `wn` 输出某个词的上位词，使用以下选项之一：名词用 `-hyper` 或动词用 `-hypev`。

⇒ 要输出名词“cat”的所有上位词，输入：

```
$ wn cat -hyper [RET]
```

## 11.2.6 检查在线词典

`Dict`

DEB: `dict`

RPM: `dict`

WWW: `http://www.dict.org/`

DICT 开发小组在其网站 [`http://www.dict.org/`] 上提供了一系列免费词典。在该页面上，你可以从包含超过 300,000 个词头的词典中查找单词（包括使用同义词库和其他搜索），或复制其词典供在自己的系统上使用。用于访问 DICT 服务器并在本地输出释义的 `dict` 客户端存在；该工具可在 `dict` 包中使用。

DICT 开发小组还提供了许多专业词典。这些词典是纯文本文件。其中一个词典称为 FILE，即 The Free Internet Lexicon and Encyclopedia。它是构建现代词汇、习语和行话词典的免费开源集合的努力。FILE 是一个志愿者项目，依赖于学者和词典编纂者的支持；DICT 页面包含有关如何帮助贡献这一值得的项目的相关信息。

### 11.3 检查语法

`Diction`

DEB: `diction`

WWW: `http://www.gnu.org/software/diction/diction.html`

有两种久负盛名的 UNIX 写作检查工具最近已为基于 Linux 的系统提供：`style` 和 `diction`。

老用户可能还记得这些名字——原版随 AT&T UNIX 一起提供，作为 20 世纪 70 年代末和 80 年代初备受喜爱的“Writer’s Workbench”工具套件的一部分。

AT&T 将 Writer’s Workbench 从其 UNIX 第 7 版产品中“拆分”出来，随着多年来各种 UNIX 的蓬勃发展，这些工具逐渐被遗忘——最终成为 UNIX 传说的组成部分。

1997 年，Michael Haardt 从头开始编写了这些工具的新 Linux 版本。它们支持英语和德语，并且现在是 GNU 项目的一部分。

Writer’s Workbench 的另外两个命令长期以来一直是 Linux 的标准：`look` 和 `spell`，本章前面已描述过。

下面是使用 `diction` 或 `style` 的配方。

#### 11.3.1 检查文本中误用的短语

使用 `diction` 检查文本中冗长、陈词滥调、陈腐或误用的短语。它检查 William Strunk 在其《风格要素》[`http://www.bartleby.com/141/`] 中警告我们的所有类型的表达。

还有一套用于格式化文本的工具，称为“Documenter’s Workbench”，并且计划有一个“Reader’s Workbench”；今天，我们只能猜测它可能是什么。

根据《The UNIX Environment》，参见附录 D [References for Further Interest]，第 731 页，随旧 Writer's Workbench 提供的 `diction` 工具只是查找短语，而一个单独的命令 called `suggest` 会输出建议。在适用于 Linux 系统的 GNU 版本中，这两个功能已合并到单个 `diction` 命令中。

在 GNU `diction` 中，单词或短语用方括号 "[like this]" 括起来。如果 `diction` 有任何建议的替换，它会以右箭头 "-> like this" 为前缀给出。

当检查不止一屏的文本时，你会希望将输出通过管道传输到 `less`，以便在屏幕上浏览它（参见 Recipe 9.1 [Perusing Text]，第 211 页），或将输出通过管道传输到文件以便稍后检查。

⇒ 这里有两种使用方法。

- 要检查文件 `dissertation` 中的陈词滥调或其他误用短语，输入：

```
$ diction dissertation | less [RET]
```

- 要检查文件 `dissertation` 中的陈词滥调或其他误用短语，并将输出写入名为 `dissertation.diction` 的文件，输入：

```
$ diction dissertation > dissertation.diction [RET]
```

如果不指定文件名，`diction` 会从标准输入读取文本，直到你在单独一行输入 `<CTRL>-D`。这在你想检查单个句子时特别有用，如图 11-3 所示。

```
$ diction [RET]
Let us ask the question we wish to state. [RET]
(stdin):1: Let us [ask the question -> ask]
[we wish to state -> (cliche, avoid)].
<CTRL>-D
$
```

图 11-3. 使用 `diction` 检查句子。

要检查网页的文本，使用 `lynx` 的 `-dump` 和 `-nolist` 选项输出给定 URL 的纯文本，并将此输出通过管道传输到 `diction`。（如果预计输出很多，在末尾再加一个管道到 `less` 以便浏览。）

要浏览 URL `http://www.westegg.com/cliche/random.cgi` 并标记可能冗长和误用的短语，输入（全部在一行）：

```
$ lynx -dump -nolist http://www.westegg.com/cliche/random.cgi | diction | less [RET]
```

**注释。** 要检查文本中是否过度使用词语，请使用第 12.2.4 节 [Counting Word Occurrences in Text] 中描述的方法，第 299 页。

### 11.3.2 检查文本中的重复词

`diction` 查找的内容之一是重复词——连续重复两次的词。如果它发现这样的序列，它会将重复对的第二个成员用方括号括起来，后面跟着一个右箭头和文本“Double word”，例如“this [<i>th</i>is → Double word.]”

要仅检查文本文件中的重复词，而不检查 `diction` 检查的其他任何内容，请使用 `grep` 仅查找 `diction` 输出中包含文本“Double word”的行（如果有）。

⇒ 要输出文件 `dissertation` 中包含重复词的所有行，输入：

```shell
$ diction dissertation | grep 'Double word' [RET]
```

### 11.3.3 检查文本的可读性

`style` 命令分析给定文本的写作风格。它对文本执行一系列可读性测试并输出其结果，并提供有关文本句子的统计信息。将要检查的文本文件名作为参数给出。

⇒ 要检查文件 `dissertation` 的可读性，输入：

```shell
$ style dissertation [RET]
```
