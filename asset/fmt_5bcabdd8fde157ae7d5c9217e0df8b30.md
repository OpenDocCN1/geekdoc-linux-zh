
# 事务处理与线程通信

当 `TransactionThread` 的事务队列变为空时，就会调用 `allTransactionsDone()` 槽。

现在转向 `TransactionThread` 类。和大多数 `QThread` 子类一样，它的实现相当棘手，因为 `run()` 函数在它自己的线程中执行，而其他函数（包括构造函数和析构函数）是从主线程调用的。该类的定义如下：

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

`TransactionThread` 类维护了一个待处理的事务队列，并在后台逐一个执行它们。在私有部分，我们声明了四个成员变量：

- `currentImage` 持有应用事务的图像。
- `transactions` 是待处理事务的队列。
- `transactionAdded` 是一个等待条件，当新事务添加到队列中时用于唤醒线程。
- `mutex` 用于保护 `currentImage` 和 `transactions` 变量免受并发访问。

这里是类的构造函数：

```cpp
TransactionThread::TransactionThread()
{
    start();
}
```

在构造函数中，我们简单地调用 `QThread::start()` 来启动线程。

```cpp
TransactionThread::~TransactionThread()
{
    {
        QMutexLocker locker(&mutex);
        while (!transactions.isEmpty())
            delete transactions.dequeue();
        transactions.enqueue(EndTransaction);
        transactionAdded.wakeOne();
    }
    wait();
}
```

在析构函数中，我们清空事务队列并在队列中添加一个特殊的 `EndTransaction`。然后我们唤醒线程并使用 `QThread::wait()` 等待其完成，最后调用基类的析构函数。如果不调用 `wait()`可能会在线程尝试访问类变量时发生崩溃。

```cpp
void TransactionThread::addTransaction(Transaction *transact)
{
    QMutexLocker locker(&mutex);
    transactions.enqueue(transact);
    transactionAdded.wakeOne();
}
```

`addTransaction()` 函数将事务添加到事务队列，如果事务线程尚未运行则唤醒它。

```cpp
void TransactionThread::setImage(const QImage &image)
{
    QMutexLocker locker(&mutex);
    currentImage = image;
}

QImage TransactionThread::image()
{
    QMutexLocker locker(&mutex);
    return currentImage;
}
```

`setImage()` 和 `image()` 函数允许主线程设置要执行事务的图像，并在所有事务完成后获取结果图像。代码视图：

```cpp
void TransactionThread::run()
{
    Transaction *transact = 0;
    QImage oldImage;

    forever {
        {
            QMutexLocker locker(&mutex);
            if (transactions.isEmpty())
                transactionAdded.wait(&mutex);

            transact = transactions.dequeue();
            if (transact == EndTransaction)
                break;

            oldImage = currentImage;
        }

        emit transactionStarted(transact->message());

        QImage newImage = transact->apply(oldImage);
        delete transact;

        {
            QMutexLocker locker(&mutex);
            currentImage = newImage;
            if (transactions.isEmpty())
                emit allTransactionsDone();
        }
    }
}
```

`run()` 函数遍历事务队列，通过调用 `apply()` 逐个执行事务，直到遇到 `EndTransaction` 标记。

在我们执行事务之前，我们会发出 `transactionStarted()` 信号，并带有一个要显示在应用程序状态栏中的消息。当所有事务处理完成后，我们会发出 `allTransactionsDone()` 信号。

```cpp
class Transaction
{
public:
    virtual ~Transaction() { }
    virtual QImage apply(const QImage &image) = 0;
    virtual QString message() = 0;
};
```

`Transaction` 类是用户可以在图像上执行的操作的抽象基类。虚析析构函数是必要的，因为我们需要通过 `Transaction` 指针删除 `Transaction` 子类类的实例。

`Transaction` 有三个具体的子类：`FlipTransaction`、`ResizeTransaction` 和 `ConvertDepthTransaction`。我们将只回顾 `FlipTransaction`；另外两个类是类似的。

```cpp
class FlipTransaction : public Transaction
{
public:
    FlipTransaction(Qt::Orientation orientation);
    QImage apply(const QImage &image);
    QString message();

private:
    Qt::Orientation orientation;
};
```

