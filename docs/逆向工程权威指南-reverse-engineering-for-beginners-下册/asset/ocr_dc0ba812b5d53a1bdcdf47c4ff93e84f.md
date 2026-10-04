[1] 即 syntactic sugar，指增强代码可读性，降低编程错误率的语法改进措施。

[2] MSVC编译器在处理线程内的局部变量时，按照其需要，可能给这些内部变量分配以tv开头的宏变量。

[3] https://en.wikipedia.org/wiki/Setjmp.h。

[4] 这个名称来自于Fortran早期的GOTO算法。虽然现在保留了这个名字，但是已经和那个概念没什么关系了。详情请参见 http://en.wikipedia.org/wiki/Branch_table。

[5] OllyDbg用画线的格式显示这些值，因为它们也是FIXUPS。本书的68.2.6节会进行详细的解释。

[6] 虽然pipeline三级流水的解释较为直观，但是官方手册《ARM architecture reference manual》第1章2节否定了这种硬件上的联系，它把PC与指令间的opcode的关系的关系解释为历史原因。