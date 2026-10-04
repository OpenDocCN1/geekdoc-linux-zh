而在Windows NT环境下，系统调用调度表位于系统服务分配表
SSDT (System Service Dispatch Table)。

计算机病毒以及shell大多数都会利用系统调用。这是因为系统库函数的地址过程非常麻烦，而直接调用系统调用却相对简单。虽然系统调用的访问过程并不麻烦，但是由于系统本身属于底层API，因此直接使用系统调用的程序并不好。另外需要注意的是：系统调用的总数由操作系统和系统版本两个因素共同决定的。

# 66.1 Linux

Linux程序通常通过80号中断/INT 80调用系统调用。在调用系统调用时，程序应当通过EAX寄存器指定调用函数的编号，再使用其他寄存器声明系统调用的参数。

指令使用系统调用66.1 syscall的简单单例

```
section .text
global _start:
_start:
mov    edx,len ; buffer len
mov    ecx,msg ; buffer
mov    ebx,1 ; file descriptor. 1 is stdout
mov    eax,4 ; syscall number. 4 is for sys_write
int    0x80

mov    eax,1 ; syscall number. 4 is for sys_exit
int    0x80
```

```
section .data
msg    db 'Hello, world!',0xa
len    equ $ - msg
```

编译指令如下所示。

```
nasm -f elf32 l.s
ld l.o
```

完整的Linux系统调用列表可以参考：
http://go.yiche.com/17319