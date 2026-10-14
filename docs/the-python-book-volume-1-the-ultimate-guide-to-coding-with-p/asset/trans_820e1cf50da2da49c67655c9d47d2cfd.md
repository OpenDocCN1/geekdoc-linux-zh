

![](img/3b256f430f51c98f1315671f6e4eec19_164_0.png)

以上是我们在本文中使用的 LED 矩阵的完整原理图（你也可以在 FileSilo 上以全尺寸查看它）

## 完整代码列表

## 11 能量控制

如果电流流过 LED，LED 就会点亮。SetData 将 74HC244 的引脚拉低，以确保来自 74HC238 的能量可以通过二极管流动。

## 12 避免 GPIO 问题

树莓派基金会有定期更改扩展头布局的倾向，而专业的过程计算机制造商则厌恶这种习惯。建议通过一组定义来处理引脚与功能之间的映射。我们的代码针对带“短”头的 Rev2 树莓派进行了优化——40 引脚版本将需要重新调整，以确保物理引脚号与逻辑 GPIO 号相对应。

## 13 添加示例数据

通过将数据存储区设置为你选择的数值来测试代码。将所有字段设置为 64 将禁用显示每个部分的每一行。

## 14 启动

检查平面板与单板计算机之间的所有连接，然后开始启动编译后的应用程序。不要忘记使用 sudo 命令——直接内存访问仅限于 root，以防止应用程序在物理内存中造成混乱。用户已习惯于此，因此要求他们在命令前加上 sudo 并不会引起担忧。

## 15 注意闪烁

眼尖的读者会注意到偶尔出现闪烁，其中一条线看起来比其他线更亮。这是由程序停滞引起的——如果内核执行其他工作，切换例程就无法运行。我们可以通过使用实时 Linux 内核来解决这个问题。

```
{
    _where->writePinLow(PIN7);
}
```

## Step 06

```
int main(void)
{
    mmapGpio rpiGpio;
    //Set outputs
    rpiGpio.setPinDir(PINA0, mmapGpio::OUTPUT);
    rpiGpio.setPinDir(PINA1, mmapGpio::OUTPUT);
    rpiGpio.setPinDir(PINA2, mmapGpio::OUTPUT);
    rpiGpio.setPinDir(PINA3, mmapGpio::OUTPUT);
    //TURN OFF ASAP!
    rpiGpio.setPinDir(PINCS0, mmapGpio::OUTPUT);
    rpiGpio.writePinHigh(PINCS0);
    //... etc
```

```
unsigned char dataStore[2][16];
```

## Step 13

```
for(int j=0;j<2;j++)
{
    for(int k=0;k<16;k++)
    {
        dataStore[j][k]=64;
    }
}
```

## Step 09

```
int blockCounter=0;
int rowCounter=0;
while(1)
{
    blockCounter++;
    if(blockCounter==16)
    {
        if(rowCounter==0)
        {
            blockCounter=0;
            rowCounter+=1;
        }
        else
        {
            blockCounter=0;
            rowCounter=0;
        }
    }
```

## Step 18

```
safelySetRow(rowCounter, &rpiGpio);
setAddress(blockCounter, &rpiGpio);
setData(dataStore[rowCounter][blockCounter], &rpiGpio);
usleep(50);
}
return 0;
}
```

## Raspberry Pi 车载电脑

制作自己的触摸屏导航系统，提供路线指引、本地天气预报并播放音乐

汽车越来越聪明了。如今，新型汽车内置智能导航界面，你不需要去买一个 TomTom 来获取路线帮助。但如果你拥有一块树莓派，你甚至不需要买那个——更不用说买一辆新车了！

在这个项目中，我们将向你展示如何使用你的 Pi、一块优质触摸屏——我们在这里使用的是 SainSmart 的 9 英寸型号，以及一些其他部件，如 GPS 模块和 USB 3G 调制解调器，来打造自己的车载电脑。你的 CarPi 将能够使用开源导航软件 Navit 在屏幕上显示路线地图，外加语音合成来读出指引，它还能检查你的位置并为你提供天气预报。当然，它也能用作音乐播放器。

这是一个雄心勃勃的项目，但你将获得对定制界面、导航软件和地理位置数据、触摸屏校准、语音合成等方面的扎实理解。虽然你不必使用与我们相同的 SainSmart 屏幕，但我们确实推荐它用于本项目，因为它是 Pi 上为数不多的超大触摸屏之一。最后还有更多改进，因此请查看组件清单，确保你已拥有所有东西，然后开始吧！
