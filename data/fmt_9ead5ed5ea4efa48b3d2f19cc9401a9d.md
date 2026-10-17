
0x00000000004106cc <364>: `mov %r9,8(%rax)`

0x00000000004106d4 <372>: `movl %rdx,rd8`

0x00000000004106d7 <375>: `mov %rsi,rax`

0x00000000004106c7 <376>: `shl $0x4,r14`

0x00000000004106cc <381>: `xor %edx,edx`

0x00000000004106d1 <386>: `mov %r8,%rax`

0x00000000004106d6 <391>: `add $0x10,rax`

0x00000000004106db <396>: `mov %rax,rsp`

0x00000000004106e0 <401>: `sub $0x4(%rsp),rbx`

0x00000000004106e5 <406>: `and 0xffffffffffffffff,rbx`

```
10. 检查被释放的地址：

```bash
(gdb) bt

#0 0x000000000040cc6b in raise () at pthread_create.c:688
#1 0x0000000000401241 in abort () at pthread_create.c:688
#2 0x0000000000401828 in lib_message ()
#3 0x00000000004015f4 in malloc_printerr ()
#4 0x000000000040179f in __int_free ()
#5 0x0000000000401c50 in proc () at pthread_create.c:688
#6 0x00000000004001c6 in bar_two () at pthread_create.c:688
#7 0x00000000004001c7 in foo_two () at pthread_create.c:688
#8 0x0000000000400d10 in thread_thread () at pthread_create.c:688
#9 0x00000000004031c3 in start_thread (arg=optimized out) at pthread_create.c:486
#10 0x00000000004034f6 in clone ()
```

```bash
(gdb) frame

#5 0x0000000000401c50 in proc () at pthread_create.c:688

688     pthread_create.c: no such file or directory.
```

反汇编 `proc` 函数 `proc`：

```assembly
Dump of assembler code <+8>

