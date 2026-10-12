
# 526 第18章。网络

图 18.2 展示了写入请求 `QByteArray` 的数据。`QByteArray` 的读写方式与其他任何 `QIODevice` 完全相同。前两个字节包含一个无符号整数，其初始值为 0。这个整数用于存储该请求所占用的字节数（不包括该整数本身的大小），即紧随其后的字节数。我们必须先将其设为 0，因为我们尚不知道最终会使用多少个字节。

![](img/9bfe0a027fcc8793bb087287001100dd_540_0.png)

在大小整数之后，我们写入数据。动作字符串是请求的动作（"BOOK" 或 "UNBOOK"），房间字符串保存房间号（例如 "213"），而日期则保存一个 `QDate`。一旦数据被写入字节数组，我们使用 `seek()` 将写入位置移动到开头，以便接下来写入的内容将覆盖 `QByteArray` 的起始部分。（实际上，我们在 `QDataStream` 底层的 `QIODevice` 上执行 seek 操作，该对象是通过调用 `QDataStream.device()` 获取的。）我们写入一个 16 位无符号整数，其值等于 `QByteArray` 的长度减去初始整数的大小。此时，请求字节数组已准备好发送。

我们更新用户界面——由于请求对象不是 None，这将禁用“预订”和“取消预订”按钮；这是为了防止用户在收到响应之前发起额外的请求。然后，我们确保套接字已关闭，因为它可能已打开以处理之前的请求，并设置响应标签以通知用户我们正试图建立连接。

最后，我们调用 `connectToHost()`。IP 地址可以以点分字符串形式给出（例如 "82.94.237.218"），也可以是主机名（例如 "www.python.org"），或者是一个 `QHostAddress` 对象。得益于我们在初始化程序中建立的信号-槽连接，我们知道一旦连接建立，我们的 `sendRequest()` 方法就会被调用，除非连接失败，在这种情况下，将会调用 `serverHasStopped()` 或 `serverHasError()` 方法。

```python
def sendRequest(self):
    self.responseLabel.setText("Sending request...")
    self.nextBlockSize = 0
    self.socket.write(self.request)
    self.request = None
```

一旦连接建立，该方法就会被调用。它会更新响应标签，告知用户请求正在发送，并将下一个块大小设置为 0。这涉及我们期望接收到的 *响应*；我们将在 `readResponse()` 方法中看到它的实际应用。然后，它将请求字节数组写入套接字。数据写入完成后，请求被设置为 None，为新请求做准备。

如果没有错误发生，且服务器未被终止，服务器将会响应，此时 `readResponse()` 方法将被调用。（否则，将调用 `serverHasStopped()` 或 `serverHasError()` 方法。）

![](img/9bfe0a027fcc8793bb087287001100dd_541_0.png)

如图 18.3 所示，服务器有两种不同的响应格式。收到响应时，我们必须先通过读取无符号整数来获取其大小。然后，一旦确定至少有足够大小的字节可供读取，我们就读取第一个 `QString`。如果其中包含文本 "ERROR"，我们就知道这是一个错误响应，只需读取包含错误消息的第二个字符串即可；否则，文本将是 "BOOK" 或 "UNBOOK"，即请求动作，并附带请求详情（第二个 `QString` 中的房间号和作为 `QDate` 的日期），以确认请求动作已成功。

```python
def readResponse(self):
    stream = QDataStream(self.socket)
    stream.setVersion(QDataStream.Qt_4_2)

    while True:
        if self.nextBlockSize == 0:
            if self.socket.bytesAvailable() < SIZEOF_UINT16:
                break
            self.nextBlockSize = stream.readUInt16()
        if self.socket.bytesAvailable() < self.nextBlockSize:
            break
        action = QString()
        room = QString()
        date = QDate()
        stream >> action >> room
        if action != "ERROR":
            stream >> date
        if action == "ERROR":
            msg = QString("Error: %1").arg(room)
        elif action == "BOOK":
            msg = QString("Booked room %1 for %2").arg(room) \
                  .arg(date.toString(Qt.ISODate))
        elif action == "UNBOOK":
            msg = QString("Unbooked room %1 for %2").arg(room) \
                  .arg(date.toString(Qt.ISODate))
        self.responseLabel.setText(msg)
        self.updateUI()
        self.nextBlockSize = 0
```

