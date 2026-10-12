# Example Use

```
```
QFile f( "anim.png" );
f.open( IO_ WriteOnly );
QPNGImagePacker p( f, 8, 0 );
QImage img = myLabel->pixmap().convertToImage();
p.packImage( img );
```
```

Given Unisys Corporation’s attitude regarding the use of LZW compression, I recommend using the PNG image format for animations to avoid the licensing that is required in some countries.

# **QPrinter**  QPrinter is a paint device for use on printers. On Microsoft Windows systems, QPrinter uses the existing printer drivers and the native spooler. On Linux systems, QPrinter generates PostScript output and sends it to a spooler of your choosing.

# A Possible Instantiation

```
```
QPrinter *p = new QPrinter();
```
```

The online documentation provides a detailed example.

# **QRegion**  QRegions define the clipping area of a QPainter.

# A Possible Instantiation

```
```
QRegion r( QRect(10, 10, 50, 50), QRegion::Ellipse );
```
```

# Example Use

```
```
QLabel *l = new QLabel( this );
QPixmap pic = QPixmap( "my_square_pic.bmp" );
QRegion rf QRect( 0, 0, pic.width(), pic.height()),
QRegion::Ellipse );
QPainter p;
p.begin( l );
p.setClipRegion( r );
p.drawPixmap( 0, 0, pic );
p.end();
```
```