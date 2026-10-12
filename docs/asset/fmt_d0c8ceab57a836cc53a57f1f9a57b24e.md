
最后，在这里以及全书其他地方的某些地方，我们看到使用了 `register` 关键字。曾经，该关键字向编译器提供提示，表明如果可能的话，应将给定变量放置在 CPU 寄存器中。使用该关键字已过时；现代编译器都基于对源代码的分析来确定寄存器分配，忽略 `register` 关键字。我们选择保留使用它的代码，但你应该意识到它已无实际用处。<sup>2</sup>

## 2.3 选项解析：`getopt()` 和 `getopt_long()`

大约 1980 年，针对 System III，AT&T 内部的 Unix 支持小组注意到每个 Unix 程序都使用临时技术来解析参数。为了使用户和开发人员更轻松，他们开发了前文列出的大多数惯例。（尽管 System III intro(1) man 页中的陈述比 POSIX 标准中的正式程度要低得多。）

Unix 支持小组还开发了 `getopt()` 函数以及几个外部变量，以便轻松编写遵循标准惯例的代码。GNU `getopt_long()` 函数提供了与 `getopt()` 兼容的版本，同时也使解析前文所述形式的长选项变得容易。

### 2.3.1 单字母选项

`getopt()` 函数的声明如下：

```c
#include <unistd.h>                             /* POSIX */

int getopt(int argc, char *const argv[], const char *optstring);
extern char *optarg;
extern int optind, opterr, optopt;
```

参数 `argc` 和 `argv` 通常直接来自 `main()` 的参数。`optstring` 是一个选项字母的字符串。如果字符串中的任何字母后面跟有一个冒号，则期望该选项具有一个参数。

要使用 `getopt()`，需要从一个 `while` 循环中反复调用它，直到它返回 -1。每次找到有效的选项字母时，它都会返回该字母。如果选项需要参数，`optarg` 会被设置指向该参数。考虑一个接受 -a 选项（不取参数）和 -b 选项（取参数）的程序：

```c
int oc;               /* 选项字符 */
char *b_opt_arg;

while ((oc = getopt(argc, argv, "ab:")) != -1) {
    switch (oc) {
      case 'a':
          /* 处理 -a，设置标志，等等 */
          break;
      case 'b':
          /* 处理 -b，从 optarg 获取参数值 */
          b_opt_arg = optarg;
          break;
      case ':':
          ...         /* 错误处理，参见正文 */
      case '?':
      default:
          ...         /* 错误处理，参见正文 */
    }
}
```

在其运行过程中，`getopt()` 设置了几个控制错误处理的变量。

```c
char *optarg
```

选项的参数，如果该选项接受参数的话。

```c
int optind
```

`argv` 中的当前索引。当 `while` 循环结束时，剩余的操作数可在 `argv[optind]` 到 `argv[argc - 1]` 中找到。（记住 `argv[argc] == NULL`。）

```c
int opterr
```

当此变量非零时（默认情况如此），`getopt()` 会为其无效选项或缺失的选项参数打印自己的错误消息。

```c
int optopt
```

当发现无效的选项字符时，`getopt()` 返回 '？' 或 '：'（见下文），并且 `optopt` 包含发现的无效字符。

人是人，程序被错误调用的情况是不可避免的，无论是使用了无效选项，还是缺少选项参数。在正常情况下，`getopt()` 会针对这些情况打印自己的消息并返回 '?' 字符。然而，你可以通过两种方式改变其行为。

首先，通过在调用 `getopt()` 之前将 `opterr` 设置为 0，可以强制 `getopt()` 在发现问题时保持沉默。

其次，如果 `optstring` 参数的第一个字符是冒号，那么 `getopt()` 会保持沉默，并根据错误返回不同的字符，具体如下：

- 无效选项

  `getopt()` 返回 '?'，并且 `optopt` 包含无效的选项字符。（这是正常行为。）

- 缺失的选项参数

  `getopt()` 返回 '：'。如果 `optstring` 的第一个字符不是冒号，那么 `getopt()` 返回 '?'，使得这种情况无法与无效选项情况区分开来。

因此，将 `optstring` 的第一个字符设为冒号是个好主意，因为它允许你区分“无效选项”和“缺失的选项参数”。代价是，使用冒号也会使 `getopt()` 保持沉默，迫使你提供自己的错误消息。下面是之前的示例，这次包含了错误消息处理：

```c
int oc;          /* 选项字符 */
char *b_opt_arg;

while ((oc = getopt(argc, argv, ":ab:")) != -1) {
    switch (oc) {
    case 'a':
        /* 处理 -a，设置标志，等等 */
        break;
    case 'b':
        /* 处理 -b，从 optarg 获取参数值 */
        b_opt_arg = optarg;
        break;
    case ':':
        /* 缺失的选项参数 */
        fprintf(stderr, "%s: option `-%c' requires an argument\n",
                argv[0], optopt);
        break;
    case '?':
        /* 无效选项 */
        fprintf(stderr, "%s: option `-%c' is invalid: ignored\n",
                argv[0], optopt);
        break;
    }
}
```

关于标志或选项变量命名规范的一句话：许多 Unix 代码对于给定的选项字母 `x` 会使用形如 `xflg` 的名称（例如，V7 中 `echo` 的 `nflg`；`xflg` 也很常见）。这对编写程序的作者来说可能很不错，因为他们无需查阅文档就知道 `x` 选项的作用。但对于其他试图阅读代码且不熟记所有选项字母含义的人来说，这并不友好。使用能传达选项含义的名称要得好得多，例如使用 `no_newline` 来表示 `echo` 的 `-n` 选项。

## 2.3.2 GNU `getopt()` 与选项顺序

标准的 `getopt()` 函数在遇到不以 `-` 开头的命令行参数时，就会停止查找选项。GNU `getopt()` 则不同：它会扫描整个命令行以查找选项。在此过程中，它会*置换*（重新排列）`argv` 的元素，使得完成处理后，所有选项都被移到前面，从而确保后续检查 `argv[optind]` 到 `argv[argc-1]` 的代码能正确工作。在所有情况下，特殊参数 `--` 都会终止选项扫描。

你可以通过在 `optstring` 中使用特殊的首字符来更改默认行为，如下所示：

- `optstring[0]` == `+`

  GNU `getopt()` 的行为类似于标准 `getopt()`；它按发现选项的顺序返回选项，并在遇到第一个非选项参数时停止。如果环境中存在 `POSIXLY_CORRECT`，此行为也成立。

- `optstring[0]` == `-`

  GNU `getopt()` 返回*所有*命令行参数，无论其是否代表参数。在这种情况下，对于每个这样的参数，该函数返回整数 `1` 并将 `optarg` 设置为指向该字符串。

与标准 `getopt()` 类似，如果 `optstring` 的第一个字符是 `:`，那么 GNU `getopt()` 通过分别返回 `?` 或 `:` 来区分“无效选项”和“缺少选项参数”。如果第一个字符是 `+` 或 `-`，`optstring` 中的 `:` 可以是第二个字符。

最后，如果 `optstring` 中的某个选项字母后面跟着*两个*冒号字符，则允许该选项具有可选的选项参数。（试着快速说三遍这句话！）如果该参数与选项位于同一个 `argv` 元素中，则视为存在该参数；否则视为不存在。如果参数不存在，GNU `getopt()` 返回该选项字母并将 `optarg` 设置为 NULL。例如，给定：

```c
while ((c = getopt(argc, argv, "ab::")) != -1)
...
```