0x0000000000401bad <+0>  push   %rbp
0x0000000000401bae <+1>  mov    %rbp,%rbp
0x0000000000401bb1 <+4>  sub    $0x10,%rsp
0x0000000000401bb8 <+8>  callq  0x4d8d0<rand>
0x0000000000401bca <+13> mov    %eax,%ecx
0x0000000000401bc5 <+15> mov    $0x68dbad,$badx
0x0000000000401bc9 <+18> mov    %ecx,%eax
0x0000000000401bc2 <+21> imul   %edx,eax
0x0000000000401bc5 <+24> sar    $0xc,%edx
0x0000000000401bc8 <+27> mov    %ecx,%eax
0x0000000000401bc9 <+29> mov    $0x1f,%eax
0x0000000000401bd2 <+32> sub    %eax,%edx
0x0000000000401bd5 <+35> mov    %edx,%eax
0x0000000000401bd1 <+36> mov    -0x4(%rsp),%rax
0x0000000000401bd4 <+39> mov    $0x2710,eax,%ecx
0x0000000000401bd7 <+42> sub    %eax,%edx
0x0000000000401bd4 <+45> mov    %ecx,%eax
0x0000000000401be1 <+48> mov    -0x4(%rsp),%rax
0x0000000000401be4 <+51> callq  0x4d8d0<rand>
0x0000000000401be7 <+54> mov    %eax,%ecx
0x0000000000401be6 <+60> mov    $0x68dbad,$badx
0x0000000000401bf0 <+63> mov    %ecx,%eax
0x0000000000401bf2 <+69> imul   %edx,eax
0x0000000000401bf4 <+71> sar    $0xc,%edx
0x0000000000401bf7 <+74> mov    %ecx,%eax
0x000000000040fc <+76> sar    $0x1f,%eax
0x000000000040ff <+79> sub    %eax,%edx
0x0000000000401f8 <+81> mov    %edx,%eax
0x0000000000401c0 <+83> mov    -0x4(%rsp),%rax
0x0000000000401c3 <+86> mov    $0x2710,eax
0x0000000000401c6 <+89> imul   %edx,eax
0x0000000000401c9 <+92> mov    %ecx,%eax
0x0000000000401c8 <+97> mov    -0x4(%rsp),%rax
0x000000000040c10 <+99> mov    -0x4(%rsp),%rax
0x000000000040c13 <+102> mov    -0x4(%rsp),%rax
0x000000000040c16 <+105> test   %rax,%rax
0x000000000040c18 <+107> lea    0x(%rax),rdx
0x000000000040c20 <+115> lea    0xc019(%rip),%rax
0x000000000040c27 <+121> mov    (%rax),rax
0x000000000040c2b <+126> test   %rax,%rax
0x000000000040c2e <+129> je      0x401c6<proc+191>
0x000000000040c30 <+131> mov    -4(%rbp),esp
0x000000000040c33 <+134> test   %rax,%rax
0x000000000040c36 <+136> leaq    0x(%rax,8),rdx
0x000000000040c3d <+139> lea     0x8(%rbp),rcx
0x000000000040c41 <+144> mov    (%rax),rax
0x000000000040c48 <+151> mov    %rax,rdx
0x000000000040c4b <+158> callq   0x41a1c0<free>
0x000000000040c4e <+156> mov    -4(%rbp),esp
0x000000000040c51 <+159> test   %rax,%rax
0x000000000040c54 <+162> lea     0x(%rax,8),rdx
0x000000000040c57 <+165> lea     0x8(%rbp),rcx
0x000000000040c5c <+174> mov    %0x,%rax,1
0x000000000040c64 <+183> movq    %rax,0(%rsp)
0x000000000040c6c <+191> test   %rax,%rax
0x000000000040c71 <+196> mov    %rax,rdx
0x000000000040c74 <+199> callq   0x41a5d0<malloc>
0x000000000040c79 <+204> mov    %rax,rcx
0x000000000040c7c <+207> mov    -4(%rbp),esp
0x000000000040c81 <+212> test   %rax,%rax
0x000000000040c84 <+215> lea     0x(%rax,8),rdx
0x000000000040c89 <+220> lea     0x8(%rbp),rcx
0x000000000040c92 <+227> mov    %rcx,%rax,1
0x000000000040c97 <+231> jmp    0x408bb5<proc+8>
End of assembler.
```

```bash
(gdb) x 0x42c40

0x42c40: allocBuf

(gdb) x 0x42c40

0x42c40: 0x7fdbd6

(gdb) x 0x42c40+8

0x42c48: 0x0
```

缩放索引 `(%rax,1)` 表明我们有一个数组。前 1000 个 `allocBuf (0x42c40)` 有两种查找方式：

```bash
(gdb) print *0x42c40

$1 = {0x7ffc8062b10, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x7ffc809fac, 0x0, 0x0, 0x0

0x7ffd00a3f0, 0x0, 0x0, 0x0, 0x7ffc413eb00, 0x0, 0x0

0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0

0x7ffd0a81a10, 0x0, 0x0, 0x7ffc78dabe00, 0x0 repeats 11 times,

0x7ffd0075d70, 0x0 repeats 31 times, 0x7ffc700b840, 0x0, 0x7ffc704d3f80, 0x0, 0x0,

0x7ffc704d1b0, 0x0, 0x0, 0x0, 0x7ffc813e10, 0x0, 0x7ffc41c6b0, 0x7ffc42e100, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x7ffc4f6e60, 0x0,

0x7ffc80259c0, 0x0, 0x7ffc70343f0, 0x0 repeats 24 times, 0x7ffc80c2760, 0x0, 0x0, 0x0, 0x0, 0x0, 0x7ffc80b2f40, 0x0, 0x0, 0x0, 0x0 repeats 13 times, 0x7ffc7020ef0, 0x0, 0x7ffc7813fd0, 0x0, 0x7ffc70df7f0, 0x0, 0x7ffc8102800, 0x0, 0x0, 0x0, 0x7ffc8008660, 0x0 repeats 18 times, 0x7ffc40c4a40, 0x0 repeats 36 times, 0x7ffc4859c40, 0x0 repeats 15 times, 0x7ffc8056260, 0x0, 0x0, 0x0, 0x0, 0x7ffc703a7f0, 0x0, 0x7ffc7040c3d0, 0x0 repeats 14 times}

