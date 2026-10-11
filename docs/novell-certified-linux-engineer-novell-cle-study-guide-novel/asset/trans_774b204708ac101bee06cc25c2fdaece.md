
在 Windows NT、2000 和 XP 中，可以安装打印机使其对系统上的所有本地用户可用，很像 Windows 9x 或 Me 系统。只有 Administrators 或 Power Users 组的成员才能创建此类型的打印机。

然而，在这些系统上，也可以配置打印机使其仅对安装它的本地用户可用。任何本地用户都可以创建此类型的打印机。

可以配置 iPrint 以支持任一种类型的打印机。这是通过编辑 NNLS 服务器上的 `/var/opt/novell/httpd/htdocs/ippdocs/iprint.ini` 文件来实现的，图 9.21 显示了该文件的一部分。

```
;DEFAULT = The installed name on client will
; Follow the full UNC/URL format:
; \\\\ipprint\\domain.com\\pa_name
;YOURNAME = This is any name you want to show
; for the installed printer’s UNC server name.
; Use only lower ASCII characters;
; DO NOT USE slash, quote, space, or comma.
; The new installed printer name format is:
; \\\\YOURNAME\\pa_name
AllowUserPrinters = 0
;Printer Installation Profile
;
;Terminal/Citrix Server clients
; These settings will be ignored!
; Instead, you must configure this on the
; Terminal/Citrix server (must have rights
; to see the tab and administer it).
; Start->Programs->Novell iPrint->Print Client
;
Settings:
;
;Windows clients
```

![](img/c7771e8540507f2b00c088c7a411b57b_434_0.png)

在图 9.21 中，请注意 `AllowUserPrinters` 参数。该参数用于定义 iPrint 在 Windows 系统中安装的打印机是如何实现的。如果该参数设置为 0（这是默认值），则只有属于 Administrators 或 Power Users 组的本地用户才能安装 iPrint 打印机。在这种情况下，安装的 iPrint 打印机可供系统中所有本地用户访问。

如果该参数设置为 1，则属于 Administrators 或 Power Users 组的本地用户可以像在设置为 0 时那样为系统中所有用户安装 iPrint 打印机。但是，如果本地用户不属于这两个组中的任何一个，他或她只能为他或她自己的用户账户安装 iPrint 打印机。在这种情况下，打印机仅对该用户可用，其他本地用户将看不到该打印机。

如果该参数设置为 2，则所有用户只能为他们自己的本地用户账户安装 iPrint 打印机。即使是 Administrators 或 Power Users 组中的用户也只能为他们自己安装 iPrint 打印机。

如前所述，这些参数对 Windows 95、98 和 Me 工作站没有影响。

配置此文件的最佳方式取决于您的组织标准。有些组织会指示只为单个 Windows 用户创建 iPrint 打印机。其他组织可能不会那么严格。当完成此文件的配置后，您就准备好完成最后一项 iPrint 配置任务：创建打印机位置地图。

## 创建基于位置的打印机地图

可以配置 iPrint 以两种方式显示与 iPrint 服务器关联的 Printer Agents。第一种方式称为列表视图。如图 9.22 所示，当使用 Internet Explorer 访问位于 `http://your_server_IP_address/ipp` 的 iPrint 网页时，会显示已配置打印机的简单列表。这是您的 iPrint 服务器的默认视图。

![](img/c7771e8540507f2b00c088c7a411b57b_435_0.png)

这种显示效果不错，但对我来说似乎相当乏味。您可能已经注意到，在这一章中我多次提到您可以配置 iPrint 来显示带有打印机图标的办公室地图，用户可以利用这些图标来访问打印机。

这是显示 iPrint 系统中 Printer Agents 的第二种方式。在我看来，这是最好的方式。它为用户提供了一种选择想要打印的打印机的简单方法。iPrint 附带了 iPrint 地图设计器，这是一个简单的基于 Web 的工具，您可以使用它为您的组织创建自定义地图。

为此，您需要一台安装了 Internet Explorer 5.5 和 iPrint 客户端的 Windows 工作站。您还需要办公室楼层平面图的一个图形文件（BMP、GIF 或 JPEG 格式）。如果您只是想进行实验，NNLS 在 `/var/opt/novell/httpd/htdocs/ippdocs/images/maps` 目录中包含几个示例地图。我们将稍后在本章的练习中使用这些示例地图。

