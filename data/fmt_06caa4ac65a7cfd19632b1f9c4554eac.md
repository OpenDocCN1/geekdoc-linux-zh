
`MOV` `ESI`, `200H` ; 初始化指向 x 的指针。

;

; y = y + x

`MOV` `EDX`, `40H` ; 循环需要执行 64 次迭代。

`CLC` ; 清除进位标志。

`XYZ:` `MOV` `EAX`, `[ESI]` ; 将 4 个源字节载入处理器。

`ADC` `[EDI]`, `EAX` ; 执行加法运算。

`INC` `ESI`

`INC` `ESI` ;

`INC` `ESI` ; 这样写很不优雅。

`INC` `ESI`

`INC` `EDI` ; 但在此处使用 `ADD` 指令

`INC` `EDI` ; 会清除进位标志。

`INC` `EDI`

`INC` `EDI`

`DEC` `EDX` ; 递减循环计数器。

`JNZ` `XYZ` ; 检查循环是否结束。

这些是如果使用 `[imm]` 格式将会产生的指令行。

乍一看，似乎我们可以用 `ADD` 指令代替多个 `INC` 指令来做得更好。但这实际上会破坏一切。由于我们使用循环以每次 4 字节的方式从最低有效字节向最高有效字节移动，我们遇到了进位标志的问题。如果在两次执行 `ADC` 指令之间，我们使用 `ADD` 指令将数值向下移动 4 个字节，我们就破坏了进位标志。在第 4 章中指出，进位标志不受 `INC` 和 `DEC` 指令的影响。这个晦涩的小例外背后的原因现在变得清晰了。多字节算术需要一个能够承受循环计数器调整的进位标志。由于它们不影响进位标志，`INC` 和 `DEC` 指令可用于执行无害的循环计数器调整。通过四个 `INC` 指令加上 4 并不美观，但它是有效的。

从占用内存空间的角度来看，这段代码并不算差，因为内存很便宜。但从增加循环执行时间的角度来看，它很糟糕。如果有一个地方执行时间代价高昂，那就是嵌套循环的内部，而这恰恰是那些额外的 `INC` 指令所在的地方。

另一种内存格式在处理这个问题时非常有用。

### 6.2.3 [reg+scale*reg+imm] 格式

最通用的内存格式是 `[reg + scale * reg + imm]` 格式，其中 `scale` 是一个比例因子，必须是 1、2、4 或 8。乘以比例因子的寄存器被称为**索引寄存器**。另一个寄存器被称为**基址寄存器**。某些字段可以省略。这给了我们各种格式的效果，包括

- `[scale*reg + imm]`
- `[reg + scale*reg]`
- `[reg + reg + imm]`
- `[reg + imm]`
- `[reg + reg]`

除了前面已经讨论过的 `[reg]` 和 `[imm]` 格式。很难相信具有这种复杂度的指令是硬编码在处理器中的。但所有这种复杂度在指令长度方面的代价实际上只是为使用此通用格式指令多了一个字节的代码。这个字节被称为 `SIB` 字节，既是 scaled-index-base 字节的缩写，也是 `ModR/M` 字节的“兄弟”。

回到 Program 6.3 中重复 `INC` 指令的问题，请注意，比例为 4 的因子会在索引寄存器递增 **1** 时将地址增加 **4**。在 Program 6.5 所示的代码中，使用 `[scale*reg + imm]` 格式来引用源和目标内存位置。在此代码中，我们看到单个 `INC` 指令取代了 Program 6.3 中的八个 `INC` 指令。

#### Program 6.5

```assembly
;
;	Edlinas program which finds 256-byte powers of 3.
;	Store the 256 bytes of x starting at memory address 100H.
;	Store the 256 bytes of y starting at memory address 200H.
		MOV EBX, 3 ; Initialize base.
		MOV EDX, 1 ; Initialize exponent.
;	y = 3
		MOV EAX, 0 ; Do the adding in EAX.
		MOV EDI, 40H ; Loop needs 64 iterations.
ZRO:		DEC EDI
		MOV [4*EDI + 200H], EAX
		JNZ ZRO
		MOV [4*EDI + 200H], EBX
;
;	x = y. Main infinite loop starts here.
;	
LUP:		MOV EDI, 40H ; Loop needs 64 iterations.
		MOV ESI, EBX ; Initialize main loop counter.
BEG:		DEC ESI
		MOV EAX, [4*EDI + 200H]
		MOV [4*EDI + 100H], EAX
		JNZ BEG
;	y = y + x
AGN:		MOV ECX, 40H ; Loop needs 64 iterations.
XYZ:		MOV EAX, [4*EDI + 200H]
		ADC EAX, [4*EDI + 100H]
		MOV [4*EDI + 200H], EAX
		INC EDI
		DEC ECX
		JNZ XYZ
;		DEC ESI
		JNZ AGN
;		INC EDX
		JMP LUP
```

