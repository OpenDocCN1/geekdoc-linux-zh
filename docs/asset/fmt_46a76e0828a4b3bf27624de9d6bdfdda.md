
当应用程序启动时，只有一个线程在运行——即主线程。这是唯一允许创建 `QApplication` 并调用 `exec()` 的线程。在调用 `exec()` 之后，该线程将等待事件。

主线程可以通过创建 `QThread` 子类的对象来启动新线程。如果这些新线程需要它们之间进行通信，它们共同使用共享变量配合互斥量、读写锁、信号量或等待条件。但这些技术中没有一种可以与主线程通信。

## 350 14. 多线程

从辅助线程向主线程通信的解决方案是使用跨线程的信号槽连接。通常情况下，信号槽机制是同步运行的，这意味着连接到信号的槽会在信号发射时立即被调用，类似于直接函数调用。

然而，当我们连接不同线程中的对象时，该机制变为异步的（这种行为可以通过通过 `QObject::connect` 的五个参数来更改）。在后台，这些连接是通过发布事件实现的。槽是由接收对象所在线程的事件循环调用的。默认情况下，`QObject` 存在于创建它的线程中；可以通过调用 `QObject::moveToThread()` 随时更改。

为了说明跨线程信号槽连接，我们将回顾 Image Pro 应用程序的代码，这是一个基本的图像处理应用程序，允许用户旋转、调整大小和更改图像深度。该应用程序（如图14.3 所示）使用一个辅助线程对图像进行操作，而不锁定事件循环。这在处理极大图像时会有显著差异。辅助线程有一个任务列表（事务）需要完成，并向主窗口发送事件以报告进度。

```cpp
ImageView::ImageView()
{
    label = new QLabel;
label->setBackgroundRole(QPalette::Dark);
label->setAutoFillBackground(true);
label->setAlignment(Qt::AlignLeft | Qt::AlignTop);
setCentralWidget(label);

    createActions();
    createMenu();

    statusBar()->showMessage("Ready", 2000);

connect(&thread, SIGNAL(transactionStarted(const QString&)),
        statusBar(this), SLOT(showMessage(const QString&)));
connect(&thread, SIGNAL(allTransactionsDone())),
        this, SLOT(allTransactionsDone()));

    setCurrentFile("");
}
```

`ImageView` 构造函数中有趣的部分是两个信号槽连接。它们都涉及由 `TransactionThread` 对象发射的信号，我们稍后会介绍。

```cpp
void ImageView::flipHorizontal()
{}
```

### 与主线程通信

![](img/930c1c6fda99d425284503ebcbc940ea_373_0.png)

**图 14.3.** Image Pro

```cpp
addTransaction(new FlipTransaction(Qt::Horizontal));
}
```

`flipHorizontally()` 槽创建一个“翻转”事务并使用私有函数 `addTransaction()` 将其注册。`flipVertically()`、`resizeImage()`、`convertTo32Bit()`、`convertTo8Bit()` 和 `convertTo1Bit()` 函数类似。

```cpp
void ImageView::addTransaction(Transaction *transact)
{
  thread->addTransaction(transact);
  openAction->setEnabled(false);
  saveAction->setEnabled(false);
  saveAsAction->setEnabled(false);
}
```

`addTransaction()` 函数将事务添加到辅助线程的事务队列中，并在处理事务期间禁用“打开”、“保存”和“另存为”操作。

```cpp
void ImageView::allTransactionsDone()
{
  openAction->setEnabled(true);
  saveAction->setEnabled(false);
  saveAsAction->setEnabled(true);
  imageLabel->setPixmap(QPixmap::fromImage(thread.image()));
  setWindowModified(true);
  statusBar()->showMessage(tr("Ready"), 2000);
}
```

当 `TransactionThread` 的事务队列为空时，会调用 `allTransactionsDone()` 槽。

现在，让我们转向 `TransactionThread` 类。和大多数 `QThread` 子类一样，它的实现有些棘手，因为 `run()` 函数在自己的线程中执行，而其他函数（包括构造函数和析构函数）是从主线程调用的。该类的定义如下：

