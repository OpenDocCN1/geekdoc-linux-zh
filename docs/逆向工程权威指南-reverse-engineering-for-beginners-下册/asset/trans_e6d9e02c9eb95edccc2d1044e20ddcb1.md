

# CPU - 主线程，模块执行

```
001A0030 75 0E      JLE SHORT 001A042
001A0036 68 00D3A000  PUSH OFFSET 001A3000
001A003C FF 15 C8F3  CALL DWORD PTR [CR18F3.print]
001A0040 52 04      XOR EAX,EAX
001A0044 68 61D3A00  PUSH OFFSET 001A3061
001A004A 65 FF15  CALL DWORD PTR [CR18F5.print]
001A004E 75 0E      JLE SHORT 001A042
001A0054 68 00D3A000  PUSH OFFSET 001A3000
001A005A FF 15 C8F3  CALL DWORD PTR [CR18F3.print]
001A005E 52 04      XOR EAX,EAX
001A0062 68 61D3A00  PUSH OFFSET 001A3061
001A0068 65 FF15  CALL DWORD PTR [CR18F5.print]
001A006C C3 04      RET  
```

| 寄存器 (tt) | 值 |
| :--- | :--- |
| EAX | 00000001 |
| EDX | 00000000 |
| ECX | 00000000 |
| ESI | 0000007F |
| EDI | 0000007F |
| ESP | 001FF0000 |
| EBP | 00000000 |
| EIP | 001A0058 |

跳转未发生
上下文：001A0145

| 分段 | 值 |
| :--- | :--- |
| CS 23 2bit | 0FFFFFFF |
| SS 23 2bit | 0FFFFFFF |
| SS 23 2bit | 0FFFFFFF |
| SS 23 2bit | 0FFFFFFF |
| FS 23 2bit | 000000FF |
| SS 23 2bit | 000000FF |

内存地址转储

| 地址 | ASCII (ASCII) |
| :--- | :--- |
| 001A0130 | 00 00 00 00 00 00 00 00 61 32 3D 3D 00 00 00 |
| 001A0138 | 61 32 00 00 00 00 00 00 61 32 3D 3D 00 00 00 00 |
| 001A0140 | 61 32 00 00 00 00 00 00 61 32 3D 3D 00 00 00 00 |
| 001A0148 | FF FF FF FF 01 00 00 00 73 71 6D 20 74 65 72 7E |
| 001A0150 | FE FF FF FF 00 00 00 00 73 71 6D 20 74 65 72 7E |
| 001A0158 | 00 00 00 00 00 00 00 00 41 53 63 69 69 20 "6E 22" |
| 001A0160 | 00 00 00 00 00 00 00 00 41 53 63 69 69 20 "6E 22" |
| 001A0168 | 00 00 00 00 00 00 00 00 41 53 63 69 69 20 "6E 22" |
| 001A0170 | 00 00 00 00 00 00 00 00 41 53 63 69 69 20 "6E 22" |
| 001A0178 | 00 00 00 00 00 00 00 00 41 53 63 69 69 20 "6E 22" |
| 001A0180 | 00 00 00 00 00 00 00 00 41 53 63 69 69 20 "6E 22" |
| 001A0188 | 00 00 00 00 00 00 00 00 41 53 63 69 69 20 "6E 22" |

| 变量 | 值 |
| :--- | :--- |
| Arg1 | 1 |
| Arg2 | 2 |
| 来自 ax 的返回 | 0 |
| 来自 ax 的返回 | 0 |
| ASCII | "6E" |
| ASCII | "6E" |

![](img/a13a81a53f805f55074b2e5d2ec754b6_196.png)

我们可以使用 IDA 给可执行文件打补丁，强制函数满足 `a==b`，忽略它的参数，如图 2 所示。

# IDA_7_exe

C:\Polygon\ollydbg\7.exe

