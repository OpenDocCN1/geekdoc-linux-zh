
## INPUT AND OUTPUT CLASSES

Every interactive application performs I/O. The input could be from a keyboard, a mouse, a file or a network socket. The output could be to a display widget, a file, or yet another network socket. Qt provides a number of useful classes to help perform these normally platform-dependent operations in a platform-independent manner.

### QAccel

This class provides handling for accelerator and shortcut keystrokes. Note that QAccel handles key events for the top-level widget that contains the QAccel parent widget, and for all children of that top-level widget.

- *A Possible Instantiation*

```cpp
QAccel *a = new QAccel( this );
```

- *Example Use*

```cpp
QAccel* a = new QAccel( this );
a->connectItem( a->insertItem( ALT+Key_M ),
                this, SLOTS( toggleMenuBar() ) );
a->connectItem( a->insertItem( ALT+Key_T ),
                this, SLOTS( toggleToolBar() ) );
a->connectItem( a->insertItem( ALT+Key_B ),
                this, SLOTS( toggleStatusBar() ) );
```

### QAsyncIO

QAsyncIO provides an abstract mechanism for performing lengthy or slow I/O operations without blocking the user interface. See QDataPump below.

### QBuffer

This class provides buffered QByteArray I/O functionality. You can use QBuffer’s internal QByteArray or provide your own.

- *A Possible Instantiation*

```cpp
QBuffer b();
```

- *Example Use*

```cpp
// A roundabout variable initializer
int a, b;
QByteArray s;
QBuffer b( &s );
QTextStream ts( &b );
ts << "456 123" << '\0';
QTextIStream tis( &s ) >> b >> a;
```

Note that this class is not appropriate for creating streams of Unicode text. QTextStream provides a QString implementation for that purpose.

### QDataStream

QDataStream provides some basic methods for serializing binary data to a QIODevice. A data stream is independent of platform-dependent byte ordering.

- *A Possible Instantiation*

```cpp
QFile f( "some_data.dat" );
f.open( IO_ReadOnly );
QDataStream s( f );
```

- *Example Use*

```cpp
float myfloat;

// Open a file for writing
QFile f( "data.dat" );
f.open( IO_WriteOnly );
// Associate the file's QIODevice with a stream
QDataStream s( f );
// Write data into the stream
s << 0x0102030405;
s << (double)3.1416;
myfloat = 0.01120113;
s << myfloat;
// Close the file
f.close();
```

Note that QDataStream allows you to specify the byte ordering of the output (the default is MSB first, or big-endian) but changing the default will break the portability.

### QDataPump

A QDataPump moves data from a QDataSource to a QDataSink during normal event processing (interleaved) by examining the QDataSource::readyToSend() and QDataSink::readyToReceive() methods of its arguments, and responding to the asyncIO::activate() signals of the QDataSource and QDataSink. QDataPump is used by the Qt toolkit to asynchronously “feed” animated image data to QMovie objects.

### QDataSink

QDataSink is an asynchronous consumer of data. It is normally used with a QDataPump and a QDataSource to move asynchronous data from point A to point B. See QDataPump above and QDataSource below.

### QDataSource

QDataSource is an asynchronous producer of data and will typically be used with a QDataPump and a QDataSink to read asynchronous data from an ASIC port or a network socket. See QDataPump above.

### QDir

QDir encapsulates the concept of a filesystem directory (on Windows systems, these are frequently called “folders”) in a platform-independent manner.

- *A Possible Instantiation*

```cpp
QDir d( "/etc/ppp" );
```

- *Example Use*

```cpp
QDir d( "/etc/ppp" );
QFile f( d.filePath( "options" ) );
if( f.open( IO_ReadWrite ) == true ){
// Modify PPP options
}else{
QMessageBox::warning( 0, "Whoops!",
"Can't open /etc/ppp/options..." );
}
```

### QFile

QFile encapsulates file I/O functionality in a platform-independent manner. Windows programmers should learn to use a forward-slash (/) as a directory delimiter. This will ease porting to other platforms.

- *A Possible Instantiation*

```cpp
QFile f( "/Windows/system.ini" );
```

- *Example Use*

```cpp
QFile f( "/Windows/win.ini" );
f.open( IO_ReadWrite );
if(f.size() > 0) {
     QString s;
     f.readLine( s, 256 );
     // Do stuff
 } else {
    // Do other stuff
 }
 f.close();
```