`FlipTransaction` 构造函数接受一个参数，用于指定翻转的方向（水平或垂直）。

```cpp
QImage FlipTransaction::apply(const QImage &image)
{
    return image.mirrored(orientation == Qt::Horizontal,
                          orientation == Qt::Vertical);
}
```

`apply()` 函数在其接收到的参数的 `QImage` 上调用 `QImage::mirrored()`，并返回生成的 `QImage`。

```cpp
QString FlipTransaction::message()
{
    if (orientation == Qt::Horizontal) {
        return QObject::tr("Flipping image horizontally...");
    } else {
        return QObject::tr("Flipping image vertically...");
    }
}
```

`message()` 函数返回操作进行期间显示在状态栏的消息。该函数在 `TransactionThread::run()` 发出 `transactionStarted()` 信号时被调用。

`Image Pro` 应用程序展示了 `Qt` 的信号与槽机制如何方便从辅助线程与主线程进行通信。

实现辅助线程更为复杂，因为我们必须使用互斥锁（mutex）保护成员变量，并且必须使用等待条件（wait condition）适当地让线程睡眠和唤醒。分两部分的 `Qt Quarterly` 季度文章系列《`Qt` 中的监视与等待条件》，在线地址为 `http://doc.trolltech.com/qq/qq21-monitors.html` 和 `http://doc.trolltech.com/qq/qq22-monitors2.html`，提供了更多关于如何开发和测试使用互斥锁和等待条件进行同步的 `QThread` 子类的想法。

## 在辅助线程中使用 Qt 类

如果一个函数可以从不同的线程同时安全地调用，则称该函数是**线程安全**的。如果从不同线程对同一个共享数据并发调用了两个线程安全的函数，其结果始终是确定的（defined）。以此类推，如果一个类的所有函数都可以从不同的线程同时调用而互不干扰（即使在操作同一个对象时也是），则称该类是线程安全的。

`Qt` 的线程安全类包括 `QMutex`、`QMutexLocker`、`QReadWriteLock`、`QReadLocker`、`QWriteLocker`、`QSemaphore`、`QThreadStorage<T>` 和 `QWaitCondition`。此外，`QThread` API 的部分以及其他几个函数是线程安全的，特别是 `QObject::connect()`、`QObject::disconnect()`、`QCoreApplication::postEvent()` 和 `QCoreApplication::removePostedEvents()`。

大多数 `Qt` 的非 GUI 类满足一个不那么严格的要求：它们是**重入的（reentrant）**的。如果一个类的不同实例可以在不同线程中同时使用，则该类是重入的。然而，在多个线程中同时访问同一个重入对象是不安全的，这种访问应该用互斥锁进行保护。重入类在 `Qt` 参考文档中被标记为此类。通常情况下，任何不引用全局或其他共享数据的 `C++` 类都是重入的。

`QObject` 是重入的，但有三个限制需要注意：

- **子 QObjects 必须在它们父对象的线程中创建。**
  特别是，这意味着在辅助线程中创建的对象绝不能以 `QThread` 对象作为其父对象，因为该对象是在另一个线程（主线程或另一个辅助线程）中创建的。
- **我们必须在删除相应的 `QThread` 对象之前，删除所有在辅助线程中创建的 QObjects。**
  这可以通过在 `QThread::run()` 中在栈上创建对象来实现。
- **QObjects 必须在创建它们的线程中删除。**
  如果我们需要删除存在于不同线程的 QObject，我们必须调用线程安全的 `QObject::deleteLater()` 函数，它会发布一个“延迟删除”事件。

非 GUI 的 `QObject` 子类如 `QTimer`、`QProcess` 和网络类是重入的。只要线程有事件循环，我们就可以在任何线程中使用它们。对于辅助线程，事件循环通过调用 `QThread::exec()` 或通过便利函数如 `QProcess::waitForFinished()` 和 `QAbstractSocket::waitForDisconnected()` 启动。

