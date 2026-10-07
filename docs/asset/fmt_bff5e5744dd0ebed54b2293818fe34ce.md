
我们将使用低功耗的 Arduino 并使用 Adafruit 库准备传感器。我们将发送包含测量结果的消息，创建一个基站来接收数据。最后，我们将利用 Atmega 的睡眠模式，仅在需要时唤醒板载，这样电池就不会一次耗尽。最终，我们将产生无需维护即可运行整个季节的温度计，获取关于家里最冷房间的丰富数据。通过这种方式你可以提前（希望如此）几个小时开启暖气。

对于本教程，你对 Arduino 的选择至关重要。电池容量以毫安时（`mAh`）测量。大多数电源宝提供 `5V`，容量约为 `220mAh`。Arduino Uno 在空闲模式下将约 `50mA`，这会在 `4` 小时内耗尽电池。这是由于板上有大量的硬件组件，即使它们没有被激活也需要电源。

为了减轻电池的负担，根据所需的少量组件自己制作一个 Arduino 是一个好主意。

上面的 Arduino Nano 带有温度传感器、发射器和纽扣电池这些“精简”板可以消除三分之二的功率浪费，并使微控制器以微安电流运行——可能持续多年。如果这超出了你的能力范围，我们建议使用较小的板，例如 Arduino Uno，它的硬件更少。然而，我们将 `img/b0e5bcf1ba8a75a2b9418fda820e5cd0_49_0`

## 准备传感器

`DHT22` 是一种廉价的温度湿度传感器。它有两种变体。为了与传感器接口交互，我们需要在代码顶部包含几行。确保 `DHT` 引脚连接到 Arduino。

```
#include "DHT.h"
#define DHTPIN 2
#define DHTTYPE DHT22
DHT dht(DHTPIN, DHTTYPE);
```

在 `setup()` 中，我们需要调用 `dht.begin()` 来初始化对象。然后我们只需要获取读取的方法在以下函数中：

```
float temperature = dht.readTemperature();
float humidity = dht.readHumidity();
```

传感器需要几秒时间获取测量值，并且在使用之前还需要两秒时间预热。这一点在我们开始关闭硬件以节省电力时将变得重要。现在你可以测量家里的温度了。如果你有一个温度计，可能想确认你的读数是否准确：如果没有，你可能需要添加校准常数来修正你的 Arduino。

## 添加无线发射器

我们有一个 Adafruit 传感器套装。为了让它有用，我们将考虑如何处理数据。有了 SD 卡适配器会有更简单的选择，但我们想通过定期发送数据来实时解释测量值。在教程中，我们将改为

## Adafruit 库让我们免于处理通信协议

使用无线发射器广播我们的数据以连接到另一个 Arduino，它将通过 USB 继这些数据。如果你使用的是树莓派，你可以连接接收器并跳过第二个 Adafruit 单元。

我们使用了 `FS-001` 和 `AM-001` - `434MHz` 接收器和发射器对，它可以连接到两个设备。例如，在焊接到发射器和接收器并以 `5V` 运行时，实现了 `50` 米的通信（无视距）。它们应该足够应对家内的短距离。如果你的墙太厚且范围出现问题，你可能需要切换到蓝牙或 Wi-Fi。

- 无需

你甚至不需要去尝试绘制两个设备之间的通信协议。有库可以安装，所以棘手的部分已经完成，你可以花时间制作更有用的设备。

# 教程

## Arduino

将发射单元连接到 Arduino。你应该能够通过 `DHT22` 的数字输出引脚为该单元供电。将数据引脚连接到数字引脚，以便输出。

为了与无线电建立接口，我们将使用 VirtualWire 库，该库可以在网上免费获取。VirtualWire 是一个外部封装库，负责处理无线模块的通信。你只需要设计数据并提供要发送的消息即可。（等一下，查看文本：“All you have to do is design data and provide a message to be sent.”）

要使用无线电发射器，你需要在初始化库之前设置高低电引脚，然后选择一个位比特率。你可能还需要对某些无线模块反转信号——最简单的方法是在运行过程中发现。

