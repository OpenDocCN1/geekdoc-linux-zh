
一种众所周知的锁定机制是互斥锁（也称为二元信号量），由 PyQt 的 `QMutex` 类提供。互斥锁仅允许锁定它的线程访问受保护的资源。PyQt 还提供更细粒度的机制，即读/写锁，由我们在本文中使用的 `QReadWriteLock` 类提供。只要一个线程持有锁，其他线程可能被阻塞，等待访问。我们可以以两种方式最小化这个问题。首先，我们尽可能使用读锁——如果当前持有的锁只是读锁，那么没有线程会被阻塞，因为如果没有线程在写入，所有线程进行读取都是安全的。其次，我们可以最小化在锁生效期间进行的处理量。我们在 `run()` 重新实现中使用了这两种技术；缺点是代码比预期要长得多。

`QMutex`、`QReadWriteLock` 以及其他保护机制之所以有效，是因为它们都是“线程安全”的。任意数量的线程可以同时调用线程安全对象的方法，并可以依赖底层系统（即 PyQt）自动序列化对共享数据的任何可能发生的访问。这意味着，例如，如果两个或更多线程试图对 `QReadWriteLock` 进行写锁定，只有一个会成功，所有其他线程都将被阻塞。这使得获得锁的线程可以对共享数据执行更新，当它释放锁时，想要写入的其他线程之一将获得访问权限，如此循环往复，直到没有线程再需要写访问。

PyQt 文档指出了哪些类，或者类中的哪些方法是线程安全的。它还指出了哪些方法是可重入的。可重入方法比线程安全方法受到更多限制。这是因为，只有当每次调用仅涉及访问唯一数据（如局部变量）时，从多个线程同时调用可重入方法才是安全的。通过使用锁来保护对实例变量的所有访问以及对指向共享数据的变量的访问，可以使可重入方法变得线程安全。

```python
if action == "BOOK":
    newlist = False
    try:
        Thread.lock.lockForRead()
        if bookings is None:
            newlist = True
    finally:
        Thread.lock.unlock()
    if newlist:
        try:
            Thread.lock.lockForWrite()
            bookings = Bookings[date.toPyDate()]
        finally:
            Thread.lock.unlock()
```

如果请求是预订房间，我们通过检查 `bookings` 变量开始。这是 `None` 或指向共享 `Bookings` 默认字典中持有的列表的引用，因此我们在访问它时必须使用读锁。如果 `bookings` 是 `None`，我们将一个新空列表插入到字典中，并以给定的日期作为其键；这次我们必须使用写锁。

```python
error = None
insert = False
try:
    Thread.lock.lockForRead()
    if len(bookings) < MAX_BOOKINGS_PER_DAY:
        if uroom in bookings:
            error = "Cannot accept duplicate booking"
        else:
            insert = True
    else:
        error = QString("%1 is fully booked").arg(
            date.toString(Qt.ISODate))
```

finally:

    Thread.lock.unlock()

if insert:

    try:

        Thread.lock.lockForWrite()

        bisect.insert(bookings, uroom)

    finally:

        Thread.lock.unlock()

    self.sendReply(socket, action, room, date)

else:

    self.sendError(socket, error)
```

如果房间在给定日期已经预订，我们不会重复预订，而是向客户端发送错误响应。在单线程服务器中，我们在这种情况下简单地调用了 `sendError()`，但在这里我们只是分配一段错误文本。这样做是为了将锁上下文中的处理工作量降至最低。

如果预订可以成功，我们获取写锁，将房间插入预订列表，并发送表示成功的响应。否则，我们发送错误响应。两种响应都不在锁的上下文中发送，再次是为了最小化锁保持生效的时间。

```
elif action == "UNBOOK":
    error = None
    remove = False
    try:
        Thread.lock.lockForRead()
        if bookings is None or uroom not in bookings:
            error = "Cannot unbook nonexistent booking"
        else:
            remove = True
    finally:
        Thread.lock.unlock()
    if remove:
        try:
            Thread.lock.lockForWrite()
            bookings.remove(uroom)
        finally:
            Thread.lock.unlock()
        self.sendReply(socket, action, room, date)
    else:
        self.sendError(socket, error)
```

取消预订的 if 分支遵循与预订分支相同的模式。我们首先使用读锁检查是否可以进行取消预订操作，如有必要，存储错误信息，而不是在锁生效期间执行耗时的发送操作。然后，我们通过从 `Bookings` 字典中对应给定日期的列表中移除该房间来取消预订，并发送成功响应；或者，我们发送错误响应。同样，响应是在没有锁生效时发送的。

```
else:
    self.sendError(socket, "Unrecognized request")
    socket.waitForDisconnected()
```

如果服务器接收到一个它无法识别的请求，它只是简单地发送一个错误响应。最后，我们调用 `QTcpSocket.waitForDisconnected()`；这会阻塞直到连接关闭，也就是说，直到响应发送完毕后。我们不需要也不希望保持连接打开，因为我们的客户端/服务器应用程序是以独立的请求-响应事务对的形式运行的。一旦连接关闭，`run()` 方法就会结束，并且得益于 `deleteLater()` 信号槽连接，线程将会被删除。

## 创建和管理辅助线程

在 GUI 应用程序中，线程的一个常见用例是将处理任务传递到辅助线程，以便用户界面能够保持响应并显示辅助线程的进度。在本节中，我们将查看页面索引器（Page Indexer）应用程序（如图 19.1 所示），该应用程序对指定目录及其所有子目录中的 HTML 文件建立索引。索引工作被交给一个辅助线程，该线程与主线程通信，以通知主线程已完成的进度以及索引何时完成。

![](img/9bfe0a027fcc8793bb087287001100dd_558_0.png)

我们将用于建立索引的算法如下：对于遇到的每个 HTML 文件，读取其文本，将实体转换为等效的 Unicode 字符，并去除 HTML 标签。然后，文本被分割成单词，每个长度在 3 到 25 个字符之间（含）且不在常用词集中的单词被添加到 `fileNamesForWords` 默认字典中。字典中的每个键都是唯一的单词，每个关联的值是一个文件名集合，其中包含该单词出现的文件。如果某个单词出现在 250 个以上的文件中，它将从字典中删除并添加到常用词集合中。这确保了字典保持在合理的大小，这意味着像“and”和“the”这样的单词的搜索将不起作用——这是一件好事，因为这样的单词可能在成千上万个文件中匹配，数量多到没有用处。

我们将首先查看应用程序主表单的两个摘录，该表单位于文件 `chAP19/pageindexer.pyw` 中。

```
class Form(QDialog):
    def __init__(self, parent=None):
        super(Form, self).__init__(parent)
        self.fileCount = 0
        self.fileNamesForWords = collections.defaultdict(set)
        self.commonWords = set()
        self.lock = QReadWriteLock()
        self.path = QDir.homePath()
```
