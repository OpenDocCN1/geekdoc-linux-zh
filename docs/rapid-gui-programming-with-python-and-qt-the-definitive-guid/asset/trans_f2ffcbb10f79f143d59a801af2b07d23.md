
Python 的网络支持也可以在其他第三方库中找到，其中最著名的是 Twisted 网络框架；更多详情请参见 http://twistedmatrix.com。

在本章中，我们只关注创建一个简单的客户端/服务器应用程序，我们将使用 PyQt 的两个网络类 `QTcpSocket` 和 `QTcpServer` 来创建客户端和服务器。在下一章，我们将查看服务器的多线程版本，它能够在无需阻塞的情况下处理多个并发请求。

客户端/服务器应用程序通常作为两个独立的程序实现：一个等待并响应请求的服务器，以及一个或多个向服务器发送请求并读取服务器响应的客户端。为了实现这一功能，客户端必须知道如何连接到服务器，即服务器的 IP 地址和端口号。此外，客户端和服务器必须使用约定的套接字协议发送和接收数据，并使用双方都能理解的数据格式。

PyQt 提供两种不同种类的套接字。UDP（用户数据报协议）由 `QUdpSocket` 类支持。UDP 轻量级但不可靠——没有保证数据能被接收。UDP 是无连接的，因此数据只是作为离散项目发送或接收的。TCP（传输控制协议）由 `QTcpSocket` 类支持。TCP 是一种可靠的、面向连接和面向流的协议；可以发送和接收任意数量的数据——套接字负责将数据分解为足够小的块以便发送，并在另一端重组数据。

UDP 通常用于监控提供连续读数的仪器，偶尔错过的读数并不重要。客户端/服务器应用程序通常使用 TCP，因为它们需要可靠性；这是我们在本章中将要使用的协议。

必须做出的另一个决定是将数据作为文本行还是二进制数据块进行发送和接收。PyQt 的 TCP 套接字可以使用这两种方法，但我们选择处理二进制数据，因为这是最通用且最易处理的。

我们要使用的示例是楼宇服务应用程序。服务器保存建筑物中房间的信息以及它们被预订的日期。客户端用于在特定日期预订和取消预订特定房间。可以使用任意数量的客户端，但如果两个客户端发出的请求在*完全*相同的时间到达，其中一个将被阻塞，直到另一个请求被处理。这个问题可以通过使用线程服务器来缓解，我们将在下一章中看到。

为了示例的目的，我们将在同一台机器上运行服务器和客户端；这意味着我们可以使用“localhost”作为 IP 地址。服务器和两个客户端如图 18.1 所示。我们还选择了端口号 `9407`——这只是一个任意数字。端口号应大于 1023，通常在 5001 到 32767 之间，尽管端口号

![](img/9bfe0a027fcc8793bb087287001100dd_537_0.png)

**图 18.1** 一个有两个客户端的服务器

最高可达 65,535 是有效的。服务器可以接受两种类型的请求：“BOOK”（预订）和“UNBOOK”（取消预订），并可以发出三种类型的响应：“BOOK”、“UNBOOK”和“ERROR”。所有请求和响应都以二进制数据形式发送和接收；我们将在以下部分中查看它们的格式。

除了保存在 PORT 变量中的端口号外，我们还创建了 SIZEDF_UINT16 变量并将其设置为 2（表示两个字节）。除了常规导入外，我们还必须导入 Qtnetwork 模块：

```python
from PyQT4.QtNetwork import *
```

相同的 PORT 和 SIZEDF_UINT16 变量，以及相同的 Qtnetwork 导入，都用于客户端和服务器应用程序。在下一节中，我们将查看客户端的实现，并在第二节中审查服务器。

## 创建 TCP 客户端

楼宇服务客户端位于 chap18/buildingservicesclient.py。它允许用户输入房间号（只接受有效的房间号）和日期，并请求在指定日期预订（或取消预订）该房间。服务器响应该请求，客户端在响应标签中显示响应供用户阅读。

我们首先查看初始化器，但省略小部件和布局的创建。我们将分三部分查看它，然后再查看客户端的方法。

