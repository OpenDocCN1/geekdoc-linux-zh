
yacc 将上下文无关文法转换为简单自动机的表，该自动机执行 LALR 解析算法。LALR（前向 LR）解析是 LR 解析的一种能力较弱的变体，产生的解析表小得多。文法可以发现 LR 文法的歧义。你可以使用指定的优先级规则来消除歧义。

你必须用 C 编译器编译 `y.tab.c` 文件以生成 `yparse(1)` 函数。然后使用 `ylex(1)` 词法分析器程序以及 `main()` 和 `yerror(1)` 错误处理程序加载此程序。你必须提供这些程序。`lex(1)` 命令用于通过 yacc 创建词法分析器。

要使用 yacc 生成解析器，请指定描述输入数据流以及解析器如何处理数据的文法文件。

文法文件包含输入结构中描述的规则、识别到这些规则时调用的代码以及一个基础输入的子程序。

两个相邻的双百分号 `%%` 分隔文法文件的每个部分。为了使文件更易读，请将 `%%` 独占一行。完整的文法文件具有以下结构：

```
declarations
%%
rules
%%
programs
```

声明部分可以是空的。如果你省略了程序部分，也省略第二组 `%%`。最小的 yacc 文法文件具有以下结构：

```
%%
rules
```

yacc 忽略文法文件中的空格、制表符和换行符。你可以使用这些字符使文件更易读。但是，你不应在名称或保留符号中使用空格、制表符或换行符。

yacc 使用文法文件中的信息生成控制输入过程的解析器。解析器调用输入过程。

### Options

- `-c filename`
  从 `filename` 获取 C 源文本。指定程序中引用抽象字符串的命名数组。默认数组名称为 `xstr`。

- `-d filename`
  生成包含 `#define` 语句的 `tab.h` 文件。默认是 `yacc.h`。

- `-t`
  默认编译运行时调试代码。不带调试代码生成的程序尺寸更小，执行速度稍快。运行时调试代码始终受条件控制。默认情况下，编译 `y.tab.c` 时不包含代码。

- `-p sym-prefix`
  对所有外部名称使用 `sym-prefix` 前缀。受影响的名称包括函数 `yyparse()`, `ylex()`, 和 `yyerror()`。

- `-Q[y|n]`
  将版本信息放在 `tab.c` 中。此选项让你知道是用哪个版本的 yacc 构建该文件。`-Q` 选项（默认）不写版本信息。

- `-v`
  准备 `y.output`，其中包含解析表中歧义的描述以及由歧义产生的冲突报告。

- `-V`
  在标准错误输出上打印 yacc 的版本信息。

### Operands

`file`
包含创建解析器所需指令的文件路径。

## Examples

通过向 `cc` 提供库搜索操作数获取 yacc 库。以下示例使用了 yacc 库 main。

```
castle% cc y.tab.c -ly
```

`lex` 库和 yacc 库都包含 main。以下示例访问了 yacc main 并确保首先搜索 yacc 库以便使用。

```
example% cc y.tab.c lex.yy.c -ly -11
```

# yacc

## 1571

对所有外部名称使用 `sym-prefix` 前缀。受影响的名称包括函数 `yyparse()`, `ylex()`, 和 `yyerror()`。

```c
/* 如果以下解析器是由 lex 创建的，则
应用程序必须小心确保 LC_CTYPE
和 LC_COLLATE 被设置为 POSIX 区域设置。 */
(void) yyparse();
    return (0);
}

#include <stdio.h>
int yerrror(const char *msg)
{
    (void) fprintf(stderr, "%s\n", msg);
    return (0);
}
```

以下示例从 `grammar.y` 文件中提取 yacc 规则并将输出放入：

y `y.tab.c`。

```
castle% yacc grammar.y
```

以下示例从 `grammar.y` 文件中提取 yacc 规则并将输出放入

y in.tab.c。它还会生成 `y.tab.h` 文件，该文件包含为 `grammar.y` 文件中定义的标记的 C 风格 `#define` 语句。

```
castle% yacc -d grammar.y
```

## 环境变量

参阅 `environ(5)` 以获取有关影响 yacc 执行的以下环境变量的描述：`LC_CTYPE`、`LC_MESSAGES` 和 `NLSPATH`。

yacc 可以处理扩展 UNIX 编码 `EUC` 的主要和补充字符集作为单令牌符号。`EUC` 编码只能是单字符引号的终端符号。yacc 期望 `yylex()` 为这些单令牌符号返回宽字符 `wchar_t` 值。

## 退出状态

- `0` 成功完成。
- `>0` 发生错误。

## 文件

- `y.output` 生成的解析器的状态转换。
- `y.tab.c` 生成的解析器的源代码。
- `y.tab.h` 生成的解析器的头文件。
- `yacc.acts` 临时文件。
- `yacc.debug` 临时文件。
- `yacc.tmp` 临时文件。
- `yaccpar` 用于 C 程序的解析器原型。

# yes 1573

### 属性

参阅 `属性(5)` `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNwtool |

# 另

- `lex(1)`, `cc(1B)`, `attributes(5)`, `environ(5)`

编程实用程序

### 诊断

标准错误输出将报告归约-归约（reduce-reduce）和移位-归约（shift-reduce）冲突。你可以在 `y.output` 文件中找到更详细的报告。同样，如果错误无法从起始符号到达，也会报告此类实例。

# yes — 生成重复的肯定输出

### 概览

`/bin/yes [expletive...]`

### 描述

你可以使用 `yes` 命令（该命令是 Solaris 9 操作系统新增）对需要交互式响应的程序进行程序响应。

使用 `yes` 命令重复输出 `y`，或者如果你指定了词句，则在其后面重复紧跟一个换行符。多个参数用空格分隔输出并以换行符结束。要终止，请输入中断字符。

### 示例

以下示例显示了 `yes` 命令的默认输出。

```
mpoke% yes
y
y
y
...
Ctrl-C
mpoke%
```

以下示例显示了当你指定词句 `goodgrief` 时，`yes` 命令的输出。

```
mpoke% yes goodgrief
goodgrief
goodgrief
goodgrief
...
```

## 1574

# ypcat

Ctrl-C

mopoke%

### 属性

参阅 `属性(5)` 获取以下属性的描述。

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNmesu |

# 另

- `- attributes(5)`

# ypcat — 打印 NIS 数据库中的值

### 概览

```
/usr/bin/ypcat [-kx] -d ypdomain mname
```

### 描述

`ypcat` 命令打印由 `mname` 指定的 NIS 名称服务映射中的值，`mname` 可以是映射名称也可以是映射别名。由于 `ypcat` 使用 NIS 网络服务，你不需要指定 NIS own。

参阅 `ypfiles(4)` 获取 NIS 名称服务的概览。

### 选项

- `-d ypdomain`
  指定一个默认域以外的域。

- `-k` 显示那些值为为空或键不是值的一部分的映射的键。从 `/etc` 中的文件派生且且具有 ASCII 值的映射都不属于此类。

- `-x` 显示映射别名。

### 示例

以下示例显示了在未连接 NIS+ 网络的系统上运行 `ypcat -x` 命令的输出。

```
castle% ypcat -x
Use "passwd" for map "passwd.byname"
Use "group" for map "group.byname"
Use "networks" for map "networks.byaddr"
Use "hosts" for map "hosts.byname"
Use "protocols" for map "protocols.bynumber"
Use "services" for map "services.byname"
Use "aliases" for map "mail.aliases"
```

# ypmatch 1575

Use "ethers" for map "ethers.byname"

castle%

### 属性

参阅 `属性(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNwhisu |

# 另
