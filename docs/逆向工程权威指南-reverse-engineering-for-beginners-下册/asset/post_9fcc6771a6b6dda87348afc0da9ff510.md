
# CPU - main thread, module ex

| | | | |
|---|---|---|---|
| 00210000 | 55 | PUSH EBP | EBP 001938D3 |
| 00210001 | 89 E5 | MOV EBP, ESP | EAX 00000001 |
| 00210004 | 8B 45 D0 | MOV EAX, PTR [EBP-40] | [Arg_2] |
| 00210008 | 89 45 C0 | MOV [EBP-40], EAX | EAX 00000001 |
| 0021000C | 6A 10 | PUSH 10 | EBP 7FFE12C0 |
| 0021000E | 53 | PUSH ESI | ESP 7FFE12C8 |
| 0021000F | 65 | PUSH EDI | ESP 7FFE12D0 |
| 00210011 | 89 C3 | MOV EBX, ESP | EDI 00FFFFFFFF |
| 00210013 | 8B 45 F8 | MOV EAX, PTR [EBP-8] | EAX 0000FFFF |
| 00210017 | 89 45 F0 | MOV [EBP-8], EAX | EAX 00000001 |
| 0021001B | 83 EC 08 | SUB ESP, 08 | EDI 00000000 |
| 0021001F | 59 | PUSH ECX | EIP 7FFE12C0 |
| 00210020 | 5A | PUSH EDX | EBP 7FFE12C8 |
| 00210022 | 89 C1 | MOV ECX, ECX | EAX 00000000 |
| 00210024 | 89 D2 | MOV EDX, EDX | EAX 00000001 |
| 00210026 | E8 FF FF FF | CALL 00210021 | EAX 0000FFFF |
| 0021002A | 5B | POP EBX | EAX 00000001 |
| 0021002B | 5D | POP EBP | EAX 00000000 |
| 0021002C | 5D | POP EDI | EIP 7FFE12C0 |
| 0021002D | C3 | RET | EBP 7FFE12C8 |

## 观察函数()

| Address | | | | | | |
|---|---|---|---|---|---|---|
| 00210040 | 44 | 00 | 00 | 02 | 00 | 00 | 00 |
| 00210044 | 00 | 00 | 00 | 00 | 00 | 00 | 00 |
| 00210048 | 00 | 00 | 00 | 00 | 00 | 00 | 00 |
| 0021004C | 00 | 00 | 00 | 00 | 00 | 00 | 00 |
| 00210050 | 00 | 00 | 00 | 00 | 00 | 00 | 00 |
| 00210054 | 00 | 00 | 00 | 00 | 00 | 00 | 00 |
| 00210058 | 00 | 00 | 00 | 00 | 00 | 00 | 00 |
| 0021005C | 00 | 00 | 00 | 00 | 00 | 00 | 00 |
| 00210060 | 00 | 00 | 00 | 00 | 00 | 00 | 00 |
| 00210064 | 00 | 00 | 00 | 00 | 00 | 00 | 00 |
| 00210068 | 00 | 00 | 00 | 00 | 00 | 00 | 00 |
| 0021006C | 00 | 00 | 00 | 00 | 00 | 00 | 00 |
| 00210070 | 00 | 00 | 00 | 00 | 00 | 00 | 00 |
| 00210074 | 00 | 00 | 00 | 00 | 00 | 00 | 00 |
| 00210078 | 00 | 00 | 00 | 00 | 00 | 00 | 00 |
| 0021007C | 00 | 00 | 00 | 00 | 00 | 00 | 00 |

观察函数()，IDA 能够识别外部的参数。它会对内存里的数据进行标注，添加如“RETURN from”之类的标注。故，被调用函数的参数并不在自己的帧，而是在调用者的帧里。

### 8.1.3 GCC

我们使用 GCC 4.4 编译上述程序，然后使用 IDA 查看它的汇编：

```assembly
public f
arg_0 = dword ptr 8
arg_4 = dword ptr 0Ch
arg_8 = dword ptr 10h

push ebp
mov ebp, esp
mov eax, [ebp+arg_0] ; 1st argument
imul eax, [ebp+arg_4] ; 2nd argument
add eax, [ebp+arg_8] ; 3rd argument
pop ebp
ret
```

