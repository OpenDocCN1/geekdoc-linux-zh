
```c
}

/* Post Handler: Invoked after running probed instruction */

void bandaid_post(struct kprobe *p, struct pt_regs *regs,
                    unsigned long flags)
{
    /* Nothing to do */
}

/* Fault Handler: Invoked if the pre/post-handlers encounter a fault */

int bandaid_fault(struct kprobe *p, struct pt_regs *regs,
                   int trapnr)
{
    return 0;
}

int init_module(void)
{
    int retval;
    /* Fill the kprobe structure */
    bandaid.pre_handler = bandaid_pre;
    bandaid.post_handler = bandaid_post;
    bandaid.fault_handler = bandaid_fault;
    /* Arrive at the target address as explained */
    bandaid.addr = (kprobe_opcode_t*)
                   kallsyms_lookup_name("memwalkd") + 0xaa;
    if (!bandaid.addr) {
        printk("Bad Probe Point\n");
        return -1;
    }
    /* Register the kprobe */
    if ((retval = register_kprobe(&bandaid)) < 0) {
        printk("register_kprobe error, return value=%d\n", retval);
        return -1;
    }
    return 0;
}

void module_cleanup(void)
{
    unregister_kprobe(&bandaid);
}

MODULE_LICENSE("GPL"); /* You can't link the Kprobes API unless your user module is GPL'ed */
```

### 清单 21.3 使用 Kprobes 在 `kallsyms_lookup_name("memwalkd") + 0xaa` 处插入一个补丁，将页面数限制为 10

要弄清楚如何到达这个探针地址，请再次查看清单 21.2。你希望补丁插入在 B 点。为了计算 B 点处的内核地址，请使用 `objdump` 反汇编 `mydrv.ko` 的内容：

**`bash> objdump -D mydrv.ko`**

```
mydrv.ko: 	 file format elf32-i386
Disassembly of section .text:
00000000 <memwalkkd>:
    0:	55 			 	push	%ebp
    1:	bd 00 40 00 00 	mov	$0x4000,%ebp
    6:	57 			 	push	%edi
    7:	56 			 	push	%esi
    8:	53 			 	push	%ebx
    9:	bb 00 f0 ff ff 	mov	$0xffff000,%ebx
    e:	81 ec 90 00 00 00 	sub	$0x90,%esp
   ... 
   ... 
   7a:	83 f8 0a 		 	cmp	$0xa,%eax 	--> Point A
   7d:	74 2b 		 	je	<memwalkkd+0xaa>
   7f:	83 f8 09 		 	cmp	$0x9,%eax
   82:	75 cc 		 	jne	50 <memwalkkd+0x50>
   ...
  a9:	c3 ret
  aa:	a1 00 00 00 00 		mov	0x0,%eax 	--> Point B
  af:	85 c0 		 	test	%eax,%eax
  b1:	0f 8e b5 00 00 00 	jle	16c <memwalkkd+0x16c>
  b7:	81 fd 7b f6 00 00 	cmp	$0xf67b,%ebp
   ...
  fa:	a1 00 00 00 00 		mov	0x0,%eax
```

如果你正在为不同的处理器平台进行交叉编译，必须使用特定于架构的 `objdump`。如果你正在反汇编一个为基于 ARM 的目标设备交叉编译的二进制文件，你将需要诸如 `arm-linux-objdump` 之类的工具。向 `objdump` 传递 `-S` 选项，可以将源代码与反汇编输出混合显示：

**`bash> arm-linux-objdump -d -S mydrv.ko`**

如果你尝试将清单 21.2 中的 C 代码与上述反汇编转储进行匹配，你可以将 A 点和 B 点与所示的内核地址关联起来。`kallsyms_lookup_name()`[6] 定位 `memwalkkd()` 的地址，而 `0xaa` 是 B 点所在的偏移量，因此在 `kallsyms_lookup_name("memwalkkd") + 0xaa` 处应用 `kprobe`。

> [6] 为了获取此函数的服务，你必须在内核配置期间启用 `CONFIG_KALLSYMS`。

注册 `kprobe` 后，`memwalkkd()` 等效于看起来像这样：

```c
static int memwalkd(void *unused)
{
/* ... */
for (...) {
/* ... */
/* Point A */
/* Free npages pages when SIGUSR1 is received */
if (sig == SIGUSR1) {
/* Point B */
if (npages > 10) npages = 10; /* The medicated patch! */
for (i=0; i < npages; i++, curr_pfn++) {
/* ... */
}
}
/* ... */
}
/* ... */
}
```

每当 `npages` 被分配一个大于 10 的值时，被探测的补丁会将其拉回 10，从而绕过该问题。

在接下来的两节中，让我们看看一些辅助设施，它们使在函数入口和出口期间使用 Kprobes 变得更加容易。

### Jprobes

*Jprobe* 是一种专门化的 `kprobe`。当调查点位于内核函数的入口处时，它简化了添加探针的工作。`Jprobe` 处理器与被探测函数具有相同原型。它使用与被探测函数相同的参数列表调用，因此你可以轻松地 `Jprobe` 处理器中访问函数参数。如果你使用 Kprobes 而不是 Jprobes，想象一下你的探针处理器需要经历的麻烦，要在函数堆栈的黑暗小巷中摸索以提取函数参数！而且这种深入堆栈以诱导参数值的代码必须高度特定于函数，更不用说它是架构依赖且不可移植的。

要了解如何使用 Jprobes，让我们回到一个示例。假设你正在通过查看其生成的 `printk()` 消息来调试一个网络设备驱动程序（该驱动程序作为内核的一部分构建）。驱动程序以八进制（基数 8）输出关键值，但令你惊恐的是，驱动程序编写者在打印格式字符串中引入了一个拼写错误，编码为 `%o` 而不是 `%o`（注：原文此处两个都是 `%o`，语境意指八进制八位格式与十六进制格式混淆或类似错误，此处直译原文描述）。因此，你所能看到的消息如下：

Number of Free Receive buffers = `$0.`

Jprobes 来救命了。你可以在几秒钟内修复这个问题，无需重新编译或重启内核。首先，查看在 `kernel/printk.c` 中定义的 `printk()`：

```c
asmlinkage int printk(const char *fmt, ...)
{
va_list args;
int r;
va_start(args, fmt);
r = vprintk(fmt, args);
va_end(args);
```

```c
    return r;
}
```
