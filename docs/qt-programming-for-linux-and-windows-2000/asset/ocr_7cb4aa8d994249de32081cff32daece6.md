```
params.dwTo = msec;
switch( status() ) {
case Playing:
    if( MCI_SendCommand( device,
                          MCI_PAUSE, 0, NULL ) )
        return( false );
    if( MCI_SendCommand( device,
                          MCI_SEEK,
                          MCI_TO | MCI_WAIT,
                          (DWORD)(LPVOID)&params) ) {
        return( false );
    }
    state = Paused;
    play();
    break;
default:
    if( MCI_SendCommand( device,
                          MCI_SEEK,
                          MCI_TO | MCI_WAIT,
                          (DWORD)(LPVOID)&params) ) {
        return( false );
    }
    break;
}
return( true );
}

// void fastPwd( int seconds )
// advance the stream position
void
LilMidi::fastPwd( int sec )
{
    if( isopen == true ) {
        unsigned long p = pos();
        p += (unsigned long) ( sec * 1000 );
        seek( p );
    }
}

// void rewind( int seconds )
// rewind the stream
void
LilMidi::rewind( int sec )
{
    if( isopen == true ) {
        unsigned long p = pos();
        if( p < (unsigned long) ( sec * 1000 ) )
            p = 0;
        else
            p -= (unsigned long) ( sec * 1000 );
        seek( p );
```