(gdb) print *(long *)0x7ffc254d800

$1 = 0x7ffc8062b10, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x7ffc809fac, 0x0, 0x0, 0x0

0x7ffd00a3f0, 0x0, 0x0, 0x0, 0x7ffc413eb00, 0x0, 0x0

0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0

0x7ffd0a81a10, 0x0, 0x0, 0x7ffc78dabe00, 0x0 repeats 11 times,

0x7ffd0075d70, 0x0 repeats 31 times, 0x7ffc700b840, 0x0, 0x7ffc704d3f80, 0x0, 0x0,

0x7ffc704d1b0, 0x0, 0x0, 0x0, 0x7ffc813e10, 0x0, 0x7ffc41c6b0, 0x7ffc42e100, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x0, 0x7ffc4f6e60, 0x0,

0x7ffc80259c0, 0x0, 0x7ffc70343f0, 0x0 repeats 24 times, 0x7ffc80c2760, 0x0, 0x0, 0x0, 0x0, 0x0, 0x7ffc80b2f40, 0x0, 0x0, 0x0, 0x0 repeats 13 times, 0x7ffc7020ef0, 0x0, 0x7ffc7813fd0, 0x0, 0x7ffc70df7f0, 0x0, 0x7ffc810280, 0x0, 0x0, 0x0, 0x7ffc8008660, 0x0 repeats 18 times, 0x7ffc40c4a40, 0x0 repeats 36 times, 0x7ffc4859c40, 0x0 repeats 15 times, 0x7ffc8056260, 0x0, 0x0, 0x0, 0x0, 0x7ffc703a7f0, 0x0, 0x7ffc7040c3d0, 0x0 repeats 14 times}
```

### 练习 A10 (A64, GDB)

**目标：** 学习如何识别内容等待、同步问题、高级反汇编以及数组 dump。

**模式：** 双重释放（进程堆）；高竞争（进程堆）；等待链（通用）；关键区域；自诊断（用户模式）。

- 从 `A64/App10` 目录加载 `core.10881` dump 文件和 `App10` 可执行文件：

```
~/AL26/A64/App10 -c core.10881 -se App10

gnu gdb (Debian 8.2-1+deb3) 8.2.1

Copyright (2018) Free Software Foundation, Inc.

License GPLv3: GNU GPL 3 or later <http://www.gnu.org/licenses/gpl.html>

This is free software: you are free to change and redistribute it.

There is NO WARRANTY, unless permitted by law.

Type "show configuration" and "show warranty" for details.

This GDB was configured as "x86_64-linux-gnu".

Type "show configuration" for configuration details.

For bug reporting instructions, please see:

<http://www.gnu.org/software/gdb/bugs//

Find the GDB manual and other documentation resources at:

<http://www.gnu.org/software/gdb/documentation/>
```

获取帮助，输入 `help`。
输入 `apropos word` 搜索与 `word` 相关的命令。
从 `App10` 读取符号...（未找到调试符号)...

```
[New LWP 10882]
[New LWP 10881]
[New LWP 10886]
[New LWP 10884]
[New LWP 10885]
[New LWP 10883]
```

```
Core was generated by './App10'.

**Program terminated with SIGSEGV, Segmentation fault.**

#0 0x0000000000419a3c in __int_free ()

[Current thread is 1 (LWP 10882)]
```

- 在案例文件中记录日志以识别命令的输出：

```
(gdb) set logging on App10.log.
Copying output to App10.log.
```
