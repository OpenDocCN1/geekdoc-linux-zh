```
```cpp
)
)

// int divisionType()
// Returns 0 on error or MCI_SEQ_DIV_???? value
int
LilMidi::divisionType()
{
    if( isopen == true ) {
        MCI_STATUS_PARMS parms;
        parms.dwItem = MCI_SEQ_STATUS_DIVTYPE;
        if( mciSendCommand( device,
            MCI_STATUS,
            MCI_WAIT | MCI_STATUS_ITEM,
            (DWORD)(LPVOID)&parms ) ) {
            return( 0 );
        }
        return( (int)parms.dwReturn );
    }
    return( 0 );
}

// int tempo()
// -1 on error, else tempo value
int
LilMidi::tempo()
{
    if( isopen == true ) {
        MCI_STATUS_PARMS parms;
        parms.dwItem = MCI_SEQ_STATUS_TEMPO;
        if( mciSendCommand( device,
            MCI_STATUS,
            MCI_WAIT | MCI_STATUS_ITEM,
            (DWORD)(LPVOID)&parms ) ) {
            return( -1 );
        }
        return( (int)parms.dwReturn );
    }
    return( -1 );
}

// void setTempo( int tempo )
void
LilMidi::setTempo( int tempo )
{
    if( isopen == true ) {
        MCI_SEQ_SET_PARMS parms;
        parms.dwTempo = tempo;
        mciSendCommand( device,
            MCI_SET,
            MCI_WAIT | MCI_SEQ_SET_TEMPO,
            (DWORD)(LPVOID)&parms );
    }
```
}
```