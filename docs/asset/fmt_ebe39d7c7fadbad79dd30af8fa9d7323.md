
产生：`Hello Miss A, aged 14.5`

通过使用字段说明符，你可以对打印的项目获得更大的控制。这些说明符扩展了转换说明符，包含了对输出间距的控制。常见的用途是设置点数的小位数或设置字符串周围的空间。

字段说明符紧跟在转换说明符的 `%` 后面。下表包含了转换说明符的一些示例。为了让情况更清晰，我们使用竖线显示输出的边界。

| Format | Argument | Output |
|---|---|---|
| `%10s` | `"Hello"` | ` Hello` |
| `%10s` | `"Hello"` | ` Hello` |
| `%10d` | `1234` | ` 1234` |
| `-10d` | `1234` | `1234 ` |
| `%01d` | `1234` | `000001234` |
| `%10.4f` | `12.34` | `12.3400` |

所有这些示例都在 10 个字符的字段中打印。注意，负字段宽度意味着项目在字段内左对齐。变量字段宽度由星号（`*`）表示。在这种情况下，下一个参数是用于宽度的。前导零表示项目带有前导零写入。根据 `POSIX` 规范，`printf` 不截断字段；相反会扩展字段以适应。因此，例如，如果我们尝试打印一个比字段长的字符串，字段会增长：

| Format | Argument | Output |
|---|---|---|
| `%10s` | `"HelloTherePeeps"` | `HelloTherePeeps` |

`printf` 函数返回一个整数，即写入的字符数。在字符串的情况下，这不包括终止的空字符。发生错误时，这些函数返回负值并设置 `errno`。

## scanf, fscanf, 和 sscanf

`scanf` 函数族的工作方式与 `printf` 组类似，不同在于这些函数是从流中读取项，并将值放入作为指针参数传递的变量地址中。它们以相同的方式使用格式化字符串来控制输入转换，并且许多转换规范是相同的。

```c
#include <stdio.h>

int scanf(const char *format, ...);

int fscanf(FILE *stream, const char *format, ...);

int sscanf(const char *s, const char *format, ...);
```

用于存储 `scanf` 函数中扫描值的变量必须是正确的类型，并且它们与格式字符串精确匹配，这非常重要。如果你的内存被损坏且程序可能崩溃，你将不会得到任何编译器错误，但如果你足够幸运，你可能会得到一个警告！

`scanf` 及其类函数的格式字符串同时包含普通字符和转换规范，就像 `printf` 一样。然而，普通字符被用于指定输入中必须存在的字符。

这里有一个简单的示例：

```c
int num;

scanf("Hello %d", &num);
```

只有当标准输入中的后续五个字符与 `"Hello"` 时，此 `scanf` 调用才会成功。然后，如果后续字符形成一个可识别的十进制数字，该数字将被读取并赋值给变量 `num`。格式字符串中的空格告诉 `scanf` 忽略转换规范之间的所有空白字符（空格、制表符、换页和换行符）。这意味着，给定以下两种输入之一，`scanf` 调用都将成功并将 `1234` 放入变量 `num` 中：

```
Hello      1234
Hello1234
```

在开始转换时，输入中的空白字符通常也会被忽略。这意味着格式字符串 `%d` 将继续读取输入，跳过空格和换行符，直到找到数字序列。如果预期的字符不存在，则转换失败，`scanf` 返回。

> 如果你不小心，这可能会导致问题；如果你在扫描整数时在输入中留下了非数字字符，你的程序可能会发生无限循环。

其他转换规范还包括：

- `%d`: 扫描十进制整数
- `%o, %x`: 扫描八进制、十六进制整数

## 处理文件

- `%f, %e, %g`: 扫描浮点数
- `%c`: 扫描字符（不跳过空白字符）
- `%s`: 扫描字符串
- `%[]`: 扫描字符集（见下文）
- `%`: 扫描 `%` 字符

