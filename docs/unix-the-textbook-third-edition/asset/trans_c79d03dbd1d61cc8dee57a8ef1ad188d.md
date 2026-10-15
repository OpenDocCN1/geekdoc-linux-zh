

```
cv.notify()
```

```
cv.release()
```

在选择 `notify()` 和 `notifyAll()` 之间时，请考虑一次状态变化是否只对一个或多个等待线程感兴趣。在典型的生产者-消费者情况下，向缓冲区添加一项只需要唤醒一个消费者线程。

下面是用于实现此目的的方法列表。

```
threading.Condition()
```

一个工厂函数，返回一个新的条件变量对象。条件变量允许一个或多个线程等待，直到被另一个线程通知。

```
acquire(*args)
```

获取底层锁。此方法调用底层锁上的相应方法；返回值是该方法返回的内容。

```
release()
```

释放底层锁。此方法调用底层锁上的相应方法；没有返回值。

```
wait([timeout])
```

等待直到被通知或超时发生。如果调用此方法的线程尚未获取锁，则会引发 RuntimeError。

唤醒所有等待此条件的所有线程。此方法与 `notify()` 类似，但唤醒所有等待线程而不是一个。如果调用此方法的线程尚未获取锁，则会引发 RuntimeError。

## 16.4.5.3 一个示例

下面的 Python 代码将本章的许多思想和语法结构结合起来，以说明多线程程序中生产者-消费者问题的 Python 解决方案。它使用 OOP 部署 `threading` 模块及其方法来启动两个线程，Producer 和 Consumer。这些线程相互通信并共享条件变量的状态，我们将其方便地命名为 `condition`。

示例 16.55 到底发生了什么？程序布局的主要块的简要说明，以及代码运行核心的描述如下：

Block 1：这是程序的初始化部分，其中导入了 `threading` 模块、子模块 `Thread` 和类 `Condition`。此外，变量 `buffer` 和 `condition` 被初始化。变量 `condition` 源自 `Condition` 类，因此可以使用该类的 方法。

Block 2：这定义了派生自 `Thread` 模块的类 `Producer`。它还指定，在一个确定的重复循环中，我们将多少次向缓冲区添加数据。在此示例中，我们只向缓冲区添加确定数量的数据对象。`Producer` 中使用条件变量的机制在此得到解释。

Block 3：这定义了派生自 `Thread` 模块的类 `Consumer`。数据如何从缓冲区中移除也被指定。`Consumer` 中使用条件变量的机制在此得到解释。

Block 4：`Producer` 启动，然后 `Consumer` 启动。

此程序的关键执行顺序，以及它如何实现其目标，描述如下：

- 0. `Producer` 线程将数据放入缓冲区并在条件实例上调用 `notify()` 方法。
- 1. `Consumer` 线程在消费前检查缓冲区是否为空。
- 2. 如果缓冲区为空，则在条件实例上调用 `wait()` 方法。
- 3. `wait()` 方法阻塞 `Consumer` 线程并同时释放与条件关联的锁。此锁由 `Consumer` 线程持有，因此它失去了对锁的持有。
- 4. 除非 `Consumer` 线程被通知，否则它将不会运行。
- 5. `Producer` 线程可以获取锁，因为锁已被 `Consumer` 线程释放。
- 6. `Producer` 线程将数据放入缓冲区并在条件实例上调用 `notify()` 方法。
- 7. 一旦在条件上完成 `notify()` 方法，`Consumer` 线程会被唤醒但不执行。
- 8. `notify()` 方法不会释放锁。即使在 `notify()` 之后，锁仍由 `Producer` 持有。
- 9. `Producer` 线程通过使用 `condition.release()` 显式释放锁。
- 10. `Consumer` 线程再次开始运行。回到步骤 0。

请在我们接下来展示的代码中追踪这 11 个步骤：

### Example 16.55

```
from threading import Thread, Condition        #Block 1.
import time
import random
buffer = []
MAX_NUM = 10
condition = Condition()

class Producer(Thread):                        #Block 2.
    def run(self):
        global buffer
        for i in range(10):
            condition.acquire()
            if len(buffer) == MAX_NUM:
                print "Queue full, Producer waiting"
                condition.wait()
                print "Queue empty, Producer notified"
            buffer.append(i)
            print "Data Produced", i
            condition.notify()
            condition.release()
            time.sleep(random.random())

class Consumer(Thread):                        #Block 3.
    def run(self):
        global buffer
        for i in range(10):
            condition.acquire()
            while not buffer:
                print "Queue empty, Consumer waiting"
                condition.wait()
                print "Data added to queue, Consumer notified"
```