一旦您的工作站和地图图像文件准备就绪，您可以通过执行以下操作来配置基于位置的打印地图：

- 1. 在您的 Windows 工作站上，将驱动器映射到 NNLS 服务器上的 Samba 共享。
- 2. 将您的地图图像文件复制到 iPrint 服务器上的 `/var/opt/novell/httpd/htdocs/ippdocs/images/maps` 目录。
- 3. 在您的 Windows 工作站上，打开 Internet Explorer 并导航到 `http://your_server_IP_address/ippdocs/maptool.htm`。执行此操作时，会出现图 9.23 中的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_436_0.png)

**图 9.23**
iPrint 地图设计器。

- 4. 在左侧框架中，向下滚动到 **Background**（背景）下拉列表。该下拉列表会根据您在步骤 2 中复制到 `maps` 目录的地图图像文件动态填充。
- 5. 在 **Background**（背景）下拉列表中，选择一个背景图像文件。地图将被设置为页面背景，如图 9.24 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_436_1.png)

**图 9.24**
向地图设计器添加地图图像文件。

- 6. 向上滚动回到 **Printer icon**（打印机图标）下拉列表。
- 7. 在 **Printer icon**（打印机图标）下拉列表中，选择最匹配您物理打印机的打印机图标。
- 8. 将打印机图标拖到背景地图上物理打印机所在的位置。图标将被放置在地图上并框在一个蓝色正方形中，如图 9.25 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_437_0.png)

- 9. 单击您刚刚放置在地图上的打印机图标。
- 10. 在 **Printer List**（打印机列表）下拉列表中，选择要与此图标关联的 Printer Agent。
- 11. 向下滚动到 **Printer Agent** 部分。请注意，打印机 URL 会自动为您填充。
- 12. 在 **Mouse Over Text**（鼠标悬停文本）字段中，输入您希望当用户在 Windows 工作站上将鼠标光标悬停在打印机图标上时出现的文本。
- 13. 在 **Printer Caption**（打印机标题）字段中，输入打印机的标题。
- 14. 在地图上方，选择 **Driver Settings**（驱动程序设置）。会出现图 9.26 中的对话框。

![](img/c7771e8540507f2b00c088c7a411b57b_437_1.png)

- 15. 配置打印机的默认设置，然后单击 **OK**（确定）。
- 16. 在顶部框架中，单击 **Save**（保存）。
- 17. 使用您选择的一个文件名，将文件保存到映射到 NNLS 服务器上 Samba 共享的驱动器。
- 18. 关闭浏览器窗口。
- 19. 在您的服务器上，将文件从您的 Windows 工作站复制到 NNLS 服务器上的 `/var/opt/novell/http/htdocs/ippdocs` 目录。

至此，iPrint 系统已准备好！现在我们讨论如何在 Windows 工作站上安装 iPrint 打印机。

## 在 Windows 工作站上配置 iPrint 打印机

### 覆盖的测试目标：

- 1. 使用 iPrint 打印。

安装了 iPrint 客户端，配置了 Driver Store，实现了 iPrint Manager，配置了 Printer Agents，并创建了 iPrint 地图后，您就准备好开始在客户端 Windows 工作站上配置 iPrint 打印机了。

这是通过使用您创建并复制到 iPrint 服务器的地图 HTML 文件来完成的。要访问此地图并安装其中包含的打印机，您需要执行以下操作：

> **警告**
> 这些步骤是使用 Windows XP Professional 编写的。如果您的组织使用不同版本的 Windows，步骤可能略有不同。

- 1. 验证您的 Windows 工作站上已安装 iPrint 客户端。为此，您可以执行以下操作：
    - a. 选择 **Start, Control Panel, Add or Remove Programs**（开始、控制面板、添加/删除程序）。
    - b. 验证已安装程序列表中显示了 Novell iPrint 客户端，如图 9.27 所示。
    - c. 关闭 **Add or Remove Programs**（添加/删除程序）和 **Control Panel**（控制面板）窗口。