从 Arduino 记录数据的简单方法可能是使用 Python 脚本。在上一个教程中，我们是从树莓派发送消息。我们将执行相同的操作，但可以在等待消息到达时将其保存到后台。打开一个新的 Python 脚本。你需要导入 `'serial'` 库，以便我们从 Arduino 读取数据。在 Python 脚本中，你可以写：

```cpp
we_tx(pin);
we_set_inverted(true);
we_set_bitrate(480);
```

你需要格式化发送到接收器的消息。任务是从 `DHT22` 测量温度（浮点数）并将其转换为字符数组。这可以在 Arduino 上使用函数轻松完成：VirtualWire 随后将获取该字符数组并传输它。这只需要几行代码：

```cpp
char message[10];
dtostrf(dataFloat, 6, message);
we_send(message, len(message));
```

```python
data = open("data.txt", "a")
while True:
    line = arduino.readline().decode("utf-8")
    data.write(line)
```

只需使用 `open()` 命令打开一个新文件并创建一个带有当前时间的字符串，然后使用 `'datetime'` 从缓冲区读取字符并将其写入该文件，然后可以将其添加到你文本文件中每行的末尾。

接收来自 Arduino 的消息是一个相似的过程。在 `setup` 中，`tx`（发射器）连接到 `rx`（接收器），在 `loop` 中，发送 `get_message`。接收到的消息以无符号整数的形式存储在缓冲区中。在另一个 sketch 中，尝试通过无线电无限接收数据并将其上传到接收器。你可以以与发射器相同的方式连接接收器，并让 VirtualWire 知道哪个数字引脚用于数据。这个过程应该是非常直接的，你可以按字母读取消息缓冲区，将整数转换为字符，并打印到串口：

```cpp
if (get_message(buf, buflen) > 0) {
    for (int i = 0; i < buflen; i++) {
        char c = buf[i];
        Serial.print(c);
    }
}
```

`b0e5cf1ba8a75a2b9418fda20e5cd0_51`

## 记录数据

现在我们已经接收到了消息，将其中继到计算机，这样我们就可以每天存储和分析数据，而不是在几周或几个月后从 SD 卡中收集。在发射器和接收器对之上；一根线，以提高绘制温度数据随时间变化的散点图的能力。

## 读取数据手册

到此为止你已经制作了一些有用的东西。然而，我们将更进一步，让你的 Arduino 尽可能节能。益处是显而易见的：通过使用微控制器芯片的低功耗模式并关闭部分硬件，你不仅节省了一些电，还能让设备运行得更久。在正确的设置下，可以创建一个能够监控并报告温度的设备，无需解释

在继续之前，你应该熟悉你的芯片数据手册——了解 Arduino 如何被“唤醒”或“进入睡眠”以及它与板的接口是非常重要的。

以下内容适用于 Arduino 板上的 `Atmega328` 和 `328P`。开始，你需要包含三个头文件：

```cpp
#include <avr/sleep.h>
#include <avr/power.h>
#include <avr/wdt.h>
```

这允许将芯片退出许多睡眠模式，关闭硬件并与看门定时器接口，我们将使用它来启动 Arduino。

通过关闭硬件开始。你启动任何东西，因为没有模数转换器、串口接口，甚至是 USB 本身。如果在与传感器和无线电连接后，你通过以下方式关闭硬件：

```cpp
ADCSRA = 0;
power_disable();
```

## 设置闹钟并睡眠

为了让 Arduino 唤醒，你需要设置一些不会关闭的硬件。中断会中断几个时钟周期。首先我们需要写入看门定时器，然后为了设置等待 Arduino 的定时器长度（在此例为秒），我们随后重置定时器：

```cpp
WDTCSR = (WDIE | WDE);
WDTCSR = (WDIE | WTC3 | WDPO0);
wdt_reset();
```

我们切断了硬件并请求唤醒。创建一个带有当前时间的字符串很容易，从缓冲区读取字符并使用 `open()` 命令将其写入文件，直到消息到达。

`b0e5cf1ba8a75a2b9418fda20e5cd0_52`

