
声明部分可以为空。如果你省略了程序部分，也省略第二组 `%%`。最小的 `yacc` 文法文件具有以下结构。

`yacc` 忽略文法文件中的空格、制表符和换行符。你可以这些字符使文件易于阅读。但是，你不应该在名称或保留符号中使用空格、制表符或换行符。

`yacc` 使用文法文件中的信息生成控制输入过程的解析器。该解析器调用输入子程序（词法分析器）从输入流中提取标记（`tokens`）。解析器使用文法文件中的结构规则组织标记。当解析器识别出其中一条文法规则时，它会执行该规则对应的用户代码动作。动作返回结果并使用其他动作返回的值。

> 注意 — 由于文件名是固定的，在给定时间内给定目录下只能运行一个 `yacc` 进程。

## 选项

- `-b file-prefix` 使用 `file-prefix` 代替 `y` 作为所有输出文件的前缀。`y.tab.c` 文件、`y.tab.h` 头文件（在指定 `-d` 时创建）以及 `y.output` 描述文件（在指定 `-v` 时创建）将改为 `file-prefix.tab.c`、`file-prefix.tab.h` 和 `file-prefix.output`。
- `-d` 生成 `y.tab.h` 文件，其中包含 `#define` 语句，将 `yacc` 用户分配的标记代码与用户声明的标记名称关联起来。这种关联允许 `y.tab.c` 以外的源文件访问标记代码。

## `yacc`

- `-l` 指定 `y.tab.c` 产生的代码不包含任何 `#line` 结构。仅在完全调试文法和关联动作后才使用此选项。
- `-P parser` 指定你选择的解析器而不是 `/usr/ccs/bin/yaccpar`。例如，你可以指定：

```
castle% yacc -P -myparser parser.y
```

- `-p sym-prefix` 在 `yy` 内部使用 `sym-prefix` 作为 `yacc` 产生的所有外部名称的前缀。受影响的名称包括函数 `yparse()`、`yyylex()`、`yerror()` 以及变量 `yylval`、`yyychar` 和 `yydebug`。（在本其余内容中，引用的符号以默认值引用仅为了符号方便。本地名称也可能受到 `-p` 选项的影响；但 `-p` 选项不影响 `yacc` 生成的 `#define` 符号。）
- `-Q[y|n]` 在 `y.tab.c` 中放入版本信息。此选项允许知道哪个版本的 `yacc` 构建了该文件。`Q` 选项（默认）不写版本信息。
- `-t` 默认编译调试代码。不带运行时调试代码的程序尺寸更小，执行速度也略快。如果指定 `-d`，则包含运行时调试代码。`-d` 选项对于调试解析器很有用。`y.output` 文件包含解析器的详细报告。
- `-V` 在标准错误上打印版本信息。

### 操作数

- `-a file` 文法文件的名称。
- `-b file-prefix` 使用 `file-prefix` 代替 `y` 作为所有输出文件的前缀。
- `-d` 生成 `y.tab.h` 文件，其中包含 `#define` 语句将 `yacc` 用户分配的标记代码与用户声明的标记名称关联起来。
- `-P parser` 指定你选择的解析器而不是 `/usr/ccs/bin/yaccpar`。
- `-p sym-prefix` 在 `yy` 内部使用 `sym-prefix` 作为 `yacc` 产生的所有外部名称的前缀。
- `-Q[y|n]` 在 `y.tab.c` 中放入版本信息。
- `-t` 默认编译调试代码。
- `-v` 显示进度报告。
- `-V` 在标准错误上打印版本信息。

使用 `yacc` 命令生成解析器，请指定一个描述输入数据流以及解析器如何处理数据的文法文件。

# 1518 yacc

文法文件包括输入结构中描述的规则、识别到这些规则时调用的代码，以及执行基本输入的子程序。

两个相邻的双百分号 `%%` 分隔文法文件的每个部分。为了方便阅读文法，请将 `%%` 独占一行。一个完整的文法文件结构如下：

```
declarations

%

rules

%%

programs
```

声明部分可以为空。如果你省略了程序部分，也省略第二组 `%%`。最小的 `yacc` 文法文件具有以下结构。

`yacc` 忽略文法文件中的空格、制表符和换行符。你可以这些字符使文件易于阅读。但是，你不应该在名称或保留符号中使用空格、制表符或换行符。

