
top->addLayout( hb );

The layout direction, horizontal or vertical, is determined at the point of instantiation, via the Direction argument to the constructor. You will note (perhaps with a bit of disappointment) that this value can be interrogated after instantiation, but cannot be changed.

As widgets (or other layouts) are added to the QBoxLayout, a cell is created within the layout to manage its geometry. It’s important to provide appropriate minimumSize() and maximumSize() methods for widgets you add. This will prevent the layout from resizing your widget to an inappropriate value. While most widgets you add will provide this automatically, you will undoubtedly run into at least one instance where the widget does not size correctly.

QBoxLayouts have two margin values associated with them. The first is the margin between the layout itself and surrounding objects, and is referred to as the border width. The second is the margin between each cell of the layout itself, and is referred to as the intra widget width. These margins are set via arguments to the constructor.

A term you need to be familiar with regarding QLayouts is stretch. The stretch of a given cell determines how that cell will resize, relative to other cells in the layout. As an example, consider the extremely common scenario in which you create several, vertically arranged pairs of labels and text fields. You probably want the text fields to resize more than their accompanying labels. You may not want the labels to resize at all, but that usually produces an undesirable “cramped” appearance. The following code fragment demonstrates a possible approach that will cause the labels to align with their text fields and horizontally resize in a manner that creates an overall spaciousness as the width is increased:

```cpp
int a;
QLabel *labs[10];
QLineEdit *fields[10];
QString str;
int StdA = AlignVCenter|AlignRight;

// A toplevel layout with 10 pels border-width and
// 5 pels of intra-widget spacing
QBoxLayout *ftop = new QBoxLayout( this, 10, 5 );
// Two vertical layout children that the toplevel
// layout will horizontally resize in a 2:5 ratio
QBoxLayout *lVbox = new QBoxLayout( );
ftop->addLayout( lVbox, 2 );
QBoxLayout *fVBox = new QBoxLayout( );
ftop->addLayout( fVBox, 5 );
for(a=0;a<5;a++) {
    str.sprintf( "Data Field %d", a+1);
    labs[a] = new QLabel( str, this );
    labs[a]->setAlignment( StdA );
    lVBox->addWidget( labs[a] );
    fields[a] = new QLineEdit( this );
    fVBox->addWidget( fields[a] );
}
```

## QGridLayout

Grid layouts are two-dimensional layouts arranged in rows and columns. The same behavior can be achieved using QBoxLayouts—at the expense of a lot more coding.

### A Possible Instantiation

```cpp
QGridLayout *gl = new QGridLayout( this, 2, 3 );
```

### Example Use

```cpp
int a, b;
QString s;
QLabel *l;

QGridLayout *gl = new QGridLayout( this, 2, 3 );
for(a=0;a<2;a++) {
    for(b=0;b<3;b++) {
        s.sprintf( "%d %d", a, b );
        l = new QLabel( s, this );
        gl->addWidget( l, a, b );
    }
}
```

## QRect, QPoint, and QSize

These classes encapsulate screen coordinates and size information and provide convenient conversion methods to support most requirements likely to be encountered. Most of the Qt widgets (and QWidget itself) accept these classes for geometry specifiers.

### A Possible Instantiation

```cpp
// get the current desktop size
QRect r_wsSize = QApplication::desktop()->rect();

// Convert to a QSize
QSize s_wsSize( r_wsSize.width(), r_wsSize.height() );
```

**QSizeGrip** This widget provides the resize grip graphic for a top-level window. Since QStatusBar (provided by QMainWindow) already incorporates a QSizeGrip, it is unlikely that you'll need to create an instance of this explicitly.

### A Possible Instantiation

```cpp
QSizeGrip *eg = new QSizeGrip( this );
```

**QSizePolicy** This is the attribute object that determines how horizontal and vertical resizing is to be performed. Use this attribute to set an appropriate resize behavior for your widgets if the default is not acceptable.

Aspect ratio control and controlled resizing based on a widget’s dynamic sizeHint() value are two possible reasons why you might customize this attribute.

## LISTS, TABLES, AND LIST ITEMS