这种方法是我们从“鸡蛋游戏”开始一直采用的方法。所有的服务——TextMap、ConsoleOutputViewer:ServerHead 等——都是基于接口的，而像 `StandardGameHolder` 这样的类依赖于这些接口，而不是实现这些类。接口提供了 `StandardGameHolder` 使用的方法，但它们具有不同的功能；例如，`ConsoleOutputViewer` 和 `ServerHead` 均实现了 `OutputInterface`，但我们在程序中实例化的任何 Spring 类都可以创建的的。

然而，这一切的代价很小，在 `main` 方法中，我们必须实例化程序中使用的每个服务类，并将对象传递给其他依赖。我们的项目足够简单，但对于更复杂的项目，跟踪所有的依赖可能会变成一项艰巨的任务。如果我们想使用 Spring 类，我们必须管理它们某些不同的依赖；因此，如果我们想避免重复代码，我们需要更好的方法来帮助我们找到依赖。

解决这个问题的一种方法是使用**依赖注入**。这是一种通过配置文件或 Java 注解来解除类依赖的模式。通过依赖注入，我们可以指定：

> 依赖注入本由 Java 内部提供，但由于它并没有提供，我们必须使用外部框架

我们所定义的每个依赖项的版本，然后这些依赖项会在运行时“注入”到需要它们的类中。例如，我们不再向 `StandardGameHolder` 构造函数传递一个 `OutputViewer`，而是决定使用 `ConsoleOutputViewer`，并让依赖注入处理将此特定依赖项插入到类中。当类被调用时，我们不需要在 `main` 方法中跟踪 `StandardGameHolder` 类的内部运作。

实现依赖注入的方法有很多：Spring Framework、Google Guice。正如 Guice 的 README 所说，依赖注入本由 Java 内部提供，但由于它并没有提供，我们必须改用外部框架。在这个项目中，我们将探索 Spring Framework，但你可能也想去看看 Google Guice。

## 依赖

- 被其他类使用的类或接口
- `IOC` 容器 (`IOC Container`)：框架中负责运行程序和依赖的部分
- Bean (`@Bean`)：`IOC` 可用于满足依赖的对象
- 服务 (`@Service`)：一个可以被实例化以形成 Spring 创建的 bean 的类
- Bean 工厂 (`Bean Factory`)：Spring 初始化时提供的对象。自动注入（`autowired`） bean 的参数就是依赖项
- `@Autowired`：用于决定 bean 是只实例化一次（`@Singleton`）还是每次需要时实例化（`@prototype`）

## Spring 概念

Spring 的核心概念是 bean。bean 是一个由 Spring 框架创建并控制的对象。Spring 并不是通过构造函数为提供这种 bean 的实例，而是搜索构造函数所需的额外 bean。例如，在我们的程序中，我们将创建一个类型为 `GameLogic` 的 bean，它将创建一个 `StandardGameLogic` 类的实例，以及该类需要使用的所有类。

### Spring 依赖注入

向 Spring Framework 注册 bean 有两种方法。第一种是编写 XML 文件来定义 bean。第二种方法是让 Spring 通过 Java 注解读取 bean 类，我们将在本节中使用后一种方法。

如果我们提供一个带有 `@Service` 注解的声明，每当 Spring 需要该特定类型的 bean 时，它就会创建该类的实例。例如，如果我们对一个接口有依赖，并且我们带有 `@Service` 注解创建了 `ServerHead` 类，Spring 将实例化 `ServerHead` 类以满足第一个 bean 的依赖。

我们可以使用 `@Bean` 注解通过定义方法来创建 bean。例如，如果我们定义了一个 `Player` 类并对其添加 `@Bean` 注解，那么每当 Spring 需要满足类型为 `Player` 的 bean 依赖时，它将使用该方法并返回值。如果方法失败，Spring 将寻找更多可以插入的 bean 以进行调用。

为了构建 bean，我们使用一种名为 **Bean Factory** 的设备，它由 Spring 提供。

在这个过程中可能会出现一些问题。例如，如果 Spring 尝试创建一个... 的 bean

