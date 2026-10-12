```
struct sockaddr_in name; int len = sizeof(name);  
getsockname(sock, (struct sockaddr *) &name, &len);  
return ntohs(name.sin_addr.s_addr);  
}

char *
Socket::line( char *p, int len )
{
    unsigned char c;
    int a;

#ifdef WIN32
    if(isinited == false) return( NULL );
#endif
    memset(p, 0, len);

    for(a=0;a<len;a++) {
        if(recv(sock, (char *)&c, 1, 0) <= 0) {
            if(a == 0) return(NULL);
            else return(p);
        }
        p[a] = c;
        if(c == '\n') return(p);
    }
    return(p);
}

Socket::~Socket()
{
    if ( readNotifier ) {
        delete readNotifier;
    }
    if ( writeNotifier ) {
        delete writeNotifier;
    }
#ifdef WIN32
    if(isinited == false) return;
#endif
    if(sock != INVALID_SOCKET) {
#ifdef WIN32
        ::closesocket( sock );
#else
        ::close( sock );
#endif
    }
    sock = INVALID_SOCKET;
}

ServerSocket::ServerSocket( int _port ) :
    sock( -1 )
{
```
```