像 `printf` 一样，`scanf` 转换也可能有一个字段宽度来限制消耗的输入量。大小指定符（`h` 表示短型或 `l`）指示接收的参数是比默认值短还是长。这意味着 `%hd` 表示短型（`short int`），`%ld` 表示长型（`long int`），`%lg` 表示双精度浮点数。以星号开头的指定符表示该项将被忽略。这意味着信息不会被存储，因此不需要值来接收它。

我们使用 `%c` 指定符来读取输入中的单个字符。这不会跳过初始的空白字符。

我们使用 `%s` 指定符来扫描字符串，但我们必须小心。它会在字符串的第一个空白字符处跳过前面的空白字符；因此，最好用它读取单词而不是通用字符串。此外，如果没有字段宽度指定符，它可能读取的字符串长度没有限制，因此接收的字符串必须足够容纳输入流中的最长字符串。最好使用字段指定符或 `%f` 和 `%s` 的组合来读取一行输入并对其扫描。这可以防止被恶意用户利用的缓冲区溢出。

给定输入行：

```
Hello, 1234, 5678, X, string to the end of the line
```

此 `scanf` 调用将正确扫描四个项：

```c
char s[256];

int n;

float f;

char c;

scanf("Hello, %d, %g, %c, %*n", &n, &f, &c, &s);
```

`scanf` 函数返回成功读取的项数，如果第一个项失败，则返回 `0`。如果在匹配第一个项之前到达输入末尾，则返回 `EOF`。如果文件流上发生读取错误，将设置流错误标志，并设置错误变量 `errno` 以指示错误类型。更多详细信息请参见本章稍后的“流错误”部分。

## 第 3 章

通常，`scanf` 及其类函数并不受推崇；这有三个原因：

尝试使用其他函数（如 `read` 或 `fgets`）来读取输入行，并使用字符串函数将输入分解为你需要的项。

## 其他流函数

许多其他标准库函数使用流参数或标准流 `stdin`、`stdout`、`stderr`：

- `fgetpos`: 获取文件流中的当前位置。
- `fsetpos`: 设置文件流中的当前位置。
- `ftell`: 返回流中的当前文件偏移量。
- `rewind`: 重置流中的文件位置。
- `freopen`: 重用文件流。
- `setbuf`: 设置流的缓冲方案。
- `remove`: 等于 `unlink`，除非路径参数是目录，在这种情况下它等于 `rmdir`。

这些都是在手册页的第 3 节中记录的库函数。

你可以使用流函数来实现各种功能。

### 另一个文件拷贝

```c
#include <stdio.h>

#include <stdlib.h>

int main() {

    int c;

    FILE *in, *out;

    in = fopen("input.txt", "r");

    out = fopen("output.txt", "w");

    while ((c = fgetc(in)) != EOF) {

        fputc(c, out);

    }

    fclose(in);

    fclose(out);

    return 0;

}
```

`error` 函数测试流的结束文件指示，如果设置则返回非零，否则返回 `0`。`clearerr` 函数清除 `stream` 指向的结束文件指示。它没有返回值，也没有定义的错误。你可以使用它从流的错误状况中恢复。

## 流与描述符

每个文件流都关联一个低级文件描述符。你可以将低级输入输出操作与高级流混合使用，但这通常是不明智的，因为缓冲的影响难以预测。

```c
#include <stdio.h>

int fileno(FILE *stream);

FILE *fdopen(int fileno, const char *mode);
```

我们可以通过调用 `fileno` 获取文件流使用的低级文件描述符。它返回流的描述符，失败时返回 `-1`。如果你需要对打开的流进行低级访问或对其调用 `fstat`，此函数非常有用。

我们可以通过调用 `fdopen` 基于已打开的文件描述符创建一个新的流。本质上，此函数为已打开的文件描述符提供了缓冲区，这可能是一个更容易解释的方式。

