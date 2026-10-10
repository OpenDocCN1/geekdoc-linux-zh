

1.  单击“背景”（Backdrop），我们将看到各种背景选择。
2.  当我们看到喜欢的背景（如 Pebbles）时，可以单击“应用”（apply），然后单击“关闭”（close）来更改背景。但请注意，此操作仅更改当前所处工作区的背景。

若要更改其他工作区，我们可以转到相应工作区并在那里调出样式管理器（Style Manager）；或者，由于样式管理器已经打开，我们可以单击窗口右上角（“File”上方）的小“*”号，访问下拉菜单。在此处，我们可以选择“占据所有工作区”（Occupy All Workspaces）。然后我们只需转到其他工作区，样式管理器就已经在那里准备好了。背景区域是唯一需要注意移动到“其他工作区”的地方。

3.  若要更改颜色，请单击颜色（Color）图标。我们会得到一份不同的颜色方案列表供选择。如果某个方案不完全符合喜好，我们可以轻松修改颜色、色调、亮度和对比度。我们甚至可以从其他位置（例如网络上的图片）提取颜色，将其纳入颜色方案。一旦确定了喜欢的颜色，我们即可使用自定义名称保存该方案。

## 在前面板中添加或移除对象

通过在前面板中包含常用项，前面板可以让我们的工作稍微轻松一些。最频繁的操作之一是打开终端窗口。虽然 CDE 默认使用 xterm 作为终端窗口，但我们有时可能希望使用另一个 xterm 窗口（注：原文此处逻辑略显矛盾，可能指特定环境的 xterm 或指代不同终端，按原文直译）。我们将把它添加到“个人应用程序”（Personal Applications）子面板中，因为 xterm 存在于 AIX 和 HP-UX 系统上。Solaris 用户可以通过将 xterm 放在“主机”（Hosts）子面板中实现相同效果，该子面板容纳“本机”（This Host）终端仿真器。

添加对象到 CDE 前面板有两种方式：

-   将它们拖放到滑出式子面板中，然后将其设为该子面板的默认项。
-   修改 `/etc/dt/appconfig/types/C/dtwm.fp` 配置文件。此方法将在我们稍后创建操作和文件类型时使用。

通过拖放添加控制按钮的基本操作如下：

-   从应用程序管理器视图中，将您希望作为前面板按钮的应用程序图标拖出，并将其放置到相应子面板的安装区（顶部区域）。
-   将鼠标指针悬停在图标上，按下鼠标按钮 3 以显示子面板菜单。
-   选择“复制到主面板”（Copy to Main Panel）。

1.  **单击** AIX 或 HP-UX 上“个人应用程序”子面板（或 Solaris 上“主机”子面板）的**向上箭头**，使其弹出。
2.  **单击应用程序管理器**（Application Manager）图标，桌面应用程序和桌面工具位于此处。
3.  **双击 Desktop_Tools**。您会在这里找到 **Xterm**。
4.  **将 Xterm** 图标从 Desktop_Tools 拖放到 HP-UX 和 AIX 上“个人应用程序”子面板顶部的“安装图标”（Install Icon）框中，或 Solaris 上的“主机”（Hosts）子面板中。

现在，如果我们想在前面板中包含 **xterm**：

1.  在“个人应用程序”或“主机”子面板中，**右键单击 Xterm** 图标。
2.  根据您使用的 CDE 版本，选择 **Copy to Main Panel**（复制到主面板）或 **Promote to Front Panel**（提升到前面板）。

## 添加另一个工作区

对前面的另一个简单更改是添加另一个工作区。CDE 默认提供四个工作区，但这很容易更改。我们将再添加一个并将其命名为“Web View”（网络视图）。这可以作为我们访问互联网的窗口。

1.  将鼠标放在前面板的工作区（Workspace）区域，按下鼠标右键。
2.  从下拉菜单中选择“添加工作区”（Add Workspace）。工作区“New”（新建）已被添加。
3.  右键单击标记为“New”的新工作区，选择“重命名”（Rename）。输入 Web View 并按下 Return（回车）键。

如果我们想删除某个工作区，只需右键单击要移除的工作区，然后选择“删除”（delete）。

进行这类更改非常简单，它们有助于为个别用户个性化工作区。

