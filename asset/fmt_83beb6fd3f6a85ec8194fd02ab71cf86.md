
`gcc version 3.3.2 (SUSE Linux)`

`/usr/lib/gcc-lib-i586-suse-linux/3.3.3/ccE -quiet -v -D_GNUC__3`

`-D_GNUC_MINOR_=3 -D_GNUC_PATCHLEVEL_=3 -`

`#include "..." * search starts here:`

```
```

`#include <..> search starts here:`

`/usr/local/include`

`/usr/lib/gcc-lib-i586-suse-linux/3.3.3/include`

`/usr/i586-suse-linux/include`

`/usr/include`

End of search list.

# 1 <stdin>

# 1 <command line>

# 1 <stdin>

```
main() { printf("hello world!\n"); }
```

在这一特定的示例中，预定义的变量如下：
`-D_GNUC_ =3 -D_GNUC_MINOR_=3 -D_GNUC_PATCHLEVEL_=3`

要为此安装定义默认变量，可以编辑文件 `usr/lib/gcc-lib/lib/i586-suse-linux/3.3.3/specs`，以添加更多预定义变量。在编译期间定义变量的另一种方法是在 `Makefile` 的相应构建标志中使用 `-D<variable_name>` 开关。

## 6.3.7 Linux 平台上的命名空间选择

Linux 头文件和库支持多种命名空间，以满足不同类型的标准。它们在表 6-7 中描述。

表 6-7
Linux 命名空间表

| Linux 定义 | 说明 |
|--- |--- |
| `__STRICT_ANSI__` | ISO 标准 C。 |
| `_ISOC99_SOURCE` | ISO C99 对 ISO C89 的扩展。 |
| `_POSIX_SOURCE` | IEEE 标准。 |
| `_POSIX_C_2001_SOURCE` | IEEE 标准 2001。 |
| `_POSIX_C_2008_SOURCE` | IEEE 标准 2008。 |
| `_POSIX_C_2019_SOURCE` | IEEE 标准 2019。 |
| `_POSIX_SOURCE_200109L` | IEEE 标准 2001。 |
| `_POSIX_SOURCE_200809L` | IEEE 标准 2008。 |
| `_C_SOURCE` | ISO 标准 C。 |
| `_STRICT_C_SOURCE` | ISO 标准 C。 |
| `_STRICT_C99_SOURCE` | ISO 标准 C。 |
| `_STRICT_C11_SOURCE` | ISO 标准 C。 |
| `_STRICT_C17_SOURCE` | ISO 标准 C。 |
| `_C_SOURCE_200809` | ISO 标准 C。 |
| `_C_SOURCE_201103` | ISO 标准 C。 |
| `_C_SOURCE_2018L` | ISO 标准 C。 |

要为此安装定义默认变量，可以编辑 `usr/lib/gcc-lib/i586-suse-linux/3.3.3/specs` 来添加更多预定义变量。在编译期间定义变量的另一种方法是在 `Makefile` 中使用 `-D<variable_name>` 开关。

## 第 6 章 - 迁移 HP-UX 应用程序

| Linux 定义 | 说明 |
|---|---|---|
| `__STRICT_ANSI__` | ISO 标准 C。 |
| `_ISOC99_SOURCE` | ISO C99 对 ISO C89 的扩展。 |
| `_POSIX_SOURCE` | IEEE 标准。 |
| `_POSIX_C_2001_SOURCE` | IEEE 标准 2001。 |
| `_POSIX_C_2008_SOURCE` | IEEE 标准 2008。 |
| `_POSIX_C_2019_SOURCE` | IEEE 标准 2019。 |
| `_POSIX_SOURCE_200109L` | IEEE 标准 2001。 |
| `_POSIX_SOURCE_200809L` | IEEE 标准 2008。 |
| `_C_SOURCE` | ISO 标准 C。 |
| `_STRICT_C_SOURCE` | ISO 标准 C。 |
| `_STRICT_C99_SOURCE` | ISO 标准 C。 |
| `_STRICT_C11_SOURCE` | ISO 标准 C。 |
| `_STRICT_C17_SOURCE` | ISO 标准 C。 |
| `_C_SOURCE_200809` | ISO 标准 C。 |
| `_C_SOURCE_201103` | ISO 标准 C。 |
| `_C_SOURCE_2018L` | ISO 标准 C。 |

## 6.4 链接器

HP-UX 和 GNU 编译器都支持将选项直接发送给链接器。这是通过使用 `-wl` 实现的，该开关可以出现多次。虽然 HP-UX 和 GNU 的某些命令行开关相似，但建议彻底检查链接器命令行参数的预期用途。

表 6-8
HP-UX 和 Linux 链接器选项比较

| HP-UX 选项 | GNU 等效选项 | 说明 |
| --- | --- | --- |
| 大多数以+ 开头的选项 | 不支持 | 以+ 开头的 HP-UX ld 选项。 |
| 例如 +b, +vtype, +s。 | | |
| `-a {archive | shared | default | archive_shared shared_archive}` | `-a {archive | shared | default}` | 告诉链接器链接到什么类型的库。 |
| | `-Bdynamic|-dy|-call_shared` | |
| | `-Bstatic|-dn|-non_shared|-static` | |
| `-B [immediate|restricted||symbolic|]` | None | 更改启动时应用程序到链接库的绑定行为。 |
| `-e entry` | `-e entry` | 使用 entry 作为程序执行的式符号，而不是默认入口点。 |
| `+e` | `-E|export-dynamic` | 导出符号。 |
| `-h` | None²³ | 隐藏符号。 |
| `-Ldir` | `-rpath path` | 指定运行时链接器的搜索方向。 |
| `-Ldir` | `-Ldir` | 用 `-L` 标志指定的目录增强系统默认搜索目录。 |
| `-1:` | None | 在 HP-UX 中，指定要链接库的完整基名。例如，`-1:libfoo.a` |

²³ 在 GNU ld 中通过 `-version-script` 选项使用导出映射。

# 第 6 章 • 迁移 HP-UX

| HP-UX Id 选项 | GNU Id 等效 | 描述 |
| --- | --- | --- |
| `-r` | `-r` | 生成可重定位输出（即生成一个可以反过来作为 1ld 输入的输出文件）。 |
| `-s` | `-s` | 从输出文件中省略符号信息。 |
| `-t` | `-t` | 在 1ld 处理输入文件时打印输入文件的名称。 |
| `-u symbol` | `-u symbol` | 将符号作为未定义符号输入符号表。 |
| `-v` | 无 | 在链接期间显示详细信息。 |
| `-V` | `-v, -v` | 显示 1ld 的版本号。 |
| `-G` | `-S` | 剥除所有不可卸载的数据（如调试信息）。 |
| `-x` | `-x` | 删除所有本地符号。 |
| `-y symbol` | `-y symbol` | 输出出现符号的每个链接文件的名称。 |
| `-z` | 无 | 允许空指针解引用（仅限 HP-UX）。 |

请参考第 3 章获取关于 Linux 上可用的库版本控制的信息。

## 6.4.1 导出映射 (Export Map)

导出映射允许用户显式告诉链接器从生成的对象导出哪些符号。GNU 链接器支持导出映射。要用此方法生成共享对象，用户必须通过链接器的 `-version-script` 选项传递映射文件名：

```bash
$ gcc -shared -o bar.so bar.c -fPIC -Wl,--version-script=bar.map
```

`bar.map` 文件可以包含如下文本：
```c
{
    global: index;
    local: *;
}
```
