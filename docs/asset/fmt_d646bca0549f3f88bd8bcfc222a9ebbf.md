
# Child-SP RetAddr      Call Site

```
0000007f 7f81c8c8 00000000415294 App12!_lll_lock_wait+0x1c
0000007f 7f81c8e0 0000000041dec App12!pthread_mutex_lock+0x54
0000007f 7f81c8d7 0000000041fa8a App12!proca+0x37
0000007f 7f81c8d8 00000000401f96 App12!bar_two+0x9
0000007f 7f81c8d9 00000000401faa App12!foo_two+0x9
0000007f 7f81c8d0 0000000044137f3 App12!thread_two+0x111
0000007f 7f81c8dc 0000000045512f7 App12!start_ofthread+0xf3
0000007f 7f81c8e8 ffffffff ffffffff App12!_clone+0x3f
0000007f 7f81c8e8 ffffffff ffffffff
```

## 16. 我们在退出 WinDbg 前关闭日志

打开文件 `C:\ALCD2\x64\App12-WinDbg.log`

## 练习 A1 (A64, WinDbg)

**目标：** 学习如何导出内存进行后处理、获取带有源代码的函数反汇编、本地变量和类型。

**模式：**
- 我们有一个去除了调试信息的 `App12` 可执行文件，并在 `App12` 文件夹中有一个原始可执行文件。
- 启动 `WinDbg`。
- 设置某些命令的输出日志文件：
  `.log C:\ALCD2\x64\App12-WinDbg.log`
- 打开文件 `C:\ALCD2\x64\App12-WinDbg.log`
- 指定符号路径并重载符号：
  `.sympath C:\ALCD2\x64\Symbols`
  符号路径为：`srv*;C:\ALCD2\x64\Symbols`
  扩展搜索路径为：`srv*;https://dl.microsoft.com/download/symbols;c:\alcd2\a64\app12\symbols`

```
*********** Path validation summary **********
Response Time (ms) Location
Deferred srv*OK C:\ALCD2\x64\Symbols
*** WARNING: Unable to verify timestamp for App12
.reload
*** WARNING: Unable to verify timestamp for App12

*********** Symbol Loading Summary ************
Module name Error
App12 系统找不到指定的文件。你可以通过开启符号诊断（!sym）并重复导致符号加载的命令来排除故障。你应该检查你的符号路径（.sympath）是否正确。注意：忽略警告和错误，因为它们现在无关。
```

### 6. 列出所有线程跟踪

我们现在包含了一些代码引用：

```
0:000 -k
```

```
Unable to get thread data for thread 0

1 Id: 45e4.45e7 Thread: 0 00000000 00000000 Frozen

   Call Site
# Child-Sp RetAddr
   App12_llbc_nanoseleep+x24

00000000 f5de45e7 00000000 004032ec App12_sleep+x10
00000000 f5de9620 00000000 004032db
00000000 f5de5810 00000000 00403ic App12_bar+x10 [/home/alloc/ALCDA2/App12/main.cpp @ 72]
00000000 f5de5820 00000000 00403dec App12_foo+x4c [/home/alloc/ALCDA2/App12/main.cpp @ 72]
00000000 f5de5830 00000000 00403dea App12_thread+x10 [/home/alloc/ALCDA2/App12/main.cpp @ 72]
00000000 f5de5840 00000000 00403df App12_pro+x48 [/home/alloc/ALCDA2/App12/main.cpp @ 43]
00000000 f5de5850 00000000 00403e00 App12_two+xc0 [/home/alloc/ALCDA2/App12/main.cpp @ 73]
00000000 f5de5860 00000000 00403b64 App12_thread_start+xb4
00000000 f5de5870 ffffffff ffffffff App12_thread_start+00
00000000 f5de5980 ffffffff ffffffff
```

```
Unable to get thread data for thread 2

1 Id: 45e4.55f1 Thread: 0 00000000 00000000 Frozen

   Call Site
# Child-Sp RetAddr
   App12_llbc_nanoseleep+x24

00000000 f5de5500 00000000 00403b4 App12_sleep+x10
00000000 f5de9620 00000000 0040364
00000000 f5de93f8 00000000 0040378 App12_bar+x10 [/home/alloc/ALCDA2/App12/main.cpp @ 72]
00000000 f5de93e8 00000000 00403cc App12_foo+x4c [/home/alloc/ALCDA2/App12/main.cpp @ 72]
00000000 f5de5830 00000000 004033b App12_thread+x10 [/home/alloc/ALCDA2/App12/main.cpp @ 72]
00000000 f5de5840 00000000 00403f4 App12_pro+x48 [/home/alloc/ALCDA2/App12/main.cpp @ 43]
00000000 f5de5850 00000000 00403870 App12_two+xc0 [/home/alloc/ALCDA2/App12/main.cpp @ 73]
00000000 f5de5860 00000000 00403b64 App12_thread_start+xb4
00000000 f5de5870 ffffffff ffffffff App12_thread_start+00
00000000 f5de5980 ffffffff ffffffff
```

```
06 0000000 f952e0fb f952e0fb fffffffff 00438b50
07 0000000 fffffffff fffffffff 00000000
08 0000000 f952e0fb fffffffff 0xffffff

App12!start_thread+0xb4
App12!thread_start+0xb3
0xffffffff ffffffff
```

无法获取线程 4 的线程数据

