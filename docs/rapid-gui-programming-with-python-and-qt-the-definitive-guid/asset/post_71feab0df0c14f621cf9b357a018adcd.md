
![](img/9bfe0a027fcc8793bb087287001100dd_486_0.png)

Figure 15.7 The Reference Data dialog

If the user clicks Delete, pop up a yes/no message box, and delete only if they click the Yes button. The application is similar to the ReferenceDataDlg from the Asset Manager application, and can be written in about 130 lines.

A solution is provided in chap15/referencedata.pw.

# Part IV

## Advanced GUI Programming

# Part IV

## Advanced Model/View Programming

In the two preceding chapters we explored the basics of PyQt model/view programming. We saw how to create custom models, and how to use the predefined SQL table models. We also saw how to create custom delegates to control the appearance and editing of data items. In this chapter, we will deepen our knowledge of PyQt model/view programming.

All of the topics covered in this chapter, and the ones that follow, are more advanced than the ones we have seen before, at least conceptually. However, in most cases the code is no more difficult than what we have already seen.

In the first section we will look at how to implement a custom view so that we can see how to visualize our data in any way we want. This section is useful for understanding more about how views work, and to see one straightforward approach to implementing a custom view.

The second section revisits the subject of custom delegates, showing how to minimize code duplication and how to easily create arbitrary delegates for views. This section should prove especially useful to those who need to create many delegates, especially for datasets such as SQL tables where each column is of a particular type.

In the final section we will see how to reflect tabular data into a tree view. One use of this is where we represent tables as trees when the first few columns often contain the same values—this has the effect of reducing the number of rows that the user must navigate to find the item they want. Another use is to let users pick particular values that form a “path”. For example, rather than providing two, three, or more comboboxes, each with values that depend on the current values of its predecessors, we just provide a single tree for the user to navigate and choose from.

> *This chapter assumes a knowledge of PyQt’s model/view architecture, covered in Chapter 14.

## Custom Views

PyQt provides several view classes that work well out of the box, including QList\_View, QTableView, and QTree\_View. One thing that all these views have in common is that they are usually used to present data items textually—although all of them can also show icons and checkboxes if desired. An alternative to textual representations of data are visual representations, and for these we can use the graphics view classes covered in Chapter 12. Sometimes, though, we want to present data in a way that doesn't really match any of the classes that are available. In such cases we can create our own view subclass and use it to visualize our models.

|    | Timestamp     | °C   | Inflow | NTU  | μS/cm | mg/L | Raw Ph | Flox Ph |
|----|---------------|------|--------|------|-------|------|--------|---------|
| 640 | 2007-06-26 15:45 | 20.48 | -0.01  | 6.30 | 441.00 | 4.31 | 5.75   | 7.60    |
| 641 | 2007-06-26 16:00 | 20.48 | -0.01  | 4.30 | 448.00 | 3.53 | 6.45   | 7.60    |
| 642 | 2007-06-26 16:15 | 20.48 | -0.01  | 3.20 | 453.00 | -0.22| 7.05   | 7.50    |
| 643 | 2007-06-26 16:30 | 20.48 | 0.01   | 2.20 | 455.00 | -0.20| 7.15   | 7.50    |
| 644 | 2007-06-26 16:45 | 20.48 | 0.01   | 2.20 | 472.70 | -0.16| 7.15   | 7.40    |
| 645 | 2007-06-26 17:00 | 20.48 | -0.01  | 2.20 | 449.80 | -0.33| 7.15   | 7.40    |
| 646 | 2007-06-26 17:15 | 20.24 | 2.50   | 2.10 | 394.60 | 209.17| 6.50  | 6.15    |
| 647 | 2007-06-26 17:30 | 20.55 | 2.80   | 2.10 | 394.10 | 192.36| 7.11  | 8.12    |

![](img/9bfe0a027fcc8793bb087287001100dd_490_0.png)

Figure 16.1 shows the same dataset presented by two different views. The left-hand view is a standard QTableView, and the right-hand view is a custom WaterQuality\_View. Both show the timestamps of water quality readings textually, but the WaterQuality\_View shows colored circles for three key indicators, and it uses Unicode arrow symbols to signify special flow situations. Obviously, the table view presents the facts in a clear and accurate way, but the water quality view makes it easier to see what the situation is at any particular time, and it makes it easier to get an impression of any important trends, just by looking at the colors.

The water quality dataset covers a six-month period at one small water treatment plant—but with readings taken every 15 minutes, this adds up to slightly more than 17,500 readings. This implies that our view is going to need a vertical scrollbar. PyQt offers three ways to get scrollbars. One way is to create a widget that inherits QAbstractScrollArea; this approach is used by the QGraphics\_View and QTextEdit widgets. Another way is to create a composite widget that includes a couple of QScrollBars. But PyQt's documentation recommends the third way—using the much simpler QScrollArea instead. The one disadvantage of using QScrollArea is that it is one of the few PyQt classes not designed to be subclassed. Instead, we must create an instance and add it to the widget for which we want scrollbars. To put this into perspective here is the Water Quality Data application's initializer:

```python
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

```python
class WaterQualityView(QWidget):
    FLOWCHARS = (unichr(0x21DC), unichr(0x21DD), unichr(0x21C9))

    def __init__(self, parent=None):
        super(WaterQualityView, self).__init__(parent)
        self.scrollArea = None
        self.model = None
        self.setFocusPolicy(Qt.StrongFocus)
        self.selectedRow = -1
        self.flowfont = self.font()
        size = self.font().pointSize()
        if platform.system() == "Windows":
            fontDb = QFontDatabase()
            for face in [face.lower() for face in fontDb.families()]:
                if face.contains("unicode"):
                    self.flowfont = QFont(face, size)
                    break
            else:
                self.flowfont = QFont("symbol", size)
            WaterQualityView.FLOWCHARS = (
                chr(0xAC), chr(0xAE), chr(0xDE))
```

Setting the focus policy to anything (except Qt.NoFocus) means that the widget can accept keyboard focus. We will discuss why we have done this, and the selectedRow instance variable, at the end of this section.

When water flow is going the wrong way, or too slowly, or too quickly, we want to indicate the situation with a suitable character—for example, ←, →, and ↓. These characters are available in Unicode, but most of the default fonts supplied with Windows don’t appear to include the whole Unicode character set, so all the arrows are shown as □ characters. (On Linux, if a Unicode character is not available in the current font, PyQt can usually find the character in another font, in which case it uses that font just for that character.)

To solve this problem on Windows we iterate over the list of available fonts until we find one with “Unicode” in its name (e.g., “Lucida Sans Unicode”). If we find such a font, we store it as the flow font; otherwise, we fall back to the standard (but non-Unicode) Symbol font and use the nearest equivalent characters in that font.

```python
    def setModel(self, model):
        self.model = model
        self.connect(self.model,
            SIGNAL("dataChanged(QModelIndex,QModelIndex)"),
            self._dataNewSize)
        self.connect(self.model, SIGNAL("modelReset()"),
            self._dataNewSize)
        self._dataNewSize()
```

Once a model is set on the view we connect to its data-changed and reset signals so that the view can be resized to match the available data.
