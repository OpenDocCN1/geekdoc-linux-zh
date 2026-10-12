We have subclassed QWidget rather than QDialog or QMainWindow. The only noticeable difference is that had we subclassed QDalog, pressing Esc would have terminated the application.

We have three objects to store. The first is the socket that the client will use to communicate with the server. The second is the "next block size"; this is a variable that we use to determine whether we have received sufficient response data to be able to process the response. The third is a request object; this is a QByteArray containing the request data, or none if we have no data to send.

We will skip the creation, setup, and laying out of the widgets, since all of that should all be familiar by now, although we will look at the widget connections after we have looked at the socket connections.

```
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

The first four signals are concerned with the socket. We need to know when the connection is established, since at that point we can send our request data. We also need to know whether the socket has data to read, since when it does, it will have the server's response, which we want to read. If the connection is terminated—for example, because the server has been shut down or an error has occurred—we want to know so that we can inform the user.

```
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

The other connections are concerned with the user interface. As usual, we have an updateUi() method for doing validation and for enabling/disabling the buttons as appropriate. We also have connections to book and unbook rooms and to terminate the application.

```
def updateUi(self):
    enabled = False
    if not self.roomEdit.text().isEmpty() and \
```