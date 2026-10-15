
# 第 5 章 • 迁移 AIX

## 5.5.2 链接器：AIX 到 Linux 的参考

此外，Linux 和 AIX 处理符号解析的代码不同。在 AIX 中，当链接器解析符号时，它无论是否需要，都会从归档中获取所有可用代码。在 Linux 中，链接器只获取它需要的部分。缺点是，在 Linux 中，你可能需要在命令行上多次列出归档（与 AIX 不同，AIX 只需列出一次）。这迫使 Linux 链接器多次搜索归档，以便在链接行后续列出的对象文件中发现额外的符号。

如你所见，如果你习惯了 AIX 构建归档和共享对象的链接器加载器机制，那么在 Linux 平台上构建之前，你必须对构建环境进行一些更改。AIX 用户在迁移到 Linux 时需要注意的额外差异包括：

- 在 AIX 中，因为归档可以包含共享模块反之亦然，对于同时包含共享对象和常规归档的归档，共享对象必须从链接行（`ld` 命令）中分离，并构建为带有 `.so` 扩展的可分离共享对象。包含共享对象的 `.o`（对象）文件也是如此。

- 通过 `-l` 参数传递给 Linux 链接器的共享对象必须移动到对象文件列表之后的链接行（`ld` 命令），并带上全名的共享库（例如 `libshobj.so`）。

- 为了解析符号，归档可能需要在链接行上列出多次，位于触发模块的下一个层级。

尽管 GNU 链接器（`ld`）拥有大量的参数，但在从 AIX 迁移时，你只需要关注少数几个。表 5-4 突出了最常用参数中的某些细微差异，在从 AIX 迁移到 Linux 时，根据你的目标这些是必要的。

### 表 5-4：AIX 和 Linux 链接器开关对比表

| AIX | Linux | 描述 |
| --- | --- | --- |
| `-bexpall` | `-E --export-dynamic` | 创建动态链接的可执行文件时，将所有符号添加到动态符号表。 |
| `-bmaxdata:<size>` | `-Gvalue --gpsize=value` | 设置由 GP 寄存器优化的对象最大大小。这对于 MIPS ECOFF 等支持将大小对象放入不同段的对象文件格式才有意义。对于其他对象文件格式忽略此项。 |
| `-eLabel` | `-e entry --entry=entry` | 使用 `entry` 作为程序开始执行的显式符号，而不是默认入口点。 |
| `-bdynamic or -bshared` | `-Bdynamic -dy -call_shared or -Wl -brt -shared` | 链接动态库。此选项的不同变是为了兼容各种系统。你可以在命令行上多次使用此选项：它会影响其随后的 `-1` 选项的库搜索。 |
| `-bM:SRE or -brtl or -G` | `-shared -shareable -larchive` | 创建一个可重入共享库（运行时链接）。将归档 `.a` 添加到文件列表中。此选项可以使用多次。 |
| `-Z` | `-Y` | 指定库名称的搜索路径。 |
| `-L` | `-rpath` | 指定运行时的搜索路径。 |
| `-L` | `-l` | 在指定的目录搜索库。 |

* 使用等效的 Linux 解决方案需谨慎。列表仅供参考，不作为官方建议。在实施之前请调查其可行性。

## 5.6 AIX Linux 共享库创建

尽管所有 UNIX 实现都提供了通用的链接和加载功能，但创建方式存在细微差异。在 AIX 中，共享库可以是对象文件或归档文件成员。归档库可以包含多个成员，其中一些是共享模块，另一些是普通对象文件。此外，在 AIX 构建共享库后，库就可以使用了。在 Linux 中并非如此。

在 Linux 中，共享库只包含普通对象文件和归档。而且共享库不能是归档的成员。此外，AIX 和 Linux 之间的主要区别在于，在 AIX 中构建库后，最后一步你必须将库通过一个版本工具将其链接到版本号。只有这样你的库才能使用。

如果你习惯了 AIX 构建库的方式，Linux 库版本对你来说是一个新概念。第 3 章详细讨论了库版本。AIX 用户必须确保完全理解第 3 章中关于 Linux 库版本的内容，并在所有要迁移到 Linux 的共享库中实现库版本控制。

## 5.7 动态加载

