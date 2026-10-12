

我们稍后将回顾 `TcpServer` 类。一旦创建了一个服务器，我们就告诉它在给定的 IP 地址和端口号上监听传入的连接。IP 地址被指定为 `QHostAddress`，使用特殊地址 "0.0.0.0"，意思是“所有网络接口”；端口号是我们之前用于客户端的相同的任意端口 9407。

该连接确保如果用户点击按钮，窗口将会关闭。我们不对 TCP 服务器执行任何特殊的清理工作；当它被销毁时，所有连接的客户端将收到通知，并触发它们套接字的 `disconnected()` 信号。

对话框没有其他内容了，所以现在我们可以看看那个继承自 `QTcpServer` 的简短的 `TcpServer` 类。

```python
class TcpServer(QTcpServer):
    def __init__(self, parent=None):
        super(TcpServer, self).__init__(parent)

    def incomingConnection(self, socketId):
        socket = Socket(self)
        socket.setSocketDescriptor(socketId)
```

这就是 TCP 服务器的完整代码。每当发生传入连接请求时，都会调用 `incomingConnection()` 方法，其中包含一个位于 `socketId` 中的套接字描述符。我们只是创建一个新的 `Socket`（一个我们将在下一节中回顾的 `QTcpSocket` 子类），并设置其使用服务器提供的套接字描述符。

这个 TCP 服务器依赖于 PyQt 事件循环。如果我们想创建一个基于 `QTcpServer` 但没有图形用户界面（GUI）的服务器，我们可以采取两种方法。一种方法是使用 `QEventLoop`，以提供不需要 GUI 的事件循环，并以与此处相同的方式编写代码。另一种方法是不使用事件循环，但在这种情况下，我们的做法需要略有不同。特别是，我们必须使用阻塞式的 `QTcpServer.waitForNewConnection()` 方法，而不是重新实现 `incomingConnection()`。当然，如果服务器没有 GUI，它可以纯粹使用 Python 的标准库编写，而完全不需要 `QtNetwork` 模块。或者，服务器可以使用 Twisted 编写。

一旦建立连接，所有的工作都交给 `Socket` 类，这是一个 `QTcpSocket` 的子类，我们现在将对此进行回顾。

```python
class Socket(QTcpSocket):
    def __init__(self, parent=None):
        super(Socket, self).__init__(parent)
        self.connect(self, SIGNAL("readyRead()"), self.readRequest)
        self.connect(self, SIGNAL("disconnected()"), self.deleteLater)
        self.nextBlockSize = 0
```

套接字将其 `readyRead()` 信号连接到我们的自定义 `readRequest()` 方法，并将其 `disconnected()` 信号连接到其 `deleteLater()` 槽——这确保了当连接终止时，套接字会被干净地删除。`nextBlockSize` 变量用于与客户端相同的目的，并以相同的方式使用，以确保只有当可用的可读字节数至少与请求中的字节数一样多时，我们才读取请求。

一旦创建套接字并建立好连接，它只是等待其 `readRequest()` 方法被调用。这个方法有点长，因此我们将分两部分来回顾它。

```python
def readRequest(self):
    stream = QDataStream(self)
    stream.setVersion(QDataStream.Qt_4_2)

    if self.nextBlockSize == 0:
        if self.bytesAvailable() < SIZEOF_UINT16:
            return
        self.nextBlockSize = stream.readInt16()
        if self.bytesAvailable() < self.nextBlockSize:
            return

        action = QString()
        room = QString()
        date = QDate()
```

我们首先检查是否至少有 2 个字节可读：如果有，我们读取下一个块的大小。如果没有 2 个字节可读，或者如果有 2 个字节但没有足够的字节来读取整个请求，我们返回并等待 `readRequest()` 再次被调用，届时更多的字节已到达。

一旦有足够的字节，我们创建空的 `action` 和 `room` 字符串，以及一个空的 `QDate`，准备好从传入的请求数据中填充它们。

```python
    stream >> action
    if action in ("BOOK", "UNBOOK"):
        stream >> room >> date
        bookings = Bookings.get(date.toPyDate())
        uroom = unicode(room)
    if action == "BOOK":
        if bookings is None:
            bookings = Bookings[date.toPyDate()]
        if len(bookings) < MAX_BOOKINGS_PER_DAY:
            if uroom in bookings:
                self.sendError("Cannot accept duplicate booking")
            else:
                bisect.insort(bookings, uroom)
                self.sendReply(action, room, date)
        else:
            self.sendError(QString("%1 is fully booked").arg(date.toString(Qt.ISODate)))
    elif action == "UNBOOK":
        if bookings is None or room not in bookings:
            self.sendError("Cannot unbook nonexistent booking")
        else:
            bookings.remove(uroom)
            self.sendReply(action, room, date)
    else:
        self.sendError("Unrecognized request")
```

