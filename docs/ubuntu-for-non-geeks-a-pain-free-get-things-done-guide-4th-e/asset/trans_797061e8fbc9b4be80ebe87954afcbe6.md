

## 3A-8: 在面板上移动项目

好吧，现在你已经在本章中向面板添加了所有要添加的内容。它现在看起来可能有点杂乱，所以让我们通过移动项目来做一些整理。你会尝试在主题上将它们 somewhat 分组，以便更容易处理。

幸运的是，你可以非常轻松地移动面板启动器，只需右键单击相关启动器，从弹出菜单中选择 Move，然后将启动器拖到你想要放置的位置。启动器到达你想要的位置后，单击一次启动器，它就会停留在那里。

为了练习这种移动操作，让我们将你添加的启动器、菜单和抽屉移动并按以下顺序从左到右放置：Applications、Places、System、Firefox、Help、OpenOffice.org Writer、OpenOffice.org Calc、Sound & Video、Games、Drawer。将剩余的启动器放在面板的右侧，位于 Network Manager applet 或任何自动出现的其他项目左侧，按以下从左到右的顺序放置：Eyes、Wanda (Fish)、Force Quit。最后，将 Run Application applet 单独放置在两个启动器集群中间。当你完成所有更改后，你的面板应该看起来与图 3-13 中的我的面板几乎一样。

![](img/f7cef0df22f9dba5a41777808c98eece_74_0.png)

图 3-13：带有新启动器的 GNOME 面板

## 更多面板乐趣

除了你在项目 3A 中完成的基本自定义之外，你还可以做很多事情来改变面板的外观和感觉。当然，你可以通过右键单击相关项目然后在弹出菜单中选择 Remove From Panel 来删除任何启动器、抽屉或菜单，但还有更多选项。大多数这些选项可以通过右键单击面板中的任何空白区域然后选择 Properties 来获得，这将打开面板属性窗口。

从此窗口你可以更改面板的位置、调整其大小、更改其颜色或使其透明——非常酷。你还可以设置面板在不使用时自动消失，并在将鼠标光标移入面板通常所在区域时重新出现。不要害怕尝试——这就是乐趣的一半！

## 项目 3B：操作菜单

现在你已经了解了可以用面板做一些很酷且有用的事情，让我们继续讨论菜单的话题。GNOME 的一个非常好的功能是它允许你编辑其菜单。你可以添加启动器、删除项目、移动项目，甚至更改菜单中出现的图标。总的来说，你对事物有很大的控制权，但对于本项目，你将把工作限制在两个领域：更改图标和移动菜单项。

### 3B-1：更改菜单中的图标

正如你毫无疑问记得的那样，你添加到面板中的 OpenOffice.org Writer 和 Calc 启动器存在的一个问题是它们共享相当相似的图标。如果你选择 Applications ▸ Office，你会看到各种 OpenOffice.org 模块的图标，虽然不相同，但也有些相似。为了改善这种情况，你将把这些图标更改为你在项目 3A-4 中为两个面板启动器使用的同一套图标。在这种情况下，只需按照以下步骤操作：

- 1. 右键单击 Applications 菜单并选择 Edit Menus，或转到 System 菜单并选择 Preferences ▸ Main Menu。
- 2. 在随后出现的菜单编辑器窗口中（图 3-14），在左侧窗格中单击 Office。那个菜单的内容将随后出现在右侧窗格中。
- 3. 在窗口的右侧窗格中，单击 OpenOffice.org Word Processor 一次，然后单击 Properties 按钮。然后将出现一个 Launcher Properties 窗口。
- 4. 在该窗口的 Name 框中，首先将启动器的名称缩短为 Writer 或 Word Processor 或适合你的任何名称。
- 5. 接下来，单击 Icon 按钮（它上面没有写 Icon，而是显示 Writer 图标）。使用“项目 3A-4：更改面板启动器图标”第 33 页中描述的方法，导航到 /usr/share/icons/hicolor/48x48/apps 中的 Choose an icon 窗口。
- 6. 向下滚动到并单击 openofficeorg3-writer.png，然后单击 Open。
- 7. 新图标现在应该出现在 Launcher Properties 窗口中。单击 Close，你将能够在菜单编辑器窗口中看到更改。
- 8. 对 OpenOffice.org Spreadsheet 甚至 OpenOffice.org Presentation 重复该过程，如果你喜欢的话。只需确保为每个项目选择合适的名称并选择合适的图标（例如 Spreadsheet 使用 openofficeorg3-calc.png，Presentation 使用 openofficeorg3-impress.png）。完成后，将编辑器窗口保持打开状态以继续项目 3B-2 的工作。

