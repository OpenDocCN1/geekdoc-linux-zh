Build it, then power on and run the software on the Arduino, so that it is able to register itself on the I2C bus:

```
```cpp
#include "Wire.h"

int i2cAddress = 0x03;

void setup() {
  Wire.begin(i2cAddress);
}
```
```

The rest of the software is as simple as the hardware! First check that the Arduino can be found on the bus. So, on the Raspberry Pi, simply run:

```
```text
$ sudo modprobe i2c-dev
$ sudo i2cdetect -y 0
     0 1 2 3 4 5 6 7 8 9 a b c d e f
00:          -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- 03 -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
70: -- -- -- -- -- -- -- -- --
```
```

From this, you can see that your Arduino is successfully connected to the bus, and on address 03. If you don’t see the Arduino, then it’s likely you’re using a revision two board, and therefore need to use bus 1, and not bus 0, so change the i2cdetect command above, and SMBus reference below.

Sending data from the Raspberry Pi uses the smbus library and code such as:

```
```python
#! /usr/bin/python
import smbus
bus = smbus.SMBus(0)

address = 0x03
dataToSend = 42

bus.write_byte_data(address, 0xC9, dataToSend)
```
```

Notice that we send two bytes, even though only one is needed. This first byte (0xC9) is like a header that indicates the type of data we’re sending. The Arduino can then watch for data on the I2C bus, at address 3, and respond accordingly. We therefore amend our program above to read:

```
```cpp
#include "Wire.h"

int i2cAddress = 0x03;

void setup() {
  Wire.begin(i2cAddress);
  Wire.onReceive(receiveEvent);
}
```
```