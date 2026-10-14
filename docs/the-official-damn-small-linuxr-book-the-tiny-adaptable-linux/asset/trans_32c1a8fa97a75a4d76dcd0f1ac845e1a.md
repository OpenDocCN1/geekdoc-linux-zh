

运行程序。要跟随我们的示例，请点击 xmahjongg.uci.info。Xmahjongg 软件扩展的 info 页面会出现，如图 5-4 所示。

## FIGURE 5-4
MyDSL 扩展信息面板。

![](img/af53325d7f38f1cdafca9f44568e4ab8_126_0.png)

非常重要的一点是，始终查看 Comments 部分，以查看是否需要在安装此软件包之前安装任何先决条件软件包。在本例中，不需要其他软件包。

此时，您可以点击 Cancel 按钮并继续浏览 UCI 仓库。但为了继续本示例，让我们继续下载。点击 Download 按钮开始下载和安装过程。

## Application Download Dialog Box

接下来，会显示一个对话框，要求输入应用程序将被下载到的目录。该目录必须存在于您的系统上，并且用户 dsl 必须具有写入权限。通常希望使用默认的 /tmp 目录来保存扩展程序（见图 5-5）。

文件将下载到此目录中，并将使用 md5 校验和文件进行完整性验证。如果出现另一条消息框，指示下载失败，您需要重试。

点击 Download 按钮继续。

## FIGURE 5-5
选择扩展将被下载到的目录。

![](img/af53325d7f38f1cdafca9f44568e4ab8_126_1.png)

## Viewing Application Download Status

进度条显示下载状态（见图 5-6）。进度条在达到 100% 时消失。

![](img/af53325d7f38f1cdafca9f44568e4ab8_127_0.png)

**FIGURE 5-6** 随着下载进行，观察应用程序下载状态。

使用 Extension 工具下载也意味着程序将被自动安装。这是安装扩展的首选方式，因为您不仅仅是为以后使用而下载它们。当扩展成功下载后，Extension 工具会安装并设置所选应用程序、菜单，通常还有桌面图标。Extension 工具还会对下载的扩展进行校验和，以确保下载良好。如果下载损坏，会弹出消息通知您，以便您可以重试。

## Launching Newly Installed Application

扩展下载并安装后，返回桌面并调出系统菜单。并非所有，但大多数应用程序都会在它们的 MyDSL 部分下列出菜单项。一些系统应用程序不需要菜单即可启动，例如 GNU 工具集合。图 5-7 显示我们的新游戏列在菜单的 MyDSL 部分下。

![](img/af53325d7f38f1cdafca9f44568e4ab8_127_1.png)

**FIGURE 5-7** 安装 Xmahjongg 后，MyDSL 菜单上会出现一个新条目。

选择 Xmahjongg 菜单项以启动应用程序。另请注意，许多 MyDSL 扩展会自动提供桌面图标。图 5-8 显示了 Xmahjongg 桌面图标。

![](img/af53325d7f38f1cdafca9f44568e4ab8_127_2.png)

**FIGURE 5-8** Xmahjongg 图标被添加到您的桌面以启动应用程序。

当扩展提供桌面图标时，只需点击即可启动应用程序。还请记住右键单击图标以查看是否还有其他应用程序选项可用。图 5-9 显示了 Xmahjongg 应用程序成功启动。

## Accessing Locally Stored Extensions with the MyDSL Extension Tool

存储在本地硬盘或U盘上的 MyDSL 扩展也可以使用 Extension 工具进行安装。Load Local 按钮打开一个文件浏览器，您可以使用它来定位并从任何已挂载的磁盘安装扩展。图 5-10 显示了此 Load Local MyDSL Extension 窗口。

## FIGURE 5-9

Xmahjongg 应用程序的成功启动。

![](img/af53325d7f38f1cdafca9f44568e4ab8_128_0.png)

## FIGURE 5-10

从本地磁盘查找并选择扩展以在 DSL 中安装。

![](img/af53325d7f38f1cdafca9f44568e4ab8_128_1.png)

文件浏览器的使用就像任何典型的文件浏览器一样。当然，任何物理设备必须在显示任何文件之前先挂载。在前面的图中，我显示驱动器 hda2 已挂载在 /mnt 目录上，我已导航到相同的 UCI 集合。只是现在这是访问我的本地驱动器。在这种情况下，使用本地扩展浏览器不需要访问互联网。

