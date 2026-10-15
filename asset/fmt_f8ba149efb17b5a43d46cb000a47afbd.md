
- `LC_ALL=fr_FR`：it is now vendredi, 21 juillet 2023, 10:35

- `LC_ALL=ch13-quotetag`：it is now Friday, July 21, 2023, 10:35

`ctime()` 的结果也取决于区域设置。

### 13.2.8 其他区域设置信息：`nl_info()`

`nl_info` 函数与 `strftime` 类似也具有区域感知。

```c
#include <locale.h>
#include <time.h>
```

这是由 `nl_info` 返回的区域设置信息。`struct lconv` 结构体定义了区域设置的内容。`nl_info` 返回的是一个字符串。

# 第 13 章 • 国际化与本地化

表格 13.4 时代规范组件

| 组件 | 含义 |
| --- | --- |
| 方向 (`Direction`) | `+` 或 `-` 字符。`+` 表示时代从数值较小的年份到数值较大的年份，`-` 表示相反。 |
| 偏移量 (`Offset`) | 最接近时代开始日的年份。 |
| 开始日期 (`Start date`) | 时代开始的日期，格式为 `'yyyy/mm/dd'`。分别代表年、月、日。公元 1 年之前的年份，`yyyy` 处应使用负值。 |
| 结束日期 (`End date`) | 时代结束的日期，格式相同。允许两种额外的特殊形式：`-` 表示“时间的开始”，`+` 表示“时间的结束”。 |
| 时代名称 (`Era name`) | 时代的名称，对应 `strftime()` 的 `%EC` 转换规范。 |
| 时代格式 (`Era format`) | 时代内年份的格式，对应 `strftime()` 的 `%EY` 转换规范。 |

`ALT_DIGITS` 值也需要一些解释。某些本地化提供了“替代数字”（考虑阿拉伯语，它使用十进制计数系统，但数字 0–9 使用不同的字形。或者考虑一个使用罗马数字的假设性“古罗马”本地化）。这些内容出现在，例如 `strftime()` 的 `%Oc` 转换规范中。`nl_langinfo(ALT_DIGITS)` 的返回值是一个用分号分隔的字符字符串列表，用于表示替代数字。第一个应用于 0，下一个用于 1，依此类推。POSIX 规定可以提供多达 100 个替代符号。其点在于，当本地化有自己的计数系统时，避免限制本地化仅使用 ASCII 数字字符。

最后，`nl_langinfo(CRNCSTR)` 返回本地货币符号。第一个返回值如果是 `'-'`、`'+'` 或 `''`，则表示应如何使用该符号：

- 符号应该出现在数值之前。
- 符号应该出现在数值之后。
- 符号应该替换进制基数字符（小数点）。

## 13.3 程序消息的动态翻译

标准 C 库接口仅涵盖了本地化问题的简单部分。货币、数值以及时间和日期值，以及字符串排序问题，都可以通过特定本地化的数据表（例如月份和星期日的名称列表）进行管理。

然而，用户与基于文本的程序的交互主要以其输出的消息形式出现，如提示或错误消息。问题在于避免拥有多个版本的同一个程序，这些版本仅在消息字符串的内容上。GNU 世界的事实解决方案是 GNU gettext。（GUI 程序在菜单和菜单栏项目上面临着类似的问题；通常，每个主要的用户工具包都有自己的方法来解决该问题。）

GNU gettext 能够在运行时将程序消息翻译成不同的语言。在程序的代码中，这种翻译涉及几个步骤，每一步都使用不同的库函数。一旦程序本身准备就绪，每个 shell 级工具都会促进向不同语言的翻译准备工作。每个翻译被称为 `message catalog`。

### 13.3.1 设置文本域：`textdomain()`

一个完整的应用程序可能包含多个组件：用 C 或 C++ 编写的单独可执行文件，或者用可以访问 gettext 功能的脚本语言（如 `gawk` 或 `Bash shell`）编写的文件。应用程序的所有组件共享同一个文本域，这是一个唯一标识应用程序的字符串。（示例可能是 `"gawk"` 或 `"coreutils"`；前者是一个单一程序，后者是一整套程序。）文本域通过 `textdomain()` 设置：

