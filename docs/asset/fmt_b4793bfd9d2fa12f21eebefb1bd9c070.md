
### 代码示例

```cpp
  ui->setupUi(this);

  // 在构造函数中，根据日期和时间初始化日期和时间编辑器。

  // 我们还隐藏了进度条，因为我们想在连接激活时显示它。

  // 在 Qt Designer 中，进度条的最小和最大属性都被设置为 0。

  // 这告诉 QProgressBar 作为一个忙碌指示器而不是标准的百分比进度条。

  // ... 初始化代码 ...

}
```

```cpp
void TripPlanner::connectToServer()
{
  tcpSocket.connectToHost("tripserver.de", 6178);

  tableWidget->setRowCount(0);

  searchButton->setEnabled(false);

  stopButton->setEnabled(true);

  statusLabel->setText(tr("正在连接服务器..."));

  progressBar->show();

  nextBlockSize = 0;
}
```

```cpp
void TripPlanner::sendRequest()
{
  QByteArray block;

  QDataStream out(&block, QIODevice::WriteOnly);

  out.setVersion(QDataStream::Qt_4_3);

  out << quint16(0) << quint8('S') << fromComboBox->currentText()
  << toComboBox->currentText() << dateEdit->date()
  << timeEdit->time();

  if (departureRadioButton->isChecked()) {
out << quint8('D');

} else {
out << quint8('A');

}

out.device()->seek(0);

out << quint16(block.size() - sizeof(quint16));

tcpSocket.write(block);

statusLabel->setText(tr("Sending request..."));

}
```

当 `QTcpSocket` 对象发射 `connected()` 信号时，会执行 `sendRequest()` 槽，这表示连接已经建立。该槽的任务是向服务器生成一个请求，包含用户输入的所有信息。

请求是一个如下格式的二进制块：

| 类型 | 说明 |
| :--- | :--- |
| `quint16` | 字节单位的块大小（不包含此字段） |
| `quint8` | 请求类型（始终为 `'S'`） |
| `QString` | 出发城市 |
| `QString` | 到达城市 |
| `QDate` | 旅行日期 |
| `QTime` | 大致的旅行时间 |
| `quint8` | 时间代表出发 (`'D'`) 还是到达 (`'A'`) |

我们首先将数据写入一个名为 `block` 的 `QByteArray` 中。我们不能直接将数据写入 `QTcpSocket`，因为在将所有数据放入 `block` 之前，我们不知道块的大小，而块的大小必须先发送。

我们最初写入 `0` 作为块大小，然后写入其余数据。接着我们在 I/O 设备（由 `QDataStream` 在后台创建的 `QBuffer`）上调用 `seek(0)` 回到字节数组开头，用块数据的大小覆盖初始的 `0`。该大小通过块的大小减去 `sizeof(quint16)`（即 2）计算得出，以便从字节计数中排除大小字段。之后，我们在 `QTcpSocket` 上调用 `write()` 将块发送到服务器。

#### 代码视图

```cpp
void TripPlanner::updateTableWidget()
{
    QDataStream in(&tcpSocket);
    in.setVersion(QDataStream::Qt_4_3);
    for (;;) {
        int row = tableWidget->rowCount();
        if (nextBlockSize == 0) {
            if (tcpSocket.bytesAvailable() < sizeof(quint16))
                break;
            in >> nextBlockSize;
        }
        if (nextBlockSize == 0xFFFF) {
            closeConnection();
            statusLabel->setText(tr("Found %1 trip(s)").arg(row));
            break;
        }
        if (tcpSocket.bytesAvailable() < nextBlockSize)
            break;
        QDate date;
        QTime departureTime;
        QTime arrivalTime;
        quint16 duration;
        quint8 changes;
        QString trainType;
        in >> date >> departureTime >> duration >> changes >> trainType;
        arrivalTime = departureTime.addSecs(duration * 60);
        tableWidget->setRowCount(row + 1);
        QStringList fields;
        fields << date.toString(Qt::LocalDate)
               << departureTime.toString(tr("hh:mm"))
               << arrivalTime.toString(tr("hh:mm"))
               << tr("%1 hr %2 min").arg(duration / 60)
               .arg(duration % 60)
               << QString::number(changes)
               << trainType;
        for (int i = 0; i < fields.count(); ++i)
            tableWidget->setItem(row, i, new QTableWidgetItem(fields[i]));
        nextBlockSize = 0;
    }
}
```

