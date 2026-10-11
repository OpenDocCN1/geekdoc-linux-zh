

# Python 专栏

## 树莓派加Arduino

本期，我们将探讨如何让树莓派与你的Arduino进行通信并使用它。

![](img/628186dda7facdc011bf39c938de3975_65_0.png)

乔伊·伯纳德是一位真正的通才，他的时间分配于制作家具、帮助研究人员解决科学计算问题以及编写Android应用程序之间。

![](img/628186dda7facdc011bf39c938de3975_65_1.png)

它是树莓派的官方语言。在 python.org/doc 阅读文档。

树莓派是一款真正令人惊叹的单板计算机，被广泛用于许多DIY项目中。这也是本专栏及之前几篇文章的基础。虽然树莓派拥有GPIO，可以与传感器和执行器通信，但在某些情况下，你可能希望将树莓派用作项目的“大脑”，并将与物理世界的交互任务卸载到另一个系统。这通常由市面上可用的众多微控制器板之一来处理。在本期中，我们将具体使用Arduino板，并查看如何将其连接到树莓派，以及如何处理两者之间的通信。一如既往地，我们将使用Python作为首选语言来处理此处示例中的所有实际编码。

Arduino是一个开源的原型平台，定义为一项规范。这意味着你可以从几个不同的制造商那里获得Arduino实现，但它们的行为应该都类似。对于本文，假设你要使用的任何实现都能正常工作。第一步是将两块板连接在一起。由于树莓派无法通过其USB端口提供大量电力，你可能需要使用带电源的USB集线器来连接它们。虽然它们通过USB连接，但Arduino对树莓派会显示为一个串行端口。这意味着你可以直接通过串行连接与Arduino通信。为了确保安装所有相关的库，你可以简单地使用以下命令安装Arduino IDE：

```bash
sudo apt-get install arduino
```

这将确保你拥有可能需要的所有核心软件。当你插入Arduino时，你需要知道通信将在哪个端口上进行。具体的端口名称将根据你使用的树莓派和Arduino的确切版本而异。然而，它应该类似于 `/dev/ttyUSB0` 或 `/dev/ttyACM0`。在下方的示例代码中，我们将假设Arduino在端口 `/dev/ttyUSB0` 上可见。

### 第一步是打开到Arduino的串行连接

两个设备已连接，你可以开始编写代码让它们互相通信。我们将从最低层的协议开始，并由此向上构建。第一步是打开到Arduino的串行连接。为了做到这一点，你需要确保安装了Python serial模块。如果你使用的是Raspbian，你可以这样做：

```bash
sudo apt-get install python-serial
```

然后，你需要创建一个连接到给定串行端口的新的Serial对象，以及你需要使用的速度。

```python
import serial
ser = serial.Serial('/dev/ttyUSB0', 9600)
```

在上面的例子中，速度是9600波特率（位/秒）。使用这个Serial对象，你可以读写Arduino的数据。但你需要在Arduino上编写代码来处理其部分的通信。Arduino有自己的基于C的编程语言，你使用它来编写将在板上运行的代码。Arduino的工作方式是，在启动时加载一个程序，只要通电，该程序就会一直运行。作为一个简单的例子，以下代码将监听一个输入引脚，看它是否变高。如果是，它将在串行端口上发送一条消息。

```cpp
int pirPin = 7;
void setup() {
  pinMode(pirPin, INPUT);
  Serial.begin(9600);
}
void loop() {
  if (digitalRead(pirPin) == HIGH) {
    Serial.println("High");
  }
  delay(500);
}
```

要将此程序加载到Arduino板中，你需要使用在本文开头安装的Arduino IDE。这是一个图形化程序，如果你想用它来执行这一步，你需要将树莓派连接到显示器。否则，你可以使用常规桌面计算机来编程你的Arduino。如果你使用的是大多数Arduino上的标准引导加载程序，它将在启动时运行最后上传的任何程序。这样，你可以使用桌面计算机上传代码，然后再将其连接到树莓派。回到树莓派，你如何从Arduino读取这条消息？你可以简单地从之前创建的Serial对象进行读取。

```python
import time
while True:
  message = ser.readline()
  print(message)
  if (message[0] == 'H'):
    do_something_useful()
  time.sleep(5)
```

如你所见，我们导入了time模块，以便能够在尝试从串行端口读取之间的循环中休眠。

那如何向Arduino发送指令呢？这也是可能的。Arduino代码需要预先上传。例如，以下代码将获取一个输入数字，并使LED闪烁该次数：

