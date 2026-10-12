
# 索引

## QSqlQuery (QSql)（续）
- exec()，447，448，449，450，464，468，469
- first()，450
- isActive()，449，450
- isValid()，450
- last()，450
- lastError()，449
- next()，449，450，451，468，469
- numRowsAffected()，449，450
- prepare()，448，450，468
- previous()，449，450
- record()，450
- seek()，449，451
- setForwardOnly()，451
- size()，450
- value()，449，450，451

## QSqlQueryModel (QSql)
- 基类，QAbstractTableModel
- record()，464，465，466，469
- setQuery()，464

## QSqlRecord (QSql)
- value()，464，465，466，469

## QSqlRelation (Qsql)，456，460，462

## QSqlRelationDelegate (QSql)，456，460，461

## QSqlRelationalTableModel (QSql)，445，456，462
- 基类，QSqlTableModel
- relationModel()，456
- setRelation()，456，460，462

## QSqlTableModel (QSql)，445，453
- 基类，QSqlQueryModel
- beforeInsert()，470
- fieldIndex()，456
- insertRecord()，464
- select()，453，456，460，462，464，469
- setFilter()，464，469
- setSort()，453，456，460，462
- setTable()，453，456，460，462
- submitAll()，453，456，460，469

## QSocket (QNetwork)，521

## QStackedWidget (QtGui)，274–276
- 基类，QFrame
- setCurrentIndex()，275

## QStatusBar (QtGui)
- 基类，QWidget

## QStatusBar (QtGui)（续）
- clearMessage()，170，232
- setSizeGripEnabled()，170
- showMessage()，170，233

## QString (QtCore)，19，23，28，233，234，256，313，402
- arg()，402，418，419，423，427，428，455，513，515
- compare()，435
- contains()，234
- endsWith()，240
- indexOf()，306，387，388
- isEmpty()，233
- isNull()，45
- lastIndexOf()，234
- left()，234，306
- length()，388
- localeAwareCompare()，416，434
- mid()，252
- number()，338
- simplified()，61，422
- split()，253
- startsWith()，252
- toInt()，251，422
- toLower()，327
- trimmed()，252，422
- 参见 str 类型和 unicode 类型

## QStringList (QtCore)，45，189
- contains()，189
- isNull()，45
- prepend()，189
- takeLast()，189

## QStyleOptionGraphicsItem (QtGui)，374

## QStyleOptionViewItem (QtGui)，438，439，461

## QSvgGenerator (QtGui)，329，363
- 基类，QPaintDevice

## QSvgRenderer (QSvg)，363

## QSyntaxHighlighter (QtGui)，386–389

## Qt 命名空间，258
- escape()，258，397，401
- WindowStaysOnTopHint，529

## Qt Assistant 应用程序，510

## Qt Designer 应用程序，205–216，272，274，275，276，277，280，324，326，333

## Qt::ItemDataRole (QtGui)，231

## Qt Linguist 应用程序，513

## Qt::WidgetAttribute (QtGui)
- WA_DeleteOnClose，156，158，284，286
- WA_GroupLeader，511

## QTableView (QtGui)，415，425，427，458，460，463，477，490，579
- 基类，QAbstractItemView
- horizontalHeader()，463，464
- resizeColumnsToContents()，232，419，460，463，490
- setColumnHidden()，460，463
- setSortingEnabled()，418，419

## QtTableWidget (QtGui)，230–232，310，313，414，418，579
- 基类，QTableView
- clear()，418
- currentColumn()，422
- currentItem()，422
- editItem()，422
- item()，422
- itemChanged() 信号，417
- 填充数据，418
- scrollToItem()，232
- setColumnCount()，231，418
- setCurrentItem()，232，419
- setHorizontalHeaderLabels()，231，418
- setItem()，231，419
- setRowCount()，231，418

## QtTableWidgetitem (QtGui)，231–232，418，419
- data()，422
- setData()，419
- setSelected()，232，419
- setTextAlignment()，231，419
- text()，422

## QtTabWidget (QtGui)，272–274，579
- 基类，QWidget

## QtCore 模块 (PyQt4)，19
- pyqtProperty()，322
- @pyqtSignature()，218，219

## QtCore 模块 (PyQt4)（续）
- PYQT_VERSION_STR 变量，200
- QT_VERSION_STR 变量，200
- QT_SIP_SIGNAL()，131
- QT_SIP_SLOT()，131
- 参见类名下的条目

## QTcpServer (QtNetwork)，529，530，539
- incomingConnection()，530，539
- listen()，529

## QTcpSocket (QtNetwork)，522，524，531，540
- 基类，QAbstractSocket

## QTTextBlock (QtGui)，396

## QTTextBlockFormat (QtGui)，404

## QTTextBrowser (QtGui)，117，381，511，579
- 基类，QTTextEdit

## QTTextCharFormat (QtGui)，386，387，404

## QTTextCursor (QtGui)，297，384，403–407
- currentFrame()，404
- hasSelection()，385
- insertBlock()，404
- insertImage()，404
- insertTable()，404
- insertText()，384，404
- removeSelectedText()，297
- selectedText()，297
- setPosition()，406

## QTTextDocument (QtGui)，381，383，396，398，401–407，403，438，439，489
- 基类，QObject
- clear()，383
- drawContents()，438，489
- idealWidth()，390，439，489
- isEmpty()，385
- isModified()，287，385
- print()，403，407
- setDefaultFont()，438，439，489
- setHtml()，403，438，439，489
- setModified()，286，383，384
- toHtml()，407

## QTextEdit (QtGui)，285，310，381，383，390，392，579

