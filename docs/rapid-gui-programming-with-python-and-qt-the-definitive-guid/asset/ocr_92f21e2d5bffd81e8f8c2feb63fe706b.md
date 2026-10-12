![](bbox=[0.13, 0.11, 0.85, 0.3])

**Figure 18.1** A server with two clients

up to 65 535 are valid. The server can accept two kinds of request, “BOOK” and “UNBOOK”, and can make three kinds of response, “BOOK”, “UNBOOK”, and “ERROR”. All the requests and responses are sent and received as binary data; we will look at their formats in the sections that follow.

In addition to the port number that is held in the PORT variable, we also create the SIZEDF_UINT16 variable and set it to 2 (meaning two bytes). In addition to the normal imports, we must also import the Qtnetwork module:

```
from PyQT4.QtNetwork import *
```

The same PORT and SIZEDF_UINT16 variables, and the same Qtnetwork import, are used in both the client and the server applications. In the following section, we will look at the implementation of the client, and in the second section we will review the server.

# ## Creating a TCP Client

The Building Services client is in chap18/buildingservicesclient.py. It allows the user to enter a room number (with only valid room numbers being accepted) and a date, and to request that the room is booked (or unbooked) for that date. The server responds to the request and the client displays the response for the user to read in the response label.

We will begin by looking at the initializer, but omitting the creation of the widgets and layouts. We will look at it in three parts, and then go on to look at the client's methods.

```
```
class BuildingServicesClient(QWidget):
    def __init__(self, parent=None):
        super(BuildingServicesClient, self).__init__(parent)
        self.socket = QTcpSocket()
        self.nexTBlockSize = 0
        self.request = None
```
```