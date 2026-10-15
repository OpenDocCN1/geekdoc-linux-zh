
- `gchar *g_strjoin(const gchar *separator, ..., NULL)`

  连接多个字符串。

- `gchar *g_strcpy(gchar *dest, const gchar *src)`

  将 `src` 拷贝到 `dest`。

- `gint *g_snprintf(gchar *string, glint n, const gchar *format, ...)`

  像 `sprintf()` 一样。

- `gint *g_vsprintf(gchar *string, glint n, const gchar *format, va_list list)`

  与上一个函数类似。

- `gchar *g_strreverse(gchar *string)`

  反转字符串。

- `gchar *g_strstrip(gchar *string)`

  消除开头的空白。

- `gchar *g_strchomp(gchar *string)`

  消除末尾的空白。

- `gchar *g_strstrip(gchar *string)`

  消除两端空白。

- `gchar *g_strreplace(const gchar *source, const gchar *search, char *exceptions)`

  转换特殊字符。

- `gchar *g_strescape(const gchar *source)`

  反转转义。

- `gchar *g_strncat(const gchar *string1, ..., NULL)`

  拼接字符串。

- `gchar *g_strjoin(const gchar *separator, ..., NULL)`

  连接字符串。

- `gchar *g_strcpy(gchar *dest, const gchar *src)`

  拷贝字符串。

- `gint *g_snprintf(gchar *string, glint n, const gchar *format, ...)`

  格式化字符串。

- `gint *g_vsprintf(gchar *string, glint n, const gchar *format, va_list list)`

  变长格式化。

- `gchar *g_strreverse(gchar *string)`

  反转字符串。

- `gchar *g_strstrip(gchar *string)`

  去除头部空白。

- `gchar *g_strchomp(gchar *string)`

  去除末尾空白。

- `gchar *g_strstrip(gchar *string)`

  去除两端空白。

- `gchar *g_strreplace(const gchar *source, const gchar *search, char *exceptions)`

  替换字符。

- `gchar *g_strescape(const gchar *source)`

  恢复转义。

- `gchar *g_strncat(const gchar *string1, ..., NULL)`

  连接字符串。

- `gchar *g_strjoin(const gchar *separator, ..., NULL)`

  连接字符串。

- `gchar *g_strcpy(gchar *dest, const gchar *src)`

  拷贝字符串。

- `gint *g_snprintf(gchar *string, glint n, const gchar *format, ...)`

  带限制格式化。

- `gint *g_vsprintf(gchar *string, glint n, const gchar *format, va_list list)`

  变长格式化。

- `gchar *g_strreverse(gchar *string)`

  反转字符串。

- `gchar *g_strstrip(gchar *string)`

  去除头部空白。

- `gchar *g_strchomp(gchar *string)`

  去除末尾空白。

- `gchar *g_strstrip(gchar *string)`

  去除两端空白。

### 1.4.4 Unicode 和字符编码

传统的 C 函数和上一节中的函数是处理字节字符串。这些函数不需要担心单个字符的身份，因为每个 `gchar` 只有一个字节。

本节中的函数则不同，因为它们处理 Unicode 字符。Unicode 是一个可以编码任何语言字符的扩展统一字符集（UCS；见 ISO 10646）。GLib 支持三种不同的编码方案（我们使用 UTF-8）：

- UCS-4 是完整的 32 位 UCS 编码，字符占用 2 个字节（另外 2 个通常为 0）。GLib 用于 Unicode 的数据类型是 `gunichar`。它是 32 位的标准 Unicode。某些函数使用 UCS-4 字符串 (`gunichar *`)。

- UTF-16 是原生编码（UTF 代表 Unicode 转换格式）。每个字符是 2 个字节。GLib 使用 `gunchar` 类型处理 UTF-16 中的字符。作为 UTF-4 的，你将使用 UTF-16 字符串。

- UTF-8 在实践中非常重要，因为它兼容 ASCII。普通的 ASCII 字符使用 8 位，但其他字符需要 2 个或更多字节。此外，每个 ASCII 格式的文件都包含 UTF-8，反之不然。一个明显的缺点是 UTF-8 的宽度使得无法对文本文件进行随机访问；要获取某部分，你必须从开始遍历字符。

注意标题大小字母（Titlecase）在英语（或其他许多其他语言）中并不常见。标题大小字母通常是某种复合字符或连字，当该字母在单词开头大写时，复合字符的第一部分变为大写。它是克罗地亚语单词 `Ljubljana` [1] 中的 `Lj`。

- `g_unichar_isalpha(gunichar)` 如果 `c` 是字母，则返回 `TRUE`。

- `g_unichar_isdigit(gunichar)` 如果 `c` 是 10 进制数字，则返回 `TRUE`。

- `g_unichar_isxdigit(gunichar)` 如果 `c` 是十六进制数字，则返回 `TRUE`。

- `g_unichar_isymbol(gunichar)` 如果 `c` 是某种符号或标点符号，则返回 `TRUE`。

- `g_unichar_isspace(gunichar)` 如果 `c` 是空白形式（包括空格、制表符和换行符），则返回 `TRUE`。

- `g_unichar_iswide(gunichar)` 如果 `c` 在屏幕上绘制时通常返回普通字符的两倍空间，则返回 `TRUE`。

- `g_unichar_iscontrol(gunichar)` 如果 `c` 是 Unicode 控制字符，则返回 `TRUE`。

- `g_unichar_isgraph(gunichar)` 如果可以打印它（且它不是控制字符、格式或空格），则返回 `TRUE`。

- `g_unichar_isprint(gunichar)` 类似于 `g_unichar_isprint()`，但也会对空格返回 `TRUE`。

如果你有一个 unicode 字符 `c`，并想知道它在 Unicode 中的分类，可以运行：

```
g_unichar_type(c)
```

此函数返回以下常量之一（更多信息请参阅 [TUC]）：

- `G_UNICODE_LOWERCASE_LETTER`: 小写字母

- `G_UNICODE_UPPERCASE_LETTER`: 大写字母

- `G_UNICODE_TITLECASE_LETTER`: 标题大小字母

- `G_UNICODE_CONTROL`: 控制字符

- `G_UNICODE_FORMAT`: Unicode 格式字符

- `G_UNICODE_MODIFIER_LETTER`: 修饰字母（用于修改读音的特殊字母）

- `G_UNICODE_SURROGATE`: 由两个 16 位 Unicode 字符组成的复合体，表示一个字符

- `G_UNICODE_UNASSIGNED`: 当前未分配

- `G_UNICODE_PRIVATE_USE`: 留供私有内部使用的字符

- `G_UNICODE_OTHER_LETTER`: 任何杂字母

- `G_UNICODE_COMBINING_MARK`: 可与另一个字母组合的标记

- `G_UNICODE_ENCLOSING_MARK`: 包含字母的标记

- `G_UNICODE_NON_SPACING_MARK`: 通常不需要空间即可的标记；其位置取决于另一个基础字符

- `G_UNICODE_DECIMAL_NUMBER`: 数字

- `G_UNICODE_DECIMAL_NUMBER`: 由字母构成的数字

- `G_UNICODE_OTHER_NUMBER`: 任何其他数字

- `G_UNICODE_CONNECTION_PUNCTUATION`: 连接性标点

- `G_UNICODE_DASH_PUNCTUATION`: 像折号那样的标点

- `G_UNICODE_OPEN_PUNCTUATION`: 开头标点（如左括号）