```cpp
class TransactionThread : public QThread
{
    Q_OBJECT
public:
    TransactionThread();
    ~TransactionThread();
    void addTransaction(Transaction *transact);
    void setImage(const QImage &image);
    QImage image();
signals:
    void transactionStarted(const QString &message);
    void allTransactionsDone();
protected:
    void run();
private:
    QImage currentImage;
    QQueue<Transaction *> transactions;
    QWaitCondition transactionAdded;
    QMutex mutex;
};
```

`TransactionThread` 类维护一个待处理的事务队列，并在后台按顺序执行它们。在私有部分中，我们声明了四个成员变量：

- `currentImage` 持有应用事务的图像。
- `transactions` 是待处理事务的队列。
- `transactionAdded` 是一个等待条件，用于在向队列添加新事务时唤醒线程。
- `mutex` 用于保护 `currentImage` 和 `transactions` 成员变量免受并发访问。

这里是该类的构造函数：

```cpp
TransactionThread::TransactionThread()
{
    start();
}
```

在构造函数中，我们只需调用 `QThread::start()` 来启动执行事务的线程。

```cpp
TransactionThread::~TransactionThread()
{
    QMutexLocker Locker(&mutex);
    while (!transactions.isEmpty()) {
        delete transactions.dequeue();
        transactions.enqueue(EndTransaction);
        transactionAdded.wakeOne();
    }
    wait();
}
```

在析构函数中，我们清空事务队列并向其添加一个特殊的 `Transaction` 标记。我们唤醒线程并使用 `QThread::wait()` 等待其完成，然后基类的析构函数会被隐式调用。调用 `wait()` 可能会在线程尝试访问成员变量时导致崩溃。

`QMutexLocker` 的析构函数会在内部块结束时、在调用 `wait()` 之前解锁互斥。在调用 `wait()` 之前解锁互斥是至关重要的；否则程序可能会陷入死锁状态，即辅助线程永远等待互斥解锁，而主线程持有互斥并等待辅助线程完成后继续执行。

```cpp
void TransactionThread::addTransaction(Transaction *transaction)
{
    QMutexLocker locker(&mutex);
    transactions.enqueue(transaction);
    transactionAdded.wakeOne();
}
```

`addTransaction()` 函数将事务添加到事务队列中，如果线程尚未运行，则唤醒它。对 `transactions` 成员变量的所有访问都受互斥锁的保护，因为主线程可能在辅助线程遍历事务的同一时间，通过 `addTransaction()` 修改它们。

```cpp
void TransactionThread::setImage(const QImage &image)
{
    QMutexLocker locker(&mutex);
    currentImage = image;
}
```

```cpp
QImage TransactionThread::image()
{
    QMutexLocker locker(&mutex);
    return currentImage;
}
```

`setImage()` 和 `image()` 函数允许主线程设置执行事务的图像，并在所有事务完成后获取结果图像。

```cpp
void TransactionThread::run()
{
    Transaction *transact = 0;
    QImage oldImage;

    forever {
        QMutexLocker locker(&mutex);
        if (transactions.isEmpty()) {
            transactionAdded.wait(&mutex);
            transact = transactions.dequeue();
            if (transact == EndTransaction)
                break;
        }
        oldImage = currentImage;
        emit transactionStarted(transact->message());
        QImage newImage = transact->apply(oldImage);
        delete transact;
        QMutexLocker locker(&mutex);
        currentImage = newImage;
        if (transactions.isEmpty())
            emit allTransactionsDone();
    }
}
```

`run()` 函数遍历事务队列并调用 `apply()` 执行每个事务，直到遇到 `EndTransaction` 标记。如果事务队列为空，线程会在“事务添加”条件上等待。

在执行事务之前，我们发出 `transactionStarted()` 信号，带有显示应用程序状态栏的消息。当所有事务处理完成后，我们发出 `allTransactionsDone()` 信号。

```cpp
class Transaction
{
public:
    virtual ~Transaction() {}
    virtual QImage apply(const QImage &image) = 0;
    virtual QString message() = 0;
};
```

`Transaction` 类是用户对图像执行的操作的抽象基类。虚析构函数是必要的，因为我们需要通过 `Transaction` 指针删除子类的实例。`Transaction` 有三个子类：`FlipTransaction`、`ResizeTransaction` 和 `ConvertTransaction`。我们将只审查 `FlipTransaction`；其他类类似。