服务器仅识别两种请求操作：“BOOK” 和 “UNBOOK”；如果收到其中之一，它会读取房间和日期，并检索给定日期（可能为空的）预订列表。它还存储房间号 `QString` 的 Unicode 副本，因为服务器使用的 `Bookings` 字典使用 Python 类型而不是 PyQt 类型来存储所有数据。

接下来，服务器尝试对给定日期预订或取消预订给定的房间。在预订时，如果给定日期没有预订，则为该日期创建一个空预订列表。这之所以有效，是因为我们使用的是默认字典（default dictionary），因此当我们用一个它没有的键访问它时，它会自动插入一个新项，给定键和默认值；在这种情况下，是一个空列表。代码有点微妙，因为我们一开始调用的是 `get()`。这样做是为了避免在操作为取消预订时，为给定日期创建一个空列表。只有当我们知道操作是预订时，我们才希望确保给定日期有一个列表。

如果我们使用的是普通字典，我们将不得不使用 `dict.setdefault()` 来检索给定日期的列表，如果键尚不存在，则创建一个以给定日期为键、空列表为值的新项。例如：

```python
bookings = Bookings.setdefault(date.toPyDate(), [])
```

> **PyQt 4.1**
> `QDate.toPyDate()` 方法是在 PyQt 4.1 中引入的；对于早期版本，我们需要通过编写 `datetime.date(date.year(), date.month(), date.day())` 自己执行转换。

一旦我们有了（可能为空的）预订列表，并且提供的预订数量少于允许的最大预订数（`MAX_BOOKINGS_PER_DAY`，其值为 5），房间号字符串将按顺序插入到列表中，并发送一个回显请求数据的回复给客户端。如果该房间在给定日期已预订，或者该日期已有最大数量的预订，则代替发送一个错误回复给客户端。

如果操作是取消预订，房间将从给定日期的预订中移除，并将操作回显给客户端；或者，如果预订一开始就不存在，则给出一个错误回复。虽然房间是按顺序存储的，但我们简单地使用了 `not in` 和 `list.remove()`，两者都执行线性搜索；对于更长的列表，我们会使用 `bisect.bisect_left()` 通过二分法查找房间，但在本示例中这似乎有些过度了。

如果请求操作无法识别，我们简单地回复一条错误消息。

```python
def sendReply(self, action, room, date):
    reply = QByteArray()
    stream = QDataStream(reply, QIODevice.WriteOnly)
    stream.setVersion(QDataStream.Qt_4_2)
    stream.writeUInt16(0)
    stream << action << room << date
    stream.device().seek(0)
    stream.writeUInt16(reply.size() - SIZEOF_UINT16)
    self.write(reply)
```

发送给客户端的回复与客户端请求的创建方式相同。我们使用 `QDataStream` 写入一个 `QByteArray`，开始时写入一个无符号 16 位整数，结束前用回复的大小覆盖该整数，然后将回复写入套接字。

```python
def sendError(self, msg):
    reply = QByteArray()
    stream = QDataStream(reply, QIODevice.WriteOnly)
    stream.setVersion(QDataStream.Qt_4_2)
    stream.writeUInt16(0)
    stream << QString("ERROR") << QString(msg)
    stream.device().seek(0)
    stream.writeUInt16(reply.size() - SIZEOF_UINT16)
    self.write(reply)
```

发送错误回复的代码与发送成功回复的代码几乎相同，事实上，我们可以用一个方法同时处理两者。

服务器可以轻松扩展以处理更多的请求类型，只需向 `readRequest()` 添加更多的 if 语句即可。例如，客户端可能想知道特定日期哪些房间已预订，或者特定房间在哪些日期已预订。

虽然我们使用了字典来保存服务器的数据，但没有理由认为服务器不能将数据保存在进程内的 SQLite 数据库、进程外的数据库或文件中。服务器也不需要具有图形用户界面；它可以没有 `QWidgets`，简单地作为 Linux 守护进程或 Windows 服务在后台运行。

