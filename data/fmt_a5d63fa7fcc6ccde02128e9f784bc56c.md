
`Status` 属性返回服务的当前状态。该属性返回 `ServiceControllerStatus` 枚举中的一个常量。如果希望应用程序等待服务达到特定状态，请使用 `WaitForStatus` 方法。将 `ServiceControllerStatus` 枚举中的常量作为第一个参数传递。可选地，如果希望等待超时，可以将 `TimeSpan` 对象作为第二个参数传递。

![](img/d6f772854306e15fb6df39b861a7b541_281_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_281_1.png)

- 1. 创建一个新的 Windows 应用程序项目。
- 2. 单击工具箱的“组件”部分，然后双击 `ServiceController` 组件。
- 3. 在“属性”窗口中，在 `MachineName` 属性中键入服务运行所在的计算机名称。
- 4. 在 `ServiceName` 属性中键入服务的名称。
- 5. 在要操作服务的窗体方法中，键入组件的名称，并在其后加上 `.Stop()` 以停止服务。
- 该示例添加了三个按钮，使用 `Button1` 停止服务，`Button2` 启动服务，`Button3` 检查状态。

# 附加

您可以检索计算机上当前正在运行的服务列表。使用 `GetDevices` 方法返回设备驱动程序服务列表，使用 `GetServices` 方法访问非设备驱动程序服务列表。这两个方法都返回一个 `ServiceController` 类数组，表示每个服务。要访问本地计算机上的服务，请不为方法指定任何参数。对于远程计算机，将计算机名称指定为唯一的参数。`ServicesDependedOn` 属性返回服务所依赖的服务数组。您可以使用 `ServiceControllerStatus` 枚举通过 `Status` 属性检查服务的状态。

| 常量 | 描述 |
|---|---|
| `ContinuePending` | 服务正在尝试恢复。 |
| `Paused` | 服务已暂停。 |
| `PausePending` | 服务正在转换到暂停状态。 |
| `Running` | 服务正在运行。 |
| `StartPending` | 服务正在启动。 |
| `Stopped` | 服务已停止。 |
| `StopPending` | 服务正在停止。 |

![](img/d6f772854306e15fb6df39b861a7b541_282_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_282_1.png)

- 6 要启动服务，请键入组件的名称，后跟 `.Start()`。
- 7 要检查服务的状态，请键入 `If ServiceController1.Status =`，并将 `ServiceController1` 替换为服务的名称。
- 8 键入 `ServiceController Status` 枚举中的常量并完成 `If` 语句。
- 9 按 `F5` 运行应用程序。

服务会适当地响应由 `ServiceController` 发送的命令。

## 创建 Web 服务

Web 服务是一个 `ASP.NET` 文件，它提供了一个对象，该对象拥有一组方法，您的应用程序可以通过 Internet 连接访问这些方法。您可以创建一个 Web 服务项目和相应的对象集，以便从 Web 上的任何其他 XML 启用应用程序访问这些对象。

要创建 Web 服务项目，您从“新建项目”对话框中选择 `ASP.NET Web 服务` 模板。选择后，`VB.NET` 将创建一个服务类，并将其命名为与给定的项目名称相同。您使用此名称访问服务的 Web 方法。

每个 `ASMX` 服务类文件代表一个单独的 Web 服务。您可以在项目中创建其他类，但除非您想通过 Internet 使其可用，否则不要从 `System.Web.Services.WebService` 基类继承。单个代码模块文件中只能存在一个 Web 服务类。`ASP.NET` 会忽略您添加到代码模块中的其他类，即使它们继承自 `WebService` 基类。每个项目可以包含多个 `ASMX` 文件，每个文件包含一个单独的 Web 服务。

Web 服务项目也可以包含 Web 窗体页面。您可以从“项目”菜单添加 Web 窗体。有关将 Web 窗体添加到项目的更多信息，请参阅第 10 章。

