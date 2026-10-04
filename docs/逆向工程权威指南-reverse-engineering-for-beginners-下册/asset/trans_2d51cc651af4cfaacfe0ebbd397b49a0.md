

```cpp
union {
  DWORD PhysicalAddress;
  DWORD VirtualSize;
} Misc;
  DWORD VirtualAddress;
  DWORD SizeOfRawData;
  DWORD PointerToRawData;
  DWORD PointerToRelocations;
  DWORD PointerToLinenumbers;
  WORD NumberOfRelocations;
  WORD NumberOfLinenumbers;
  DWORD Characteristics;
} IMAGE_SECTION_HEADER, *PIMAGE_SECTION_HEADER;
```

上述代码摘自于：https://msdn.microsoft.com/en-us/library/windows/desktop/ms680341 (vs.85).aspx

简单的说，基于 PointerToRawData 指向原始实体的偏移量 Offset，而虚拟地址 VirtualAddress 就是在 Hiew 的 RVA。

## 6.2.6 重定向 Relocations (relocs)

至少在 Hiew 中，它也可以表示为 FIXUP-s。

重位段是 MS-DOS 时代一直存在于可执行文件的实体段，几乎所有的可执行文件都有这个段。

前文知道，程序可能会被加载到模块的基地址。但是如何处理全局变量等共享数据呢？程序必须通过地址来访问此类数据，然而程序又不能事先知道共享数据的存储地址，为了解决这个问题，我们推出了“位置无关代码/PIC”（详情请阅 67.1）的解决方案。不使用 PIC 来是不行的。

> 是，我们推出了基于“重定向”的地址重定向技术。重定向表记录了该文件被加载到不同基地址时需要修正的地址所指引。

如果 PE 文件声明了一个地址为 0xA10000 的全局变量，那么这个变量的指令地址大致上将会是：

```
A1 00 01 00    mov    eax, [00000000]
```

此时，模块的基地址是 0x400000（默认链接器地址），全局变量的相对虚拟地址 RVA 是 0xA10000。

如果这个模块被加载到基地址为 0x500000 的基地址，那么这个全局变量的真实地址应当被调整为 0x510000。

在上述 opcode 中，变量地址应该是 0xA1（MOV EAX 指令）之后的几个字节。为了让操作系统在重定向时正确处理该地址，PE文件的重定向表必须收集这四个字节的相对地址。

当操作系统的加载器需要这个模块加载到不同的基址时，它会遇到一张重位表中所所有基址，这些基址所指向的数据作为模块的地址指针，减去初始基址（这样就能获得 RVA，也就是相对虚拟基址），并加上新的基址。

如果模块被加载到它的原始基址上，那么操作系统就不会进行重定向处理。

所有全局变量的处理过程都是如此。

重定向的数据结构并不唯一，Windows for x86 重定向一般采用 IMAGE_REL_HIGHLOW 的数据结构。

另外，Huimage 颜色区域显示重定向段，图 7.12 节。

以及 OlyDbg 在内存中用线下的方式标记重定向，图 13.11 节。

## 6.2.7 导出和导入

我们知道，任何执行文件都必须至少地调用由操作系统的提供者或者 DLL 动态库。

广泛地，由于某个模块（来说是 DLL）声明的所有函数，最终会被其他模块（.exe 文件或其他的 DLL）的指令来调用，只是调用方式不同而已。

为此，每一个 DLL 动态库文件都有“导出/exports”表。导出表声明了该模块的函数名称和基址。

同时每一个 exe 和 DLL 文件还有一个“导入”表。这个表声明执行该模块所需的函数名称、以及对应的 DLL 文件。

在加载可执行文件主体的之后，接着在 DLL 的导出列表中查找所需的函数地址，最后把这些地址写到模块的 IAT 中。

由此可见，操作系统的加载器的进程过程中要对比大量的函数名称。但是字符串搜索的效率不会太高。后来又引入了“排序”或“命中”（对应相关数据结构的 Hints 或 Ordinal 表）的导出符号表示法，把函数名称排列为排序，以此解决脱序操作的效率问题。

因此，DLL 只需要在导出表里标注函数的函数“序号”。这显著提升了 DLL 文件的加载速度。

举例来说，调用 MFC 的程序就能通过“序号”调用 mfc.dll 动态链接。而这种程序就不需要导入表（Import Address Table, IAT）中使用字符串。

## 6.2.8 导入段

编译器通常会给导入表及其相关内容分配一个单独的 section（例如 idata），但这次不是一个强制规定。导入段涉及大量的术语，因此理解起来困难。本节将通过典型的例子演示。

导入段的主体是 IMAGE_IMPORT_DESCRIPTOR。它记录着 PE 文件要导入哪些库。在其元素中：

- Name 存储着字符串
- OriginalFirstThunk 字段是 INT 地址
- FirstThunk 字段存储的是 IAT 指针

IAT表的每个成员都是由操作系统解析出来的相对地址（RVA）。
- Hint 字段是一个 16 位整数，“序号”。

加载模块时，如果可以通过序号查找函数名，那么操作系统加载器就不进行字符串对比。外部函数至少有两种调用方法：

