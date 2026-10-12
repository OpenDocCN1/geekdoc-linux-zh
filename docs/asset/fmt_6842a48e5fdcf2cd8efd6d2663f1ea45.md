
```csharp
report.Report = weatherObject.Result.main;
report.Humidity = weatherObject.Result.humidity;
Winds wind = weatherObject.Result.Winds;
report.Winds = wind;
return report;
```

## 填充 MVM 脚手架代码以实现简单的天气页面

视图（View）、模型（Model）和控制器（Controller）的基础脚手架现在支持简单的天气示例，无需担心下面所示的代码片段，此示例的完整文件可在`FileSite`获取。

## 09 调试 ASPNET Core Web 启动

通过探索`ASPNET Core`环境和`Web`托管的运行时节点，你可能需要在`Startup.cs`的各个点设置断点，以便有机会检查应用程序启动期间创建和安装的许多`ASPNET Core`对象和数据结构。

### Model 和 ViewModel：

模型实现使用`C#`结构来处理温度和风力，以及压力等相关数据。`ViewModel`类将这些对象分组，以便视图于消费。

```csharp
public class WeatherModel {
    public Temperature Temperature;
    public double Pressure { get; set; }
    public double Humidity { get; set; }
    public Winds Wind { get; set; }
}
```

## 10 写入控制器

脚手架已生成且`ASPNET Core`应用将构建并启动（成功），现在是关注所编写代码了。为了提供实时天气数据，我们将使用`openweather.api`提供的`OpenWeatherMap`公共`API`。该`API`为基础天气示例等低频率、简单的示例提供了增强的理解。

### Controller：

事件控制器的方法也已填充，在这种情况下是为了向`OpenWeatherMap`发起请求。它使用相同的模型类，从`FileSite`或磁盘选择选定的城市数据以完成实现。

注意，需要注册以获取代码调用设置中指定的`API`密钥。

`OpenWeatherMapClient`类封装了对`OpenWeatherMap API`的`RESTful`调用，在调用期间管理`API`密钥，并在与`.NET`框架`HttpClient`交互时使用异步语言特性。

```csharp
public ActionResult Index(WeatherViewModel model) {
    var weather = new WeatherViewModel();
    if (ModelState.IsValid) {
        if (model.SelectedCity == null) {
            var weatherReport = new WeatherHelper;
            GetWeather(model.SelectedCity);
            weather.Temperature = weatherReport;
        }
    }
}
```

![](img/90ce260f8df0a9c6339df2d60332346d_35_0.png)

## 温度；

`Web`浏览器和`localhost:5000`的地址栏，

在选择城市后应产生类似的结果。

```csharp
weather.Pressure = weatherReport.Pressure;
weather.Humidity = weatherReport.Humidity;
weather.Wind = weatherReport.Winds;
weather.SummaryDescription = weatherReport.Summary;
```

### 描述；

```csharp
{
    return View(Weather);
}
```

### 视图；

基于`HTML`的视图`Index.cshtml`面向`Web`界面。此脚手架已更新以支持城市选择以及从查询到`OpenWeather API`的数据绑定。视图使用键绑定显示天气数据。

![](img/90ce260f8df0a9c6339df2d60332346d_36_0.png)

```html
@model Weather.Models.WeatherViewModel
<h2>Current temperature is: @Model.Temperature</h2>
```

注意，你也可以从命令行提示符的项目级别（即存在`project.json`文件的地方）运行`ASPNET Web`。此外，你可以使用`dotnet run`命令直接执行应用程序。顺便一下，如果你想调整城市列表以符合你的偏好。

```csharp
public class WeatherViewModel
{
    public string SelectCity { get; set; }
    public List<City> Cities { get; set; } = new List<City>
    {
        new City { Value = "Chicago,", Text = "Chicago" },
        new City { Value = "Detroit,", Text = "Detroit" },
        new City { Value = "Seattle,", Text = "Seattle" }
    };
}
```

```html
<p>Current temperature is: @Model.Temperature</p>
<p>High: @Model.High</p>
<p>Low: @Model.Low</p>
<p>Pressure: @Model.Pressure</p>
<p>Humidity: @Model.Humidity</p>
```

注意，需要注册以获取代码调用设置中指定的`API`密钥。

`OpenWeatherMapClient`类封装了对`OpenWeatherMap API`的`RESTful`调用，在调用期间管理`API`密钥，并在与`.NET`框架`HttpClient`交互时使用异步语言特性。

虽然无疑`rsh`、`rcp`等命令仍然包含在大多数`Linux`发行版中，但需要注意的是，某些工具的执行可能比当前的`SSH`命令更快。然而，连接的安全性与加密有关。通常倾向于忽略这些遗留命令，但它们在某些情况下可能很有用。此文本用于与路由器、交换机等网络设备通信，这些设备可能无法`SSH`守护进程。这给……带来了问题

当`Linux`专业人员需要访问其他计算机进行远程管理时，可以使用命令行。有许多`SSH`命令可以提供帮助。与安全`Shell (SSH)`相关的工具允许远程登录和文件传输。通过这些工具，在不安全的网络上提供加密通信。通过虚拟网络隧道，你将能够拥有远程桌面。它支持`Telnet`、`ftp`（文件传输协议）、`ssh`（远程`shell`）、`rcp`（远程拷贝）、远程执行（远程登录）等。凭据在公共网络上被认为是不安全的。

`SSH`客户端是一个用于登录远程机器并在其执行命令的程序。它旨在取代`login`和`rsh`，并为不信任主机之间提供加密通信。`X11`连接、任意`TCP`端口和`UNIX`套接字可以在安全通道中转发。

`Swayam Prashak`拥有计算机工程硕士学位。他在信息技术领域工作多年，专注于安全、网络和`Web`服务器。他编写了许多出版物并在行业会议上演讲。你可以通过`swayam.prashak@gmail.com`联系他。

通过探索`ASPNET Core`环境和`Web`托管的运行时节点，你可能……

深入了解`Ubuntu`远程管理

## 资源

- [Linux Administration Basics](https://github.example.com/...)

- [Linux Administration and Configuration](https://github.example.com/...)

- [Remote Administration](https://github.example.com/...)

如今，`SSH`被认为是`Linux`专业人员进行远程管理的“瑞士军刀”。

`pswayam@pswayam-VirtualBox:~$ ssh-keygen`

Generating public/private rsa key pair.

Enter file in which to save the key (/home/pswayam/.ssh/id_rsa): already exists.

overwrite? (y/n)

Enter passphrase (empty for no passphrase):
