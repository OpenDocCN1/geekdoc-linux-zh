
工具包通常原生原生运行，这意味着它们生成的对象代码运行在编译它的同一个系统上。如果你在 x86 系统上开发内核并将其加载到另一个（或同一个）x86 系统上，你可以直接使用系统自带的任何编译器。Power Mac 和无数 x86 机器都编译在它们各自架构上运行的代码。但如果我们想在一个平台上编写代码，并在另一个平台上运行它又该呢？

这听起来并不奇怪。考虑一下嵌入式市场。嵌入式系统的实现通常只具有足够的内存和 I/O 来完成工作。无论是控制汽车、路由器还是手机，嵌入式系统中很少有空间容纳完整的原生开发环境（更不用说显示器或键盘了）。

# 9.1.3 链接器

当我们编译一个 C 程序（"hello world!"）时，代码比那三行代码要多得多。链接器的任务是为与模块相关的每个符号找到定义。符号可以是全局的或局部的。全局符号可以定义在模块内部，也可以被模块外部引用。链接器提取这些库，修复指针（重定位），并将它们链接。（注意，用户空间库对内核程序员是不可用的，内核有自己的版本可用。）。静态库在链接时被找到并复制，而动态库或共享库可以在运行时加载并在进程间共享。

# 9.1.4 ELF 对象文件

对象文件的格式因制造商而异。今天，大多数 UNIX 系统使用可执行和链接格式 (`ELF`)。存在许多类型的 ELF 文件，每种类型执行不同的功能。ELF 文件的主要类型包括执行文件、可重定位对象文件以及核心文件或共享库。ELF 格式允许对象文件跨平台和跨架构兼容。图 9.3 展示了一个可执行和非可执行对象文件。

| 非可执行 ELF 对象文件 | 可执行 ELF 文件 |
|---|---|
| ELF Header | ELF Header |
| 程序头部表（可选） | 程序头部表（用于加载的段） |
| Section 1 | Section 1 |
| Section 2 | Section 2 |
| Section 3 | Section 3 |
| ... | ... |
| 节头部表（用于链接的段） | 节头部表（可选） |

图 9.3

可执行与非可执行 ELF 文件

530

第 9 章 • 构建 Linux 内核

ELF 头始终位于 ELF 文件偏移量为 0 的位置。文件中的所有内容都可以通过 ELF 头找到。由于 ELF 头是对象文件中唯一的固定结构，它必须指向并指定文件中各个子结构的大小。所有的 ELF 文件都被划分为相似数据的数据块，称为节（sections）或段（segments）。不可执行的对象文件包含节和一个节头表，而可执行的对象文件必须包含段和一个程序头部（program header table）。

### 9.1.4.1 ELF 头

ELF 头记录在 Linux 结构 `elf32_hdr` 中（对于 32 位系统是如此；对于 64 位系统，有 `elf64_hdr` 结构）。让我们来看这个结构：

```c
include</linux/elf.h>
234 #define EI_NIDENT 16
235
237 typedef struct elf32_hdr{
238 unsigned char e_ident [EI_NIDENT];
239 Elf32_Half e_type;
240 Elf32_Half e_machine;
241 Elf32_Word e_version;
242 Elf32_Addr e_entry; /* Entry point */
243 Elf32_Off e_shoff;
244 Elf32_Word e_flags;
245 Elf32_Half e_ehsize;
246 Elf32_Half e_phentsize;
247 Elf32_Half e_phnum;
248 Elf32_Half e_shsize;
249 Elf32_Half e_shnum;
250 Elf32_Half e_shstrndx;
251 Elf32_Elddr;};
```

#### 第 237 行

`e_ident` 字段持有 16 字节的魔数，它用于识别文件是否为 ELF 文件。

第 238 行

`e_type` 字段指定对象文件的类型，例如可执行文件、可重定位文件或共享对象文件。

## 9.1 工具链

第 239 行

