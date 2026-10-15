

# 安装 Windows 服务

与常规应用程序不同，Windows 服务无法安装并在程序菜单上放置图标，因为服务必须在计算机启动时启动，并响应服务请求。您可以通过创建一个专门的类来提供初始化，从而将服务安装到系统上。创建此类需要对类有良好的理解。有关类、成员变量和构造函数的详细信息，请参阅第 7 章。

您必须向服务项目添加一个新类。在类模块中，您导入 System.Configuration.Install 和 System.ServiceProcess 命名空间。Install 命名空间位于一个单独的 DLL 中，您必须引用该 DLL。有关添加引用的信息，请参阅第 12 章。

在类定义中，您必须定义属性 <RunInstaller(True)>，以便服务安装可以找到要使用的适当类。您的类还必须继承自 Installer 类。

ServiceInstaller 和 ServiceProcessInstaller 对象提供了必要的安装功能。您的类应仅包含一个构造函数，该构造函数设置安装程序。ServiceInstaller 对象设置服务信息。ServiceInstaller 的 ServiceName 属性，您将其与服务项目名称设为相同，设置要安装的服务名称。将 StartType 属性设置为 ServiceStartType 枚举中的常量。

ServiceProcessInstaller 对象管理进程的运行方式。将 Account 属性设置为 ServiceAccount 枚举中的常量。使用 User 常量时，您必须使用 Username 和 Password 属性指定运行服务的用户帐户。

设置这两个对象后，您将它们都添加到 Installers 集合中。

在将服务构建为可执行文件后，您可以使用 Visual Basic .NET 的 installutil.exe 程序通过指定服务路径和文件名作为命令行参数来安装服务。要从计算机卸载服务，请在可执行文件名称后运行安装实用程序并加上 /u。

![](img/d6f772854306e15fb6df39b861a7b541_279_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_279_1.png)

- 1 在 Windows 服务项目中，添加对 System.Configuration.Install.dll 文件的引用。
- 2 添加一个继承自 Installer 的新类。

注意：有关更多信息，请参阅第 7 章和第 8 章。

- 3 在模块顶部键入 Imports System.ServiceProcess, System.Configuration.Install。
- 4 在 Class 关键字之前键入 <RunInstaller(True)>。
- 5 声明两个私有成员变量作为 ServiceInstaller 和 ServiceProcess Installer 类型的新的对象。
- 6 添加一个无参数的构造函数。
- 7 键入进程安装程序的名称并在其后加上 Account = 以及一个合适的常量。
- 8 键入服务安装程序的名称并在其后加上 ServiceName = 以及服务的名称。

# 额外

您可以使用 ServiceStartType 指定服务在客户端计算机上的安装方式。您可以指示是否希望自动启动服务、手动启动或禁用它。

| CONSTANT | DESCRIPTION |
|---|---|
| Automatic | 表示操作系统在系统启动时启动服务。如果自动启动的服务依赖于手动启动的服务，则手动启动的服务也会在系统启动时自动启动。 |
| Disabled | 表示一个被禁用的服务，用户或系统都无法启动。 |
| Manual | 表示服务手动启动。只有在用户或应用程序调用它时才能启动。 |

您可以使用 ServiceAccount 枚举指定服务使用的用户帐户。

| CONSTANT | DESCRIPTION |
|---|---|
| LocalService | 提供广泛的本地权限，并向远程服务器出示计算机的凭据。 |
| LocalSystem | 在本地计算机上充当非特权用户，并向远程服务器出示匿名凭据。 |
| NetworkService | 使用域控制器或工作组服务帐户进行身份验证。 |
| User | 在本地计算机上充当非特权用户，并向远程服务器出示计算机的凭据。 |

![](img/d6f772854306e15fb6df39b861a7b541_280_0.png)

- 9 键入服务安装程序变量的名称并在其后加上 StartType = 以及启动方法的常量。
- 10 键入 Installers.Add 并在其后加上服务安装程序对象的名称放在括号中。
- 11 键入 Installers.Add 并在其后加上进程安装程序对象的名称放在括号中。
- 12 构建服务项目。

![](img/d6f772854306e15fb6df39b861a7b541_280_1.png)

现在您可以运行 installutil.exe 实用程序将服务安装到机器上。您可以在 C:\WINNT\Microsoft.NET\vX 目录中找到该程序，其中 X 为当前程序版本。

使用位于程序菜单中管理工具中的服务控制台来停止和启动服务。