`yacc` 使用文法文件中的信息生成控制输入过程的解析器。该解析器调用输入子程序（词法分析器）从输入流中提取标记。解析器使用文法文件中的结构规则组织标记。当解析器识别出其中一条文法规则时，它会执行该规则对应的用户代码动作。动作返回结果并使用其他动作返回的值。

> 注意 — 由于文件名是固定的，在给定时间内给定目录下只能运行一个 `yacc` 进程。

## 选项

- `-b file-prefix` 使用 `file-prefix` 代替 `y` 作为所有输出文件的前缀。`y.tab.c` 文件、`y.tab.h` 头文件（在指定 `-d` 时创建）以及 `y.output` 描述文件（在指定 `-v` 时创建）将改为 `file-prefix.tab.c`、`file-prefix.tab.h` 和 `file-prefix.output`。
- `-d` 生成 `y.tab.h` 文件，其中包含 `#define` 语句将 `yacc` 用户分配的标记代码与用户声明的标记名称关联起来。这种关联允许 `y.tab.c` 以外的源文件访问标记代码。

## `yacc`

- `-l` 指定 `y.tab.c` 产生的代码不包含任何 `#line` 结构。仅在完全调试文法和关联动作后才使用此选项。
- `-P parser` 指定你选择的解析器而不是 `/usr/ccs/bin/yaccpar`。例如，你可以指定：

```
castle% yacc -P -myparser parser.y
```

- `-p sym-prefix` 在 `yy` 内部使用 `sym-prefix` 作为 `yacc` 产生的所有外部名称的前缀。受影响的名称包括函数 `yparse()`、`yyylex()`、`yerror()` 以及变量 `yylval`、`yyychar` 和 `yydebug`。（在本其余内容中，引用的符号以默认值引用仅为了符号方便。本地名称也可能受到 `-p` 选项的影响；但 `-p` 选项不影响 `yacc` 生成的 `#define` 符号。）
- `-Q[y|n]` 在 `y.tab.c` 中放入版本信息。此选项允许知道哪个版本的 `yacc` 构建了该文件。`Q` 选项（默认）不写版本信息。
- `-t` 默认编译调试代码。不带运行时调试代码的程序尺寸更小，执行速度也略快。如果指定 `-d`，则包含运行时调试代码。`-d` 选项对于调试解析器很有用。`y.output` 文件包含解析器的详细报告。
- `-V` 在标准错误上打印版本信息。

### 操作数

- `-a file` 文法文件的名称。
- `-b file-prefix` 使用 `file-prefix` 代替 `y` 作为所有输出文件的前缀。
- `-d` 生成 `y.tab.h` 文件，其中包含 `#define` 语句将 `yacc` 用户分配的标记代码与用户声明的标记名称关联起来。
- `-P parser` 指定你选择的解析器而不是 `/usr/ccs/bin/yaccpar`。
- `-p sym-prefix` 在 `yy` 内部使用 `sym-prefix` 作为 `yacc` 产生的所有外部名称的前缀。
- `-Q[y|n]` 在 `y.tab.c` 中放入版本信息。
- `-t` 默认编译调试代码。
- `-v` 显示进度报告。
- `-V` 在标准错误上打印版本信息。

## `ypcat` — 打印 NIS 数据库中的值

### 概要

```
/usr/bin/ypcat [-kx][-d ypdomain] mname
```

## 描述

`ypcat` 命令打印由 `mname` 指定 NIS 命名服务映射中的值，其中 `mname` 可以是映射名称，也可以是映射别名。由于 `ypcat` 使用 NIS 网络服务，因此你不需要指定 NIS 服务器。有关 NIS 命名服务的概述，请参阅 `ypfiles(4)`。

## 选项

- `-d ypdomain` 指定一个默认域之外的域。
- `-k` 显示那些值为为空或键不属于键键的映射的键。所有源自 `/etc` 中具有 ASCII 版本的文件的派生映射都不属于此类。
- `-x` 显示映射的别名。

## 示例

以下示例显示了在未连接到 NIS 网络的系统上运行 `ypcat -x` 命令的输出。

```
castle@ ypcat -x

Use "passwd" for map "passwd.byname"

Use "group" for map "group.byname"

Use "networks" for map "networks.byaddr"

Use "hosts" for map "hosts.byname"

Use "protocols" for map "protocols.byname"

Use "services" for map "services.byname"

Use "aliases" for map "mail.aliases"

Use "ethers" for map "ethers.byname"

castle@
```
