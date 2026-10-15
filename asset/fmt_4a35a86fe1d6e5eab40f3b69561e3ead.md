
**图 23.16** | 使用 `ArrayBlockingQueue` 创建同步缓冲区。

# 第 23 章 多线程

`set` 方法中的第 17 行（15–20 行）调用了 `ArrayBlockingQueue` 对象的 `put` 方法。该方法在必要时会阻塞，直到缓冲区有空间放置该值。`get` 方法（23–32 行）调用了 `ArrayBlockingQueue` 对象的 `take` 方法（第 27 行）。该方法在必要时会阻塞，直到缓冲区中有元素。第 18–19 行和 28–29 行使用 `ArrayBlockingQueue` 对象的 `size` 方法显示 `ArrayBufferTest` 中当前元素的总数。（图 23.17）包含一个启动程序的 `main` 方法。第 11 行创建了一个 `ExecutorService`，第 14 行创建了一个 `BlockingBuffer` 对象并将引用赋值给共享变量 `sharedLocation`。第 16–17 行执行了生产者和消费者 `Runnable`。注意，虽然 `ArrayBlockingQueue` 的 `put` 和 `take` 方法经过了适当的同步，但 `BlockingBuffer` 的 `set` 和 `get` 方法（图 23.16）并未声明为 `synchronized`。`set` 方法中的语句——`put` 操作（第 19 行）和输出（第 20–21 行）不是原子的；`take` 操作（第 36 行）和输出（第 37–38 行）也是。因此，无法保证每次输出都会在相应的 `put` 或 `take` 操作后立即发生，输出可能会出现乱序。即使如此，`ArrayBlockingQueue` 对象也对数据的访问进行了适当的同步，这一点从消费者读取的值之和始终是正确的得到了证明。

```java
// Fig 23.17: BlockingBufferTest.java
// 两个线程操作一个阻塞缓冲区。
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
public class BlockingBufferTest {
    public static void main(String[] args) {
        // 创建带有两个线程的新线程池
        ExecutorService application = Executors.newCachedThreadPool();
        // 创建 BlockingBuffer 来存储 int
        Buffer sharedLocation = new BlockingBuffer();
        application.execute(new Producer(sharedLocation));
        application.execute(new Consumer(sharedLocation));
        application.shutdown();
    } // end main
} // end class BlockingBufferTest
```

| 生产者写入 | 1 | 缓冲区占用单元: 1 |
| :--- | :--- | :--- |
| 消费者读取 | 1 | 缓冲区占用单元: 0 |
| 生产者写入 | 2 | 缓冲区占用单元: 1 |
| 消费者读取 | 2 | 缓冲区占用单元: 0 |

图 23.17 | 两个线程操作一个阻塞缓冲区。（2 部分中的第 I 部分。）

| 生产者写入 | 3 | 缓冲区占用单元: 1 |
| :--- | :--- | :--- |
| 消费者读取 | 3 | 缓冲区占用单元: 0 |
| 生产者写入 | 4 | 缓冲区占用单元: 1 |
| 消费者读取 | 4 | 缓冲区占用单元: 0 |
| 生产者写入 | 5 | 缓冲区占用单元: 1 |
| 消费者读取 | 5 | 缓冲区占用单元: 0 |
| 生产者写入 | 6 | 缓冲区占用单元: 1 |
| 消费者读取 | 6 | 缓冲区占用单元: 0 |
| 生产者写入 | 7 | 缓冲区占用单元: 1 |
| 消费者读取 | 7 | 缓冲区占用单元: 0 |
| 生产者写入 | 8 | 缓冲区占用单元: 1 |
| 消费者读取 | 8 | 缓冲区占用单元: 0 |
| 生产者写入 | 9 | 缓冲区占用单元: 1 |
| 消费者读取 | 9 | 缓冲区占用单元: 0 |
| 生产者写入 | 10 | 缓冲区占用单元: 1 |

生产者完成生产
终止生产者
消费者读取 10 缓冲区占用单元: 0

