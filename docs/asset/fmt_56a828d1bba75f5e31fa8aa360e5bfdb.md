
```
crash> dis foo+0x8
0ffff8007beaa0b <foo+8>:    b 0ffff8007beaa0b <foo+8>
crash> dis kthread_f
0ffff8007beaa08 <kthread_f>: mov     x9, x30
0ffff8007beaa0c <kthread_f+0x4>:  nop
0ffff8007beaa10 <kthread_f+0x8>:  paciasm
0ffff8007beaa14 <kthread_f+0xc>:  mov     w0, #02710                // #10000
0ffff8007beaa18 <kthread_f+0x10>: stp     x29, [sp], [sp, -16]
0ffff8007beaa1c <kthread_f+0x14>: mov     x29, sp
0ffff8007beaa20 <kthread_f+0x18>: bl     0ffff8000801d338 <msleep>
0ffff8007beaa24 <kthread_f+0x1c>: bl     0ffff8007beaa0b <foo>
0ffff8007beaa28 <kthread_f+0x20>: mov     w0, #0x0
0ffff8007beaa2c <kthread_f+0x24>: ldp     x29, x30, [sp], #16
0ffff8007beaa30 <kthread_f+0x28>: mov     x16, #0x0                // #0
0ffff8007beaa34 <kthread_f+0x30>: mov     x17, #0x0                // #0
0ffff8007beaa38 <kthread_f+0x34>: ret     .inst 0x81634280
0ffff8007beaa3c <kthread_f+0x38>: .inst 0xffff8000                // undefined
crash> dis 0ffff807beaa0b+4
0ffff8007beaa00 <foo+0>:  mov     x9, x30
0ffff8007beaa04 <foo+4>:  nop
0ffff8007beaa08 <foo+8>:    b 0ffff8007beaa0b <foo+8>
0ffff8007beaa0c <foo+12>: udf     #0
```

## 练习 K4 (A64, WinDbg)

### 目标

学习识别飙升线程。

### 模式

堆栈收集 (CPU)；中断堆栈；飙升线程。

1. 将 A64 目录下的 `vmlinux-6.8.0-1018` 文件并设置符号。
2. 启动 `WinDbg`。从 A64/KSym 目录加载 `2025101833.kdump` 并设置路径 A64/KSym（输入 `.reload` 命令时可能会出现延迟/无响应）。

```
Microsoft (R) Windows Debugger Version 10.0.2722.0 AM64
Copyright (c) Microsoft Corporation. All rights reserved.
Loading Dump File: [C:\ALDA2\A64\2025101833.kdump] 64-bit machine 64-bit

*** Path validation ***
Response Time (ms) Location Deferred
Symbol path: is Executable search path: Generic Kernel Version 10 (procs) Free 64-bit (Arch64)
Primary image base = 0xffffff008010000 Loaded module list = 0x0000000000000000
System Uptime: not available
Loading Kernel Symbols
Loading User Symbols
For analysis of this file, run .analyze -v fffff8008029d70 stp x1,x2,[x2]
.sympath C:\ALDA2\A64\KSym
Symbol path is: C:\ALDA2\A64\KSym
*** Path validation ***
Response Time (ms) Location OK C:\ALDA2\A64\KSym
.reload
Loading Kernel Symbols
*** WARNING: Unable to verify timestamp for vmlinux
Loading User Symbols
*** Loading Error Summary ***
Error Module name vmlinux 系统找不到的文件可以通过开启符号诊断 (!noisy) 并重复导致符号加载的命令来排除符号相关问题。你还应该检查符号路径 (.sympath) 是否正确。
```

手动 dump 的 CPU 0 线程跟踪：

