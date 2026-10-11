
第 7 行定义了 `myname`，它指向程序名称；该变量用于 `globerr()`（定义在第 11–15 行）的错误消息。

第 33–45 行是程序的核心。它们遍历命令行中给出的模式，并对每个模式调用 `glob()`，将其结果追加到列表中。循环的大部分是错误处理（第 36–44 行）。第 47–48 行打印结果列表，第 50–51 行进行清理并返回。

第 39–41 行的代码并不美观；应该使用一个独立的函数将整型常量转换为字符串；我们主要为了节省空间才这样写。对于小型程序来说，这样的代码是可以接受的，但较大的程序应使用函数。

如果你仔细思考一下底层所发生的所有工作（打开和读取目录、匹配模式、动态分配以扩展列表、排序列表），你开始会意识到 `glob()` 为你做了多少事情！以下是一些结果：

```
$ ch12-glob '/usr/lib/*\.so' .../*\.texi'
/usr/lib/xchat-autoS.so
/usr/lib/xchat-autoGS.so
.../00-prefix.texi
.../01-intro.texi
.../02-cmdline.texi
.../03-memory.texi
...
```

注意，我们必须引用参数，以防止 shell 进行扩展！

> **通配符扩展？那是什么？**
>
> 在远古时代，大约 V6 Unix 时期，shell 使用一个独立的程序在幕后执行通配符扩展。这个程序被命名为 /etc/glob，根据 V6 源代码，¹ “glob” 是 “global” 的缩写。
>
> 因此，“to glob”（通配）这个词进入了 Unix 词汇表，意思是“执行通配符扩展”。这反过来又赋予了 `glob()` 和 `globfree()` 这些函数名称。Unix 手册中偶尔流露出的那种含蓄的幽默感因此得以延续，并正式载入 POSIX 标准。（你能想象在 20 世纪 70 或 80 年代的 IBM，有人将一个系统例程命名为 `glob()` 吗？）

### 12.7.3 Shell 单词扩展：wordexp() 和 wordfree()

许多 POSIX 委员会成员认为 glob() 做得还不够：他们希望有一个库例程，能够完成 shell 所能做的一切：波浪号扩展（`echo $~arndld`）、shell 变量扩展（`echo $HOME`）以及命令替换（`echo $(cd ; pwd)`）。许多其他人认为 glob() 不是实现这一目的的正确函数。为了“满足”每个人，POSIX 提供了另外两个功能，它们可以完成所有工作：

```
#include <wordexp.h>   POSIX
int wordexp(const char *words, wordexp_t *pwordexp, int flags);
void wordfree(wordexp_t *pwordexp);
```

这些函数的作用类似于 glob() 和 globfree()，但它们在 wordexp_t 结构体上操作：

```
typedef struct {
    size_t we_wordc;      /* 匹配到的单词数量 */
    char **we_wordv;      /* 扩展后的单词列表 */
    size_t we_offs;       /* 在 we_wordv 中保留的槽位 */
} wordexp_t;
```

其成员与前面描述的 glob_t 完全类似；我们不会在此重复整个描述。

与 glob() 一样，几个标志控制 wordexp() 的行为。标志列在表 12.5 中。

**表 12.5**
wordexp() 的标志

| 常量 | 含义 |
| :--- | :--- |
| WRDE_APPEND | 将当前调用的结果追加到前一次调用的结果中。 |
| WRDE_DOFFS | 在 we_wordv 的前部保留 we_offs 个位置。 |
| WRDE_NOCMD | 不允许命令替换。 |
| WRDE_REUSE | 复用 we_wordv 已指向的存储空间。 |
| WRDE_SHOWERR | 扩展过程中的错误不要静默处理。 |
| WRDE_UNDEF | 使未定义的 shell 变量产生错误。 |

如果一切顺利，返回值为 0；否则为表 12.6 中的某个值。

**表 12.6**
wordexp() 错误返回值

| 常量 | 含义 |
| :--- | :--- |
| WRDE_BADCHAR | 在无效位置出现了元字符（换行符、`' '`、`&`、`;`、`<`、`>`、`(`、`)`、`{`、`}` 或 `)` 之一）。 |
| WRDE_BADVAL | 变量未定义且设置了 `WRDE_UNDEF`。 |
| WRDE_CMDSUB | 尝试了命令替换且设置了 `WRDE_NOCMD`。 |
| WRDE_NOSPACE | 动态内存分配出现问题。 |
| WRDE_SYNTAX | 存在 shell 语法错误。 |

我们将修改 ch12-glob.c 以使用 wordexp() 和 wordfree() 的任务留给你作为练习（见后文）。以下是我们版本的运行情况：

