
## 附录 B • AIX 到 Linux 引用表

| C/C++ VisualAge for AIX 选项 | GNU gcc 选项 | 说明 (基于 AIX) |
| --- | --- | --- |
| `-qignerrno` | None | 假设 `errno` 不会被系统调用修改。 |
| `-qignprag` | None | 指编译器忽略 `pragma` 语句。 |
| `-qinfo` | None | 生成信息消息。 |
| `-qinauto` | None | 初始化自动存储的值。 |
| `-qinlue` | None | 生成调用外部函数所需的快速链接胶代码。 |
| `-qinline` | None | 尝试内联函数。 |
| `-qipa` | None | 启用或自定义名为过程间分析（intercedural analysis）的优化类。 |
| `-qisolated_call` | None | 指定源文件中具有副作用的函数。 |
| `-qkeeplinlines` | `-fkeep-inline-functions` | 指示编译器保留未引用外部函数的内联定义。 |
| `-qkeyword` | None | 控制指定的字符串被视为关键字还是标识符。 |
| `-L` | `-L` | 在指定的目录中搜索由 `-l` 指定的库文件。 |
| `-l` | `-l` | 链接时搜索指定的库。 |
| `-qlanglvl` | - | 选择编译时的 C 或 C++ 语言级别。 |
| `-qlargepage` | 参见大页支持 | 指示编译器利用运行 5.1D 或更高版本的 POWER4 系统上的大页堆。 |
| `-qldbl128 -qlongdouble` | None | 将 long double 类型的大小从 64 位增加到 128 位。 |
| `-qlibansi` | None | 假设所有与 ANSI C 库函数同名的函数都是系统函数。 |
| `-qlinedebug` | None | 为调试器生成简短的行号和源文件信息。 |
| `-qlist` | None | 生成包含对象列表的编译器列表。 |
| `-qlistopt` | None | 生成显示生效选项的编译器列表。 |
| `-qlonglit` | None | 在 64 位模式下使带有的字面量变为 long 类型。 |
| `-qlonglong` | `-mlong64`（参考目标平台的 `-m` 选项） | 允许程序中使用 long long 类型。 |

### B.1 AIX 和 Linux 编译器选项表

| C/C++ VisualAge for AIX 选项 | GNU gcc 选项 | 说明 (基于 AIX) |
| --- | --- | --- |
| `-M` | `-M` | 创建一个输出文件，其中包含的目标适用于包含在 AIX `make` 命令描述文件中。 |
| `-ma` | Refer to `alloc` | (仅限 C) 使用内联代码替换对函数 `alloca` 调用，就像在源代码中存在 `#pragma alloca` 指令一样。 |
| `-qmacptr` | None | (仅限 C) 将 Pascal 字符串字面量转换为空终止字符串，其中第一个字节包含字符串的长度。 |
| `-qmaf` | None | 指定是否生成浮点乘加法指令。 |
| `-qmakedep` | `-M` | 创建一个输出文件，其中包含的目标适用于包含在 AIX `make` 命令描述文件中。 |
| `-qmaxerr` | None | 指令编译器在达到指定数量的指定或更严重级别的错误时停止编译。 |
| `-qmaxmem` | None | 限制用于特定内存密集型优化的本地表使用的内存量。 |
| `-qmbcs`, `dbcs` | `LANG`⁵ | 如果程序包含多字节字符，请使用 `-qmbcs` 选项。 |
| `-qmkshshj` | `-shared` or `libtool`⁶ | 从生成的对象文件创建共享对象。 |
| `-qnamemangling` | None | 为从 C++ 源代码生成的外部符号选择修饰方案。 |

## 附录 B • AIX 到 Linux 参考表

| C/C++ VisualAge for AIX 选项 | GNU gcc 选项 | 说明 (基于 AIX) |
| --- | --- | --- |
| `-qoptimize` | | 在编译期间按选的级别优化代码。 |
| `-O` | `-O` | 指定由编译器或链接编辑器创建的可执行文件的输出名称或目录。 |
| `-qobjmodel` | None | (C++) 设置对象模型的类型。 |
| `-goldpassbyvalue` | None | (C++) 指定包含成员或引用成员的类如何在函数参数中传递。 |
| `-p` | `-E` | 预处理在编译器调用中命名的 C 或 C++ 源文件，并为每个输入文件创建一个输出预处理源文件。 |
| `-p` | None | 设置编译器产生的对象文件以用于性能分析。 |
| `-qpascal` | None | (仅限 C) 忽略类型规范和函数声明中的单词 `pascal`。 |
| `-qpath` | None | 构建备用程序和路径名称。 |
| `-qpdf1 -qpdf2` | None | 通过剖分析引导反馈（Profile-Directed Feedback）调整优化。 |
| `-pg` | `-fprofile-generate` | 为性能分析设置对象文件，但提供的信息比 `-p` 选项更多。 |
| `-qphsinfo` | `gcov`⁷ | 报告在每个编译阶段所需的时间。 |
| `-qprint` | None | 抑制列表输出。 |
| `-qpriority` | None | (C++) 指定静态构造函数初始化的优先级。 |

### B.1 AIX 和 Linux C 编译器选项表

| C/C++ VisualAge for AIX 选项 | GNU gcc 选项 | 说明 (基于 AIX) |
| --- | --- | --- |
| `-qproclocal` | None | 将函数标记为本地、导入或未知。 |
| `-qproimported` | | |
| `-qprocunknown` | | |
| `-qproto` | None | (仅限 C) 假设所有函数都有原型。 |
| `-Q` | `-03` | 尝试内联函数而不是生成对函数的调用。 |
| `-r` | `-mrelocatable` | 生成可重定位的对象。 |
| `-qreport` | None | 指令编译器生成转换报告，显示程序循环如何并行化和优化。 |
| `-qrndfit` | None | 控制常量浮点表达式在编译时的舍入模式。 |
| `-qrandsngl` | None | 指定每个单精度浮点操作的结果都应将结果舍入到单精度。 |
| `-qro` | None | 指定字符串字面量的存储类型。 |
| `-qcroconst` | None | 指定常量值的存储位置。 |
| `-qrrm` | None | 防止与运行时舍入到正负无穷大模式不兼容的浮点优化。 |
| `-qrtti` | None | (C++) 为 `typeid` 运算符和 `dynamic_cast` 运算符生成运行时类型识别 (RTTI) 信息。 |
| `-s` | `-s` | 为每个源文件生成汇编语言文件 (`.s`)。 |
| `-s` | None | 剥离符号表。 |
| `-qshowinc` | None | 如果与 `-source` 使用，则所有文件都包含在源列表中。 |
| `-qsmallstack` | None | 指令编译器减小栈帧的大小。 |
| `-qsmmp` | None | IBM SMP 标准程序代码的并行化。 |
| `-qsource` | None | 生成编译器列表并包含源代码。 |
| `-qspill` | None | 指定寄存器分配溢出区域的大小。 |
| `-qspnans` | None | 生成额外的指令，以检测从单精度转换为双精度过程中的信号 `NaN`。 |
| `-qsrcmsg` | None | (仅限 C) 在诊断消息中添加源行。 |
| `-qstaticinline` | None | (C++) 控制内联函数是否被视为静态。 |
| `-qstatsym` | None | 将源行添加到 `xcoff` 对象中。 |
| `-qstdinc` | `-stdinc` | 指定包含 `<include>` 的文件。 |
| `-qtemplate` | None | (C++) 添加 `#include "file_name"`。 |
| `-qstrict` | None | 关闭可能更改程序的激进优化。 |
| `-qstrict_induction` | None | 禁止更改程序的感变量。 |
