
到该区域的 RAM 中，并从此处执行。这样做的原因是性能：从 RAM 进行的原始读取速度比从 Flash 读取快一个数量级（甚至更多）。然而，对于 4xx CPU，还有一个更微妙的原因来启用指令缓存，我们将很快就会发现。

## 7.4.4 板级特定初始化

任何板级特定初始化的第一次机会出现在 `.../cpu/ppc4xx/start.S` 中，就在可缓存区域初始化完成之后。在这里，我们找到了对外部汇编语言例程 `ext_bus_cntrlr_init` 的调用。

```assembly
bl ext_bus_cntrlr_init /* 板级特定总线控制器初始化 */
```

该例程定义在 `.../board/ep405/init.S` 中，位于针对您主板的新板级特定目录中。它提供了早期基于硬件的初始化的钩子。这是为我们 EP405 平台定制的文件之一。此文件包含用于初始化 405GP 外部总线控制器以适用于我们应用的板级特定代码。列表 7-7 包含了该文件功能的核心部分。这是初始化 405GP 外部总线控制器的代码。

### 列表 7-7

外部总线控制器初始化

```assembly
.globl ext_bus_cntrlr_init
ext_bus_cntrlr_init:
	mflr		r4		/* 保存链接寄存器	*/
	bl		..getAddr
..getAddr:
	mflr		r3		/* 获取 _this_ 地址	*/
	mtlr		r4		/* 恢复链接寄存器	*/
	addi	r4,0,14	/* 预取 14 个缓存行... */
	mctr r4		/* ...以容纳此函数	*/
				/* 缓存 (8xI4=12 条指令)	*/
..ebcloop:
	icbm	r0, r3	/* 预取 [r3] 的缓存行 */
	addi	r3, r3,32	/* 移动到下一个缓存行	*/
	bdnz	..ebcloop	/* 继续执行 14 个缓存行 */
	
/*-------------------------------------------*/
/* 延迟以确保对 ROM 的所有访问完成 */
/* 在更改 bank 0 时序之前			*/
/* 200微秒应该足够了				*/
/* 200,000,000 (cycles/sec) x .000200 (sec) = */
/* 0x9C40 个周期 */
/*----*----*----*----*----*----*----*----*----*----*----*----*----*----*/
addis r3,0,0x9C40
ori r3,r3,0x0000 /* 确保 200微秒已经过 */
mtctr r3

...spinl: ...
spinl: bdnz .spinlp /* 自旋循环 */

/* 现在执行此函数的实际工作 */
/* 内存 Bank 0 (Flash 和 SRAM) 初始化 */

addi r4,0,pb0ap /* *ebcfga = pb0ap; */
mtdcr ebcfga,r4
addis r4,0,EBC0_B0AP0h /* *ebcfgd = EBC0_B0AP; */
ori r4,r4,EBC0_B0AP0l
mtdcr ebcfgd,r4

addi r4,0,pb0cr /* *ebcfga = pb0cr; */
mtdcr ebcfga,r4
addis r4,0,EBC0_B0CR0h /* *ebcfgd = EBC0_B0CR; */
ori r4,r4,EBC0_B0CR0l
mtdcr ebcfgd,r4

/* 内存 Bank 4 (NVBRAM & BCSR) 初始化 */

addi r4,0,pb4ap /* *ebcfga = pb4ap; */
mtdcr ebcfga,r4
addis r4,0,EBC0_B4AP0h /* *ebcfgd = EBC0_B4AP; */
ori r4,r4,EBC0_B4AP0l
mtdcr ebcfgd,r4

addi r4,0,pb4cr /* *ebcfga = pb4cr; */
mtdcr ebcfga,r4
addis r4,0,EBC0_B4CR0h /* *ebcfgd = EBC0_B4CR; */
ori r4,r4,EBC0_B4CR0l
mtdcr ebcfgd,r4

blr /* 返回 */
```

选择列表 7-7 中的示例是因为它典型地展示了底层处理器初始化中涉及的微妙复杂性。重要的是要意识到这段代码运行的上下文。它从 Flash 执行，此时任何 DRAM 都尚不可用。没有栈。这段代码正准备对控制其对本身正在执行的 Flash 访问的控制器进行根本性的修改。对于该特定处理器，有充分的文档记录表明，在修改 Flash 所连接的外部总线控制器时，从 Flash 执行代码可能会导致错误的读取，进而导致处理器崩溃。

解决方案显示在这个汇编语言例程中。从标签 `..getAddr` 开始，接下来的七条汇编语言指令，代码基本上使用 `icbi` 指令将自身预取到指令缓存中。当整个子程序成功读取到指令缓存中后，它就可以继续对外部总线控制器进行必要的更改，而不用担心崩溃，因为它正在直接从内部指令缓存执行。虽然微妙，但很巧妙！随后是一个短暂的延迟，以确保所有请求的指令缓存读取已完成。

当预取和延迟完成后，代码继续配置内存 Bank 0 和内存 Bank 4 以适配我们的主板。这些值来自对底层组件及其在主板上互连方式的详细知识。感兴趣的读者可以查阅本章末尾的“延伸阅读建议”，以获取 PowerPC 汇编器和 405GP 处理器的所有细节，本示例即由此衍生。

