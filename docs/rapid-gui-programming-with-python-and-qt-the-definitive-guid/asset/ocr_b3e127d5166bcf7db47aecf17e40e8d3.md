The Thread subclass has one static variable and four methods. The sendReply() and sendError() methods are identical to those shown in the preceding chapter, so we will omit them.

```
class Thread(QThread):
    lock = QReadWriteLock()
    def __init__(self, socketId, parent):
        super(Thread, self).__init__(parent)
        self.socketId = socketId
```

The Thread.lock variable is static, so all the Thread instances share it. The initializer simply takes note of the socket descriptor ready for when the thread is started. The run() method is quite long, so we will review it in parts.

```
def run(self):
    socket = QTcpSocket()
    if not socket.setSocketDescriptor(self.socketId):
        self.emit(SIGNAL("error(int)"), socket.error())
        return
    while socket.state() == QAbstractSocket.ConnectedState:
        nextBlockSize = 0
        stream = QDataStream(socket)
        stream.setVersion(QDataStream.Qt_4_2)
        while True:
            socket.waitForReadyRead(-1)
            if socket.bytesAvailable() >= SIZEOF_UINT16:
                nextBlockSize = stream.readInt16()
                break
            if socket.bytesAvailable() < nextBlockSize:
                while True:
                    socket.waitForReadyRead(-1)
                    if socket.bytesAvailable() >= nextBlockSize:
                        break
```

We begin by creating a new socket and setting its socket descriptor to the one we were given. We take a slightly more robust approach than before, checking the return value of the QTcpSocket.setSocketDescriptor() call, and giving an error message on failure. Once the run() method finishes, the finished() signal is emitted and, thanks to our earlier signal–slot connection, the thread will be deleted.

As long as the socket is connected, we can use it to receive requests and send responses. Unlike the TCP server we created in the preceding chapter, rather than running asynchronously and waiting for things to happen, such as data being available, through signal–slot connections, here we block using waitForReadyRead() until there is data. (The −1 argument means “wait forever”.) It does not matter that we block, because we are in a separate thread of execution, so