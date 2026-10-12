

## QIODevice (QtCore) _(续)_
- waitForReadyRead( ), 540

## QItemDelegate (QtGui), 436, 437, 485–489
- _基类_, QAbstractItemDelegate

## QKeyEvent (QtGui), 307
- _基类_, QInputEvent
- key( ), 307, 334, 365, 384, 391, 483

## QKeySequence (QtGui), 171, 175, 285, 292, 393

## QLabel (QtGui), 114, 168, 340, 577
- _基类_, QFrame
- setAlignment( ), 168, 340
- setBuddy( ), 143, 425
- setPixmap( ), 199

## QLayout (QtGui), 146
- _基类_, QLayoutItem
- addWidget( ), 146, 151, 273
- setSizeConstraint( ), 277, 279

## QLCDNumber (QtGui), 577

## QLinearGradient (QtGui), 343

## QLineEdit (QtGui), 117, 310, 314, 440, 461, 577
- _基类_, QWidget
- inputMask 属性, 157
- returnPressed( ) 信号, 440
- setAlignment( ), 461
- setInputMask( ), 461
- setText( ), 441, 462
- setValidator( ), 461
- text( ), 441
- textEdited( ) 信号, 161, 217, 218

## QListView (QtGui), 415, 578
- _基类_, QAbstractItemView

## QListWidget (QtGui), 275, 312, 315, 414, 418, 578
- _基类_, QListView
- addItem( ), 418
- clear( ), 418
- currentRowChanged( ) 信号, 275
- 填充数据, 418
- setCurrentItem( ), 418

## QListWidgetItem (QtGui), 316, 418
- setIcon( ), 316

## QListWidgetItem (QtGui) _(续)_
- takeItem( ), 316

## QLocale (QtCore), 513, 516
- _Qm_ (Qt 消息文件), 516, 518

## QMainWindow (QtGui), 168, 186, 284, 290
- _基类_, QWidget
- dockWidget( ), 169, 186
- addToolBar( ), 179, 186
- closeAllWindows( ), 289, 293
- menuBar( ), 177, 186
- restoreState( ), 183, 186
- saveState( ), 183, 186
- setCentralWidget( ), 168, 186, 285
- statusBar( ), 170, 186

## QMatrix 和 QTransform (QtGui), 356
- reset( ), 370, 377
- scale( ), 370

## QMDIArea (QtGui), 290

## QMenu (QtGui), 307, 365, 392, 393
- _基类_, QWidget
- aboutToShow( ) 信号, 178, 187, 285, 292
- addMenu( ), 178
- addSeparator( ), 178, 180, 307
- exec( ), 307, 365, 392, 393

## QMenuBar (QtGui), 177, 178

## QMessageBox (QtGui), 153, 187, 188, 200, 361, 423, 455

## QMetaObject (QtCore), 217
- connectSlotsByName( ), 217

## QTextDocument (QtCore), 311, 313, 316
- _基类_, QObject
- data( ), 315, 316
- hasFormat( ), 314, 316
- html( ), 312
- setData( ), 316
- setHTML( ), 311

## QModelIndex (QtCore), 414, 432, 504, 508, 528
- column( ), 428, 431, 439, 461, 462, 486, 496, 503
- index( ), 427
- internalPointer( ), 504
- isValid( ), 427, 428, 504
- model( ), 438, 441, 462, 489
- row( ), 427, 491

## QModelIndex (QtCore) _(续)_
- sibling( ), 491

## QMouseEvent (QtGui), 309
- _基类_, QInputEvent
- button( ), 333
- pos( ), 309

## QMutex (QtCore), 541, 552, 553, 554

## QMutexLocker (QtCore), 554

## QObject (QtCore), 119, 127, 304, 322, 370
- blockSignals( ), 135
- connect( ), 124, 130, 133, 145, 146, 151, 158, 453
- deleteLater( ), 287, 531, 539, 544
- destroyed 信号, 286, 288
- disconnect( ), 130
- emit( ), 130, 131, 219, 333, 340, 391, 431, 440, 556
- event( ), 304, 309, 310, 384
- installEventFilter( ), 304
- parent( ), 433, 504
- 属性, 157, 211
- property( ), 322, 324
- sender( ), 135, 289, 393, 395, 440
- setObjectName( ), 169, 183, 324
- setProperty( ), 322, 324
- startTimer( ), 370
- timerEvent( ), 372
- tr( ), 513, 514, 515
- trUtf8( ), 513

## QPainter (QtGui), 306, 328, 337, 342, 343, 344, 361, 363, 400, 407–410, 408, 480
- drawArc( ), 344
- drawChord( ), 344
- drawConvexPolygon( ), 344
- drawEllipse( ), 344, 374, 377, 481
- drawImage( ), 344, 363, 400
- drawLine( ), 338, 344
- drawPath( ), 344, 377
- drawPicture( ), 363
- drawPie( ), 344
- drawPixmap( ), 344, 363, 408
- drawPoint( ), 344
- drawPolygon( ), 338, 343, 344, 345
- drawPolyline( ), 344, 345

