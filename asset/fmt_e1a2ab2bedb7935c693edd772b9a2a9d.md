
要设置输出电平，只需以十六进制格式向设备发送数字值即可。它是一个 12 位 DAC，因此在 0V 到 3.3V-out 之间有 4096 个步阶，十六进制格式为 `0x0000` 到 `0FFF`。例如，要输出 1 V 的电压电平，你可以设置十进制值 `(1 × 4096) / 3.3V = 1241`——十六进制为 `0x04D9`；2V 为 `0x09B0`，3V 为 `0x0EB0`。你必须将最高位（MSB）优先将这些字节写入设备。例如，要将直流输出电压设置为 1V、2V、3V 和 3.3V，请使用以下步骤：

```
pi@erpi $ i2cset -y 1 0x62 04D 0xD8
pi@erpi $ i2cset -y 1 0x62 009 0xB0
pi@erpi $ i2cset -y 1 0x62 00E 0xB8
pi@erpi $ i2cset -y 1 0x62 0FF 0xFF
```

可以使用第 8 章中的 `I2Device` 类来构建 `DACDriver` 类，如列表 9-5 所示。类封装了设置输出电平的功能，并将直流输出阻抗设置为 1Ω (`DISABLE`)、1kΩ、100kΩ 或 500k。

Listing 9-5: `/exploringhipi/cp09/i2cdAC/DACDriver.h`

```cpp
class DACDriver:I2Device{
    // 电源模式
    enum PD_MODE { DISABLE, GND_1K, GND_100K, GND_500K };
    private:
        unsigned int I2CBus, I2CAddress;
        unsigned int lastValue;
        int setOutput(unsigned int value, DACDriver::PD_MODE mode);
    public:
        DACDriver(unsigned int I2CBus=1, unsigned I2CAddress=0x62);
        virtual int powerDown(DACDriver::PD_MODE mode = GND_500K);
        virtual int wake();
        virtual int setOutput(unsigned int value);
        virtual int setOutput(float percentage);
        virtual int setOutput(unsigned int waveform[], int size, int loops=1);
        virtual unsigned int getLastValue() { return lastValue; }
        virtual ~DACDriver();
};
```

你可以从 DAC 输出端提供或消耗的最大电流取决于输出电压，但范围在 12 mA 到 16 mA 之间（参见数据手册中的图 2-16）。你还必须考虑到树莓派 3.3V 电源对电流的总需求。

图 9-6 右侧提供了一个可选的外部电路，描述了增加 DIP 封装的 `MCP6002` 运放的方法。该 IC 中的其中一个运放被用于电压跟随器配置（如第 4 章所述），这意味着运放的输出电压 (`IOut`) 镜像 DAC 设置的输入电压 (`In+`)。目前，输出由 `MCP6002` 提供，而不是由 DAC。在室温下，`MCP6002` 在 5 V 电源下可以提供或消耗最大 25.5 mA 电（参见 `MCP6002` 数据手册中的图 2-13）。可选的运放设备可以扩展这一范围。

Listing 9-6 提供了一个短代码示例，可用于在输出端输出 50% 的电压电平（在本例中为 1.65 V）。程序在按下键之前会关闭输出。即使在程序终止或树莓派重启，DAC 也会保持其输出电平。

Listing 9-6: `/ch09/i2cdAC/dacTest.cpp` (segment)

```cpp
int main() {
    DACDriver *driver = new DACDriver(1, 0x62);
    driver->setOutput(50.0); // (即 2048)
    cout << "The output is " << driver->getLastValue() << endl;
    cout << "Press Enter to sleep the DAC..." << endl;
    getch();
    driver->powerDown(DACDriver::GND_100K); // 留空则 500K
    cout << "Press Enter to wake the DAC..." << endl;
    getch();
    driver->wake();
    cout << "DAC is on and maintains value on exit" << endl;
    return 0;
}
```

Listing 9-6 的构建和执行方式如下：

```
pi-er ./exploringrpi/ch09/i2cdAC ./build

pi-er ./exploringrpi/ch09/i2cdAC ./dactest
```

输出是 2048

Press Enter to sleep the DAC...

Press Enter to wake the DAC...

DAC is on and maintains value on exit

同一目录 (`dacTest.cpp`) 中提供了另一个示例，演示了如何使用 I2C DAC 输出约 30 Hz 的正弦波，正弦波周期由 100 个离散样本组成。输出受到 I2C 总线速度的限制；提供了针对 SPI DAC 的类似示例，它可以实现更高的频率。

# SPI 数字模拟转换器

`MCP4921` 是一种廉价（$2）单通道 12 位 SPI DAC，采用 DIP 封装（参见 `tiny.cc/erpi906`）。它是 Microchip SPI DAC 系列的一部分，还包含 8 位 (`MCP4901`) 和 10 位 (`MCP4911`) 变体。该 DAC 系列支持 2.7 V 到 5.5 V 电源以及轨到轨输出。

# 第 9 章增强 RPi 的输入/输出接口

![](img/8d97725dcf071daded8acede3920e981_408_0.png)

图 9-8：(a) SPI DAC 输出；(b) 使用 BCM2835 C 库的 DAC 输出

在 `chp09/spIDAC/bcm2835/` 目录下提供了另一个代码示例，该示例利用 BCM2835 库向 SPI DAC 发送样本。此代码的输出显示在图 9-8(b) 中，你可以看到正波频率为 1.75 kHz，这意味着 DAC 正在使用 RPi 特有的内存映射方法处理每秒 175,000 次 SPS。

# 在 RPi 上添加 PWM 输出

脉宽调制（PWM）的概念在第 4 章中介绍，其在 RPi 上的用法在第 6 章中进行了详细描述。PWM 输出可以通过调整控制信号的占空比来控制 LED 的亮度或控制舵服电机（如第 6 章所述）。遗憾的是，RPi 上板载硬件 PWM 输出的数量有限，这可能会限制你的开发项目。然而，你可以使用外部 PWM 控制器为 RPi 添加 PWM 输出。

现有许多类型的 PWM 控制器，例如流行的 `TLC5940`，但此类设备通常需要外部振荡器和定时器，增加了 RPi 实现的复杂性。`PCA9685` 不需要任何外部电路，因为它有一个 25 MHz 的内部振荡器，因此被选为讨论的重点。它是一个 16 通道 12 位 PWM 控制器，接口到 IC 总线。它可以输出 24 Hz 到 1,526 Hz 之间的信号频率，16 个输出中的每一个都可以调整为具有独立的占空比（0%–100%）。它采用表面贴装 TSSOP28 封装，28 个引脚之间的间距为 0.65 mm。对于原型制作，你必须从 Adafruit 等供应商处购买成品模块（约 15 美元），或者购买一个 0.65 mm 转 0.1 英字的适配板。本文讨论使用了 Adafruit 模块，因为它设计良好，可以轻松地与 RPi 接口，如图 9-9 所示。

# 382 第二部分 — 接口、控制与通信

> 警告：不要混淆 Adafruit `PCA9685` 模块上的 `Vcc` 和 `V` 输入，否则你可能会损坏 RPi。`Vcc` 是 3.3 V 逻辑电平电源，而 `V+` 是电机电压电源（例如， 5 V）。

![](img/8d97725dcf071daded8acede3920e981_409_0.png)

图 9-9：Adafruit `PCA9685` 16 通道 12 位 PWM 驱动器