| 地址 | 指令 |
| :--- | :--- |
| .00040100 | 55 | push ebp |
| .00040101 | 88 EC | mov ebp,esp |
| .00040103 | 8A 45 08 | mov eax,[eb+8] |
| .00040106 | 34 55 00 | cmp eax,[eb+0C] |
| .00040109 | 75 E0 | jle .00040118 |
| .00040110 | E6 A4 00 00 | push .0004018F-B2 |
| .00040115 | 83 C4 04 | call .0004018F-B3 |
| .00040118 | 88 42 08 | add esp,4 |
| .0004011A | 38 D4 0C | mov eax,[eb+0C] |
| .0004012E | 75 00 | cmp eax,[eb+0C] |
| .0004012F | 6B 08 00 00 | jnz .000401D2 |
| .0004012A | E9 B5 00 00 | push 'a=b'-E5 |
| .00040130 | 83 C4 04 | call .0004018F-B3 |
| .00040136 | 38 55 0C | add esp,4 |
| .00040133 | 7D 00 | mov eax,[eb+0C] |
| .00040135 | 61 B8 00 00 | cmp eax,[eb+0C] |
| .0004013A | E8 00 00 | jge .00040110 |
| .0004013F | 83 C4 04 | push .0004018F-D7 |
| .00040142 | 50 | call esp,4 |
| .00040145 | CC | pop ebp |
| .00040145 | CC | int 3 |
| .00040146 | CC | int 3 |
| .00040147 | CC | int 3 |
| .00040148 | CC | int 3 |

| 类型 | 值 |
| :--- | :--- |
| Global | 2110B |
| Reload | 500 |
| String | 701 |
| rect | 5byte |
| Table | 10 |
| Naked | 12 |
| AddNam | |

![](img/a13a81a53f805f55074b2e5d2ec754b6_197.png)

本文将多次修改可执行程序，分别完成三个任务：
- 强制修改第一个跳转指令。
- 强制拦截第二个跳转指令。
- 强制触发第三个跳转指令。

故需要修改三条指令（三个字符）：

- 把第一个跳转改为jmp，并保留原始的偏移量（jump offset）。
- 第二个跳转指令的触发条件一定成立，无论条件是否都要跳转下一条指令。我们将我们将量设置为零。
- 第三个跳转指令的修改方法和第一个跳转相同。我们只需要将跳转替换为JMP（无跳转）即可。

修改之后的 `f_unsigned()` 函数图 12 所示。

![](img/a13a81a53f805f55074b2e5d2ec754b6_198.png)

修改之后的 `f_unsigned()` 函数，三个跳转指令全部修改。如果少修改一个，它可能会多次调用printf()函数，与我们的预期——只调用printf()的目标相同。

# Non-optimizing GCC

如果关闭了GCC的优化选项，那么编译出来的程序和MSVC编译出来的没什么区别，只不过把printf替换为了puts。

# Optimizing GCC

聪明的一定会问，既然比较的值相同，比较之后的标志位也是相同，还有必要对同样的参数进行多次比较？或者MSVC真的不能智能一些？但是启用优化选项后，GCC 4.8是否能够这种深度优化。

### GCC 4.8.1 f_signed

```
f_signed()
   mov eax, [esp+8]
   cmp [esp+4], eax
   jg  .L6
   je  .L7
   mov [esp+4], .LC2 ; "a<b"
   puts

.L6:
   mov [esp+4], .LC0 ; "a>b"
   puts

.L1:
   ret

.L7:
   mov [esp+4], .LC1 ; "a==b"
   puts
```

很明显，它使用jmp替代了肿胀的“CALL ...... RET”指令。本书在13.1节将详细解答这种技术。不得不说在x86系统中，这种程序比较容易。MSVC做不到GCC那种深度优化。另一方面，汇编语言的程序员学会跳转用的技巧。所以，如果你遇到了这种精简的程序，而且能够判断它是GCC编译出来的，那么基本上可以判断它是手写的汇编程序。即使开启了同样的选项，f_unsigned()对应的指令也没有精致。

### GCC 4.8.1 f_unsigned

```
f_unsigned:
   push esi
   push ebx
   sub esp, 20
   mov esi, [esp+32]
   mov ebx, [esp+36]
   cmp esi, ebx
   ja  .L13
   cmp esi, ebx          ; instruction may be removed
   je  .L14
.L10:
   jb .L15
   add esp, 20
   pop ebx
   pop esi
   ret
.L15:
   mov [esp+32], .LC2 ; "a<b"
   add esp, 20
   pop ebx
   pop esi
   ret
.L13:
   mov [esp+32], .LC0 ; "a>b"
   add esp, 20
   pop ebx
   pop esi
   ret
.L14:
   mov [esp+32], .LC1 ; "a==b"
   add esp, 20
   pop ebx
   pop esi
```

可见，ARM模式的程序完全不依赖条件跳转指令。

这样做有什么优点？精简指令集（RISC）ARM处理器采用流水技术（pipeline）。简单来说，这种技术使得ARM模式的程序完全不依赖条件跳转指令。

