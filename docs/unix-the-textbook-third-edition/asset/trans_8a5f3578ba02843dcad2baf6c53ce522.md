

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

Example 16.53 到底发生了什么？创建并同时运行了五个线程。在每个线程内部，计数器值从 0 到 4 被打印到标准输出。函数 counter 中的 time.sleep(1) 方法用于模拟可能用于执行某些系统编程任务的代码。

## EXERCISE 16.17

如果 Example 16.52 中启动的每个线程都要执行某些操作，你会在给定代码的哪一行之后放置执行该工作的代码行？

## EXERCISE 16.18

在所示的 Example 16.53 的输出中，你会注意到打印的 myId 变量的值的顺序并不总是相同的。为什么会这样？

## EXERCISE 16.19

如果你多次运行 Example16_53.py，每次连续运行程序时打印的 myId 的顺序是否相同？为什么会或不会？

## 16.4.4.2 Python Thread Example Using the OOP Model

threading 模块在低级 thread 模块之上构建了更高级别的线程接口。如果你希望你的应用程序更好地利用多核机器的计算资源，建议你使用 multiprocessing 模块。然而，

如果希望同时运行多个 I/O 密集型任务，threading 仍然是一个合适的模型。

### 16.4.4.2.1 threading Functions Reference

threading 模块定义了以下函数和对象：

```
threading.active_count()
```

```
threading.activeCount()
```

返回当前存活的线程对象的数量。返回的计数等于 enumerate() 返回的列表的长度。

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

返回当前存活的所有线程对象的列表。该列表包括守护线程、由 current_thread() 创建的虚拟线程对象以及主线程。它不包括已终止的线程和尚未启动的线程。

```
threading.Event()
```

一个工厂函数，返回一个新的事件对象。事件管理一个标志，可以通过 set() 方法设置为 true，并通过 clear() 方法重置为 false。wait() 方法会阻塞直到标志为 true。

```
class threading.local
```

表示线程本地数据的类。这些是值特定于线程的数据。要管理线程本地数据，只需创建一个 local 的实例（或其子类）并在其上存储属性，例如：

```
mydata = threading.local()
mydata.x = 1
```

实例的值对于不同的线程是不同的。

```
threading.Lock()
```

一个工厂函数，返回一个新的原始锁对象。一旦线程获取了它，后续获取尝试将被阻塞，直到它被释放；任何线程都可以释放它。

```
threading.RLock()
```

一个工厂函数，返回一个新的可重入锁对象。

```
threading.Semaphore([value])
```

一个工厂函数，返回一个新的信号量对象。

```
threading.BoundedSemaphore([value])
```

一个工厂函数，返回一个新的有界信号量对象。

```
class threading.Thread
```

表示控制线程的类。该类可以以有限的方式安全地进行子类化。

```
class threading.Timer
```

一个在指定间隔过去后执行函数的线程。

```
threading.settrace(func)
```

为从 threading 模块启动的所有线程设置跟踪函数。函数 func 将在每个线程的 run() 方法被调用之前传递给 sys.settrace()。

```
threading.setprofile(func)
```

为从 threading 模块启动的所有线程设置分析函数。函数 func 将在每个线程的 run() 方法被调用之前传递给 sys.setprofile()。

```
threading.stack_size([size])
```

返回创建新线程时使用的线程堆栈大小。

```
exception threading.ThreadError
```

因各种线程相关错误而引发，如下所述。

### 16.4.4.2.2 Thread Class Objects

threading 模块的 Thread 类提供了适用于接下来介绍的多线程示例的方法，并且通常适用于所有基于 Python OOP 的线程同步

