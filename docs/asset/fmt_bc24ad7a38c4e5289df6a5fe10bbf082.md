
```
kdb> btp 2571
0xc575800 00002571 00000000 0 000 stop 0xcdf2280 init
ESP EIP Function (args)
0xcdf3aec 0xc0119e62 do_schedule+0x192 (0xc0421bbc, 0xc0421bbc, 0x8f5908)
->kcdfa20000 .text 0xc0125cb0
->kernel 0xc0110000 0xc0119cd0
0xc0110a40
0xcdf3fe0 0xc0125393 schedule_timeout+0x63 (0x104, 0xcdf2000, 0x1388)
0x0, 0x0,
kernel .text 0xc0110000 0xc01258d0
0xc0125980
0xcdf3f1c 0xc01548e1 do_select+0x1e (0xb, 0xcdf3f90, 0xcdf3f8c, 0x1,
0x4)
kernel .text 0xc0110000 0xc0154700
0xc0154930
0xcdf3f58 0xc0154c88 sys_call+0x328 (0xb, 0xbfff720, 0x0, 0x0,
0xbffffffff
kernel .text 0xc0110000 0xc0154960
0xc0154630
0xcdf3fc4 0xc01008dd3 system_call+0x33
kernel .text 0xc0110000 0xc0108da80
0xc0108de0
```

栈回溯中的所有函数都是内核函数。在不深入了解内核编程的情况下，我们可以看到在 KDB 被调用时，它正处于从用户态执行 `select()` 系统调用的中间。这个结论可以根据 `do_select` 栈帧得出的。系统调用都有一个与系统调用同名的内核工作例程，并在其前面加了 `do_` 前缀。`schedule_timeout` 和 `do_schedule` 栈帧是 `do_select` 调用该进程的，以便进行通信。

## ELF：可执行与链接格式 第 9 章

`-rw-r--r-- 1 wilding build 275 Apr 15 2004 main.C`

`-rw-r--r-- 1 wilding build 276 Dec 28 18:37 pic.C`

> 注意：这些文件中的源代码可以在章节末尾的“源文件”标题下找到。

注意：`.C` 扩展名用于 C++ 文件，尽管 `.cc` 和 `.cpp` 也可以用。

这些对象都被编译为 C++ 源文件。其中一些对象包含简单的 C++ 对象，将用于解释 ELF 如何处理简单的 C++ 功能（如构造函数和析构函数）。

源文件 `foo.c` 包含多个全局对象、一个构造函数、多个全局变量以及多个函数。源文件 `foo.h` 包含了 `foo.c` 中全局对象所需的类定义。源文件 `main.c` 调用了 `foo.c` 中的函数并实例化了一个对象。源文件 `pic.c` 是一个较小且不复杂的源文件，用于说明重定位。最后，make 文件 `Makefile` 使得使用 `make` 工具编译和链接源文件变得更容易。

要编译并链接源文件，只需在包含文件的目录下运行 `make` 即可：

```bash
penguin> make
g++ -c main.C
g++ -c -fPIC foo.c
g++ -shared -fPIC -o libfoo.so
g++ -o main.o -L,-W1,-rpath, -lffoo
g++ -c -fPIC pic.C
g++ -o pic.c -L -W1,-rpath,
g++ -c pic_nopic pic.C -o pic_nopic.o
g++ -o pic_nopic pic_nopic.o -L -W1,-rpath,
gcc -fPIC intercept.c
gcc -o intercept.so -shared intercept.o
```

> 注意：`-fPIC` 选项用于某些源文件以创建位置无关的对象文件。这是创建共享库时的首选。位置无关代码将在本章稍后部分进行详细介绍。

> 注意：`-L.` 切换是为了方便起见。它告诉链接器在当前目录（`.`）中查找共享库。通常情况下会使用真实的共享库目录，但考虑到共享库与可执行文件位于同一目录，这样做非常方便。

## 9.2 概念与定义

源文件 `foo.c` 用于创建 `libfoo.so`，而源文件 `main.c` 用于构建可执行文件 `foo`。

