
## Mesa 称为 Jar-Jar Binks

如果你的程序包含 20 个类，由于失去控制的习惯，独立文件会变得有问题，寻找文件将成为一项困难且令人厌的任务。部署 `JAR` 归档 —— 类的集合以及描述其内容的清单文件。

从 Java 运行时环境启动第三方程序只需三行代码。使用运行时 `exec` 函数，它接收要执行的程序或程序的路径，然后等待进程直到执行完成。

Eclipse 可以以极少的努力生成 `JAR` 文件。该过程从点击 `File/Export` 并选择你的可运行文件（Runnable File）开始。你指定正在执行的类，它将被用作清单文件。通过 `Export` 目录指定存储目标后，点击 `Finish` 按钮。调用 `JAR` 文件中包含的代码像调用独立类一样完成。最重要的一点是，你现在必须向 Java 传递文件名。

程序的很大一部分专门用于处理你的 shell 脚本。我们使用 `BufferedReader` 类来从运行时流中获取数据：

## java-Untitled jar

## 向一个方向

```java
StringBuffer output = new StringBuilder();
BufferedReader reader = new BufferedReader(new InputStreamReader(proc.getInputStream()));
String line = "";
while (line = reader.readLine()) != null) {
  output.append(line + "\n");
}
System.out.println(output.toString());
catch (Exception e) {
}
```

Java 的真正力量在于它从单元建模复杂系统的能力。轻松选择是很的：进程单元与许多对象和资源交互，同时具有底层命令单元来获取数据并进行计算。顺便说，这并不简单。

## .NET Core 和 Docker 教程

## 使用 ASP.NET Core 和 Docker 实现微服务架构

![](img/db87aeaad27e4efbbf36e01180be02e6_37_0.png)

学习如何使用 `ASP.NET` 在 Linux 中开发基于 .NET 的微服务，从零到运行容器。

`ASP.NET` 代表了 .NET 世界的新事物。微软通过其活跃的开源社区，实现了一个 Web 应用程序框架，该框架已通过多种方式用于开发基于 .NET 的微服务。现在，利用 `Docker` 方法和容器对 C# 中的 Web API 进行轻松部署和扩展已成为可能。

要开始学习，请如下所示启动 Yokohama 终端提示符：

本文将介绍使用 `ASP.NET Core` 开发 RESTful Web API 的关键方面，以及关于如何在 Linux 环境下部署它们的实用实用技巧。为了演示开发中的微服务，将处理云端。

![](img/db87aeaad27e4efbbf36e01180be02e6_37_1.png)

- .NET SDK（支持大多数 Linux）
- Docker 命令行项目生成器，用于创建基于 C# 的 Web API
- VM（使用 OpenARP 开发支持）
- Docker 和 `docker-compose` 命令行工具，用于包含复制 Web API 的 `ASP.NET Core` 容器

从 Yokohama `ASP.NET Core` 生成器的顶部菜单开始，选择 `Web API` 选项并继续输入以下项目名称：

## MyWeatherApi

### 编写 ASP.NET Core Web API 实现

使用生成的 Web 项目脚架，我们将定义一个短端点，支持对温度、当前日期和当天天气的查询。

`class WeatherController : inherit from Controller.`

API 实现将包含 `GetTemperatureDetail`。此方法将调用客户端助手 `open WeatherReporter` 返回与城市相关的实时温度。

Kevin Winter 是矿业公司的软件技术专家和 经理。他喜欢 Linux 并构建了许多项目，特别是使用 C#。

## 资源

### 适用于任何平台的 .NET

开始使用 `ASP.NET Core`

### Yokohama 生成器

`http://bit.ly/z3okk`

### 用于 Docker 和脚本的 Yokohama 生成器

`https://docker.io/docker`

### Docker

`docker.io`

`ASP.NET Core` 的 Docker 镜像仓库

### Kubernetes

`kubernetes.io`

打开 Map API

`http://bit.ly/2fdf64`

### 作者的 GitHub 项目空间

`http://bit.ly/2cck8p`

## 02 生成 ASP.NET Core 项目骨架

要使用 Yokohama 命令行生成器开始 `ASP.NET Core` Web 项目的骨架，请参考上一篇关于 `ASP.NET` 的文章，并查看 `OpenMapper` 以实现 RESTful Web

![](img/db87aeaad27e4efbbf36e01180be02e6_37_2.png)

上方：基于 `ASP.NET Core` 栈 .NET Web API 的微服务架构蓝图。该蓝图详细说明了 `Docker` 和容器管理，以实现可扩展的服务架构和一致、健壮的部署模型。

API 的路由使用特性路由定义，此 API 的基础是 `weather/city`，因为它绑定到 `WeatherController` 类。

方法命名为 `GetTemperatureDetail`，并带有 HTTP 注解。此外，路径被扩展以包含 'temperature' 和一个接受城市字符串作为输入的参数。因此，路径结束于 `weather/city/temperature/{city}`。

从 RESTful Web 来看，可以创建为结果：`result:5000/weather/city/temperature/london`。

实时数据封装在 JSON 对象中，它符合 `ActionResult` 接口。该对象以 JSON 格式返回并由 Web 端解析给消费者 RESTful 客户端。

下面的代码代表了 Controller 如何突出显示。你可以在本文的源码中找到扩展此文章的示例。

```csharp
[Route("api/{controller}")]
public class WeatherController : Controller
{
    [HttpGet("temperature/{city}")]
    public IActionResult GetTemperature(string cityLocation)
    {
        var reporter = new OpenWeatherReporter();
        var weatherReport = reporter.GetWeather(cityLocation);
        return new ObjectResult(weatherReport);
    }
}
```

使用 `Fact` 标记可执行方法。`Assert` 类包含多种断言方法来执行集成测试，检查返回的温度是否在预期范围内。

```csharp
using XUnit;
[Fact]
public void WeatherReportInExpectedRange(string city = "Chicago")
{
    var reporter = new OpenWeatherReporter();
    var weatherReport = reporter.GetWeather(city);
    Assert.InRange(weatherReport.Temperature, -15, 85);
}
```

序列化为 JSON 的对象代表 `Temperature` 类型：
