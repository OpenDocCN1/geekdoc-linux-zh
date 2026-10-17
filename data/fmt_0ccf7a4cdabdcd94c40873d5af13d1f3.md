
```bash
albino-lobster@ubuntu:~~antire_book/chap_3_format_hacks/trouble/build$ gdb ./trouble
GNU gdb (Ubuntu 7.11.1-16.04) 7.11.1
Copyright (C) 2016 Free Software Foundation, Inc.
License GPLv3; GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
这是免费软件：你可以自由地更改和分发它。
在法律允许的范围内不提供任何担保。详情请查阅 "show copying" 和 "show warranty"。
此 GDB 配置为 "x86_64-linux-gnu"。
请输入 "show configuration" 查看配置详情。
有关错误报告说明，请参：
http://www.gnu.org/software/gdb/bugs/
可以在在线查找 GDB 手册和其他文档资源：
http://www.gnu.org/software/gdb/documentation/
需帮助请输入 "help"
输入 "apropos word" 搜索与 "word" 相关的命令
"/home/albino-lobster/antire_book/chap_3_format_hacks/trouble/build/.trouble": not a x format: File format not recognized
```

哎。`GDB` 用“无法识别文件格式”拒绝了该可执行文件。我有点担心 Trouble 无法执行。然而，一个快速测试证明我可以执行 Trouble，并且客户端仍然连接连接。

### Trouble 仍然可用

```bash
albino-lobster@ubuntu:~$ nc 127.0.0.1 1270
irsrle@v1Ac70x708rk
pwd
/home/albino-lobster/antire_book/chap_3_format_hacks/trouble
```

看来翻转一个位就让 `readelf` 和 `GDB` 无法工作了。让我们看看我们喜爱的反汇器如何应对这种攻击。

### 用字节序谎言弄崩 Radare2

```bash
albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/trouble/build$ radare2 ./trouble
Warning: Cannot initialize program headers
Warning: Cannot initialize section headers
Warning: Cannot initialize strings table
Warning: Cannot initialize dynamic strings
Warning: Cannot initialize dynamic section
Warning: read (init_offset)
Warning: read (get_fini)
-- radare2 for Fide05, now with extra potato
[0xf20240000000000]> aaaa
[x] 分析 0xf20240000000000 处以 .entry 开头的标志 (aa)
[Warning]: 在非执行区域中搜索交叉引用 (aar)
[x] 为 fcn.* 和 sym.func.* 函数构造函数名称 (aan)
[0xf20240000000000]> fcn
[0xf20240000000000]> pdf
p: Cannot find function at 0xf20240000000000
[0xf20240000000000]>
```

好了，Radare2 也坏了。我也尝试了 Hopper，但它什么都不显示……从反逆向工程的角度来看，这很棒，因为它给了用户一个关于哪里错误的提示。

IDA 的响应很有意思。它首先显示了这条消息：

![](img/fdf1e4bfff3995dc5a8580eb00fa23e5_87_0.png)

“IDA 关于字节序（endianness）谎言的错误信息”

这个拼写错误让我内心的小三年级感到很快，但我确定他们指的是“第六字节（byte six）”。然而，在点击“是”继续后，IDA 成功反汇编了整个文件。看来 IDA 必须有确定真实字节序的辅助方法。

尽管 IDA 给我们泼了冷水，但这似乎是一个实用的小混淆手段，而且很容易添加到我们的构建过程中。只需在 Trouble 的 `CMakeLists.txt` 末尾添加以下行即可。

## 用于插入字节序谎言的 CMake 命令

```
add_custom_command(TARGET ${PROJECT_NAME}
                     POST_BUILD
                     COMMAND echo 'Ag==' | base64 -d | dd conv=notrunc of=${CMAKE_CURVE_BINARY_DIR}/${PROJECT_NAME} bs=1 seek=5)
```

## echo ‘Ag==' | base64-d

你可能在想：“这个插入字节序谎言的 CMake 命令到底是怎么回事？”有趣的是，CMake 不喜欢在 `add_custom_command()` 函数中使用反斜杠，而我没有找到任何解决方法。我尝试过直接选择 `\x02` 的 UTF-8 表示法，但这破坏了本书的版本跟踪系统。我最终决定对 `echo -ne '\x02’` 进行 base64 解码。

