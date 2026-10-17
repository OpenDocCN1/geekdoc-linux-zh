
# 死锁 (x64, GDB)

![](img/3944f3cabeeec58663646c309af01b5f_457_0.png)

```
(gdb) print *thread_mutex_t* mutexA
$2 = _data = {lock = 2, count = 0, __nusers = 1, __kind = 0, 
elision = 0, _list = {prev = 0, next = 0}, 
size = 0x0020000000000000000007000000010001, '\x00' (repeats 26 times),
align = 2)
```

```
(gdb) print *thread_mutex_t* mutexB
$3 = _data = {lock = 2, count = 0, __nusers = 1, __kind = 0, 
elision = 0, _list = {prev = 0, next = 0}, 
size = 0x00200000000000000000000007000000010001, '\x00' (repeats 26 times),
align = 2)
```

注意：我们看到了各自的线程所有者（LWP 号）。

```
(gdb) thread 5
Switching to thread 3 (Thread 0x7fa8cbff70 (LWP 598))
#0 __llock_wait at /sysdeps/native/sysv/linux/x86_64/lowlevel.s
```

```
(gdb) bt
#0 __llock_wait at /sysdeps/native/sysv/linux/x86_64/lowlevel.s:103
#1 0000000000007114 __pthread_mutex_lock(mutex=0x7fa0d34e0)
  80 in /nptr/pthread_lock.c
#2 000000000000710ec proc_a()
  88 in pthread_create.c
#3 000000000000718a bar_two()
  88 in pthread_create.c
#4 0000000000007196 foo_two()
  88 in pthread_create.c
#5 0000000000001faa thread_two(void*)
  88 in pthread_create.c
#6 0000000000001f73 start_thread(arg-optimized out)
  86 in pthread_create.c:486
#7 000000000040512f in clone()
```

```
(gdb) set print-demangle off
```

```
(gdb) disassembler code for function _ZProcAv:
Dump of 0x00000000004101ec
0x00000000004101b5 <0>:	push    %rbp
0x0000000000410be6 <4>:	mov     %rsp,%rbp
0x00000000004101c4 <8>:	lea     0x4152e0(%rip),%rdi    # 0x4d34a0 <thread_mutex_lock>
0x00000000004101c5 <12>:	callq   0x415fcf(%rip),%rdi    # 0x4d34a0 <mutexA>
0x00000000004102cd <16>:	lea     0x4160d0(%rip),%rdi    # <thread_mutex_unlock>
0x00000000004102d <28>:	mov     %x14,%rdi
0x00000000004102e <38>:	callq   0x4152c8<sleep>
0x00000000004102f <48>:	lea     0x4152d8(%rip),%rdi    # 0x4d34e <mutexB>
0x000000000041030 <50>:	callq   0x4152e8(%rip),%rdi    # <thread_mutex_lock>
0x00000000004101ec <55>:	lea     0x4152e8(%rip),%rdi    # 0x4d34e <mutexB>
0x00000000004101f4 <67>:	jmp     0x4001f9 <Z5ProcAv+84>
0x00000000004101ed <69>:	mov     %rax,%rdi
0x00000000004101f2 <77>:	callq   0x40202c<__xa_begin_catch>
0x00000000004101f7 <82>:	callq   0x402f30 <__xa_end_catch>
0x00000000004101f9 <84>:	jmp     0x4012d6 <Z5ProcAv+33>
0x0000000000410f0a <85>:	pop     %rbp
	retq
End of assembler dump.
```

# 练习 A11 (A64, GDB)

目标：学习识别同步等待链、死锁、隐藏异常和已处理异常。

模式：等待链（互斥锁对象）、死锁（互斥锁对象）。

- 1. 从 `A64/App11` 目录加载 `App11.11410` dump 文件和 `App11` 可执行文件：

