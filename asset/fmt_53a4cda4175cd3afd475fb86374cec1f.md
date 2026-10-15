
注意我们没有使用解析器。通常作为 `perl_parse` 的参数处理，而这里 `env` 被替换为 `NULL`，这意味着将使用当前环境。

宏 `PERL_SYS_INIT3()` 和 `PERL_SYS_TERM()` 提供了运行 Perl 解释器所需的特定系统的 C 运行时环境调整；无论你创建或销毁多少个解释器，它们都应该只调用一次。在创建第一个解释器之前调用 `PERL_SYS_INIT3()`，在释放最后一个解释器之后调用 `PERL_SYS_TERM()`。

由于 `PERL_SYS_INIT3()` 可能会更改 `env`，因此将 `env` 作为参数传递给 `perl_parse()` 可能更为合适。

另外请注意，无论你向 `perl_parse()` 传递什么参数，都必须在 C `main()` 的 `argc`、`argv` 上调用一次 `PERL_SYS_INIT3()`。

现在将此程序（我将将其命名为 `interp.c`）编译为可执行文件：
`% cc -o interp interp.c -XExtUtils::Embed -ccopts -ldopts`

编译成功后，你就可以像这样使用 perl：
`% interp -e 'print "Pretty Good Perl\n"; print "10890 - 9801 = 10890 - 9801"; <CTRL-D'`
Pretty Good Perl
10890 - 9801 = 10889

或
`% interp -e 'printf("%x", 3735928559)'`
deadbeef

你也可以在 C 程序运行过程中，通过在调用 `perl_run` 之前将文件名放入 `argv[1]` 来从文件中读取并执行 Perl 程序。

## 在你的 C 程序中调用 Perl 子程序

调用单个 Perl 子程序，你可以使用 `percall` 中记录的任何 `call_*` 函数。在示例中，我们将使用 `call_argvv`。

如下所示，在一个我命名为 `Showtime.c` 的程序中。

```c
#include <perl.h>

static PerlInterpreter *my_perl;

int main(int argc, char **argv, char **env) {

    char *args[] = { NULL };

    PERL_SYS_INIT3(&argc,&argv,&env);

    my_perl = perl_alloc();

    perl_construct(my_perl);

    perl_parse(my_perl, &argc, argv, NULL);

    pl_exit_flags |= PER_EXIT_DESTRUCT_END; /**** 跳过 perl_run() ***/

    call_argvv("showtime", G_NOARGS, args);

    perl_destruct(my_perl);

    perl_free(my_perl);

    PERL_SYS_TERM(0);

}
```

这是一个不接受参数的 Perl 子程序（即 `G_NOARGS`），我将忽略它的返回值（即 `G_DISCARD`）。这些标志以及其他标志定义在 `percall` 中。

我将在名为 `showtime.pl` 的文件中定义 `showtime` 子程序：

```perl
print "I shan't be printed."; sub showtime { print time; }
```

编译和运行非常简单：

```bash
% cc -o showtime showtime.c -perl -MExtUtils::Embed -ccopts -ldopts

% showtime.pl 818284590
```

产生自 1970 年 1 月 1 日（纪元开始）以来经过的秒数，我指的是自写下这个实例以来的时间。

在这种特殊情况下，我们不需要调用 `perl_run`，因为我们设置了 `pl_exit_flag` `PERL_EXIT_DESTRUCT_END`，它会在 `perl_destruct` 中执行块。

如果你想向 Perl 子程序传递参数，可以使用 `call_argv` 向 `NULL-args` 中添加字符串。对于其他数据类型，或者为了检查返回值，你需要操作 Perl 栈。这在“从你的 C 程序中操纵 Perl 栈”中有所演示。

## 在你的 C 程序中评估 Perl 语句

Perl 提供了两个 API 函数来评估 Perl 代码段。它们是 `perlapi` 中的 `eval_sv` 和 `perlapi` 中的 `eval_pv`。

可以说，这些是你从 C 程序中执行 Perl 代码片段时唯一需要的例程。代码可以很长；它可以包含多个语句；它可以利用 `perlfunc` 中的 `use`、`perlfunc` 中的 `require` 以及 perl 中的 `do` 来包含外部文件。

`eval_pv` 让我们评估单个字符串并将变量转换为类型。此程序 `string.c` 执行了三个 Perl 字符串，从第一个提取 int，第二个提取字符串，第三个提取 char。

```c
#include <perl.h>

static PerlInterpreter *my_perl;

int main (int argc, char **argv, char **env) {

    char *args[] = { "-e", "0" };

    PERL_SYS_INIT3(&argc,&argv,&env);

    my_perl = perl_alloc();

    perl_construct(my_perl);

    perl_parse(my_perl, NULL, argc, argv);

    pl_exit_flags |= PERL_EXIT_DESTRUCT_END;

    perl_run(my_perl); /* 将 $a 视为整数 */

    eval_sv("$a=3;a=2"); printf("%d\n", (int)eval_sv("$a", 0))); // 将 $a 视为字符串 */

    eval_sv("$a=3;a=2"); printf("%s\n", (char*)eval_sv("$a", 0))); /* 将 $a 视为字符串 */

    eval_sv("$a=reverse($a)"); printf("%s\n", (char*)eval_sv("$a", 0)));

    perl_free(my_perl);

    PERL_SYS_TERM();

}
```

所有名称带有 `sv` 的奇怪函数都会将 Perl 标量转换为类型。它们设计在 `perlapi` 中。

如果你编译并运行 `string.c`，你会看到结果：
`SvIV()` 创建 int，
`SvNV()` 创建浮点数，`SvPV()` 创建字符串：`a = 9.56`

在上面的示例中，我们创建全局变量来临时存储 `eval_expression` 的计算值。大多数情况下，更好的策略是从 `eval_pv()` 获取返回值。

```c
SV *val = eval_pv("reverse($a)", TRUE);

printf("%s\n", (char*)val);
```

通过这种方式，通过不创建全局变量避免命名空间污染并简化了代码。

## 从你的 C 程序执行匹配和替换

`eval_sv()` 函数评估 Perl 代码字符串，因此我们可以定义使用它来“专门化”匹配和替换的函数：`match()`、`substitute()` 和 `matches`。

`int match(SV *string, char *pattern);`
给定一个字符串和一个模式（例如 `/class/` 或 `/m\w*\b/`），在你的 C 程序中可能表现为 `"/\b\w*\b/"`，如果字符串匹配模式则返回 1，否则返回 0。

`int substitute(SV **string, char *pattern);`
给定一个 sv 指针和一个操作（例如 `s/bob/` 或 `tr[A-Z][a-z]`），`substitute()` 修改 SV 内部的字符串，返回替换次数。

给定一个 sv、一个模式和一个空 SV 指针，`match()` 在列表上下文中评估 `$string =~pattern` 并填充匹配数组元素，返回匹配次数。

这里有一个示例程序 `match.c`，它使用了三处（长行在这里已折行处理）：

```c
#include <perl.h>

static PerlInterpreter *my_perl;

/**
eval_sv(code, error_check) 类似于栈的返回值
*/

int my_sv(SV *sv, sv2_croak_on_error) {
    PUSHMARK(sv);
```
