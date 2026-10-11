

## A.1 Perl 函数

### 表 A.1 Perl 函数（续）

| 函数 | 描述 |
| :--- | :--- |
| **oct** | `oct(EXPR)`<br>`oct EXPR`<br><br>返回*EXPR*的十进制值，*EXPR*为一个八进制字符串。如果*EXPR*以0x开头，则*EXPR*被解释为十六进制。如果没有*EXPR*，则转换$_。 |
| **open** | `open(FILEHANDLE, EXPR)`<br>`open(FILEHANDLE)`<br>`open FILEHANDLE`<br><br>打开一个实际的文件，*EXPR*，并将其附加到*FILEHANDLE*。如果没有*EXPR*，则必须有一个与*FILEHANDLE*同名的标量被赋予了该文件名。<br><br>- `"FILEHANDLE"`：读取<br>- `">>FILEHANDLE"`：写入<br>- `">>>FILEHANDLE"`：读/写<br>- `">>>FILEHANDLE"`：追加<br>- `"\|UNIX 命令"`：管道输出<br>- `"*UNIX 命令 \|"`：管道输入 |

| 函数 | 描述 |
| :--- | :--- |
| **pack** | `$packed=pack(TEMPLATE, LIST)`<br><br>将值列表打包为一个二进制结构并返回该结构。`TEMPLATE`是一个带引号的字符串，包含值的数量类型。`TEMPLATE`为：<br>- **a** ASCII 字符串，用 null 填充<br>- **A** ASCII 字符串，用空格填充<br>- **b** 位字符串，从低到高顺序<br>- **B** 位字符串，从高到低顺序<br>- **h** 十六进制字符串，低半字节优先<br>- **H** 十六进制字符串，高半字节优先<br>- **c** 带符号的 char 值<br>- **C** 无符号的 char 值<br>- **s** 带符号的 short 值<br>- **S** 无符号的 short 值<br>- **i** 带符号的整型值<br>- **I** 无符号的整型值<br>- **l** 带符号的 long 值<br>- **L** 无符号的 long 值<br>- **n** '网络'顺序的 short<br>- **N** '网络'顺序的 long<br>- **f** 本机格式的单精度浮点数<br>- **d** 本机格式的双精度浮点数<br>- **p** 指向字符串的指针<br>- **x** 一个 null 字节<br>- **X** 回退一个字节<br>- **@** 使用 null 填充至绝对精度<br>- **u** 一个 uencoded 字符串 |
| **package** | `package NAMESPACE`<br><br>包声明为 `NAMESPACE` 创建一个独立的命名空间（符号表），这是 Perl 创建类的方式。`NAMESPACE` 属于最内层封闭的块、子例程、`eval` 或文件的剩余部分。如果包声明在同一层级，新的将覆盖旧的。 |
| **pipe** | `pipe(READHANDLE, WRITEHANDLE)`<br><br>打开一个用于读写（通常是在 *fork* 之后）的管道。参见 `pipe(2)`。 |
| **pop** | `pop ARRAY`<br>`pop(ARRAY)`<br><br>弹出并返回数组的最后一个元素。数组将减少一个元素。 |

