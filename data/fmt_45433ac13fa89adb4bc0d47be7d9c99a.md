
```javascript
ipcRenderer.on("information-dialog-reply", (sender, index) => {
    let message = "You selected ";

    if(index == 0) {
        message += "yes.";
    } else {
        message += "no.";
    }

    document.getElementById("info-selection").innerText = message;
});
```

以及要在你的 C# 后端中包含的代码。

```csharp
Electron.IpcMain.On("information-dialog", async (args) =>
{
    var options = new MessageBoxOptions("This is an information dialog. Isn't it nice?")
    {
        Type = MessageBoxType.Info,
        Title = "Information",
        Buttons = new string[] { "Yes", "No" }
    };

    var result = await Electron.Dialog.ShowMessageBoxAsync(options);

    var mainWindow = Electron.WindowManager.BrowserWindows.First();
    Electron.IpcMain.Send(mainWindow, "information-reply", result.Response);
});
```

有许多类型的原生对话框窗口可用（除了上面描述的那种之外），你可以详细审查 `dialog.cs` 文件的代码，以获取更多关于如何使用此功能的示例。

这些仅是示例应用程序中展示的一小部分特性，但似乎它们是 Web 应用程序开发人员看来最独特的部分。

正如你所见，这些基本功能（菜单和对话框）在应用程序中的实现并不明显。管理由 Electron 架构引入的双进程存在许多复杂性。随着你的应用程序本身变得更加复杂，这种复杂性将会增加。

研究 `ElectronNET-API-Demos` 项目可能有助于你在 Electron.NET 开发人员所需的阶段学习过程中提供帮助。

**注意**：该示例无法从 `Visual Studio 2019` IDE 中执行，在这种情况下，你必须使用 `dotnet CLI`。

`ElectronNET-API-Demos` 的完整源代码可在 `GitHub` 上获取。

![](img/3d310cc066dda6e2dfa67a650614076f_161_0.png)

请注意，Electron.NET 仍在持续开发中，它对应用程序中包含的每个包的版本非常敏感。这使得当你尝试使用互联网上的代码示例应用程序（使用旧版本）时，构建过程变得有些棘手。

你可以在下方查看应用程序在各个平台上的渲染效果。

## 在 macOS 上：

![](img/3d310cc066dda6e2dfa67a650614076f_162_0.png)

## 在 ubuntu 上：

![](img/3d310cc066dda6e2dfa67a650614076f_163_0.png)

# ELECTRON.NET API 演示

- 组件
    - 创建和管理 WebViews
        - 包括进程内和进程外
    - 访问
        - 上下文菜单
        - 注册原生快捷键
    - 系统用户界面
        - 在系统文件管理器中打开外部链接
        - 系统与浏览器之间的交互
- 交互
    - 打印页面和文件
    - 共享进度
- 通信
    - 在两个进程之间通信
- 系统
    - 获取用户/系统交互信息
    - 用作此小应用的配置
- 页面
    - 偏好设置 & PDF
    - 截图

# 使用系统对话框

Electron.NET 允许你使用原生系统对话框来打开文件或目录、保存文件或显示信息消息。

这是使用进程的主要原因，与原生 UI 效率更高，并且允许用户在 Electron.net 和渲染进程之间进行交互。

![](img/3d310cc066dda6e2dfa67a650614076f_163_0.png)

`错误对话框`

```csharp
public static void Error() {
  var dlg = new ErrorDialog();
  dlg.ShowDialog();
}
```

`信息对话框`

```csharp
public static void Information() {
  var dlg = new InfoDialog();
  dlg.ShowDialog();
}
```

在这个演示中，使用 `InfoDlg` 类向渲染进程发送消息。渲染进程将拦截 `InfoDlg` 消息并响应来自在渲染进程中显示的 UI 线程的 `InformationMsg` 消息。

此外，`Msgs` 将是 `Msgs`，即渲染进程。

信息对话框可以显示任何自定义内容，包括：

- 标题
- 消息
- 图标

## 在 Windows 上：

- Electron.NET API 演示
- 查看
- 窗口
- 帮助

# 跟上节奏

使用 Electron.net 演示中的演示项目供你自己使用。`Electron Quick Start` 是一个最简单的模板，展示了基本应用的基本布局。如果你想制作一个 Electron 应用，`.NET` 模板是一个很好的起点。访问文档以了解如何使用 Electron.NET Core API 创建 Electron.NET 项目。

> `Electron Quick Start` 是一个最简单的模板，展示了基本应用的基本布局。如果你想制作一个 Electron 应用，`.NET` 模板是一个很好的起点。访问文档以了解如何使用 Electron.NET Core API 创建 Electron.NET 项目。

```csharp
// Include the namespace:
using ElectronNETCore;

public static void Main() {
  var host = new ElectronHost(ElectronHostOptions());
  host.Init().Run();
  host.WaitFor();
  host.Exit();
}
```

当你在 Windows 上运行应用程序（使用 `dotnet electronize start` 命令）时，会注意到一个安全对话框窗口出现（具体取决于所使用的安全级别），你必须确认提出的安全规则（点击下方窗口中的“确定”）。

![](img/3d310cc066dda6e2dfa67a650614076f_164_0.png)

## 8.3.6 Electron.NET 应用的优缺点

由于该应用是一种 Web GUI 实现，因此在所有平台上的渲染都非常相似。GUI 显示在平台间的一致性是该类解决方案所实现的特点（和优势）之一。能够使用增强的 JavaScript 界面设计是另一个优势，但此类桌面应用程序的性能并不总是最优的。

尽管你可以使用 Visual Studio 开发工具来开发 Web 应用程序部分，但 Electron.NET 工具无法在 Visual Studio 2019 内部使用，你必须使用 `dotnet CLI` 来初始化、运行、构建和打包应用程序（如前所述）。

Electron.NET 为 ASP.NET 开发人员提供了将其应用程序针对离线桌面环境运行的能力，但在这样做之前，仍有一些特定的 Electron.NET 知识需要消化。即使你是一名资深 ASP.NET Web 开发人员，你也必须经历一个学习曲线，以消化桌面开发的特定要求。

**注意：** Electron.NET 对其必须使用的 `.NET Core` 版本要求非常严格，你必须找到 Electron.NET 版本和 `.NET Core` 版本之间的正确组合，才能成功构建和执行程序（在某些情况下这可能很棘手）。

## 8.4 C++ 原生 GUI 应用程序

在 `.NET Core 3` 应用程序中实现原生 UI 有几种解决方案。使用原生 GUI 可以为每个操作系统的用户提供一种该应用程序是专门为其自身平台开发的感受。通过使用标准的窗体和控件，用户可以直接熟悉软件界面（应用程序看起来像是原生的）。

图形原语在三大系统（Linux、macOS、Windows）上的稳定标准化，为开发人员提供了编写在所有系统上都工作的图形界面的机会。通过使用经过适当包装的 `.NET Core 3`，开发人员可以受益于已存在相当一段时间的 C++ 库（可靠性）。

这里展示了在 `.NET Core 3` 应用程序中使用原生库实现 GUI 的架构模式（图 1）。
