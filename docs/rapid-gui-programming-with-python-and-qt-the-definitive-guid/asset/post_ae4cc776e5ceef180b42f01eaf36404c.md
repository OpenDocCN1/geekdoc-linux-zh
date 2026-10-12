
# 526 Chapter 18. Networking

Figure 18.2 shows the data that is written to the request `QByteArray`. A `QByteArray` can be read from and written to just like any other `QIODevice`. The first two bytes contain an unsigned integer, initially with the value 0. This integer is used to store the number of bytes occupied by the request (excluding the size of the integer itself), that is, the number of bytes that follow it. We must start by making it 0 because we do not know how many bytes will be used.

![](img/9bfe0a027fcc8793bb087287001100dd_540_0.png)

After the size integer, we write the data. The action string is the request action ("BOOK" or "UNBOOK"), the room string holds a room number (e.g., "213"), and the date holds a `QDate`. Once the data has been written to the byte array, we use `seek()` to move the writing position to the beginning so that what we write next will overwrite the start of the `QByteArray`. (We actually perform the seek on the `QDataStream`'s underlying `QIODevice`, which is retrieved by the `QDataStream.device()` call.) We write an unsigned 16-bit integer whose value is the length of the `QByteArray` minus the size of the initial integer. The request byte array is now ready to be sent.

We update the user interface—this will disable the Book and Unbook buttons since the request object is not None; this is to prevent the user from making additional requests before a response has been received. We then make sure that the socket is closed, since it may have been opened to handle a previous request, and set the response label to inform the user that we are attempting to establish a connection.

Finally, we call `connectToHost()`. The IP address can be given as a dotted string (e.g., "82.94.237.218"), as a hostname (e.g., "www.python.org"), or as a `QHostAddress` object. Thanks to the signal–slot connections that we made in the initializer, we know that once the connection is established our `sendRequest()` method will be called, unless the connection fails, in which case either the `serverHasStopped()` or the `serverHasError()` method will be called instead.

```python
def sendRequest(self):
    self.responseLabel.setText("Sending request...")
    self.nextBlockSize = 0
    self.socket.write(self.request)
    self.request = None
```

Once the connection has been established this method is called. It updates the response label to tell the user that the request is being sent, and sets the next block size to be 0. This is concerned with the *response* we hope to get back; we will see it in use in the `readResponse()` method. Then it writes the request byte array to the socket. Once the data is written, the request is set to None, ready for a new request to be made.

If no error occurs, and providing the server has not been terminated, the server will respond, and at that point the `readResponse()` method will be called. (Otherwise, either the `serverHasStopped()` or the `serverHasError()` method will be called.)

![](img/9bfe0a027fcc8793bb087287001100dd_541_0.png)

The server has two different response formats, as shown in Figure 18.3. When the response is received we must begin by reading its size from the unsigned integer. Then, once we know that at least as many bytes as the size are available to read, we read the first `QString`. If this contains the text “ERROR”, we know that we have an error response, and we can simply read the second string that contains the error message; otherwise, the text will be “BOOK” or “UNBOOK”, that is, the request action, with the request’s details, the room in the second `QString`, and the date as a `QDate`, to confirm that the request’s action has succeeded.

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

It is possible that the server's response will be returned in fragments. For this reason we use an infinite loop, first to retrieve the byte count and then to ensure that there are at least that number of bytes available to read. This leaves the responsibility for buffering with the server, and it means that when we read we know that we can read a complete response in one go.

If at least two bytes are available, we read them as an unsigned 16-bit integer: this gives us the number of bytes that are to follow. Then we test to see whether there are enough bytes to read: if there aren't, we exit the loop and wait for another `readyRead()` signal to result in the `readResponse()` method being called. If there are enough bytes, we read the action, and the string that follows—this is either the room number or an error message. If the action is not “ERROR”, we also read the date. Then, depending on which action we received, we prepare a message string and display it in the response label.

Having read an entire response we reset the next block size since we have read that many bytes. Now when we loop, either another response is waiting, in which case `QTcpSocket.bytesAvailable()` will return a value greater than zero, and we repeat the process of reading and displaying; or there is no other response and we simply break out of the loop and finish.

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

If the server is terminated or if the server responds with a networking error (rather than with our own “ERROR” response), the relevant `serverHas*()` method is called. In both cases, we display the error message to the user in the response label and close the socket.

The `BuildingServicesClient` class is now complete. The user can enter their booking and unbooking requests and send them to the server by clicking the Book and Unbook buttons, and can see the results of their requests displayed in the response label. Requests are sent by writing a `QByteArray` to a suitably set up socket. Responses are read back from the socket through a `QDataStream`; this enables us to directly read `QStrings`, `QDates`, and any other data-stream-supported types, into local variables.

Now that we have seen how the client is created, we can turn our attention to the server.

## Creating a TCP Server

The Building Services TCP server is in `chap18/buildingservicesserver.pyw`. It has three components: a GUI that holds a TCP server instance and that provides an easy means by which the user can terminate the server, a `QTcpServer` subclass that is instantiated to provide the server instance, and a `QTcpSocket` subclass that is used to handle incoming connections. We will begin by looking at the first two, since they are short, and then focus on the `QTcpSocket` subclass where most of the work is done.

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

Just for a change, and to remind us that any PyQt widget can be a top-level window, we have made the dialog a `QPushButton` subclass. We have also set the `Qt.WindowStaysOnTopHint`; most windowing systems will respect the hint and keep the widget on top of all other windows.

We won't cover the `loadBookings()` method; it is used to populate the in-memory data structure, the `bookings` default dictionary, that holds the bookings data. The dictionary's keys are dates stored as `datetime.date` objects, and the values are ordered lists of room numbers stored as unicode strings. Default dictionaries were introduced with Python 2.5. They are like normal dictionaries, except that when we use a key that isn't in the dictionary, the key is inserted with a default value. What default value is used depends on how we create the dictionary. In the Building Services server we have created the dictionary like this:

```python
bookings = collections.defaultdict(list)
```

Here we have said that the default value for any new key is to be an empty `list`; in other cases, we might have chosen an empty set. We can always replace a default dictionary with a normal dictionary—for example, if using a Python version older than 2.5—by using the `dict.setdefault()` method when accessing possibly nonexistent keys, as we will show later.

![](img/9bfe0a027fcc8793bb087287001100dd_543_0.png)
