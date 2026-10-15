
# 568 GNU/Linux 编程

```c
27: /* Exhaust the stack */

28:

29: ret = stackPush(&myStack_1, 1 );

30: ASSERT( ret == 0), "Stack Push 1 failed." );

31:

32: ret = stackPush(&myStack_1, 2 );

33: ASSERT( ret == 0), "Stack Push 2 failed." );

34:

35: ret = stackPush(&myStack_1, 3 );

36: ASSERT( ret == 0), "Stack Push 3 failed." );

37:

38: ret = stackPush(&myStack_1, 4 );

39: ASSERT( ret == 0), "Stack Push 4 failed." );

40:

41: ret = stackPush(&myStack_1, 5 );

42: ASSERT( ret == 0), "Stack Push 5 failed." );

43:

44: ret = stackPush(&myStack_1, 6 );

45: ASSERT( ret == -1), "Stack exhaustion failed." );

46:

47: 

48: }

49:

50: void __CUT_PushPopTest( void )

51: {

52: int ret;

53: int value;

54:

55: /* Test two pushes and then two pops */

56:

57: ret = stackPush(&myStack_2, 55 );

```
# 568 GNU/Linux 编程

```c
58: ASSERT( ret == 0), "Stack Push of 55 failed." );

59:

60: ret = stackPush(&myStack_2, 101);

61: ASSERT(ret == 0), "Stack Push of 101 failed." );

62:

63: ret = stackPop(&myStack_2, &value);

64: ASSERT(ret == 0), "Stack Pop failed." );

65: ASSERT(value == 101), "Stack Popped Wrong Value.");

66:

67: ret = stackPop(&myStack_2, &value);

68: ASSERT(ret == 0), "Stack Pop failed." );

69: ASSERT(value == 55), "Stack Popped Wrong Value.");

70:

71:

72:

73:

74: void __CUT_TAKEDOWN__Explode( void )

75: {

76: int ret;

77:

78: ret = stackDestroy(&myStack_1);

79: ASSERT(ret == 0), "Stack 1 Destruction." );

80:

81: ret = stackDestroy(&myStack_2);

82: ASSERT(ret == 0), "Stack 2 Destruction." );

83:

84: printf("\nTest Complete\n");

85: }

```

现在你已经拥有了单元测试文件（已为 `cut` 环境编码），你可以查看如何将其变为可执行的测试程序。虽然这很容易在简单的 `Makefile` 中进行编码，但此示例演示了命令行构建。

你需要从 `cut` 系统获取三个文件（获取这些文件的 URL 在本章的“Resources”部分提供）。`cut` 工具根据你提供的单元测试源文件提供单元测试环境。这些是 Python 文件，因此目标系统上需要一个 Python 解释器。另外两个文件是 `cut.h` 和 `libcut.inc`，它们最终与你的单元测试应用程序链接。

第一步是创建 `cut` 单元测试环境。这会创建一个 C 语言 `main` 函数并汇集单元测试所需的 API。`cutgen.py` 工具为你提供此功能，如下所示：

```bash
cutgen.py test_1.c > cutcheck.c
```

# 第 29 章 软件单元测试框架 569

给定你的单元测试文件（列表 29.6），你将其作为 `cutgen.py` 的唯一参数，并将输出重定向到源文件 `cutcheck`。为了进一步理解 `cutgen` 提供了什么，你现在可以查看此文件（如列表 29.7）。

由 `cutgen` 自动生成的文件仅是将你单元测试文件中的单元测试汇在一起并顺序调用它们。你可以向 `cutgen` 提供许多测试文件，这会导致在生成的文件调用更多的单元测试函数。

# 列表 29.7 由 cutgen 创建的单元测试环境源码

```c
1: #include "libcut.inc"

2:

3:

4:     void _CUT_BRINGUP__Explode( void );

5:     void _CUT_PushConsumptionTest( void );

6:     void _CUT_PushPopTest( void );

7:     extern void _CUT_TAKEDOWN__Explode( void );

8:

9:

10:    int main(int argc, char *argv[])

11:    {

12:         cut_init( -1 );

13:         cut_start("Explode", _CUT_TAKEDOWN__Explode );

14:             _CUT_BRINGUP__Explode();

15:             _CUT_PushConsumptionTest();

16:             _CUT_PushPopTest();

17:         cut_end("Explode" );

18:             _CUT_TAKEDOWN__Explode();

19:

20:         cut_break();

21:     }
```

最后，你只需编译并链接文件来构建单元测试镜像。此镜像包含了自动生成的源码、单元测试文件和要测试的源码（`stack.c`）。此处所示：

```bash
gcc -o cutcheck stack.c test_1.c
```

# 570 GNU/Linux 编程

你可以通过简单调用 `cutcheck` 来执行单元测试。它会输出数字和字符来指示进度。

```bash
./cutcheck
Stack bringup called
.......10
Test Complete
```
