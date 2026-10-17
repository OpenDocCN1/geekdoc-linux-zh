
IN_=96 -D__GNUC_PATCHLEVEL =0 -D_ELF -Dunix -Dlinux -D_ELF -D_unix-D_linux -D_unix -Asym(posix)-D_NO_INLINE -Acpu(i386)-march(i386)-DI386 -D_i386 -D_tune_i386_s.c /tmp/cc86nu.i

```
GNU CPP version 2.96 20000731 (Red Linux 7.1 96-98) (cpp i386 Linux/ELF)
searching nonexistent directory "/usr/i386-redhat-linux/include",
```

#include "" starts here:

#include...> starts here:

/usr/local/include

/usr/lib/gcc-lib/i386-redhat-linux/296/include

/usr/include

```
```

End of search list.

/usr/lib/gcc-lib/i386-redhat-linux/296/ccl /tmp/cc86nu.i -quiet -dumpbase slogan.c-version -o /tmp/cc4ySmi.s

```
GNU C version 2.96 20000731 (Red Linux 7.1 96-98) (i386-redhat-linux) compiled by GNU C version 2.96 20000731 (Red Linux 7.1 96-98).as -V -Qy -o /tmp/ccWb.o /tmp/cc4ySmi.s.
GNU assembler version 2.11.90.8 (i386-redhat-linux) using BFD 2.11.90. 0.8
/usr/lib/gcc-lib/i386-redhat-linux/296/collect2 -m elf _i386 -dynamic-linker /lib-linux.so.2 /usr/lib/gcc-lib/i386-redhat-linux/296/...../..//crti.o /usr/li
b/gcc-lib/i386-redhat-linux/296/...../..//crti.o /usr/lib/gcc-lib/i386-redhat-li
ux/296/crtbegin.o -L/usr/lib/gcc-lib/i386-redhat-linux/296 -L/usr/lib/gcc-lib
c/i386-redhat-linux/296/...../..//tmp/ccWb.o -lm -lgcc -lgcc /usr/lib/gc
c-i386-redhat-linux/296/...../..//crtend.o /usr/lib/gcc-lib/i386-redhat-linux/296/...../..//crtn.o

$

接下来的章节内练习旨在让你练习使用 `gcc` 命令 `te -v` 选项以帮助你理解其基本逻辑。

## 章节内练习

+   9.2 在你的 UNIX 或 LINUX 系统上重复上述会话，以探索 `gcc` 命令的工作原理，并理解生成可执行代码的各种编译步骤。你的系统使用什么版本的编译器和汇编器？

### 9.4.1 编译多个源文件

你可以使用 `gcc` 命令在单条命令行中编译并链接多个 C 源文件并创建一个可执行文件。例如，你可以使用以下命令行为 `driver.c`、`stack.c` 和 `misc.c` 创建一个名为 `polish` 的可执行文件。

```bash
$ gcc driver.c stack.c misc.c -o polish
```

$ 如果三个源文件中的一个被修改，你需要重新输入整行命令行，这产生了两个问题。首先，即使只有一个文件需要重新编译，所有三个文件都会被编译成对象模块，这导致编译时间变长，特别是当文件很大时。其次，当你处理三个文件（如此处所示）时，重新输入整行可能不是什么大问题，但当你需要处理大量文件时，你肯定不会喜欢这样做。虽然使用 `-o` 运算符（参见第 1.6.11 节）你不需要重试整个命令，但使用该运算符指定不同的模式来调用多个命令仍然是一项耗时的任务。为了避免这些问题，你应该链接所有源文件的对象模块，然后只重新编译那些更新的模块。这被称为**增量编译**。然后将所有对象模块链接在一起，创建一个单一的可执行文件。

你可以使用 `gcc` 命令配合 `-c` 选项为 C 源文件创建对象模块。当你使用 `-c` 选项编译程序时，编译器会在你的当前目录下留下一个对象文件，而不生成可执行文件。对象文件的名称与源文件名相同，并带有 `.o` 扩展名。你可以通过另一个 `gcc` 命令链接多个对象文件。在下面的会话中，我们分别编译三个源模块 `driver.c`、`stack.c` 和 `misc.c` 来创建它们的对象文件，然后使用另一个 `gcc` 命令将它们链接并创建一个名为 `polish` 的单一可执行文件。

```bash
$ gcc -c driver.c
$ gcc -c stack.c
$ gcc -c misc.c
$ gcc misc.o stack.o driver.o -o polish
$ polish
```
[程序输出]

$ 你可以使用 `-c` 选项编译多个源文件并生成它们的对象模块。在接下来的第一条命令行中，我们使用单一编译器命令编译三个源文件以生成对象文件。第二条命令行链接这三个对象文件并生成一个可执行文件 `polish`。

```bash
$ gcc -c driver.c stack.c misc.c
$ gcc misc.o stack.o driver.o -o polish
```

$

## 编译 C+/C++ 程序

现在，如果你更新了其中一个源文件，你需要使用 `gcc -c` 命令仅为该源文件生成对象文件。然后再次链接所有对象文件（使用第二条 `gcc` 命令）来生成可执行文件，如下所示。在示例中，假设假设更新了 `misc.c`。

```bash
$ gcc -c misc.c
$ gcc misc.o stack.o driver.o -o polish
$
```

在接下来的课内练习中，你将使用 `gcc` 编译器为 C 源文件创建一个可执行文件。

# 课内练习

- 9.3 为名为 `power.c` 的文件中的 C 程序创建可执行代码，并将其放在名为 `XpowerY` 的文件中。你使用了什么种 `command()`？运行 `XpowerY` 以确认程序正常工作。

### 9.4.2 链接库

LINUX 和 UNIX 系统中的 C/C++ 编译器在编译程序时会将适当库与你的程序链接；你需要包含（使用预处理器的 `#include` 指令）一个头文件，例如字符串库的 `<string.h>`，以便库被链接。然而，有时你必须显式告诉编译器链接所需的库。你可以通过在程序中包含库的头文件并使用带有 `-l` 选项的 `gcc` 命令来实现，紧跟其后的是库名的字母（lib/lib.a）以供对象代码链接。在接下来的会话中，我们将数学库 (`lib/math.a`）链接到 `power.c` 程序的对象代码。我们使用第一个 `gcc` 命令来显示即使包含了 `<math.h>` 头文件（位于 `/usr/include` 目录），如果未链接数学库，编译器生成的错误信息。信息显示在 `power.c` 文件未找到符号 `pow`。数学库的名称为 `libm.a`，因此我们使用 `-l` 选项配合字母 `m`（它在字符串 `lib` 之后，扩展名之前）并重新编译程序以将可执行代码存储在 `power` 文件中。现在程序可以正常编译并运行。

```c
$ cat power.c
#include <math.h>
```

```c
main() {
    float x,y;
    printf("The program takes x and y from stdin and displays x^y.\n");
    printf("Enter number x: %f");
    scanf("%f", &x);
    printf("Enter number y: %f");
    scanf("%f", &y);
    printf("x^y is: %6.3f\n", pow((double)x,(double)y));
}
```

```bash
$ gcc power.c -o power
/tmp/cc67RTX0.o: In our current `main`:
/tmp/cc67RTX0.o: undefined reference to `pow`
ld: collect error in /tmp/cc67RTX0.o
: undefined reference to `pow`
exit status 1
```