在本章中，我们将一直使用 `g++` 编译器。该编译器安装在许多/大多数 Linux 系统上，并将编译 C++ 代码以帮助说明 ELF 如何处理基本的 C++ 功能。

学习 ELF 可能会是一项挑战，因为这些概念之间是相互依赖的，学习一个概念可能需要理解另一个概念，反之亦然。因此，在深入研究 ELF 细节之前，我们将介绍一些基本概念和定义，而不涉及过多细节。这些概念中最基础的就是“符号”。

### 9.2.1 符号

符号是存储在 ELF 文件中的函数或变量（或其他）的描述。符号类似于电话簿中的条目。它包含了关于 ELF 文件中函数或变量的简要信息，但就像电话条目一样，它显然不是所描述的项本身。符号可以描述许多内容，但它们主要用于函数和变量，我们目前将关注这些。

符号具有与其相关的大小、值和名称，以及其他一些信息。大小是符号所代表的函数或变量的实际大小。值提供了函数/变量在 ELF 文件中的位置，或者函数/变量的预期地址（以共享库或可执行文件的加载地址为基准）。名称是为了人类的方便，用于让软件开发人员可以在程序中使用描述性名称。

考虑本章所用系统中“libc.so.6”中的 `printf` 函数：我们可以使用 `nm` 命令查看此“符号”的细节（注意：... 表示未包含在内的感兴趣的输出）：

```bash
penguin -v -f s /lib/libc.so.6
```

来自 `/lib/libc.so.6` 的符号：

| Name | Value | Class | Type | Size | Line | Section |
|---|---|---|---|---|---|---|
| printf | 0004fc90 | T | FUNC | 00000039 | | .text |

> 注意：某些发行版可能会剥离（strip）共享库，这会移除主符号表并使得这里的 `nm` 命令能够如所示工作。在这种情况下，请选择系统上未被剥离的库。你也可以对 ELF 文件使用 `file` 命令来查看它是否被剥离（将显示“stripped”字样）。

注意：ELF 使用“class”（类）术语来描述符号的范围/类别。ELF 术语 `class` 在描述符号时，与 C++ 类无关。

“Value”（值）字段是库中找到 `printf` 的可执行指令的偏移量。`class` 为“T”，表示“text”（文本段）。在此背景下，text 是只读的。类型为“FUNC”，表示函数。大小为 `0x39` 字节，即十进制的 57 字节，最后是在“text”节中找到的节，该节包含了库的所有可执行代码。符号可以有不同的“scope”（范围），例如全局或局部。共享库中的全局变量是暴露的，供其他共享库或可执行文件本身使用。局部变量在原始源文件中被定义为“static”，使其在该 particular源文件的代码中是局部的。静态符号对其他 ELF 文件不可用。

源文件 `foo.c` 中定义了两个用于说明范围概念的变量：

```c
globInt = 5;
static int staticInt = 5;
```

第一个是全局变量，第二个被定义为“static”。再次使用 `nm`，我们可以看到类型变量的“class”（即范围）：

```bash
nm -v -f s foo.o | egrep "staticInt|globInt"
globInt 00000000  OBJECT 00000004 .data
staticInt 00000004  d       .data
```

输出显示全局数据变量为大写的 `D`，局部数据为小写的 `d`。在文本符号的情况下，大写的 `T` 指向全局符号；而小写的 `t` 指向局部符号。

符号也可以被定义或未定义。已定义的符号意味着对象文件实际上包含了它。未定义的符号意味着对象文件引用了它但没有包含它。例如，`main.C` 调用了 `printf` 但没有包含它。再次使用 `nm`，可以看到 `class` 是 `U`（未定义）：

```bash
penguin> nm -v -fs main.o | egrep printf
printf | U
```

其他符号是只读或未初始化的（这些在 `nm` 输出中为 `R` 或 `B`）。ELF 还有绝对符号（在 `nm` 中标记为 `A`），用于标记文件中的偏移量。以下命令显示了一些：