当添加了新的 EI_DATA 混淆编译 Trouble 时，它看起来应该是这样的：

## 第 3 章：文件格式

## 使用 EI_DATA 混淆编译 Trouble

```
albino-lobster@ubuntu:~/antire-book/chap_3_format_hacks/trouble/build$ make clean; make -j
-- Configuring done
-- Generating done
-- Build files have been written to: /home/albino-lobster/antire_book/chap_3_format_hacks/trouble/build
Scanning dependencies of target trouble
[50%] Building C object CMakeFiles/trouble.dir/src/trouble.c
[100%] Linking C executable trouble
The bind shell password is: lu0NwoGb2CtAeqwiHe8GNJcXRfxuLV
1+0 records in
1+0 records out
1 byte copied, 4.1259e-05 s, 24.2 kB/s
[100%] Built target trouble
```

## 节是谎言

在之前的章节中，你学习了运行可执行文件不需要节头（headers），你可以在 ELF 头中插入虚假信息以阻碍分析。某些反汇器依赖节表来提供地址映射，并发现如 `.init3`⁴ 和 `.fini` 这样的特殊节。通过干扰节表是否可以欺骗反汇器呢？

## 翻转执行位

编译三个版本的 Trouble bind shell，并使用 `stripBinary` 工具移除节表。在 `readelf` 中，Trouble 现在应该看起来像这样：

> ⁴https://gcc.gnu.org/onlinedocs/gccint/Initialization.html

## 第 3 章：文件格式破解

## stripBinary 后的 Trouble 视图

```
albino-lobster@ubuntu:~/antire_book/chap_3_format_hacks/trouble/build$ readelf -a /t/ouble
```

ELF Header:

Magic: 7f 45 4c 43 46 02 01 00 00 00 00 00 00 00 00

Class: ELF64

Data: 2's, little endian

Version: 1 (current)

OS/ABI: UNIX System V

ABI Version: 0

Type: EXEC (Executable file)

Machine: Advanced Micro Devices X86-64

Version: 0x1

Entry point address: 0x4002f

Start of program headers: 64 (bytes into file)

Start of section headers: 0 (bytes into file)

Flags: 0x0

Size of this header: 64 (bytes)

Size of program headers: 56 (bytes)

Number of program headers: 4

Size of section headers: 64 (bytes)

Number of section headers: 0

Section header string table index: 0

文件中没有节（sections）。

文件中没有可以分组的节。

| Type | Offset | VirtAddr | PhysAddr | Flags | Align |

| :--- | :--- | :--- | :--- | :--- | :--- |

| LOAD | FileSize | MemSize | | | |

| 0x0000000000000000 | 0x0000000000004000 | 0x0000000000004000 | E | 200000 | |

| 0x000000000000000 | 0x00000000000001cc | 0x00000000000001cc | R | | |

| LOAD | 0x0000000000001fe | 0x00000000000011 | | | |

| 0x0000000000000178 | 0x00000000000004b8 | 0x00000000000004b8 | RW | 200000 | |

| GNU_STACK | 0x0000000000000000 | 0x0000000000000000 | | | |

| 0x0000000000000000 | 0x0000000000000000 | 0x0000000000000000 | RW | 10 | |

| GNU_RELO | 0x00000000000001fe | 0x00000000000001fe | | | |

| 0x0000000000000018 | 0x0000000000000018 | 0x0000000000000018 | R | 1 | |

文件中没有节。

第 3 章：文件格式破解

文件中没有动态节（dynamic section）。文件中没有重定位（relocations）。目前不支持 Advanced Micro Devices X86-64 类型的展开节（unwind sections）解码。符号不可用。文件中没有版本信息。有四个程序头描述了 Trouble 的地址空间。程序头的一个重要部分是 `flags` 字段。该字段描述段是可执行、可写还是可读的。四个程序头中有一个只读（r），两个可读可写（rw），一个可读可执行（re）。反汇器会使用 `flags` 字段吗？让我们实验一下。创建一个伪造节表来反转程序头的 `flag` 字段。这将让反汇器认为第一个 LOAD 段描述的空间不可执行，而第二个段是可执行的。节表将包含四个项：