| 函数 | 描述 |
| :--- | :--- |
| **pos** | `pos(SCALAR)`<br>`pos SCALAR`<br><br>返回 SCALAR 中最后一次匹配搜索结束后的字符偏移量；即下一次搜索将开始的位置。偏移量从 0 开始。<br>如果 *$scalar* 是一个带符号的 `\hello` 且搜索为 *$scalar* = *m*/*elig*，则<br>pos 函数将返回第一个 *1* 后字符的位置。<br>位置 3。 |
| **print** | `print(FILEHANDLE LIST)`<br>`print(LIST)`<br>`print FILEHANDLE LIST`<br>`print LIST`<br>`print`<br><br>将字符串或逗号分隔的字符串列表打印到 FILEHANDLE 或当前选择的 FILEHANDLE，或到默认的标准输出 STDOUT。如果成功返回 1，否则返回 0。 |
| **printf** | `printf(FILEHANDLE FORMAT, LIST)`<br>`printf(FORMAT, LIST)`<br><br>将格式化的字符串打印到 FILEHANDLE，如果省略 FILEHANDLE，则打印到当前选择的输出文件句柄。默认是 STDOUT。类似于 C 的 printf，但不支持 `*`。<br>参见 printf(3)。 |
| **prototype** | `prototype FUNCTION`<br><br>以字符串形式返回函数的原型，其中 FUNCTION 是函数名。如果没有原型则返回 *undef*。 |
| **push** | `push(ARRAY, LIST)`<br><br>将 LIST 中的值推入 ARRAY 的末尾。数组将增加。返回 ARRAY 的新长度。 |
| **q, qq, qw, qx** | `q/STRING/`<br>`qq/STRING/`<br>`qw/LIST/`<br>`qx/COMMAND/`<br><br>引号的替代形式。*q* 结构将 STRING 视为由单引号包围。*qq* 结构将 STRING 视为由双引号包围。*qw* 结构将 LIST 中的每个元素视为由单引号包围，而 *qx* 将 COMMAND 视为反引号。 |
| **quotemeta** | `quotemeta EXPR`<br><br>返回 EXPR 的标量值，其中所有正则表达式元字符都被反斜杠转义。 |

| 函数 | 描述 |
| :--- | :--- |
| **rand** | `rand(EXPR)`<br>`rand EXPR`<br><br>`rand`<br><br>返回 0 到 EXPR 之间的一个随机小数（标量），其中 EXPR 是一个正数。没有 rand 生成相同的数字序列。如果省略 EXPR，则返回 0 到 1 之间的值。<br>参见 rand(3)。 |
| **read** | `read(FILEHANDLE, SCALAR, LENGTH, OFFSET)`<br>`read(FILEHANDLE, SCALAR, LENGTH)`<br><br>从 FILEHANDLE 中读取 LENGTH 个字节，从 OFFSET 位置开始，读入 SCALAR 并返回读取的字节数，如果是 EOF 则返回 0（类似于 fread 系统调用）。<br>参见 fread(3)。 |
| **readdir** | `readdir(DIRHANDLE)`<br>`readdir DIRHANDLE`<br><br>读取目录结构 DIRHANDLE 的下一个条目，该目录由 opendir 打开。参见 directory(3)。 |
| **readline** | `readline FILEHANDLE`<br><br>从选定的 FILEHANDLE 中读取并返回一行；例如，$line = readline(STDIN)。 |
| **readlink** | `readlink(EXPR)`<br>`readlink EXPR`<br><br>返回符号链接的值。EXPR 是符号链接的路径名，如果省略则使用 $_。参见 readlink(2)。 |
| **readpipe** | `readpipe scalar EXPR`<br>`readpipe LIST(proposed)`<br><br>一个实现 qq// 引号结构或反引号用于命令替换的内部函数；例如，要打印 UNIX ls 命令的输出，输入 print readpipe( )。 |
| **recv** | `recv(SOCKET, SCALAR, LEN, FLAGS)`<br><br>在套接字上接收 LEN 字节的消息到 SCALAR 变量。返回发送者的地址。<br>参见 recv(2)。 |
| **redo** | `redo LABEL`<br>`redo`<br><br>重新开始循环块而不重新评估条件。如果有 continue 块，则不会执行。没有 LABEL 时，从最内层封闭的循环重新开始。 |

| 函数 | 描述 |
| :--- | :--- |
| **ref** | `ref EXPR`<br><br>如果 EXPR 是一个引用，则返回 EXPR 的数据类型的标量 TRUE 值，否则返回 NULL 字符串。返回值取决于被引用的对象，是 REF, SCALAR, ARRAY, HASH, CODE 还是 GLOB。如果 EXPR 是一个已转换为某个包的对象的对象，则返回值是包（类）名。 |
| **rename** | `rename(OLDNAME, NEWNAME)`<br><br>将文件 OLDNAME 重命名为 NEWNAME。不能跨文件系统边界工作。如果 NEWNAME 已经存在，它将被销毁。<br>参见 rename(2)。 |
| **require** | `require(EXPR)`<br>`require EXPR`<br>`require`<br><br>通过搜索 @INC 数组中指定的文件，从 Perl 库中包含文件 EXPR。同时检查库是否尚未被包含。如果省略 EXPR，则使用 $_。 |
| **reset** | `reset(EXPR)`<br>`reset EXPR`<br>`reset`<br><br>清除变量和数组，或者如果省略 EXPR，则重置 ?? 搜索。 |
| **return** | `return LIST`<br><br>从子例程中返回值。不能在子例程之外使用。 |
| **reverse** | `reverse(LIST)`<br><br>反转 LIST 的顺序并返回一个数组。 |
| **rewinddir** | `rewinddir(DIRHANDLE)`<br>`rewinddir DIRHANDLE`<br><br>将 DIRHANDLE 中的位置回绕到目录结构的开头。<br>参见 directory(3)。 |
| **rindex** | `rindex(STRING, SUBSTR, OFFSET)`<br>`rindex(STRING, SUBSTR)`<br><br>如果指定了 OFFSET，则从 OFFSET 开始返回 SUBSTR 在 STRING 中的最后位置，行为类似于 index，但返回子串的最后位置而不是第一个位置。 |
| **rmdir** | `rmdir(FILENAME)`<br>`rmdir FILENAME`<br><br>如果目录为空，则删除目录 FILENAME。 |

| 函数 | 描述 |
| :--- | :--- |
| **s** | `s/SEARCH_PATTERN/REPLACEMENT/[g][l][o][e]`<br><br>搜索 SEARCH_PATTERN，如果找到，则用一些文本替换该模式。返回执行的替换次数。g 选项在线内是全局的。i 选项关闭大小写敏感性。e 选项将替换字符串作为表达式进行评估；例如，$/d+\$&+$/e |
| **scalar** | `scalar (EXPR)`<br><br>强制 EXPR 在标量上下文中求值。 |
| **seek** | `seek(FILEHANDLE, POSITION, WHENCE)`<br><br>根据文件中的位置 WHENCE，在文件 FILEHANDLE 中定位文件指针。如果 WHENCE 为 0，则从文件开头开始；如果 WHENCE 为 1，则从文件当前位置开始；如果 WHENCE 为 2，则从文件末尾开始。如果 WHENCE 为 0，POSITION 不能为负数。 |
| **seekdir** | `seekdir(DIRHANDLE, POSITION)`<br><br>为与 DIRHANDLE 关联的目录结构上的 readdir 函数设置 POSITION。<br>参见 directory(3)。 |
| **select** | `select(FILEHANDLE)`<br>`select`<br><br>如果省略 FILEHANDLE，则返回当前选择的文件句柄。如果指定 FILEHANDLE，则设置当前默认用于写入和打印的文件句柄。<br>参见 Formatting。 |
| **select** | `select(RBITS, WBITS, EBITS, TIMEOUT)`<br><br>检查 I/O 文件描述符，看描述符是否准备好读取或写入，或者是否有异常状态待处理。指定位掩码，TIMEOUT 以秒为单位。<br>参见 select(2)。 |
| **semctl** | `semctl(ID, SEMNUM, CMD, ARG)`<br><br>调用 semctl 系统调用，允许对信号量进行控制操作。返回代码很古怪。需要库文件 ipc.ph 和 sem.ph。<br>参见 System V IPC。<br>另参见 semctl(2)。 |
| **semget** | `semget(KEY, NSEMS, SIZE, FLAGS)`<br><br>返回与 KEY 关联的信号量 ID，如果出错则返回未定义。需要库文件 ipc.ph 和 sem.ph。<br>参见 System V IPC。<br>另参见 semget(2)。 |