| kd | Child-SP | RetAddr | Call Site |
| :--- | :--- | :--- | :--- |
| 00 | fffff880085993a60 | fffff880080d2b5f0 | `vmlinux!crash_regs+0xa0` |
| 01 | fffff880085993a60 | fffff880080d2e6c0 | `vmlinux!cr_6h_exec+0x60` |
| 02 | fffff880085993a60 | fffff880080d32e68 (T) | `vmlinux!panic+0x350` |
| 03 | fffff880085993b48 | fffff880080d39a98 | `vmlinux!sysrq_handle_crash+0x1c` |
| 04 | fffff880085993b50 | fffff880080d3074 | `vmlinux!handle_sync+0xb8` |
| 05 | fffff880085993b60 | fffff880085f22cc0 | `vmlinux!write_trigger+0x154` |
| 06 | fffff880085993c20 | fffff88008510270 | `vmlinux!proc_reg_write+0xcc` |
| 07 | fffff880085993c40 | fffff88008510728 | `vmlinux!k_ys_write+0x0` |
| 08 | fffff880085993c50 | fffff880085107e8 | `vmlinux!ksys_write+0x0` |
| 09 | fffff880085993d20 | fffff88008001c60 | `vmlinux!arm64_system_write+0x24` |
| 0a | fffff880085993d30 | fffff88008001ab8 | `vmlinux!invoke_syscall+0x78` |
| 0b | fffff880085993e10 | fffff880080015d0 | `vmlinux!el0_svc_common_const.op+0x48` |
| 0c | fffff880085993e70 | fffff88008150fd8 | `vmlinux!do_el1_svc+0x28` |
| 0d | fffff880085993e80 | fffff88008150ff0 | `vmlinux!el1_svc+0x40` |
| 0e | fffff880085993e90 | fffff88008110640 | `vmlinux!el1_svc_handler+0x15c` |
| 0f | fffff880085993e00 | fffff88000000000 | `vmlinux!el64_sync+0xa8` |

CPU 1 线程跟踪显示了一个无限循环：

```
*** WARNING: Unable to reset page
```

| kd | Child-SP | RetAddr | Call Site |
| :--- | :--- | :--- | :--- |
| 00 | fffff880085993a60 | fffff88008010f30 | `mod_c+0xb8` |
| 01 | fffff880085993a70 | fffff88008017a30 | `vmlinux!kthread_f+0xe0` |
| 02 | fffff880085993a60 | fffff880000000000 | `vmlinux!ret_from_fork+0x140` |

```
x0=0000000000000000 x1=0000000000000000 x2=0000000000000000 x3=0000000000000000 x4=ffffffff8000c31d08 x5=ffffffff80007b6ed02 x6=0000000000000000 x7=0000000000000000 x8=ffffffff8000c831df0 x9=0000000000000000 x10=0000000000008176 x11=0000000000000154 x12=0000000000000000 x13=0000000000000000 x14=0000000000000000 x15=0000000000000000 x16=0000000000000000 x17=ffffffff80008593968 x18=0000000000000000 x19=ffffffff8000c056b40 x20=ffffffff8000ca9e6b0 x21=ffffffff80008593e598 x22=ffffffff8000c83dc40 x23=ffffffff80007aea008 x24=0000000000000000 x25=000000000000e360 x26=0000000000000000 x27=0000000000000000 x28=0000000000000000 fp=ffffffff80008593e560 lr=ffffffff80007beea028 sp=ffffffff80008593e560 pc=ffffffff80007beea0b8 -ZC- EL1
mod_c+0xb8:
ffffff8800 7beea0b8 b mod_c+0xb8 (ffff8800 7beea0b8)
```

## 练习 K5

### 目标

学习识别堆栈溢出和内核堆栈边界

### 模式

堆栈溢出（内核模式）

- `\ALCDA-Dumps\Exercise-K5-x64-GDB.pdf`
- `\ALCDA-Dumps\Exercise-K5-A64-GDB.pdf`
- `\ALCDA-Dumps\Exercise-K5-A64-WinDbg.pdf`
- `\ALCDA-Dumps\Exercise-K5-x64-WinDbg.pdf`

## 状态：运行中 (恐慌)

`crash/`

2. 回溯显示在任务栈溢出时发生了递归错误和双重异常：

