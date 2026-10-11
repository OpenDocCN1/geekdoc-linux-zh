
## 12.2.5 列出上位词

单词的上位词（Hypernym）是指含义比给定单词更通用的相关术语。（例如，`mammal` 和 `animal` 是 `cat` 的上位词。）

要用 `wn` 输出单词的上位词，请使用以下选项之一：`-hyphen` 用于名词，`-hypev` 用于动词。

- 输出名词 `cat` 的所有上位词，输入：

```bash
$ wn cat -hyphen RET
```

## 12.2.6 在线字典

(Debian) `dict` (WWW): http://www.dict.org/ 字典开发小组在其网络网站 http://www.dict.org/ 上提供了许多免费字典。在该页面上，你可以从包含超过 300,000 个词条的字典中查询单词定义（包括同义词和其他搜索），或者为自己的系统复制一份字典。存在一个 `dict` 客户端用于访问 DI 服务器并在本地输出定义；该工具在 `dict` 软件包中可用。

DICT 还有许多纯文本文件的专业字典（包括《自由新闻字典》，其中包含了新闻和出版行业中使用的术语和词汇）。他们的 FILE 项目——“自由互联网词汇与百科全书”，是一项构建免费、开源的现代词汇、成语和术语集合的努力。FILE 是一项志愿者活动，取决于学者和词典编者的支持；DICT 页面包含了如何帮助贡献这一伟大项目的信息。

## 12.3 检查语法

### 12.3.1 检查误用短语

要检查网页文本，请使用纯文本网络浏览器 `lynx` 并带有 `~dump` 和 `-nolist` 选项输出给定 URL 的纯文本，并将此输出通过到 `diction`。（如果你预计会有大量输出，请在末尾添加另一个管道以便你进行翻阅。）

要查看 http://example.org/1.html 带有可能的冗余和误用短语标记的文本副本，输入：

```bash
$ lynx ~dump -nolist http://example.org/1.html | dict | less
```

### 12.3.2 检查重复单词

`diction` 查找的内容之一是重复单词（doubled words）——即连续出现两次的单词。如果它发现这样的序列，会将成对的第二个成员括在括号中，后面跟一个右箭头和文本 `Double`，例如 `this <i> Double word`。

要仅检查文件中的重复单词，而不检查 `diction` 检查的任何其他内容，请使用 `grep` 查找 `diction` 输出中所有包含 `Double word` 的行（如果有）。

- 输出文件 `dissertation` 中所有包含重复单词的行，输入：

```bash
$ dict dissertation | grep 'Double word' RET
```

### 12.3.3 检查文本的可读性

`style` 命令用于分析给定文本的写作风格。它对文本进行多种可读性测试并输出结果，同时提供有关文本中句子的统计信息。传入要检查的文件名作为参数。

- 要检查文件 `dissertation` 的可读性，请输入：

```
$ style dissertation RET
```

和 `diction` 命令一样，如果没有提供文本，`style` 会从标准输入读取文本——这对于流水线的末端非常有用，也可以用于检查你输入的特定句子或其他文本的写作风格。

`style` 输出的文本句子特征如下：

- 字符数
- 单词数、其平均长度以及平均音节数
- 句子数及平均单词长度
- 短句和长句的数量
- 段落数及平均句子长度
- 疑问句和祈使句的数量

`style` 使用并输出的各种可读性公式如下：

- Kincaid 公式，最初为海军训练手册开发；对于技术文档具有良好的可读性参考价值
- 自动可读性指数 (ARI)
- Coleman–Liau 易读评分，提供从 0（困难）到 100（简单）的可读性近似值
- Fog 指数，提供学校年级阅读水平
- WSTF 指数，德国文档的可读性指标
- Wheeler–Smith 指数、Lix 公式和 SMOG 等级测试，均为提供学校年级水平的可读性指标

## 12. 语法与参考

### 12.3.4 检查困难句

要输出文本中的 `difficult` 句子，请使用 `style` 并配合 `-r` 后跟一个数字；`style` 将仅输出自动可读性指数 (ARI) 大于指定数字的句子。