# 教程

## Java

这是一个 Maven 项目，但到目前为止我们还没有使用 Maven 的功能。

注意：在本节中，“dependency”（依赖）一词指的是我们可以添加到项目中的外部 Java 软件包。在其他地方，我们将按照依赖注入的含义使用它，如下所示。

如果我们在 Eclipse 中展开项目，会在底部看到一个 `pom.xml`。双击此文件将打开底到 Build 的图表（图 1）。`pom.xml` 文件为我们提供了关于如何编辑 `pom.xml` 的图形界面。

我们想要做的第一个更改是使其成为 Spring Framework 项目的子项目。这将使我们更容易添加依赖项，而无需覆盖 Overview 标签页，选择标题为 Parent 的

### 图 1

Eclipse 上方为 Maven 配置文件 `pom.xml` 提供了一个实用的图形界面。

为了管理依赖项，我们给它一个名称和 ID，Maven 将下载其存储库

> 找不到类型为 `lead.UserModel` 的组件。

另一个问题发生在我们在同一个项目中注册两个类型相同的 bean 时。Spring 会给我们一条如下所示的错误消息：

### 找到 2 个匹配的 bean

在这种情况下，我们将使用进一步的注解来告诉 Spring 在本文中使用哪些 bean，但你可能也想去看看 `@Qualifier` 和注解。

### 安装 Spring

| 图 2 |

|---|---|

| Group Id | `org.springframework.parent` |

| Artifact Id | `spring-boot-starter` |

| Version | `1.5.8.RELEASE` |

| | Add... |

| | Remove |

### 选择依赖

- `junit 3.8.1` [test]

### 依赖

第一步我们需要将 Spring Framework 安装到我们的项目中，我们将使用 Maven 实现这一点。如果你从未用过任何 Java 框架，你可能不知道从哪里开始。在 Eclipse 中，点击图 4 中的 `...` 按钮。点击顶部的 Maven Build，然后按 New... 图标。在顶部，给它一个名称并按回车。

在下方，点击 Base 目录树下的 Workspace...，然后点击 "eggs" 项目的名称并按回车。在 General 下，向下找到，输入 install。然后，点击底部的 Run 开始依赖项的安装。

Maven 现在将从互联网下载 Spring Framework 所需的 JAR 文件，如果你的电脑上还没有这些文件。你可以通过展开 Package Explorer 中的 Maven Dependencies 文件夹来检查它们是否已下载。如果它在 Spring 5 中运行符合预期，那么你就可以开始工作了。

## 启动依赖注入

在项目 `luad.eggs.spring.boot` 中创建一个新包，并在其中创建两个类：`EggsServer`（它应该包含一个 `main` 方法）和 `EggsRunner`（它应该实现 `CommandLineRunner`）。在 `org.springframework.framework.boot` 包中的 `main` 方法应该启动 EggsServer。

```
public static void main(String[] args) {
    SpringApplication.run(EggsServer.class, args);
}
```

我们还需要在类定义处，在主类 EggsServer 的正上方添加注解：

```
@SpringBootApplication(scanBasePackages = {
    "luad.eggs"
})
```

从常规方法的角度来看，这个选择顺序没有提到我们的其他任何类。`SpringApplication.run` 方法的作用是搜索实现 `ApplicationRunner` 接口或 `CommandLineRunner` 接口的 bean。因此，我们可以选择在 EggsRunner 的 `run` 方法中启动应用程序。

`@SpringBootApplication` 注解告诉 Spring 扫描 `scanBasePackages` 以搜索这些包内的 bean。由于我们想将 EggsRunner 类注册为一个 bean，我们还必须在类声明的正上方添加 `@Component` 注解（即 `@Component` 这一行）。

由于我们想将 EggsRunner 类注册为一个 bean，我们还必须在类声明的正上方添加 `@Component` 注解（即 `@Component` 这一行）。

```
import java.util.observable.*;
import java.util.Set;
import luad.eggs.util.MapperFactory;
```

// 使用基于文本的类型定义的类模型。
