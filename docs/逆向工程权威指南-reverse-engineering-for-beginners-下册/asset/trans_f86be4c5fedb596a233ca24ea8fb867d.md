

```assembly
mov      si, [bp+arg_0]
mov      bx, [bp+arg_4]

loc_3A: ; CODE XREF: string_compare_far+35j
mov      es, [bp+arg_6]
mov      al, [es]
mov      es, [bp+arg_2]
cmp      al, es:[si]
jz       short loc_4C
xor      ax, ax
jmp       short loc_67
```

```assembly
loc_4C: ; CODE XREF: string_compare_far+16j
mov      es, [bp+arg_6]
cmp      byte ptr:[bx], 0
jz       short loc_5E
mov      es, [bp+arg_2]
cmp      byte ptr:[es:[si], 0
jz       short loc_63
```

```assembly
loc_5E: ; CODE XREF: string_compare_far+23j
mov      ax, 1
jmp       short loc_67
```

```assembly
loc_63: ; CODE XREF: string_compare_far+2Cj
inc      bx
inc      si
jmp       short loc_3A
```

```assembly
loc_67: ; CODE XREF: string_compare_far+1Aj
        ; string_compare_far+31j
pop      si
pop      bp
retn     8 endp
string_compare_far end
```

```assembly
remove_digits proc near ; CODE XREF: WinMain+1Fp

arg_0 = word ptr 4

push     bp
mov      bp, sp
mov      bx, [bp+arg_0]

loc_72: ; CODE XREF: remove_digits+18j
mov     al, [bx]
test    al, al
jz      short loc_86
cmp     al, 30h ; '0'
jb      short loc_83
cmp     al, 39h ; '9'
ja      short loc_83
mov     byte ptr [bx], 2Dh ; '-'
```

```assembly
loc_83: ; CODE XREF:remove_digits+Ej
        ; remove_digits+12j
inc     bx
jmp     short loc_72
```

```assembly
loc_86: ; CODE XREF:remove_digits+Aj
        pop    bp
retn   2
remove_digits  endp
```

```assembly
WinMain proc near ; CODE XREF:start+EDp
push   bp
mov     bp, sp
mov     ax, offset aAsd ; "asd"
push   ax
mov     ax, offset aDef ; "def"
push   ax
call   string_compare
push   ds
mov     ax, offset aAsd ; "asd"
push   ax
push   ds
mov     ax, offset aDef ; "def"
push   ax
call   string_compare_far
mov     ax, offset aHello1234World ; "hello 1234 world"
push   ax
call   remove_digits
xor    ax, ax
push   ax
push   ds
mov     ax, offset aHello1234World ; "hello 1234 world"
push   ax
push   ds
mov     ax, offset aCaption ; "caption"
push   ax
mov     ax, 3 ; MB_YESNOCANCEL
push   ax
call MESSAGEBOX
xor ax, ax
pop bp
retn 0Ah
WinMain endp
```

这个程序使用了“near”和“far”两种类型的指针。每个指针针对适配16位8086C的一种特定的指针寻址模式。这方面的详细内容，请参见本文书第94章的详细介绍。

“near”指针的寻址空间是不限于数据段（DS）内的所有地址。字符串比较函数 `string_compare()` 读取两个指针，把DS寄存器的值用作寻址的基（段）地址，对这两个指针进行寻址。在此处的`mov al, [bx]`等指令等效于，只是没有明确指出它使用的DS寄存器。

“far”指针的寻址空间不限于当前数据段，它可以是其他段的内存地址。由于需要指定基（段）地址，由于两个16位地址才能形成一个型指针。本例的 `string_compare_far()`函数从对16位数据里取两个内存地址。把基地址存入寄存器ES，然后在执行指针时通过基地址寻址（mov al, es:[bx]`）。本章的例2，16位程序的 `MessageBox()`函数（属于系统函数）使用的是far指针。的确，当Windows在内核访问文本字符串时使用的是far指针，当它在内层访问文本字符串的时候需要指明指针的段地址。

near指针的寻址范围是64k，这可是16位数据的长度。对于小型程序来说，这种指针就足够了、不必在每次寻址的时候都要传递指针的段地址。大的程序通常占据多个64k的数据段，就需要每次寻址的时候都指明的数据段（段地址）。

代码段没有寻址意义上的差别。一个64k内存内可以包含所有的小型程序，可以使用 `CALL NEAR`指令调用其他函数；其被调用的函数可以用 `RETN`返回回调函数。但是，大型程序占据多个代码段，它就需要使用 `CALL FAR`指令，用对16位操作跳转的目的地址；其调用的函数必须使用 `RETF`返回函数。这就是编译器“内存模型（memory model）”选项的实际意义。

面向-DOS和Win16编译器为各种内存模型准备了相应的库。这些库代码指针和数据指针存在区别。

## 3.6 示例

```c
#include <windows.h>
#include <time.h>
#include <stdio.h>