```cpp
int ledPin = 13;
void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
}
void loop() {
  if (Serial.available()) {
    flash(Serial.read() - '0');
  }
  delay(1000);
}
void flash(int n) {
  for (int i = 0; i < n; i++) {
    digitalWrite(ledPin, HIGH);
    delay(100);
    digitalWrite(ledPin, LOW);
    delay(100);
  }
}
```

然后，你可以使用类似于以下的Python代码发送一个计数：

```python
ser.write('5')
```

这将使连接到你Arduino引脚13的LED闪烁五次。

树莓派上缺少的一个元素是模数转换器（ADC），用于将给定的电压转换为可在某些控制软件中使用的数字。这就是连接Arduino极其有帮助的地方，因为它内置了10位ADC转换器。以下代码将读取引脚3上的电压，然后通过串行连接将其发送到树莓派。

```cpp
int analogPin = 3;
int val = 0;
void setup() {
  Serial.begin(9600);
}
void loop() {
  val = analogRead(analogPin);
  Serial.println(val);
}
```

这将测量的电压映射为0到1,023之间的整数。最小电压为零，而最大电压可以通过函数analogReference()设置。默认情况下，最大电压是提供给板子的电源（5V板为5伏特，3.3V板为3.3伏特）。你还可以使用两个内部提供的参考电压，一个是1.1伏特，另一个是2.56伏特。在特殊情况下，你可以向AREF引脚提供外部参考电压。你需要确保它仅在0伏特和5伏特之间。

反过来说，你可以使用Arduino提供输出电压。这是通过使用PWM（脉冲宽度调制）输出信号来实现的。这里的想法实际上是发送一定数量的脉冲，其占空比在部分时间内为高，在剩余时间内为低。例如，如果你有一个LED连接在其中一个引脚上，你可以用以下代码以半亮度点亮它。

```cpp
int ledPin = 9;
void setup() {
  pinMode(ledPin, OUTPUT);
}
void loop() {
  analogWrite(ledPin, 127);
}
```

analogWrite()函数的第二个参数是一个介于0和255之间的值，它定义了占空比（从0%即完全关断到100%即完全开启）。此模拟输出信号在给定占空比下保持开启，直到对analogWrite()函数的新调用。通过让树莓派通过串行连接输出数值，它可以发送一个简单的整数来控制输出占空比。

希望这篇短文能激发一些关于如何开始结合多个计算平台以扩展你自己项目能力的想法。当你可以选择那些实际上最能完成各自任务的子模块，并从这些简单部件构建出所需的复杂行为时，没有理由去尝试为你的项目寻找唯一的一揽子解决方案平台。

### PyFirmata 可以提供更多帮助

虽然你可以编写自己的代码在Arduino上运行，但有几个项目可以上传到其中，使交互变得更轻松。其中之一是Firmata项目，它包含一个Python模块，帮助你与Arduino通信。第一步将是下载Firmata Arduino代码并将其上传到你的Arduino，使用桌面计算机完成这一点最容易。代码可在 github.com/firmata/arduino 获取。有几个不同的版本可用，但对于这些示例，你应该使用Arduino IDE上传StandardFirmata草图。许多不同的编程语言都有可用的客户端库，包括几个Python库。我们将查看使用的那个是pyFirmata。你可以从你的树莓派上安装它：

```bash
sudo pip install pyfirmata
```

现在你可以使用Firmata作为Arduino的一种远程控制器，你的Python代码可以几乎直接访问所有可用的功能。要开始，导入pyFirmata模块并创建一个连接到相关串行端口的新的Arduino对象：

```python
import pyfirmata
board = pyfirmata.Arduino('/dev/ttyUSB0')
```

现在你可以直接访问数字I/O引脚。例如，以下代码会将1写入引脚10。

```python
board.digital[10].write(1)
```

当你想从引脚读取时，你有可能溢出输入缓冲区。为了解决这个问题，你可以在进行任何读取之前创建并启动一个迭代器对象，使用如下代码。

```python
it = pyfirmata.util.Iterator(board)
it.start()
```

现在你可以为输入或输出获取选定的引脚。以下代码将获取用于数字输入的引脚4和用于模拟PWM输出的引脚12。

```python
pin4 = board.get_pin('d:4:i')
pin12 = board.get_pin('a:12:p')
```

然后你可以使用相关方法对这些新的引脚对象进行读写：

```python
val = pin4.read()
pin12.write(100)
```

完成后，别忘了将任何输出引脚重置回0伏特，然后你可以使用以下命令关闭连接：

```python
board.exit()
```