GNU 链接器（`ld`）旨在涵盖广泛的情况，并尽可能与其他链接器兼容。因此，你有许多其他选择来控制它的行为。但如果你希望你的应用程序保持可移植性，可以使用 `GNUtool`。`GNUtool` 是一个通用支持脚本，将使用库的复杂性（例如创建和安装库）隐藏在一致的可移植接口之后。在 Linux 上，`GNUtool` 构建在标准库（`glib`）之上。更多选项和用法请参考在线文档。

### 表 5-5：AIX 与 Linux 之间的动态加载例程

| AIX | Linux | 说明 |
| --- | --- | --- |
| `dlopen` | `dlopen` | 将模块动态加载到调用进程中。 |
| Flags: `RTLD_LAZY` | Flags: `RTLD_LAZY` | |
| `RTLD_NOW` | `RTLD_NOW` | |
| `RTLD_GLOBAL` | `RTLD_GLOBAL` | |
| `RTLD_LOCAL` | `RTLD_LOCAL` | |
| `RTLD_MEMBER` | `RTLD_NODELETE` | |
| `RTLD_NOAUTODEFER` | `RTLD_NOLOAD` | |
| | `RTLD_BINDING_MASK` | |
| `dlsym` | `dlsym` | 在用 `dlsym` 加载的模块中查找符号的位置。 |
| Handles: `RTLD_DEFAULT` | Handles: `RTLD_DEFAULT` | |
| `RTLD_NEXT` | `RTLD_NEXT` | |
| `RTLD_MYSELF` | | |
| `dlerror` | | 返回一个指向上次 `dlopen`、`dlsym` 或 `dlclose` 错误的信息的指针。 |
| `dlclose` | `dlclose` | 关闭并卸载由 `dlopen` 子程序加载的模块。 |
| `dladdr` | `dladdr` | 将地址转换为符号信息。 |
| `DI_info_structure`: | `DI_info_structure`: | |
| `const char *dli_fname;` | `const char *dli_fname;` | |
| `void *dli_fbase;` | `void *dli_fbase;` | |
| `const char *dli_sname;` | `const char *dli_sname;` | |
| `void *dli_saddr;` | `void *dli_saddr;` | |
| `size_t dli_size;` | `size_t dli_size;` | |
| `int dli_type;` | | |
| None | `dlvsym` | (仅限 Linux) 功能与 `dlsym()` 相同，但接受版本字符串作为额外参数。 |

## 5.8 AIX 与 Linux 之间的模板实例化差异

用于 DL 库的 dl 函数（`dlopen`、`dlclose`、`dladdr` 等）在 Linux 中的行为与 AIX 相同。从 AIX 迁移到 Linux 应该是无缝的。在 Linux 中，为了启用 DL 功能，应用程序必须与 `libdl.so` 库链接（`-ldl`）。第 3 章列出了如何在 Linux 上使用 DL 的示例。

C++ 模板是第一个要求环境提供比通常 UNIX 系统更多智能的语言特性。通过某种方式，编译器和链接器必须确保每个需要的模板实例在可执行文件中恰好出现一次，或者完全不出现。今天编译器使用的流行方法是使用一个仓库来存储模板实例化，并在链接前的编译过程最后一步与其他所有代码一起编译。这被称为 CFront 模型；你让编译器处理仓库的管理和编译。

AIX 通过 `-qtempinc` 和 `-templateristry` 参数处理这种样式。`-qtempinc` 参数在当前工作目录下创建一个 `tempinc` 目录，而 `-templateristry` 则在当前工作目录下创建一个 `templateristry` 文件。这两个区域都用于存储模板实例化方法，以便编译器在链接阶段之前对其进行收集和编译。

GNU 使用 `-frepo` 参数处理这种样式。该参数在当前工作目录下创建一个扩展名为 `.rpo` 的文件。它同样持有了模板实例化方法，供编译器在链接阶段之前的最后一步使用。这是将模板代码从 AIX 迁移到 Linux 最简单且最推荐的方法。然而，除了参数更改，在 Linux 中包含模板代码的方式与 AIX 有一些细微差异。以下小节将检查这些差异并解决一些常见问题。

### 5.8.1 使用 `#pragma` 或 `#include`

在 AIX 中，使用模板代码的源代码通常只包含模板头以获取完整的模板实现。示例 5-2 显示了 AIX 下的模板实例化。

#### 示例 5-2：AIX 模板

```
stack.h

#ifndef STACK_H

#define STACK_H

#if __TEMPINC__

#pragma implementation ("stack.C")

#endif

template <class T> class stack

{

private:

    T* v;
```