`e_machine` 字段识别编译该文件的系统架构。

第 240 行

`e_version` 字段指定对象文件的版本。

第 241 行

`e_entry` 字段持有程序的起始地址。

第 242 行

`e_phoff` 字段持有程序头部表的偏移量（字节为）。

第 243 行

`e_shoff` 字段持有节头表的偏移量（字节为）。

第 244 行

`e_flags` 字段持有特定于处理器的标志位。

第 245 行

`e_ehsize` 字段持有 ELF 头的大小。

第 246 行

`e_phentsize` 字段持有程序头部表中每个条目的的大小。

第 247 行

`e_phnum` 字段包含程序头部条目的数量。

第 248 行

`e_shentsize` 字段持有节头表中每个条目的的大小。

第 249 行

`e_shnum` 字段持有节的条目数量，这表示文件中节的数量。

第 250 行

`e_shstrndx` 字段持有节头部中节字符串索引。

### 9.1.4.2 节头表

节头表是一个 `Elf32_Shdr` 类型的数组。它在 ELF 文件中的偏移由 ELF 头中的 `e_shoff` 字段给出。文件中的每个节都有一个节头表：

```c
include/linux/elf.h
332 typedef struct {
333     Elf32_Word sh_name;
334     Elf32_Word sh_type;
335     Elf32_Word sh_flags;
336     Elf32_Addr sh_addr;
337     Elf32_Off sh_offset;
338     Elf32_Word sh_size;
339     Elf32_Word sh_link;
340     Elf32_Word sh_info;
341     Elf32_Word sh_addral;
342     Elf32_Word sh_entsize;
343 } Elf32_Shdr;
```

#### 第 333 行

`sh_name` 字段包含节的名字。

第 334 行

`sh_type` 字段包含节的内容。

第 335 行

`sh_flags` 字段包含杂杂属性的信息。

第 336 行

`sh_addr` 字段持有节在内存映像中的地址。

第 337 行

`sh_offset` 字段持有该节在 ELF 文件中第一个字节的偏移量。

第 338 行

`sh_size` 字段包含节的大小。

第 339 行

`sh_link` 字段包含链接表的索引，这取决于 `sh_type`。

第 340 行

`sh_info` 字段包含额外信息，取决于 `sh_type` 的值。

第 341 行

`sh_addral` 字段包含地址对齐。

第 342 行

`sh_entsize` 字段在持有固定大小表时，包含节的条目大小。

### 9.1.4.3 不可执行节

ELF 文件被划分为若干节，每个节都包含特定的类型信息。`e_shnum` 表示文件中节的数量。

| 节名 | 描述 |
| :--- | :--- |
| .bss | 未初始化的数据 |
| .comment | 编译器使用信息 |
| .data | 已初始化的数据 |
| .debug | 调试信息 |
| .dynsym | 动态链接 |
| .fini | 退出代码 |
| .init | 初始化代码 |
| .interp | 动态解释器的位置 |
| .line | 行号 |
| .note | 杂项信息 |
| .plt | 过程跳转表 |
| .rel | 重定位信息 |
| .rodata | 只读数据 |
| .shstrtab | 节名称 |
| .symtab | 符号表 |
| .strtab | 字符串表 |
| .text | 可执行代码 |

### 9.1.4.4 程序头部

可执行文件或共享对象的程序头部是一个数组，每个条目描述一个段。它包含了关于段如何到内存的信息：

```c
include/linux/elf.h
276 typedef struct {
277     Elf32_Word p_type;
278     Elf32_Off p_offset;
279     Elf32_Addr p_addr;
280     Elf32_Addr p_paddr;
281     Elf32_Word p_filesz;
282     Elf32_Word p_memsz;
283     Elf32_Word p_flags;
284     Elf32_Word p_align;
285 } Elf32_Phdr;
```

`e_phnum` 表示程序段的数量。

#### 第 277 行

`p_type` 字段描述段的类型。