```
~ALCDA2/A64/App11$ gdb-multilibarch -C App11.11410 -se App11
GNU gdb (Debian 8.2-1b) 8.2
Copyright (2018) Free Software Foundation, Inc.
License GPL3 or later <http://www.gnu.org/licenses/gpl.html>
这是自由软件，你可以自由运行并重新分发它，在法律允许的任何范围内。
此 GDB 配置为 "x86_64-linux-gnu"。
详情请执行 "show configuration"。
报告错误请参阅：http://www.gnu.org/software/gdb/
获取帮助请执行 "help"。
执行 "word"来搜索与"word"相关的命令。
正在从 App1 读取符号（无调试符号）...完成。
[New LWP 11411]
[New LWP 11412]
[New LWP 11421]
[New LWP 11422]
[New LWP 11423]
[New LWP 11410]
由 ./App11 生成转储
#0 0x000000000041ae24 in nanosleep
当前线程是 1 (LWP 11411)
```

- 2. 将输出记录到文件：

```
(gdb) set logging on
App11.log
```

- 3. 列出所有线程追踪并识别等待链和死锁：

```
(gdb) thread apply all bt
Thread 6 (LWP 11410):
#0 0x000000000041ae24 in nanosleep
#1 0x0000000000033b84 in sleep ()
#2 0x00000000000330f0 in bar_five ()
#3 0x00000000000330f4 in foo_five ()
#4 0x00000000004341c in thread_five(void*)
#5 0x000000000041a0a4 in thread_start ()
#6 0x0000000000438760 in thread_start ()

Thread 4 (LWP 11422):
#0 0x000000000041a110 in __lll_lock_wait ()
#1 0x000000000041ea4 in pthread_mutex_lock ()
#2 0x0000000000433a20 in procB ()
#3 0x0000000000433a38 in bar_four ()
#4 0x0000000000433bc in foo_four ()
#5 0x0000000000433d4 in thread_four(void(*))
#6 0x000000000041b84 in thread_start ()
#7 0x0000000000438760 in thread_start ()

Thread 3 (LWP 11421):
#0 0x000000000041ae24 in nanosleep
#1 0x0000000000433b84 in sleep ()
#2 0x0000000000433664 in bar_three ()
#3 0x0000000000433778 in foo_three ()
#4 0x0000000000433d90 in thread_three(void(*))
#5 0x000000000041b84 in thread_start ()
#6 0x0000000000438760 in thread_start ()

Thread 2 (LWP 11420):
#0 0x000000000041a110 in __lll_lock_wait ()
#1 0x000000000041ea4 in pthread_mutex_lock ()
#2 0x000000000043025c in procA ()
#3 0x0000000000433c1c in bar_two ()
#4 0x0000000000433d30 in foo_two ()
#5 0x0000000000433a48 in thread_two(void(*))
#6 0x000000000041b84 in thread_start ()
#7 0x0000000000438760 in thread_start ()

Thread 1 (LWP 11419):
#0 0x000000000041ae24 in nanosleep
#1 0x0000000000433b84 in sleep ()
#2 0x0000000000430d28 in bar_one ()
#3 0x0000000000430e2c in foo_one ()
#4 0x0000000000433b04 in thread_one(void(*))
#5 0x0000000000413a04 in thread_start ()
#6 0x0000000000438760 in thread_start ()
```

- 4. 检查线程 `#4` 及其等待代码：

```
(gdb) thread 4
Switching to thread 4 (LWP 11422)
(gdb) bt
#0 0x000000000041a110 in __lll_lock_wait
#1 0x000000000041ea4 in pthread_mutex_lock ()
#2 0x0000000000433a20 in procB ()
#3 0x0000000000433a38 in bar_four ()
#4 0x0000000000433bc in foo_four ()
#5 0x0000000000433d4 in thread_four(void(*))
#6 0x000000000041b84 in thread_start ()
#7 0x0000000000438760 in thread_start ()
```

- 5. 检查线程 `#2` 及其等待代码：