### QFileInfo

QFileInfo provides file information in a platform-independent manner.

- *A Possible Instantiation*

```cpp
QFile f( "/vmlinux" );
QFileInfo fi( f );
```

- *Example Use*

```cpp
QFile of( "/usr/src/linux/arch/i386/vmlinux" );
QFileInfo ofi( of );
QFile f( "/vmlinux" );
QFileInfo fi( f );
if( fi.lastModified() < ofi.lastModified() ) {
      // vmlinux is older or the same...
}
```

### QIODevice

This is the base class for all Qt I/O devices and provides much of the common functionality required by platform I/O devices. QBuffer and QFile are subclasses of QIODevice.

### QIODeviceSource

This class is a subclass of QDataSource, whose data is provided by any QIODevice or QIODevice subclass (such as a QFile). It provides an asynchronous source of data with a QIODevice as the source.

### QTextIStream

This subclass of QTextStream is a convenience class that provides a text input stream.

- *A Possible Instantiation*

```cpp
...
QCString s = "1234567";
int n;
QTextIStream( &s ) >> n;
...
```

### QTextOStream

This subclass of QTextStream is a convenience class that provides a text output stream.

### QTextStream

QTextStream provides typical C++ I/Ostream functionality that is required for reading or writing text (ASCII or Unicode) from or to a QIODevice.

### QSocketNotifier

QSocketNotifier provides the mechanisms needed for event-driven socket communications. Since the Linux/X11 implementation of this class uses a single select() system call for all QSocketNotifiers, it may be possible to use the class to monitor objects other than network sockets—a named pipe, for example.

- *A Possible Instantiation*

```cpp
...
QSocketNotifier *gen = new QSocketNotifier( sock,
                                            QSocketNotifier::Read );
...
```

- *Example Use*

```cpp
...
Socket.h

#ifndef SOCKET_H
#define SOCKET_H
#include <stdio.h>
#include <stdlib.h>

#ifndef WIN32
#include <unistd.h>
#include <stdarg.h>
#endif

#include <qapplication.h>
#include <qsocknotifier.h>
#include <sys/types.h>
#ifndef WIN32
#include <sys/socket.h>
#include <netinet/in.h>
#include <sys/ioctl.h>
#include <fcntl.h>
#include <netdb.h>
#include <sys/param.h>
#else
#include <winsock.h>
#endif
#include <errno.h>

// For Linux, we define a common type
#ifndef WIN32
#define INVALID_SOCKET -1
typedef int SOCKET;
#endif

class Socket : public QObject
{
    Q_OBJECT
public:
    //Create on existing descriptor
    Socket( SOCKET _sock );

    // Create and connect
    Socket( const char *_host, unsigned short _port );

    // Destroy - closing if still open
    ~Socket();

    // Retrieve the descriptor
    SOCKET socket() const { return sock; }

    // Enable read - If true, emit readEvent on socket input
    void enableRead( bool );

    // Enable write - If true, emit writeEvent on socket input
    void enableWrite( bool );

    // Retrieve the address
    unsigned long getAddr();

    // Formatted print()
    void print( const char *fmt, ... );

    // Retrieve one 'line' of data up to 'len' bytes or
    // EOF or newline
    char *line(char *p, int len);

signals:
// Data is available for reading (if enableRead( true ) called)
void readEvent( Socket * );

// Socket is ready for writing (if enableWrite( true ) called)
void writeEvent( Socket * );

// Raised when connection is broken
void closeEvent( Socket * );

public slots:
// Connected to the Notifiers
void slotWrite( int );
void slotRead( int );

protected:
bool connect( const char *_host, unsigned short _port );
bool init_sockaddr( const char *hostname, unsigned short port );

struct sockaddr_in name;
SOCKET sock;
in_addr addr;

QSocketNotifier *readNotifier, *writeNotifier;
};

class ServerSocket : public QObject
{
Q_OBJECT
public:
ServerSocket( int _port );
~ServerSocket();

// Retrieve the descriptor
SOCKET socket() const { return sock; }

// Retrieve the port being monitored
unsigned short getPort();

// Retrieve the current address
unsigned long getAddr();

public slots:
// Called when someone connects to our port
virtual void slotAccept( int );
}
```
