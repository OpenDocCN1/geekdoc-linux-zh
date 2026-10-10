
# 342 14. 多线程

`ThreadDialog` 声明了两个 `Thread` 类型变量以及一些按钮以提供基础的用户界面。

```cpp
ThreadDialog::ThreadDialog(QWidget *parent)
    : QDialog(parent)
{
    threadA.sendMessage("A");
    threadB.sendMessage("B");
    
    threadButton = new QPushButton(tr("Start A"));
    threadButton = new QPushButton(tr("Start B"));
    quitButton = new QPushButton(tr("Quit"));
    quitButton->setDefault(true);
    
    connect(threadButton, SIGNAL(clicked()), this, SLOT(startStopThreadA()));
    connect(threadButton, SIGNAL(clicked()), this, SLOT(startStopThreadB()));
    
    ...
}
```

在构造函数中，我们调用 `sendMessage()` 让第一个线程不断打印 'A'，让第二个线程打印 'B'。

```cpp
void ThreadDialog::startStopThreadA()
{
    if (threadA.isRunning()) {
        threadA.stop();
        threadButton->setText(tr("Start A"));
    } else {
        threadA.start();
        threadButton->setText(tr("Stop A"));
    }
}
```

当用户点击线程 A 的按钮时，`startOrStopThreadA()` 如果线程正在运行时停止它，否则会启动它。它还会更新按钮的文本。

```cpp
void ThreadDialog::startStopThreadB()
{
    if (threadB.isRunning()) {
        threadB.stop();
        threadButton->setText(tr("Start B"));
    } else {
        threadB.start();
        threadButton->setText(tr("Stop B"));
    }
}
```

`startStopThreadB()` 的代码在结构上完全相同。

```cpp
void ThreadDialog::closeEvent(QCloseEvent *event)
{
    threadA.stop();
    threadB.stop();
    threadA.wait();
    threadB.wait();
    event->accept();
}
```

## 创建线程 343

如果用户点击 Qt 或关闭窗口，我们会停止任何正在运行的线程，并等待它们完成（使用 `QThread::wait()`），然后再调用 `QCloseEvent::accept()`。这确保了应用程序以干净的状态退出，尽管在本文示例中这并不重要。

如果你运行应用程序并点击 "Start A"，控制台将充满 'A'。如果你点击 "Start B"，它现在将充满交替顺序的 'A' 和 'B' 序列。点击 "Stop A"，现在它将只打印 'B'。

## 同步线程

多线程应用程序的一个常见需求是同步多个线程。Qt 提供了以下同步类：`QMutex`、`QReadWriteLock`、`QSemaphore` 和 `QWaitCondition`。

`QMutex` 类提供了一种保护变量或代码段的方法，使得一次只有一个线程访问它。该类提供了一个 `lock()` 函数来锁定互斥锁。如果互斥锁未解锁，当前线程将获取并锁定它；否则，当前线程将被阻塞，直到持有互斥锁的线程解锁它。... 调用 `unlock()`。`QMutex` 类还提供了一个 `tryLock()` 函数，如果互斥锁已锁定，它将立即返回。

例如，假设我们想用 `QMutex` 保护上一节中 `Thread` 类的 `stopped` 变量。我们在 `Thread` 中添加以下成员变量：

```cpp
private:
    ...
    QMutex mutex;
};
```

`run()` 函数将更改为：

```cpp
void Thread::run()
{
    mutex.lock();
    if (stopped) {
        stopped = false;
        mutex.unlock();
        break;
    }
    mutex.unlock();
    std::cerr << QPrintable(messageStr);
    std::cerr << std::endl;
}
```

`stop()` 函数将变成：

```cpp
void Thread::stop()
{
    mutex.lock();
    stopped = true;
    mutex.unlock();
}
```

在复杂函数或抛出异常的函数中锁定和解锁互斥锁很容易出错。Qt 提供了 `QLocker` 类来简化互斥锁的处理。`QLocker` 的构造函数接受一个 `QMutex` 并锁定它。`QLocker` 的析构函数解锁互斥锁。例如，我们可以这样重写 `run()` 和 `stop()` 函数：

```cpp
void Thread::run()
{
    QLocker locker(&mutex);
    if (stopped) {
        stopped = false;
        break;
    }
    std::cerr << QPrintable(messageStr);
}

void Thread::stop()
{
    QLocker locker(&mutex);
    stopped = true;
}
```

使用互斥锁的问题是时间只有一个线程可以访问变量。在许多尝试读取同一变量（但不修改）的程序中，互斥锁可能会成为瓶颈。在这种情况下，可以使用 `QReadWriteLock`，这是一种允许在不影响性能的同时读取的同步类。