一种不被允许的变体是在两个操作数位置都使用内存引用。没有 x86 处理器指令同时使用内存作为源和目的操作数。例如，指令

```assembly
ADD [EAX], [EBX]
```

并不存在。然而，确实有涉及从内存读取和写入内存的指令；例如，`INC [EAX]` 既从地址在 `EAX` 中的内存位置读取，又写入该位置。称为 *load/store* 的体系结构不允许混合处理器操作和内存操作。加载/存储体系结构中访问内存的唯一命令是 *load* 和 *store*。

### 6.2.4 16 位地址

在 6.2.2 节中介绍了内存寻址的 `[reg]` 格式，其中 `reg` 可以是八个 32 位通用寄存器中的任何一个。8086 和 80286 也使用 `[reg]` 格式。并非所有八个 16 位寄存器都允许使用；然而，只有 `BP`、`BX`、`SI` 和 `DI`。还有一种 `[reg + reg + imm]` 形式。`imm` 必须是一个 16 位数字。如果使用两个寄存器，允许的组合只有 `BP + SI`、`BP + DI`、`BX + SI` 和 `BX + DI`。由于这些限制很容易忘记，不习惯 16 位地址的程序员可能会发现自己使用了不允许的地址形式。大多数程序员会尽量避免在可能的情况下使用 16 位寻址。

这些 16 位内存地址形式可用于 80386。当它们出现在 32 位代码中时，必须向机器码应用一个特殊前缀 `67H`，以通知处理器 `ModR/M` 字节中的内存地址位是使用旧的 16 位编码系统编码的。这个前缀被称为地址大小前缀。它与第 5 章 5.5 节中讨论的操作数大小前缀类似。

### 6.2.5 CISC 与 RISC

x86 计算机通常被认为是一个复杂指令集计算机（CISC）。这 partly 是因为复杂的寻址，例如 `[EDX + 4*ESI + ABC]` 内存操作数。像 SUN 和 MIPS 工作站这样的机器基于这样的想法：通过简化指令并减少指令数量，它们变得更易于执行且速度更快。这可以抵消编写程序需要更多这类小指令的事实。基于此理念的计算被称为 RISC（精简指令集计算）。RISC 与 CISC 的问题并不是像小端序与大端序那样的非此即彼的问题。RISC 是一组可以部分采用、不同程度上采用的功能特性。486 和 Pentium 处理器能够与早期的 RISC PowerPC 处理器竞争的一个原因是它们采用了部分 RISC 理念。尽管允许在 Pentium 上使用 CISC 指令，但如果使用类似 RISC 的指令子集进行编程，其运行速度会更快。

尽管名字如此，Pentium II 和 Pentium Pro 已全面转向 RISC 架构。内部使用的指令集是纯 RISC 指令集。传统的 x86 指令在执行前会在内部转换为 RISC 指令。在某种意义上，苹果营销人员在 Pentium 身上挂的“此路不通”标签是正确的。但具有讽刺意味的是，386 汇编语言现在比以往任何时候都更强大。

## 6.3 操作数大小歧义

在大多数双操作数指令中，两个操作数必须具有相同的大小。因此，当在此类上下文中使用内存操作数时，如果另一个操作数是寄存器操作数，可以确定其引用的字节数。例如，在 `ADD [EBX], AX` 中，内存操作数 `[EBX]` 必须引用两个内存字节，因为 `AX` 是一个双字节寄存器。然而，当内存操作数与立即数操作数一起使用时，结果会产生歧义。例如，以下命令具有歧义：

```assembly
MOV [EBX], 5
```
