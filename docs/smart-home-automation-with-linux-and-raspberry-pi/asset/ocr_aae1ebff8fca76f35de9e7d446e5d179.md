```
```cpp
char *pChimesPhrase3 = "L3204edL64c";
char *pChimesPhrase4 = "L3204edL6403g";
char *pChimesPhrase5 = "L3203g04deL64c";

// a quarter past
ampPlayString(CHANNEL_OUTPUT_PIEZO_SPEAKER, pChimesPhrase1);

// half past
ampPlayString(CHANNEL_OUTPUT_PIEZO_SPEAKER, pChimesPhrase2);
ampPlayString(CHANNEL_OUTPUT_PIEZO_SPEAKER, pChimesPhrase3);

// a quarter to
ampPlayString(CHANNEL_OUTPUT_PIEZO_SPEAKER, pChimesPhrase4);
ampPlayString(CHANNEL_OUTPUT_PIEZO_SPEAKER, pChimesPhrase5);
ampPlayString(CHANNEL_OUTPUT_PIEZO_SPEAKER, pChimesPhrase1);

// top of the hour
ampPlayString(CHANNEL_OUTPUT_PIEZO_SPEAKER, pChimesPhrase2);
ampPlayString(CHANNEL_OUTPUT_PIEZO_SPEAKER, pChimesPhrase3);
ampPlayString(CHANNEL_OUTPUT_PIEZO_SPEAKER, pChimesPhrase4);
ampPlayString(CHANNEL_OUTPUT_PIEZO_SPEAKER, pChimesPhrase5);
```
```

Using the various shields provides more complex audio output, including sample playback.

# Communication with a PC

The basic Arduino allows bidirectional communication with a PC through its built-in USB port. This uses the same serial port that’s used to upload the program in the first place. It must be set up first before data can be sent or received, both of which are supported with this method:

```
```cpp
Serial.begin(9600);
```
```

The Arduino can read data from the PC only on a byte-by-byte basis, so you will need to read it within a loop using code like this:

```
```cpp
int incomingData = Serial.read();
```
```

Note, however, that this function is blocking. That is, it will not return from the read function until there is data on the serial port. If your device responds only to messages, then this will work fine. However, it is more usual to place this at the start of your loop, surrounded with this:

```
```cpp
if (Serial.available() > 0) { /* ... */ }
```
```

Writing data from the Arduino back to the PC, however, is easier since the size of the data is already known. This can be handled by the Serial.print or Serial.println function for quick and easy string messages. Or individual bytes can be written using Serial.write:

```
```cpp
Serial.write(byteData);
```
```