在 `Thread` 类中，用 `QReadWriteLock` 替换 `QMutex` 来保护变量没有意义，因为一次最多只有一个线程尝试读取变量。更合适的示例涉及一个或多个读取者访问某些数据，以及一个或多个写入者修改数据：

```cpp
QReadWriteLock lock;

void ReaderThread::run()
{
    lock.lockForRead();
    access_data_without_modifying(&data);
    lock.unlock();
}

void WriterThread::run()
{
    lock.lockForWrite();
    modify_data(&data);
    lock.unlock();
}
```

为了方便起见，我们可以使用 `QSemaphore` 类。`QSemaphore` 是互斥锁的另一种泛化，但与读写锁不同，信号量可以保护特定数量的资源。以下两个代码段显示了 `QSemaphore` 和 `QMutex` 的对应关系：

- `QSemaphore semaphore(1);`
    `semaphore.acquire();`
    `semaphore.release();`
- `QMutex mutex;`
    `mutex.lock();`
    `mutex.unlock();`

通过向构造函数传递 1，我们告诉信号量它控制单个资源。使用信号量的优势是我们可以向构造函数传递 1 外的数字，然后多次调用 `acquire()` 来获取资源。信号量的典型应用是在使用特定大小的缓冲区（`BufferSize`）在两个线程之间传输特定的数据（`DataSize`）：

```cpp
const int DataSize = 10000;
const int BufferSize = 4096;
char buffer[BufferSize];
```

生产者线程向缓冲区写入数据直到末尾，然后从头重新开始覆盖现有数据。消费者线程在数据生成时读取它。图 14.2 说明了这一点，假设使用 16 字节的缓冲区。

![](img/930c1c6fda99d425284503ebcbc940ea_367_0.png)

图 14.2. 生产者-消费者模型

# 14. 多线程

生产者-消费者示例的需求有两个：

如果生产者生成数据太快，会覆盖消费者尚未读取的数据；如果消费者读取数据太快，会跳过生产者并读取垃圾数据。

解决此问题的简单方法是让生产者填充缓冲区，然后等待消费者读取整个缓冲区，以此类推。然而，在多处理器机器上，这不如让生产者消费者线程同时操作缓冲区的不同部分快。

解决问题的一种方法涉及两个信号量：

```cpp
QSemaphore freeSpace(BufferSize);
QSemaphore usedSpace(0);
```

`freeSpace` 信号量控制生产者可以填充的缓冲区部分。`usedSpace` 信号量控制消费者可以读取的区域。这两个区域是互补的。`freeSpace` 信号量初始化为 `BufferSize` (4096)，意味着有很多可以可以。当应用程序启动时，读取线程将开始获取“空”字节并将其转换为“已用”字节。`usedSpace` 信号量初始化为 0，以确保消费者启动时不会读取垃圾数据。

对于此示例，每个字节算一个资源。在实际应用中，我们可能会一次处理较大的单元（例如 64 或 256 字节），以减少信号量相关的开销。

```cpp
void Producer::run()
{
    for (int i = 0; i < DataSize; i++) {
        freeSpace.acquire();
        buffer[i % BufferSize] = "ACGT"[uint](std::rand()) % 4];
        usedSpace.release();
    }
}
```

在生产者中，每次迭代都从获取一个“空”字节开始。如果缓冲区满了消费者尚未读取的数据，`acquire()` 的调用将阻塞直到消费者开始消耗数据。一旦我们获取了缓冲区，就会用一些随机数据（'A', 'C', 'G' 或 'T'）填充它，并将缓冲区释放为“已用”，这样消费者就可以读取它。

```cpp
void Consumer::run()
{
    for (int i = 0; i < DataSize; ++i) {
        usedSpace.acquire();
        std::cerr << buffer[i % BufferSize];
        freeSpace.release();
    }
    std::cerr << std::endl;
}
```

346

# 线程同步 347

在消费者中，我们首先获取一个“已使用”的字节。如果缓冲区中没有数据可读，`acquire()` 调用将阻塞，直到生产者生成了一些数据。一旦我们获取了该字节，就会将其打印并将其释放为“空闲”，以便生产者再次向其填充数据。

```cpp
int main()
{
    Producer producer;
    Consumer consumer;
    producer.start();
    consumer.start();
    producer.wait();
    consumer.wait();
    return 0;
}
```

最后，在 `main()` 中，我们启动了生产者和消费者线程。然后生产者将一些“空闲空间”转换为“已使用空间”，而消费者可以将其转换回“空闲空间”。

