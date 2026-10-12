QListView and QListWidget

Through these widgets users can choose an item, or with a suitable selection mode, multiple items. The widgets can be in list mode (as shown), or icon mode, where the icons appear larger and the text is displayed under the icons. A QListView must be used in conjunction with a custom or built-in QAbstractItemModel subclass using QListView.setModel(). A QListWidget has a built-in model, so items can be added to it directly using QListWidget.addItem() and QListWidget.addItems(). Where vertical space is at a premium, a QComboBox can be used instead.

QProgressBar

This widget can be used to show users the progress of long-running operations. It is often put in a QMainWindow's status bar using QStatusBar.addWidget() or addPermanentWidget(). An alternative is to pop up a QProgressDialog.

QPushButton

Buttons are used to invoke actions. If a button click will lead to a dialog being popped up, we normally add an ellipsis (...) to the end of the button's text. Buttons can also be set to have pop-up menus (in which case, PyQt will add a little triangle indicator), or they can be set as toggle buttons, staying down when clicked an odd number of times and coming back up when clicked an even number of times. Since Qt 4.2, most applications use QDialogButtonBoxes rather than individual QPushButtons.

QSlider

A slider is often used to show proportionality, and is commonly used in conjunction with a QLabel or QLCDNumber that shows an actual amount. Sliders can be aligned vertically or horizontally. A QScrollBar could be used for a similar purpose.

QDoubleSpinBox and QSpinBox

These widgets are used to accept and display numbers. The number can be shown with a prefix or suffix and with a particular alignment. (The QDoubleSpinBox shown here has a "$" prefix.) They can have minimum and maximum values set, and for the QDoubleSpinBox, the number of digits shown after the decimal point can be set. An alternative is to use a QLineEdit in conjunction with a QIntValidator or a QDoubleValidator.