```
4 Id: A45e6.453 Suspended: Et: 00000000 00000000 00000000 Unfrozen

## Child-SP

| RetAddr | Call Site |
| --- | --- |
| 00 0000000 f841d650 00000000 00433b44 |
| 01 0000000 f841d620 00000000 004031f0 |
| 02 0000000 f841d618 00000000 00403404 |
| 03 0000000 f841d62e 00000000 0040341c |
| 04 0000000 f841d638 00000000 004100a4 |
| 05 0000000 f841d640 00000000 00403508 |
| 06 0000000 fffffffff fffffffff fffffffff |
| 07 0000000 fffffffff 00000000 |

App12!_lib_nanleep+0x24
App12!sleep+0x10
App12!bar_one+0x10 [/home/opt/ALCD2/App12.main.cpp @ 76]
App12!foo_one+0xc0 [/home/opt/ALCD2/App12.main.cpp @ 76]
App12!thread_start+0x10 [/home/opt/ALCD2/App12.main.cpp @ 76]
App12!thread_start+0xb3
0xffffffff ffffffff
```

无法获取线程 5 的线程数据

```
6 Id: A45e6.456 Suspended: Et: 00000000 00000000 00000000 Unfrozen

## Child-SP

| RetAddr | Call Site |
| --- | --- |
| 00 0000000 f841bbcc6 00000000 00433b44 |
| 01 0000000 f841b1d0 00000000 004034e6 |
| 02 0000000 f841b4e6 00000000 00410dbc |
| 03 0000000 f841f4f0 00000000 004030b8 |
| 04 0000000 f841c1a0 00000000 004030c4 |

App12!_lib_nanleep+0x24
App12!sleep+0x10
App12!max_0+0xb8 [/home/opt/ALCD2/App12.main.cpp @ 93]
App12!_lib_start_max+0x304
```

### 7. 如果我们想使用这种变体

```
0:000~-kl

## Child-SP

| RetAddr | Call Site |
| --- | --- |
| 00 0000000 f841bd5e 00000000 00433b48 |
| 01 0000000 f841b520 00000000 004032d8 |
| 02 0000000 f841b510 00000000 004032ec |
| 03 0000000 f841b528 00000000 00403304 |
| 04 0000000 f841b5310 00000000 00403b04 |
| 05 0000000 f841d580 00000000 00438760 |
| 06 0000000 f841d590 00000000 00000000 |

App12!_lib_nanleep+0x24
App12!sleep+0x10
App12!foo_one+0xc0
App12!thread_one+0xe10
App12!start+0xb4
App12!thread_start+0xb3
0xffffffff fffff
```

### 8. 如果想在栈中包含参数，使用另一种变体

```
0:000-s

## Child-SP

| RetAddr | Call Site |
| --- | --- |
| 00 0000000 f841bc00 00000000 00433b44 |
| 01 0000000 f841b1d0 00000000 004034e6 |
| 02 0000000 f841b2f0 00000000 00410dbc |
| 03 0000000 f841b4f0 00000000 004030b8 |
| 04 0000000 f841c1a0 00000000 004030c4 |

int **arg = 0;
char **arg = (0x00000000f841c0a)+xb8

App12!_lib_nanleep+0x24
App12!sleep+0x10
App12!main
App12!_lib_start_main+0x304
App12!start+0x4c
```

### 9. 切换到线程 #5 及其帧、参数和局部变量

```
0:000~5

App12!_lib_nanleep+0x24:

00000000 0041ae24 d400001 svc

#0

| Register | Value |
| --- | --- |
| x0 | 00000000f841ffff |
| x1 | 00000000f841bd40 |
| x2 | 00000000f841bef0 |
| x3 | 00000003a6e0108 |
| x4 | 00000000f841b30 |
| x5 | 00000000f841fb7 |
| x7 | 00000003a6e0267 |
| x8 | 0000000000000005 |
| x9 | 0000000004d07b |
| x11 | 00000003a6e0350 |
| x12 | 0000000000000000 |
| x13 | 00000000f841bd4d |
| x15 | 00000000000003d0 |
| x16 | 0000000000000000 |
| x17 | 00000000f841ad3d |
| x19 | 0000000000000011 |
| x20 | 00000000000000d8 |
| x21 | 000000000000025e |
| x22 | 0000000000000018 |
| x24 | 00000000000004e0 |
| x25 | 0000000000000250 |
| x27 | 00000000f8414d50 |
| x28 | 0000000000000000 |
| fp | 00000000f841f8e1c |
| sp | 00000000f841bef0 |
| pc | 000000000000034e |

App12:
000000000000034e 52800000 mov w0, #0

prv param 00000000f841f8b2c @fp+0x0001c
prv param 00000000f841f8f0 @fp+0x0001c
argv = 0x00000000f841c0a8
```

### 10. 检查 `argv` 数组

```
0005: dpa 00000000f841c08 L10

| Address | Value |
| --- | --- |
| 00000000f841c1a8 | 00000000f841f67 "/App12" |
| 00000000f841c1a8 | 0000000000000000 |
| 00000000f841c0b6 | "XDG_SESSION,ID=8954" |
| 00000000f841c0c6 | 00000000f841ff3 "HOSTNAME=instance-202109204" |
| 00000000f841c0c8 | 00000000f841f13 "SELIN_ROLE_REQUESTED-" |
| 00000000f841cda | 00000000f841fe2 "TERM_version=256" |
| 00000000f841c0db | 00000000f8417b1 "SHELL:/bin/bash" |
| 00000000f841c0e0 | 00000000f8417a4 "HISTSIZE=100" |
| 00000000f841c0e2 | 00000000f84175d "PWD=/home/op/ALCD2" |
```

### 11. 我们可以通过 `ctx` 命令重置后续代码并设置帧来指定源代码路径（源码视图）

```
0005: .srcpath C:\ALDA2\A64\App12
```
