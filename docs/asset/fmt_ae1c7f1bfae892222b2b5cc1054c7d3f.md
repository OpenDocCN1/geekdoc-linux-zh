
```
21:        checkResult(3, 0);

22:   }

23:

24:   if (stackDestroy(&stack) == 0) {

25:        checkResult(4, 1);

26:   } else {

27:        checkResult(4, 0);

28:   }

29:

30:   if (failed == 0) {

31:        printf("All tests passed!\n");

32:   } else {

33:        printf("Some tests failed.\n");

34:   }

35:

36:   return 0;

37: }
```

# C 单元测试系统

C 单元测试系统（简称 `cut`）是构建单元应用程序的简单架构。`Cut` 为单元测试的集成提供了一个简单环境，并有一套工具汇总测试并构建主框架。`Cut` 解析单元测试文件并将它们构建成单个镜像，按顺序执行提供的单元测试。

`Cut` 提供了一个用 Python 编写的工具称为 `cutgen.py`。该工具解析单元测试源文件并围绕要运行的测试构建 `main` 函数。单元测试文件必须以特定方式编写；我们将在示例源码中探索这一点。

让我们通过一个示例来验证之前栈示例中的 `push` 和 `pop` 函数。`Cut` 提供了一个我们用来构建的简单接口，该接口在列表 24.6 中显示。

我们在第 5 和 6 行声明了局部变量（我们要执行测试的两个栈），然后是四个作为接口的函数。

需要注意的两个函数是第一个最后一个。它们是初始化函数 `_CUT_BRINGUP_Explode`（第 8–20 行）和测试执行后函数 `_CUT_TAKEDOWN_Explode`（第 74–85 行）。`cut` 框架调用

## 426 GNU/Linux 应用程序编程

在测试开始之前的准备（bringup）函数，一旦所有测试函数执行完毕，将调用清理（teardown）函数。注意，我们仅仅执行了必要的初始化（使用 `stackCreate` 初始化两个栈），但我们也执行了单元测试，以确保单元测试中所需的元素是可用的。同样，在所有单元测试调用完毕后的 `teardown` 函数中，我们销毁了栈，但也检查了所有用例的返回状态。

单元测试以 `_CUT_` 前缀编码。这允许 `cutgen` 工具能够找到它们并在测试框架中调用它们。当我们执行单元测试的必要元素时，我们会调用一个特殊的函数 `ASSERT`，它用于记录错误。`ASSERT` 函数包含两个部分：一个测试表达式和一个在测试失败时嵌入的字符串。测试表达式标识成功条件，如果为 `false`，则测试元素失败。

请注意，在某些情况下，我们为每个 API 元素编写了多个测试（如第 64–65 行所示）。

## 列表 24.6 为 Cut 编写的单元测试示例（位于光盘 `/source/ch24/cut_test_1.c`）

```
1:    #include <stdio.h>

2:    #include "stack.h"

3:    #include "cut.h"

4: 

5:    stack_t myStack1;

6:    stack_t myStack2;

7: 

8:    void __CUT_BRINGUP__Explode( void ) 

9:    {

10:        int ret;

11: 

12:        printf("Stack test bringup called\n");

13: 

14:        ret = stackCreate(&myStack_1, 5);

15:        ASSERT(ret == 0, "Stack 1 Creation.");

16: 

17:        ret = stackCreate(&myStack_2, 5);

18:        ASSERT(ret == 0, "Stack 2 Creation.");

19: 

20: 

21: 

22: 

23:    void __CUT_PushConsumptionTest( void ) 

24:    {

25:        int ret;

26:

27:    /* Exhaust the stack */

28:

29:    ret = stackPush(&myStack_1, 1 );

30:    ASSERT(ret == 0, "Stack Push 1 failed.");

31:

32:    ret = stackPush(&myStack_1, 2 );

33:    ASSERT(ret == 0, "Stack Push 2 failed.");

34: 

35:    ret = stackPush(&myStack_1, 3 );

36:    ASSERT(ret == 0, "Stack Push 3 failed.");

37: 

38:    ret = stackPush(&myStack_1, 4 );

39:    ASSERT(ret == 0, "Stack Push 4 failed.");

40: 

41:    ret = stackPush(&myStack_1, 5 );

42:    ASSERT(ret == 0, "Stack Push 5 failed.");

43: 

44:    ret = stackPush(&myStack_1, 6 );

45:    ASSERT(ret == -1, "Stack exhaustion failed.");

46: 

47:    }

48: 

49: 

50:    void __CUT_PushPopTest( void )

51:    {

52:        int ret;

53:        int value;

54: 

55:        /* Test two pushes and then pops */

56: 

57:        ret = stackPush(&myStack_2, 55 );

58:        ASSERT(ret == 0, "Stack Push of 55 failed.");

59: 

60:        ret = stackPush(&myStack_2, 101 );

61:        ASSERT(ret == 0, "Stack Push of 101 failed.");

62: 

63:        ret = stackPop(&myStack_2, &value );

64:        ASSERT(ret == 0, "Stack Pop failed.");

65:        ASSERT(value == 101, "Stack Popped Wrong Value.");

66: 

67:        ret = stackPop(&myStack_2, &value );

68:        ASSERT(ret == 0, "Stack Pop failed.");

69:        ASSERT(value == 55, "Stack Popped Wrong Value.");

70: 

71:  }

72: 

73:  void _CUT_TAKEDOWN__Explode(void  )

74:  {

75:    int ret;

76: 

77: 

78:    ret = stackDestroy(&Stack_1);

79:    ASSERT(ret == 0, "Stack 1 Destruction.");

80: 

81:    ret = stackDestroy(&Stack_2);

82:    ASSERT(ret == 0, "Stack 2 Destruction.");

83: 

84:    printf("\nTest Complete\n");

85:  }
```
