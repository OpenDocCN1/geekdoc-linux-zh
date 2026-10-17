
除非你需要 `threading` 模块中更强大的 OOP 工具和功能，否则选择在很大程度上取决于程序员和编程团队的偏好，以及编程设计目标/方法。我们在第 16.4.5 节中介绍 `threading` 模块提供的一些函数。

基本的 `thread` 模块不强制 OOP，如果你习惯于函数式编程，则非常易于使用。如前所述，`thread` 模块在 Python 3 中已重命名为 `_thread`。

该模块为处理共享其全局数据空间的多个控制线程（也称为轻量级进程或任务）提供了低级原语。对于同步，提供了简单的锁（也称为互斥锁）。

### 16.4.4.1.1 thread 函数参考

`thread` 模块定义了以下常量和函数：

```
exception thread.error: Raised on thread-specific errors.
```

```
thread.LockType: This is the type of lock object.
```

`thread.start_new_thread(function, args[, kwargs])`: 启动一个新线程并返回其标识符。线程执行名为 `function` 的函数，并使用参数列表 `args`（必须是元组）。可选的 `kwargs` 参数指定关键字参数的字典。当函数返回时，线程静默退出。当函数因未处理的异常而终止时，会打印堆栈跟踪，然后线程退出（但其他线程继续运行）。

`thread.interrupt_main()`: 在主线程中引发 `KeyboardInterrupt` 异常。子线程可以使用此函数中断主线程。

`thread.exit()`: 引发 `SystemExit` 异常。如果未捕获，这将导致线程静默退出。

`thread.allocate_lock()`: 返回一个新的锁对象。锁的方法稍后描述。锁初始时为未锁定状态。

`thread.get_ident()`: 返回当前线程的“线程标识符”。这是一个非零整数。其值没有直接含义；它旨在用作魔术 cookie，例如用于索引线程特定数据的字典。线程标识符在线程退出并创建另一个线程时可能会被回收。

`thread.stack_size([size])`: 返回创建新线程时使用的线程栈大小。

`Lock` 对象具有以下方法：

`lock.acquire([waitflag])`: 如果没有可选参数，此方法无条件地获取锁，如果必要则等待直到被其他线程释放（一次只有一个线程可以获取锁——这就是它们存在的原因）。

`lock.release()`: 释放锁。锁必须先前已被获取，但不一定是同一线程。

`lock.locked()`: 返回锁的状态：如果已被某个线程获取则返回 `True`，否则返回 `False`。

由于基本线程模块比下一小节中稍后介绍的更高级的 `threading` 模块要简单一些，我们先给出它的示例。该模块为平台上可用的任何线程系统提供可移植接口：其接口在 PC-BSD 和 Solaris 上以相同的方式工作，以及在安装了 `pthreads` POSIX 线程实现（包括 Linux 等）的任何系统上。Python 脚本使用 Python `thread` 模块可在所有这些平台上工作而无需更改源代码。

## 16.4.4.1.2 Examples

让我们从实验一个部署主线程接口的脚本开始。

示例 16.52 中的脚本一次只启动一个线程，直到你在控制台输入 `x` 然后按 `<Enter>` 为止：

# Example 16.52

```
import thread
def child(tid):
    print('Started thread', tid)
def parent():
    i = 0
    while 1:
        i += 1
        thread.start_new_thread(child, (i,))
        if raw_input() == 'x': break
parent()
% python Example16_52.py
Started thread 1
Started thread 2
Started thread 3
Started thread 4
x
%
```

示例 16.52 中到底发生了什么？启动了一个线程，然后它立即死亡，程序无限循环，允许你创建连续的新线程。此示例中只做了两次线程调用：导入 `thread` 模块和创建线程的调用。要启动一个线程，请调用 `thread.start_new_thread` 函数。此调用将一个函数（或其他可调用对象）作为元组参数，并启动一个新线程以执行对所传函数的调用并使用所传参数。

下面是另一个示例，它迭代创建同时存在、并行运行的新线程：

# Example 16.53

```
import thread, time
def counter(myId, count):    # function that will run in each
                            thread
    for i in range(count):
        time.sleep(1)           # simulate useful code here
        print '[%s] => %s' % (myId, i)
for i in range(5):            # call start_new_thread 5 times
    thread.start_new_thread(counter, (i, 3)) # loop the newest
                                            thread 3 times
time.sleep(5)                 # prevents exit from parent too
                              early
print 'Main thread exiting.'  # all threads are destroyed by
                              default
```

当我们执行此脚本文件时，我们得到：

```
% python Example16_53.py
[4] => 0
[2] => 0
[1] => 0
[3] => 0
[0] => 0
[0] => 1
[4] => 1
[1] => 1
[2] => 1
[3] => 1
[2] => 2
[4] => 2
[3] => 2
[0] => 2
[1] => 2
Main thread exiting.
%
```

`Example 16.53` 到底发生了什么？创建并同时运行了五个线程。在每个线程内部，计数器值从 0 到 4 被打印到标准输出。函数 `counter` 中的 `time.sleep(1)` 方法用于模拟可能用于执行某些系统编程任务的代码。

## EXERCISE 16.17

如果 `Example 16.52` 中启动的每个线程都要执行某些操作，你会在给定代码的哪一行之后放置执行该工作的代码行？

## EXERCISE 16.18

在所示的 `Example 16.53` 的输出中，你会注意到打印的 `myId` 变量的值的顺序并不总是相同的。为什么会这样？

## EXERCISE 16.19

如果你多次运行 `Example16_53.py`，每次连续运行程序时打印的 `myId` 的顺序是否相同？为什么会或不会？

## 16.4.4.2 Python Thread Example Using the OOP Model

`threading` 模块在低级 `thread` 模块之上构建了更高级别的线程接口。如果你希望你的应用程序更好地利用多核机器的计算资源，建议你使用 `multiprocessing` 模块。然而，

如果希望同时运行多个 I/O 密集型任务，`threading` 仍然是一个合适的模型。

### 16.4.4.2.1 threading Functions Reference

`threading` 模块定义了以下函数和对象：

```
threading.active_count()
```

```
threading.activeCount()
```

返回当前存活的线程对象的数量。返回的计数等于 `enumerate()` 返回的列表的长度。

```
threading.Condition()
```

一个工厂函数，返回一个新的条件变量对象。条件变量允许一个或多个线程等待，直到被另一个线程通知。

```
threading.current_thread()
```

```
threading.currentThread()
```

返回当前线程对象，对应于调用者的控制线程。

```
threading.enumerate()
```

返回当前存活的所有线程对象的列表。该列表包括守护线程、由 `current_thread()` 创建的虚拟线程对象以及主线程。它不包括已终止的线程和尚未启动的线程。

```
threading.Event()
```
