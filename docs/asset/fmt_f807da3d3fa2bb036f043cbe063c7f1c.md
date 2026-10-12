
```
$ nl -ba buggy.c
1 /* Out of bounds check */
2 #define SIZE 10
3
4 int main()
5 {
6   char str[SIZE];
7   str[SIZE] = '\0';
8   return 0;
9 }
$ gcc buggy1.c -o buggy1
$ cppcheck buggy1.c
Checking buggy1.c...
[buggy1.c:8]: (error) Array 'str[10]' accessed at index 10, which is out of bounds.
```

在接后的 `buggy2.c` 程序中，我们展示了 `cppcheck` 如何报告 `gcc` 无法检测的空指针解引用错误。

```
$ cat buggy2.c
/* Null pointer dereferencing error */
int main()
{
  char *str;
  *str = '\0';
}
$ gcc buggy2.c
$ cppcheck buggy2.c
Checking buggy2.c...
[buggy2.c:6]: (error) Uninitialized variable: str
$
```

下面的示例说明了 `gcc` 未报告但被 `cppcheck` 捕获的内存泄漏。

```
$ cat buggy3.c
/* Memory leak stdlib */
#include <stdlib.h>

struct student {
  char name[100];
  int ID;
}

int main()
{
  struct student s;
  char *s1, *s2;
  int size;

  size = sizeof(size);
  s1 = malloc(size);
  s2 = malloc(size);
  free(s1);

  return 0;
}
$ gcc buggy3.c
$ cppcheck buggy3.c
Checking buggy3.c...
[buggy3.c:20]: (error) Memory leak: s2
$
```

你可以在命令行中指定多个文件，如下所示。

```
$ cppcheck buggy1.c buggy2.c buggy3.c
Checking buggy1.c...
[buggy1.c:8]: (error) Array 'str[10]' accessed at index 10, which is out of bounds
1/3 files checked 25% done
Checking buggy2.c...
[buggy2.c:6]: (error) Uninitialized variable: str
2/3 files checked 43% done
Checking buggy3.c...
[buggy3.c:20]: (error) Memory leak: s2
3/3 files checked 100% done
$ 
```

接下来的章内练习旨在让你领会 `cppcheck` 工具的使用，并帮助你理解它产生的一些错误信息。

## 练习 14

（此处省略重复的练习描述文本，保持与原文一致）

```c
printf("Hello, World!\n");
return 0;
}
void f1(int count) {
    int i;
    for (i=0; i < count; i++)
        f2(COUNT2);
    return;
}
void f2(int count) {
    int i;
    for (i=0; i < count; i++)
        f3();
    return;
}
```

```c
void f3(void) {}
$ gcc -Wall -pg gprof_test.c -o gprof_test
$ gprof_test
Hello, World!
$ gprof gprof_test.gmon.out > prof.out
$ cat prof.out
```

扁平分析 (Flat profile):

每个样本计数为 `0.01` 秒。

| 时间 (秒) | 累计 (秒) | 自身 (秒) | 总计 (秒) | 调用次数 | 毫秒/调用 | 毫秒/调用 | 函数名 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `54.12` | `0.47` | `0.47` | `1074790401` | `0.00` | `0.00` | `f3` |
| `47.06` | `0.87` | `0.40` | `1025` | `0.39` | `0.85` | `f2` |
| `0.00` | `0.87` | `0.00` | `1` | `0.00` | `869.27` | `f1` |

`%` 该函数所占总运行时间的百分比。

`cumulative` 该函数以及上述列出的记录的秒数总和。

```
[ 输出截断]
...
```

调用图（下文附说明）

粒度：每个样本覆盖 `2` 字节，占 `0.87` 秒中的 `1.15%`

| 索引 | 自身 | 子节点 | 调用 | `<自发>` |
| :--- | :--- | :--- | :--- | :--- |
| | | | | `main [1]` |
| `[1]` | `100.0` | `0.00 0.87` | `1/1 f1 [3]` | |
| | | `0.00 0.87` | `1/1025 f2 [2]` | |
| | | `0.00 0.00` | `1/1074790401 f3 [4]` | |

`422`

`Linux`

| | | | | | | |
|---|---|---|---|---|---|---|
| | | `0.00` | `0.00` | `1/1025` | `main [1]` | |
| | | `0.40` | `0.46` | `1024/1025` | `f1 [3]` | |
| `[2]` | `100.0` | `0.40` | `0.47` | `1025` | `f2 [2]` | |
| | | `0.47` | `0.00` | `1072490400/1072490401` | `f3 [4]` | |
| | | `0.00` | `0.87` | `1/1` | `main [1]` | |
| `[3]` | `99.9` | `0.00` | `0.46` | `0.87 1024/1025` | `f1 [3] f2 [2]` | |
| | | `0.00` | `0.00` | `1/1072490401` | `main [1]` | |
| | | `0.47` | `0.00` | `1072490400/1072490401` | `f2 [2]` | |
| `[4]` | `53.5` | `0.47` | `0.00` | `1072490401` | `f3 [4]` | |

此表描述了程序的调用树，并根据在函数及其子函数上花费的总时间进行了排序。

表中的每个条目由多行组成。左侧边缘带有索引的行列出当前函数。其上面的行列出调用该函数的函数，下面的行列出该函数调用的函数。

- **赋予表中每个元素的唯一数字。** 索引按数字排序。索引号打印在每个函数名旁边，方便查找该函数在表中的位置。

- **% 时间** 这是在该函数及其子函数上花费“总”时间的百分比。注意，对于不同的视图，被选项排除的函数等，这些数字不会相加到 `100%`。

```
[输出截断]
$
```

注意，只有当你的程序通过 `exit()` 或 `return` 退出时，`gprof` 才会生成分析文件 `gmon.out`。如果程序正常终止或通过 `_exit()` 终止，不会生成分析文件。由于分析文件生成在当前工作目录下，你的程序必须具有创建该文件的适当权限。

# 练习 14.14

在你的 `Linux` 系统上重复之前的会话。得到的结果相同吗？

# 练习 14.15

显示命令序列，用于为 `gprof_test.c` 文件中的程序生成注释源文件。

# 14.7 动态分析工具

程序的动态分析涉及在其运行期间对其分析。如前所述，此阶段包括对软件的调试、追踪和性能监控。本节将讨论用于追踪程序执行并测量程序的工具……（注：此处原文逻辑混乱，已按语义翻译）

# 14.7.1 使用 `gdb` 调试源代码

（注：原文此处存在大量逻辑重复，已根据语意进行了整理翻译）

# 14.7.1 使用 `gdb` 调试源代码

对程序的调试是耗时且困难的。调试包括在 `gdb` 环境下：

- 运行程序
- 设置断点
- 单步执行
- 列出源代码
- 编辑代码
- 修改变量

`Linux` 有许多调试器，常用的是 `gdb` 和 `pdb`。它们提供了类似的功能。`gdb` 允许：

- 运行程序
- 设置断点
- 单步执行

在用 `gdb` 调试之前，必须使用 `-g` 选项进行编译。`gdb` 提供了：

- 运行程序
- 设置断点
- 单步执行
- 列出源代码
- 访问变量

语法：

`gdb [options] [executable-file] [core-file]`
