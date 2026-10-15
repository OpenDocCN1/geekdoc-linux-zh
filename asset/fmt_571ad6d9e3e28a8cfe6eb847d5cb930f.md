
如本示例所示，当故意从一个 case 语句贯穿到另一个 case 语句时，注释是一种常见（且良好的）做法。

## 空格

本节涵盖符号和关键字周围的空格，而不是我们在前几节中涵盖过的缩进空格。总的来说，Linux 编码风格规定了大多数函数周围有空格，且其括号之间没有空格。例如：

```
if (foo)
while (foo)
for (int i = 0; i < NR_CPUS; i++)
switch (foo);
```

约定、函数、宏以及看起来像函数的关键字——例如 `sizeof`、`typeof` 和 `alignof`——同样在关键字与括号之间没有空格。

```
wake_up_process(task);
size_t nlongs = BITS_TO_LONG(bits);
int len = sizeof(struct task_struct);
typeof(p)
alignof((struct sockaddr *)__attribute__)
```

在二元运算符周围两边加空格。例如：

```
int sum = a + b;
int product = a * b;
int mod = a % b;
int len = a / b;
```

括号内部没有前导或后续空格。例如：

```
if (foo)
```

在赋值运算符周围两边加空格。例如：

```
x = y
```

在三元运算符周围两边加空格。例如：

```
int ret = (x) ? y : z;
```

在关系运算符周围两边加空格。例如：

在一元运算符周围，运算符与操作数之间不留空格。例如：

```
x++;
--mask
```

## 大括号

以及这个示例：

```c
do {
    percpu_counter_add(&ca->cpustat[idx], val);
    ca = ca->parent;
} while (ca);
```

最后，不需要大括号的语句可以省略。例如，以下是鼓励但不是要求的：

```
if (cnt > 63)
cnt = 63;
```

背后的逻辑都是 `K&R`。大部分 Linux 编码风格遵循 `K&R` 风格，即在那本著名的书中使用的 C 编码风格。

## 行长度

源代码行应保持在 80 个字符以内。这使得代码可以在标准的 80x24 终端上垂直显示。

对于代码必须超过 80 个字符的情况，还没有被公认的标准做法。有些开发者允许行换行，让他们的编辑器处理如何以可读的方式显示代码。另一些人手动折行，在合适的地方插入换行符，每个新行从原始制表符停止位开始。

同样，有些开发者会将换行的函数参数进行对齐。

```c
static void get_new_parrot(const char *name,
                           unsigned long disposition,
                           unsigned long feather_quality)
```

其他开发者会折行但不对齐参数，而是使用标准的两个 tab：

```c
int find_pirate_flag_by_color(const char *color, char *name, int len)
```

《C 语言程序》由 `Brian Kernighan` 和 `Dennis Ritchie` 出版（Prentice Hall，ISBN# 0-13-11-362-8），被称为 `K&R`，是 C 语言的圣经，由 C 语言作者及其同事编写。

### 第20章 补丁、黑客与社区

在这种情况下没有绝对的规则，选择权交由开发者你自己。许多内核贡献者（包括我在内）倾向于前一种例子：手动拆分超过80个字符的行，并尝试产生的新行与上一行保持对齐。

### 命名

任何名称都不应使用驼峰命名法（CamelCase）、大驼峰（Studly Caps）或其他混合大小写方案。如果用途明确，调用局部变量 `idx` 甚至 `j` 是完全可以的。像 `LoopIndex` 这样的名字是不可接受的。匈牙利命名法（在变量名中编码变量类型）是没有必要的，永远不应该使用。这里是 C、Java、Unix 或 Windows。

尽管如此，全局变量和函数具有描述性的名称，使用小写字母并通过下划线分隔。调用全局函数 `atty()` 会令人困惑；像 `get_active_tty()` 这样的名称要接受得多。这是 Linux，不是 BSD。

### 函数

根据经验，函数不应超过两个屏幕的内容，且局部变量应少于十个。一个函数应该只做一件事并把它做好。将一个函数拆分为一系列较小的函数没有坏处。如果你担心函数调用开销，可以通过 `inline` 关键字使用内联函数。

### 注释