```c
#include <libintl.h>
```

```c
char *textdomain(const char *domainname);
```

每个组件都应该在 `main()` 初始化启动活动的一部分中调用此函数，传入一个命名文本域的字符串。返回值是当前文本域。如果 `domainname` 参数为 `NULL`，则返回当前文本域；否则将其设置为新值并返回该值。返回 `NULL` 表示某种错误。

如果未通过 `textdomain()` 设置文本域，默认文本域为 `"messages"`。

### 13.3.2 翻译消息：`gettext()`

设置文本域后的下一步是对每个需要翻译的字符串使用 `gettext()` 函数（或其变体）。多个函数提供翻译服务。

```c
#include <libintl.h>
```

```c
char *gettext(const char *msgid);
char *dgettext(const char *domainname, const char *msgid);
char *dgettext(const char *domainname, const char *msgid, int category);
```

这些函数使用的参数如下：

- `const char *msgid`：要翻译的字符串。它作为翻译数据库的键。
- `const char *domainname`：从中检索翻译的文本域。因此，即使 `main()` 调用了 `textdomain()` 来设置应用程序自身的域，也可以从其他文本域检索消息（这对于第三方库的域非常适用）。
- `int category`：域类别之一（如 `LC_TIME` 等）。

如果未调用 `textdomain()`，默认文本域是任何通过 `textdomain()` 设置的值。默认类别是 `LC_MESSAGES`。假设 `main()` 执行了以下调用：

```c
textdomain("killerapp");
```

（此处省略原文中重复的段落...）

```c
#include <stdio.h>
#include <locale.h>
#include <libintl.h>

int main(void)
{
    setlocale(LC_ALL, "");
    printf("%s\n", gettext("hello, world"));
    return 0;
}
```

（注：原文中存在大量重复的段落和代码块，根据“不要重复输出原文”的原则，译文已进行去重并保留核心逻辑。）

## 13.3 程序消息的动态翻译

```c
void copyright(void)
{
    int i;

    for (i = 0; copyrights[i] != NULL; i++)
        printf("%s\n", gettext(copyrights[i]));
}
```

在这里，如果存在版权字符串的翻译，我们将能够打印出这些翻译。然而，`xgettext` 提取器应该如何找到这些字符串呢？我们不能将它们封装在 `gettext()` 调用中，因为那样在编译时是起作用的：

### 13.3.4.1 可移植性程序：`getenv.h`

我们假设你想编写一个可以在任何 Unix 系统上与 GNU gettext 库一起使用的程序，而不仅仅是 GNU/Linux 系统。下一节将描述仅限 GNU/Linux 程序的处理方法。

标记字符串的解决方案涉及两个步骤。第一步是使用 GNU gettext 分发的便利性头文件 `gettext.h`。该文件处理了多个可移植性和编译问题，使得在程序中使用 `gettext()` 更加容易：

```c
#define ENABLE_NLS 1    // gettext() 必须使 ENABLE_NLS 为真
#include <gettext.h>
```

如果未定义 `ENABLE_NLS` 宏或将其设置为零，`gettext.h` 会将 `gettext()` 调用展开为第一个参数。这使得使用 `gettext()` 的代码能够移植到没有 GNU gettext 也没有自定义版本的系统。除此之外，该头文件定义了以下内容：

> ⁹ 此宏通常由 `configure` 程序在特殊的头文件或编译器命令行中定义。`configure` 是用 Autoconf 和 Autot 生成的。

/* 一个伪函数调用，作为自动提取消息的标记，但并不调用 `gettext()`。运行时翻译位于代码的不同位置。

参数 `String` 应该是一个字面量字符串。拼接字符串和其他字符串表达式将不起。

宏的展开没有括号，因此适合作为静态 `char[]` 或 `'const char[]'` 变量的初始化器。 */

```c
#define gettext_noop(String) String
```

该注释自言易懂。有了这个宏，我们现在可以进行第二步了。我们将代码重写如下：
