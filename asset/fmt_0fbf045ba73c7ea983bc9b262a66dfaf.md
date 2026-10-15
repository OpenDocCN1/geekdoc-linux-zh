
132 `struct vm86_plus_info_struct` `vm86plus`;

133 };

图 24.4 扩展的 `vm86_struct`

- 116-122 这是 `vm86_struct` 中包含的额外信息（见第 132 行）。它由一个长位图和一个 32 字节数组组成。
- 117 当该位为 0 时，如果在处理异常后启用了中断，处理器管理器应立即返回 32 位模式。控制程序（例如 `dosemu`）想要自己处理硬件中断（见 2.6.1 节）。
- 118 此位由 DOS 调试器使用。如果设置，则第 122 行的 `vm86dbg_intxxtab[]` 字段中的信息是有效的。

119 第 2 位也用于 DOS 调试器。它指定 8086 程序应在单步模式下运行。

120 第 3–30 位未使用。

121 尽管用户可能提供 `vm86_struct` 或 `vm86plus_struct` 格式的信息，但在内部，进程管理器始终以后者的扩展格式维护这些信息。因此，尽管该信息一直存在那里，但有时 `vm86_info_struct` 是有效的，而其他时候则无效。第 31 位用于区分这一点：当设置时，它表示 `vm86plus_info_struct` 中的数据是有效的。

122 该数组是一个位图，256 个中断中的每一个都有一个条目。DOS 调试器会为想要在 32 位保护模式下自行处理的任何中断设置相应的位。

125–133 这是扩展结构。它与第 24.1.1.1 节中的 `vm86_struct` 相同，但增加了第 132 行。

## 24.1. 栈布局

无论上一节中描述的数据结构实际上由用户提供，它们始终保留在用户地址空间中。然而，一个稍微扩展的版本是构建在内核栈上的。
标准的栈布局（如 32 位保护模式所示）是 `struct pt_regs` 结构（见第 10.3.1.1 节）。在 vm86 模式下，寄存器只有 16 位宽。但用于保存寄存器的栈布局通过使用填充字段变得与 `struct pt_regs` 相似。在这种结构中，指针可以从一种类型转换为另一种类型。

### 24.1.2.1 vm86 栈帧

进入 vm86 模式（第 24.4.1 节）时在栈上构建的数据结构格式如如图 24.5 所示，来自 `<asm-i386/vm86.h>`。

```
173 struct kernel_vm86_struct {

174     struct kernel_vm86_regs       ;

183 #define VM86_TSS_ESP0 flags

184     unsigned long               flags;

185     unsigned long               screen_bitmap;

186     unsigned long               cpu_type;

187     struct revector_struct      int_revector;

188     struct revector_struct      int21_revector;

189     struct vm86plus_info_struct vm86plus;

190     struct pt_regs             *regs32;

201 }
```

> **图 24.5** 在 vm86 模式下的内核栈

174 `kernel_vm86_regs` 结构将在第 24.1.2.2 节中进行描述。

183 这定义了该结构中 `flags` 字段（第 184 行）的别名。这是寄存器保存区域的顶部。

184–189 这些字段与 `struct vm86plus_struct` 中的剩余字段相同。

190 这是一个指向 `struct pt_regs` 的指针，该结构是由第 10.4.3.2 节的标准系统调用入口例程在上方栈上构建的。

### 24.1.2.2 内核看到的寄存器保存区域

来自 `arch/i386/kernel/vm86.c` 的图 24.6 显示了在 vm86 模式下寄存器保存到栈上的顺序。与 `struct pt_regs` 主要区别在于旧的段描述符不再不再，并被内核强制置零，而真实的段描述符位于结构的末尾。

```
struct kernel_vm86_regs {

149    long               ebx;

150    long               ecx;

151    long               edx;

152    long               esi;

153    long               edi;

154    long               ebp;

155    long               __null_ds;

156    long               __null_es;

157    long               orig_eax;

158    long               eip;

159    unsigned short cs, __csh;

160    long               flags;

161    long               esp;

162    unsigned short ss, __ssh;

163    unsigned short es, __esh;

164    unsigned short ds, __dsh;

165    unsigned short fs, __fsh;

166    unsigned short gs, __gsh;

171    };
```

> 图 24.6 内核看到的栈布局

163–166 结构的这部分的大小和顺序上与 `struct pt_regs` 相同。指向其中一个的指针可以毫无问题地指向另一个。

167–170 这些字段在 `struct pt_regs` 中不存在。它们实际上是在 vm86 模式下由中断硬件在其他任何操作之前推入内核栈的。它们也会在（最后）通过 `IRET` 恢复到 vm86 模式。

### 24.1.2.3 结构之间的转换

为了方便从一种寄存器保存区域形式转换为另一种形式，提供了一些宏，用于度量 `struct kernel_vm86_regs` 结构的适当部分；见来自 `arch/i386/kernel/vm86.c` 的图 24.7。

```
60 #define VM86_REGS_PART2 orig_eax

61 #define VM86_REGS_SIZE1(sizeof(struct vm86_regs))

62     &((struct vm86_regs*)0)->VM86_REGS_PART2

63 VM86_REGS_SIZE1
```

图 24.7 `struct vm86_regs` 的大小

这只是在较大的 `struct vm86_regs` 内部 `orig_eax` 处设置一个标记。

此以及后续宏用于从 `struct vm86_regs` 拷贝到 `struct vm86_regs`，反之亦然。`VM86_REGS_SIZE1` 评估 `struct vm86_regs` 的大小，但不包括 `orig_eax` 字段。

此宏评估从 `orig_eax`（包含）到结束部分的结构。

图 24.8 显示了用户提供的结构与在执行 vm86 模式时由进程管理器存储的方式之间的关系。

图 24.8 用户提供的信息

### 24.1.2.4 从 32 位到 16 位和 8 位的转换

来自 `arch/i386/kernel/vm86.c` 的图 24.9 所示的宏便于处理之前节定义的的数据结构。

```
36 #define KVM86      ((struct kernel_vm86_regs *)regs)

37 #define VMPI       (VM86->vm86plus)

43 #define AL(regs)   ((unsigned char*)(regs)->eax)[0]

44 #define AH(regs)   ((unsigned char*)(regs)->eax)[1]

45 #define IP(regs)   ((unsigned short*)(regs)->eip)

46 #define SP(regs)   ((unsigned short*)(regs)->esp)
```
