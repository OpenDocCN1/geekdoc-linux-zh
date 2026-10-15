
`MSVCR80.DLL` 中的 `comp` 参数是传递给 `qsort()` 函数的第四个参数。在 `qsort()` 的过程中，系统会将控制权传递给 `comp` 参数指向的函数指针地址。在使用它之前，`comp` 函数所需的两个参数已经传递到这里。在执行它之后，排序已经完成了。

可见，函数指针十分危险。首先传递给 `qsort()` 的函数指针如果错误，那么 `qsort()` 函数也会把控制权传递给错误的指针地址，此时程序将会崩溃，而且指针错误很难发现问题所在。

其次，`callback` 函数必须严格遵守命名规范。无论是函数名不当、参数还是数据类型不当，都会引发严重的问题。相比之下，关键问题并不是程序是否会崩溃，而是程序崩溃的手段是什么。在编译器处理函数指针的时候，它不会对问题进行任何提示。

### 23.1.1 MSVC+OlDlg

我们使用 OlDlg 加载这个程序，并在首次调用 `comp` 函数的地址设置起点。

图 23.1 所示为程序首次调用 `comp` 函数的情况。OlDlg 在代码窗口显示了被比较的两个值，此时指针指向 RA，即 `qsort` 函数的地址（实际上是 `MSCR100 DLL` 内部的）。

![](img/a13a81a53f805f55074b2e5d2ec754b6_594_0.png)

图 23.1 OlDlg 第一次调用 `comp` 函数

在程序运行 `RETN` 指令之前，我们一直等待 F8 键，等待进入 `qsort()` 函数，如图 23.2 所示。

![](img/a13a81a53f805f55074b2e5d2ec754b6_995_0.png)

程序将再次调用比较函数。

![](img/a13a81a53f805f55074b2e5d2ec754b6_595_1.png)

#### CPU - main thread, it17_1

```
| | | | | Registers (FPU) |
|---|---|---|---|---||
| 000110D0 | 84424 08 | MOV EAX,DWORD PTR:[ESP] | | | EAX 00000000 |
| 000110D4 | 84424 08 | MOV ECX,DWORD PTR:[ESP] | | | ECX FFFE2560 |
| 000110D8 | 8000 | MOV EDX,DWORD PTR:[ESP] | | | EDX 00000000 |
| 000110BC | 8000 | MOV EBX,DWORD PTR:[ESP] | | | EBX 00007F6C |
| 000110C0 | 59 C7 | POP EBX | | | ESP 000073B8 |
| 000110C4 | 75 03 | JNE 000110CB | | | ES 00007F69 |
| 000110C8 | 33 20 | XOR EAX,EAX | | | EDI 00007F63 |
| 000110CC | 33 C2 | XOR EDX,EDX | | | |
| 000110D0 | 8B 45 01 88 | CMP EAX,EBX | | | |
| 000110D4 | 7F C2 | JGE label | | | |
| 000110D8 | 44 FF 01 | MOV EDI,[EAX+EDX] | | | |
| 000110DC | C7 | RET | | | |
| 000110E0 | 83 EC 20 | SUB ESP,20 | | | |
| 000110E4 | 8B 19 A8 FF 00 | MOV EBX,DWORD PTR:[ESP] | | | |
| | | | | | Address | Hex dump | (ASCII) |
| |---|---|---|---|---|---|---|
| 00401000 | 48 65 6C 6C 0F 20 77 6F 64 20 21 20 | Hello World! | | | | | |
| 00401010 | 54 68 65 79 20 74 65 74 20 20 69 73 | This test of | | | | | |
| 00401020 | 66 61 73 74 20 00 00 00 00 00 00 | fast | | | | | |
| 00401030 | 63 6D 70 20 24 00 00 00 00 00 00 | comp | | | | | |
| 00401040 | 00 00 00 00 00 00 00 00 00 00 00 | | | | | | |
| 00401050 | 00 00 00 00 00 00 00 00 00 00 00 | | | | | | |
| 00401060 | 00 00 00 00 00 00 00 00 00 00 00 | | | | | | |
| 00401070 | 00 00 00 00 00 00 00 00 00 00 00 | | | | | | |
| 00401080 | 00 00 00 00 00 00 00 00 00 00 00 | | | | | | |
```

图 23.3 OlDlg 第二次调用 `comp()` 函数

### 23.1.2 MSVC+trace

程序将比较的10个数字分别是 1892, 45, 200, -988, 4087, 5, -12345, 1087, 88, -100000。

我们在 `comp()` 函数中找到第一个 `CMP` 指令，它的地址是 `0x0040100C`。我们在此处设置一个断点：

```
tracer.exe -l:it1_7.exe bpx=it1_7.exe:0x004010C
```

当程序执行到该断点时，各寄存器的情况如下：

```
PID=4336|New process 17_1.exe

(0) 17_1.exe:0x004010c

EAX=0x00000764 EBX=0x0051f7c8 ECX=0x00000005 EDX=0x00000000

ESI=0x0051f7d8 EDI=0x0051f7b4 EBP=0x0051f794 ESP=0x0051f6c7

EIP=0x00281c00

FLAGS=IF

(0) 17_1.exe0x401000

EAX=0x00000005 EBX=0x0051f7c8 ECX=0x0FE7960 EDX=0x00000000

ESI=0x0051f7d8 EDI=0x0051f7b4 EBP=0x0051f794 ESP=0x0051f6c7

EIP=0x00281c00

FLAGS=PF ZF

(0) 17_1.exe0x401000

EAX=0x00000764 EBX=0x0051f7c8 ECX=0x00000005 EDX=0x00000000

ESI=0x0051f7d8 EDI=0x0051f7b4 EBP=0x0051f794 ESP=0x0051f6c7

EIP=0x00281c00

FLAGS=IF
```

得到寄存器的值。

```assembly
xor eax, eax
cmp [ecx], edx
jnz short loc_8084858
pop ebp
retn
```

```assembly
loc_8084858:
setnl al
movzx eax, al
lea eax, [eax+eax-1]
pop ebp
retn
endp
```

`qsort()` 函数的计算过程封装在库文件 `libc.so.6` 里。因此，Linux 的 `qsort()` 只是 `qsort_r()` 的一个 wrapper。

此处会调用 `quicksort()`，后者通过函数指针调用我们写的 `comp()` 函数。

glibc 版本—2.10.1 中的 `libc.so` 文件中有下述指令。

#### 指令清单 23.4（file libc.so.6, glibc version—2.10.1）

```assembly
.text:0002DDF6 mov edx, [ebp+arg_10]
.text:0002DDF9 mov [esp+4], esi
.text:0002DDFD mov [esp], edi
.text:0002DE00 mov [esp+8], edx
.text:0002DE04 call [ebp+arg_c]
```
