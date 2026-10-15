

# VISUAL BASIC .NET

## WATCH FOR FILE SYSTEM CHANGES

Windows Explorer 会在文件保存到磁盘时立即更新。Windows 子系统允许程序在特定目录更新时请求通知。当特定驱动器或目录上的文件系统发生变化时，您可以使用 FileSystemWatcher 类接收事件。

您可以创建 FileSystemWatcher 类的实例，也可以从工具箱的组件类别将 FileSystemWatcher 添加到 Windows 窗体。本主题假设您使用 Windows 窗体组件，因为它通过可视界面增加了简便性。

Path 属性指定组件监视更改的驱动器或目录。将 IncludeSubdirectories 设置为包含指定 Path 下的任何目录。EnableRaisingEvents 属性启用或禁用组件的通知事件。

组件提供四个在文件系统更改时触发的事件：Changed、Created、Deleted 和 Renamed。有关 Windows 窗体中事件的更多信息，请参阅第 2 章。

Changed 事件在文件的属性发生变化时触发，例如文件大小、最后修改日期和最后查看日期。您可以更改 NotifyFilter 属性以设置 Changed 事件触发的条件。例如，将 NotifyFilter 设置为 LastWrite 即可使组件仅在应用程序写入文件时触发。

Created 事件在文件系统出现新文件或目录时触发。Deleted 事件在用户从文件系统删除文件或目录时触发，而 Renamed 事件在文件或目录名称更改时触发。

每个事件都将 FileSystemEventArgs 对象作为变量 e 传递给您的事件处理程序。该对象包含一个 Name 属性，指定相对于指定 Path 的更改的文件或目录的名称。FullName 属性返回完整路径。对于 Renamed 事件，OldFullName 属性指定文件的先前名称。

## WATCH FOR FILE SYSTEM CHANGES

![](img/d6f772854306e15fb6df39b861a7b541_129_0.png)

- 1. 创建一个新的 Windows 应用程序项目或打开一个现有项目。
本示例将 ListBox 控件加载到窗体上以显示输出。

- 2. 在工具箱中，单击组件类别。
- 3. 双击 FileSystemWatcher 组件。
组件加载到窗体的组件托盘中。

- 4. 在属性窗口中，在 Path 属性中输入要监视的路径。
- 5. 设置其他必要的属性。

- 6. 双击组件托盘中的 FileSystemWatcher。

## Extra

您可以使用一些规则来确保 FileSystemWatcher 正常运行。只要您不切换或移除磁盘，FileSystemWatcher 就会监视磁盘。如果远程驱动器出现网络问题，组件可能不再响应更改。FileSystemWatcher 不能与 CD 或 DVD 一起使用，因为驱动器内容是静态的。FileSystemWatcher 仅适用于 Windows 2000 和 Windows NT 4.0。远程机器必须安装其中一个平台才能使组件正常运行。但是，您不能从 Windows NT 4.0 计算机监视远程 Windows NT 4.0 计算机。

您可以根据文件系统的大小更改 FileSystemWatcher 的缓冲区大小。系统通过缓冲区通知组件更改。如果短时间内发生许多更改，缓冲区可能会溢出，导致组件无法跟踪目录中的更改。InternalBufferSize 属性可让您更改控件使用的内存量。增加缓冲区大小可能会导致计算机速度显著降低，因此应尽可能少地增加缓冲区。为了避免缓冲区溢出，请使用 NotifyFilter 和 IncludeSubdirectories 属性来过滤掉不需要的通知。

![](img/d6f772854306e15fb6df39b861a7b541_130_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_130_1.png)

Changed 事件加载到代码编辑器中。

7 输入代码以响应 Changed 事件。

您可以处理 Created、Deleted 或 Renamed 属性而不是 Changed，或响应多个事件。

注意：有关处理事件的更多信息，请参阅第 3 章。

8 按 F5 运行您的项目。

FileSystemWatcher 记录 Path 中所做的更改。

