
## QAbstractItemView (QtGui) (cont.)

- setDragEnabled(), 312, 313, 315
- setEditTriggers(), 231
- setItemDelegate(), 437, 460, 463, 490
- setModel(), 425, 437, 460, 463, 477, 490
- setSelectionBehavior(), 231, 460, 463, 495
- setSelectionMode(), 231, 460, 463
- startDrag(), 316

## QAbstractScrollArea (QtGui)

- base class, QFrame
- viewport(), 392, 393

## QAbstractSlider (QtGui)

- base class, QWidget
- setRange(), 369
- setValue(), 128, 369

## QAbstractSocket (QtNetwork), 521

- base class, QIODevice
- connectToHost(), 525
- state(), 540
- waitForDisconnected(), 544

## QAbstractSpinBox (QtGui)

- base class, QWidget
- lineEdit(), 327
- setAlignment(), 340, 487
- validate(), 327, 328

## QAbstractTableModel (QtCore), 425, 427

- base class, QAbstractItemModel

## QAction (QtGui), 171–172, 175, 194, 385

- base class, QObject
- data(), 172, 393, 395
- editor, visual, 206
- isChecked(), 172, 176
- isEnabled(), 172
- setCheckable(), 393
- setChecked(), 172, 177, 393
- setData(), 172, 189, 392, 393
- setEnabled(), 172
- setSeparator(), 172
- setShortcut(), 171, 172
- setStatusTip(), 172
- setText(), 172

### QAction (QtGui) (cont.)

- setToolTip(), 172
- setWhatsThis(), 172
- toggled() signal, 172, 176, 177
- triggered() signal, 172, 176

## QActionGroup (QtGui), 176

## QApplication (QtGui), 113, 115, 304

- base class, QCoreApplication
- clipboard(), 297, 311
- palette(), 438, 489
- setQuitOnLastWindowClosed(), 121

## QBoxLayout (QtGui), 146, 326

- base class, QLayout
- addLayout(), 146
- addSpacing(), 146
- addStretch(), 146
- setStretchFactor(), 146

## QBrush (QtGui), 374, 377

## QByteArray (QtCore), 313, 316, 358, 359, 525, 526, 533

## QCalendarWidget (QtGui), 575

## QCheckBox (QtGui), 575

## QClipboard (QtGui), 297, 310–312

- base class, QObject
- hashUrl(), 312
- mimeData(), 312
- pixmap(), 311
- setImage(), 311
- setMimeData(), 311
- setPixmap(), 311
- setText(), 297, 311
- text(), 297, 311

## QCloseEvent (QtGui), 186

## QColor (QtGui), 337, 345, 371, 392, 393, 438, 481, 489

## QComboBox (QtGui), 440, 576

- base class, QWidget
- addItem(), 276
- addItems(), 440
- currentIndexChanged() signal, 124, 275
- currentText(), 441
- findText(), 142, 441, 457
- setCurrentIndex(), 441, 457
- setEditable(), 440
- setModel(), 456

### QComboBox (QtGui) (cont.)

- setModelColumn(), 456

## QContextMenuEvent (QtGui), 307

- base class, QInputEvent

## QCoreApplication (QtCore), 538

- base class, QObject
- applicationDirPath(), 173
- applicationName(), 194
- exec(), 115, 184
- installTranslator(), 516
- notify(), 305
- processEvents(), 294, 537
- quit(), 115
- translate(), 513, 515

## QCursor (QtGui), 318

- pos(), 318, 357

## QDataStream (QtCore), 240–246, 242, 245, 315, 316, 358, 359, 435, 525, 528, 531, 533, 540

- atEnd(), 245
- device(), 525, 533
- isOpen(), 525
- readBool(), 245
- readDouble(), 241, 245
- readInt(), 243, 245, 360, 435
- readUInt(), 245, 528, 540
- setVersion(), 241, 243, 245, 525, 528, 531, 533, 540
- write(), 526, 533
- writeBool(), 245
- writeDouble(), 241, 245
- writeInt(), 241, 242, 245, 359, 435
- writeUInt(), 245, 525, 533

