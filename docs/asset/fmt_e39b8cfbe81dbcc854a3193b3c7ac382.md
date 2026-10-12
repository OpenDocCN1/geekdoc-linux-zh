
        define MALLOC 1     /* 可以释放 */

        define TEMP 2      /* 应该释放 */

        define PERM 4       /* 无法释放 */

        define STRING 8    /* 赋值为字符串 */

        define STRUC 16    /* 当前为字符串值 */

        define NUMCUR 32  /* 当前为数值值 */

        define NUMBER 64 /* 赋值为数字 */

        define MAYBE_NUM 128 /* 使用输入：如果那么

                            /* 是一个 NODE */

        define ARRAYMAXED 256 /* 数组达到最大尺寸 */

        define FUNC 512     /* 此参数实际上是一个

                            /* 函数名；参见 awkgram.y */

                            /* 这是一个字段 */

        define FIELD 1024   /* 使用本地版本 */

        define INTLSTR 2024

};

使用标志的原因是它们可以节省大量的数据空间。如果`NODE`为每个标志使用单独的`char`字段，将占用`12`字节而不是`2`个`unsigned short`。`NODE`的当前大小（在`Intel x86`上）是`32`字节。增加`10`字节就会将其增加到`42`字节。由于`gawk`可以分配数十万（甚至数百万）个`NODE`，保持其尺寸至关重要。

这与调试有什么关系？我们不是建议使用枚举（`enums`）作为符号常量吗？对于通过逻辑或（`OR`）组合的值，枚举没有任何帮助，因为它们不再能被单独识别了！

**建议：** 提供一个将标志转换为字符串的函数。如果你有多个独立的标志，请设置一个通用的程序。

> 认真的！人们经常通过`gawk`处理数兆的数据。记住，不要有任意限制！

> 注意：这些调试函数不同寻之处在于，应用程序代码从未调用它们。它们存在仅是为了可以从调试器中调用。此类函数应该始终被编译进去，即使没有外围的`#ifdef`，这样你就可以使用它们而无需采取特殊步骤。（通常很微小的）额外代码量是为了开发者节省时间的代价。

首先我们向你展示最初是如何做的。这里是`gawk`早期版本（`3.0.6`）中的`flags2str()`（简化版）：

```c
1 /* flags2str - 使标志值可读 */

2

3 char *

4 flags2str(flagval)

5 int flagval;

6 {

7 static char buffer(BUFSIZ);

8 char *sp;

9

10

11 sp = buffer;

12

13 if (flagval & MALLOC) {

14 strcpy(sp, "MALLOC");

15 sp += strlen(sp);

16 }

17 if (flagval & TEMP) {

18 if (sp != buffer)

19 *sp++ = '|';

20 strcpy(sp, "TEMP");

21 sp += strlen(sp);

22 }

23 if (flagval & PERM) {

24 if (sp != buffer)

25 *sp++ = '|';

26 strcpy(sp, "PERM");

27 sp += strlen(sp);

28 }

29

30 ... 更多类似的内容，为了简洁起见已省略...

31

32

33 return buffer;

34 }
```

（行号相对于函数的开头。）结果是一个字符串，类似于`"MALLOC|PERM|NUMBER"`的内容。每个标志都经过单独测试，如果存在，每个标志的操作都是相同的：测试是否不在缓冲区开头，以便我们可以添加`'|'`字符，将字符串复制到相应位置并更新指针。程序中还存在用于格式化和显示其他类型标志的类似函数。

代码既重复又容易出错，对于`gawk 3.1`，我们对其进行简化和泛化。以下是`gawk`现在的做法。从`awk.h`中的此定义开始：

```c
/* 用于调试目的 */

struct flag {

    int val;            /* 整数标志值 */

    const char *name;   /* 字符串名称 */

};
```

该结构体可以表示任何带有相应字符串值的标志集合。每组标志都有一个对应的函数，该函数返回当前设置的标志的可打印表示。来自`eval.c`：

```c
/* flags2str --- 使标志值可读 */

const char *flags2str(int flagval) {

    static const struct flagtab values[] = {

        { MALLOC, "MALLOC" },

        { TEMP, "TEMP" },

        { PERM, "PERM" },

        { STRING, "STRING" },

        { STRUC, "STRUC" },

        { NUMCUR, "NUMC" },

        { NUMBER, "NUMBER" },

        { MAYBE_NUM, "MAYBE_NUM" },

        { ARRAYMAXED, "ARRAYMAXED" },

        { FUNC, "FUNC" },

        { FIELD, "FIELD" },

        { INTLSTR, "INTLSTR" },

        { 0, NULL }

    };

    /* ... 实现细节 ... */

}
```

`flags2str()`定义了数组。按照约定，`0`表示数组的结束。代码调用`flags2str()`来生成字符串。

# 590

# 第 15 章 • 调试

```bash
$ gdb gawk

GNU gdb 5.3

(gdb) break do_print

Breakpoint 1 at 0x805a584: file builtin.c, line 1547.

(gdb) run 'BEGIN { print "hello, world "'

Starting program: /home/arnold/gnu/gawk/gawk-3.1.4/gawk 'BEGIN print (

  "hello, world \'

Breakpoint 1, do_print (tree=0x80955b8) at builtin.c:1547

    struct redirect *rp = NULL;

(gdb) print *tree

$1 = (sub (node = (lptr = 0x8095599, param_name = 0x8095598 "xU\t\b")

      l1 = 134829464), r = (rptr = 0x0, pptr = 0, preg = 0, hd = 0x0,

      av = 0x0, r_ent = 0), x = (extra = 0x0, xl = 0, param_list = 0x0,

      name = 0x0, flags = 0))

    fltnm = 6.6614605206895102e-31, sp = 0x0, slen = 0, sref = 1,

    idx = 0x0), hash = (next = 0x80955598, length = 0, value = 0x0,

      ref = 1)), type = Node_K_print, flags = 1

$2 = 0x80918a0 "MALLOC"

(gdb) next

    fp = redirect_to_fp(tree->rnode, &rp);

    "print", FALSE);

    fwrite(t[i]->stptr, sizeof(char), t[i]->stlen, fp);

(gdb) print *t[i]

$4 = (sub = (node = (lptr = 0x80955599, param_name = 0x80955598 "xU\t\b")

      l1 = 134829464), r = (rptr = 0x0, pptr = 0, preg = 0, hd = 0x0,

      av = 0x0, r_ent = 0), x = (extra = 0x8095ad8, xl = 134830808,
```
