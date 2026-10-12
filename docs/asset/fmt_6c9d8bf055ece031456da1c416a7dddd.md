
```cpp
}
mciSendCommand(device, MCI_SEEK, MCI_SEEK_TO_START, NULL);
state = Stopped;
}
}

// void pause()
void
LilMidi::pause()
{
    if (isopen == true && state == Playing) {
        MCI_PLAY_PARMS parms;
        if (mciSendCommand(device, MCI_PAUSE, 0, (DWORD)(LPVOID)&parms))
            return;
        state = Paused;
    }
}

// unsigned long pos()
// Returns current stream position
unsigned long
LilMidi::pos()
{
    if (isopen == true) {
        MCI_STATUS_PARMS parms;
        parms.dwItem = MCI_STATUS_POSITION;
        if (mciSendCommand(
```

```cpp
MCI_STATUS,
MCI_WAIT | MCI_STATUS_ITEM,
(DWORD)(LPVOID)&parms)) {
    return(OL);
}
return(parms.dwReturn);
return(OL);
```

// int status()
// update and return current state
// LilMidi:::(Stopped, Playing, or Paused)
int
LilMidi::status()
{
    if (isopen == true) {
        MCI_STATUS_PARMS parms;
        parms.dwItem = MCI_STATUS_MODE;
        if (mciSendCommand(
            device,
            MCI_STATUS,
            MCI_WAIT | MCI_STATUS_ITEM,
            (DWORD)(LPVOID)&parms)) {
            return(Stopped);
        }
        switch (parms.dwReturn) {
            case MCI_MODE_PLAY:
                state = Playing;
                break;
            case MCI_MODE_PAUSE:
                state = Paused;
                break;
            default:
                state = Stopped;
                break;
        }
    } else {
        state = Stopped;
    }
    return(state);
}

// bool seek(unsigned long milliseconds)
// seek to the stream position
bool
LilMidi::seek(unsigned long msec)
{
    if (isopen == true) {
        MCI_SEEK_PARMS params;
        params.dwTo = msec;
        switch (status()) {
            case Playing:
                if (mciSendCommand(device, MCI_PAUSE, 0, NULL))
                    return(false);
                if (mciSendCommand(device, MCI_SEEK, MCI_TO | MCI_WAIT, (DWORD)(LPVOID)&params)) {
                    return(false);
                }
                state = Paused;
                play();
                break;
            default:
                if (mciSendCommand(device, MCI_SEEK, MCI_TO | MCI_WAIT, (DWORD)(LPVOID)&params)) {
                    return(false);
                }
                break;
        }
        return(true);
    }
    return(false);
}

// void fastPwd(int seconds)
// advance the stream position
void
LilMidi::fastPwd(int sec)
{
    if (isopen == true) {
        unsigned long p = pos();
        p += (unsigned long)(sec * 1000);
        seek(p);
    }
}

// void rewind(int seconds)
// rewind the stream
void
LilMidi::rewind(int sec)
{
    if (isopen == true) {
        unsigned long p = pos();
        if (p < (unsigned long)(sec * 1000))
            p = 0;
        else
            p -= (unsigned long)(sec * 1000);
        seek(p);
    }
}

// int divisionType()
// Returns 0 on error or MCI_SEQ_DIV_???? value
int
LilMidi::divisionType()
{
    if (isopen == true) {
        MCI_STATUS_PARMS parms;
        parms.dwItem = MCI_SEQ_STATUS_DIVTYPE;
        if (mciSendCommand(device, MCI_STATUS, MCI_WAIT | MCI_STATUS_ITEM, (DWORD)(LPVOID)&parms)) {
            return(0);
        }
        return((int)parms.dwReturn);
    }
    return(0);
}

// int tempo()
// -1 on error, else tempo value
int
LilMidi::tempo()
{
    if (isopen == true) {
        MCI_STATUS_PARMS parms;
        parms.dwItem = MCI_SEQ_STATUS_TEMPO;
        if (mciSendCommand(device, MCI_STATUS, MCI_WAIT | MCI_STATUS_ITEM, (DWORD)(LPVOID)&parms)) {
            return(-1);
        }
```