```assembly
public main
arg_10 = dword ptr -10h
var_C = dword ptr -0Ch
var_8 = dword ptr -8

push ebp
mov ebp, esp
and esp, 0xFF0h
sub esp, 10h
mov [ebp+var_8], 3 ; 3rd argument
mov [ebp+var_C], 2 ; 2nd argument
mov [ebp+arg_10], 1 ; 1st argument
call f
mov edx, offset "%d\n"
mov [ebp+var_C], eax
mov [ebp+arg_10], edx
call printf
mov eax, 0
leave
ret
```

GCC的编译结果和MSVC十分相似。不同的是调用函数(printf)没有还原指针。这是由于函数尾部的数第二条指令——LEAVE（参见附录 A.6）。

### 8.2 x64

x86-64系统的参数传递不同。x86-64系统使用寄存器传递（前6参数）。就这个程序而言，被调用函数完全不需要访问。

### 8.2.1 MSVC

启用优化选项后，MSVC编译的结果如下：

```assembly
main
  sub rsp, 40
  mov edx, 2
  lea r8, QWORD PTR [rdx+1] ; R8=3
  lea ecx, QWORD PTR [rdx-1] ; ECX=1
  call f
  lea rcx, offset "%d" ; shadow space
  mov edx, eax
  call printf
  xor eax, eax
  add rsp, 40
  ret
```

```assembly
f
  ; ECX - 1st argument
  ; EDX - 2nd argument
  ; R8 - 3rd argument
  imul ecx, edx
  lea eax, DWORD PTR [r8+rcx]
  ret
```

看到，f()通过寄存器获取了全部参数。此处的加法运算是通过LEA指令实现的。明显，编译器认为LEA指令的效率比ADD指令高，所以它分配了LEA指令。f函数的第一个和第三个参数，main()函数使用了LEA指令。

### 8.2.2 GCC

在启用优化选项后，GCC生成的代码更为内联：

```assembly
f:
  ; EDI - 1st argument
  ; ESI - 2nd argument
  ; EDX - 3rd argument
  imul esi, edi
  lea eax, [rdx+rsi]
  ret

main:
  sub rsp, 28h
  mov r8d, 3 ; 3rd argument
  mov edx, 2 ; 2nd argument
  mov ecx, 1 ; 1st argument
  mov f
  call f
  mov edx, eax
  lea rcx, "%d\n"
  call printf
  return 0
  xor eax, eax
  add rsp, 28
  ret
```

### 8.6 Optimizing GCC 4.4.6 x64

```assembly
f:
  ; EDI - 1st argument
  ; ESI - 2nd argument
  ; EDX - 3rd argument
  imul esi, edi
  lea eax, [rdx+rsi]
  ret

main:
  sub rsp, 28h
  mov r8d, 3 ; 3rd argument
  mov edx, 2 ; 2nd argument
  mov ecx, 1 ; 1st argument
  mov f
  call f
  mov edx, eax
  lea rcx, "%d\n"
  call printf
  return 0
  xor eax, eax
  add rsp, 28
  ret
```

### 8.5 MSVC 2012 x64

```assembly
f
proc
  ; shadow space:
  arg_0 = dword ptr 8
  arg_8 = dword ptr 10h
  arg_10 = dword ptr 18h

  ; ECX - 1st argument
  ; EDX - 2nd argument
  ; RDX - 3rd argument
  mov [rsp+arg_10], r8d, edx
  mov [rsp+arg_8], edx
  mov [rsp+arg_0], ecx
  mov eax, [rsp+arg_0]
  imul eax, [rsp+arg_8]
  add eax, [rsp+arg_10]
  ret
endp

main
  sub rsp, 28h
  mov r8d, 3 ; 3rd argument
  mov edx, 2 ; 2nd argument
  mov ecx, 1 ; 1st argument
  mov f
  call f
  mov edx, eax
  lea rcx, "%d\n"
  call printf
  return 0
  xor eax, eax
  add rsp, 28
  ret
```

比较的是原本原本寄存器的3个参数都被推到了堆里。这种现象叫做“阴影空间/shadow space”[1]。每个Win64程序可以（但非必须）把4个寄存器的值存到阴影空间里。使用阴影空间有两个优点：1）通过传递参数，避免寄存器消耗（可能会占用4个寄存器）；2）便于调试器debugger在程序中断时找到寄存器参数（请参见：https://mdn.microsoft.com/en-us/library/ew572(vs=VS.90.29.aspx)。

大型函数可能会存在参数阴影空间，但是小型函数（如例）可能就不会使用阴影空间。在用阴影空间时，由调用的函数分配空间，被调用函数根据需要将寄存器参数存储到它的阴影空间中。