`updateTableWidget()` 槽连接到 `QTcpSocket` 的 `readyRead()` 信号，每当 `QTcpSocket` 从服务器收到新数据时，就会发射该信号。服务器向我们发送符合用户标准的可能的旅行列表。每个匹配的旅行都作为一个单独的块发送，每个块都以大小开头。图 15.2 展示了这样的块流。使用 `forever` 循环是必要的，因为我们并不一定每次都能从服务器接收一个块数据。(*) 我们可能收到整个块，或者只是块的一部分、一个半个块，甚至一次性收到所有的块。

(*) `forever` 关键字由 Qt 提供。它简单地展开为 `for (;;)`。

**图 15.2. 旅行服务器的块**

![](img/1bc72df8c60cf85926d3aefcc273027d_599_0.png)

那么，`forever` 循环是如何工作的呢？如果变量 `nextBlockSize` 为 `0`，意味着我们还没有读取下一个块的大小。我们尝试读取它（假设至少有 2 个字节可读）。服务器使用大小值 `0xFFFF` 表示没有更多数据待接收，因此如果我们读取到这个值，我们就到达了末尾。

如果块大小不是 `0xFFFF`，我们尝试读取下一个块。首先，我们检查是否有可读的块大小字节。如果没有，我们目前就停止。当有更多数据可用时，`readyRead()` 信号将再次发射，届时我们会再次尝试。

一旦我们确定整个块已经到达，就可以安全地对 `QDataStream` 使用 `>>` 运算符来提取与旅行相关的信息，并根据这些信息创建 `QTableWidgetItem`。

```cpp
nextBlockSize = 0;

}
```

在构造函数中，我们建立了必要的信号与槽连接，并将 `nextBlockSize` 变量设置为 `0`，这表示我们目前尚不知道客户端发送的数据块的大小。

`disconnected()` 信号连接到 `deleteLater()`，这是一个继承自 `QObject` 的函数，它会在控制权返回 Qt 的事件循环时删除该对象。这确保了当连接关闭时，`ClientSocket` 对象会被删除。

#### 代码视图

```cpp
void ClientSocket::readClient()
{
    QDataStream in(this);
    in.setVersion(QDataStream::Qt_4_3);
    if (nextBlockSize == 0) {
        if (bytesAvailable() < sizeof(quint16))
            return;
        in >> nextBlockSize;
    }
    if (bytesAvailable() < nextBlockSize)
        return;
    quint8 requestType;
    QString from;
    QString to;
    QDate date;
    QTime time;
    quint8 flag;
    in >> requestType;
    if (requestType == 'S') {
        in >> from >> to >> date >> time >> flag;
        std::srand(from.length() * 3600 + to.length() * 60 + time.hour());
        int numTrips = std::rand() % 8;
        for (int i = 0; i < numTrips; ++i)
            generateRandomTrip(from, to, date, time);
        QDataStream out(this);
        out << quint16(0xFFFF);
    }
    close();
}
```

`readClient()` 槽连接到 `QTcpSocket` 的 `readyRead()` 信号。如果 `nextBlockSize` 为 `0`，我们首先读取数据块的大小；否则，我们已经读取了它，此时而是检查整个数据块是否已经到达。一旦整个数据块准备好读取，我们就会一次性读取它。我们直接在 `QTcpSocket`（即 `this` 对象）上使用 `QDataStream` 并使用 `>>` 运算符读取字段。

