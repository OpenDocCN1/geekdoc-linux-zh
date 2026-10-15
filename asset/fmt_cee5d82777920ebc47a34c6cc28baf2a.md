
## 非线性传感器

红外距离传感器用于机器人导航（例如，避障）和开关。这些传感器在室内环境中工作良好，在一定距离内具有 39ms 的响应，因此在 25 秒内可以提供足够的数据。图 11(a) 显示了这些非线性传感器（tiny.cc/erpi005）。

![](img/8d97725dcf071daded8acede3920e981_450_0.png)

图 11-10：非线性传感器

## 使用 GNUPLOT 进行数据拟合

除了绘制数据外，`gnuplot` 还可以用于使用非线性最小二乘 `NLS` Marquardt-Levenberg 算法将数据拟合到曲线。例如，可以使用以下步骤将 10-12(b) 中的数据拟合为 1/x 的函数：

```
pi@ /exploringrpi/ch10/sharp $ more data

9925 10

2790 15

npi@ /exploringrpi/ch10/sharp $ gnuplot

G N U L O T

Version 4.6 patchlevel 6

gnuplot f(x) = a + b/x

gnuplot fit(x) "data" using 1:2 via a,b

...
```

最终参数集 渐近标准误差

| | | | |
|---|---|---|---|
| a | = 1.19894 | +/- 1.415 | (118%) |
| b | = 42466.4 | +/- 1335 | (3.144%) |

因此，最佳拟合函数为：`f(x) = 119894+(42466.4/x)`，其中 `x` 是采集到的 ADC 输入值。使用校准数据得到的拟合函数值可见 10-12(b)。

你也可以通过继续之前的步骤，使用 `gnuplot` 拟合呈指数衰减形式的函数。为 `c` 和 `d` 值提供初始估计有助于 NLS 算法收敛到有效解。为此，你使用通过 Wolfram Alpha 输出确的值或近似值：

```
gnuplot g(x) = c * exp(-x * d)

gnuplot c = 115

gnuplot d = 0.00088

gnuplot fit g(x) "data" using 1:2 via c,d
```

最终参数集 渐近标准误差

| | | | |
|---|---|---|---|
| c | = 115 | +/- 7.632 | (6.637%) |
| d | = 0.000836017 | +/- 7.2244e-05 | (8.664%) |

最佳拟合函数为：`g(x) = 115e^-0.000836107`，其中 `x` 是采集到的 ADC 输入值。在这种情况下，标准误差值较低，且图 10-12(b) 表指数衰减函数提供了更好的拟合效果，特别是在近距离。

### 第 10 章 ■ 与物理环境交互 427

注意，此过程用于许多类型的模拟传感器，提供一个可用于在测量值之间进行插值的表达式。哪种拟合曲线最适合数据取决于传感器的底层物理过程。例如，你可以使用线性拟合来为第 9 章描述的 LDR 导出一个表达式。可以编写 C++ 代码来读取 ADC 值并转换为距离，如列表 10-5 所示，指数表达式被编码在单行中。

列表 10-5: `/chp10/sharp/sharp.cpp` (片段)

```cpp
int main() {
    cout << "Starting the RPI2PD12 sensor example" << endl;
    SPIDevice *busDevice = new SPIDevice(0,0);
    busDevice->setSpeed(500000);
    busDevice->setMode(SPIDevice::MODE0);
    for (int i=0; i<1000; i++) {
        unsigned char send[3], receive[3]; // Reading single-ended input from channel 0
        send[0] = 0xB0000000;
        busDevice->transfer(send, receive, 3);
        int raw = ((receive[1] & 0x00001111) << 8) | receive[2];
        float distance = 115.804f * exp(-0.000843107f) * (float)raw;
        cout << "The distance is: " << distance << " cm" << '\r' << flush;
        leep(100000);
    }
    busDevice->close();
    return 0;
}
```

当代码执行时，它将继续以厘米为单位输出检测对象的距离，持续约 100 秒：

```
pi@erpi ~ /exploringpi/chp10/sharp ./build
pi@erpi ~ /exploringpi/chp10/sharp $ sharp
Starting the RPI2PD12 sensor example
The is: 16.117 cm
```

列表 10-6 是使用三种不同曲线拟合近似进行距离计算的代码段。

列表 10-6: `/chp10/sharp/sharpft.cpp` (片段)

```cpp
cout << "Raw value is " << (int)raw << endl;
float distance = 115.804f * exp(-0.000843107f) * (float)raw);
cout << "Estimate 1 (Wolfram): " << distance << endl; // Note: original had extra paren here
distance = 119894+(42466.4/x);
cout << "Estimate 2 (Linear): " << distance << endl;
distance = 115.804f * exp(-0.000836107f) * (float)raw;
cout << "Estimate 3 (Exponential): " << distance << endl;
```
