# Creating a TCP Server

The Building Services TCP server is in chap18/buildingservicesserver.pyw. It has three components: a GUI that holds a TCP server instance and that provides an easy means by which the user can terminate the server, a QTcpServer subclass that is instantiated to provide the server instance, and a QTcpSocket subclass that is used to handle incoming connections. We will begin by looking at the first two, since they are short, and then focus on the QTcpSocket subclass where most of the work is done.

```
```python
class BuildingServicesDlg(QPushButton):
    def __init__ (self, parent=None):
        super(BuildingServicesDlg, self).__init__(
            "&Close Server", parent)
        self.setWindowFlags(Qt.WindowStaysOnTopHint)

        self.loadBookings()
        self.tcpsvr = TcpServer(self)
        if not self.tcpsvr.listen(QHostAddress("0.0.0.0"), PORT):
            QMessageBox.critical(self, "Building Services Server",
                                 Qstring("Failed to start server: %1") .arg(self.tcpsvr.errorString()))
        self.close()

        self.connect(self, SIGNAL("clicked()"), self.close)
```
```

Just for a change, and to remind us that any PyQt widget can be a top-level window, we have made the dialog a QPushButton subclass. We have also set the Qt.WindowStaysOnTopHint; most windowing systems will respect the hint and keep the widget on top of all other windows.

We won't cover the loadBookings() method; it is used to populate the in-memory data structure, the `bookings` default dictionary, that holds the bookings data. The dictionary's keys are dates stored as `datetime.date` objects, and the values are ordered lists of room numbers stored as unicode strings. Default dictionaries were introduced with Python 2.5. They are like normal dictionaries, except that when we use a key that isn't in the dictionary, the key is inserted with a default value. What default value is used depends on how we create the dictionary. In the Building Services server we have created the dictionary like this:

```
```python
bookings = collections.defaultdict(list)
```
```

Here we have said that the default value for any new key is to be an empty `list`; in other cases, we might have chosen an empty set. We can always replace a default dictionary with a normal dictionary\-for example, if using a Python version older than 2.5\-by using the `dict.setdefault()` method when accessing possibly nonexistent keys, as we will show later.

![](bbox=[0.9, 0.63, 0.97, 0.72])