```
crash! bt

PID: 2662 TASK: fffff97e51058000 CPU: 0 COMMAND: "mod_d thread"

#0 [ffff7f1174acc00] machine_kmalloc at fffffffffa8c92db1

#1 [ffff7f1174ad7d8] crash_kmalloc at fffffffffa8df1e46

#2 [ffff7f1174ad7e8] panic at fffffffff8cdcdf29

#3 [ffff7f1174ae6e8] oops_end at fffffffffa8c432c2

#4 [ffff7f1174a7e90] handle_stack_overflow at fffffffffa8c43cd3

#5 [ffff7f1174a7f60] double_fault at fffffffffa9ffcb61

#6 [ffff7f1174a7f740] double_fault at fffffffffa9ef0cac

[exception] RIP: foo=1f5

RIP: fffffffff09a0a4 RSP RSP: fffffffff4c01a708 RFLAGS: 0010246

RAX: 0000000000000000 RBX: 0000000000000000 RCX: 0000000000000000

RDX: 0000000000000000 RSI: 0000000000000000 RDI: 0000000000000000

RBP: fffffffff4c01a708 R9: 0000000000000000

R10: 0000000000000000 R11: fffffffff4c01a708 R12: fffff97e5c0c2a80

R13: fffff14e7b7b668 R14: fffff97e5c0c92e80 R15: ffffffc0c09a910

ORX: ffffffffffffffff CS: 0010 SS: 0018

--双重异常栈栈:

#8 [ffff14e041740d8] bar at fffffffff09a0b4 [mod_d]

#9 [ffff14e04174018] bar at fffffffff09a0b4 [mod_d]

#10 [ffff14e04174038] bar at fffffffff09a0b4 [mod_d]

#11 [ffff14e04174058] bar at fffffffff09a0b4 [mod_d]

#12 [ffff14e04174078] bar at fffffffff09a0b4 [mod_d]

#13 [ffff14e04174098] bar at fffffffff09a0b4 [mod_d]

#14 [ffff14e041740b8] bar at fffffffff09a0b4 [mod_d]

#15 [ffff14e041740d8] bar at fffffffff09a0b4 [mod_d]

#16 [ffff14e041740f8] bar at fffffffff09a0b4 [mod_d]

#17 [ffff14e04174118] bar at fffffffff09a0b4 [mod_d]

#18 [ffff14e04174138] bar at fffffffff09a0b4 [mod_d]

#19 [ffff14e04174158] bar at fffffffff09a0b4 [mod_d]

#20 [ffff14e04174178] bar at fffffffff09a0b4 [mod_d]

#21 [ffff14e04174198] bar at fffffffff09a0b4 [mod_d]

#22 [ffff14e04174218] bar at fffffffff09a0b4 [mod_d]

#23 [ffff14e04174238] bar at fffffffff09a0b4 [mod_d]

#24 [ffff14e04174258] bar at fffffffff09a0b4 [mod_d]

#25 [ffff14e04174278] bar at fffffffff09a0b4 [mod_d]

#26 [ffff14e04174298] bar at fffffffff09a0b4 [mod_d]

#27 [ffff14e041742b8] bar at fffffffff09a0b4 [mod_d]

#28 [ffff14e041742d8] bar at fffffffff09a0b4 [mod_d]

#29 [ffff14e041742f8] bar at fffffffff09a0b4 [mod_d]

#30 [ffff14e04174318] bar at fffffffff09a0b4 [mod_d]

#31 [ffff14e04174338] bar at fffffffff09a0b4 [mod_d]

#32 [ffff14e04174358] bar at fffffffff09a0b4 [mod_d]

#33 [ffff14e04174378] bar at fffffffff09a0b4 [mod_d]

#34 [ffff14e04174398] bar at fffffffff09a0b4 [mod_d]

#35 [ffff14e041743b8] bar at fffffffff09a0b4 [mod_d]

#36 [ffff14e041743d8] bar at fffffffff09a0b4 [mod_d]

--由于原始栈没有空间，使用了不同的栈区域。

注意：由于原始区域没有空间，使用了不同的栈区域。
```

3. 我们可以从任务结构体中获取栈限制（在 x64 系统上，栈为 4 页，`0x4000` 字节）：

```
crash> mach
MACHINE TYPE: x86_64
MEMORY SIZE: 4 GB
CPU: 4
HYPERVISOR: Hyper-V
PROCESSOR SPEED: 211 MHz
HZ: 1000
PAGE SIZE: 4096
KERNEL VIRTUAL BASE: fffff7e4c000000
KERNEL VMALLOC BASE: fffffac1e4c0000
KERNEL VMMAP: fffffbb4c0000000
KERNEL START MAP: fffffffff8000000
KERNEL MODULES BASE: fffffffff000000
KERNEL STACK SIZE: 16384
```
