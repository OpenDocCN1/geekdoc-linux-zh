
`gcc -shared -o bar.so bar.c -fPIC -Wl,--version-script=bar.map`

```
bar.map 文件可以包含如下文本：
```

```
{
  global: index;
  local: *;
};
```

### 4.4.2 链接器工具

Solaris 拥有各种链接器工具，如 `elfdump`, `l`, `nm`, `dump`, `ldd`, `pvs` 和 `elf`。GNU binutils 提供了类似的工具。有关 GNU binutils 的更多信息，请参考第 2 章。

表 4-7 提供了 Solaris 链接器工具及其 Linux 上等效工具的对比。

### 表 4-7 链接器工具

| Solaris 工具 | Linux 等效工具 |get |
|--- | --- | --- |
| elfdump | readelf, objdump | 转储对象文件的选择部分 |
| l | N/A | 运行时接口的链接分析 |
| nm | nm | 打印对象文件的名称列表 |
| dump | objdump, readelf | 转储对象文件的选择部分 |
| ldd | ldd | 列出可执行文件或共享对象的动态依赖 |
| pvs | readelf -V | 显示动态对象的内部版本信息 |

### 4.4.3 共享库

Linux 目前使用 ELF（可执行链接格式）二进制格式。生成应用程序和共享库之间的唯一区别在于最后的链接命令。GNU ld 的 `-shared` 选项告诉链接器创建共享库而不是应用程序。

在 Solaris 中创建共享库：

```
cc -o libfoo.so -G -K pic foo.c
```

在 Linux 中创建共享库：

```
gcc -o libfoo.so -shared -fpic foo.c
```

在 Solaris 中，当人们想要在共享对象本身中记录 soname 时，使用 `-h` 选项：

```
cc -o libfoo.so -G -K pic -h libfoo.so.1 foo.c
```

Linux 上的等效方法是：

```
gcc -o libfoo.so -shared -fpic -W1,-soname=libfoo.so.1 foo.c
```

或者

```
gcc -o libfoo.so -shared -fpic -W1,-libfoo.so.1 foo.c
```

## 4.4 链接器

Solaris 中的 `dump` 命令等于 Linux 中的 `objdump` 命令。以下示例显示了如何使用 Linux 中的 `objdump` 命令显示 soname 记录：

```
#objdump -x libGLU.so.1.3 | grep SONAME
SONAME  libGLU.so.1
```

### 4.4.4 库版本控制

在第 3 章“分析”中，我们提供了关于 Linux 如何实现库版本控制的信息。虽然外部版本是在 Linux 中实现的，但 Solaris 的版本控制类似。

### 4.4.5 动态链接器

Linux 目前使用 ELF（可执行链接格式）二进制格式。生成应用程序和共享库之间的唯一区别在于最后的链接命令。GNU ld 的 `-shared` 选项告诉链接器创建共享库而不是应用程序。

Solaris 中的默认区域（locale）所示：

```
$ locale
LANG="C"
LC_CTYPE="C"
LC_NUMERIC="C"
LC_TIME="C"
LC_COLLATE="C"
LC_MONETARY="C"
LC_MESSAGES="C"
LC_ALL="C"
```

附录 A 中的表 A-1，“Solaris 到 Linux 的参考表” 提供了 Solaris 和 Linux 之间国际化 API 的比较。

## 4.7 Make

Linux 中的 make 开发工具是 GNU Make。截至本文编写，GNU Make 的最新版本是 3.8，本节即基于该版本。GNU Make 的页面位于 www.gnu.org/software/make/。请注意，Solaris 上也提供 GNU Make 3.8，并可以从 www.istec.com/sunfreeware/ 下载。将构建环境从 Solaris 迁移到 Linux 意味着使用 GNU Make，并确保用于构建应用程序的 Makefile 被正确移植到 POSIX.2 标准。Solaris 和 GNU Makefile 语法之间有很多相似之处。然而，仍然存在一些差异，本节将涵盖这些差异。需要注意的第一个差异是命令行开关。表 4-9 显示了 Solaris 和 GNU Make 命令行开关的比较。

