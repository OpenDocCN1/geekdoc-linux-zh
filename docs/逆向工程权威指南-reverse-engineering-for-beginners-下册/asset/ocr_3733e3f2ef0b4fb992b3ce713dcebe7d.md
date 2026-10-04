```
public main
proc near
    = dword ptr -54h
    = dword ptr -4

push ebp
mov ebp, esp
sub esp, 60h ; 96
mov [ebp+i], 0
jmp short loc_8043C3

loc_8043C3:
mov eax, [ebp+i]
mov edx, [ebp+i]
mov [ebp+eax*4+a], edx
add [ebp+i], 1

loc_8043D1:
cmp [ebp+i], 1Dh
jle short loc_8043C3
mov eax, 0
leave
retn
main
```

在Linux系统中执行这个程序引发错误/Segmentation fault。

我们使用GDB Debugger调试：

```
(gdb) r
Starting program: /home/dennis/RE/1
nProgram received signal SIGSEGV, Segmentation fault.
0x00000016 in ?? ()
(gdb) info registers
eax             0x0               0
cx             0xd2f96388      -755407992
edx             0x1d                29
ebx             0x26eff44b0      0xbfff4b0
sp             0x15                0x15
si             0x0               0
edi             0x0               0
elp             0x16                0x16
eflags         0x102002      [ RF ]
cs             0x73                115
ss             0x7b                123
ds             0x7b                123
fs             0x0                 0
```