当我们运行程序时，它会向控制台写入序列 100,000 个随机的 'A'、'C'、'G' 和 'T'，并退出。为了理解发生了什么，我们可以禁用输出，改为在每次生产者生成字节时写入 'P'，在每次消费者读取字节时写入 'C'。为了尽可能易跟随，我们可以对 `DataSize` 和 `BufferSize` 使用较小的值。

例如，存在一种 `DataSize` 为 10 且 `BufferSize` 为 4 的可能运行情况：`PcPcPcPcPcPc`。在这种情况下，消费者在生产者生成字节时立即读取它们；两个线程以相同的速度执行。另一种可能性是生产者在消费者开始读取之前填满了整个缓冲区：`"PPPPccccPPPPPccccPPc"`。还有许多其他可能性。信号量为特定于系统的调度器提供了很大的灵活性，调度器可以研究线程的行为并选择合适的调度策略。

同步生产者和消费者的另一种方法是使用 `WaitCondition` 和 `QMutex`。`WaitCondition` 允许线程在某些条件满足时唤醒其他线程。这比仅使用互斥量更精确的控制。为了展示它是如何工作的，我们将使用等待条件重做生产者示例。

```cpp
const int DataSize = 100000;
const int BufferSize = 4096;
char buffer[BufferSize];
```

```cpp
WaitCondition bufferIsNotFull;
WaitCondition bufferIsEmpty;
QMutex mutex;
int usedSpace = 0;
```

# 348 14. 多线程

除了缓冲区外，我们还声明了两个 `QWaitConditions`、一个 `QMutex` 以及一个存储缓冲区中“已使用”字节数的变量。

```cpp
void Producer::run() {
    for (int i = 0; i < DataSize; ++i) {
        mutex.lock();
        while (usedSpace == BufferSize)
            bufferIsNotFull.wait(&mutex);
        buffer[i % BufferSize] = "ACGT"(int(std::rand()) % 4);
        ++usedSpace;
        bufferIsEmpty.wakeAll();
        mutex.unlock();
    }
}
```

在生产者中，我们首先检查缓冲区是否已满。如果是，则在“缓冲区未满”条件上等待。当条件满足时，我们向缓冲区写入一个字节，增加 `usedSpace`，并唤醒任何等待“缓冲区不空”条件变为真的线程。

我们使用一个互斥量来保护对 `usedSpace` 变量的所有访问。`QCondition::wait()` 函数可以接受锁定的互斥量作为第一个参数，它会在阻塞当前线程之前解锁，并在返回之前重新锁定。

对于这个示例，我们可以将 `while` 循环

```cpp
while (usedSpace == BufferSize)
    bufferIsNotFull.wait(&mutex);
```

替换为此语句：

```cpp
if (usedSpace == BufferSize) {
    mutex.unlock();
    bufferIsNotFull.wait();
    mutex.lock();
}
```

然而，这将会失效，因为我们允许存在多个生产者线程，由于另一个生产者可以在 `wait()` 调用后立即夺取互斥量，并使“缓冲区未满”条件再次变为假。

```cpp
void Consumer::run() {
    for (int i = 0; i < DataSize; ++i) {
        mutex.lock();
        while (usedSpace == 0)
            bufferIsEmpty.wait(&mutex);
        std::cerr << buffer[i % BufferSize];
        --usedSpace;
        bufferIsNotFull.wakeAll();
        mutex.unlock();
    }
    std::cerr << std::endl;
}
```

# 线程同步

消费者的操作与生产者完全相反：它等待“缓冲区不空”条件，并唤醒任何等待“缓冲区未满”条件的线程。

在目前所有的示例中，我们的线程都访问了相同的全局变量。但某些多线程应用程序需要全局变量在不同线程中持有不同的值。这通常被称为线程本地存储（thread-local storage）或线程特定数据。我们可以使用以线程 ID（通过 `QThread::currentThread()` 返回）为键的映射表来模拟它，但更好的方法是使用 `QThreadStorage<T>` 类。

`QThreadStorage<T>` 的常见用途是缓存。通过在不同线程中拥有单独缓存，我们避免了锁定、解锁以及可能等待互斥量的开销。例如：

```cpp
QThreadStorage<QHash<int, double *>> cache;

void insertCache(int id, double value)
{
    if (!cache.hasLocalData())
        cache.setLocalData(new QHash<int, double>());
    cache.localData()->insert(id, value);
}

void removeCache(int id)
{
    if (cache.hasLocalData())
        cache.localData()->remove(id);
}
```

第一次使用 `QThreadStorage<T>` 时，`hasLocalData()` 返回 `false`。除了缓存，`QThreadStorage<T>` 还可以用于全局状态变量，以确保修改不会影响其他线程。

## 与主线程通信