## 以其他方式更改前面板

除了添加和移除按钮，您还可以以其他方式塑造前面板。这些其他方式使用工作区管理器（Workspace Manager）资源来修改默认值。以下资源与前面板相关：

-   **clientTimeoutInterval** - 从前面板启动客户端时，忙碌指示灯闪烁且指针保持为沙漏状的持续时间。
-   **geometry** - 前面板的 x 和 y 坐标位置。
-   **highResFontList** - 在高分辨率显示器上使用的字体。
-   **lowResFontList** - 在低分辨率显示器上使用的字体。
-   **mediumResFontList** - 在中等分辨率显示器上使用的字体。
-   **name** - 当 dtwm.fp 中存在多个前面板时，所使用的某个前面板的名称。
-   `pushButtonClickTime` - 区分两次单击和一次双击的时间间隔（以避免意外双击启动应用程序）。
-   `waitingBlinkRate` - 前面板忙碌指示灯的闪烁频率。
-   `workspaceList` - 工作区名称列表。
-   `title` - 显示在工作区按钮上的标题。

与其他所有工作区管理器资源一样，这些前面板资源具有以下语法：

```
Dtwm*screen*resource: value
```

例如，假设除了默认的四个工作区外，用户只需一个具有六个名为 Mail、Reports、Travel、Financials、Projects 和 Studio 的工作区的前面板。此外，他们更喜欢大字体，并决定使用 10 号粗体 New Century Schoolbook。作为系统管理员，您可以使用以下资源规范让所有用户满意：

```
Dtwm*0*workspaceList: One Two Three Four Five Six
Dtwm*0*One*title: Mail
Dtwm*0*Two*title: Reports
Dtwm*0*Three*title: Travel
Dtwm*0*Four*title: Financials
Dtwm*0*Five*title: Projects
Dtwm*0*Six*title: Studio
Dtwm*0*highResFontList:
 -adobe-new century schoolbook-bold-r-normal\n -10-100-75-75-p-66-iso8859-1
```

屏幕标识通常为 0，除非显示器同时具备图像平面和叠加平面能力。X*screens* 文件中屏幕的顺序决定了屏幕编号；第一个屏幕（通常是图像平面）标识为 0。请注意，在六个标题资源规范中包含了工作区名称（One, Two, Three, Four, Five 和 Six）。

这些更改可以添加到 `sys.resources` 文件中，该文件在本章后面的“高级 CDE 主题”中详细讨论。这些更改也可以通过使用 `EditResources` 操作将新的资源行插入每个用户的 `RESOURCE_MANAGER` 属性中，然后重启工作区管理器来实现。

显而易见的缺点是，您需要物理前往每个用户的工作区域，并接管机器几分钟。然而，好处是更改是即时的，并且会自动保存到恢复当前会话的用户的正确的 **dt.resources** 中。您还可以避免更改被覆盖，这种情况可能发生在用户仍在线时修改了错误的 **dt.resources** 文件的时候。

## 修改滑出式子面板中的内容

子面板在 **dtwm.fp** 中定义于前面板及前面板控件定义之后。要将子面板与前面板控件按钮关联，需将前面板控件名称列在子面板定义中的容器名称（container name）位置。

注意：全局更改在 **/etc/dt** 中进行。**$HOME/dt** 中进行本地或个别用户的更改。

要将滑出式子面板添加到前面板，请遵循以下步骤：

1.  将文件 **/usr/dt/appconfig/types/C/dtwm.fp** 复制到 **/etc/dt/appconfig/types/C/dtwm.fp** 或 **$HOME/dt/types/dtwm.fp**。
2.  确定滑出式面板要与之关联的控件按钮。
3.  在 **dtwm.fp** 中创建子面板定义文件。其形式如下：

```
SUBPANEL  SubPanelName
{
 CONTAINER_NAME AssociatedFrontPanelControlButton
 TITLE  SubPanelTitle
}
```

4.  为子面板创建子面板控件定义。其形式如下：

```
CONTROL  ControlName
{
 TYPE icon
 CONTAINER_NAME SubPanelName
 CONTAINER_TYPE SUBPANEL
 ICON  BitmapName
 PUSH_ACTION  ActionName
}
```