服务器的响应可能会分片返回。因此，我们使用无限循环，首先获取字节计数，然后确保有足够数量的字节可供读取。这将缓冲责任留给服务器，这意味着当我们读取时，我们知道可以一次性读取完整的响应。

如果至少有两个字节可用，我们将它们作为 16 位无符号整数读取：这给了我们接下来要读取的字节数。然后我们测试是否有足够的字节可供读取：如果没有，我们退出循环，等待下一个 `readyRead()` 信号触发 `readResponse()` 方法。如果有足够的字节，我们读取动作以及随后的字符串——这是房间号或错误消息。如果动作不是 "ERROR"，我们还读取日期。然后，根据接收到的动作，我们准备一条消息字符串并在响应标签中显示它。

读取完整个响应后，我们会重置下一个块大小，因为我们已经读取了相应数量的字节。现在当循环继续时，要么另一个响应正在等待，此时 `QTcpSocket.bytesAvailable()` 将返回大于零的值，我们重复读取和显示的过程；要么没有其他响应，我们就简单地跳出循环并结束。

```python
def serverHasStopped(self):
    self.responseLabel.setText(
        "Error: Connection closed by server")
    self.socket.close()

def serverHasError(self, error):
    self.responseLabel.setText(QString("Error: %1") \
        .arg(self.socket.errorString()))
    self.socket.close()
```

如果服务器被终止，或者服务器以网络错误（而不是我们自己的 "ERROR" 响应）进行响应，相关的 `serverHas*()` 方法将被调用。在这两种情况下，我们都会在响应标签中向用户显示错误消息并关闭套接字。

`BuildingServicesClient` 类现已完成。用户可以输入预订和取消预订请求，并通过点击“预订”和“取消预订”按钮将其发送到服务器，并可以在响应标签中看到请求的结果。请求是通过将 `QByteArray` 写入适当设置的套接字来发送的。响应通过 `QDataStream` 从套接字读回；这使我们能够直接将 `QStrings`、`QDates` 以及任何其他数据流支持的类型读取到局部变量中。

既然我们已经了解了客户端是如何创建的，我们可以将注意力转向服务器。

## 创建 TCP 服务器

Building Services TCP 服务器位于 `chap18/buildingservicesserver.pyw`。它有三个组件：一个包含 TCP 服务器实例的 GUI，并为用户提供了一种简单的服务器终止方式；一个实例化以提供服务器实例的 `QTcpServer` 子类；以及一个用于处理传入连接的 `QTcpSocket` 子类。我们将首先查看前两者，因为它们很短，然后再重点介绍 `QTcpSocket` 子类，因为大部分工作都在那里完成。

```python
class BuildingServicesDlg(QPushButton):
    def __init__(self, parent=None):
        super(BuildingServicesDlg, self).__init__(
            "&Close Server", parent)
        self.setWindowFlags(Qt.WindowStaysOnTopHint)

        self.loadBookings()
        self.tcpsvr = TcpServer(self)
        if not self.tcpsvr.listen(QHostAddress("0.0.0.0"), PORT):
            QMessageBox.critical(self, "Building Services Server",
                                 QString("Failed to start server: %1").arg(self.tcpsvr.errorString()))
        self.close()

        self.connect(self, SIGNAL("clicked()"), self.close)
```

换个花样，并提醒我们任何 PyQt 控件都可以是顶层窗口，我们将对话框制作成了 `QPushButton` 子类。我们还设置了 `Qt.WindowStaysOnTopHint`；大多数窗口系统会尊重此提示，并使该控件保持在所有其他窗口之上。

我们不会详细介绍 `loadBookings()` 方法；它用于填充内存数据结构——即保存预订数据的 `bookings` 默认字典。该字典的键是存储为 `datetime.date` 对象的日期，值是存储为 unicode 字符串的房间号有序列表。默认字典是在 Python 2.5 中引入的。它们与普通字典类似，不同之处在于，当我们使用一个字典中不存在的键时，该键会以默认值被插入。使用哪个默认值取决于我们如何创建字典。在 Building Services 服务器中，我们像这样创建了字典：

```python
bookings = collections.defaultdict(list)
```

在这里，我们指定任何新键的默认值是一个空的 `list`；在其他情况下，我们可能会选择一个空的 set。如果我们使用早于 2.5 的 Python 版本，随时可以用普通字典替换默认字典——例如，通过使用 `dict.setdefault()` 方法访问可能不存在的键，我们稍后会展示这一点。

![](img/9bfe0a027fcc8793bb087287001100dd_543_0.png)