Many applications (not all) require the display of, or selection from, a list of items. When the list is static (never changes), it is sometimes best to provide an array of checkboxes, pushbuttons, toggle buttons, and so on. When the list is dynamic, subject to frequent or infrequent change, or when the list is large, it usually makes more sense to provide a scrolling list of these items and let the user pick the ones to use.

Every serious toolkit provides a list box, and so does Qt. The Qt lists are a bit faster, a little more efficient, and the class methods make a lot more sense. Other than that, you will notice very little difference in appearance or behavior from MFC, Motif, Lesstif, and others.

**QHeader** QHeader (Fig. 3.17) provides a heading for tables, such as those provided by the QListView widget. They allow the end-user to rearrange columns, resize columns of tabular data, or toggle the sorting order.

![](img/64220583cb3d8a303f33ac97f5433b04_107_0.png)

**Figure 3.17** QHeader widgets in a QListView

### Example Use

```cpp
// Create a list and implied header-3 cells
QListView *theView = new QListView( this );
theView->addColumn( "Employees" );
theView->addColumn( "Salary" );
theView->addColumn( "Raise" );

// If profits were uninspired...
if( profits < ideal ) {
    theView->header()->setLabel( 2, "Pay Cut" );
}
```

## QListBox

QListBox (Fig 3.18) provides typical list box functionality. It presents a list of read-only items and provides signals when a user selects an item or changes her selection. Vertical and horizontal scrollbars are displayed if the size of the displayed data is greater than the list box's viewport.

![](img/64220583cb3d8a303f33ac97f5433b04_108_0.png)

**Figure 3.18** QListBox widget

### A Possible Instantiation

```cpp
QListBox *lb = new QListBox( this );
```

### Example Use

```cpp
QString s;
QListBox *lb = new QListBox( this );
for(int a=0;a<1000;a++) {
    s.sprintf( "List Item %d", a );
    lb->insertItem( s );
}
```

Qt list boxes use QListBoxItems for displayed content. This is a little different from other toolkits' implementations, but provides much greater flexibility in controlling the contents of the list.

## QListBoxItem

This is the base class for all QListBox line items. It is subclassed by QListBoxPixmap and QListBoxText, which are discussed below.

While it is certainly a matter of preferences and style, I feel it is confusing to provide multiple objects in a list item (e.g., a pixmap and a text item). This is only because a listbox does not provide column headers that provide a clue as to what the user is supposed to be looking at. Aren't opinions useful?

## QListBoxPixmap

This is a list box item that provides only a pixmap.

## QListBoxText

This is a list box item that provides only a text label.

## QListView

List views (Fig 3.19) provide a tabular view with optional tree behavior. List views display QListViewItems, which can contain a limited number of pixmap or text label items. The Qt examples included with the Qt software distribution adequately demonstrate the many uses for list views, so I won't bore you with detailed examples.

![](img/64220583cb3d8a303f33ac97f5433b04_109_0.png)

### A Possible Instantiation

```cpp
QListView *theView = new QListView( this );
```

### Example Use

```cpp
// Create a list and implied header-3 cells
QListView *theView = new QListView( this );
theView->addColumn( "Employee" );
theView->addColumn( "Salary" );
theView->addColumn( "Raise" );

// If profits were uninspired...
if( profits < ideal ) {
    theView->header()->setLabel( 2, "Pay Cut" );
}
QCheckBox *cb = new QCheckBox( "Option A", this );
QListViewItem *li = new QListViewItem( theView,
    "Billy", "$0.14/week", "$0.02" );
```

Data sets, or line-items, in a Qt list view are encapsulated by the QListViewItem or its descendants. QListViewItems can be tracked or enumerated with a QListViewItemIterator.

Tree behavior and appearance in a Qt list view is a function of QListViewItem parenting: a QListViewItem whose parent is the QListView itself will have top-level appearance in the list view, while a QListViewItem that has one of these top-level widgets for a parent will appear as a second-level child of the list view, and so on.

## QListViewItem

A QListView displays information using QListViewItems (see Fig. 3.20) and QListViewItems can manage very large data sets quite well. The parenting of QListViewItems determines QListView tree appearance and behavior.

![](img/64220583cb3d8a303f33ac97f5433b04_110_0.png)

### A Possible Instantiation

```cpp
QListViewItem *li = new QListViewItem( parent_ListView,
    "Column0", "Column1", "Column2" );
```
