在3.2节的那个例子里，程序在调用printf()函数之前前清空了EAX寄存器。本例中存在相同的操作。

# 指令清单6.4 Optimizing GCC 4.4.6 x64

```
.LCO
    .string "a=%d; b=%d; c=%d; d=%d; e=%d; f=%d; g=%d; h=%d\n"
main:
    sub    rsp, 40
    mov    r9d, 5
    mov    r8d, 4
    mov    ecx, 3
    mov    edx, 2
    mov    esi, 1
    mov    edi, OFFSET FLAT:.LCO
    xor    eax, eax; # number of vector registers passed
    mov    DWORD PTR [rsp+16], 8
    mov    DWORD PTR [rsp+8], 7
    mov    DWORD PTR [rsp], 6
    call   printf

    xor    eax, eax
    add    rsp, 40
    ret
```

# GCC + GDB

在使用GDB调试之前，我们首先要编译源代码：

```
$ gcc -g 2.c -o 2
$ gdb gdb
GNU gdb (GDB) 7.6.1-ubuntu
Copyright(C) 2013 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version3 or
later<http://gnu.org/licenses/gpl.html>
This is free software : you are free to change and redistribute it.
There is no WARRANTY, to the extent permitted by law. Type "show
copy"
and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>...
Reading symbols from /home/dennis/polygon/2...done.
```

接下来，我们在printf()运行之前设置断点，然后运行这个程序：