
#include <iostream>

#include <unistd.h>

#include <wiringPi.h>

using namespace std;

#define APHASE 15 // GPIO22 的物理引脚

#define AENABLE 33 // GPIO27 的物理引脚

#define BPHASE 7 // GPIO4 的物理引脚

#define BENABLE 12 // GPIO28 的物理引脚

int main() {

    wiringPiSetup();

    pinMode(APHASE, OUTPUT);

    pinMode(AENABLE, OUTPUT);

    pinMode(BPHASE, OUTPUT);

    pinMode(BENABLE, OUTPUT);

    // 电机 A 正向 50% 运行 5s

    digitalWrite(APHASE, HIGH);

    digitalWrite(AENABLE, HIGH);

    pwmWrite(AENABLE, 128);

    sleep(5);

    // 电机 A 反向全速运行 5s

    digitalWrite(APHASE, LOW);

    pwmWrite(AENABLE, 255);

    sleep(5);

    // 电机 B 正向 75% 运行 5s

    digitalWrite(BPHASE, HIGH);

    digitalWrite(BENABLE, HIGH);

    pwmWrite(BENABLE, 192);

    sleep(5);

    // 电机 B 反向 25% 运行 5s

    digitalWrite(BPHASE, LOW);

    pwmWrite(BENABLE, 64);

    sleep(5);

    // 停止

    digitalWrite(AENABLE, LOW);

    digitalWrite(BENABLE, LOW);

    return 0;

}
```

列表 10-1 中的代码可以这样编译并执行：
`pi@erpi:exploring/chp10/drv8835` `g++ motor.cpp -o motor -wiringPi`
`pi@erpi:exploring/chp10/drv8835` `./motor`

电机 A：正向 50% 运行 5 秒
电机 A：反向 100% 运行 5 秒
电机 B：正向 75% 运行 5 秒
电机 B：反向 25% 运行 5 秒
程序结束

## 驱动大型直流电机（大于 1.5 A）

Pololu Simple Motor Controller ($30–$55）如图 10-5(a) 所示，它可以驱动电流高达 23 A、电压最高 34 V 的刷直流电机。它支持 USB、TTL 串口、模拟和爱好遥控 (RC) PWM 接口。该控制器使用 3.3 V 逻辑电平，但也兼容 5 V。

尽管名称为“Simple”（简单），但这是一种高级控制器，可以配置如最大加速/减速、可调启动速度、电子制动、过热阈值等设置，这使其成为大型机器人应用的良好选择。可以使用 Windows GUI 应用程序配置控制器（如图 10-5(b) 所示），或者使用 Linux 命令行界面。Windows 配置工具还可以通过 USB 监控电机温度和电压状况并控制速度、制动、PWM、通信设置，即使电机正通过 TTL 串口连接到 RPi。

![](img/missing_image_5.png)

图 10-5：Pololu Simple Motor Controller 以及 (b) 相关的电机配置工具

3.3 V TTL 串口接口可能是嵌入式应用的最佳选择，因为它可以直接与 UART 设备配合。可以使用廉的 USB UART 设备进行通信，如第 8 章所述。

# 第10章 与物理环境交互 413

```bash
pi@erpi $ lsusb
Bus 001 Device 004: ID 1a86:7523 QinHeng El. HL-340 USB-Serial adapter
pi@erpi $ ls -l /dev/ttyUSB0
crw-rw---- 1 root dial 188, 0 Jan 1 1970 /dev/ttyUSB0
```

**注意** 在尝试进行串口通信之前，请为简单电机控制器（Simple Motor Controller）供电。电源必须足够驱动控制板，红色 LED 将闪烁表示错误状态。此外，在将其连接到树莓派（RPi）之前，请使用 Windows 电脑配置控制器，并选择 115,200 的固定波特率，而不是选择自动协商。

简单电机控制器可以在串口 ASCII 模式下配置，可以使用 `minicom` 通过树莓派的 UART 设备进行控制。例如，在 Input Settings 标签页（图 10-5b）中启用 ASCII 模式并将波特率为115,200 (8N1)，树莓派可以直接连接到电机控制器，并使用基于文本的命令控制电机，如 `v`（版本）、`F`（前进）、`B`（刹车）、`R`（反转）、`GO`（退出安全启动模式）、`x`（停止）。完整命令列表请参见手册（tiny.cc/erpi1003）：

```bash
pi@erpi $ sudo minicom -b 115200 -o -D /dev/ttyUSB0
V
!161 01.04
GO
F 50%
B
T
?
GO
R 25%
```

简单电机控制器还可以使用第8章描述的 C/C++ UART 通信代码直接控制。可以使用配置工具将串口 TTL 线设置为 115,200。假设电机控制器已连接到 `/dev/ttyUSB0`（如上所示），可以使用 `/chap10/simple/` 目录下的 `motor.c` 代码示例来控制电机控制器：

```bash
pi@erpi ~/exploringrpi/chap10/simple $ gcc motor.c -o motor
pi@erpi ~/exploringrpi/chap10/simple $ sudo ./motor
Starting the motor controller example
Error status: 0x000
Current Target Speed is 0.
Setting Target Speed is 3200.
```
