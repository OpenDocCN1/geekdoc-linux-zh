
当子程序完成时，控制需要传回主程序；特别是，主程序中执行的下一条指令需要是 `CALL` 指令之后的指令。为了做到这一点，处理器在离开前会将下一条指令的地址压入堆栈

主程序。`CALL` 指令会执行此操作。`RET` 指令会将此地址从栈中弹出并跳转到该位置。

例如，程序 7.3 是一个接受用户输入的程序，它使用一个子程序将 `EBX` 寄存器的值加 1 以递增数字，然后将结果输出给用户。

## 程序 7.3

```asm
;           MOV ESP, 2000H ; initialize the stack
;           ; Eddinas programs must initialize the stack
;           ; Unix programs must not.
;
;           IN EAX, [0]      ; Get a user input
;           MOV EBX, EAX     ; EBX is where the subroutine works.
;           CALL subpr       ; Leave for the subroutine.
;           MOV EAX, EBX     ; Back now from the subroutine!
;           OUT [1], EAX     ; Output the incremented value
;           RET              ; Go back to Eddinas.
; subpr:
;           INC EBX          ; Subprogram does its job.
;           RET              ; Go back to the main program.
```

对于一个更复杂的例子，考虑以下算法。该算法是一个著名的未解决数学问题——考拉兹猜想（Collatz Problem）的核心。

- 如果 `x` 是偶数，将其除以 2

- 如果 `x` 是奇数，将其乘以 3 并加 1。

- 重复此过程，直到 `x = 1`。

假设我们需要一个程序来执行此算法，并计算直到 `x` 的值变为 1 所需多少步。

由于判断一个数是偶数还是奇数，或者将其除以 2 都需要循环，如果我们要使用加法、减法和条件跳转指令，那么设计一个子程序来执行此操作是合理的。具体来说，假设我们分配给子程序的任务是检查 `EAX` 寄存器，如果 `EAX` 是偶数，则将 `EAX` 的一半存储在 `EBX` 中，否则在 `EBX` 中存储零。我们可以按以下方式编写此子程序：

## 程序 7.4

```asm
HAF: MOV ECX, EAX
     MOV EBX, 0
AGN: INC EBX      ; Count the subtractions
     SUB ECX, 2   ; Repeatedly subtract 2
     JG AGN       ;
     JZ DUN       ; It comes out even
     MOV EBX, 0   ; It's not even.
DUN: RET
```

有了这个子程序，我们现在可以编写一个主程序来执行程序 7.4。

## 7.3 参数传递

栈最重要的功能之一是用于参数传递。例如，假设在 C 程序中调用了字符代码转换函数 `tolower()`。

标准 C 库 `ctype.h` 中的 `tolower()` 函数将字符代码转换为小写。例如，在使用 ASCII 的机器上，如果给定的输入参数是 65（'A' 的 ASCII 代码），它将返回 97（'a' 的 ASCII 代码）。输入参数被推入栈中。因此，相同函数调用的汇编代码如下所示：

## 程序 7.5

```c
#include <ctype.h>

main()
{
    int x, y;

    x = 65; /* x = 'A' */
    y = tolower(x); /* y = 'a' */
}
```

```asm
    MOV EBX,  65
    PUSH EBX
    MOV EDX,  0
    IN EAX, [DX]
ABC:  CMP EAX,  1         ;
      JE FIN              ;If EAX = 1 then it's over.
      INC EDX             ;Use EDX as the counter.
      CALL HAF            ;This is the subroutine call!
      CMP EBX,  0         ;EBX = 0 means EAX is odd
      JE ODD              ;
      MOV EAX, EBX        ;If not then EBX is half of EAX
      JMP ABC
ODD:  MOV EBX,  EAX       ;Triple EAX and add 1
      ADD EAX, EBX
      ADD EAX, EBX        ;
      INC EAX
      JMP ABC             ;
FIN:  MOV EAX,  EDX       ;EDX contains the final count.
      MOV EDX,  1
      OUT [DX], EAX
      RET
```

## 程序 7.6

```asm
    CALL tolower
    ADD ESP, 4
```

虽然使用栈来存储返回值看起来似乎是一个自然的想法，但更常见的是使用寄存器。在 x86 的 GNU C 中，返回的整数值存储在 `EAX` 寄存器中。不同语言在谁负责从栈中弹出参数方面存在差异。在 Fortran、Basic 和 Pascal 中，子程序负责弹出栈，但在 C 中，调用程序负责弹出栈。这就是为什么在刚刚展示的调用程序中出现 `ADD ESP, 4` 指令的原因。

不同语言在将参数推入栈中的顺序上也有所不同。C 语言从右侧开始推送参数。假设我们定义了一个整数幂函数 `ipow()`：

```c
    int ipow(int base, int exponent);
```

调用此函数以计算 $2^3$ 的汇编代码如下所示：

```asm
    MOV EBX,  3
    PUSH EBX
    MOV EBX,  2
    PUSH EBX
    CALL ipow
    ADD ESP, 8
```

在此调用之后，结果 `ipow(2, 3) = 8` 将存储在 `EAX` 寄存器中。

### 7.3.1 全局汇编指令

在 GNU 编译器生成的 `.o` 文件中，诸如 `printf` 或 `tolower` 等需要外部链接的符号在符号表中的编码方式不同。如果没有这种特殊编码，GNU 链接器将跳过它们，导致链接失败。为了获得这种特殊编码，汇编语言源代码必须特别指示哪些符号将接受这种处理。GNU 汇编器和 Edlinas 识别一条汇编指令，该指令会使汇编器在符号表中将符号编码为可供链接使用。其语法为：

```asm
.globl symbol
```

在 NASM 中，语法为：

```asm
global symbol
```

### 7.3.2 从 C 调用汇编

如果从 C 调用 `half` 子程序，它不会正常工作，因为它没有在 `EAX` 寄存器中返回值。此外，它没有推送其使用的寄存器。在下方的代码中，`ECX` 被推送，因为它被使用，且调用程序可能正在将其用于其他用途。我们还需要使用 `global` 指令使函数名可见。

我们刚刚编写了一个汇编函数，可以从 C 程序中调用。C 程序将调用参数存储在栈中。它将被调用程序推送的返回地址和刚刚推送的 `ECX` 的内容所掩埋。这两项在栈上占用 8 个字节，因此调用参数在地址 `ESP` + 8 处访问。结果存储在 `EAX` 中，而不是 `EBX`。要在 Edlinas 中将目标代码保存为 `.o` 文件，请使用 `o` 键。要使用 NASM 生成目标代码文件，请输入：

## 程序 7.7
