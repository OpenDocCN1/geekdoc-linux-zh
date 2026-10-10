
```
.../chp08/spi/ADXL345_cpp $ g++ SPITest.cpp SPIDevice.cpp -o SPITest
.../chp08/spi/ADXL345_cpp $ ./SPITest
The device ID is: 229
SPI Mode: 3
Bits per word: 8
Max speed: 50000000
Dumping Registers for Debug Purposes:
e5 00 00 00 00 00 00 00 00 00 00 00 00 4a
82 30 00 00 00 00 ff 07 00 00 b7 00 00 00
00 00 00 00 00 00 00 00 00 00 0a 08 00 00
02 0b 00 00 00 00 ff e9 00 00 00 00 00 00 00
```

相同的 `SPIDevice` 类也可以作为修改列表 8-3 中 `ADXL345` 的基础，以支持 SPI 总线而非 I2C 总线。列表 8-7 提供了该类的一个片段，该片段位于 `/chp08/spi/ADXL345_cpp/` 目录下。

### 列表 8-7: `/chp08/spi/ADXL345_cpp/ADXL345.h` (片段)

```cpp
class ADXL345{
public:
    enum RANGE { };
    enum RESOLUTION { };
private:
```

`SPIDevice` *device;

unsigned char *registers;

...

public:

    `ADXL345`(`SPIDevice` *busDevice);

    virtual int readSensorState();

    ...

    virtual void displayPitchAndRoll(int iterations = 600);

    virtual ~`ADXL345`();

```

可以使用 8-7 中的完整类来构建如列表 8-8 所示的示例。该示例有助于演示如何用高层面向对象（OOP）类封装连接到总线之一的嵌入式设备。

# 列表 8-8: `/ch08/spi/ADXL345_cpp/testADXL345.cpp`

```cpp

#include <iostream>

#include <sstream>

#include "SPIDevice.h"

#include "ADXL345.h"

using namespace std;

int main() {

    cout << "Starting RPI ADXL345 Test" << endl;

    SPIDevice *spiDevice = new SPIDevice(0,0);

    spiDevice->setSpeed(500000);

    spiDevice->setMode(SPIDevice::MODE3);

    ADXL345 acc(spiDevice);

    acc.displayPitchAndRoll(100);

    cout << "End of RPI ADXL345 Test" << endl;

}

```

执行此程序时，它会在终端窗口显示当前的加速度计俯仰和横角：
`pi@rpi:~/exploring/chp08/spi/ADXL345_cpp $ ./testADXL45`
Starting RPI ADXL345 Test
Pitch:2.7509 Roll:79.124

# 三线 SPI

`ADXL345` 支持三线 SPI（半双工）模式。在这种模式下，数据在同一线上进行读取和写入。要在 `ADXL345` 上启用此功能，必须将 `0x40` 写入 `0x31`（`DATA_FORMAT`）寄存器，并在 `ADXL345` 的 `SD0` 和 `Vcc` 之间放置一个 10kΩ 电阻。在 `ch08/spi/ADXL345_cpp` 目录下，目前的 Linux 发行版不支持该模式。

# wiringPi

第 6 章安装的 `wiringPi` 库有一组与 SPI 交互的基本 C 函数。此短代码显示了 `ADXL345` 的完整寄存器集：

```c

$ pi@rpi:~/exploring/chp08/spi/wiringPi $ writeADXL345.c

#include <wiringPi.h>

#include <stdio.h>

#include <string.h>

int main(){

    unsigned char data[0x41]; // 用于存储读数据的缓冲区

    int i; // 需要读取最后一个值

    memset(data, 0x00, 0x41); // 清空缓冲区

    data[0]=0xC0; //连续读取数据

    wiringPiSetup(0, 1000000, 3); // SPI 通道、速率、模式

    wiringPiDataRW(0, data); // 写入所有 40 个寄存器

    // 为 ADXL345 将数据移位（例如 data[1] 移动到 data[0]）

    memmove(data, data+1, 0x40);

    printf("The ID is %d\n", data[0]); // 显示寄存器

    printf("The full set of 40 registers are:\n");

    for(i=0; i<0x40; i++){ // 显示所有 40 个寄存器

        printf("%02X ", data[i]); // 以十六进制显示值

        if(i%16==15) printf("\n"); // 每行后换行

    }

    return 0;

}

```

```
$ ../chp08/spi/wiringPi $ gcc ADXL345 -o ADXL345 -lwiringPi

$ ../chp08/spi/wiringPi $ ./ADXL345
```

设备 ID 229

完整的 40 个寄存器为：

E5 00 00 00 00 00 00 00 00 00 00 00 00 4A
82 30 00 00 00 00 3B 00 00 00 7 000 00 00
00 00 00 00 00 00 00 00 00 00 0A 08 00 00
02 08 00 00 00 00 ED 00 00 00 00 00 00

此示例中需要进行内存移位，因为 `wiringPiDataRW` 函数在单个通道内执行 SPI 写入和读取。示例代码中来自 `ADXL345` 的响应存储在请求之后的数组索引中。例如，如果读取设备 ID（`0x80`）的请求存储在 `data[0]` 中，那么 `ADXL345` 对该请求的响应（即 `0xE5`）存储在 `data[1]` 中。`memmove()` 将所有返回值移动一个地址（例如将 `data[1]` 移动到 `data[0]`）。该库的更多信息请访问 tiny.cc/rpi806。

# 树莓派上的多个 SPI 从设备

在本章中，总线上连接了一个 SPI 设备，这是一个非常有限的总线！SPI 总线可以与多个从设备共享，前提是通信发生时只有一个从设备处于激活状态。树莓派内核支持 SPI 总线上的两个选择引脚：`SPI_CE0_N`（引脚 24）和 `SPI_CE1_N`（引脚 26）。这就是 `/dev` 目录下存在两个 SPI 设备的原因。

```
pi@raspberrypi $ ls -l /dev/spi*
crw-rw-rw-- 1 root 0 Jan 1 1970 spidev.0
crw-rw-rw-- 1 root 0 Jan 1 1970 spidev.1
```
