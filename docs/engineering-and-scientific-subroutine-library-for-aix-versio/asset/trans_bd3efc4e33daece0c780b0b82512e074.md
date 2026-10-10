

# 术语表

本术语表定义了本出版物中使用的术语和缩写。如果您未找到所需的术语，请参阅本书的索引部分。本术语表包含以下来源的术语和定义：

- *IBM Dictionary of Computing*，纽约：McGraw Hill (1-800-2MC-GRAW)，1994年。
- *American National Standard Dictionary for Information Systems*，ANSI X3.172-1990，版权所有1990年美国国家标准学会（ANSI）。可从位于纽约州纽约市西42街11号（邮编10036）的美国国家标准学会购买副本。定义后带有符号 (A) 表示该定义来自此标准。
- *Information Technology Vocabulary*，由国际标准化组织（ISO）和国际电工委员会（IEC）联合技术委员会第1分委员会（ISO/IEC JTC1/SC1）开发。这些词汇表已发布章节中的定义，在定义后带有符号 (I) 进行标识。取自 ISO/IEC JTC1/SC1 正在制定的国际草案标准、委员会草案和工作文件的定义，在定义后带有符号 (T) 进行标识，表明 SC1 的参与国家机构尚未就最终协议达成一致。

**APAR。** 授权程序分析报告（Authorized Program Analysis Report）。针对当前未发布版本中的疑似缺陷所导致问题的报告。

**argument。** 在调用程序与子程序（SUBROUTINE）、函数（FUNCTION）子程序或语句函数之间传递的参数。

**array。** 由单个名称标识的有序数据项集合。

**array element。** 数组中的数据项，通过数组名后跟一个指示其在数组中位置的脚本（下标）来标识。

**array name。** 组成数组的有序数据项集合的名称。

**assignment statement。** 将值分配给变量或数组元素的语句。它由一个变量或数组元素组成，后跟一个等号 ( = )，再后跟一个表达式。该变量、数组元素或表达式可以是字符型、逻辑型或算术型。当处理赋值语句时，等号右侧的表达式会替换等号左侧变量或数组元素的值。

**Basic Linear Algebra Subprograms (BLAS)。** 一组标准的、公域的数学子例程，用于执行线性代数操作。

**BLAS。** 基础线性代数子例程（Basic Linear Algebra Subprograms）。

**cache。** 一种专用缓冲存储，比主存储器更小、更快，用于保存从主存储器获取的指令和数据的副本，这些数据很可能接下来会被处理器使用。(T)

**character constant。** 由一个或多个字母数字字符组成的字符串，用撇号括起来。分隔用的撇号不是常量值的一部分。

**character expression。** 形式为单个字符常量、变量、数组元素、子字符串、函数引用或括号包围的其它表达式的表达式。字符表达式的类型始终是字符型。

**character type。** 用于表示字母数字字符字符串的数据类型；在存储中，每个字符使用一个字节。

**column-major order。** 一种用于存储多维数组的顺序方法，依据数组元素的脚本（下标）进行排序。在此方法中，最左侧的脚本位置变化最快，并在右侧下一个脚本位置递增之前完成一个完整周期。

**complex conjugate even data。** 实部为偶函数且虚部为奇函数的复数数据。

**complex constant。** 由逗号分隔并用括号括起来的有序实数或整数常数组。该常数组中的第一个实数是复数的实部；第二个是虚部。

**complex type。** 用于表示复数数值近似的近似值的数据类型。该类型的数据项由逗号分隔并用括号括起来的有序实数数据对组成。第一个项表示复数的实部；第二个项表示虚部。

**constant。** 不变的量。常量的四个类别指定了数字（算术型）、真值（逻辑型）、字符数据（字符型）和十六进制数据。

**data type。** 数据可能被编程语言直接指定的结构特征、特性和属性；例如，Fortran 中的整数、实数；APL 中的数组；LISP 中的链接列表；SNOBOL 中的字符串。

**decoration。** 形成包含另一个序列中每个 *n* 个元素之一的序列的过程。

**dimension of an array。** 数组脚本（下标）中的一个脚本表达式位置。在 Fortran 中，数组可以有一到七个维度。图形上，第一维度由行表示，第二维度由列表示，第三维度由平面表示。与秩（rank）对比。另见维度的范围（extent of a dimension）。

**direct access storage。** 一种存储设备，其访问时间实际上独立于数据的位置。(A)

**divide-by-zero exception。** 处理器识别的一种条件，由试图除以零的程序运行导致。

**double precision。** 长精度的同义词。

**expression。** 表示值的符号：单独出现的基本量（primary），或基本量和运算符的组合。表达式可以是算术型、字符型、逻辑型或关系型。

**extent of a dimension。** 用于数组脚本中特定维度的脚本表达式可表示的不同整数值数量。

**external function。** 在引用它的程序单元外部定义的函数。它可以在过程子程序或主程序中引用，但不能直接或间接引用自身。与语句函数（statement function）对比。

**function。** 在 Fortran 中，通过在表达式中引用而被调用的过程，并向该表达式提供值。提供的值即为该函数的值。另见外部函数（external function）、内部函数（intrinsic function）和语句函数（statement function）。与子例程（subroutine）对比。

**function reference。** Fortran 源程序对内部函数、外部函数或语句函数的引用。

**general matrix。** 不具有对称性等假设特殊属性的矩阵。矩阵（matrix）的同义词。

**integer constant。** 由不含小数点的十进制数字组成的字符串，表示一个整数。

**integer expression。** 值为整数类型的算术表达式。

**integer type。** 能够表示整数值 的算术数据类型。它可以具有正值、负值或 0 值。它不得包含小数点。

**intrinsic function。** 由 Fortran 提供的，执行数学或字符操作的函数。

**leading dimension。** 对于二维数组，一个增量，用于找到数组中每一成功列中矩阵元素的起始点。

**logical constant。** 可以具有两个值之一的常量：真或假。这些值在 Fortran 中的形式分别为：.TRUE. 和 .FALSE.。

**logical expression。** 单独的逻辑基本量，或逻辑基本量和逻辑运算符的组合。逻辑表达式可以具有两个值之一：真或假。

**logical type。** 数据项类型为真或假，且可对其执行 .NOT. 和 .OR. 等逻辑操作的数据类型。另见“数据类型”（data type）。

**long-precision。** 长度为 8 的实数数据类型。与单精度（single precision）和短精度（short-precision）对比。

**main program。** 在 Fortran 中，一个用于运行的程序单元，它可以调用其他程序单元，但不能被它们调用。

**mask。** 使用字符模式来控制另一个字符模式部分保留或消除的操作。(I)

**matrix。** 按行列排列的元素矩形数组，可根据矩阵代数规则进行操作。(A) (I)

**multithreaded。** 进程中可能存在一个或多个线程，且每个线程由操作系统并发执行。如果一个应用程序并发执行多个线程，则它是多线程的。

**overflow exception。** 由算术操作结果的大小超出最大可能数值而导致的条件。

**platform。** 大型机或工作站。

**primary。** 不可再分的数据单位；单个常量、变量、数组元素、函数引用或括号包围的表达式。

