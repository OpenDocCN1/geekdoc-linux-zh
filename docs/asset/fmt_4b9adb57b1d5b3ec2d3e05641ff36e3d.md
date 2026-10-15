
| 0000000 <init_module> | sub | $0x8,ebp |
| :--- | :--- | :--- |
| 0: | 83 c8 | |
| 3: | 74 24 04 00 | mov | $0x0,04(ebp) |
| b: | 74 24 04 00 | mov | $0x2,(ebp) |
| e2: | 88 fc ff ff | call | 13 <init_module+0x13> |
| 17: | a1 00 00 00 | mov | $0x0,(ebp) |
| c2: | 74 24 04 00 | mov | $0x2,(ebp) |
| 29: | 89 44 24 00 | mov | eax,04(ebp) |
| 27: | 88 c8 ff ff | call | 25 <init_module+0x28> |
| 2c: | 31 c0 | xor | eax, eax |
| 31: | 83 c8 00 | add | $0x8,ebp |

* 在 `http://www.kernelloops.org` 维护着当前 oops 的数据库，并帮助内核开发人员成功调试。

section_exit 节的反汇编。

这是一个简单的模块（`crashit.c`），它包含一个空指针解引用，这可以触发 oops 消息：

| 0000000 <linux_module> | sub | $0x8,ebp |
| :--- | :--- | :--- |
| 0: | 83 c8 | |
| 3: | 74 24 04 00 | mov | $0x0,04(ebp) |
| b: | 74 24 04 00 | mov | $0x2,(ebp) |
| e2: | 88 fc ff ff | call | 13 <linux_module+0x13> |
| la: | 83 c8 00 | add | $0x8,ebp |

```c
#include <linux/module.h>
#include <linux/init.h>
static int __init init_module(void)
{
    int *i;
    i = 0;
    printk(KERN_INFO "Hello: module is loaded at 0x%p\n", (void *)i);
    init_module;
    printk(KERN_INFO "Hello: module loaded at 0x%p\n", (void *)i);
    return 0;
}
```

我们通过尝试加载 `crashit` 产生了一个 oops；它在初始化步骤挂起，并产生了以下 oops 消息（该消息会被追加到 `/var/log/messages`）：

```text
Hello: init_module loaded at address 0xf81f7000
kernel NULL pointer dereference at virtual address 00000000
```

```c
static void __exit exit_module(void)
{
    printk(KERN_INFO "Hello: module unloaded at 0x%p\n", (void *)0);
    cleanup_module;
}
```

```text
printing_exit:
fs0073
* = = NULL dereference
Oops: 001 [#1]
PHB00
Module linked in crashit: w93b627f emros lm 15 sensor_i2c_inaec1c, vispro_dev_i2c_dev_i2c_core spi_busif spi_master_ubci_ecdi
```

## 10.2. 内核调试器

```text
snd_x86_sdx_snd_codec_snd_pcm_oss_snd_mixer_oss_snd_timer
snd_page_alloc_snd_v3601_uart_snd_rawimidi_dev_snd_soundcard
flappy_floppy_prata_via_libata
```

### kdb

`kdb` 是一个交互式内核调试器。

### kgdb

`kgdb` 是另一个内核调试器。它需要两台计算机通过串口线连接。

### gdb

`gdb` 调试器可以调试运行中的内核。

### crash

`crash` 工具由你的 Linux 发行版提供。

# 第 10 章 调试技术

## 10.4. KPROBES 和 JPROBES

- 预处理器（pre-handler）在探针指令执行之前被调用。
- 后处理器（post-handler）在探针指令执行后被调用，前提是没有产生异常。
- 故障处理器（fault-handler）在探针指令产生异常时被调用。
- 断点处理器（break-handler）在探针指令被单步执行或设置断点时被调用。

基础函数和数据结构定义在 `/usr/src/include/linux/kprobes.h` 和 `/usr/src/kernel/kprobes.c`。

```c
#include <kprobes.h>
```

```c
int register_kprobe(struct kprobe *kp);
void unregister_kprobe(struct kprobe *kp);
struct kprobe {
    struct list_head list;
    /* 探点位置 */
    kprobe_opcode *addr;
    /* 允许指示探点的符号名称 */
    char *symbol_name;
    /* 符号偏移量 */
    unsigned offset;
    /* 在 addr 执行前调用 */
    kprobe_pre_handler *pre_handler;
    /* 在 addr 执行后调用，除非... */
    kprobe_post_handler *post_handler;
    /* 如果执行 addr 导致故障（例如页错误） */
    // 如果失败则返回 1，否则内核将看到它：
    kprobe_fault_handler *fault_handler;
    /* 如果在探针处理器中发生断点陷获 */
    // 如果通过断点则返回 1，否则内核将看到它：
    kprobe_break_handler *break_handler;
    /* 保存的操作码（已替换为断点） */
    kprobe_opcode opcode;
    /* 原始指令的副本 */
    struct spec_info original_ins;
    /* 函数，及其参数 */
    typedef int (*kprobe_pre_handler_t)(struct kprobe *kp, struct pt_regs *regs);
    typedef int (*kprobe_post_handler_t)(struct kprobe *kp, struct pt_regs *regs);
    typedef int (*kprobe_fault_handler_t)(struct kprobe *kp, struct pt_regs *regs, unsigned long flags);
    typedef int (*kprobe_break_handler_t)();
```

注意，处理器函数接收一个指向 `pt_regs` 数据结构的指针，该结构包含寄存器的内容。这取决于架构，详细信息见 `/usr/src/arch/x86/include/ptrace.h`。

传递处理器的 `flags` 参数目前未使用，而处理器的 `trap` 参数给出了导致故障的类型。

为了使用 kprobes，必须：

- 填充 `kprobe` 数据结构中的指针，指向所提供的处理器函数。
- 提供要插入探点的地址 (`addr`) 或符号名称（带有可选偏移量的 `symbol_name`）。
- 调用 `register_kprobe()`，返回值为 0 表示插入成功。

完成后使用 `unregister_kprobe()`，如果忘记这样做将导致显而易见的灾难性后果。

唯一剩余的目标是获取探针指令的插入。如果符号是导出的，你就可以向其打印操作码，如下：

```c
kp->addr = (struct kprobe_opcode_t *)mod_timer;
```

即使符号没有导出，你也可以指定如下简单的名称：

```c
kp->symbol_name = "do_fork";
```
