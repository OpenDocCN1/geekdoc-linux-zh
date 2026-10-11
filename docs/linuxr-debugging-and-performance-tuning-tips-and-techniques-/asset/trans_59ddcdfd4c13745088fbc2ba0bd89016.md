
这些宏并不显眼，在实际应用中，所有使用 GNU gettext 的 GNU 程序都遵循此约定。如果您打算使用 GNU gettext，您也应该遵循此约定。

### 13.3.4.2 仅限 GLIBC：<libintl.h>

对于仅在使用 GLIBC 的系统上运行的程序，头文件的使用和宏定义相似但更简单：

```c
#include <stdio.h>
#include <libintl.h>
#define _(msgid) gettext(msgid)
#define N_(msgid) msgid
... 其他内容相同 ...
```

正如前面所见，`<libintl.h>` 头文件声明了 `gettext()` 和其他函数。您仍然需要定义 `_()` 和 `N_()`，但无需担心 `ENABLE_NLS`，也无需将 `gettext.h` 随程序的源代码分发。

### 13.3.5 使用 printf() 调整单词顺序

在生成翻译时，英语中自然的语序在其他语言中可能是错误的。例如，在英语中形容词出现在它所修饰的名词之前，而在许多语言中它出现在名词*之后*。因此，像下面的代码就存在问题：

```c
char *animal_color, *animal;

if (...) {
    animal_color = __("brown");
    animal = __("cat");
} else if (...) {
    ...
} else {
    ...
}
printf_("The %s %s looks at you enquiringly.\n", animal_color, animal);
```

在这里，格式字符串、`animal_color` 和 `animal` 都正确地包含在 `gettext()` 调用中。然而，翻译后该语句仍然不正确，因为*运行时无法改变参数的顺序*。

为了解决这个问题，POSIX（但*非* ISO C）版本的 `printf()` 系列函数允许您在格式说明符中提供*位置说明符*。其形式为：在初始 `%` 字符之后立即跟一个 `$` 字符和十进制数字。例如：

```c
printf("%2$s, %1$s\n", "world", "hello");
```

位置说明符指示使用参数列表中的哪个参数；计数从 1 开始，不包括格式字符串本身。此示例以正确的顺序打印著名的 'hello, world' 消息。

GLIBC 和 Solaris 实现了此功能。由于这是 POSIX 的一部分，如果您的 Unix 供应商的 `printf()` 没有此功能，它应该会很快出现。

位置说明符后面可以跟随任何常规的 `printf()` 标志、字段宽度和精度。使用位置说明符的规则如下：

- 位置说明符形式不能与非位置形式混合。换句话说，要么每个格式说明符都包含位置说明符，要么都不包含。当然，`%%` 始终可以使用。
- 如果使用了第 $n$ 个参数，则前 $N$ 个参数必须也被字符串使用。因此，以下代码是无效的：
  `printf('$3$s $1$s\n', 'hello', 'cruel', 'world');`
- 特定参数可以通过位置说明符多次引用。非位置格式说明符始终按顺序遍历参数列表。

此设施不旨在让应用程序员直接使用，而是供翻译人员使用。例如，对于之前格式字符串 "The %s %s looks at you enquiringly.\n" 的法语翻译，可能是：
"Le %2$s %1$s te regarde d'un air interrogateur.\n"
（即使这个翻译也不完美：冠词 "Le" 是特定性别的。为程序准备翻译是一项艰巨的工作）

### 13.3.6 在私有目录中测试翻译

程序中的消息集合被称为*消息目录*（message catalog）。这个术语也适用于消息到不同语言的每种翻译。当程序安装时，每种翻译也会安装在标准位置，以便 `gettext()` 在运行时能够找到正确的那个。

将翻译放在标准目录之外的目录中可能很有用，特别是对于程序测试。特别是在大型系统上，常规开发人员可能没有将文件安装到系统目录所需的权限。`bindtextdomain()` 函数为 `gettext()` 提供了一个查找翻译的替代位置：

```c
#include <libintl.h>
char *bindtextdomain(const char *domainname, const char *dirname);

GLIBC
```

有用的目录包括表示当前目录的 `.` 和 `/tmp`。从环境变量中获取目录也可能很方便，如下所示：

```c
char *td_dir;

setlocale(LC_ALL, "");
textdomain("killerapp");
if ((td_dir = getenv("KILLERAPP_TD_DIR")) != NULL)
    bindtextdomain("killerapp", td_dir);
```

应在调用 `gettext()` 系列函数之前调用 `bindtextdomain()`。我们在第 13.3.8 节“创建翻译”（第 517 页）中看到了如何使用它的示例。

### 13.3.7 准备国际化程序

到目前为止，我们已经查看了构成国际化程序的所有组件。本节将总结该过程。

1. 将 `gettext.h` 头文件引入您的应用程序，并在包含于所有 C 源文件的头文件中添加 `_()` 和 `N_()` 宏的定义。不要忘记定义 `ENABLE_NLS` 符号常量。
2. 适当调用 `setlocale()`。最简单的方法是调用 `setlocale(LC_ALL, "")`，但偶尔应用程序可能需要更细致地选择要启用的区域设置类别。
3. 为应用程序选择一个文本域，并使用 `textdomain()` 设置它。
4. 如果进行测试，使用 `bindtextdomain()` 将文本域绑定到特定目录。
5. 适当使用 `strftime()`、`strfmon()` 和 `printf()` 的 `'` 标志。如果需要其他区域信息，请使用 `nl_langinfo()`，特别是与 `strftime()` 结合使用时。
6. 使用 `_()` 或 `N_()` 调用标记所有应被翻译的字符串，视情况而定。

不过，有些字符串不应这样标记。例如，如果您使用 `getopt_long()`（参见第 2.1.2 节“GNU 长选项”，第 27 页），您可能*不想*将长选项名称标记为待翻译。此外，像 `"%d %d\n"` 这样的简单格式字符串不需要翻译，调试消息也不需要。

7. 在适当的情况下，使用 `ngettext()`（或其变体）来处理值可能为 1 或大于 1 的情况。
8. 通过使用表示完整句子的多个字符串，而不是使用 %s 和 ?: 进行单词替换，可以简化翻译人员的工作。例如：

```c
if (an error occurred) {     /* 正确 */
    /* 使用多个字符串以简化翻译。 */
    if (input_type == INPUT_FILE)
        fprintf(stderr, _("%s: cannot read file: %s\n"),
                    argv[0], strerror(errno));
    else
        fprintf(stderr, _("%s: cannot read pipe: %s\n"),
                    argv[0], strerror(errno));
}
```

**这比下面这种写法更好**

```c
if (an error occurred) {     /* 错误 */
    fprintf(stderr, _("%s: cannot read %s: %s\n"), argv[0],
            input_type == INPUT_FILE ? _("file") : _("pipe"),
            strerror(errno));
}
```

正如刚才所示，包含一个注释说明故意使用多个消息是一个好主意——这使得翻译这些消息更容易。

### 13.3.8 创建翻译

一旦您的程序被国际化，就需要准备翻译。这是通过几个 shell 级别工具完成的。我们从 `ch06-echodate.c` 的国际化版本开始，该文件来自第 6.1.4 节“将分解的时间转换为 time_t”，第 176 页：

```c
/* ch13-echodate.c --- 演示翻译 */

#include <stdio.h>
#include <time.h>
#include <locale.h>
#define ENABLE_NLS 1
#include "gettext.h"
#define _(msgid) gettext (msgid)
#define N_(msgid) msgid
```

