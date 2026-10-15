
通过添加检查前置和后条件的语句，你可以进一步扩展错误检测阶段。这些是在函数开始和结束时应该是真的的假设。例如，如果一个函数期望一个非空指针，就检查这一点。对于在范围内的参数也是如此。标准 C 库支持断言的概念。断言被定义为应该是真的条件，描述了代码中所做的假设。它们被用于检查不应该发生的情况。

让我们看看断言的一个简单用法。如果我们是一个平方根函数，我们可能只想处理正参数。我们可能会记录该函数必须仅与正参数一起。我们断言参数是正数。C 库中的 `assert` 函数允许用直接的方法实现这种断言。这里有一个实现此功能的程序：

```c
#include <stdlib.h>
#include <assert.h>
#include <math.h>
#include <stdio.h>

double mysqrt(double x) {
 /* 断言的使用示例 */
    assert(x >= 0);
    return sqrt(x);
}

int main() {
    double value = -1.0;
    printf("mysqrt returns %g\n", mysqrt(value));
    exit(EXIT_SUCCESS);
}
```

函数 `mysqrt` 必须仅带正或零参数调用。`assert` 的调用表示表达式 `x >= 0` 在代码执行时必须始终成立。如果测试失败，我们的程序将立即停止。`assert` 函数的实际实现可能随系统而异；在 UNIX98 标准中，它实际上是一个宏。通常 `assert` 在结束程序并调用 `assert` 之前会打印消息。在我们 `main` 函数中的示例中，我们用负参数调用了 `mysqrt`。让我们编译并运行看看发生了什么。

```bash
gcc -o asserts asserts.c -lm
./asserts
```

```
assertions: asserts.c:9: mysqrt: Assertion 'x >= 0' failed.
```

## 调试 Bug

你可以看到 `assert` 函数已经检测到我们的测试失败了并打印了一条消息。这是一个断言失败。`Aborted` 消息来自 shell 的报告，表示我们的程序异常终止。如果断言没有失败（即在值为正数的情况下），`assert` 函数将什么都不做（除了求表达式的值）。

虽然断言在开发程序时非常有用，但在应用程序发布后，它们对用户并不友好。在出现问题后立即停止程序可能会给用户带来极大的不便。我们可能会在数据库中留下损坏的文件或无效的数据。让用户在退出之前保存他们的工作总是更好的。断言确实有其用武之地，特别是在记录代码中所做的假设方面。通过在包含 `#include <assert.h>` 之前定义 `NDEBUG` 可以禁用断言。这样做的效果是将 `assert` 函数变为什么都不做。这样，我们可以在源代码中保留断言，在开发和测试期间启用它们，并在发布后可能禁用它们（如果我们添加了错误恢复机制）。

与头文件不同，`assert.h` 设计为可以多次包含，在包含之前使用 `#define undef` 可以打开或关闭断言检查。

定义 `NDEBUG` 宏的一种简单方法是在编译器命令行上：

```
$ gcc -o asserts -NDEBUG asserts.c -lm

./asserts

mysqrt returns $
```

在这里我们看到 `assert` 并没有起作用，尽管我们知道测试将会失败。`sqrt` 函数被传入了一个负数参数并返回了一个无效结果。在这种情况下，使用了特殊值 `Nan` 来表示“不是数字”。调用了 `printf` 函数来显示此结果并打印了 `nan`。

断言对于监控可以描述为函数与其调用者之间“合同”的内容非常有用。函数用户必须通过函数内部断言中列出的条件来承诺。如果对函数返回结果使用断言，它的效果是确保函数在结果方面履行了其契约的一方。

## 你在何处？

大量的调试信息可能很有用，但也难以筛选，尽管采用一致的错误消息风格并审慎地使用 `grep` 可以有所帮助。

有时将信息量限制在关键点是合适的，也许当发生错误时。在这种情况下，了解更多关于错误是如何产生的可能会有所帮助。我们想知道程序到达这一点所经过的路径。在启用了完全调试信息的情况下，这是可能的，但我们可以实现一个工具，告诉我们我们在哪里，而不会产生堆积的信息。

这个想法非常简单。如果我们向程序中添加一些追踪功能并进行记录，我们就可以在需要时打印它们。让我们来看一种可能的实现。在我们编写程序时，我们将为每个函数添加对 `trace` 函数的调用。我们在进入函数时调用一个函数，在离开函数时调用另一个。我们将使用宏，这样就可以像以前一样捕获文件名和函数名，但这次我们不再打印它们，而是将它们记录在栈中，并在代码返回时将其移除。用例子说明可能更容易。我们想写出这样的代码：

```
int main() {

    trace_in();

    function();

    trace_out();

}

void function() {

    trace_in();

    if(error) {

        trace_print();

    }

    trace_out();

}
```

当发生错误且我们调用 `trace_print` 时，我们希望看到类似这样的输出：

因此我们可以看到我们通过 `main` 中的调用进入了 `function`。这在效果上等于如果我们在调试器控制下运行程序并在错误发生的地方设置断点，从调试器器获取的堆栈跟踪。但在这里，我们不需要使用调试器，也不需要停止程序。

追踪日志功能的简单实现可能如下：

```c
#include <stdio.h>
#include <assert.h>
#include <signal.h>
void handle_signal(int sig) {
    trace_print();
}
#define debug_db(x) if (debug && DEBUG_DB) {
    fprintf(stderr, "DB: %s (%d), %d\n", __FILE__, __LINE__);
    fprintf(stderr, "in %s\n", __PRETTY_FUNCTION__);
}
#define DEBUG_DB 1
int trace_idx = 0;
#define TRACE_STACK 100
char *trace_stack[TRACE_STACK];
#define stringify(x) str2(x)
```

```
#define str2(x) #x
#define trace_in()
{
    assert(trace_idx < TRACE_STACK);
    trace_stack[trace_idx++] = __FILE__ ":" __LINE__ ":";
    __PRETTY_FUNCTION__ = "in\n";
}
#define trace_out()\
{
    trace_idx--;
}
trace_print(){
    int idx = 0;
    while(idx < trace_idx) {
        fprintf(stderr, trace_stack[idx++]);
    }
}
```

我们为栈留留了 100 个空间，之后程序将由于断言失败而终止。这种深度对于大多数程序应该是足够的。如果超过了栈，可能程序陷入了递归循环，或者在一个没有包含 `trace_out` 用的函数中。事实上，为了检测循环，在中止之前打印栈可能会更好！

另一种实现方法可以选择记录最后 100 次 `trace_in` 记录，而不是使用简单的栈。这将列出最近进入的函数。最后，对于这一节，我们可以考虑让出错程序交出秘密，而无需预先决定想知道什么。如果我们安排在程序中捕获信号，可以使用它让程序告诉我们在哪里。

```c
#include <signal.h>
void handle_signal(int sig) {
    trace_print();
}
int main() {
    struct sigaction act;
    act.sa_handler = handle_signal;
    sigemptyset(&act.sa_mask);
    act.sa_flags = 0;
    sigaction(SIGUSR1, &act, 0);
}
```

# 第 6 章

如果我们想知道程序在忙碌时在哪里，可以向它发送信号，它就会忠实地报告位置。

```
$ ./debug & 
[11] 1835
$ kill -USR1 1835
debug.c: main in
debug.c: function in
```