- 要输出文件 `dissertation` 中所有 ARI 大于 20 的句子，请输入：

```
$ style -r 20 dissertation RET
```

### 12.3.5 检查长句

使用 `style` 向 `-l` 参数传入最小单词数，可以输出超过特定长度的句子。

- 要输出文件 `dissertation` 中所有长于 14 个单词的句子，请输入：

```
$ style -l 14 dissertation RET
```

## 12.4 词列表与参考文件

@sf(Debian): `miscfiles`
@sf(WWW): http://ftp.gnu.org/pub/gnu/miscfiles/miscfiles-1.1.tar.gz

GNU Miles 是包含各种事实和参考材料的文本集合，例如常用缩写、电话区号和英语连接短语。

这些文件存储在 `/usr/share/misc` 目录下，并且经过了压缩；使用 `zless` 来浏览（参见“查阅文本”章节）。

下表列出了 `/usr/share/misc` 中的文件及其内容描述。

| 文件 | 描述 |
| :--- | :--- |
| GNU-manifesto.gz | GNU 宣言。 |
| abbrevs.talk.gzabbrevs.gen | 电子通信中常用缩写词的集合。（这里可以找到 TTYL 和 `LOL` 的秘密秘籍。） |
| airport.gz | 某些主要机场的三字母城市代码列表。城市代码用于查询国家气象局计算机以获取你所在地区的最新天气状况。 |
| ascii.gz | ASCII 字符集表。 |
| birhtoken.gz | 每个月的传统生肖和长令牌。 |
| cities.dat.gz | 许多城市的人口、政治坐标（国家、地区）和地理坐标（纬度、经度）。 |
| inter.phone.gz | 国际和城市电话代码。 |
| languages.gz | 来自 ISO 639 的语言双字母代码。 |
| latin1.gz | 扩展 ASCII 字符集，也称为 ISO 8859 (“Latin-1”）字符集。 |
| mailinglists.gz | 所有公共 GNU 项目相关邮件列表的描述。 |
| na.phone.gz | 北美 (+1) 电话区号。 |
| operator.gz | C 语言运算符的优先级表。 |
| postal.codes.gz | 美国、墨西哥州和加拿大省的邮政编码。 |
| us-constitution.gz | 美利坚联合国宪法（尽管没有权利法案）。（在 Debian 系统上，此文件置于 `/usr/share/state/`） |
| us-declaration.gz | 十殖民地的独立宣言。（在 Debian 系统上，此文件置于 `/usr/share/state/`） |
| rfc-index.txt | 互联网标准请求意见稿 (RFC) 文档索引。（在 Debian 系统上，此文件置于 `/usr/share/rfc/`） |
| zipcodes.gz | 美国五位邮政编码。 |

不过，`miscfiles` 并非 Debian 系统唯一的参考包；其他相关包包括：

## 13.1.3 统计文本行数

使用 `wc` 命令配合 `-l` 选项来指定统计并输出行数。

- 要输出文件 `outline` 的行数，输入：

```bash
$ wc -l outline RET
```

## 13.1.4 统计某些内容的出现次数

要查找某个文本字符串或模式在文件或多个文件中出现次数，请使用 `grep` 搜索文件中的该文本字符串，并将输出管道给带有 `-l` 选项的 `wc`。

- 要查找文件 `outline` 中包含字符串 `chapter` 的行数：

```bash
$ grep chapter outline | wc -l RET
```

**注意**：更多搜索文本的技巧以及关于 grep 的更多信息，请参阅[搜索文本]。

## 13.1.5 Emacs 中统计每页行数

Emacs 中的 `count-lines-page` 函数会输出缓冲区（minuffer）中当前页（由分页符分隔）的行数（如果有的话——参见[文本分页]），然后是点（point）之前的缓冲区行数，以及点之后的缓冲区行数。

- 要统计 Emacs 中当前缓冲区每页的行数，输入：

```bash
C-x l1
```
