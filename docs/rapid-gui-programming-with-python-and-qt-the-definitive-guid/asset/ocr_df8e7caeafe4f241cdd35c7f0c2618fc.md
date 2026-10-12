```
self.responseLabel.setText(msg)
self.updateUI()
self.nextBlockSize = 0
```

It is possible that the server's response will be returned in fragments. For this reason we use an infinite loop, first to retrieve the byte count and then to ensure that there are at least that number of bytes available to read. This leaves the responsibility for buffering with the server, and it means that when we read we know that we can read a complete response in one go.

If at least two bytes are available, we read them as an unsigned 16-bit integer: this gives us the number of bytes that are to follow. Then we test to see whether there are enough bytes to read: if there aren't, we exit the loop and wait for another readyRead() signal to result in the readResponse() method being called. If there are enough bytes, we read the action, and the string that follows—this is either the room number or an error message. If the action is not “ERROR”, we also read the date. Then, depending on which action we received, we prepare a message string and display it in the response label.

Having read an entire response we reset the next block size since we have read that many bytes. Now when we loop, either another response is waiting, in which case QTcpSocket.bytesAvailable() will return a value greater than zero, and we repeat the process of reading and displaying; or there is no other response and we simply break out of the loop and finish.

```
def serverHasStopped(self):
    self.responseLabel.setText(
        "Error: Connection closed by server")
    self.socket.close()

def serverHasError(self, error):
    self.responseLabel.setText(QString("Error: %1") \
        .arg(self.socket.errorString()))
    self.socket.close()
```

If the server is terminated or if the server responds with a networking error (rather than with our own “ERROR” response), the relevant serverHas*() method is called. In both cases, we display the error message to the user in the response label and close the socket.

The BuildingServicesClient class is now complete. The user can enter their booking and unbooking requests and send them to the server by clicking the Book and Unbook buttons, and can see the results of their requests displayed in the response label. Requests are sent by writing a QByteArr ay to a suitably set up socket. Responses are read back from the socket through a QDataS tream; this enables us to directly read QStrings, QDates, and any other data-stream-supported types, into local variables.

Now that we have seen how the client is created, we can turn our attention to the server.