
现在，让我们添加 `templateinfo`，它包含 `folderType`。这些标签决定了在打开之后，Windows 资源管理器中显示的列和详细信息

> 521 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/windows/win32/shell-library-schema

> 522 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/windows/win32/shell-library-entry-namespace-versioning

> 523 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/win32/shell-library-description

> 524 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/win32/shell-library-name

> 525 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/win32/shell-library-version

> 526 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/win32/shell-library-ispinned

> 527 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/win32/shell-library-icon-reference

> 528 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/win32/shell-library-templateinfo

> 529 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows/win32/shell-library-foldertype

PWK - Copyright © 2023 OffSec Limited

下方的列表包含了库文件的命名空间。这是从 Windows 7 开始的库文件版本的命名空间。列表还包含了库描述的结束标签。以下所有内容都将添加到 `libraryDescription` 标签内部。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<libraryDescription xmlns="http://schemas.microsoft.com/windows/2009/library">

</libraryDescription>
```

### 列表 222 - XML 和库描述版本

接下来，我们将添加两个提供库的信息。`name` 标签指定此库的名称。我们不能将其与可以随机定义的属性名称混淆。我们需要通过提供 DLL 和索引来指定库的名称。我们可以按照微软网站上的指定，使用 `#shell32.dll,-34575` 或 `@windows.storage.dll,-34582`。我们将使用后者，以避免可能标记“shell32”的文本过滤器产生任何问题。`version` 标签可以设置为你任选的数值，例如：

```xml
<name>@windows.storage.dll,-34582</name>
<version>6</version>
```

### 列表 223 - 库的名称和版本标签

接下来，我们将添加库的 `isLibraryPinned`。此元素指定库是否被固定在 Windows 资源管理器的导航窗格中。对于我们的目标来说，这可能是让整个过程看起来更真实的另一个小细节，因此我们将将其设置为 `true`。我们将添加的下一个标签是 `iconReference`，用于识别库文件。我们必须以与元素名相同的格式指定值。我们可以使用 `imagesres.dll` 在所有 Windows 图标中进行选择。我们可以使用“1002”作为文档文件夹或图片文件夹图标。我们将提供后者以使其看起来更良性。

```xml
<isLibraryPinned>true</isLibraryPinned>
<iconReference>imagesres.dll,-3603</iconReference>
```

### 列表 224 - 导航栏固定和图标配置

现在，让我们添加 `templateinfo`，它包含 `folderType`。这些标签决定了在打开之后，Windows 资源管理器中显示的列和详细信息

### 一旦连接

一旦连接，我们会在桌面上找到 Visual Studio Code (VSC)^50，我们将用它来创建我们的库文件。我们需要注意的是，我们也可以使用记事本来创建该文件。双击图标打开 VSC。

![](img/987dc9f6ebd8893c565a1d124d7724e6_340_0.png)

在菜单栏中，我们点击文件（File） > 新文本文件（New Text File）。然后，我们将空文件保存为 offsec 用户桌面上的 `config.ms`。只要我们以这个文件扩展名保存文件，它就会显示一个图标。虽然该图标看起来并不危险，但 Windows 并不经常使用它，因此可能会引起怀疑。为了增加受害者执行我们文件的概率，让我们更改它的外观吧。

图 189：Windows 11 桌面

![](img/987dc9f6ebd8893c565a1d124d7724e6_340_1.png)

图 190：空的 Windows 库文件

库文件由三个主要部分组成并用 XML 编写，以指定访问远程位置的参数。这些部分是：常规库信息、库属性和库位置。让我们通过添加并解释标签来构建 XML 代码。我们可以参考

^520 (Visual Studio, 2022), https://code.visualstudio.com/