为代码编写注释很重要，但必须正确地注释。通常情况下，你想描述代码在做什么以及为什么要这样做，而不是它是怎么做的。如何做应该从代码本身就能看出。如果不是，你可能需要重新思考你写的内容。此外，注释不应包含谁编写了函数、修改日期或其他无关紧要的废话。然而，源文件中是可以接受此类信息的。

内核使用 C 风格注释，尽管 `gcc` 支持 C++ 风格的注释。内核中的注释风格保持为：

```c
/*
 * speed() - 返回海盗船的当前速度
 * 我们需要此来计算船坐标。由于此函数可能会睡眠，
 * 不要持有自旋锁时调用。
 */
```

在注释中，重要的注意事项通常以 `"XXX:"` 前缀，错误通常用 `"FIXME:"` 来修复，例如：

```c
/*
 * FIXME: 我们假设 dog == cat，这在未来可能不成立
 */
```

内核具有一种自生成文档的功能。它基于 `GNOME`，但经过了轻微修改并重命名为 `Kernel-doc`。要创建 HTML 格式的独立文档，运行：

```bash
make htmldocs
```

或者生成 postscript 格式：

```bash
make psdocs
```

你可以通过遵循特殊的注释格式来使用系统记录你的函数：

```c
/**
 * find_treasure - 寻找“X标记处”
 * @map - 宝藏地图
 * @time - 宝藏隐藏的时间
 *
 * 必须在持有 pirate_ship_lock 时调用。
 */
```

```c
void find_treasure(int map, struct timeval *time)
{
    /* ... */
}
```

更多信息请参见 `Documentation/kernel-doc-nano-nano-HOWTO.txt`。

### Typedef

Linux 内核开发者社区对 `typedef` 运算符非常反感。他们的理由是：

- `typedef` 隐藏了数据结构的真实类型。
- 因为类型被隐藏了，代码更容易出现坏事，例如在栈上按值传递结构。
- `typedef` 仅仅是因为懒。

因此，为了避免被嘲笑，请避免使用 `typedef`。

当然，`typedef` 也有几个好的用处：隐藏特定架构的变量实现，或者在类型可能更改时提供前向兼容性。仔细决定是否需要 `typedef`，或者它仅仅是为了减少你需要输入的字符数而存在。

### 使用现有例程

不要重复造轮子。内核提供了字符串处理函数、压缩例程和链表接口，所以请使用它们。

不要用通用接口来封装现有的接口。你经常能看到明显是从某一个操作系统移植到 Linux 的代码，各种内核接口被封装在某些粗陋的胶水函数中。没有人喜欢这样，所以请直接使用提供的接口。

### 在源码中最小化 ifdefs

直接在 C 源码中放置 `ifdef` 预处理器指令是不受欢迎的。你不应该在函数中做诸如下所示的操作：

```c
#ifdef CONFIG_FOO
    foo();
#endif
```

相反，如果没有设置 `CONFIG_FOO`，将 `foo()` 定义为空：

```c
#ifdef CONFIG_FOO
static int foo(void)
{
    /* ... */
}
#else
static inline int foo(void) { }
#endif /* CONFIG_FOO */
```

然后，你就可以无条件地调用 `foo()`。让编译器为你完成工作。

### 结构体初始化

需要使用标记标识符（labeled identifiers）来初始化结构体。这是好事，因为防止了结构的变化导致错误的初始化。它还允许值被弃用。`C99` 为标记标识符采用了一种丑陋的格式，而 `gcc` 正在废弃 `GNU` 风格的标记标识符的使用，这有点奇怪。因此，内核代码需要使用新的 `C99` 标记标识符格式，无论它有多丑：

```c
struct foo_foo = {
    .a = INITIAL_A,
    .b = INITIAL_B,
};
```

在此代码中，`a` 和 `b` 是 `struct foo` 的成员，`INITIAL_A` 和 `INITIAL_B` 分别是它们的初始化值。如果字段未设置，它将被设置为 `ANSI C` 的默认值（例如，指针为 `NULL`，整数为零，浮点数为 `0.0`）。例如，如果 `struct foo` 也有 `int c` 作为成员。
