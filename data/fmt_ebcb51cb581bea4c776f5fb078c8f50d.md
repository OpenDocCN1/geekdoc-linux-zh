
一个简单的流写入器 `StreamWriter` 类提供对写入文本数据的支持。要声明 `StreamWriter`，请使用 `Dim` 语句。要声明类的新实例，请在类名前面加上 `New`，对于最基本的构造函数，请将文件流实例传递给 `StreamWriter` 类。第 7 章提供了有关实例化类和使用构造函数的详细信息。

初始化 `StreamWriter` 后，`Write` 方法将 `Char`、`Char` 数组或 `String` 写入流，但不会移到下一行。传入的变量是唯一参数。有关字符串的更多信息，请参阅第 4 章。`WriteLine` 方法执行相同的操作，但会自动向文件流添加新行。

调用 `Write` 或 `WriteLine` 方法时，流仅在内存中更新。`Flush` 方法将存储在流中的任何新数据写入文件。你可以向流中写入大量信息，并一步将其刷新到磁盘。因为内存传输数据的速度远快于磁盘，所以对磁盘进行单次大写入更高效。如果在调用 `Write` 或 `WriteLine` 后需要立即将数据移动到磁盘，请将 `StreamWriter.AutoFlush` 设置为 `True`。

`Close` 方法关闭写入器与文件的连接，并从内存中移除与写入相关的所有资源。在 `StreamWriter` 关闭之前，未写入的数据会自动刷新到文件中。

### 写入流

![](img/d6f772854306e15fb6df39b861a7b541_128_0.png)

- 1. 打开用于初始化流的方法。
- 注意：请参阅“使用文件流”一节来创建文件流。
- 2. 键入 `Dim myWriter`，将 `myWriter` 替换为写入器的变量名。
- 3. 键入 `As New IO.StreamWriter(myStream)`，将 `myStream` 替换为 `FileStream` 的名称。
- 4. 键入用于写入文件的代码。
- 5. 按 `F5` 运行项目。

流写入器将文本输出到文件。

# VISUAL BASIC .NET

## WATCH FOR FILE SYSTEM CHANGES

Windows Explorer 会在文件保存到磁盘时立即更新。Windows 子系统允许程序在特定目录更新时请求通知。当特定驱动器或目录上的文件系统发生变化时，您可以使用 `FileSystemWatcher` 类接收事件。

您可以创建 `FileSystemWatcher` 类的实例，也可以从工具箱的组件类别将 `FileSystemWatcher` 添加到 Windows 窗体。本主题假设您使用 Windows 窗体组件，因为它通过可视界面增加了简便性。

`Path` 属性指定组件监视更改的驱动器或目录。将 `IncludeSubdirectories` 设置为包含指定 `Path` 下的任何目录。`EnableRaisingEvents` 属性启用或禁用组件的通知事件。

组件提供四个在文件系统更改时触发的事件：`Changed`、`Created`、`Deleted` 和 `Renamed`。有关 Windows 窗体中事件的更多信息，请参阅第 2 章。

`Changed` 事件在文件的属性发生变化时触发，例如文件大小、最后修改日期和最后查看日期。您可以更改 `NotifyFilter` 属性以设置 `Changed` 事件触发的条件。例如，将 `NotifyFilter` 设置为 `LastWrite` 即可使组件仅在应用程序写入文件时触发。

`Created` 事件在文件系统出现新文件或目录时触发。`Deleted` 事件在用户从文件系统删除文件或目录时触发，而 `Renamed` 事件在文件或目录名称更改时触发。

每个事件都将 `FileSystemEventArgs` 对象作为变量 `e` 传递给您的事件处理程序。该对象包含一个 `Name` 属性，指定相对于指定 `Path` 的更改的文件或目录的名称。`FullName` 属性返回完整路径。对于 `Renamed` 事件，`OldFullName` 属性指定文件的先前名称。

![](img/d6f772854306e15fb6df39b861a7b541_129_0.png)

- 1. 创建一个新的 Windows 应用程序项目或打开一个现有项目。

本示例将 `ListBox` 控件加载到窗体上以显示输出。

- 2. 在工具箱中，单击组件类别。
- 3. 双击 `FileSystemWatcher` 组件。

组件加载到窗体的组件托盘中。

- 4. 在属性窗口中，在 `Path` 属性中输入要监视的路径。
- 5. 设置其他必要的属性。
- 6. 双击组件托盘中的 `FileSystemWatcher`。

