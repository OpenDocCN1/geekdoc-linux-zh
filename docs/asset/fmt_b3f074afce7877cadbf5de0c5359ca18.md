
```
MPSSHEAP=size
MPSTACK=size
```

`MPSSHEAP` 和 `MPSTACK` 指定了堆和栈的大小。大小可以使用 `K`、`M`、`G` 或 `T` 转换为 `KB`、`MB`、`GB` 或 `TB`。

`MPSSCFILE` 是包含以下格式或多个 `MPSS` 配置的文件：

```
exec-name:heap-size:stack-size
```

`exec-name` 指定应用程序或可执行文件的名称。它可以是全路径、基名或模式字符串。如果没有指定堆大小或栈大小，则不会设置相应的首选页面大小。`MPSSCFILE` 的优先级高于 `MPSSHEAP` 和 `MPSTACK`。

### 示例

以下示例使用 `MPSSCFILE` 配置首选页面大小。

```
example$ LD_PRELOAD=$LD_PRELOAD:mpss.so.1
example$ MPSSCFILE=mpsscfg
example$ export LD_PRELOAD MPSSCFILE
example$ cat $MPSSCFILE
foo*:512K:64K
example$
```

以下示例使用 `MPSSHEAP` 和 `MPSSSTACK` 配置首选页面大小。

以下 Bourne shell 命令为所有具有 `MPSSHEAP` 和 `MPSSSTACK` 环境变量的应用程序配置 512K 堆和 64K 栈的首选页面大小。

```
example$ LD_PRELOAD=$LD_PRELOAD:mpss.so.1
example$ MPSSHEAP=512K
example$ MPSSSTACK=64K
example$ export LD_PRELOAD MPSSHEAP MPSSSTACK
example$
```

应用程序启动后，可以使用 `pmap`（参见 `proc(1)`）查看配置的实际页面大小。

```
example$ foobar &
example$ pmap -s `pgrep foobar`
```

如果未配置所需的页面大小（在 `pmap` 输出中显示），可能是由于 `MPSS` 配置文件或环境变量存在错误。检查错误日志（默认为 `/var/adm/messages`）以获取错误。如果没有发现错误，可能是资源或对齐限制导致的。

`MPSSCFILE` 中的首选页面大小配置将覆盖 `MPSSHEAP` 和 `MPSSSTACK`。按照上一个示例中的命令操作，将为所有应用程序配置 512K 堆和 64K 栈的首选页面大小，但 `ls` 命令和所有以 `ora` 开头的应用程序除外。

```
example$ MPSSCFILE=mpsscfg2
example$ export MPSSCFILE
example$ cat $MPSSCFILE
ls::
ora*:4m:4m
example$
```

# msgfmt 881

### 属性

有关以下属性的描述，请参阅 `attributes(5)`。

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | `SUMwesxu` (32位) `SUMwesxu` (64位) |
| 接口稳定性 | 演进中 (Evolving) |

## 参见

`cat(1)`, `ld.so.1(1)`, `pagesize(1)`, `ppgsz(1)`, `proc(1)`, `sh(1)`, `vi(1)`, `exec(2)`, `fork(2)`, `memcntl(2)`, `getexname(3C)`, `getpagesize(3C)`, `syslog(3)`, `proc(4)`, `attributes(5)`

# msgfmt - 从消息文件创建消息对象

### 概要

```
/usr/bin/msgfmt [-D dir --directory=dir] [-f --use-fuzzy] [-g]
[-v] [-o output-file --output-file=output-file] [-s] [--strict]
[-v] [--verbose] filename.po...
```

### 描述

`msgfmt` 从可移植对象文件(`filename.po`)创建消息对象，且不更改可移植对象。

`po` 文件包含系统命令或应用程序向用户显示的消息。你可以编辑 `.po` 文件并用系统支持的任何语言重写其中的消息。

你可以使用 `xgettext(1)` 命令从脚本或程序创建 `.po` 文件。`msgfmt` 根据当前 `LC_CTYPE` 语言区域的设置将数据解释为字符。

> 注意 — `msgfmt` 及其任何 `gettext()` 例程均未对消息的总长度施加限制。然而，`.po` 文件中的每行被限制为 `MAX_INPUT(512)` 字节。

