
CALL HAF ;这是一个子程序调用！

CMP EBX, 0 ;EBX = 0 意味着 EAX 是

JE ODD

MOV EAX, EBX ;如果不是 EBX 是 EAX 的一半

JMP ABC

ODD: MOV EAX, EB ;将 EAX 三倍并加1

ADD EAX, EBX ;

ADD EAX, EBX ;

INC EAX

JMP ABC

FIN: MOV EAX, ED ;EDX 包含最终计数。

MOV EAX, 1

OUT [DX], EAX

RET

程序 7.5

```c
#include <ctype.h>
main()
{
    int x,y;
    x = 65; /* x = 'A' */
    y = tolower(x); /* y = 'a' */
}
```

程序 7.6

```assembly
CALL tolower
ADD ESP, 4
```

虽然使用栈来传递返回值似乎是一个自然的想法，但更常见的方法是使用寄存器。对于 x86 的 gnu C，整数返回值存储在 `EAX` 寄存器中。不同语言对于由子程序还是主程序负责弹出栈空间存在差异。在 Fortran、Basic 和 Pascal 中，由子程序弹出栈，但在 C 语言中，由调用程序负责。这就是在刚才展示的调用程序中使用 `ADD ESP, 4` 指令的原因。

不同语言在参数入栈的顺序上也不同。C 从右侧开始推入参数。假设我们定义了一个整数幂函数 `ipov()`：

```c
int ipov(int base, int exponent);
```

调用此函数计算 `2^3` 的汇编代码如下：

```assembly
MOV EBX, 3
PUSH EBX
MOV EBX, 2
PUSH EBX
CALL ipov
ADD ESP, 8
```

此调用后，结果 `ipov(2, 3) = 8` 将存储在 `EAX` 寄存器中。

### 7.3.1 全局汇编指令

在 gnu 编译器产生的 `.o` 文件中，像 `printf` 或 `tolower` 这样需要外部链接的符号在符号表中的编码方式不同。如果没有这种特殊编码，gnu 链接器在通过链接传递它们将会失败。为了获得这种特殊编码，汇编源代码必须特殊地指定需要这种处理的符号。gnu 汇编器和 Edlin 都能识别一种汇编器指令，它会使汇编器将符号表中的符号编码为可链接状态。其语法为：

```
.global symbol
```

在 NASM 中，语法为：

```assembly
global symbol
```

### 7.3.2 从 C 调用汇编

如果从 C 调用 `HAF` 子程序将无法工作，因为它没有在 `EAX` 寄存器中返回值。此外，它没有推入它所使用的寄存器。在下面的代码中，`ECX` 被推入栈是因为它被使用了，而调用程序可能正将其用于其他地方。我们还需要使用全局指令使该函数可见。

我们用汇编编写了一个函数，可以在 C 程序中调用它。C 程序会将调用参数存储在栈上。它会被埋在调用程序推入的返回地址以及刚刚推入的 `ECX` 内容之下。这两项内容在栈上占据了 8 个字节，因此通过地址 `ESP + 8` 访问调用参数。结果存储在 `EAX` 而不是 `EBX`。要像 Edlin 那样将目标代码保存为 `.o` 文件，请使用 `o` 键。使用 NASM 生成目标文件，输入

## 7.4 节 递归

```assembly
global half ;或 Edlinas 中的 .globl
half:
PUSH ECX ;ECX 被使用了，所以推入它。
MOV ECX, [ESP + 8] ;栈顶 + 2 整数
MOV EAX, 0
INC ECX ;计数减法
SUB ECX, 2 ;反复减去 2
JG AGN ;
JZ DUN ;如果是偶数
AGN:
MOV EAX, 0 ;不是偶数。
DUN:
POP ECX
RET
```

程序 7.7

```bash
linuxbox$ nasm -f elf half.asm
```

`-f elf` 指定了目标代码文件的格式，Linux elf 格式在第 8 章讨论。程序 7.8 是调用 `half()` 的 C 程序，其汇编代码在程序 7.7 中。如果程序 7.8 保存在 `colatz.c` 中，则使用 `gcc` 编译并链接它：

```bash
linuxbox$ gcc collatz.c half.o
```

.4 递归

在递归中，大部分计算工作是通过参数传递完成的。递归定义通常可以转换为计算有效的程序。这通常使用斐波那契数来演示。

```
fib(k) = if k < 2 fib(k - 1) + fib(k - 2) otherwise.
```

程序 7.9 显示了这种定义如何转换为 C。在汇编语言中，我们可以这样做，前提是必须推入除 `EAX` 以外的寄存器。程序 7.10 显示了如何仅使用 `ECX` 和 `EAX`。从 C 测试此程序，可以使用小型调用程序，如程序 7.11。像 Edlinas 那样测试，还需要初始化栈，如程序 7.3 所示。

### 第 7 章 栈

```c
main(){
    int count,y;
    count = 0;
    printf("Enter a number: ");
    scanf("%d", &x);
    while(x != 1) {
        count = count + 1;
        y = half(x); /*这是一个子程序调用！ */
        if (y != 0) {
            x = y;
        } else {
            x = 3*x + 1;
            printf("\n x = %d.\n", x);
        }
    }
    printf("\n were %d iterations.\n", count);
}
```

程序 7.8

```c
int fib(int k){
    int d;
    if(k < 2) {
        d = 1;
    } else {
        d = fib(k-1) + fib(k-2);
    }
    return d;
}
```

程序 7.9

```assembly
fib: global fib
PUSH ECX ;让我们访问 ECX
MOV EAX, [ESP + 8] ;访问参数
CMP EAX, 2 ;如果 k < 2
JAE ELS
MOV EAX, 1 ;将返回值放入 EAX
JMP DUN
ELS: DEC EAX ;获取 k-1
MOV ECX, EAX ;EAX 将被覆盖！
PUSH ECX ;将 k-1 作为参数
CALL fib ;在 EAX 中返回 fib(k-1)
ADD ESP, 4 ;移除参数
DEC ECX ;获取 k-2
PUSH ECX ;将 k-2 作为参数
MOV ECX, EAX ;将 fib(k-1) 放入 ECX
CALL fib ;在 EAX 中返回 fib(k-2)
ADD ESP, 4 ;移除参数
ADD EAX, ECX ;相加两个部分结果
POP ECX ;恢复原始值
```

程序 7.10

```c
main(){
    int x, y;
    printf("Enter a number: %d");
    scanf("%d", &x);
    y = fib(x);
    printf("%d\n", y);
}
