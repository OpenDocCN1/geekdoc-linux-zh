# TEXT SUPPORT

The following classes provide the data and methods needed to support text display.

**QFont, QFontInfo, and QFontMetrics** QFont provides the encapsulation for platform-dependent text fonts. QFontInfo provides general information about a specified font. QFontMetrics provides metrics information about a font.

# *Example Use*

```
```
QFont f( "Helvetica", 10 );
setFont( f );
int fw = fontMetrics().width( "Hello" );
int fh =
    QLabel *l = new QLabel( "Hello", this );
l->setFixedWidth( fw );
```
```

**QSimpleRichText** QSimpleRichText encapsulates the Qt simplified implementation of rich text. You will use this primarily to add rich-text drawing support to custom widgets.

# *A Possible Instantiation*

```
```
QSimpleRichText rt( "<b>Boldly</b> going", font() );
```
```

# *Example Use*

```
```
QLabel *l = new QLabel( this );
QSimpleRichText rt( "<b>Boldly</b> going", font() );
QPainter p;
p.begin( l );
rt.draw( &p, 0, 0,
         QRegion( QRect( 0, 0, rt.widthUsed() ),
                  rt.height() ) );
palette());
p.end();

// It's much easier to simply:
l->setRichText( "<b>Boldly</b> going" );
```
```

As the above example implies, a limited subset of Qt widgets provide support for the Qt rich-text implementation. This will undoubtedly change over time. In the meantime, you can implement Qt rich text on any paint device using QSimpleRichText.