## QDataWidgetMapper (QtGui), 453, 456

- base class, QObject
- addMapping(), 453, 456
- currentIndex(), 454, 455
- setCurrentIndex(), 454, 455
- setModel(), 453, 456
- setSubmitPolicy(), 453, 456
- submit(), 453

## QDate (QtCore), 19, 45, 253, 513

- addDays(), 491

### QDate (QtCore) (cont.)

- addYears(), 490
- currentDate(), 46, 236, 401, 490
- isNull(), 45
- toDate(), 532, 541
- toString(), 258, 401

## QDateEdit (QtGui), 487, 576

- base class, QDateTimeEdit

## QDateTime (QtCore), 45, 454, 513

- currentDateTime(), 454
- dateTime(), 455
- isNull(), 45
- setDateTime(), 454
- toString(), 455

## QDateTimeEdit (QtGui), 452, 576

- base class, QAbstractSpinBox
- date(), 487
- setCalendarPopup(), 487
- setDate(), 487
- setDateRange(), 452, 487
- setDisplayFormat(), 452, 487

## QDesktopServices (QtGui), 510

## QDialog (QtGui), 128

## QDialog (QtGui), 118, 154, 217

- base class, QWidget
- accept(), 151, 154, 425
- done(), 154, 457, 464
- exec(), 142, 154, 511
- reject(), 215
- setSizeGripEnabled(), 154

## QDialogButtonBox (QtGui), 145, 150, 576

- base class, QWidget
- accepted(), 145, 150
- addButton(), 150
- button(), 150, 158
- defaultButton(), 145, 188
- rejected(), 145, 150

## QDir (QtCore)

- homePath(), 545
- nativeSeparators(), 547, 551

## QDockWidget (QtGui), 169

- base class, QWidget
- setAllowedAreas(), 169, 170
- setFeatures(), 170

## QDomDocument (QtXml), 257, 259–262

- base class, QDomNode

### QDomDocument (QtXml) (cont.)

- documentElement(), 260
- setContent(), 259
- toString(), 257, 260

## QDomElement (QtXml)

- base class, QDomNode
- attribute(), 261
- tagName(), 260

## QDomNode (QtXml)

- firstChild(), 260
- isNull(), 260
- nextSibling(), 260
- nodeType(), 261
- toElement(), 260
- toText(), 261

## QDoubleSpinBox (QtGui), 123, 578

- base class, QAbstractSpinBox

## QDrag (QtGui), 316

- base class, QObject
- exec_(), 316
- setHotSpot(), 316
- setMimeData(), 316
- setPixmap(), 316
- start(), 316

## QDropEvent (QtGui)

- base class, QEvent
- mimeData() (QDropEvent), 314
- setDropAction(), 314, 315, 316

## QEvent (QtCore)

- accept(), 314, 333, 391
- globalPos(), 307, 309
- ignore(), 314
- type(), 384

## QFile (QtCore), 241, 243, 250, 252, 258, 259, 262

- base class, QIODevice
- exists(), 294

## QFileDialog (QtGui)

- getExistingDirectory(), 547
- getOpenFileName(), 193, 194, 233, 234, 287, 295, 356
- getSaveFileName(), 196

## QFileInfo (QtCore), 189

- fileName(), 189
- isFile(), 294
- path(), 233, 356

## QFont (QtGui), 335, 336, 408, 478

- setPointSize(), 335, 336

## QFontComboBox (QtGui), 576

- base class, QComboBox

## QFontMetrics (QtGui), 349

## QFont, 335, 336, 340, 341, 342, 390, 408, 439

## QFrame (QtGui), 277

- base class, QWidget
- setFrameStyle(), 170, 278

## QGraphicsItem (QtGui), 349, 364, 365, 366, 367, 373, 376