要指定服务的命名空间和其他属性，您将属性添加到类标识符，即指定 `Class` 关键字的行。将 `WebService()` 放在箭头括号 (`< >`) 内，作为 `Class` 语句行的第一个条目。通过使用属性名称后跟冒号、等号和值来指定 `WebServiceAttribute` 类的属性。

`Description` 属性指定一个文本描述，用于说明服务的功能。`Namespace` 属性允许您为 Web 应用程序分配一个命名空间。

![](img/d6f772854306e15fb6df39b861a7b541_283_0.png)

1 在开发环境中单击 `File > New > Project`。
2 如果未选择，请单击 `Visual Basic Projects`。
3 在项目模板列表中单击 `ASP .NET Web Service`。
4 为服务项目输入一个名称。
5 单击 `OK`。

### 额外

您可以使用命名空间为 Web 服务提供不同的名称。不同的名称使客户端能够轻松访问他们想要的类。命名空间在使 Web 服务发挥功能方面也起着重要作用。由于 Web 的庞大，类落入同一名称的机会更多。因此，Web 服务需要由通用资源标识符 (`URI`) 定义的命名空间。您定义 `URI` 就像任何 Web 地址一样，除了此 `URI` 仅用作命名资源，并且不提供指向服务器上实际资源的链接。`URI` 用作服务的默认 XML 命名空间。您应使 `URI` 指定您拥有的唯一域。事实上，您可以使用 Web 服务的位置作为其命名空间标识。

#### 示例：

```
<WebService(Namespace:="http://www.mycomp.com/Webservices/", Description:="This class does something important.")>
Public Class VB.NETWebService
...
End Class
```

![](img/d6f772854306e15fb6df39b861a7b541_284_0.png)

开发环境创建项目并打开服务类的组件视图。

6 单击此处切换到代码视图链接。

代码编辑器加载。

您可以删除模板显示的示例代码。

7 在类声明的行上，键入 `<WebService (Description:="Sample")>`，将 `Sample` 替换为您服务的描述。

您现在可以向服务添加方法。

> 注意：有关更多信息，请参阅“添加 Web 服务方法”部分。

## 添加 Web 服务方法

Web 服务的强大之处在于其能够通过标准通信协议在 Internet 上公开功能。为了使您的服务发挥作用，您需要提供服务方法，供对象使用者使用。

要创建 Web 方法，您在 Web 服务类内部定义一个标准类方法。有关定义方法的更多信息，请参阅第 4 章。

为了使方法可供外部用户访问，您在方法之前放置 `WebMethod` 属性，以便编译器知道应公开哪些方法。为此，在定义方法的行上，您将 `WebMethod()` 属性放在左箭头括号和右箭头括号 (`<>`) 内。这将方法定义为可通过 Web 访问的公共方法。

`WebMethod` 属性包含许多属性来解释您的方法的目的。您与 `WebMethod` 属性一起使用的各种属性都是命名参数，这意味着您在要使用的参数名称后跟冒号和等号。在等号之后，您指定必要的值。您可以使用命名参数指定可用参数的部分列表。

`MessageName` 属性如果底层方法被重载，则定义方法的唯一标识。默认情况下，`MessageName` 仅等于您分配给类的名称。例如，如果您有两个 `Add` 类，一个用于整数，一个用于双精度，则必须指定唯一名称，例如 `AddInteger` 和 `AddDouble`。您使方法名称对 Web 服务器唯一。对于重载方法，您必须指定 `MessageName` 属性为每个方法提供唯一的 Web 方法名称。

`Description` 属性为方法指定文本描述，允许方法向客户端描述其功能。此描述会自动出现在服务帮助页面上。有关使用服务帮助界面的更多信息，请参阅“使用服务帮助界面”部分。

![](img/d6f772854306e15fb6df39b861a7b541_285_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_285_1.png)

- 1. 创建新的 Web 服务应用程序或打开现有应用程序。
- 2. 单击此处切换到代码视图链接。
- 3. 定义一个 `Public` 方法。

注意：要创建 Web 服务应用程序，请参阅“创建 Web 服务”部分。

注意：要定义方法，请参阅第 4 章。

代码编辑器出现。

### 额外