## QTextEdit (QtGui)（续）
- 基类，QAbstractScrollArea
- append()，120
- canPaste()，385
- currentCharFormat()，393，395
- cursorRect()，392，393
- cut()，385
- document()，286，287，383，384，385，396
- ensureCursorVisible()，392，393
- insertPlainText()，297
- mergeCurrentCharFormat()，395
- setHtml()，488
- setLineWrapMode()，390
- setPlainText()，384
- setTabChangesFocus()，390
- setTextColor()，393
- textCursor()，297，384，385
- toHtml()，395
- toPlainText()，384，395

## QTextOption (QtGui)，409

## QTextStream (QtCore)，250–255，254，258，384
- atEnd()，252，253，254
- readAll()，384
- readLine()，252，253，254
- setCodec()，250，252，254，258，384

## QTextTableFormat (QtGui)，404

## QtGui 模块 (PyQt4)，19
- 参见类名下的条目

## QThread (QtCore)，538，540
- isRunning()，547，551
- run()，538，540，548，553
- start()，539，547，553
- wait()，547，548，551

## QTime (QtCore)，45
- isNull()，45
- 参见 time 模块

## QTimeEdit (QtGui)，576
- 基类，QAbstractTimeEdit

## QTimer (QtCore)，373，376
- 基类，QObject
- singleShot()，115，306
- start()，373，376
- timeout() 信号，373，376

## QNetwork 模块 (PyQt4)，521，523
- 参见类名下的条目

## QToolBar (QtGui)，179–180，180
- 基类，QWidget
- addSeparator()，178，180

## QToolTip (QtGui)，171，200，514

## QTransform (QtGui)，356

## QTreeWidgetItem (QtCore)，516

## QTreeView (QtGui)，415，495，579
- 基类，QAbstractItemView
- 填充数据，502
- setItemsExpandable()，420
- setUniformRowHeights()，495

## QTreeWidget (QtGui)，414，579
- 基类，QTreeView
- clear()，420
- expandItem()，421
- 填充数据，420
- setColumnCount()，420
- setCurrentItem()，421
- setHeaderLabels()，420

## QTreeWidgetItem (QtGui)，420，421

## QtSql 模块 (PyQt4)，445，446
- 参见类名下的条目

## QtSvg 模块 (PyQt4)，363
- 参见类名下的条目

## QT_VERSION_STR 变量，200

## QtXml 模块 (PyQt4)，235
- 参见类名下的条目

## QUdpSocket (QtNetwork)，522
- 基类，QAbstractSocket

## 查询
- 数据库；参见 QSqlQuery 和 SQL 语句

## question() (QMessageBox)，187，188，361，423，455

## quit() (QCoreApplication)，115
- 退出应用程序；参见 终止应用程序

## 带引号的字符串
- 参见 字符串字面量

## QVariant (QtCore)，183，185，231，323，392，414，427，428，429，430，441，448，451，488，496
- toBool()，324
- toDate()，487，491
- toDateTime()，449
- toDouble()，481

## QVariant (QtCore)（续）
- toInt()，395，431，449
- toLongLong()，422
- toString()，427，431，441，449，488

## QBoxLayout (QtGui)，146，270
- 基类，QBoxLayout

## QWidget (QtGui)，118，119，127，168，273，305，306，309，322–324，324，325–326，328，329，330，331，370，421
- 基类，QObject 和 QPalette
- QDevice
- activateWindow()，160，289
- addAction()，172，178，180，307，330，365，392，393
- addActions()，178
- close()，175，285，289，330
- closeEvent()，175，185，187，282，285，289，293，309，551
- contextMenuEvent()，307，309，390
- dragEnterEvent()，309，314，316
- dragMoveEvent()，309，314，315，316
- dropEvent()，309，315，316
- font()，336，342
- geometry()，357
- hasFocus()，330，426
- hasMouseTracking()，308
- height()，330
- hide()，279，330
- keyPressEvent()，307，309，334，391，483
- keyReleaseEvent()，307
- layout()，277
- mapFromGlobal()，357
- mapToGlobal()，309，392，393
- maximumHeight()，390
- minimumHeight()，390
- minimumSizeHint()，271，335，340，341，479
- mouseDoubleClickEvent()，308，309，417，422，440
- mouseMoveEvent()，309，317
- mousePressEvent()，309，333
- mouseReleaseEvent()，308，309

## QWidget (QtGui)（续）
- move()，183，330，341
- paintEvent()，306，309，336，342，480
- palette()，337
- raise()，160，289，330
- rect()，306，330
- resize()，183
- resizeEvent()，306，309，341
- restoreGeometry()，183，186，330
- saveGeometry()，183，186，330
- setAcceptDrops()，312，313，314，315，316，330
- setAttribute()，156，284，330，511
- setTextMenuPolicy()，168，330，365
- setCursor()，330
- setEnabled()，219，330
- setFocus()，120，310，330，422，369，478
- setFocusPolicy()，180，217，331，369，478
- setFont()，330
- setLayout()，273，279，330
- setMaximumHeight()，390
- setMinimumHeight()，390
- setMinimumSize()，168，340
- setMinimumWidth()，340
- setMouseTracking()，308，334
- setSizePolicy()，330，331，340
- setStatusTip()，171，180
- setStyleSheet()，323，330
- setTabOrder()，206
- setToolTip()，171，180，390
- setVisible()，277，280
- setWindowFlags()，529
- setWindowIcon()，156，330
- setWindowModified()，192
- setWindowTitle()，146，151，186，330，370
- show()，115，155，280，286，330，511
- showMinimized()，297
- showNormal()，297
- sizeHint()，335，390，479
- update()，306，330，332，479，482