请考虑在不完全理解这里正在发生什么的情况下修改此代码。也许你添加了几行代码，使其大小超出了预取到缓存的范围。它很可能会崩溃（更糟糕的是，它可能偶尔才崩溃），但使用调试器逐步执行此代码不会提供任何关于原因的线索。

板级特定初始化的下一个机会是在从处理器的数据缓存中分配临时栈之后。这是在 `.../cpu/ppc44x/start.S` 大约第 727 行分支去初始化 SDRAM 控制器的地方：`bl sdr_init`。

执行上下文现在包括一个栈指针和一些用于本地数据存储的临时内存——也就是说，一个部分 C 上下文，允许开发者使用 C 语言来完成设置系统 SDRAM 控制器和其他初始化任务等相对复杂的任务。在我们的 EP405 移植中，`sdr_init()` 代码位于 `.../board/ep405/ep405.c`，并针对此特定主板和 DRAM 配置进行了定制。由于该主板没有使用市售的内存 SIMM，因此无法动态确定 DRAM 的配置，而 U-Boot 支持的其他许多主板是可以动态确定的。它是硬编码在 `ddram_size` 中的。

许多现成的内存 DDR 模块都有一个 SPD (Serial Presence Detect) PROM，其中包含定义内存模块参数的参数。这些参数可以通过 I2C 在程序控制下读取，并用作确定内存控制器正确参数的输入。U-Boot 支持此技术，但可能需要修改才能适用于你的特定主板。在 U-Boot 源代码中可以看到其许多使用示例。配置选项 `CONFIG_SPD_EFFRONT` 启用了此功能。你可以 grep 此选项以查找其使用示例。

## 7.4.5 移植总结

至此，你可以体会到将引导程序移植到硬件平台的一些困难。对于底层硬件的详细知识是无可替代的。当然，我们希望尽量减少为此任务所需的时间投入。毕竟，我们通常不是根据我们对给定处理器每个硬件细节的理解程度来支付报酬的，而是根据我们按时提供可行解决方案的能力。事实上，这是开源蓬勃发展的主要原因之一。我们刚才看到了将 U-Boot 移植到新硬件平台是多么容易——不是因为我们是对该处理器世界级的专家，而是因为在此之前，许多人已经完成了大部分艰苦的工作。

列表 7-8 是完成 U-Boot EP405 基本移植的新文件或修改文件的完整列表。当然，如果存在 U-Boot 中没有支持的新硬件设备，或者我们移植到一个 U-Boot 尚未支持的新 CPU，那么这将是一个更大规模的工作。这里要强调的一点，尽管有重复之嫌，是对于硬件（CPU 和子系统）和底层软件（U-Boot）的详细知识是无可替代的，才能在合理的时间内成功完成移植。如果你带着这种心态开始项目，你将获得成功的结果。

### 列表 7-8

U-Boot EP405 移植的新 diff 或更改的文件

```bash
$ diff -purN u-boot u-boot-ep405/ | grep +++
+++ u-boot-ep405/board/ep405/config.mk
+++ u-boot-ep405/board/ep405/ep405.c
+++ u-boot-ep405/board/ep405/ep405.h
+++ u-boot-ep405/board/ep405/flash.c
+++ u-boot-ep405/board/ep405/init.S
+++ u-boot-ep405/board/ep405/Makefile
+++ u-boot-ep405/board/ep405/u-boot.lds
+++ u-boot-ep405/include/config.h
+++ u-boot-ep405/include/config.mk
+++ u-boot-ep405/include/configs/EP405.h
+++ u-boot-ep405/include/configs/ppc405.h
+++ u-boot-ep405/Makefile
```

请记住，`.../board/ep405` 目录中的所有文件都是从另一个目录衍生而来的。确实，在这次移植中，我们没有任何从零开始创建的文件。我们借鉴了前人的工作，并在必要时进行定制以实现我们的目标。

## 7.4.6 U-Boot 镜像格式

现在，我们已经有了适用于 EP405 主板的可用引导程序，我们可以在上面加载和运行程序。理想情况下，我们希望运行 Linux 等操作系统。为此，我们需要理解 U-Boot 所需的镜像格式。U-Boot 期望在镜像文件上有一个小标题，用于标识镜像的几个属性。U-Boot 使用 `mkimage` 工具（U-Boot 源代码的一部分）来构建此镜像标题。

最近的 Linux 内核发行版内置支持直接构建可由 U-Boot 启动的镜像。内核源代码树的 ARM 和 PPC 分支都支持一个名为 `uImage` 的目标。让我们看看 PPC 的情况。以下 Linux 内核 PPC makefile `.../arch/ppc/boot/images/Makefile` 中的片段包含构建名为 `uImage` 的 U-Boot 目标的规则：

```makefile
quiet_cmd_uimage = UIMAGE $@
cmd_uimage = $(CONFIG_SHELL) $(MKIMAGE) -A ppc \
	-O linux -T kernel -C gzip -a 00000000 -e 00000000 \
	-n 'Linux-S$(KERNELRELEASE)' -d $^ $@
```
