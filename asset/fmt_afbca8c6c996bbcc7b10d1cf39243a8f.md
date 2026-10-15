
cut 系统提供了一些额外的特性，但通过快速回顾，你可以看到这个简单的工具有多强大。

## 嵌入式单元测试

嵌入式单元测试框架（称为 `emunit`）是一个为嵌入式系统设计的有趣框架。它可以在不需要标准库分配对象的情况下运行。`emunit` 提供了许多生成测试模板以及测试环境的 main 函数。`emunit` 框架与 cut 非常相似，并提供的测试函数见表 29.1。

### 表 29.1 emunit 提供的测试函数

| 函数 | 目的 |
|---|---|
| `TEST_ASSERT_EQUAL_STRING(exp,actual)` | 断言字符串比较失败 |
| `TEST_ASSERT_EQUAL_INT(exp,actual)` | 断言整数比较失败 |
| `TEST_ASSERT_NULL(pointer)` | 断言指针为空 |
| `TEST_ASSERT_NOT_NULL(pointer)` | 断言指针不为空 |
| `TEST_ASSERT_MESSAGE(cond, message)` | 如果条件为假则断言并输出消息 |
| `TEST_ASSERT(condition)` | 断言条件为假 |
| `TEST_FAIL(message)` | 失败测试并输出消息 |

现在是时候查看为 `emunit` 框架编写的单元测试以及设置环境的主程序了。列表 29.8 显示了一个用于 `emunit` 的最小单元测试。在第 1 行，你包含了 `embUnit` 头文件（这为你的单元测试提供了接口）。你定义了两个在每个单元测试前后调用的函数，标记为 `embUnit`：第 7-10 行的 `setup` 和第 13-16 行的 `teardown`。

你定义了各个单元测试（19-54 行）。此处说明三个测试：第一个是 `testUnit`（19-25），第二个是 `testPushPop`，第三是 `testStackDestroy`（48-54）。与之前的单元测试一样，你执行操作然后测试结果。在这种情况下，你使用 `emunit` 提供的 `TEST_ASSERT_EQUAL_INT` 函数来检查响应，如果断言失败，会打印错误消息。

最后，你在 `StackTest_tests` 函数（57-68 行）中指定单元测试。这是在测试固件（fixtures）结构完成的。你定义了一个简单的数组，使用提供的函数和函数名称以便在发生故障时指示特定的测试。然后你在第 64-65 行创建了另一个结构，定义了测试、setup 函数、teardown 函数和固件（你的单元测试列表）。这个新结构（称为 `StackTest`）被返回给调用者，稍后将进行探讨。

### 列表 29.8 为 emunit 框架编写的单元测试（位于 CD-ROM 的 `./source/ch24/emb/stackTest.c`）

```c
1:   #include <embUnit/embUnit.h>

2:   #include <stdio.h>

3:   #include "stack.h"

4: 

5:   stack_t myStack;

6: 

7:   static void setup(void *)

8:   {

9:       printf("setup called.\n");

10:  }

11: 

12: 

13:  static void teardown(void *)

14:  {

15:      printf("teardown called.\n");

16:  }
```

#### 572 GNU/Linux 编程

```c
19:   static void testInit( void )

20:   {

21:       int ret;

22:

23:       ret = stackCreate(&myStack, 5 );

24:       TEST_ASSERT_EQUAL_INT( 0, ret );

25:   }

26: 

27: 

28:   static void testPushPop( void )

29:   {

30:       int ret, value;

31:

32:       ret = stackPush(&myStack, 55 );

33:       TEST_ASSERT_EQUAL_INT( 0, ret );

34:

35:       ret = stackPush(&myStack, 101);

36:       TEST_ASSERT_EQUAL_INT( 0, ret );

37:

38:       ret = stackPop(&myStack, &value );

39:       TEST_ASSERT_EQUAL_INT( 0, ret );

40:       TEST_ASSERT_EQUAL_INT( 101, value );

41:

42:       ret = stackPop(&myStack, &value );

43:       TEST_ASSERT_EQUAL_INT( 0, ret );

44:       TEST_ASSERT_EQUAL_INT( 55, value );

45:   }

46: 

47: 

48:   static void testStackDestroy( void )

49:   {

50:       int ret;

51:

52:       ret = stackDestroy(&myStack);

53:       TEST_ASSERT_EQUAL_INT( 0, ret );

54:   }
```

### 第29章 软件单元测试框架 573

```c
63:    };

64: EMBB_UNIT_TESTCALLER( StackTest, "StackTest",

65:        setUp, tearDown, fixtures);

66: 

67:    return (TestRef)&StackTest;

68: }
```

`EMBB_UNIT_TESTFIXTURES` 和 `EMBB_UNIT_TESTCALLER` 是宏，用于创建表示单个单元测试（固件）以及单元测试聚合体（`StackTest`）的特殊数组。

主程序提供了调用单元测试的方法（参见列表 29.9）。你包含 `embUnit` 头文件以汇集类型和符号。在第 3 行，你声明了前述函数，该函数创建了测试固件数组（回想列表 29.8 的第 57–68 行）。你调用 `Runner_start` 函数来初始化测试环境，然后使用你的单元测试初始化函数（`StackTest_tests`）调用 `Runner_runTest`。这将调用列表 29.8 中的所有单元测试。最后，你调用 `TestRunner_end`，它会输出有关单元测试的统计信息，包括运行次数和失败运行次数。

### 列表 29.9 Embunit 主程序（位于 CD-ROM 的 `.//source/ch24/emb/main.c`）

```c
1:    #include <embUnit/embUnit.h>

2:

3:    TestRef StackTest_tests( void );

4:

5:    int main(int argc, const char *argv[])

6:    {

7:        TestRunner_start();

8:        TestRunner_runTest(StackTest_tests());

9:        TestRunner_end();

10:    return 0;

11:}
```

在 Embunit 中构建单元测试只需将你的源文件与 Embunit 库编译并链接。要找到 Embunit 库，必须指定它的位置（以及头文件的位置）。构建和运行单元测试的操作所示：

```bash
# gcc -Wall -I/usr/local/src/embunit/ \ 
    -L/usr/local/src/embunit/lib \
    -o stackTest main.c stackTest.c -lembUnit
    ./stackTest
```

#### 574 GNU/Linux 编程

```
.setUp called.
testInit called
tearDown called.
.setUp called.
tearDown called.
.setUp called.
tearDown called.
```

```
OK (3 tests)
#
```
