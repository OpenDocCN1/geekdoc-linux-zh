

checked=320000
checked=320000
found (thread 3): [hello, world![0x1ff446522]. seconds spent=3
  min[0]=0x00000000  max[0]=0xffffff
  min[1]=0x02000000  max[1]=0x3fffffff
  min[2]=0x04000000  max[2]=0x5fffffff
  min[3]=0x06000000  max[3]=0x7fffffff
```

计算结果的前3个字符确实是零：

```
C:\...sha512sum test
000000f4a8fac5aed38794da4c139f5427ad5d9b3bc35465cdf57af6040
3
d3fe360195764fc997e507395fed78fee50eb38dd4027c9cb114672
2 *
```

在笔记本的4核上Intel Xeon E3-1230 CPU运行这个程序，耗时大约2~3秒。我们可以在任务管理器中看到5个线程：1个主进程和4个线程。虽然它还有精简的结构，但是我没有对程序源代码进行优化。深度优化可以大幅度提升的运行效率。另，由于我的CPU有4个内核，所以它引发了4个线程——完全符合OpenMP规范。

通过程序输出的数据统计，我们可以清楚地观察到整个穷举空间被划分为大致相等的四个部分。严格来说，考虑到最后一个比特位，这四个区域确实并不完全相等。

OpenMP提供了屏障块atomic（原子性）的Pragma指令。顾名思，被标记为原子的代码不会被拆分为多个线程运行。我们来看这段代码：

```c
#pragma omp atomic
checked++;

#pragma omp critical
if ((checked % 100000)==0)
  printf("checked=%d\n", checked);
```

MSVC 2012 编译，上述代码对应的汇编指令如下。

## 指令清单92.3 MSVC

```assembly
push      edi
push      OFFSET _checked
call      __vcomp_atomic_add_i4
; Line 55
push      OFFSET $vcomp$critsect$
call      __vcomp_enter_critsect
add       esp, 12
;
000000Ch
; Line 56
mov       ecx, DWORD PTR _checked
cdq
mov       eax, ecx
mov       esi, 100000
;
000186a0H
div       esi
test      edx, edx
jne       SHORT LN1@check_nonc
; Line 57
push      ecx
push      OFFSET ??_C@0M@NPNHLIOO@checked?$DN$CFd?6?
$AA$
call      _printf
pop       ecx
pop       ecx
$LN1@check_nonc:
push      DWORD PTR $vcomp$critsect$
call      __vcomp_leave_critsect
pop       ecx
```

函数vcomp_enter_critsect() 调用的Win32 API函数EnterCriticalSection()[4]。

## 92.2 GCC

GCC 4.8.1生成的程序，统计结果和上面的程序一样。所以GCC分割区域的方法与MSVC相同。

## 指令清单92.4 GCC 4.8.1

```assembly
mov       edi, OFFSET FLAT:main._omp_fn.0
call      GOMP_parallel_start
```

GCC编译生成的程序，会发起3个新的线程，原有线程扮演第四的角色。所以，总体上GCC的进程数是4，MSVC的进程数是5。

其中，函数main_omp_fn.0的代码如下所示。

## 指令清单92.5 GCC 4.8.1

```assembly
mov      edi, 0
call     main_omp_fn.0
call     GOMP_parallel_end
main_omp_fn.0:
push     rbp
mov      rbp, rsp
push     rbx
sub      esp, 40
mov      QWORD PTR [rbp-40], rdi
call     omp_get_num_threads
mov      ebx, eax
call     omp_get_thread_num
mov      esi, eax
mov      eax, 2147483647 ; 0x7FFFFFFF
cdq      ebx
idiv     ebx
mov      ecx, eax
mov      eax, 2147483647 ; 0x7FFFFFFF
cdq      ebx
idiv     ebx
mov      eax, edx
mov      esi, eax
jl       .L15
L18:
imul     esi, ecx
mov      edx, esi
add      eax, edx
lea      ebx, [rax+rcx]
mp      eax, ebx
je       .L14
mov      DWORD PTR [rbp-20], eax
L17:
mov      eax, DWORD PTR [rbp-20]
mov      edi, eax
call     nonce
add      DWORD PTR [rbp-20], 1
cmp      DWORD PTR [rbp-20], ebx
jl       .L17
.L15:
jmp .L14
mov      eax, 0
add      ecx, 1
jmp .L18
.L14:
add      rsp, 40
pop      rbx
pop      rbp
ret
```

上述指令清晰显示：程序通过函数omp_get_num_threads() 和另一个函数omp_get_thread_num() 获取当前线程数以及当前线程编号，然后分割。GCC在代码中直接使用LOCK指令，而MSVC则是调用另一个函数：

## 指令清单92.6 GCC 4.8.1

```assembly
lock add DWORD PTR checked[rip], 1
call GOMP_critical_start
mov      ecx, DWORD PTR checked[rip]
mov      edx, 5184372
mov      eax, ecx
imul      eax
sar      edx, 13
mov      eax, ecx
sar      edx, 31
sub      edx, eax
mov      eax, edx
0x00000
mov      esi, eax
jl       .L15
mov      ecx, eax
mov      eax, 0x00000
imul     eax, 10000
sub      ecx, eax
mov      eax, edx
test      edx, edx
jne       .L7
mov      DWORD PTR checked[rip]
mov      esi, eax
mov      edi, OFFSET:.LC "checked=%d\n"
mov      eax, 0
call      printf
.L7:
call GOMP_critical_end
```

以gomp开头的函数属于GNU OpenMP Library。可以在[https://github.com/gcc/tree/master/libgomp](查其源码。
- [1] 仅演示说明。在实际情况下，使用OpenMP更为。
- [2] OpenSSL的库：http://www.openssl.org/source/
- [3] 有LOCK前缀的详细说明，请参附录6。

## 第93章 安腾指令

来说，安腾 (Itanium)处理器几乎是失败。但是Itanium (IA64)架构非常研究。乱序执行（OoO）侧于CPU指令的片段，再把重组后的指令到并行。而特尔（Intel）架构的并行技术（Explicitly Parallel Instruction Code, EPIC），让编译器这种并行技术的编译器因为复杂而引起了争议。本章从Linux内核取了部分。Intel和HP的开发者针对常见指令进行了划分，从而得出了指令类型（即指令模板）。CPU据此将指令分为基本类型（basic types），基本类型又分为带有停止位的指令和不停止位的实例。例如，0类指令叫做MFII指令，依次由内存读写操作（M）和两类整数操作（II）构成；最后一种，0xd1类，又叫MFB类，依次由内存读写操作（M）、浮点数操作（B）构成。如果汇编器在指令槽（instruction slot）上没有操作指令，那么它可能在这些位置上插入nop。在人工汇编中，m代表内存。

## 指令清单93.1 Linux kernel 3.2

```c
#define TEA_ROUNDS 32
#define TEA_DELTA 0x9e37b9

static void tea_encrypt(struct crypto_ctx *tfm, u8 *dst, u8 *src)
{
	u32 y, z, n, sum = 0;
	u32 k0, k1, k2, k3;
	struct crypto_ctx *ctx = tfm;
	const le32 *in = src;
	le32 *out = dst;

	y = le32_to_cpu(in[0]);
	z = le32_to_cpu(in[1]);

	k0 = ctx->KEY[0];
	k1 = ctx->KEY[1];
	k2 = ctx->KEY[2];
	k3 = ctx->KEY[3];

	n = TEA_ROUNDS;
	while (n-- > 0) {
		sum += TEA_DELTA;
		y += ((z << 4) + k0) ^ (z >> 5);
		z = ((y << 4) + k2) ^ (y >> 5) + k3;
	}
	out[0] = le32_to_cpu(y);
	out[1] = le32_to_cpu(z);
}
```

其详细结果所示：

## 指令清单93.2 Linux Kernel 2.0.4 for Itanium 2 (McKinley)

```assembly
0090                   tea_encrypt:
0090   08 80 80 41 00 21    adds r16 = 96, r32    // ptr to ctx->KEY[2]
0096   80 02 00 42 00        adds r8 = 88, r32     // ptr to ctx->KEY[0]
009C   00 00 04 00             nop.i 0
00A0   09 18 70 41 00 21    adds r3 = 92, r32     // ptr to ctx->KEY[1]
00A6   F0 20 28 28 00        ld4 r15 = [r34], 4   // load z
00AC   44 06 01 84            adds r32 = 100, r32  // ptr to ctx->KEY[3]
00B0   08 98 00 20 10 10        ld4 r19 = [r16]      // r19=k2
00B6   01 00 00 42 40        mov.i r6=0           // r0—是0
00BC   08 CA 00             mov.i r2 = ar.lc      // 保存lc
00C0   05 70 00 44 10 9E FF 7F 20  ld4 r14 = [r34]  // load y
00CC   0F 32 CE 6B            mov.i r17 = 0xFFFE9E379B9 // TEA_DELTA
00D0   08 00 00 01 00        nop.m 0
00D6   50 01 20 20 00        ld4 r21 = [r8]       // r21=k0
00DC   F0 09 2A 00            mov.i ar.lc = 31     // TEA_ROUNDS=32
00E0   A0 00 06 10          ld4 r20 = [r32]      // r20=k1
00E6   20 01 80 20 20        ld4 r18 = [r32]      // r18=k3
00EC   00 00 04 00             nop.i 0
00F0:
00F0   08 80 80 41 00 21    adds r16 = 96, r32    // sum
00F6   80 02 00 42 00        adds r8 = 88, r32     // z
00FC   00 00 04 00             nop.i 0
0100   09 18 70 41 00 21    adds r3 = 92, r32     // k2
0106   F0 20 28 28 00        ld4 r15 = [r34], 4   // y
010C   44 06 01 84            adds r32 = 100, r32  // k3
0110   08 98 00 20 10 10        ld4 r19 = [r16]      // k0
0116   01 00 00 42 40        mov.i r6=0           // n
011C   08 CA 00             mov.i r2 = ar.lc      // lc
0120   05 70 00 44 10 9E FF 7F 20  ld4 r14 = [r34]  // sum
0126   0F 32 CE 6B            mov.i r17 = 0xFFFE9E379B9 // TEA_DELTA
012C   08 00 00 01 00        nop.m 0
0130   50 01 20 20 00        ld4 r21 = [r8]       // y
0136   F0 09 2A 00            mov.i ar.lc = 31     // rounds
013C   A0 00 06 10          ld4 r20 = [r32]      // z
0140   20 01 80 20 20        ld4 r18 = [r32]      // k3
0146   00 00 04 00             nop.i 0
014C   00 00 04 00             nop.i 0
```

