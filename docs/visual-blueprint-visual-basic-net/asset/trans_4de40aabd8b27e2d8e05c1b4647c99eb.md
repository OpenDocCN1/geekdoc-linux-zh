

# 监视 Windows 服务

您可以在另一个应用程序中监视并操作 Windows 服务的状态。例如，您可以提供一个配置界面，允许用户配置服务的属性。当用户进行配置更改时，您可以停止并重新启动服务，以使配置更改生效。

ServiceController 组件是 System.ServiceProcess 命名空间的一部分，用于操作正在运行的服务。您可以通过工具箱的“组件”部分添加此组件，也可以在代码中创建该类的对象实例。有两个属性指定要使用的服务。MachineName 属性设置服务运行所在的计算机。如果服务在本地计算机上运行，则将其设置为句点 (.)。将 ServiceName 属性设置为要操作的服务的名称。

CanPauseAndContinue 属性返回一个值，该值确定服务是否可以暂停和恢复。如果此值为 True，则可以使用 Pause 方法暂停服务，并使用 Continue 方法恢复服务的执行。CanStop 属性返回一个值，该值确定服务在启动后是否可以停止。如果将其设置为 True，则可以使用 Stop 方法停止服务。您可以使用 Start 方法启动服务。

Status 属性返回服务的当前状态。该属性返回 ServiceControllerStatus 枚举中的一个常量。如果希望应用程序等待服务达到特定状态，请使用 WaitForStatus 方法。将 ServiceControllerStatus 枚举中的常量作为第一个参数传递。可选地，如果希望等待超时，可以将 TimeSpan 对象作为第二个参数传递。

![](img/d6f772854306e15fb6df39b861a7b541_281_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_281_1.png)

- 1. 创建一个新的 Windows 应用程序项目。
- 2. 单击工具箱的“组件”部分，然后双击 ServiceController 组件。
- 3. 在“属性”窗口中，在 MachineName 属性中键入服务运行所在的计算机名称。
- 4. 在 ServiceName 属性中键入服务的名称。
- 5. 在要操作服务的窗体方法中，键入组件的名称，并在其后加上 .Stop() 以停止服务。
- 该示例添加了三个按钮，使用 Button1 停止服务，Button2 启动服务，Button3 检查状态。

# 附加

您可以检索计算机上当前正在运行的服务列表。使用 GetDevices 方法返回设备驱动程序服务列表，使用 GetServices 方法访问非设备驱动程序服务列表。这两个方法都返回一个 ServiceController 类数组，表示每个服务。要访问本地计算机上的服务，请不为方法指定任何参数。对于远程计算机，将计算机名称指定为唯一的参数。ServicesDependedOn 属性返回服务所依赖的服务数组。您可以使用 ServiceControllerStatus 枚举通过 Status 属性检查服务的状态。

| 常量 | 描述 |
|---|---|
| ContinuePending | 服务正在尝试恢复。 |
| Paused | 服务已暂停。 |
| PausePending | 服务正在转换到暂停状态。 |
| Running | 服务正在运行。 |
| StartPending | 服务正在启动。 |
| Stopped | 服务已停止。 |
| StopPending | 服务正在停止。 |

![](img/d6f772854306e15fb6df39b861a7b541_282_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_282_1.png)

- 6 要启动服务，请键入组件的名称，后跟 .Start()。
- 7 要检查服务的状态，请键入 If ServiceController1.Status = ，并将 ServiceController1 替换为服务的名称。
- 8 键入 ServiceController Status 枚举中的常量并完成 If 语句。
- 9 按 F5 运行应用程序。

服务会适当地响应由 ServiceController 发送的命令。