- boundingRect(), 365, 366, 367, 373, 377
- collidesWithPath(), 366
- collidingItems(), 366
- contains(), 366
- contextMenuEvent(), 365
- isObscured(), 366
- isSelected(), 366
- itemChange(), 362, 366
- keyPressEvent(), 365
- matrix(), 359, 377
- mouseDoubleClickEvent(), 362
- moveBy(), 366
- paint(), 366, 368, 374, 377
- pos(), 359, 366
- resetMatrix(), 366
- rotate(), 360, 366, 371, 375, 377
- scale(), 366
- scene(), 366, 375
- sceneBoundingRect(), 366, 377
- setCursor(), 366
- setEnabled(), 366
- setFlag(), 366
- setFlags(), 351, 356, 362, 364
- setFocus(), 364, 366
- setFont(), 362
- setMatrix(), 362, 364, 367, 377
- setPos(), 356, 362, 364, 367, 373, 375
- setSelected(), 356, 362, 364, 367
- setValue(), 367
- shape(), 365, 367, 374, 377
- shear(), 367
- translate(), 367

### QGraphicsItem (QtGui) (cont.)

- update(), 365, 367
- zValue(), 367

## QGraphicsLineItem (QtGui), 349

- base class, QGraphicsItem

## QGraphicsPixmapItem (QtGui), 349, 356

- base class, QGraphicsItem
- pixmap(), 359

## QGraphicsRectItem (QtGui), 355

- base class, QGraphicsShapeItem

## QGraphicsScene (QtGui), 349, 354, 369

- base class, QObject
- addEllipse(), 354
- addItem(), 354, 356, 362, 364, 371
- addLine(), 354
- addPath(), 354
- addPixmap(), 354
- addPolygon(), 354
- addRect(), 354, 355
- addText(), 354
- clearSelection(), 356, 361, 362, 364
- collidingItems(), 354, 375
- items(), 354, 372
- removeItem(), 354, 355, 359, 361, 372
- render(), 354, 361
- selectedItems(), 358, 360, 361
- setBackgroundBrush(), 354
- setSceneRect(), 354, 369
- update(), 354
- views(), 354, 362

## QGraphicsSceneContextMenuEvent (QtGui), 365

- base class, QEvent
- screenPos(), 365

## QGraphicsSimpleTextItem (QtGui), 349

- base class, QGraphicsShapeItem

## QGraphicsTextItem (QtGui), 349, 362

- base class, QGraphicsItem
- font(), 359
- toPlainText(), 359

## QGraphicsView (QtGui), 349, 351–352, 369, 577

- base class, QAbstractScrollArea
- mapToScene(), 357
- matrix(), 370
- render(), 361
- scale(), 352
- setDragMode(), 352
- setMatrix(), 370
- setRenderHint(), 352, 369
- setScene(), 354, 369

## QGridLayout (QtGui), 123, 144, 146, 150, 270, 273

- base class, QLayout
- addLayout(), 146, 151
- setColumnStretch(), 146
- setRowStretch(), 146

## QGroupBox (QtGui), 577

## QHBoxLayout (QtGui), 144, 146, 270

- base class, QBoxLayout

## QIcon (QtGui), 173, 313, 392

## QImage (QtGui), 168, 195, 197, 198, 199, 329, 400

- base class, QPaintDevice
- invertPixels(), 197
- isNull(), 400
- mirrored(), 197
- rgbSwapped(), 197
- save(), 196
- scaled(), 199
- size(), 363, 400

## QImageReader, 193

## QImageWriter, 196

## QInputDialog (QtGui), 199

## QIntEvent (QtGui)

- base class, QEvent
- modifiers(), 307, 365, 391

## QIODevice (QtCore), 526

- base class, QObject
- bytesAvailable(), 528, 531, 540
- close(), 243, 259, 525, 528
- errorString(), 241, 243, 250, 252, 258, 259, 528
- open(), 241, 243, 250, 252, 258, 259
- readAll(), 254