## QPainter (QtGui) _(续)_
- drawRect( ), 337, 344, 368, 410
- drawRoundRect( ), 344
- drawText( ), 306, 338, 344, 408, 410, 481
- fillPath( ), 344
- fillRect( ), 344, 438, 481, 489
- restore( ), 343, 346, 410, 438, 482, 489
- rotate( ), 343
- save( ), 343, 346, 438, 481, 489
- scale( ), 343
- setBrush( ), 337, 344, 345, 374, 377, 481
- setMatrix( ), 343
- setFont( ), 344, 408, 482
- setPen( ), 337, 338, 343, 344, 345, 374, 377, 409, 410, 481
- setRenderHint( ), 306, 337, 342, 343, 363
- setViewport( ), 329, 342, 343, 363
- setWindow( ), 329, 342, 343, 363
- shear( ), 343
- translate( ), 343, 438, 489
- viewRect( ), 363, 400

## QPainterPath (QtGui), 374, 376
- addEllipse( ), 374, 376
- addPolygon( ), 376
- boundingRect( ), 377
- closeSubPath( ), 376

## QPaintEvent (QtGui), 480
- _基类_, QEvent
- rect( ), 480

## QPalette (QtGui), 337, 481

## QPen (QtGui), 368
- setColor( ), 368
- setWidth( ), 368

## QPicture (QtGui), 329
- _基类_, QPaintDevice

## QPixmap (QtGui), 199, 329, 392, 404, 408, 496
- _基类_, QPaintDevice
- fill( ), 392
- fromImage( ), 199
- isNull( ), 496

# 610

# 索引

## QPoint/QPointF (QtCore), 309, 338, 343, 371

## QPolygon/QPolygonF (QtGui), 343, 345, 376

## QPrintDialog (QtGui), 361, 363, 400, 403, 404, 408

## QPrinter (QtGui), 170, 329, 353, 361, 363, 398, 400, 401
- _基类_, QPaintDevice
- newPage( ), 410
- pageRect( ), 408
- setPageSize( ), 353, 398, 400

## QProcess (QtCore), 537

## QProgressBar (QtGui), 578

## QPushButton (QtGui), 276, 278, 369, 578
- _基类_, QAbstractButton
- clicked( ) 信号, 219
- defaultButton, 145, 188
- 另见 QRadioButton

## QRadioButton (QtGui), 577
- .qr (PyQt 资源文件), 173, 207, 517

## QReadWriteLock (QtCore), 540, 541, 545, 552
- lockForRead( ), 541, 542, 543, 548, 550, 551, 556
- lockForWrite( ), 542, 543, 556
- unlock( ), 541, 542, 543, 548, 550, 551, 556

## QRect/QRectF (QtCore), 355, 357, 364, 376, 410
- adjusted( ), 355, 367
- center( ), 392, 393
- contains( ), 357
- setBottom( ), 365
- setRight( ), 365
- size( ), 400

## QRegExp (QtCore), 327, 386, 387, 461

## QRegExpValidator (QtGui), 157, 327, 461

## QScintilla 附加组件, 381, 382

## QScrollArea (QtGui), 476, 477, 479

## QSettings (QtCore), 182–183, 228, 282, 293, 514
- _基类_, QObject

## QSettings (QtCore) _(续)_
- iniFormat 常量, 228
- value( ), 183

## QSignalMapper (QtCore), 292, 297–300

## QSize (QtCore), 183, 335, 341, 390, 400, 439, 489
- scale( ), 363, 400

## QSlider (QtGui), 369, 578
- _基类_, QAbstractSlider

## QSpacerItem (QtGui), 212
- _基类_, QLayoutItem

## QSpinBox (QtGui), 180, 326, 340, 440, 578
- _基类_, QAbstractSpinBox
- setRange( ), 180, 340, 440
- setSingleStep( ), 440
- setSuffix( ), 180, 340
- setValue( ), 128, 180, 340, 441
- textFromValue( ), 327, 328
- value( ), 441
- valueChanged( ), 124, 128, 199
- valueFromText( ), 327, 328

## QSplitter (QtGui), 280–283, 477
- _基类_, QFrame
- restoreState( ), 282
- saveState( ), 282
- setStretchFactor( ), 283

## QSqlDatabase (QtSql), 446
- addDatabase( ), 446, 459
- commit( ), 449, 465, 468, 469
- database( ), 465, 468, 469
- driver( ), 449
- lastError( ), 446, 450, 459, 465
- open( ), 446, 459
- rollback( ), 449, 465, 469
- setDatabaseName( ), 446, 459
- transaction( ), 449, 465, 468, 469

## QSqlDriver (QtSql), 449
- _基类_, QObject
- hasFeature( ), 449

## QSqlQuery (QtSql), 445, 446–451, 450, 464, 468, 469
- addBindValue( ), 448, 450
- bindValue( ), 448, 450, 468
- boundValue( ), 450
- driver( ), 450

