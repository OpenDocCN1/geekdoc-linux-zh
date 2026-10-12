```
signals:
// A connection has been accepted
// don't forget to delete the Socket when no longer needed
void accepted( Socket * );

protected:
bool init( unsigned short );

QSocketNotifier *notifier;
SOCKET sock;
};

#endif

Socket.cpp
#include <Socks.h>

#ifdef WIN32
static bool isinitied = false;
// Here's where we initialize Winsock (goofy, huh?)
static void
initWinSock()
{
    if(isinitied == true) return;
    WORD wVersionRequested;
    WSADATA wsaData;
    int r;

    wVersionRequested = MAKEWORD( 1, 1 );

    r = WSAStartup( wVersionRequested, &wsaData );
    if ( r == 0 ) {
        isinitied = true;
    }
}
#endif

// Socket ctor with existing platformf socket
Socket::Socket( SOCKET _sock )
{
#ifdef WIN32
    initWinSock();
#endif
    sock = _sock;
    readNotifier = 0L;
    writeNotifier = 0L;
}

// Socket ctor from host/port info
Socket::Socket( const char *_host, unsigned short int _port )
{
#ifdef WIN32
    initWinSock();
```