```
class MainForm(QDialog):
    def __init__(self, parent=None):
        super(MainForm, self).__init__(parent)
        self.model = WaterQualityModel(os.path.join(
            os.path.dirname(__file__), "waterdata.csv.gz"))
        self.tableView = QTableView()
        self.tableView.setAlternatingRowColors(True)
        self.tableView.setModel(self.model)
        self.waterView = WaterQualityView()
        self.waterView.setModel(self.model)
        scrollArea = QScrollArea()
        scrollArea.setBackgroundRole(QPalette.Light)
        scrollArea.setWidget(self.waterView)
        self.waterView.scrollArea = scrollArea

        splitter = QSplitter(Qt.Horizontal)
        splitter.addWidget(self.tableView)
        splitter.addWidget(scrollArea)
        splitter.setSizes([600, 250])
        layout = QBoxLayout()
        layout.addWidget(splitter)
        self.setLayout(layout)

        self.setWindowTitle("Water Quality Data")
        QTimer.singleShot(0, self.initialLoad)
```

The preceding code is the whole thing. The WaterQualityModel is a QAbstractTableModel subclass that provides read-only access to a water quality data file. The WaterQualityView is the class we will develop in this section. One special thing that we have done here is to create a QScrollArea widget and add the water quality view to it—it basically means that the water quality view can be as wide and as tall as we like and the scroll area will take care of scrolling issues.

We will see shortly that keyboard users can navigate in the water quality view using the up and down arrow keys, and to ensure that the selected row is always visible we must pass the scroll area to the water quality view so that our key press handler can interact with it. Another thing that is special is that we have given initial sizes to the two parts of the horizontal splitter so that at start-up, they are roughly in the right proportions for the widgets they are holding.

We will now review the WaterQualityView, beginning with some static data and the initializer.

```
class WaterQualityView(QWidget):
    FLOWCHARS = (unichr(0x21DC), unichr(0x21XD), unichr(0x21C9))
```