`fdopen` 函数的操作方式与 `fopen` 函数相同，但它接受的不是文件名而是低级文件描述符。如果我们使用 `open` 创建文件（可能是为了获得对权限的精确控制），但想使用流来写入，这非常有用。`mode` 参数与 `fopen` 函数相同，并且必须与最初打开文件时建立的访问模式兼容。`fdopen` 返回新的文件流，失败时返回 `NULL`。

## 文件和目录维护

标准库和系统调用提供了对文件和目录创建与维护的完全控制。

## chmod

你可以使用 `chmod` 系统调用更改文件或目录的权限。这是 `chmod` shell 程序的基础。

语法如下：

```c
#include <sys/stat.h>

int chmod(const char *path, mode_t mode);
```

由 `path` 指定的文件更改为指定的 `mode`。模式在 `open` 系统调用中指定，是权限的按位或。除非程序被赋予适当权限，否则文件所有者或超级用户才能更改其权限。

## chown

超级用户可以使用 `chown` 系统调用更改文件的所有者。

```c
#include <unistd.h>

int chown(const char *path, uid_t owner, gid_t group);
```

该调用使用了用户 ID 和组 ID 的数值值（从 `getuid` 和 `getgid` 调用获取）以及一个现在可以更改文件所有权的常量。如果设置了适当的权限，将更改文件的所有者和组。

- `POSIX` 实际上允许非超级用户可以更改文件所有权的系统。所有“标准”的 `POSIX` 系统都不会允许这样做，但严格来说，这是一种扩展（针对 `FIPS 151-2`）。我们在书中将处理的种类系统符合 `X/Open` 系统接口规范，并确实执行了所有权规则。

## unlink, link, and symlink

我们可以通过取消链接（`unlink`）来删除文件。

`unlink` 系统调用移除文件的目录条目并减少其链接计数。如果取消链接成功，返回 `0`；出错则返回 `-1`。你必须在文件条目所在的目录具有写入和执行权限，才能调用此函数。

```c
#include <unistd.h>

int unlink(const char *path);

int link(const char *path1, const char *path2);

int symlink(const char *path1, const char *path2);
```

如果计数达到零且没有进程打开该文件，则文件将被删除。事实上，目录条目总是会被移除，但在最后一个进程（如果有的话）关闭它之前，文件的空间不会被恢复。`rm` 程序使用文件的别名，这些别名通常由 `ln` 程序创建。我们可以使用 `link` 系统调用以编程方式为文件创建新链接。

使用 `open` 创建文件然后对其进行 `unlink` 是一些程序员用于创建临时文件（`transient files`）的技巧。这些文件仅在它们打开时才对程序可用；当程序退出且文件关闭时，它们将被有效删除。

`link` 系统调用为现有文件 `path1` 创建一个新链接。新的目录条目由 `path2` 指定。我们可以以类似的方式使用 `symlink` 系统调用创建符号链接。注意，指向文件的符号链接并不像普通（硬）链接那样防止文件被有效删除。

## mkdir and rmdir

我们可以使用 `mkdir` 和 `rmdir` 系统调用创建和删除目录。

```c
#include <sys/stat.h>

int mkdir(const char *path, mode_t mode);
```

## 第 3 章

`mkdir` 系统调用用于创建目录，相当于 `mkdir` 程序。`mkdir` 以路径作为名称创建新目录。目录权限通过参数 `mode` 传递，并作为 `open` 系统调用的 `O_CREAT` 选项给出，并且同样受到 `umask` 的影响。

```c
#include <unistd.h>

int rmdir(const char *path);
```

`rmdir` 调用删除目录，但仅当目录为空。`rmdir` 程序使用此系统调用来完成工作。

## chdir and getcwd

程序导航目录的方式类似于用户在文件系统中移动。正如我们在 shell 中使用 `cd` 命令切换目录，程序也可以使用 `chdir` 系统调用。

```c
#include <unistd.h>

int chdir(const char *path);
```

程序可以通过调用 `getcwd` 函数确定其当前工作目录。

```c
#include <unistd.h>

char *getcwd(char *buf, size_t size);
```

