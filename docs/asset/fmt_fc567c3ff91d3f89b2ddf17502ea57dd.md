
函数的大部分是一个遍历标志值数组的循环（第 12 行）。当找到一个标志时（第 13 行），代码计算字符串所需的多少空间（第 18 行），并测试是否还有那么多剩余空间（第 19–20 行）。

测试`sp != buffer`会在找到的第一个标志值上失败，并返回 0。在后续的标志中，该测试的值为 1。这告诉我们是否需要在数值之间使用`', '`分隔符。通过将结果（1 或 0）加到字符串的长度上，我们就能得到`space_needed`的正确值。出于同样的原因，第 22 行也使用了相同的测试来控制第 23 行和第 24 行，这两行负责插入`'|'`字符。

最后，第 26–29 行将字符串值复制进来，调整剩余的空间量，并更新`sp`指针。第 33 行返回缓冲区的地址，其中包含字符串的可打印表示形式。

那么，那个`静态缓冲区`呢？通常，良好的编程实践不鼓励使用返回`静态`缓冲区地址的函数：多次调用此类函数很容易每次都会覆盖缓冲区，迫使调用者复制返回的数据。

此外，`静态`缓冲区按定义是固定大小的缓冲区。那 GNU 的“无任意限制”原则去哪里了？

这两个问题的答案在于要记住，这是一个`调试`函数。正常代码`绝不会`调用`genflags2str()`；它只由使用调试器的人类调用。没有调用者持有指向缓冲区的指针；作为进行调试的开发人员，我们不关心每次调用函数时缓冲区被覆盖。

在实践中，固定大小也不是问题；我们知道`BUFSIZ`足够大，可以表示我们使用的所有标志。尽管如此，基于经验并知道情况可能会变化，`genflags2str()`包含有保护自身免受缓冲区溢出影响的代码。（即`space_left`变量和第 18–20 行的代码。）

附带一提，`BUFSIZ`的使用是可以商榷的。该常量应专门用于 I/O 缓冲区，但通常也用于一般的字符串缓冲区。此类代码最好定义显式的常量，例如`FLAGVALSIZE`，并在第 11 行使用`sizeof(buffer)`。

下面是一个简化的 GDB 会话，展示了`flags2str()`的使用：

```text
$ gdb gawk

GNU gdb 5.3

... 

(gdb) break do_print

Breakpoint 1 at 0x805a584: file builtin.c, line 1547.

(gdb) run 'BEGIN ( print 'hello, world!' ) '

Starting program: /home/arnold/Gnu/gawk/gawk-3.1.4/gawk 'BEGIN ( print 
"hello, world!' )'

Breakpoint 1, do_print (tree=0x80955b8) at builtin.c:1547

1547	struct redirect *rp = NULL;

(gdb) print *tree

$1 = {sub = {ndep = {l = ({lptr = 0x8095598, param_name = 0x8095598 'x\0u\t/b\u0027,
						l = 134829464), r = ({rptr = 0x0, pptr = 0, preg = 0x0, hd = 0x0,
								av = 0x0, x_ent = 0}), x = {extra = 0x0, xl = 0, param_list = 0x0},
						name = 0x0, number = 1, reflags = 0), val = {
										fignum = 6.6614606209589101e-316, sp = 0x0, slen = 0, sref = 1,
										idx = 0), hash = {next = 0x8095598, name = 0x0, length = 0, value = 0x0,
										ref = 1}), i_type = Node_K_print, flags = 1

(gdb) print flags2str(tree->flags)

$2 = 0x80918a0 "HALLOC"

(gdb) next

1553						fp = redirect_to_fp(tree->rnode, & rp);

... 

1588						fwriter(t[t]->atptr, sizeof(char), t[i]-'start, fp,
								"print", rp, FALSE);

(gdb) print *t[1]

$4 = {sub = {ndep = {l = ({lptr = 0x8095598, param_name = 0x8095598 'x\0u\t/b\u0027,
							l = 134829464), r = ({rptr = 0x0, pptr = 0, preg = 0x0, hd = 0x0,
								av = 0x0, x_ent = 0}), x = {extra = 0x8095ad8, xl = 134830808,
									param_list = 0x8095ad8), name = 0xc 'Address (hex out of bounds',
										 number = 1, reflags = 4294967295), val = {
											fignum = 6.6614606209589101e-316, sp = 0x8095ad8 'hello, world',
											slen = 12, sref = 1, idx = -1}, hash = {next = 0x8095598, name = 0x0,
											length = 134830808, value = 0xc, ref = 1}), i_type = Node_val, flags = 29}

(gdb) print flags2str(t[1]->flags)

$5 = 0x80918a0 "HALLOC|PERM|STRING|STRUC"
```

我们希望你会同意，当前的通用机制比原来的机制优雅得多，且更容易使用。

仔细设计和使用结构体（structs）通常可以替换或整合重复的代码。

### 15.4.1.5 尽量避免使用联合体

> “天下没有免费的午餐。”

>

> —`拉撒路·朗（Lazarus Long）`—

C 语言中的`union`（联合体）是一个相对深奥的机制。它允许通过在同一物理空间内存储不同的项目来节省内存；程序如何处理它取决于访问方式：

```c
/* ch15-union.c --- 联合体使用的简要演示。 */
#include <stdio.h>

int main(void)
{
    union i_f {
        int i;
        float f;
    } u;

    u.f = 12.34;    /* 赋值一个浮点值 */
    printf("%f also looks like %#x\n", u.f, u.i);
    exit(0);
}
```

当程序在 Intel x86 GNU/Linux 系统上运行时，会发生以下情况：

```text
$ ch15-union
12.340000 also looks like 0x414570a4
```

该程序以十六进制整数的形式打印出表示浮点数的位模式。两个字段的存储占用同一块内存；区别在于内存的处理方式：`u.f`像浮点数一样运作，而`u.i`中的相同位则像整数一样运作。

联合体在编译器和解释器中特别有用，因为它们经常创建表示源代码文件结构（称为`解析树`）的树状结构。这模拟了编程语言被形式化描述的方式：`if`语句、`while`语句、赋值语句等都是更通用的“语句”类型的实例。因此，编译器可能会有类似这样的定义：

```c
struct if_stm { ... };                  // IF 语句的结构
struct while_stm { ... };               // WHILE 语句的结构
struct for_stm { ... };                 // FOR 语句的结构
... 其他语句类型的结构 ...

typedef enum stm_type {                // 我们实际拥有的
    IF, WHILE, FOR, ... 
} TYPE;
```

```c
/* 这包含了类型以及各个种类语句的联合体。 */
struct statement {
  TYPE type;
  union stmt {
    struct if_stmt if_st;
    struct while_stmt while_st;
    struct for_stmt for_st;
    ...
  } u;
};
```

除了使用`union`外，惯例上使用宏来使`union`的组件看起来像是`struct`中的字段。例如：
