```
lVBox->addWidget( labs[a] );
fields[a] = new QLineEdit( this );
fVBox->addWidget( fields[a] );
}
```

# QGridLayout

Grid layouts are two-dimensional layouts arranged in rows and columns. The same behavior can be achieved using QBoxLayouts—at the expense of a lot more coding.

# A Possible Instantiation

```
QGridLayout *gl = new QGridLayout( this, 2, 3 );
```

# Example Use

```
int a, b;
QString s;
QLabel *l;

QGridLayout *gl = new QGridLayout( this, 2, 3 );
for(a=0;a<2;a++) {
    for(b=0;b<3;b++) {
        s.sprintf( "&d", a, b );
        l = new QLabel( s, this );
        gl->addWidget( l, a, b );
    }
}
```

# QRect, QPoint, and QSize

These classes encapsulate screen coordinates and size information and provide convenient conversion methods to support most requirements likely to be encountered. Most of the Qt widgets (and QWidget itself) accept these classes for geometry specifiers.

# A Possible Instantiation

```
// get the current desktop size
QRect r_wsSize = QApplication::desktop()->rect();

// Convert to a QSize
QSize s_wsSize( r_wsSize.width(), r_wsSize.height() );
```