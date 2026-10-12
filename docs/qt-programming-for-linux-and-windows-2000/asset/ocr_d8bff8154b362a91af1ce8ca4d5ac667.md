**QIconSet** This class provides a set of icons of various sizes and provides icons that present an enabled or disabled visual queue. You will normally use icon sets for QToolButton icons.

# *A Possible Instantiation*

```
```cpp
QPixmap p = QPixmap( "pix.bmp" );
QIconSet ico( p );
```
```

# *Example Use*

```
```cpp
#include "myicon.xpm"
QPixmap p = QPixmap( const char **)myicon );
toolb = new QToolButton( p, "Save",
                         "Save this document",
                         this, SLOT(save()) ),
              mytools, 0 );
toolb->setIconSet( QIconSet( myicon ) );
connect( this, SIGNAL(pixmapSizeChanged( bool )),
         toolb(0), SLOT(setUsesBigPixmap( bool )) );
```
```

**QImage** QImages are platform-independent image representations that provide direct access to the per pixel image data.

# *A Possible Instantiation*

```
```cpp
// Create a 640x480 monochrome image
QImage i( 640, 480, 1, 2 );
```
```

# *Example Use*

```
```cpp
QImage i, mirror;
if( i.load( "Pix.bmp", "BMP" ) == true) {
    mirror = i.mirror( true, false );
} else {
    mirror = i;
}
```
```

**QMovie** QMovie incrementally loads animated images and provides methods to deal with their display on a widget that provides a paint device. Typically, you will implement a movie on a QLabel, but a QPushButton will work just as well.