

![](img/6c226e8ba1efd427dec3bf582418d33f_160_0.png)

FIGURE 7-4 The KDE file manager

以不同的方式查看。您可以将文件和目录显示为图标、小图标或详细列表。详细列表提供权限、所有者、组和大小信息。权限是控制对该文件访问的权限（参见第28章）。配置文件，也称为隐藏文件，通常不会显示。要让文件管理器显示这些文件，请从 View 菜单中选择 Show Hidden Files。Konqueror 还支持拆分视图，让您在同一窗口中查看不同的目录（Windows 菜单）。您可以垂直或水平拆分。

您可以通过单击文件或先选择它然后在 File 菜单中选择 Open 条目来打开文件。如果您想选择文件或目录，则需要按住 CTRL 键同时单击它，或单击一次。双击打开文件。如果文件是程序，则该程序会启动。如果是数据文件，例如文本文件，则会使用该数据文件运行关联的应用程序。例如，如果您双击文本文件，Kate 应用程序将开始显示该文件。如果 Konqueror 无法确定要使用的应用程序，它会打开一个对话框提示您输入应用程序名称。您可以单击此框上的 Browse 按钮，使用目录树定位您想要的应用程序程序。

文件管理器还可以提取 tar 归档文件并安装 RPM 包。归档文件是以 .tar.gz、.tar 或 .tgz 结尾的文件。单击归档文件会列出其中的文件。您只需将其拖出窗口即可提取特定文件。单击归档中的文本文件会使用 Kate 显示它，而单击图像文件会使用 KView 显示它。选择 RPM 包会使用 redhat-config-packages 实用程序打开它，然后您可以使用它来安装该包。

## Navigation Panel

导航面板是一个侧边栏，列出了用户可以使用 Konqueror 访问的不同资源。您可以通过在 Windows 菜单中选择其条目来打开或关闭导航面板。侧边栏使用 Navigation Panel Configuration 工具进行配置，该工具可作为导航面板按钮栏上的第一个按钮访问。

| Keys | Description |
|---|---|
| ALT-LEFT ARROW, ALT-RIGHT ARROW | Backward and Forward in History |
| ALT-UP ARROW | One directory up |
| ENTER | Open a file/directory |
| ESC | Open a pop-up menu for the current file |
| LEFT/RIGHT/UP/DOWN ARROWS | Move among the icons |
| SPACEBAR | Select/unselect file |
| PAGE UP, PAGE DOWN | Scroll up fast |
| CTRL-C | Copy selected file to clipboard |
| CTRL-V | Paste files from clipboard to current directory |
| CTRL-S | Select files by pattern |
| CTRL-L | Open new location |
| CTRL-F | Find files |
| CTRL-W | Close window |

TABLE 7-2 KDE File Manager Keyboard Shortcuts

如果您知道要再次访问特定目录，可以对其进行书签，就像对网页一样。只需打开目录并在 Bookmarks 菜单中选择 Add Bookmarks 条目。然后该目录的条目将被放置在文件管理器的 Bookmark 菜单中。要再次移动到该目录，请在 Bookmark 菜单中选择其条目。为了帮助您从一个目录导航到另一个目录，您可以使用 Location 字段或目录树。在 Location 字段中，您可以输入目录的路径名，如果您知道的话，然后按 ENTER。目录树提供了一个树形列表，列出系统上和您主目录中的所有目录。

## Copy, Move, Delete, Rename, and Link Operations

要对文件或目录执行操作，您首先必须选择它。在 Red Hat 上，要选择文件或目录，您单击文件的图标或列表。要选择多个文件，请继续按住 CTRL 键同时单击您想要的文件。您也可以使用键盘方向键在文件图标之间移动，然后使用 SPACEBAR 选择您想要的文件。

要复制和移动文件，您可以使用鼠标的标准拖放方法。要复制文件，您可以使用文件管理器找到它。打开另一个文件管理器窗口到要复制文件的目录。然后单击并拖动文件图标到该窗口。会出现一个弹出菜单，其中包含 Move、Copy 或 Link 的选项。选择 Copy。要将文件移动到另一个目录，请遵循相同的程序，但从弹出菜单中选择 Move。要复制或移动目录，请使用与文件相同的程序。目录的所有文件和子目录也会被复制或移动。