使用 C 语言安装消息目录是没有意义的，因为为了效率考虑，它们会被忽略。

# 可移植对象文件

所有 `.po` 文件的格式都是相同的。每个 `.po` 文件包含一个或多行，每行包含一个注释或一个语句。注释以井号 (`#`) 开头并以换行符结束。所有注释（后文描述的特殊注释除外）和空行都会被忽略。语句的格式为：

```
directive value
```

每个指令从行首开始，并通过空白（如一个或多个空格或制表符）与值隔开。值由一个或多个用空白隔开的字符串组成。对于 Solaris 消息文件使用以下任何类型的指令。

```
domain domain
msgid message_identifier
msgstr message_string
```

从 Solaris 9 版本开始，对于与 GNU 兼容的消息文件，使用以下任何类型的指令。

```
domain domain
msgid message_identifier
msgid_plural translated_string_plural
msgstr message_string
msgstr[n] message_string
```

`domain` 指令的行为受所用选项的影响。请参见第 884 页的“选项”，了解指定 `-o` 或 `--output-file` 选项时的行为。（`--output-file` 选项是 Solaris 9 版本中新增的）。如果你没有指定 `-o` 或 `--output-file` 选项：

- 如果你使用 Solaris 9 版本中的新消息目录文件格式-new 生成消息对象，或指定了 `--strict` 选项，则将每个 `.po` 文件开始到第一个 `domain` 指令的所有 `msgs` 放入默认消息对象 `messages.mo` 中。否则，默认对象名为 `messages.mo`

- 当 `msgfmt` 在 `.po` 文件中遇到 `domainname` 指令时，在遇到下一个 `domain` 指令之前，将所有后续 `msgs` 放入消息对象 `domainname` 中，如果你使用 Solaris 9 版本中的新消息目录文件格式-new 生成消息对象，或者指定了 `--strict` 选项。否则，将 `msgs` 放入名为 `domainname` 的消息对象中。

- 在每个 `domain` 的范围内定义重复 `msgs`。也就是说，只有当相同 `domain` 中存在相同的 `msgid` 时，`msgid` 才被视为重复。

- 忽略所有重复项

`msgid` 指令指定了与其随后的指令相关的消息标识符的值。Solaris 9 版本中的 `msgid_plural` 指令为消息处理函数 `ngettext()`, `dgettext()`, 或 `dngettext()` 指定了复数形式消息。`message_identifier` 标识了检索时使用的字符串。每个 `msgid` 指令后必须跟一个包含 `msgstr` 指令或 `msgstr(n)` 的语句。

`msgstr` 指令指定了与紧前一个 `msgid` 指令声明的 `message_identifier` 关联的目标字符串。Solaris 9 版本中的 `msgstr[n]` 指指令（其中 `n = 0, 1, 2...`）指定了与复数形式函数 `ngettext()`, `dgettext()` 和 `dngettext()` 使用的目标字符串。

消息字符串可以包含转义序列 `\n`（换行）、`\t`（制表符）、`\v`（垂直制表符）、`\r`（返回）、`\f`（分页）、`\\`（反斜杠）、`\"`（双引号）、`\ddd`（八进制位模式）和 `\xdd`（十六进制位模式）。

# GNU 兼容的消息文件

GNU 兼容的消息文件注释使用以下格式之一（`msgfmt` 命令在处理 Solaris 消息文件时忽略这些注释）。

```
# translator-comments
# automatic-comments
# reference...
# flag
```

`#: ` 注释表示 `msgstr` 字符串在源文件中的位置，格式为文件名: 行号。`#`, `#. ` 和 `#` 注释仅供参考，会被 `msgfmt` 命令静默忽略。`#` 注释需要一个或多个由逗号隔开的标志。你可以指定以下标志。

`fuzzy`

翻译人员可以插入 `fuzzy` 显示内容是模糊的。

翻译人员可以插入 `fuzzy` 以显示内容是模糊的。`msgfmt` 命令在处理 Solaris 消息文件时忽略这些注释。模糊的的。如果你使用 Solaris 9 版本中的新消息目录文件格式-new 生成消息对象，或指定了 `--strict` 选项，则将每个 `.po` 文件开始到第一个 `domain` 指令的所有 `msgs` 放入默认消息对象 `messages.mo` 中。否则，默认对象名为 `messages.mo`
