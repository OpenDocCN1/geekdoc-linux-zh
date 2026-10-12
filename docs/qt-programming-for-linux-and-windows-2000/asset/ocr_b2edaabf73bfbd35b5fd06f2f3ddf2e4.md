```
```
sparms.dwReturn = 0;
}
parmс.dwCallback = NULL;
parmс.dwFrom = sparmс.dwReturn;
if( mciSendCommand(
     device,
     MCI_PLAY,
     MCI_FROM,
     (DWORD)(LPVOID)&parmс) ) {
     return;
}
state = Playing;
}
```

```
// void stop()
// Stop and reposistion stream to 0
void
LilMidi::stop()
{
    if( isopen == true ) {
        if(state == Playing ) {
            mciSendCommand( device, MCI_STOP,
            NULL, NULL );
        }
        mciSendCommand( device, MCI_SEEK,
            MCI_SEEK_TO_START, NULL );
        state = Stopped;
    }
}
```

```
// void pause()
void
LilMidi::pause()
{
    if( isopen == true && state == Playing ){
        MCI_PLAY_PARMS parms;
        if( mciSendCommand( device, MCI_PAUSE, 0,
        (DWORD)(LPVOID)&parmс) )
            return;
        state = Paused;
    }
}
```

```
// unsigned long pos()
// Returns current stream position
unsigned long
LilMidi::pos()
{
    if( isopen == true ) {
        MCI_STATUS_PARMS parms;
        parms.dwItem = MCI_STATUS_POSITION;
        if( mciSendCommand(
```
```