### Extra

您可以使用一些规则来确保 `FileSystemWatcher` 正常运行。只要您不切换或移除磁盘，`FileSystemWatcher` 就会监视磁盘。如果远程驱动器出现网络问题，组件可能不再响应更改。`FileSystemWatcher` 不能与 CD 或 DVD 一起使用，因为驱动器内容是静态的。`FileSystemWatcher` 仅适用于 Windows 2000 和 Windows NT 4.0。远程机器必须安装其中一个平台才能使组件正常运行。但是，您不能从 Windows NT 4.0 计算机监视远程 Windows NT 4.0 计算机。

您可以根据文件系统的大小更改 `FileSystemWatcher` 的缓冲区大小。系统通过缓冲区通知组件更改。如果短时间内发生许多更改，缓冲区可能会溢出，导致组件无法跟踪目录中的更改。`InternalBufferSize` 属性可让您更改控件使用的内存量。增加缓冲区大小可能会导致计算机速度显著降低，因此应尽可能少地增加缓冲区。为了避免缓冲区溢出，请使用 `NotifyFilter` 和 `IncludeSubdirectories` 属性来过滤掉不需要的通知。

![](img/d6f772854306e15fb6df39b861a7b541_130_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_130_1.png)

`Changed` 事件加载到代码编辑器中。

7 输入代码以响应 `Changed` 事件。

您可以处理 `Created`、`Deleted` 或 `Renamed` 属性而不是 `Changed`，或响应多个事件。

注意：有关处理事件的更多信息，请参阅第 3 章。

8 按 `F5` 运行您的项目。

`FileSystemWatcher` 记录 `Path` 中所做的更改。

# 访问文件信息

可以使用 `IO` 命名空间中的 `FileInfo` 类来浏览文件和目录、删除和移动文件以及修改属性。

要将 `FileInfo` 类链接到文件，请使用 `New` 关键字创建该类的一个实例。构造函数接受一个参数，即要访问的路径和文件名。创建类实例后，即可开始访问属性。

`DirectoryName` 属性返回文件的完整路径。如果要访问该目录的属性，`Directory` 属性提供对 `DirectoryInfo` 对象的访问。有关 `DirectoryInfo` 的更多信息，请参阅“访问目录信息”部分。

`Extension` 属性返回文件的扩展名，即文件名中最后一个句点后的三字符或四字符扩展名。`Name` 属性指定不带路径的文件名。`FullName` 返回包含文件名的完整路径。`Length` 属性返回一个 `Long` 值，指定文件中的字节数。`Attribute` 属性使您能够检索或更改文件的属性。

`CreationTime` 属性使您能够使用 `DateTime` 变量检索或更改文件的创建日期和时间。`LastAccessTime` 属性使您能够检索或更改文件的最近访问时间。`LastWriteTime` 属性使您能够检索或更改文件的最近写入时间。

`Delete` 方法永久地从文件系统中删除文件，并且不需要参数。`CopyTo` 将文件复制到新位置。传递一个字符串作为参数，其中包含新位置的路径。您可以提供要复制到的路径，或复制的新文件名。`MoveTo` 执行相同操作，只不过该方法将文件复制到新位置并删除原文件。

![](img/d6f772854306e15fb6df39b861a7b541_131_0.png)

- 1. 创建一个新项目或打开现有项目。
- 2. 打开需要执行文件操作的方法或事件。
- 3. 键入 `Dim myFile As New IO.FileInfo("C:\Text.txt")`，将 `myFile` 替换为变量名，将 `C:\Text.txt` 替换为文件的完整路径。
- 4. 要修改文件属性，请键入 `myFile.LastWriteTime =`，将 `myFile` 替换为分配给 `FileInfo` 类的变量名，将 `LastWriteTime` 替换为某个属性。
- 5. 键入一个新值。
- 6. 键入代码以使用某个属性。

## 附加说明

`Attributes` 属性由 `FileAttributes` 枚举中的常量按位组合而成。您可以使用 `Attributes` 属性来测试文件是否具有特定属性。要测试文件，请使用 `And` 运算符与常量组合。要设置文件的属性，请使用 `Or` 运算符组合多个属性，并将值赋给 `Attributes` 属性。此处列出了 `FileAttributes` 中最重要的常量表。完整列表请参阅 Visual Basic .NET 帮助。

### FILEATTRIBUTE 常量：