### 表 4：Make 命令行开关

| Solaris 标志 | GNU 等效项 | 说明¹⁵ |
|---|---|---|
| -d | -d | 显示 Make 选择重新构建目标的原因。Make 会显示所有较新的依赖项。此外，Make 还会显示从 `MAKEFLAGS` 环境变量读取的选项。 |
| -dd | N/A | 极其详细显示依赖检查和处理。 |
| -D | N/A | 显示读取的 Makefile 文本。 |
| -DD | N/A | 显示 Makefile 文本、make.rules 文件以及所有隐藏依赖报告。 |
| -e | -e | 环境变量覆盖 Makefile 内部赋值。 |
| -f make | -fmakefile | 使用指定的 Makefile。 |
| -i | -i | 忽略命令返回的错误代码。 |
| -k | -k | 当规则返回非零错误状态或当 make 找不到规则时，放弃对当前目标的工作，但继续处理不依赖于它的其他依赖分支。 |
| -K statefile | N/A | 使用状态文件 statefile。 |
| -n | -n | 不执行模式。打印命令但不执行它们。即使是以 @ 开头的行也会打印。但是，如果命令行中包含对 `$(MAKE)` 宏的引用，则该行始终会被执行。在 POSIX 模式下，以 + 开头的行会被执行。 |
| -p | -p | 打印完整的宏定义和目标描述。 |
| -P | N/A | 仅报告依赖，而不是构建它们。 |
| -q | -q | 询问模式。 |
| -r | -r | 不读取默认的 Makefile /usr/share/lib/make/make.rules。 |
| -s | -s | 静默模式。在执行命令前不打印命令行。等同于特殊函数目标 SILENT:。 |
| -S | -S | 撤销 -k 选项的效果。当命令返回非零退出状态时停止处理。 |
| -t | -t | 触摸目标文件（使其保持更新）而不是执行它们的规则。警告：当文件由多个人维护时，这可能是危险的。makefile 中会出现 .KEEP_STATE: 目标，此选项更新状态文件，就像规则已经执行过一样。在 POSIX 模式下，以 + 开头的行会被执行。 |
| -v | N/A | 将 make 置于 SysV 模式 |

### 4.7.1 C++ 的内置 Makefile 变量

在 Solaris 原生 Make 中，指定默认 C++ 编译器的内置 make 变量是 `CCC`，而 GNU Make 中是 `CXX`。同样，默认编译器标志从 `CCFLAGS` 变为 `CFLAGS`。

### 4.7.2 库依赖

在 Solaris 上，`lib(( ))` 符号的目标名称指向随机对象库的成员，该成员定义了名为 symbol 的入口点。GNU Make 的等效项是 `lib(file.o)`。

### 4.7.3 空规则

空规则是指未指定命令的后缀指定。要在 GNU Make 中指定空规则，请在依赖项后紧跟一个分号：

```
Solaris: .c.a:
GNU: Make:.c.a;
```

### 4.7.4 当前目标

在 Solaris makefiles 中，符号 `$$` 在依赖列表中用于引用当前目标：

```
Solaris:    $(targets):$$.o
```

在 GNU Make 中，你必须使用如下：

### 4.7.5 SCCS 和 RCS 文件

处理 System V makefiles 以支持包含 ~ 的 SCCS 文件的后缀规则不受 GNU Make 识别。后缀 `.c~o` 会从 SCCS 文件 s.n.c 创建文件 x.o。GNU Make 通过应用两个用于从 SCCS 或 RCS 提取的模式规则结合通用规则来区别处理 SCCS 和 RCS 文件。

### 4.7.6 条件宏赋值

```
$(targets) := special_flags = -g
```

在 Solaris 上，`$(targets)` 中的任何目标都会被处理，并将 `$(special_flags)` 设置为 `-g`。Linux 上的对应写法是：

```
$(targets) : special_flags= -g
```

### 4.7.7 模式替换宏

```
$(targets) := special_flags = -g
```
