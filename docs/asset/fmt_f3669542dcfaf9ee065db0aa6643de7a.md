
# `#7` `0x00000000045d2f2` in `clone(void *)`

`Thread 3` (`0x7f645e8b7f0` (`LWP 165`)):

# `0` `0x00000000455a70` in `nanosleep`

# `1` `0x0000000045a99f` in `sleep()`

# `2` `0x0000000004023b6` in `procNE()` at `pthread_create.c:688`

# `3` `0x0000000004023f2` in `bar_two()`

# `4` `0x0000000004025e` in `foo_one()` at `pthread_create.c:688`

# `5` `0x00000000040242` in `four(void*)` at `pthread_create.c:688`

# `6` `0x0000000041b4b3` in `start_thread (arg-optimized out)` at `pthread_create.c:486`

# `7` `0x00000000045d222` (`(` (`(` (`(`)

  1 (`00006000000000011__....()`

# `3` `0x0000000042b46` in `__cxa1_terminate(void (**))` at `pthread_create.c:688`

# `4` `0x0000000042681` in `std::terminate()` at `pthread_create.c:688`

# `5` `000000000424c4` in `__raise()` at `pthread_create.c:688`

# `6` `0x00000000422de` in `procB()` at `pthread_create.c:688`

# `7` `0x00000000423b3` in `procA()` at `pthread_create.c:688`

# `8` `0x000000000023a0` in `procW()` at `pthread_create.c:688`

# `9` `0x0000000004023c2` in `bar_one()` at `pthread_create.c:688`

`--<RET>`, from `main`, to `quit`, `quit` to continue without paging-

# `10` `0x00000000040255e` in `sleep()` at `pthread_create.c:688`

# `11` `0x0000000004023e2` in `thread_one(void*)()` at `pthread_create.c:688`

# `12` `0x0000000041b4b3` in `start_thread (arg-optimized out)` at `pthread_create.c:486`

# `13` `0x00000000045d2f2` in `clone(void *)`

`Thread 1` (`0x7f6457fb070` (`LWP 162`)):

# `0` `0x0000000042fdb` in `raise()`

# `1` `0x000000004017d` in `abort()` at `pthread_create.c:688`

# `2` `0x0000000041553` in `__gnu_cxx_terminate_handler()` `[clone.so]`

# `3` `0x0000000042b46` in `__cxa1_terminate(void (**))` at `pthread_create.c:688`

# `4` `0x0000000042681` in `std::terminate()` at `pthread_create.c:688`

# `5` `000000000424c4` in `__raise()` at `pthread_create.c:688`

# `6` `0x00000000422de` in `procB()` at `pthread_create.c:688`

# `7` `0x00000000423b3` in `procA()` at `pthread_create.c:688`

# `8` `0x000000000023a0` in `procW()` at `pthread_create.c:688`

# `9` `0x0000000004023c2` in `bar_one()` at `pthread_create.c:688`

```
0x7f4d5f88070d: 0x0 0x0
0x7f4d5f88070e: 0x0 0x0
0x7f4d5f88070f: 0x0 0x0
0x7f4d5f880800: 0x0 0x0
0x7f4d5f880801: 0x0 0x0
0x7f4d5f880820: 0x0 0x0
0x7f4d5f880830: 0x0 0x0
0x7f4d5f880840: 0x0 0x0
0x7f4d5f880850: 0x0 0x0
0x7f4d5f880860: 0x0 0x0
0x7f4d5f880870: 0x0 0x0
0x7f4d5f880880: 0x0 0x0
0x7f4d5f880890: 0x0 0x0
0x7f4d5f8808a0: 0x0 0x0
0x7f4d5f8808bd: 0x7f4d5f8808c0 0x4021dd <Zwork_8_v9>
--<按 <RET> 查看更多，按 <quit> 退出，在分页时继续>--
0x7f4d5f8808c0: 0x7f4d5f8808c0 0x4021e0 <Zwork_7_v9>
0x7f4d5f8808d0: 0x7f4d5f8808d0 0x4021f5 <Zwork_6_v9>
0x7f4d5f8808e0: 0x7f4d5f8808e0 0x402201 <Zwork_5_v9>
0x7f4d5f8808f0: 0x7f4d5f8808f0 0x40220d <Zwork_4_v9>
0x7f4d5f880900: 0x7f4d5f880900 0x402219 <Zwork_3_v9>
0x7f4d5f880910: 0x7f4d5f880910 0x402225 <Zwork_2_v9>
0x7f4d5f880920: 0x7f4d5f880920 0x402231 <Zwork_1_v9>
0x7f4d5f880930: 0x7f4d5f880930 0x402244 <Z4work_v16>
0x7f4d5f880940: 0x0 0x0
0x7f4d5f880950: 0x0 0x0
0x7f4d5f880960: 0x0 0x0
0x7f4d5f880970: 0x0 0x0
0x7f4d5f880980: 0x0 0x0
0x7f4d5f880990: 0x0 0x0
```

```bash
(gdb) disassembly 0x402210
函数 _Zwork_3 的汇编代码转储：
0x0000000000402210 <>: push   %rbp
0x0000000000402211 (+1): mov    %rsp,%rbp
0x0000000000402214 (<4>): callq  0x402204 <Zwork_4_v4>
0x0000000000402219 (+9): nop
0x000000000040221a (+10): pop    %rbp
0x000000000040221b (+11): ret
汇编结束。
注意：rbp 指向最后一个帧，可以轻松恢复之前的堆栈片段：
```

```
0x7f4d5f880800: 0x7f4d5f8808c0 0x4021dd <Zwork_8_v9>

0x7f4d5f8808c0: 0x7f4d5f8808c0 0x4021e0 <Zwork_7_v9>

0x7f4d5f8808d0: 0x7f4d5f8808d0 0x4021f5 <Zwork_6_v9>

0x7f4d5f8808e0: 0x7f4d5f8808e0 0x402201 <Zwork_5_v9>

0x7f4d5f8808f0: 0x7f4d5f8808f0 0x40220d <Zwork_4_v9>

0x7f4d5f880900: 0x7f4d5f880900 0x402219 <Zwork_3_v9>

0x7f4d5f880910: 0x7f4d5f880910 0x402225 <Zwork_2_v9>

0x7f4d5f880920: 0x7f4d5f880920 0x402231 <Zwork_1_v9>

0x7f4d5f880930: 0x7f4d5f880930 0x402244 <Z4work_v16>
```

```bash

(gdb) thread 2

切换到线程 2 (Thread 0x7f4d5f880700 (LWP 164))

#0 0x0000000045aa70 in nanosleep ()

```

```bash

(gdb) bt

#0 0x0000000045aa70 in nanosleep ()

#1 0x0000000045a9fa in sleep ()

#2 0x000000004236c in start () at pthread_create.c:688

#3 0x00000000420422 in bar () at pthread_create.c:688

#4 0x0000000042042e in foo_thread () at pthread_create.c:688

#5 0x00000000420424 in three_thread(void*) at pthread_create.c:688

#6 0x0000000041b4b3 in start_thread (arg=<optimized>) at pthread_create.c:486

#7 0x0000000045d2ef in clone ()

```

```bash

(gdb) x/152 $sp-rsp2000

0x7f4d5f07f530: 0x418950 <fd_encoding_encoding> 0x418600 <frame_down+112>

0x7f4d5f07f530: 0x7f4d5f080520 0x04f460 <object>

0x7f4d5f07f540: 0x7f4d5f0844a0 0xe3

0x7f4d5f07f550: 0x11b00000360 0x0

0x7f4d5f07f560: 0x7f4d5f0844b0 0x04f460 <object>

0x7f4d5f07f570: 0x01c770 0x6b

0x7f4d5f07f580: 0x7f4d5f084a0 0x041861 <frame_heap+145>

0x7f4d5f07f590: 0x03b8 0x3e635c37a

0x7f4d5f07f5a0: 0x7f4d5f08010 0x40172 <read_encoded_with_base>

0x7f4d5f07f5b0: 0x04f460 <object>

0x7f4d5f07f5c0: 0x7f4d5f08be0 <<Unwind_Raise+61>

0x7f4d5f07f5d0: 0x4d40d8

0x7f4d5f07f5e0: 0x041976 <search_object+854>

0x7f4d5f07f5f0: 0x042228

0x7f4d5f07f600: 0x7f4d5f07600 0x000001

0x7f4d5f07f610: 0x0

0x7f4d5f07f620: 0x7f4d5f07c8

0x7f4d5f07f630: 0x0423a4

0x7f4d5f07f640: 0x3

0x7f4d5f07f650: 0x04f460 <object>

0x7f4d5f07f660: 0x7f4d5f07760 0x7f4d5f07b8

0x7f4d5f07f670: 0x041db 0x0430b <pthread_key>

0x7f4d5f07f680: 0x042357 <personality+184>

0x7f4d5f07f690: 0x7f4d5f00b0

0x7f4d5f07f6a0: 0x0614234

0x7f4d5f07f6b0: 0x7f4d5f07f750 0x042033b <procAv+9>

0x7f4d5f07f6c0: 0x4c43d9

0x7f4d5f07f6d0: 0x05f07a1

0x7f4d5f07f6e0: 0x1db

0x7f4d5f07f6f0: 0x7f4d5f07f60 0x04165d <uw_frame_state_for+800>

0x7f4d5f07f700: 0x9b0000000000

0x7f4d5f07f710: 0x0c4339 0x7f4d5f07f718

0x7f4d5f07f720: 0x7f4d5f07f760 0x0460c0

0x7f4d5f07f730: 0x7f4d5f07f760 0x04000b00

0x7f4d5f07f740: 0x0

0x7f4d5f07f750: 0x7f4d5f07f7b0 0x4176fb <<Unwind_RaiseException_Phase2+75>

0x7f4d5f07f760: 0x0

0x7f4d5f07f770: 0x0

0x7f4d5f07f780: 0x0

0x7f4d5f07f790: 0xffffffffffffff

0x7f4d5f07f7a0: 0x0
```

### `4.` 转到线程 `#2`，识别异常处理代码，并检查其有效性：

```
0x7f4d5f0f7b0: 0x0

0x7f4d5f0f7c0: 0xffffffffff 0x1

0x7f4d5f0f7d60: 0x0

0x7f4d5f0f7b70: 0x0

0x7f4d5f0f7b80: 0x0

0x7f4d5f0f7b90: 0x0

0x7f4d5f0f7b00: 0x0

0x7f4d5f0f7b10: 0x0

0x7f4d5f0f7b40: 0x0

0x7f4d5f0f7b50: 0xffffffffff 0x1

0x7f4d5f0f7b60: 0x0

0x7f4d5f0f7b70: 0x0

0x7f4d5f0f7b80: 0x10

0x7f4d5f0f7b90: 0x06

0x7f4d5f0f7c00: 0x40283c <Z5hv++66>

-- 更多，按 <q> 退出，在分页时继续 --

0x7f4d5f0f7c10: 0x4030d0 <personality_v0> 0xffffffffff

0x7f4d5f0f7c20: 0x10

0x7f4d5f0f7c30: 0x011b 0x00

0x7f4d5f0f7c40: 0x7f4d5f07c8 0x0411f0

0x7f4d5f0f7c50: 0x04f460 <0000

0x7f4d5f0f7c50: 0x0

0x7f4d5f0f7c00: 000

0x7f4d5f0f7c10: 0x4a1fa7 <Unwind_RaiseException<730>

0x7f4d5f0f7c20: 0x4000000000000000 0x0

0x7f4d5f0f7c30: 0x00

0x7f4d5f0f7c40: 0x00

0x7f4d5f0f7c50: 0x7f4d5f0f7c88 0x7f4d5f0f7c90

0x7f4d5f0f7c60: 0x7f4d5f07fd28

0x7f4d5f0f7d70: 0x00

0x7f4d5f0f7d80: 0x7f4d5f0f7fd50 0x7f4d5f0f7f98

0x7f4d5f0f7d90: 0x00

0x7f4d5f0f7da0: 0x00
```

```bash

(gdb) disassemble code for function _0x4a17fa

函数 _Unwind_RaiseException 的汇编代码转储：

0x0000000000407cd0 <+0>: push   %rbp

0x0000000000407cd1 <+1>: mov     %rsp,%rbp

0x0000000000407cd4 <+4>: push    %r15

0x0000000000407cd6 <+6>: push    %r14

0x0000000000407cd8 <+8>: lea     -0x3a(%rip),%r14

0x0000000000407cdf <+15>: mov     0x10(%rip),%r6

0x0000000000407ce3 <+19>: push    %r13

0x0000000000407ce5 <+21>: mov    %di,%r13

0x0000000000407ce8 <+24>: mov    %r14,%di

0x000000000041cd0 <+29>: push   %r12

0x000000000041ce9 <+29>: lea     -0xc0(%rip),%r12

0x000000000041cf4 <+36>: push   %rbx

0x000000000041cf5 <+37>: lea     -0x2b(%rip),%rbx

0x000000000041cf6 <+44>: push   %rdx

0x000000000041cf7 <+45>: sub    -0x368(%rip),%rsp

0x0000000000417d8 <+56>: mov    0x08(%rip),%rdx

0x0000000000417d9 <+57>: call   0x417a0 <init_context_1>

0x000000000041de2 <+62>: movq   -0xa3(%rip),%xmm0

0x000000000041de6 <+70>: movq   -0x398(%rip),%xmm1

0x00000000004176a <+78>: movq   -0x380(%rip),%xmm2

0x0000000000417de6 <+86>: movq   -0x370(%rip),%xmm3

0x0000000000417de9 <+94>: movq   -0x364(%rip),%xmm4
```