```
(gdb) thread 2
Switching to thread 2 (LWP 11421)
(gdb) bt
#0 0x000000000040a110 in __lll_lock_wait
#1 0x000000000040a1a in __pthread_mutex_lock()
#2 0x000000000043025c in procA()
#3 0x0000000000433c1c in bar_two()
#4 0x0000000000433d30 in foo_two()
#5 0x0000000000433a48 in thread_two(void*)
#6 0x000000000040130a in start_thread()
#7 0x0000000000408760 in thread_start()
```

```
(gdb) disassemble procA

Dump of assembler for function _ZprocA:

0x0000000000403280 <0>:  stp     x29,x30, [sp],#16

0x0000000000403284 <4>:  mov     x29,sp

0x0000000000403288 <8>:  adpr     x0,0x4d1000 <main_area-2128>

0x0000000000403290 <12>: add     x0,x0,0x68

0x0000000000403294 <16>: bl      0x414bdc <pthread_mutex_lock>

0x0000000000403298 <20>:  adpr     x0,0x4d1000 <main_area-2128>

0x000000000040329c <24>:  mov     x0,x0,#0x5d

0x00000000004032a0 <28>: bl      0x414bdc <pthread_mutex_lock>

0x00000000004032a4 <32>:  mov     x0,#16

0x00000000004032a8 <36>: add     x0,x0,0x74

0x00000000004032ac <40>: adpr     x0,0x4d1000 <main_area-2128>

0x00000000004032d0 <44>: mov     x0,x0,#0x5d

0x00000000004032d4 <48>: bl      0x416054 <pthread_mutex_unlock>

0x00000000004032d8 <52>: adpr     x0,0x4d1000 <main_area-2128>

0x00000000004032dc <56>: add     x0,x0,0x68

0x00000000004032e0 <60>: bl      0x416054 <pthread_mutex_unlock>

0x00000000004032e4 <64>: ldp     x29,x30,[sp],#16

0x00000000004032e8 <68>: ret

End of assembler dump.
```

注意：线程 `#4` 拥有互斥锁 `0x004d1000+0x68`，正在等待互斥锁 `0x004d1000+0x608`。

我们确定线程 `#2` 正在等待互斥锁 `0x004d1000+0x608`，该锁在 `procC` 中被意外解锁了。我们还注意到 catch 异常触发了等待互斥锁 `0x004d1000+0x608` 的代码执行。

注意：C++ 函数名经过修饰，如有需要请取消修饰：

```
(gdb) print asm-demangle
```

```
(gdb) disassemble procA

Dump of assembler code for function procA():

0x0000000000433220 <0>: stp     x29, x30, [sp],#-16

0x0000000000433224 <4>: mov     x29,sp

0x0000000000433228 <8>: adpr     x0,0x4d1000 <main_area-2128>

0x0000000000433230 <12>: add     x0,x0,#0x5d

0x0000000000433234 <16>: bl      0x414bdc <pthread_mutex_lock>

0x0000000000433238 <20>: bl      0x403200 <ZprocCV>

0x000000000043323c <24>: add     x0,x0,0x68

0x0000000000433240 <28>: adpr     x0,0x4d1000 <main_area-2128>

0x0000000000433244 <32>: mov     x0,x0,#0x5d

0x0000000000433248 <36>: bl      0x416054 <pthread_mutex_unlock>

0x000000000043324c <40>: mov     x0,#16

0x0000000000433250 <44>: add     x0,x0,0x74

0x0000000000433254 <48>: adpr     x0,0x4d1000 <main_area-2128>

0x0000000000433258 <52>: add     x0,x0,0x68

0x000000000043325c <56>: bl      0x416054 <pthread_mutex_unlock>

0x0000000000433260 <60>: add     x0,x0,0x68

0x0000000000433264 <64>: ldp     x29,x30,[sp],]#16

0x0000000000433268 <68>: b      0x403278 <_ZprocAv+84>

0x0000000000433270 <72>: bl      0x04039b4 <cxa_begin_catch>

0x0000000000433270 <76>: bl      0x0403a58 <cxa_end_catch>

0x0000000000433274 <80>: b       0x403248 <Z5procAv+36>
```