char strbuf[256];

int PASCAL WinMain( HINSTANCE hInstance,
                    HINSTANCE hPrevInstance,
                    LPSTR lpCmdLine,
                    int nCmdShow )
{
    struct tm *t;
    time_t unix_time;

    unix_time=localtime(&unix_time);

    sprintf(strbuf, "%04d-%02d-%02d %02d:%02d:%02d",
             t->tm_year+1900, t->tm_mon, t->tm_day,
             t->tm_hour, t->tm_min, t->tm_sec);

    MessageBox(NULL, strbuf, "caption", MB_OK);
    return 0;
}
```

```assembly
WinMain proc near
var_4= word ptr -4
var_2= word ptr -2

push bp
mov bp, sp
push ax
xor ax, ax

call time
mov unix_time_low, ax
mov unix_time_high, dx
mov ax, offset unix_time_low
call localtime
mov bx, ax
mov t, ax                      ; will not used in future...

push word ptr [bx]      ; seconds
push word ptr [bx+2]      ; minutes
push word ptr [bx+4]      ; hour
push word ptr [bx+6]      ; day
push word ptr [bx+8]      ; month
mov ax, [bx+0Ah]         ; year
add ax, 1900
push ax
mov ax, offset a04d02d002d002  ; "%04d-%02d-%02d %02d:%02d:%02d"
push ax
mov ax, offset strbuf
push ax
call sprintf
add sp, 10h
xor ax, ax               ; NULL
push ax
ds
mov ax, offset strbuf
push ax
ds
mov ax, offset aCaption ; "caption"
push ax
xor ax, ax ; MB_OK
push ax
call MESSAGEBOX
mov ax, ax
mov sp, bp
ret 0Ah
```

在调用`time()`函数和`localtime()`函数的时候，编译器使用的是Watcom约定：通过AX、DX传递，其前4个参数通过AX、DX传递。遵循这种调用约定的库，其函数名称（汇编层面）尾部有划线。不过，`sprintf()`函数遵循的调用约定既不是ASC也不是Watcom，所以编译器使用常规规范（cdecl）（参考6.1节）。

## 全局变量

我们刚才的例子修改后，使用全局变量实现它的功能：

```c
#include <windows.h>
#include <time.h>
#include <stdio.h>

char strbuf[256];
struct tm *tm;
time_t unix_time;

int PASCAL WinMain( INSTANCE hInstance,
                   INSTANCE hPrevInstance,
                   LPSTR lpCmdLine,
                   int nCmdShow )
{
    unix_time=time(NULL);

    t=localtime(&unix_time);

    sprintf(strbuf, "%04d-%02d-%02d %02d:%02d:%02d",
             t->tm_year+1900, t->tm_mon, t->tm_day,
             t->tm_hour, t->tm_min, t->tm_sec);

    MessageBox(NULL, strbuf, "caption", MB_OK);
    return 0;
}
```

```assembly
unix_time_low dw 0
unix_time_high dw 0
t

WinMain proc near
push bp
mov bp, sp
xor ax, ax

call time
mov unix_time_low, ax
mov unix_time_high, dx
mov ax, offset unix_time_low
call localtime
mov bx, ax
mov t, ax                      ; will be used in future...

push word ptr [bx]      ; seconds
push word ptr [bx+2]      ; minutes
push word ptr [bx+4]      ; hour
push word ptr [bx+6]      ; day
push word ptr [bx+8]      ; month
mov ax, [bx+0Ah]         ; year
add ax, 1900
push ax
mov ax, offset a04d02d002d002  ; "%04d-%02d-%02d %02d:%02d:%02d"
push ax
mov ax, offset strbuf
push ax
call sprintf
add sp, 10h
xor ax, ax               ; NULL
push ax
ds
mov ax, offset strbuf
push ax
ds
mov ax, offset aCaption ; "caption"
push ax
xor ax, ax ; MB_OK
push ax
call MESSAGEBOX
mov ax, ax
mov sp, bp
ret 0Ah
```

编译器保留了汇编默认值，但是这个值实际上并没有被后续调用。由于编译器无法判断其他模块（文件）是否访问这个值。

## 第四部分 Java

![](img/a13a81a05f5574b940.png)

## 54章 Java