```cpp
class FlipTransaction : public Transaction {
public:
    FlipTransaction(Qt::Orientation orientation);
    QImage apply(const QImage &image);
    QString message();

private:
    Qt::Orientation orientation;
};
```

`FlipTransaction` 构造函数接收一个参数，指定翻转的方向（水平或垂直）。

```cpp
QImage FlipTransaction::apply(const QImage &image) {
    return image.mirrored(orientation == Qt::Horizontal,
                         orientation == Qt::Vertical);
}
```

`apply()` 函数对其接收的 `QImage` 调用 `QImage::mirrored()` 并返回结果图像。

```cpp
QString FlipTransaction::message() {
    if (orientation == Qt::Horizontal) {
        return QObject::tr("Flipping image horizontally...");
    } else {
        return QObject::tr("Flipping image vertically...");
    }
}
```

`message()` 函数返回执行期间显示在状态栏的消息。这在 `TransactionThread::run()` 发出 `transactionStarted()` 时被调用。

Image Pro 应用展示了 Qt 的信号与槽机制如何使辅助线程与主线程之间的通信。实现辅助线程更为棘手，因为我们必须使用互斥锁保护成员变量，并且必须使用等待条件适当地让线程睡眠和唤醒。两部分的 Qt 季度文章系列“Qt 中的互斥锁与等待条件”，在线地址为 http://doc.trolltech.com/qq21-monitors.html 和 http://doc.trolltech.com/qq22-monitors2.html，介绍了关于如何开发和测试使用互斥锁（`mutex`）和等待条件进行同步的 `QThread` 子类的思路。

## 在辅助线程中使用 Qt 类

如果一个函数可以同时从不同的线程被调用，则称它是线程安全的。如果从不同的线程对同一份共享数据并发调用两个线程安全的函数，其结果始终是有定义的。以此类推，当一个类的所有函数都可以从多个线程同时调用且互不干扰（即使在同一个对象上操作），则称该类是线程安全的。

Qt 的非 GUI 类包括 `QMutex`、`QMutexLocker`、`QReadWriteLock`、`QReadLocker`、`QWriteLocker`、`QSemaphore`、`QStorage<>` 和 `WaitCondition`。此外，Qt API 的部分以及其他一些函数是线程安全的，特别是 `QObject::connect()`、`QObject::disconnect()`、`QApplication::postEvent()` 和 `QApplication::removeEvents()`。

大多数 Qt 类意味着一个不那么严格的要求：它们是**重入的（reentrant）**。如果该类的不同实例可以在不同的线程中同时使用，则称它是重入的。然而，在多个线程中同时访问同一个重入对象是不安全的，因此访问应该用互斥锁进行保护。重入类在 Qt 参考文档中被标记为重入类。通常情况下，任何不引用全局或其他共享数据的 C++ 类都是重入的。

`QObject` 是重入的，但有三个限制需要注意：

- `QObject` 必须在其父对象的线程中创建。

特别，这意味着在辅助线程中创建的对象必须以 `QThread` 对象为父对象来创建，因为该对象是在另一个线程（主线程或另一个辅助线程）中创建的。

- 我们必须在删除 `QThread` 对象之前，删除所有在辅助线程中创建的 `QObject`。

这可以通过在 `QThread::run()` 中在栈上创建对象来实现。

- `QObject` 必须在创建它的线程中删除。

如果我们需要删除一个存在不同线程的 `QObject`，则必须调用线程安全的 `QObject::deleteLater()` 函数，它会发送一个“延迟删除”事件。

非 GUI `QObject` 子类（如 `QTimer`、`QProcess` 和网络类）是重入的。只要线程有事件循环，我们就可以在任何线程中使用它们。对于辅助线程，事件循环通过调用 `QThread::exec()` 或便利函数如 `QProcess::waitFinished()` 和 `AbstractSocket::waitDisconnected()` 来启动。

### 在辅助线程中使用 Qt 类（补充）

由于继承自构建 Qt GUI 支持的底层库的限制，`QWidget` 及其子类不是重入的。这的一个后果是，我们无法直接从辅助线程直接调用小部件上的函数。如果我们想（例如）从辅助线程更改 `QLabel` 的文本，可以发射一个连接到 `QLabel::setText()` 的信号，或者从该线程调用 `QMetaObject::invokeMethod()`。

例如：