① 代码通过 call 形式调用外部函数。从某种意义上，引入函数的地址全部存储到全局空间。第二种方法是对于每个函数进行处理。调用外部函数时，跳转到“重定向值+函数”。这种方法也称为 thunks。如果外部函数的频率足够高，那么链接器完全可以通过 thunk 选择两种方法之一。

③ 这种 old-style binding 静态绑定。在足够情况下，链接器不需要创建 thunk。此时生成的指令是：

```
MOV EAX, (dllfunction)
JMP EAX
```
这种存储的是外部函数的第一个地址。而言之，调用 DLL 时，加载器程序直接替换为地址。需要注意的是代码段都是可读的。我们需要在代码段中增加一个标记 IMAGE_MEM_WRITE。这样的，调用时可能会发生错误（禁止访问）。如果程序只查询一套 DLL 文件里的函数名和地址不变，还能进一步提高加载的速度。现在的 PE 文件中，Thunk 组可以写入外部函数的地址。需要注意的是 DLL 结构的 timestamp 字段。标准 DLL 中，多个文件的地址表（Input Address Table, IAT）都是 PE 头部。是为了优化的考虑而刻意设计的。运行一个执行文件时，exe 文件不会一次性加载到内存中（否则大型程序的加载速度就太慢了），在访问过程中映射到内存里。它的目的就是加速 exe 文件的速度。

## 6.2.9 资源数据

文件中的资源段索引不是资源就是图表、字符串以及属性等界面的支持：该资源与主程序共享一份编译，大部分是为了实现多语言支持：操作系统需要根据用户的设置可以选择相应的资源或文件。而这也带来了一个副作用：由于 PE文件的二进制比较难以编辑，具备 PE 文件知识的人可以借助工具（ResHack）直接修改资源。相关的可以参考书籍。

## 6.2.10 .NET

.NET 程序不会编译成机器码，而是会被编译一种特殊的字节码。严格来说，这种文件由字节结构组成，并不是有意义的 X86 指令。这种程序的入口（OEP）确实是一个跳转：

```
jmp mscore.dll
```

自 Windows XP 起，操作系统的加载器会自动识别格式。有关信息访问：https://msdn.microsoft.com/en-us/library/windows/desktop/ms680341.aspx

## 6.2.11 TLS

TLS 段里存储了 TLS 数据。启动一个新的线程时，TLS 数据是通过该段初始化的。此外，PE 文件约定了 TLS回调。如果声明了 TLS回调，技术广泛应用于 PE 文件的压缩和加密。

- Objdump (cywin版)
- Hiew（可以参考本书）
- Prefile（用于PE文件的工具）
- ResHack（是一个资源编辑器）
- PE_add_import（一个小工具，可以将符号加入PE文件的导入表中）
- PE_patcher（一个小工具，给PE文件打补丁）
- PE_search_refs（一个小工具，可以在执行文件中寻找这些字符串）
- Daniel: https://www.codeproject.com/articles/125/net-format.html

## 6.2.12 Windows SEH

Windows操作系统中，结构异常机制（Structured Exception Handling, SEH）是用来处理异常的。它是语言无关的，与 C++ 面向对象编程（Oriented Object Programming）无关联。本节讲解SEH 的特性。每一个运行都有一个 SEH链，线程信息块（Thread Information Block, TIB）有 SEH 的最后一个。当出现异常时（比如地址访问正确或程序主动用 RaiseException()回调），就会出现异常处理时CPU的状态。操作系统会在 TIB 中寻找 SEH 的最后一个（包含寄存器的值），此时异常处理就会开始检查是否应对这种异常。如果答案是肯定的，那么异常处理就会接手。如果异常处理无法处理这种情况，就会通知操作无法处理，此操作就会逐一尝试异常处理链中的程序，直到能够应对这种异常的程序为止。在异常处理链的末尾有一个大的异常处理程序；它显示一个标准的对话框，通知用户已崩溃，崩溃时CPU的状态是什么，用户是否愿意把这些信息发送给开发者。

img/a13a81a53f80f55074b2e5d2ec754b_1090.png
Windows XP 下的崩溃截图

Error Report Contents

The following information about your process will be reported:

| Exception Information | |
|---|---|
| Code: 0x0000005 | Flags: 0x0000000 |
| Record: 0x0000000000000000 | Address: 0x000000000000401e |

System Information
Windows NT S.1 Build: 2600
CPU Vendor Code: 756E6547 - 49656E69 - 60C5746E
CPU Version: 000206A7 CPU Feature Code: 0AFABBFF
CPU AND Feature Code: 00D1E324

Module 1
crash.exe
Image Base: 0x00400000 Image Size: 0x00000000
Checksum: 0x00000000 Time Stamp: 0x52d1973c

Version Information

The following files will be included in this error report:

```
C:\DDOCUME~1\ADMIN~1\LOCALS~1\Temp\b15_compat.txt
```

img/a13a81a53f80f55074b2e5d2ec754b_1091.png
Windows XP 下的崩溃细节

img/a13a81a53f80f55074b2e5d2ec754b_1092.png

