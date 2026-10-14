
Files moved into the Trash remain there until you empty the Trash. If you haven’t emptied the Trash since you moved a file there, you can get it back. The Trash is just a special folder for holding documents you are about to delete. You can open it as you do other folders by clicking on it. To rescue a file, just click it and move it out of the Trash.

## Emptying the Trash

As the amount of trash grows, you might wish to empty it to regain the disk space consumed by trashed files. To empty the Trash, right-click its icon and choose Empty Trash Bin from the menu that is displayed (see the following figure).

![](img/edf072a03d4de1f8f4a13465ac79e7fb_66_0.png)

To empty the Trash, right-click the Trash Bin icon and choose Empty Trash Bin from the resulting menu.

要访问内容，请单击章节和节标题。

## 完全傻瓜的 Linux 使用指南

（出版商：Macmillan Computer Publishing）

作者：Manuel Ricart

ISBN：078971826x

出版日期：12/22/98

搜索本书：

### 文件属性

创建文件或文件夹后，你执行的大多数操作将以重命名或更改权限的形式进行。KFM 通过在其图标上右键单击为上一节中描述的一些操作提供了快捷方式。上下文菜单将弹出以显示多个选项（见下图）。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_67_0.png)

KFM 上下文菜单在你右键单击文件或文件夹时显示各种选项。

上下文菜单中的命令取决于你单击的内容——因此得名。

- Open with—显示一个面板，你可以在其中输入要用于打开所选文件的应用程序的名称。
- Up—向上导航一个目录。
- Back—导航到上一个目录。
- Forward—如果你使用 Back 来到达此目录，可以使用 Forward 返回到上一个位置。
- Cd—将当前窗口聚焦到所选目录。
- New View—在新的 KFM 窗口中打开目录。
- Copy—将文件或目录复制到剪贴板。然后你可以使用 Paste 命令将复制的文件或目录放置在当前目录中。
- Move To Trash—将所选文件或目录移动到名为 Trash 的特殊目录。这会将文件从当前位置移除，但不会删除它们。
- Delete—删除所选项目。
- Add To Bookmarks—将所选文件夹添加到你的书签列表中。
- Properties—弹出一个面板，允许你检查和更改有关文件的信息，例如其权限设置和名称。

### 重命名文件或文件夹

要重命名文件或文件夹，请右键单击该文件或文件夹并从显示的菜单中选择 Properties。这将显示一个面板，允许你重命名文件（见下图）。

重命名文件时，请注意不要更改文件的扩展名（如果有）。文件扩展名由文件名末尾的句点后跟的三个或更多字符组成。扩展名将文件与应用程序关联起来。

有很多东西你不应该重命名。你主目录中的所有内容都是你的，可以随意重命名。但是，Linux 根目录或其他系统相关区域中的文件应保持不变。大多数用户无需担心；一般来说，除非你在超级用户（root）账户下工作，否则 Linux 不会允许你更改不应更改的任何内容。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_68_0.png)

General 选项卡显示有关文件的通用信息，例如其名称和路径。要重命名文件或文件夹，请在名称文本字段中输入新名称并按 Enter。

### 设置文件和文件夹权限

Properties 面板还允许你修改和设置创建的文件和文件夹的权限设置。权限在第 16 章“Permissions: Protecting and Sharing Your Work”中有详细说明。如果你觉得需要控制权限，我建议你先阅读本章以了解更改设置的影响，因为权限是一个高级主题。本节解释如何使用 KFM 更改权限，并假设你了解这些影响。

权限允许你保护文件和文件夹免受其他用户的访问。默认情况下，你创建的文件会分配一组权限。在使用 KDE 时，你可以使用图形控件更改文件权限。要进入权限面板，请右键单击文件或文件夹并从出现的菜单中选择 Properties。然后选择 Permissions 选项卡（见下图）。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_69_0.png)

Permissions 选项卡显示用于设置文件或文件夹权限的多个控件。每个设置都为文件的所有者（User）、分配给文件的组的成员（Group）以及其他人（Others）重复。通过设置值，你可以为不同用户控制不同级别的访问。

权限可以在 Permissions 选项卡中以多种方式更改：

- User 行设置目录所有者的权限。
- Group 行设置组成员的权限。
- Others 行设置既不是所有者也不是组成员的用户权限。
- Owner 字段显示拥有该文件的用户名称。
- Group 选择菜单显示分配给此文件的组名称。如果你是文件所有者并且属于多个组，则会显示选择菜单。
- Show Entries 列允许用户查看目录内容。
- Write Entries 列允许用户向目录添加或删除文件。
- Change Info 列允许用户遍历目录。
- Special 列启用特殊设置

面板的外观会根据你操作的是文件还是文件夹而略有不同。如果你操作的是文件，权限列将称为 Read、Write 和 Execute 权限。否则，它们将称为 Show Entries（Read）、Write Entries（Write）或 Change Into（Execute）。尽管标签不同，但其功能完全相同。

#### Techno Talk：每个权限控件的作用

每个文件与用户在一种或多种角色相关（见下图）：

- 用户可以是文件的所有者
- 用户可以是被授予文件权限的组的成员
- 用户既不是所有者也不是组的成员

这些角色中的每一个都可能具有 Read、Write 或 Execute 权限，或其组合。

对文件或文件夹的 Read 权限允许你查看（读取）其内容。

对文件或文件夹的 Write 权限允许你更改其内容。对于文件夹而言，这可能意味着你有权向目录添加文件。

Execute 权限是特殊的。当设置在文件上时，表示该文件是一个程序。如果你的角色具有 Execute 权限，你就可以运行该程序。对于目录，Execute 权限还控制谁可以进入目录。如果你打算将文件复制到目录中，你的角色必须对该目录具有 Execute 权限。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_70_0.png)

### 理解权限面板。

在前述的 Permissions Panel 图中，用户（文件所有者）具有 Read 和 Write 权限；分配给文件的组的成员具有 Read 和 Write 权限；其他用户能够读取文件，但由于缺乏写权限而无法修改它。

如果权限设置被选中，则表示已启用。权限只能由文件所有者或超级用户（root）分配。

除非你知道自己在做什么，否则不要更改文件或文件夹的权限。例如，如果你删除文件夹的 Change Into 设置（Execute 权限），你将使任何用户都无法导航或打开该文件夹中的文件。

+ Previous | Table of Contents | Next

### 更改文件或文件夹的组

如果你与一组其他用户协作进行项目，你可能希望授予他们访问一组文件和文件夹的权限。当你创建文件或文件夹时，它们会自动分配给你的默认组。如果你是其他组的成员，你可以重新分配对文件和文件夹的不同组访问权限。

要更改文件或文件夹的组成员身份，请右键单击它并选择 Properties；然后从显示的面板中选择 Permissions 选项卡。

要更改文件的组，请单击组选择菜单以显示你所属的组并选择你想要的组（见下图）。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_71_0.png)

如果你属于多个组，你可以为你的文件分配不同的组。

### KDE 模板

KDE 提供了一个有用的功能：Templates。模板允许你创建原型文档和文件夹结构，以便轻松重复使用和自定义。
