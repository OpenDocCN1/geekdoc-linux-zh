
```text
main target : requirements

instructions

target1 : requirements1

instructions1

...

targetN : requirementsN

instructionsN
```

如您所见，每行对——尽管可能多于一组指令——遵循相同的格式。它从`目标`开始，它是以下之一：

- C 对象文件（`file.o`）。
- 称为`make target`的`make`参数。此类型目标允许您输入某些标准安装说明，例如`make install`，从而自动化整个过程。
- 可执行程序本身。

`需求`指在运行此特定目标的指令之前必须构建的对象文件。这只是一个空格分隔的对象文件列表。最后，`指令`通常是简单的`gcc`命令。一个简短的 Makefile 可能类似于以下内容：

```text
main : main.o sub1.o sub2.o
       gcc -o aill main.o sub1.o sub2.o
main.o : main.c
        gcc -c main.c
sub1.o : sub1.c
        gcc -c sub1.c
sub2.o : sub2.c
        gcc -c sub2.c
```

> **注：** 此处讨论的所有 GNU 工具的手册可在 [www.gnu.org/manual/manual.html](http://www.gnu.org/manual/manual.html) 获取。

## 立即解决方案

### 安装 C 编译器

要安装 C 编译器，请执行以下操作：

1. 以 root 身份登录。
2. 通过输入 `rpm -q egcs` 检查您是否已安装 C 编译器。如果找到此软件包，则无需继续。
3. 将 Red Hat CD-ROM 插入 CD-ROM 驱动器。
4. 通过输入 `mount /mnt/cdrom` 挂载 CD-ROM。
5. 通过输入 `cd /mnt/cdrom/RedHat/RPMS` 切换到 packages 目录。
6. 通过输入 `rpm -ivh egcs-1` 然后按 Tab 键扩展文件名来安装 C 编译器。按 Enter 键。

> **注：** 您可能好奇为什么我之前在章节中说编译器是 `gcc`，但您安装的是软件包 `egcs`。GNU C 编译器官方由 EGCS 维护，作为合并两个独立开发项目的一种方式。有关此项目的最新信息可在 [http://gcc.gnu.org](http://gcc.gnu.org) 获取。

### 使用 gcc 编译 C 代码

要使用 `gcc` 编译 C 代码，请执行以下操作：

1. 登录到拥有您要处理的代码的账户。
2. 使用 `cd` 命令切换到包含代码的目录。
3. 通过在命令行中输入 `gcc` 开始。尚未按 Enter 键。
4. `gcc` 使用的四个步骤中每一步都有其可用的一组命令选项。从表 22.1 中选择您要使用的预处理选项。对于此示例，您要越过预处理点，因此避免使用 `-E` 选项。您还想指定头文件位于 `/bin/cocode/headers`，并保存有助于构建 Makefile 的信息。因此，在此时，您拥有以下内容：

```
gcc -idirafter ~/bin/cocode/headers -MD
```

## 表 22.1 gcc 中常用的预处理器选项

| 选项 | 用途 | 值 | 示例 |
| :--- | :--- | :--- | :--- |
| `-D` | 根据使用情况，定义一个结果为字符串的宏，或者定义一个结果特定为 `1` 的宏 | 宏名称或宏名称及其结果 | `-Done` 或 `-Dtwo='2'` |
| `-dD` | 在相应位置输出所有宏定义 | 无 | `-dD` |
| `-dN` | 以 `#define` 语句的形式输出所有宏 | 无 | `-dN` |
| `-E` | 执行代码预处理然后停止；有关与此选项配合使用的额外选项，请参见表 22.2 | 无 | `-E` |
| `-H` | 打印头文件名称 | 无 | `-H` |
| `-idirafter` | 如果头文件未在预期位置找到，则指定查找头文件的目录 | 查找路径 | `-idirafter ~/ccode/headers` |
| `-imacros` | 在预处理代码之前处理指定文件，但丢弃其输出 | 文件路径 | `-imacros addthis` |
| `-include` | 在预处理代码之前处理指定文件 | 文件路径 | `-include additions` |
| `-iprefix` | 指定 `-iwithprefix` 选项的前缀参数 | 顶层目录 | `-iprefix ~` |
| `-isystem` | 指定额外的系统头文件目录 | 路径 | `-isystem ~/bin/sys` |
| `-iwithprefix` | 指定如果头文件未在预期位置找到时查找头文件的目录，该目录的路径挂接在指定的 `-iprefix` 目录下 | 剩余路径 | `-iwithprefix ccode/headers` |
| `-iwithprefixbefore` | 指定初始查找头文件的目录，该目录的路径挂接在指定的 `-iprefix` 目录下 | 剩余路径 | `-iwithprefixbefore ccode/headers` |
| `-MD` | 输出可用于构建此程序 Makefile 的语句，但将依赖信息保存到 .d 扩展名的文件中，以避免干扰剩余的编译步骤 | 无 | `-MD` |
| `-MMD` | 输出可用于构建此程序 Makefile 的语句，但将依赖信息保存到 .d 扩展名的文件中，以避免干扰剩余的编译步骤；忽略系统头文件 | 无 | `-MMD` |
| `-nostdinc` | 忽略系统头文件目录 | 无 | `-nostdinc` |
| `-trigraphs` | 确保输出标准 C 代码，尽管由于其严格的性质，这通常是不受欢迎的 | 无 | `-trigraphs` |
| `-U` | 取消定义指定的宏 | 宏名称 | `-Uthree` |
| `-undef` | 指定除非在代码中明确定义，否则不应定义任何宏 | 无 | `-undef` |
| `-Wp,` | 将特定选项（或多个选项）传递给预处理器 | 选项，如果多个则用逗号分隔 | `-Wp,-MG` |

## 表 22.2 仅使用 gcc 进行预处理时的选项

| 选项 | 用途 |
| :--- | :--- |
| `-C` | 保留注释 |
| `-dM` | 仅在预处理结束时输出已设置的宏定义 |
| `-M` | 输出可用于构建此程序 Makefile 的语句 |
| `-MG` | 输出可用于构建此程序 Makefile 的语句，假设头文件与源文件位于同一位置 |
| `-MM` | 输出可用于构建此程序 Makefile 的语句，但省略 `#include` 命令 |
| `-P` | 保留 `#line` 命令而不是展开它们 |

5. 预处理器完成后，编译本身开始。编译 C 代码有许多可用选项。任何习惯编译 C 程序的人都知道，有时你会得到大量的警告消息，其中一些应该是可以忽略的，而另一些则很重要。请参见表 22.3 从可用的警告选项中进行选择。对于这个示例，确保在使用前定义项目很有用。现在你应该有如下内容：

```
gcc -idirafter ~/bin/ccode/headers -MD -Wimplicit
```

> 注意：选项 `-Wall` 激活了表 22.3 中列出的许多警告。

## 表 22.3 gcc 在编译阶段常用的警告选项

| 选项 | 用途 |
| :--- | :--- |
| `-fsyntax-only` | 忽略除语法错误以外的一切 |
| `-pedantic` | 对所有非标准 C 内容发出警告；通常不受欢迎，因为标准 C 非常严格 |
| `-pedantic-errors` | 对任何非标准 C 内容产生错误消息而不是警告 |
| `-w` | 关闭所有警告 |
| `-Wchar-subscripts` | 当数组下标被赋值为 `char` 类型时产生警告 |
| `-Wcomment` | 关于嵌套注释发出警告——两个 `/*` 项目未关闭注释——或者如果 `//` 出现在注释中 |
| `-Werror` | 将所有警告更改为错误消息；如果你使用大量警告，通常不建议这样做 |
| `-Werror-implicit-function-declaration` | 当函数在使用前未定义时给出错误 |
| `-Wformat` | 确保需要格式化参数的命令被正确使用 |