```python
class BuildingServicesClient(QWidget):
    def __init__(self, parent=None):
        super(BuildingServicesClient, self).__init__(parent)
        self.socket = QTcpSocket()
        self.nextBlockSize = 0
        self.request = None
```

我们继承自 QWidget 而非 QDialog 或 QMainWindow。唯一的明显差异是，如果我们继承自 QDialog，按下 Esc 键将终止应用程序。

我们需要存储三个对象。第一个是客户端用于与服务器通信的套接字。第二个是“下一个块大小”；这是我们用来确定是否已接收到足够的响应数据以能够处理响应的变量。第三个是请求对象；这是一个包含请求数据的 QByteArray，如果没有要发送的数据则为空。

我们将跳过小部件的创建、设置和布局，因为所有这些现在都应该很熟悉了，尽管我们将在查看完套接字连接后再查看小部件连接。

```python
self.connect(self.socket, SIGNAL("connected()"),
             self.sendRequest)
self.connect(self.socket, SIGNAL("readyRead()"),
             self.readResponse)
self.connect(self.socket, SIGNAL("disconnected()"),
             self.serverHasStopped)
self.connect(self.socket,
             SIGNAL("error(AbstractSocket::SocketError)"),
             self.serverHasError)
```

前四个信号与套接字有关。我们需要知道连接何时建立，因为在那时我们可以发送请求数据。我们还需要知道套接字是否有数据可读，因为当有数据时，它将包含服务器的响应，这是我们要读取的。如果连接终止——例如，因为服务器已关闭或发生错误——我们希望知道这一点，以便通知用户。

```python
self.connect(self.roomEdit, SIGNAL("textEdited(QString)"),
             self.updateUi)
self.connect(self.dateEdit, SIGNAL("dateChanged(QDate)"),
             self.updateUi)
self.connect(self.bookButton, SIGNAL("clicked()"),
             self.book)
self.connect(self.unBookButton, SIGNAL("clicked()"),
             self.unBook)
self.connect(quitButton, SIGNAL("clicked()"), self.close)
```

其他连接与用户界面有关。通常，我们有一个 updateUi() 方法用于执行验证以及根据需要启用/禁用按钮。我们还有连接用于预订和取消预订房间，以及终止应用程序。

```python
def updateUi(self):
    enabled = False
    if not self.roomEdit.text().isEmpty() and \
self.dateEdit.date() > QDate.currentDate():
        enabled = True
    if self.request is not None:
        enabled = False
    self.bookButton.setEnabled(enabled)
    self.unBookButton.setEnabled(enabled)
```

如果房间编辑框包含房间号且日期编辑框中的日期晚于今天，我们会启用预订和取消预订按钮——但如果有待处理的请求（即 self.request 不为空），我们将禁用它们。

```python
def closeEvent(self, event):
    self.socket.close()
    event.accept()
```

如果应用程序终止，我们确保关闭套接字并接受关闭事件。我们实际上不必做这些事情，但通过这样做，我们表明我们已经考虑了终止时应采取的措施。

```python
def book(self):
    self.issueRequest(QString("BOOK"), self.roomEdit.text(),
                     self.dateEdit.date())

def unBook(self):
    self.issueRequest(QString("UNBOOK"), self.roomEdit.text(),
                     self.dateEdit.date())
```

如果用户单击“预订”，将调用 book() 方法。该方法简单地调用 issueRequest()，参数为请求操作 "BOOK"、房间号（作为 QString）和日期。unBook() 方法几乎相同，只是其请求操作为 "UNBOOK"。

```python
def issueRequest(self, action, room, date):
    self.request = QByteArray()
    stream = QDataStream(self.request, QIODevice.WriteOnly)
    stream.setVersion(QDataStream.Qt_4_2)
    stream.writeUInt16(0)
    stream << action << room << date
    stream.device().seek(0)
    stream.writeUInt16(self.request.size() - sizeof_uint16)
    self.updateUI()
    if self.socket.isOpen():
        self.socket.close()

    self.responseLabel.setText("Connecting to server...")
    self.socket.connectToHost("localhost", PORT)
```

此方法用于准备请求 QByteArray 并启动将请求发送到服务器的过程。

