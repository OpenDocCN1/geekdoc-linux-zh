

# 3.3.2 ASP.NET 5

要运行 ASP.NET 5 应用程序，我们可以使用 `dnx` 搭配 kestrel。首先，导航到 HelloWeb 项目。输入以下命令。

```
$ cd samples/latest/HelloWeb/
$ dnx . kestrel
```

```
agusk@ubuntu15: ~/books/aspnet/home/samples/latest/ConsoleApp
agusk@ubuntu15: ~/books/aspnet/home$ ls
CONTRIBUTING.md    dnvm.ps1       GettingStartedDeb.md   README.md
dnvm.cmd           dnvm.sh        Home.sln               samples
dnvm.ps1           LICENSE.txt
agusk@ubuntu15: ~/books/aspnet/home$ cd samples/latest/ConsoleApp/
agusk@ubuntu15: ~/books/aspnet/home/samples/latest/ConsoleApp$ dnx . run .
Hello World
agusk@ubuntu15: ~/books/aspnet/home/samples/latest/ConsoleApp$
```

现在打开浏览器，然后导航到 `http://localhost:5004/`。你应该能看到 ASP.NET 5 应用程序。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_34_0.png)

要停止 kestrel，你可以输入 `exit`。

```
exit
```

### 3.3.3 ASP.NET MVC

要运行 ASP.NET MVC，我们可以使用 `dnx`。首先，导航到 HelloMvc 项目。输入以下命令。

```
$ cd samples/latest/HelloMvc/
$ dnx . kestrel
```

```
agusk@ubuntu15:~/books/aspnet/home/samples/latest/HelloMvc$ ls
Controllers  Models  project.lock.json  Startup.cs  wwwroot
HelloMvc.xproj  project.json  Properties  Views
agusk@ubuntu15:~/books/aspnet/home/samples/latest/HelloMvc$ dnx . kestrel
Started
```

现在打开浏览器，然后导航到 `http://localhost:5004/`。你应该能看到 ASP.NET MVC 应用程序。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_35_0.png)

要停止 kestrel，你可以输入 `exit`。

## 3.4 开发工具

下一步是构建程序。为了编写程序，你可以使用任何文本编辑器。微软还提供了 Visual Studio Code。它运行在 Windows、Linux 和 Mac 上。你可以在 `https://code.visualstudio.com/` 上下载它。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_36_0.png)

# 4. 在 Windows 上部署 ASP.NET 5

在本章中，我们将学习如何在 Windows 上部署 ASP.NET 5。

## 4.1 入门

在本节中，我们开始在 Windows 上部署 ASP.NET 5。在这本书中，我使用的是 ASP.NET 5 预览版，beta4。为了说明，我使用 Windows 8.1。请遵循下一节的安装步骤。

## 4.2 部署 ASP.NET 5

此安装过程基于此文档，`https://github.com/aspnet/Home/blob/dev/GettingStartedDeb.md`。在本节中，我们在 Windows 上安装 ASP.NET 5。首先，你更新你的 Windows。

通常，要在 Ubuntu 上安装 ASP.NET 5，你可以执行以下步骤：

- 安装 .NET
- 安装 DNVM
- 安装 git（可选）

### 4.2.1 安装 .NET

你需要最新版本的 .NET Framework 运行时。要安装它，你可以在 `https://www.microsoft.com/net` 上下载它。

### 4.2.2 安装 DNVM

你可以通过命令提示符安装 DNVM。打开 CMD 并输入此命令。

```
@powershell -NoProfile -ExecutionPolicy unrestricted -Command "&{$Branch='dev';iex ((new-object net.webclient).DownloadString('https://raw.githubusercontent.com/aspnet/Home/dev/dnvminstall.ps1'))}"
```

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_39_0.png)

如果成功，你可以通过输入此命令来验证 `dnvm` 的位置。

```
where dnvm
```

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_40_0.png)

如果收到错误，请检查你的 PATH 配置。确保 `.dnx` 路径已经添加。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_40_1.png)

下一步是升级 DNVM。输入此命令。

```
$ dnvm upgrade
```

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_41_0.png)

现在你已经安装了 `dnvm`。它将用于管理 Windows 上的 ASP.NET 5 运行时。你可以通过输入此命令来验证 `dnvm`。

```
$ dnvm help
```

因此你会看到 `dnvm` 参数列表。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_41_1.png)

你还可以通过输入此命令来查看你的 DNX 运行时列表。

```
$ dnvm list
```

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_42_0.png)

### 4.2.3 安装 git

