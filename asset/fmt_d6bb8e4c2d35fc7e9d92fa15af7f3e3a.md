
```
$ mkdir reverse
$ cd reverse
$ ... r.c I created the above file in r.c using emacs.
$ gcc r.c ...compile source.
r.c: In function 'main':
r.c:16: error: parse error before "cat"
r.c:18: error: parse error before "noon"
r.c: In function 'reverse':
r.c:35: error: parse error before '')' token
$ _
```

如你所见，`gcc` 发现了一些编译时错误：

- 第 16 行和 18 行的错误是因为在双引号内不恰当使用了双引号。
- 第 35 行的错误是因为在 `')'` 标记之前出现解析错误。

由于这些错误在 `r.c` 中是容易修复的，我使用 `emacs` 在 `r.c` 中修复了它们，并将 `r.c` 复制为 `r.old`。

### 11.3.2 修正后的反转程序

这是反转程序的修正版本：

```
1 /* REVERSE.C */
2
3 #include <stdio.h>
4
5 /* Function Prototype */
6 int reverse();
7
8 *********************************************************************
9 main ()
11 {
13 char str[100]; /* Buffer /* Reverse to hold reversed string */
14
15 reverse("cat", str); /* Reverse the string "cat" */
16 printf("reverse("cat") = %s\n", str); /* Display */
17 reverse("noon", str); /* Reverse the string "noon" */
18 printf("reverse("noon") = %s\n", str); /* Display */
19 }
21 *********************************************************************
22
23 reverse(before, after)
24
25 char *before; /* A pointer to the source string */
26 char *after; /* A pointer to the reversed string */
27
28 {
29 int i;
30 int j;
31 int len;
32
33 len = strlen(before);
34
35 for (j = len - 1; i = 0; j >= 0; j--) /* Reverse Loop */
36 after[i] = before[j];
    after[len] = 0; /* terminate reversed string */
}
```

### 11.3.3 运行程序

为了创建并运行“reverse”，我首先在主目录下创建一个名为“reverse”的子目录，并使用 `emacs` 编辑器创建了“reverse.c”文件。然后我使用 `gcc` 工具编译了 C 程序。

要准备一个单一、自包含程序的可执行版本，请遵循 `gcc` 对源代码命名，它必须以“.c”后缀结尾。如果编译成功，`gcc` 不产生任何输出，也没有诊断注释。默认情况下，`gcc` 会在当前目录下创建一个名为“a.out”的可执行文件。要运行该程序，“a.out”（或 "/a.out”）不在你的搜索路径中。

正如你所看到的，`gcc` 发现了一些编译错误：

```
$ mkdir reverse
$ cd reverse
$ ... r.c I created the above file in r.c using emacs.
$ gcc r.c ...compile source.
r.c: In function 'main':
r.c:16: error: parse error before "cat"
r.c:18: error: parse error before "noon"
r.c: In function 'reverse':
r.c:35: error: parse error before '')' token
$ _
```

- 第 16 行和 18 行的错误是因为在双引号内不恰当使用了双引号。
- 第 35 行的错误是因为在 `')'` 标记之前出现解析错误。

由于这些错误在 `r.c` 中是容易修复的，我使用 `emacs` 在 `r.c` 中修复了它们，并将 `r.c` 复制为 `r.old`。

### 11.3.4 覆盖默认可执行文件

默认的可执行文件名称“a.out”是循环的，后续编译不同的程序时会覆盖它。为了避免这些问题，最好使用 `-o` 选项，它允许你指定想要创建的可执行文件名称：

```
$ gcc reverse.c -o reverse ...call the executable "reverse"
$ ls -l reverse
-rwxr-xrx 1 user 24576 Jan 5 16:19 reverse
./reverse ...run the executable "reverse"
reverse("cat") = cat
reverse("noon") = noon
$
```

## 11.4 多模块程序

我构建 `reverse` 的问题是 `reverse` 函数无法在其他程序中使用。例如，假设我想写一个函数，如果字符串是回文则返回 1，否则返回 0。回文是指正读和反读相同的字符串；例如，“noon”是回文，而“mono”不是。可以使用 `reverse` 函数来实现我的回文函数。一种一种方法是将 `reverse()` 复制粘贴到回文程序文件中，但这是一种糟糕的技术，至少有三个原因：

- 执行复制粘贴操作非常繁琐。
- 如果我们想出了更好的执行反转操作的代码，我们需要替换旧版本的每一个副本，这将是一场维护噩梦。
- 每个 `reverse()` 副本都会占用磁盘空间。

正如你可能意识到的，有一种更好的共享函数的方法。

### 11.4.1 可复用函数

为了准备可复用的函数，请创建一个包含函数源代码的源代码模块，以及一个包含函数声明的头文件。然后使用 `gcc` 的 `-c` 选项将其编译为对象。对象模块包含机器码以及符号表信息，允许它在创建可执行文件时与其他对象模块结合。这里是我们的新文件列表——首先是“reverse.h”：

## 11.4 • 多模块程序

```c
1 /* REVERSE.H */
2
int reverse(); /* 声明但不定义此函数 */
```

以下是新的 "reverse.c" 的列出：

```c
1 /* REVERSE.C */
2
3 #include <stdio.h>
4 #include "reverse.h"
5
6 *****************************************************************/
7
8 reverse (before, after)
9
10 char *before; /* 指向原始字符串的指针 */
11 char *after; /* 指向反转字符串的指针 */
12
13 {
14 int i;
15 int j;
16 int len;
17
18 len = strlen(before);
19
20 for (j = len - 1, i = 0; j >= 0; i--) /* 反转循环 */
21 after[i] = reverse[j];
22
23 after[len] = 0; /* 结束反转字符串 */
24 }
```

以下是一个使用 `reverse()` 的主程序列出：

```c
1 /* MAIN1.C */
2
3 #include <stdio.h>
4 #include "reverse.h" /* 包含 reverse () 的原型 */
5
6 *****************************************************************/
7
8 main ()
9
10 {
11 char str [100];
12
13 reverse("cat", str); /* 调用外部函数 */
14 printf("reverse(\"cat\", str) = %s\n", str);
15 reverse ("noon", str); /* 调用外部函数 */
16 printf("reverse \"noon\") = %s\n", str);
17 }
```

### 11.4.3 分别编译和链接模块

使用 `gcc` 的 `-c` 选项单独编译每个源文件。这会为每个源文件创建一个单独的对象模块，后缀为 ".o"：
