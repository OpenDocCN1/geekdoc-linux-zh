This is useful for applications wanting to transfer a lot of data. But for testing and development, I find a simple ASCII-based protocol easier to work with, because a simple serial terminal allows me to send and receive messages in human-readable text. The Minerva feature, MINX (Minerva INput transfer), uses the delimiters `<` and `|>` to surround control messages, allowing an Arduino to pass messages back to the PC so that further processing can take place, without affecting any other debugging or trace messages. I’ll cover this fully in Chapter 7.

> **Note**  Some models of Arduino, such as the Mega, have three additional serial ports addressable as Serial1, Serial2, and Serial3.

On the PC side of this transmit-receive equation, you have a much simpler job because everything in Linux is treated like a file. You can therefore issue this:

```
```text
tail -f /dev/ttyUSB0
```
```

To see all the data that is sent back from the Arduino and introduce commands to the board, use this:

```
```text
echo -n send data > /dev/ttyUSB0
```
```

It is from this that demonstrates the benefit of an ASCII-based protocol. In the simplest case, you can issue this:

```
```text
Serial.print("1");
```
```

from the Arduino to switch the PC control program into an on state, with an equivalent for off. This makes the C program very simple:

```
```c
// USB script trigger
#include <stdio.h>

char *szUSBDevice = "/dev/ttyUSB0";
int main() {
char v;

FILE *fp = fopen(szUSBDevice, "r");
if (!fp) {
    printf("Failed to open USB...");
    return 1;
}

while(1) {
  if (fread(&v, 1, 1, fp)) {
    if (v == '1') {
      // button pressed
    } else if (v == '0') {
      // button released
    } else {
      printf("%c", v);
```
```