此任务是可选的，但我建议安装它，因为我们想从 `https://github.com/aspnet/Home` 运行示例应用程序。你可以在 `https://git-scm.com/downloads` 上下载来安装 git。

## 4.3 测试

为了测试我们的 ASP.NET 5，我们使用来自 `https://github.com/aspnet/Home` 的代码示例。我们克隆这些代码示例，然后使用 `dnu` 命令还原所有必需的库。

输入这些命令。

```
$ git clone https://github.com/aspnet/Home
$ cd Home
$ dnu restore
```

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_43_0.png)

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_43_1.png)

现在你准备好运行代码示例了。

### 4.3.1 ASP.NET 控制台

要运行 ASP.NET 控制台，我们可以使用 `dnx`。首先，导航到 ConsoleApp 项目。输入这些命令。

```
$ cd samples/latest/ConsoleApp/
$ dnx . run .
```

如果成功，你可以在终端上看到“Hello World”消息。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_44_0.png)

### 4.3.2 ASP.NET 5

要运行 ASP.NET 5 应用程序，我们可以使用 `dnx` 搭配 kestrel。首先，导航到 HelloWeb 项目。输入这些命令。

```
$ cd samples/latest/HelloWeb/
$ dnx . kestrel
```

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_45_0.png)

当你运行这些命令时，你可能会收到一个安全确认。请点击 **Allow access** 按钮以授予安全权限。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_45_1.png)

现在打开浏览器，然后导航到 `http://localhost:5004/`。你应该能看到 ASP.NET 5 应用程序。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_46_0.png)

要停止 kestrel，你可以输入 `exit`。

```
exit
```

### 4.3.3 ASP.NET MVC

要运行 ASP.NET MVC，我们可以使用 `dnx`。首先，导航到 HelloMvc 项目。输入这些命令。

```
$ cd samples/latest/HelloMvc/
$ dnx . kestrel
```

```
D:\Temp\Home>cd samples/latest/ConsoleApp/
D:\Temp\Home\samples\latest\ConsoleApp>dnx . run.
Hello World

D:\Temp\Home\samples\latest\ConsoleApp>cd ..

D:\Temp\Home\samples\latest>cd HelloWeb

D:\Temp\Home\samples\latest\HelloWeb>dnx . kestrel
```

现在打开浏览器，然后导航到 `http://localhost:5004/`。你应该能看到 ASP.NET MVC 应用程序。

```
D:\Temp\Home\samples\latest\ConsoleApp>cd ..

D:\Temp\Home\samples\latest>cd HelloWeb

D:\Temp\Home\samples\latest\HelloWeb>dnx . kestrel
Started
exit

D:\Temp\Home\samples\latest\HelloWeb>cd ..

D:\Temp\Home\samples\latest>cd HelloMvc

D:\Temp\Home\samples\latest\HelloMvc>dnx . kestrel
Started
exit
```

要停止 kestrel，你可以输入 `exit`。

## 4.4 开发工具

下一步是构建程序。为了编写程序，你可以使用任何文本编辑器。微软还提供了 Visual Studio Code。它运行在 Windows、Linux 和 Mac 上。你可以在 `https://code.visualstudio.com/` 上下载它。

![](img/2b788c7cc1c2fc37b428b6e7f92dcaed_48_0.png)

# 5. ASP.NET 5 开发

在本章中，我将解释如何处理 ASP.NET 5 开发。

## 5.1 入门

在本章中，我们学习如何从头开始为 ASP.NET 5 编写程序。我们使用两个场景，ASP.NET 5 控制台和 ASP.NET 5 MVC，进行说明。

## 5.2 构建 ASP.NET 5 控制台应用程序

在这种情况下，我们为 ASP.NET 5 控制台构建一个简单的程序。我们使用 Math 类来实现 Math 操作。

### 5.2.1 创建项目

要创建一个项目，我们可以创建一个文件夹，名为 ConsoleDemo。在 Linux/OS X 中，你可以在终端中输入此命令。

```bash
mkdir ConsoleDemo
```

此外，我们创建一个文件，**project.json**。输入此脚本。

```json
{
"dependencies" : {
},
"commands" : {
"ConsoleApp" : "ConsoleDemo"
},
"frameworks" : {
"dnx451" : { },
"dnxcore50" : {
"dependencies" : {
"System.Console" : "4.0.0-beta- *"
}
}
}
}
```

此文件是一个项目配置，使用 ASP.NET 5 DNX。

### 5.2.2 编写程序

要创建一个程序，我们创建一个类，SimpleMath。创建一个文件，名为 **SimpleMath.cs**。然后，编写此代码。

```csharp
using System;

public class SimpleMath
{
public SimpleMath(){ }
}
```