`getcwd` 函数将当前目录名称写入给定的缓冲区 `buf`。如果目录名称超过了由参数 `size` 指定的缓冲区大小（`ERANGE` 错误），它将返回 `NULL`。成功时返回 `buf`。

> 如果在程序运行期间目录被移除（`EINVAL`）或权限被更改（`EACCES`），`getcwd` 也可能返回 `NULL`。

## 扫描目录

`Linux` 上的一个常见问题是扫描目录，即确定位于特定目录中的文件。在 shell 程序中，这很容易——只需让 shell 扩展通配符表达式即可。过去，不同的 `UNIX` 变体允许以编程方式访问底层文件系统结构。我们仍然可以像普通文件一样打开目录并读取目录条目，但不同的文件系统和实现使得这种方法变得不可移植。已经开发了一个标准函数库，使得目录扫描变得简单得多。

目录函数在头文件 `dirent.h` 中声明。它们使用 `DIR` 结构作为目录操作的基础。指向该结构的指针称为目录流（`DIR *`），其作用类似于文件流（`FILE *`）处理普通文件的作用。目录条目本身在 `dirent` 结构中返回，也声明在 `dirent.h` 中，因为不应直接修改 `DIR` 结构中的字段。

## 与文件操作

我们将回顾这些函数：

- `opendir, closedir`
- `readdir`
- `teldir`
- `seekdir`

## opendir

`opendir` 函数打开目录并建立目录流。如果成功，它返回一个指向 `DIR` 结构的指针，用于读取目录条目。

```c
#include <sys/types.h>

#include <dirent.h>

DIR *opendir(const char *name);
```

`opendir` 在失败时返回空指针。注意，目录流使用低级文件描述符来访问目录本身，因此 `opendir` 可能会因为打开文件过多而失败。

## readdir

`readdir` 函数返回一个指针，指向目录流 `dirp` 中的下一个目录条目。连续调用 `readdir` 会返回更多目录条目。在出错或目录末尾，`readdir` 返回 `NULL`。`POSIX` 标准系统在目录末尾返回 `NULL` 时保持 `errno` 不变，在发生错误时设置它。

```c
#include <sys/types.h>

#include <dirent.h>

struct dirent *readdir(DIR *dirp);
```

注意，如果同时其他进程在目录下创建和删除文件，`readdir` 扫描无法保证列出所有的文件（和子目录）。

包含目录条目的 `dire` 结构包含以下条目：

- `ino_t d_ino`：文件的 `inode`
- `char d_name[]`：文件名

要确定目录内文件的详细信息，我们需要调用 `stat`，我们在本章之前介绍过。

## 第 3 章

## teldir

`teldir` 函数返回一个记录目录流当前位置的值。你可以将其用于随后的 `seekdir` 调用，将目录扫描重置到当前位置。

```c
#include <sys/types.h>

#include <dirent.h>

long teldir(DIR *dirp);
```

## seekdir

`seekdir` 函数设置目录流 `dirp` 中的项指针。用于设置位置的 `loc` 值应该从先前的 `teldir` 调用获取。

```c
#include <sys/types.h>

#include <dirent.h>

void seekdir(DIR *dirp, long loc);
```

## closedir

`closedir` 函数关闭目录流并释放与其相关的资源。成功时返回 `0`，出错时返回 `-1`。

```c
#include <sys/types.h>

#include <dirent.h>

int closedir(DIR *dirp);
```

```c
#include <string.h>

#include <sys/stat.h>

#include <stdlib.h>

void printdir(char *dir, int depth)

{

    DIR *dp;

    struct dirent *entry;

    struct stat statbuf;

    if((dp = opendir(dir)) == NULL) {

        fprintf(stderr, "cannot open directory: %s\n", dir);

        return;

    }

    chdir(dir);

    while((entry = readdir(dp)) != NULL) {

        stat(entry->d_name, &statbuf);

        if (S_ISDIR(statbuf.st_mode)) {

            /* Found a directory, but ignore . and .. */
```
