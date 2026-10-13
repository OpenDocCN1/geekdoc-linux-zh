
`name` 保存源文件保存时的名称；在这种情况下，它与 `target` 相同，但如果未指定目标，则将是生成的名称——例如，`/tmp/tmp~R823.tar.gz`。对于 HTTP 下载，`message` 是一个 `http.HTTPMessage` 实例，包含相关的 HTTP 头。

Python 的 `urllib` 和 `urllib2` 标准库模块非常多功能。它们可以使用 FTP 和 HTTP 协议，在后者情况下使用 GET 或 POST，并且可以使用 HTTP 代理。`urllib2` 模块支持基本身份验证，并可用于设置 HTTP 头。如果 Python 安装时带有 SSL 支持，`urllib2` 模块可以使用 HTTPS 协议。标准库还包括对许多其他网络协议的支持，包括用于电子邮件的 IMAP4、POP3 和 SMTP，用于网络新闻的 NNTP，以及处理 cookies、XML-RPC 和 CGI 的库，以及用于创建服务器的库。Python 的大多数网络支持基于 `socket` 模块，该模块可以直接用于低级网络编程。

除了 Python 标准库，PyQt4 还提供了自己的网络类集合，包括用于客户端端 FTP 支持的 `Qftp` 和用于 HTTP 支持的 `Qhttp`。低级网络可以使用 `QAbstractSocket` 子类完成，包括 `QTcpSocket`、`QTcpServer` 和 `QUdpSocket`，以及从 Qt 4.3 开始的 `QSslSocket`。

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

除了保存在 `PORT` 变量中的端口号外，我们还创建了 `SIZEDF_UINT16` 变量并将其设置为 2（表示两个字节）。除了常规导入外，我们还必须导入 Qtnetwork 模块：

```python
from PyQT4.QtNetwork import *
```

相同的 `PORT` 和 `SIZEDF_UINT16` 变量，以及相同的 Qtnetwork 导入，都用于客户端和服务器应用程序。在下一节中，我们将查看客户端的实现，并在第二节中审查服务器。

## 创建 TCP 客户端

楼宇服务客户端位于 `chap18/buildingservicesclient.py`。它允许用户输入房间号（只接受有效的房间号）和日期，并请求在指定日期预订（或取消预订）该房间。服务器响应该请求，客户端在响应标签中显示响应供用户阅读。

我们首先查看初始化器，但省略小部件和布局的创建。我们将分三部分查看它，然后再查看客户端的方法。

```python
class BuildingServicesClient(QWidget):
    def __init__(self, parent=None):
        super(BuildingServicesClient, self).__init__(parent)
        self.socket = QTcpSocket()
        self.nextBlockSize = 0
        self.request = None
```

我们继承自 `QWidget` 而非 `QDialog` 或 `QMainWindow`。唯一的明显差异是，如果我们继承自 `QDialog`，按下 Esc 键将终止应用程序。

我们需要存储三个对象。第一个是客户端用于与服务器通信的套接字。第二个是“下一个块大小”；这是我们用来确定是否已接收到足够的响应数据以能够处理响应的变量。第三个是请求对象；这是一个包含请求数据的 `QByteArray`，如果没有要发送的数据则为空。

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

其他连接与用户界面有关。通常，我们有一个 `updateUi()` 方法用于执行验证以及根据需要启用/禁用按钮。我们还有连接用于预订和取消预订房间，以及终止应用程序。
