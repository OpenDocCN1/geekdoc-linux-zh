
# 安装 C 库

为了应用更改，重启树莓派。

C [7] 库对 GPIO 使用 BCM 法，这意味着 SPI 引脚在软件中是数字 10（引脚 19）。该库可以在线免费下载。要安装库，然后与 LED 通信，它创建一个名为 `matrix` 的对象。表 1 显示了各个参数的含义。对象将前三个像素设置为红色、绿色和蓝色，`matrix.render()` 命令将数据写入 LED。

## 列表 1：WS28Test.java

```java
// WS28Test.java
import com.github.mbelling.ws281x.*;

public class WS28Test{
    public static void main(String[] args){
        Ws281xLedStrip matrix = new WS281xLedStrip(
            64, 10, 80000, 10, 4, 0, false, LedStripType.WS2811_STRIP_GRB, false);
        matrix.setPixel(0, 255, 0, 0);
        matrix.setPixel(1, 0, 255, 0);
        matrix.render();
    }
}
```

```java
matrix.setPixel(2, 0, 0, 255);
```

```bash
$ javac -cp /home/pi/rpi-ws281x-java/
```

```java
matrix.render();
```

`build/libs/rpi-ws281x-java-2.0.0-SNAPSHOT.jar` `WS28Test.java`

```java
// main
```

```java
// class
```

如果你不想在命令中包含类路径，你可以选择：

```bash
$ cd ~
```

`rpi-ws281x-java.git`

```bash
$ git clone https://github.com/Ujgarff/rpi-ws281x.git
```

```bash
$ cd rpi-ws281x-java/src/scripts
```

或者与 `CLASSPATH` 变量配合工作：

```bash
$ bash createNativeLib.sh
```

我使用了参数 `-cp`，以便更清晰地查看各个库。

```bash
$ cd rpi-ws281x
```

```bash
$ cd ~rpi-ws281x-java/
```

```bash
$ scons
```

```bash
$ ./gradle assemble -x signArchives
```

```bash
$ ./test -g 10
```

运行封装器的命令还需要 Log4J 库，你可以通过以下方式下载并安装：

最后一条命令启动了一个测试程序，该程序使 LED 矩阵以不同的颜色亮起。

```bash
$ java -cp /home/pi/rpi-ws281x-java/build/libs/rpi-ws281x-java-2.0.0-SNAPSHOT.jar:/home/pi/U/apache-log4j-2.13.1-bin/log4j-api-2.13.1.jar:/home/pi/U/logging/log4j/2.13.1/apache-log4j-2.13.1-bin/log4j-core-2.13.1.jar WS28Test
```

```bash
$ cd ~
```

```bash
$ wget http://archive.apache.org/dist/logging/log4j/2.13.1/apache-log4j-2.13.1-bin.tar.gz
```

## Java 封装器 (Wrapper)

各种编程语言都有 C 库的封装器，包括 Java 封装器。封装器是一种通过接口为其他编程语言提供一种语言功能的软件。

`-cp` 参数还传递了所有需要的库。注意，在执行期间库必须在类路径中。

要安装 Java 封装器，请使用命令：

完成所有安装步骤后，使用一个初始的小程序（列表 1）测试 WS2812 灯带，该程序使矩阵中的所有 LED 闪烁蓝色。你可以任意更改输出内容（例如输出吃豆人或滚动字体）。

## 蛇游效果 (Meander)

LED 在矩阵上呈波浪形排列（图 3），这使得起初编写程序变得有些困难。为了方便起，我使用了多维数组缓冲区来创建动画（第 6 行）。在缓冲区内部，可以通过引用 `x` 和 `y` 坐标来控制单个 LED。

在缓冲区中完成所有更改后（列表 2，第 39 行和 42 行），程序通过 `writeBufferToMatrix()` 命令（第 7 到 25 行）将数据传输到 LED 矩阵，因此你不需要关心 LED 的物理布局。

### 表 1：Ws281xLedStrip() 参数

| 参数编号 | 类型 | 含义 |
| :--- | :--- | :--- |
| 1 | `int` | 连接的 LED 数量 |
| 2 | `int` | 使用的 GPIO 连接 (10 用于 SPI，18 用于 PWM) |
| 3 | `int` | 控制 LED 的频率 |
| 4 | `int` | 使用的直接内存访问 (10 通常是一个不错的个人选择) |
| 5 | `int` | 亮度，0 到 255 (建议 4 到 32) |
| 6 | `int` | PWM 通道 |
| 7 | `int` | 信号反相 (如果使用反相电平转换器) |
| 8 | `LedStripType` | 见表 2 |
| 9 | `boolean` | 为 `true` 时程序结束时关闭 LED |

### 表 2：LedStripType

| `LedStripType` | 可能类型 |
| :--- | :--- |
| `LedStripType.SK6812_STRIP_<Type>` | `RGB`, `RBGW`, `GRBW`, `GBRW`, `BRGW`, `BGR` |
| `LedStripType.WS2811_STRIP_<Type>` | `RGB`, `RBG`, `GRB`, `GBR`, `BRG`, `BGR` |

## 结论

WS2812 LED 是一件小技术杰作。如果你结合许多元素创建一个矩阵，你就可以实现伟的项目。例如，你可以用这些模块显示彩色的滚动字体，甚至是小型动画。在篇文章中，我使用了 8x8 矩阵，但矩阵模块也有更大的尺寸，并且可以连接在一起。

![img/d478ca893bf12a417e8f507b165_0.png]

### 列表 2：Matrix.java