消费者读取值总和为 55
终止消费者

**图 23.17** | 两个线程操作一个阻塞缓冲区（2 部分中的第 II 部分。）

## 23.8 带同步的生产者/消费者关系

上一个示例展示了如何使用 `ArrayBlockingQueue` 类以线程安全的方式让多个线程共享单个缓冲区，该类封装了共享数据所需的同步。出于教学目的，我们解释了如何使用 `synchronized` 关键字自己实现一个共享缓冲区。使用 `ArrayBlockingQueue` 将产生更具维护性且性能更好的代码。

同步缓冲区访问的第一步是将方法并存 `set` 设置为 `synchronized` 方法。这要求线程在尝试访问数据之前获取 `Buffer` 的监视锁（monitor lock），但这不能确保与生产者/消费者关系相关的状态依赖问题。我们必须确保有一种允许线程等待的方法，取决于某些条件是否为真。在向缓冲区中放入新项的情况下，允许操作继续的条件是缓冲区未满。在从缓冲区获取项的情况下，允许操作继续的条件是缓冲区不空。如果条件为真，操作可以进行；如果为假，线程必须等待直到该条件变为真。当线程在某个条件上等待时，它将从处理器的竞争中被移除，放入对象的等待队列中并持有锁。

### wait, notify 和 notifyAll 方法

`wait`、`notify` 和 `notifyAll` 方法在 `Object` 类中声明并被所有其他类继承，可以结合条件使用，让线程在无法执行任务时等待。如果线程获取了对象的监视锁，它发现可以继续执行任务，直到满足某些条件，此时线程可以调用 `Object wait()`；这会释放对象的锁，线程并在等待状态等待，而其他线程尝试进入对象的同步状态或方法。当执行 `synchronized` 语句（或方法）的线程完成或满足了另一个线程可能正在等待的条件时，它可以调用 `notify` 方法允许等待的线程重新变为可运行（runnable）状态。此时，从等待状态转换为可运行状态的线程可以尝试重新获取对象的监视锁。即使它能够重新获取监视锁，此时它也可能无法执行其任务——以防线程保持等待状态并隐式地释放了监视锁。如果线程调用 `notifyAll()`，所有等待监视锁的线程都将变得请求锁（即它们都转变为可运行状态）。记住，同一时间只有一个线程可以获取对象的监视锁——其他尝试获取相同监视锁的线程将被阻塞，直到锁再次可用（即，直到没有其他线程在 true对象上执行 `synchronized` 语句）。

#### 常见编程错误 23.1

如果线程在没有获取该对象锁的情况下对对象执行 `wait`、`notify` 或 `notifyAll`，这是一个错误。这会导致 `IllegalMonitorStateException`。

#### 错误预防提示 23.1

使用 `notify` 让等待线程变为可运行是一种良好的做法。这样做避免了你的程序忘记等待线程的可能性，这会导致饥饿。

图 23.18 和 23.19 中的应用程序演示了使用同步共享缓冲区的生产者和消费者。在这种情况下，生产者首先产生一个值，消费者只有在生产者产生值且在消费者了上一个（或第一个）值后正确产生下一个值后进行消费。我们重用了 23.6 节示例中的 `Buffer` 接口以及生产者和消费者类。同步工作在 `SynchronizedBuffer` 类的 `set` 和 `get` 方法中处理（图 23.18），该类实现了 `Buffer` 接口（第 4 行）。因此，生产者和消费者的运行 方法简单地调用共享对象的同步 `set` 和 `get` 方法。

```java
// Fig 23.18: SynchronizedBuffer.java
// 使用 Object 方法 wait 和 notify 同步共享数据。
public class SynchronizedBuffer implements Buffer {
    private int buffer = -1; // 生产者和消费者线程共享
    private boolean occupied = false; // 缓冲区是否被占用
    // 将值放入缓冲区
    public synchronized void set(int value ) {
```

## 23.8 生产者/消费者关系与同步

```java
// 当没有空位置时，将线程置于等待状态
```