由于继承了构建 `Qt` GUI 支持的底层库的局限性，`QWidget` 及其子类不是重入的。这导致的结果之一是我们不能从辅助线程直接调用小部件上的函数。如果我们想（例如）从辅助线程更改 `QLabel` 的文本，可以发出一个连接到 `QLabel::setText()` 的信号，或者从该线程调用 `QMetaObject::invokeMethod()`。例如：

```cpp
void MyThread::run()
{
    ...
    QMetaObject::invokeMethod(label, SLOT(setText(const QString &)), ARG(QString, "Hello"));
    ...
}
```

大多数 `Qt` 的非 GUI 类满足一个要求较低的标准：它们是重入的。`QImage`、`QString` 和容器类等许多非 GUI 类使用隐式共享作为优化。虽然这种优化通常使类变为重入，但 `Qt` 使用原子指令来实现线程安全的引用计数。`Qt` 的 `SQL` 模块也可以用于多线程应用程序，但它有自己的限制，视数据库而异。详细信息请参见 `http://doc.trolltech.com/4.3/sql-driver.html`。关于线程警告的完整列表，请参见 `http://doc.trolltech.com/4.3/threads.html`。

## 15. 网络

`img/1bc72df8c60cf859263aefcc273027d_565_0.png`

### 编写 FTP 客户端
### 编写 HTTP 客户端
### 编写 TCP 客户端/服务器应用程序
### 发送和接收 UDP 数据

`Qt` 提供了 `QFtp` 和 `QHttp` 类来处理 `FTP` 和 `HTTP`。这些协议对于下载和上传文件非常方便，对于 `HTTP` 发送请求并获取结果也非常方便。`Qt` 还提供了底层的 `QTcpSocket` 和 `QUdpSocket` 类，它们实现了 `TCP` 和 `UDP` 传输协议。`TCP` 是一种基于网络节点数据流的可靠面向连接协议，而 `UDP` 是一种基于网络节点离散数据包的不可靠无连接协议。两者都可以用于网络客户端和服务器应用程序。对于服务器，我们还需要 `QTcpServer` 类来处理传入的 `TCP` 连接。通过使用 `QSslSocket` 代替 `QTcpSocket` 可以建立 `SSL/TLS` 连接。

```cpp
if (args.count() != 2) {
    std::cerr << "Usage: ftpget url" << std::endl
    << "Example:" << std::endl
    << " ftpget ftp://ftp.trolltech.com/mirrors"
    << std::endl;
    return 1;
}

FtpGet getter;

if (!getter.getFile(QUrl(args[1])))
    return 1;

QObject::connect(&getter, SIGNAL(done()), &app, SLOT(quit()));

return app.exec();
}
```

我们创建一个 `QCoreApplication` 而不是其子类 `QApplication`，以避免链接 `QtGui` 库。`QCoreApplication::arguments()` 函数将命令行参数作为 `QStringList` 返回，其中第一项是程序调用时的名称，并移除了任何 `Qt` 特有的参数（如 `-style`）。`main()` 函数的核心是构造 `FtpGet` 对象并调用 `getFile()`。如果调用成功，我们让事件循环运行，直到下载完成。

所有工作都由 `FtpGet` 子类完成，其定义如下：

```cpp
class FtpGet : public QObject
{
    Q_OBJECT

public:
    FtpGet(QObject *parent = 0);
    bool getFile(const QUrl &url);

signals:
    void done();

private slots:
    void ftpDone(bool error);

private:
    QFtp ftp;
    QFile file;
};
```

该类有一个公共函数 `getFile()`，用于检索由 URL 指定的文件。`QUrl` 类提供了一个高层接口，用于提取 URL 的不同部分，例如文件名、路径、协议和端口。

`FtpGet` 有一个私有槽 `ftpDone()`，它在文件传输完成时被调用；以及一个在文件下载完成后发射的 `done()` 信号。

该类还有两个私有变量：类型为 `QFtp` 的 `ftp` 变量，它封装了与 `FTP` 服务器的连接；以及用于将下载的文件写入磁盘的 `file` 变量。

```cpp
FtpGet::FtpGet(QObject *parent)
 : QObject(parent)
{
}
```
