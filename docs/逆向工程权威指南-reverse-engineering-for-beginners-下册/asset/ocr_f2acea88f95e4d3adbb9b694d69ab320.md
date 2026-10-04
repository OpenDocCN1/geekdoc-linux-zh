CS/DS/ES代表Code Segment代码寄存器、Data Segment数据寄存器、Stack Segment堆栈寄存器和Extra Segment附加寄存器。

在Win32系统里，FS附加寄存器（Extra Segment Register）承担TLS（线程本地存储/Thread Local Storage）的角色；而在Linux系统里，GS（另一个附加寄存器）承担了这个角色。早期，这两个寄存器用于实现段式寻址；现在，它们用于提供更为快速的TLS和TIB（线程信息块/ThreadInformationBlock）功能。有关段地地址寄存器的详细介绍，请参见本书第94章。

# A. 2.19 标识寄存器

标识寄存器即Eflags。

| Bit位（及编码） | 写入（及含义） | 描述 |
|---|---|--|
| 0（1） | CF（进/借位） | 除了了常规计算指令之外，专门操作CF的指令还有CLC/STC/CMC |
| 2（4） | PF（奇偶标识位） | 参见17.7.1节 |
| 4（0x10） | AF（辅助进/借位标识） | |