一旦读取了客户端的请求，我们就可以准备生成回复了。如果这是一个真实的应用程序，我们将会在列车时刻数据库中查找信息，并尝试找到匹配的行程。但在这里，我们满足于名为 `generateRandomTrip()` 的函数，它将生成一个随机行程。我们随机调用该函数几次，然后发送 `0xFFFF` 来表示数据的结束。在最后，我们关闭连接。

#### 代码视图

```cpp
void ClientSocket::generateRandomTrip(const QString /* from */, const QString &to, const QDate &date, const QTime &time)
{
    QByteArray block;
    QDataStream out(&block, QIODevice::WriteOnly);
    out.setVersion(QDataStream::Qt_4_3);
    quint16 duration = std::rand() % 200;
    out << quint16(0) << date << time << duration << quint8(1) << QString("InterCity");
    out.device()->seek(0);
    out << quint16(block.size() - sizeof(quint16));
    write(block);
}
```

`generateRandomTrip()` 函数展示了如何通过 TCP 连接发送一个数据块。这与我们在客户端的 `sendRequest()` 函数中所做的非常相似（第 374 页）。再次，我们将数据块写入 `QByteArray`，以便在使用 `write()` 发送它之前能够确定其大小。

#### 代码视图

```cpp
int main(int argc, char *argv[])
{
    QApplication app(argc, argv);
    TripServer server;
    if (!server.listen(QHostAddress::Any, 6178)) {
        std::cerr << "Failed to bind to port" << std::endl;
        return 1;
    }
    QPushButton quitButton(QObject::tr("&Quit"));
    quitButton.setWindowTitle(QObject::tr("Trip Server"));
    QObject::connect(&quitButton, SIGNAL(clicked()), &app, SLOT(quit()));
    quitButton.show();
    return app.exec();
}
```

在 `main()` 中，我们创建了一个 `TripServer` 对象和一个允许用户停止服务器的 `QPushButton`。我们通过调用 `QTcpSocket::listen()` 来启动服务器，该函数接收我们想要接受连接的 IP 地址和端口号。特殊地址 `0.0.0.0` (`QHostAddress::Any`) 表示本地主机上存在的任何 IP 接口。

在开发期间，使用 `QPushButton` 来表示服务器是非常方便的。然而，部署的服务器预计将在没有 GUI 的情况下运行，作为 Windows 服务或 Unix 守护进程。Trolltech 为此目的提供了一个商业插件，称为 `QtService`。

我们的客户端-服务器示例到此结束。在这种情况下，我们使用了一种面向块的协议，这允许我们使用 `QDataStream` 进行读写。如果我们想使用面向行的协议，最简单的方法是在连接到 `readyRead()` 信号的槽函数中使用 `QTcpSocket` 的 `canReadLine()` 和 `readLine()` 函数：

```cpp
QStringList lines;
while (tcpSocket.canReadLine())
    lines.append(tcpSocket.readLine());
```

然后我们将处理每个被读取的行。至于发送数据，可以使用 `QTcpSocket` 上的 `QTextStream` 完成。

我们所使用的服务器实现在存在大量连接时扩展性并不良好。问题在于，当我们处理一个请求时，没有处理其他连接。更具扩展性的方法是……

### UDP 示例

它们的内容包含在五个只读的 `QLineEdit` 中。这里感兴趣的唯一私有变量是类型为 `QUdpSocket` 的 `udpSocket`，我们将用它接收数据包。

#### 代码视图

```cpp
WeatherStation::WeatherStation(QWidget *parent)
    : QDialog(parent)
{
    udpSocket.bind(5824);

    connect(&udpSocket, SIGNAL(readyRead()),
            this, SLOT(processPendingDatagrams()));
    ...
}
```

在构造函数中，我们首先将 `QUdpSocket` 绑定到气球传输的端口。由于我们没有指定主机地址，套接字将接受发送到运行 `WeatherStation` 机器的任何 IP 地址的数据包。然后，我们将套接字的 `readyRead()` 信号连接到私有的 `processPendingDatagrams()` 槽，该槽负责提取并显示数据。
