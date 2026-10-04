并行处理这两条指令。很明显，此时编译器不能找到更好的并行处理手段，无法有效地利用CPU，所以在此添加了2个停止位和多个NOP指令。虽然编译器在智能方面远不够成熟，但是人工的IA64汇编编程也毫不轻松；程序员要手动完成指令字符分组的工作。

要省事的话，程序员可以给每条指令添加停止位，不过这将大幅度浪费安处理器的运算性能。

Linux内核的代码中，就有一些经典的、手写IA64汇编代码。感兴趣的读者可参考：http://lxr.free-electrons.com/source/arch/ia64/lib/

+   有关IA64汇编语言编程的具体方法，可以参见Mike Burrell撰写的专业论著《Writing Efficient Itanium 2 Assembly Code》(http://phrack.org/issues/57/5.html