```text
$ ch12-wordexp 'echo $HOME'                Shell 变量扩展
echo
/home/arnold
$ ch12-wordexp 'echo $HOME/*.gz'          变量和通配符
echo
/home/arnold/48000.wav.gz
/home/arnold/ipmapq-HOWTO.tar.gz
/home/arnold/rc.firewall-examples.tar.gz
$ ch12-wordexp 'echo ~arnold'             波浪号扩展
echo
/home/arnold
$ ch12-wordexp 'echo ./arnold/.p*'        波浪号和通配符
echo
/home/arnold/.posinitnotes
/home/arnold/.procmailrc
/home/arnold/.profile
$ ch12-wordexp 'echo `~arnold/.p*``'      引用有效
echo
~arnold/.p*
```

## 12.8 正则表达式

*正则表达式* 是一种描述要匹配的文本模式的方法。如果你已经使用 GNU/Linux 或 Unix 有一段时间，你肯定熟悉正则表达式：它们是 Unix 程序员工具箱中的基础部分。它们是 `grep`、`egrep`、`sed`、`awk`、Perl 以及 `ex`、`vi`、`vim` 和 Emacs 编辑器等日常程序的重要组成部分。如果你完全不了解正则表达式，我们建议你绕道去阅读第 12.9 节“推荐阅读”，第 480 页中列出的一些书籍或网址。

POSIX 定义了两种类型的正则表达式：*基础* 和 *扩展*。诸如 `grep`、`sed` 和行编辑器 `ed` 等程序使用基础正则表达式。诸如 `egrep` 和 `awk` 等程序使用扩展正则表达式。以下函数使你的程序能够使用这两种类型中的任意一种：

```
#include <sys/types.h> 
#include <regex.h> 
int regcomp(regex_t *preg, const char *regex, int cflags); 
int regexec(const regex_t *preg, const char *string, size_t nmatch, 
regmatch_t pmatch[], int eflags); 
size_t regerror(int errcode, const regex_t *preg, 
char *errbuf, size_t errbuf_size); 
void regfree(regex_t *preg)
```

![](img/766b5597246d532412fad21b1c59ccec_504_0.png)

要进行正则表达式匹配，你必须首先*编译*正则表达式的字符串版本。编译将正则表达式转换为内部形式。然后，编译后的形式被*执行*于字符串之上，以查看它是否匹配原始正则表达式。这些函数如下：

```
int regcomp(regex_t *preg, const char *regex, int cflags)
```

将正则表达式 `regex` 编译为内部形式，并将其存储在 `*preg` 指向的 `regex_t` 结构中。`cflags` 控制编译方式；其值为 0 或表 12.7 中一个或多个标志的按位或结果。

```
int regexec(const regex_t *preg, const char *string, size_t nmatch, 
regmatch_t pmatch[], int eflags)
```

将 `*preg` 中编译好的正则表达式应用于字符串 `string`。`eflags` 控制执行方式；其值为 0 或表 12.8 中一个或多个标志的按位或结果。我们稍后讨论其他参数。

```
size_t regerror(int errcode, const regex_t *preg, char *errbuf, 
size_t errbuf_size)
```

将 `regcomp()` 或 `regexec()` 返回的错误转换为可供人类阅读的字符串。

```
void regfree(regex_t *preg)
```

释放 `*preg` 中编译好的正则表达式所使用的动态内存。

<regex.h> 头文件定义了许多标志。有些用于 regcomp()，其他用于 regexec()。但是，它们都以前缀 'REG' 开头。表 12.7 列出了使用 regcomp() 编译正则表达式时的标志。

**表 12.7**
regcomp() 的标志

| 常量 | 含义 |
| :--- | :--- |
| REG_EXTENDED | 使用扩展正则表达式。默认是基础正则表达式。 |
| REG_ICASE | regexec() 匹配时忽略大小写。 |
| REG_NEWLINE | 可以匹配任何字符的操作符不匹配换行符。 |
| REG_NOSUB | 不需要子模式开始和结束信息（参见文本）。 |

使用 regexec() 进行正则表达式匹配的标志见表 12.8。

**表 12.8**
regexec() 的标志

| 常量 | 含义 |
| :--- | :--- |
| REG_NOTBOL | 不允许 ^（行首）操作符匹配。 |
| REG_NOTEOL | 不允许 $（行尾）操作符匹配。 |

REG_NEWLINE、REG_NOTBOL 和 REG_NOTEOL 标志相互关联。这有点复杂，所以我们一步步来。

- 当 cflags 中不包含 REG_NEWLINE 时，换行符充当普通字符。'.'（匹配任何字符）元字符可以匹配它，取反的字符列表（'^ . . .'）也可以。此外，$ 不匹配嵌入的换行符之前，^ 也不匹配换行符之后。
- 当 eflags 中设置了 REG_NOTBOL 时，^ 操作符不匹配字符串的开头。当 string 参数是正在匹配的文本中间某个字符的地址时，这很有用。
- 类似地，当 eflags 中设置了 REG_NOTEOL 时，$ 操作符不匹配字符串的结尾。
- 当 cflags 中包含 REG_NEWLINE 时：

