
函数所需的前4参数由寄存器传递。MIPS平台有两个特殊的寄存器：`HI`和`LO`。用来存储`MUL`指令计算结果——64位的。只有`MFLO`指令访问`HI`和`LO`。其中`MFLO`负责低32位。在本例中将低32位存储到`v0`。由于实例访问高2位，被弃了。我们的程序就是设计的：积是32位的整型数据。最终`ADDU` (Add Unsigned) 指令计算三个参数的和。

在MIPS平台上，`ADD`和`ADDDU`是不同的指令。两者的区别体现在溢出的处理上。`ADD`指令可以触发溢出，溢出有时候是必要的。`C++`不支持这种机制，所以本例中使用`ADDDU`而非`ADD`指令。

此后寄存器存储了32位运算结果。`main()`函数使用了`JAL`（Jump and Link）指令。`JAL`和`JALR`指令，前者使用的是相对地址—偏移量，后者跳转到绝对地址。`JALR`代表寄存器。由于`f()`函数和`main()`函数都位于同一个`object`文件，所以`f()`函数的相对地址是已知的，可以计算出来。

# 第9章 返回值

## 返回值

在x86系统里，被调用函数返回值通常通过`EAX`寄存器返回。若返回`byte`或`char`数据，则返回值将存储在`EAX`寄存器的低位——`AL`寄存器。如果返回值是浮点型数据，那么返回值将存储在`FPU`的`ST(0)`寄存器里。`ARM`系统的情况简单一些，它通常使用`R0`寄存器返回。

## 9.1 void类型的返回值

函数`main()`的数据类型通常是`void`而不是`int`，程序如何处理返回值？

调用`main()`有关代码大致是这样的：

```
push envp

push argv

push argc

call main

push eax

call exit
```

将其转换为源代码，也就是：

```c
exit(main(argc, argv, envp));
```

如果声明`main()`的数据类型是`void`，则`main()`函数不会返回任何值（没有`return`指令）。不过在`main()`函数退出时，`EAX`寄存器含有调用函数残留的确定，也就是说此时`EAX`存储的值应该是上一个函数——`puts()`函数的返回值。我们将一段`bash`脚本，观察程序的退出状态（返回值）。

## 指令清单9.2 tst.sh

```bash
#!/bin/sh

./hello_world

echo $?
```

执行上述脚本之后，我们将看到：

```
$ ./tst.sh

Hello, world!

14
```

```assembly
mov ecx, DWORD PTR _y$[esp-4]

mov eax, DWORD PTR _x$[esp-4]

lea edx, DWORD PTR [eax+ecx]

imul eax, ecx

mov ecx, DWORD PTR _product$[esp-4]

push esi

mov esi, DWORD PTR _sum$[esp]

mov DWORD PTR [esi], edx

mov DWORD PTR [ecx], eax

pop esi

ret 0
```

```assembly
_main PROC

	push OFFSET _product

	push _sum

	push 456             ; 000001c8H

	push 123             ; 0000007b

	call _f1

	mov eax, DWORD PTR _product

	mov ecx, DWORD PTR _sum

	push eax

	push ecx

	push OFFSET $SG2803

	call DWORD PTR __imp__printf

	add esp, 28          ; 000000cH

	xor eax, eax

	ret 0

_main ENDP
```
