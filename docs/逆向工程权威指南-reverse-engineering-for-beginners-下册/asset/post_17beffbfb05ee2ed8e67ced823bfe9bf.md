
printf ("val=%d\n", val);

// deinstall exception handler
asm
{
record mov    eax, [ESP]      // remove our EXCEPTION_REGISTRATION
      mov    FS:(0), EAX         // install previous record
      add    esp, 8             // clean our EXCEPTION_REGISTRATION
}

return 0;
```

在Win32环境下，FS: 段寄存器的数据就是线程块（Thread Information Block, TIB）的指针。在TIB中的第一个元素是异常处理链里最后一个处理程序的地址。所谓“注册”异常处理程序就是把定义的异常处理程序的地址链接到这个异常处理指针链。在注册异常处理程序时，需要使用一种名为_EXCEPTION_REGISTRATION的数据结构。它其实是一个简单的单向链表，使用结构存储各项节点的链点的数据。

指令清单68.1 MSVC/VC/crt/src/exsup.inc

```
\EXCEPTION\_REGISTRATION struct {
    prev dd ?;
    handler dd ?;
}\EXCEPTION_REGISTRATION ends
```

可见，每个节点的“handler”都是一个异常处理程序的起始地址，每个节点的“prev”字段都是上一个节点的地址指针。而最后一个节点的“prev”字段的值为0xFFFFFFFF (-1).

![](img/a13a81a53f805f55074b2e5d2ec754b6_1095_0.png)

在注册好我们自定义的异常处理程序以后，我们将调用RaiseException()函数、触发用户异常的处理过程，异常处理程序首先检查异常代码，如果异常代码为0xE1223344，它就会返回ExceptionContinueExecution，这个返回值代表“已纠正CPU的状态”（通过调整EIP/ESP寄存器实现）、“操作系统会继续执行后续指令”。如果把异常代码设为其他值，那么函数的返回值就会变为ExceptionContinueSearch。如果如此，操作系统就会遇到尝试一次其他的异常处理程序，万一没有找到有关问题（并不只是仅仅是错误代码）的异常处理程序，我们就会看到标准的Windows进程崩溃对话框。

系统异常（system exceptions）和用户异常（user exceptions）之间的区别是什么？系统异常的有关信息是：

| 由WinBase定义的异常状态 | 在ntstatus.里的对应状态 | 错误编号 |
|---|---|---|
| EXCEPTION_ACCESS_VIOLATION | STATUS_ACCESS_VIOLATION | 0xC0000005 |

| 由WinBase.h定义的异常状态 | 在ntstatus.h里的相应状态 | 错误编号 |
|---|---|---|
| EXCEPTION_DATATYPE_MISALIGNMENT | STATUS_DATATYPE_MISALIGNMENT | 0x80000002 |
| EXCEPTION_BREAKPOINT | STATUS_BREAKPOINT | 0x80000003 |
| EXCEPTION_SINGLE_STEP | STATUS_SINGLE_STEP | 0x80000004 |
| EXCEPTION_ARRAY_BOUNDS_EXCEEDED | STATUS_ARRAY_BOUNDS_EXCEEDED | 0xC000008C |
| EXCEPTION_FLT_DENORMAL_OPERAND | STATUS_FLOAT_DENORMAL_OPERAND | 0xC0000008D |
| EXCEPTION_FLT_DIVIDE_BY_ZERO | STATUS_FLOAT_DIVIDE_BY_ZERO | 0xC0000008E |
| EXCEPTION_FLT_INXACT_RESULT | STATUS_FLOAT_INXACT_RESULT | 0xC000008F |
| EXCEPTION_FLT_INVALID_OPERATION | STATUS_FLOAT_INVALID_OPERATION | 0xC00000090 |
| EXCEPTION_FLT_OVERFLOW | STATUS_FLOAT_OVERFLOW | 0xC00000091 |
| EXCEPTION_FLT_STACK_CHECK | STATUS_FLOAT_STACK_CHECK | 0xC00000092 |
| EXCEPTION_FLT_UNDERFLOW | STATUS_FLOAT_UNDERFLOW | 0xC00000093 |
| EXCEPTION_INT_DIVIDE_BY_ZERO | STATUS_INTEGER_DIVIDE_BY_ZERO | 0xC00000094 |
| EXCEPTION_INT_OVERFLOW | STATUS_INTEGER_OVERFLOW | 0xC00000095 |

| 由WinBase.h定义的异常状态 | 在ntstatus.h里的相应状态 | 错误编号 |
|---|---|---|
| EXCEPTION_PRIV_INSTRUCTION | STATUS_PRIVILEGED_INSTRUCTION | 0xC0000096 |
| EXCEPTION_IN_PAGE_ERROR | STATUS_IN_PAGE_ERROR | 0xC0000006 |
| EXCEPTION_ILLEGAL_INSTRUCTION | STATUS_ILLEGAL_INSTRUCTION | 0xC000001D |
| EXCEPTION_NONCONTINUABLE_EXCEPTION | STATUS_NONCONTINUABLE_EXCEPTION | 0xC0000025 |
| EXCEPTION_STACK_OVERFLOW | STATUS_STACK_OVERFLOW | 0xC00000FD |
| EXCEPTION_INVALID_DISPOSITION | STATUS_INVALID_DISPOSITION | 0xC0000026 |
| EXCEPTION_GUARD_PAGE | STATUS_GUARD_PAGE_VIOLATION | 0x80000001 |
| EXCEPTION_INVALID_HANDLE | STATUS_INVALID_HANDLE | 0xC0000008 |
| EXCEPTION_POSSIBLE_DEADLOCK | STATUS_POSSIBLE_DEADLOCK | 0xC0000194 |
| CONTROL_C_EXIT | STATUS_CONTROL_C_EXIT | 0xC000013A |

32位错误代码的具体含义，如下图所示。

| | Facility code | Error code |
|---|---|---|
| S U | | |

S是最高的两位（第30、31位），为基本的状态代码，一共有4种组合，分别为11、10以及00。它们分别的意义是：11代表错误，10代表警告，01代表信息，00代表成功。

U是第29位（第29位），它只有0和1两种状态，代表该异常是否属于用户侧异常。

上面我们得到的一个返回值是0xE1223344。最高的是0xE (1110)。这个比特位代表：①它是属于用户异常；②这是一个错误信息。实务上地讲，本例程序与这个最高值没有关系；而是考虑的异常处理程序应当充分利用错误代码的所有信息。

接着，程序试图读取地址为0的内存。这个地址实际上是NULL指针；访问这个地址会导致系统崩溃，因为根据ISO 标准这个地址不应当存放任何数据（硬件规定）。此操作后，系统会优先调度自己注册的异常处理程序，后者会判断错误代码为EXCEPTION_ACCESS_VIOLATION，从而知道该异常是自己可以处理的问题。

读取地址为0的指令如下：

```
xor      eax, eax
mov      eax, DWORD PTR [eax] ; exception will occur here
push     push
push     OFFSET msg
call     printf
add      esp, 8
```

我们的程序不是可以实时恢复这个程序以便程序继续执行吗？答案是肯定的。我们的异常处理程序能够修复EAX寄存器的值，让操作系统继续执行下去。这就是自定义异常处理程序的功能。字符串printf的值是12345，因为了我们的异常处理函数值是0，EAX的值不再是0，而是全局变量new_value的值。因此程序运行找回了恢复。

以下是程序恢复的步骤：首先在内部寄存器中使用CPU抛出的错误信息，接着CPU将此异常挂起，并在Windows的内核中查找异常处理程序的路径。然后依次使用SEH的handler。

本例是用MSVC 2010 编译的。当然，我们不能保证其他的编程程序同样使用EAX寄存器导致崩溃。

我们所采用的地址转换技巧是精妙的。很少使用这种技术使用SEH的内部结构。不过，我不使用这种技术时引发异常崩溃。

为什么SEH相关的记录存储在这里，而不是其他地方？据说，如此这样操作系统就不需要关心这些数据的释放，毕竟函数返回以后这些数据都会自动释放。但是，笔者不能100%保证这种做法的正确性。这一点在第5.2节4节提到的alloca()函数。

## 68. 3.2 我们重新初始化MSVC

据说，C++语言环境已经能够稳定的处理各种异常，只有C语言的开发者才需要注册代码的异常处理机制。因此我们推出了一个面向MSVC的非标准3C扩展。这个扩展。