- 1. `SHT_NULL` 节。通常位于节表的开头，如果漏掉会看起来很奇怪。
- 2. `SHT_PROBITS` 节。在该节中，我们将地址空间设置为第一个 LOAD 段。但不是像第一个 LOAD 那样的 re，而是像第二个 LOAD 那样的 rw。该节的名字将是“data”，这样它看起来就像普通的数据节。
- 3. 另一个 `SHT_PROBITS` 节。在该节中，我们将地址空间设置为第二个 LOAD 段。这次将段标记为“re”而不是“rw”。该节的名字应该是“text”，因为它看起来像是一个代码段。
- 4. `SHT_STRTAB` 节。该节将指向文件末尾，你将在那里追加一个新的节列表。我在第三章中包含了此操作的代码。项目名为“fakeHeadersBit”。该项目再次包含两个文件：`CMakeLists.txt` 和 `fakeHeadersBit.cpp`。

第 3 章：文件格式破解

### chap_3_format_hacks/fakeHeadersBit/CMakeLists.txt

```
project(fakeHeadersBit CXX)
cmake_minimum_required(VERSION 3.0)

set(CMAKE_FLAGS "-Wall -Wextra -Wshadow")
add_executable(${PROJECT_NAME} src/fakeHeadersBit.cpp)
```

### fakeHeadersBit.cpp

```cpp
#include <cstdlib>
#include <iostream>
#include <fstream>
#include <iomanip>
#include <cstring>
#include <elf.h>
```

```cpp
/**
 * 此工具的目标是迷惑反汇器，使其认为代码的可执行部分是数据，而数据部分是可执行的。
 *
 * 此工具将向没有节表的二进制文件添加节表。节表由4个头组成：
 * - null header
 * - .data: 该节我们取消了 X 并设置了 W
 * - .text: 该节应该覆盖 .data，但我们设置了 X 并取消了 W
 * - .strhtab: 字符串表
 *
 * 此代码假设二进制文件有两个 LOAD 段。一个段设置了 PF_X，另一个设置了 PF_W。
 */
```

```cpp
/**
 * 编辑 ELF 头以指示有 6 个节头，且字符串表是最后一个。
 * @param[in,out] p_data ELF 二进制文件
 * @return 如果可以添加节表则返回 true，否则返回 false
 */
```

## 第 3 章：文件格式破解

```cpp
bool edit_elf_header(std::string& p_data)
{
    if (p_data[0] != 0x7f || p_data[1] != 'E' || p_data[2] != 'L' ||
        p_data[3] != 'F')
    {
        return false;
    }
    Elf64_Ehdr* ehdr = reinterpret_cast<Elf64_Ehdr*>(&p_data[0]);
    if (ehdr->e_shoff != 0)
    {
        std::cerr << "The binary already has a section table." << std::endl;
        return false;
    }
    if (ehdr->e_shentsize != sizeof(Elf64_Shdr))
    {
        std::cerr << "Unexpected section header size" << std::endl;
        return false;
    }
    ehdr->e_shoff = p_data.size();
    ehdr->e_shnum = 4;
    ehdr->e_shstrnd = 3;
    return true;
}
```

```cpp
bool add_data_section(std::string& p_data, std::string& p_strings)
{
    Elf64_Ehdr* ehdr = reinterpret_cast<Elf64_Ehdr*>(&p_data[0]);
    Elf64_Phdr* phdr = reinterpret_cast<Elf64_Phdr*>(&p_data[0] + ehdr->e_phoff);
    for (int i = 0; i < ehdr->e_phnum; i++, phdr++)
    {
```

## 第 3 章：文件格式技巧

```cpp
if (phdr->p_type == PT_LOAD)
  if ((phdr->p_flags & PF_X) == PF_X)
{
```

```cpp
Elf64_Shdr data_header = {};
data_header.sh_name = p_strings.size();
data_header.sh_type = SHT_PROBITS;
data_header.sh_flags = SHF_ALLOC | SHF_WRITE;
data_header.sh_addr = phdr->p_vaddr;
data_header.sh_offset = phdr->p_offset;
data_header.sh_size = phdr->p_filesz;
data_header.sh_link = 0;
data_header.sh_info = 0;
data_header.sh_addralign = 4;
data_header.sh_entsize = 0;
p_strings.append(".data");
p_strings.push_back("\x00");
```
