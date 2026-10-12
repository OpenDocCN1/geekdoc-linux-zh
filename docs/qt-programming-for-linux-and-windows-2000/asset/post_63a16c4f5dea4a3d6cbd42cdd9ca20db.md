
# QChar

QChar encapsulates Unicode characters and provides test, classification, and conversion methods much like those provided for ASCII characters by ctype.h.

# QClipboard

QClipboard provides methods to access the underlying window system’s clipboard.

# QConstString

This class provides the functionality of the QString class, optimized for existing Unicode data. By eliminating copy operations (the primary overhead of the QString class) the QConstString class can provide a significant performance increase. If any modification is attempted on the data, however, the class will make a copy of the data so that it will persist unmodified.

# QString

This class is an abstraction of typical zero-terminated strings. QString inherits QArray, so its contents are explicitly shared. Also see QString.

# QDoubleValidator

QDoubleValidator provides range checking for double precision floating point numbers. See QValidator and QIntValidator.

# QRegExp

QRegExp provides pattern matching using regular expressions in a manner similar to the GNU regex implementation. Support is provided for Unicode support and case-insensitive matching except for non-ASCII Latin-1 characters.

# QString

QString is an abstraction of Unicode text and character strings. QString implicitly shares text strings.

# QTextCodec

This abstract class provides conversions between text encodings and encapsulates the common elements of Qt text encodings.

# QTextDecoder

QTextDecoder provides a single method, toUnicode(), that is used to convert an array of bytes into Unicode text. The class maintains prior state information for continued processing in subsequent calls, making QTextDecoder useful in data streams. See QTextEncoder.

QTextEncoder converts from Unicode to another format (you have to provide the target format of course), maintaining prior state information for processing in subsequent calls. This makes the class suitable for use with data streams. See QTextDecoder.

# QtTranslator

QtTranslator provides internationalization support for text output. A QtTranslator object contains a set of translations from the reference language to a target language, and provides methods to add, find, or remove such translations. Methods are also provided to save the current object to a file or load a previously saved file.

# QtValidator

QtValidator is a base class for validating input text. See QIntValidator and QDoubleValidator.

# DATE AND TIME

While all the supported platforms provide the time_t standard value as a representation of time plus all the associated library functions, Qt provides its own encapsulation of date and time that is not quite as limited as the platform representations are.

# QtDate

QtDate is an abstraction of date values. The implementation is a platform-independent calculation of Gregorian dates, valid from September 14, 1752, to the eighth millennium. I expect the resolution to change significantly in future releases of Qt as 64-bit CPU architectures become more prevalent. The native time_t value on these systems is valid to BSN (Beyond Solar Nova).

# QtDateTime

QtDateTime combines the functionality of the QtDate and QtTime classes. The class also adds some convenience routines to permit interfacing to the native time_t values supplied by the platforms that Qt is available for.

# QtTime

The QtTime class is an abstraction of time in hours, minutes, seconds, and milliseconds since midnight. QtTime provides methods for comparison and conversion.

# MISCELLANEOUS

Most of the following classes belong in no specific category, but are extremely useful, nonetheless.

# QRangeControl

This class provides the means to bound integer values within a specific range. This is much more intuitive than letting the user input an integer with a text field and in some circumstances, is even more intuitive than a spin box (it depends on the context).

## Likely Instantiation

```cpp
QRangeControl *rc = new QRangeControl( 0, 100, 1, 10, 0 );
```

## Common Use

```cpp
QRangeControl *rc = new QRangeControl( 0, 100, 1, 10, 0 );
int n = rc->pageStep();
```

There are five concepts covered by the class which make its use in QScrollBar widgets rather apparent:

- A current value as a bounded integer which is retrieved via the QRangeControl::value() method and set using the QRangeControl::setValue() method.
- The minimum value.
- The maximum value.
- A line-step value that can be used to determine the preferred number of lines to scroll.
- A page-step value that can be used to determine the appropriate number of lines to scroll for a page-forward or page-backward scroll.

# QGuardedPtr

This template class provides guarded pointers to QObjects. A guarded pointer behaves like any other C++ pointer except that its value is set to NULL when the object it references is deleted. I have not been able to measure any significant performance hit as a result of using guarded pointers, and they can improve product reliability. Using guarded pointers does increase coding time and complexity, of course.

# QMimeSource

QMimeSource encapsulates an abstract piece of data. It is used by the drag and drop classes and by QClipboard.

# QMimeSourceFactory

QMimeSourceFactory provides an interface to a collection of abstract data.

# QPoint

QPoint is an abstraction of a point within a plane.

# QPointArray

QPointArray maintains an explicitly shared array of QPoint objects.

# QRect

QRect provides an abstraction of a rectangular area of a plane.

# QSignal

QSignal provides a very simple way to send a signal with no parameters to a slot that accepts no parameters. This is typically used by classes that don’t inherit QObject to send signals.

# QSignalMapper

QSignalMapper provides mechanisms to map signals that don’t provide a parameter to signals that provide either an integer or QString parameter. This is very useful for managing multiple popup menu items from a single slot. You can also use this class to map an array of pushbuttons to a single slot.

# QSize

QSize defines the size (in pixels) of two dimensional objects and provides methods and operators for comparison and value modifications.

# QTimer

QTimer provides periodic and single-shot timing signals.

## Likely Instantiation

```cpp
QTimer *t = new QTimer( this, false );
```

## Common Use

```cpp
// We need a flashing text label, so we subclass QLabel and
// add a QTimer. We tried to tell the customer it uses a lot
// of resources…
class Blinky : public QLabel
{
   Q_OBJECT
public:
   Blinky( QWidget *p=0, const char *n=0 );
   Blinky( const QString &s, QWidget *p=0, const char *n=0 );

public slots:
   void setValue( const QString &s );

protected slots:
   void myTimeout();

private:
   QLabel *l;
   QString str;
   bool showing;
};

// Convenience ctor sets the label text and saves a copy
Blinky::Blinky( const QString &s, QWidget *p, const char *n )
{
   QLabel( s, p, n )
   str = s;
}

// Standard constructor adds the timer
Blinky::Blinky( QWidget *p, const char *n )
{
   Blinky( ":", p, n );
   showing = true;
   tnr = new QTimer( this );
   connect( tnr, SIGNAL(timeout( ) ), SLOT(myTimeout()) );
   t -> start( 500 );
}

// A slot to set the text value
void
Blinky::setValue( const QString &s )
{
   setText( s );
   str = s;
}
```

```cpp
// This is called by our QTimer every 500ms
void
Blinky::myTimeout()
{
// Toggle text every 500ms...
if (showing == true) {
showing = false;
setText( "" );
} else {
showing = true;
setText( str );
}
}
...
```

# QVariant

QVariant behaves like a union of many commonly used Qt data types.

# QMatrix

QMatrix performs 2D transformations of a coordinate system. The result can be applied to a graphic image to translate, scale, shear, or rotate the image. See QPainter in the previous chapter.

# SUMMARY

While Qt doesn't provide a class for every conceivable programming need outside the purely visual interface component arena, it certainly covers a wide range of common tasks, from the obvious timesavers to the dauntingly complex linked-list handlers. I expect great things in future releases.
