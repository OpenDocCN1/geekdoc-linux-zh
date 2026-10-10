
通过 `hwclock` 命令启用中断来触发处理程序的执行：

```bash
bash> hwclock
...    --> Kernel panic occurs when execution hits rtc_interrupt()
         causing kexec to boot into the capture kernel.
```

将 `/proc/vmcore` 保存到 `/dump/vmcore.dump`，重新引导回第一个（崩溃的）内核，并使用 `crash` 工具开始分析。在真实情况下，当然，转储可能是在客户现场捕获的，而分析是在支持中心进行的：

```bash
bash> crash /usr/src/linux/vmlinux /dump/vmcore.dump
crash 4.0-2.24
...
KERNEL: /usr/src/linux/vmlinux
DUMPFILE: /root/vmcore.dumpfile
CPUS: 1
DATE: Mon Nov 26 04:15:49 2007
UPTIME: 00:17:22
LOAD AVERAGE: 0.82, 1.02, 0.87
TASKS: 63
...
PANIC: "Oops: 0000 [#1]" (check log for details)
crash>
```

### 检查堆栈跟踪

检查堆栈跟踪以了解崩溃的原因：

```bash
crash> bt
PID: 0     TASK: c03a32e0  CPU: 0   COMMAND: "swapper"
#0 [c0431eb8] crash_kexec at c013a8e7
#1 [c0431f04] die at c0103a73
#2 [c0431f44] do_page_fault at c0343381
#3 [c0431f84] error_code (via page_fault) at c010312d
    EAX: 00000008 EBX: c59a5360 ECX: c03fbf90 EDX: 00000000
    EBP: 00000000
    DS: 007b    ESI: 00000000  ES: 007b    EDI: c03fbf90
    CS: 0060    EIP: f8a8c004  ERR: fffffff EF LAGS: 00010092
#4 [c0431fb8] rtc_interrupt at f8a8c004
#5 [c0431fc4] handle_IRQ_event at c013de51
#6 [c0431fdc] __do_IRQ at c013df0d
```

堆栈跟踪将嫌疑指向 `rtc_interrupt()`。让我们反汇编 `rtc_interrupt()` 附近的指令：

```bash
crash> dis 0xf8a8c000 5
0xf8a8c000 <rtc_interrupt>:    push    %ebx
0xf8a8c001 <rtc_interrupt+1>: sub     $0x4,%esp
0xf8a8c004 <rtc_interrupt+4>: mov     0xff,%eax
0xf8a8c009 <rtc_interrupt+9>: mov     $0xc03a6640,%eax
0xf8a8c00e <rtc_interrupt+14>: call   0xc0342300 <_spin_lock>
```

地址 `0xf8a8c004` 处的指令试图将 `EAX` 寄存器的内容移动到地址 `0xff`，这显然是导致崩溃的无效引用错误。修复此问题并构建新的内核。

如果使用 `irq` 命令，你可以确定在崩溃时刻正在进行的中断身份。在这种情况下，输出确认 RTC 中断确实处于活动状态：

```bash
crash> irq
IRQ: 8
STATUS: 1 (IRQ_INPROGRESS)
...
handler:  f8a8c000  <rtc_interrupt>
           flags: 20000000  (SA_INTERRUPT)
           mask: 0
           name: f8a8c29d  "rtc"
crash> quit
bash>
```

### 内核挂起而非 Oops 的情况

让我们换个角度，看看内核挂起而不是产生“oops”的情况。考虑以下有 bug 的驱动程序 `init()` 例程：

```c
static int __init
mydrv_init(void)
{
    spin_lock(&mydrv_wq.lock);   /* Usage before initialization! */
    spin_lock_init(&mydrv_wq.lock);
    /* ... */
}
```

该代码错误地在初始化之前使用了自旋锁。实际上，CPU 会一直旋转以尝试获取锁，内核似乎挂起了。让我们使用 kdump 来调试这个问题。在这种情况下，由于没有恐慌，不会自动触发，因此通过按下魔术 Sysrq 组合键 Alt-Sysrq-c 来强制产生崩溃转储。你可能需要向 `/proc/sys/kernel/sysrq` 写入 1 来启用 Sysrq：

```bash
bash> echo 1 > /proc/sys/kernel/sysrq
bash> insmod mydrv.ko
```

这会导致内核在 `mydrv_init()` 内部挂起。按下 Alt-Sysrq-c 组合键以触发崩溃转储：

```text
Alt-Sysrq-c
...
→ Messages announcing that a crash dump
has been triggered
```

在 kexec 启动捕获内核后将转储保存到磁盘，引导回原始内核，并在保存的转储上运行 `crash`：

```bash
bash> crash vmlinux vmcore.dump
...
PANIC: "SysRq : Trigger a crashdump"
PID: 2115
COMMAND: "insmod"
  TASK: f7e57000  [THREAD_INFO: f6170000]
CPU: 0
STATE: TASK_RUNNING (SYSRQ)
crash>
```

通过检查在崩溃时刻正在运行的进程身份来试探一下。在这种情况下，它是显然是在 `insmod` `mydrv.ko` 时：

```
crash> ps
**
  2171    2137     0 f6bb7000  IN  0.5  11728  5352  emacs-x
  2214       1     0 f6b5b000  IN  0.1  2732   1192  login
  2230    2214     0 f6bb0550  IN  0.1  4580   1528  bash
> 2261    2230     0 c596f550  RU  0.0  1572    376  insmod
```

堆栈跟踪除了告诉你 Sysrq 按键操作导致了转储外，没有提供更多有用信息：

```
crash> bt
PID: 2115  TASK: f7c57000  CPU: 0   COMMAND: "insmod"
 #0 [c0431e88] crash_kexec at c013a8e7
 #1 [c0431eb4] __handle_sysrq at c0254664
 #2 [c0431edc] handle_sysrq at c0254713
```

接下来，让我们尝试查看崩溃内核生成的日志消息。`log` 命令从转储文件中的内核 `printk` 环形缓冲区读取消息：

```
crash> log
**
BUG: soft lockup detected on CPU#0!
Pid: 2261, comm:    		insmod
EIP: 0060: [<c010eclb>]  CPU: 0
EIP is at delay_pmtmr+0xb/0x20
EFLAGS: 00000246	Tainted: P		(2.6.16.16 #11)
EAX: 5caaa48c EBX: 00000001 ECX: 5caaa459 EDX: 00000012
ESI: 02e169c9 EDI: 00000000 EBP: 00000001 DS: 007b ES: 007b
CR0: 8005003b CR2: 08062017 CR3: 35e89000 CR4: 000006d0
[<c01fede9>] __delay+0x9/0x10
[<c0200089>] __raw_spin_lock+0xa9/0x150
[<f893d00d>] mydrv_init+0xd/0xb2 [wgdrv]
```
