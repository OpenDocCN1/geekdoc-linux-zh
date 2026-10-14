

在 Screen 部分，添加以下行：

```
BlankTime 5
SuspendTime 10
OffTime 15
```

BlankTime 是 X Window System 在空闲多少分钟后将屏幕变空白的时间。SuspendTime 是在空闲多少分钟后将显示器置于挂起模式的时间。最后，OffTime 是在空闲多少分钟后将显示器关闭的时间。

/etc/XF86Config 文件通常包含不止一个 screen 部分。如果你不确定应该将行添加到哪一个，就将它们全部添加进去。如果你使用 SaX 来设置你的 X Window，你会发现只有两个 screen 部分。

### Theme Manager
要完全改变你的 KDE 外观，你可以使用主题。KDE 主题可以改变窗口边框、颜色等等。SuSE Linux 附带了相当数量的 KDE 主题，当你点击桌面分支中的 Theme 节点时，这些主题会出现在主题列表中（见图 24.15）。如果你点击一个主题，主题的预览会出现在预览窗口中，并在其下方显示简短描述。你可以使用 Contents 选项卡来自定义要应用于所选主题的主题内容。在你选择了主题和要应用的内容之后，点击 Apply 来测试你的设置，或点击 OK 来在不测试的情况下使用该主题。你可以通过从主题列表中选择 Default 并在 Contents 选项卡上选择所有内容来恢复默认 KDE 主题。

FIGURE 24.15
你可以使用 KDE Theme Manager 轻松更改你的 KDE 主题。

![](img/659f91d9da7b29976c0625e2e9628511_489_0.png)

### Languages
KDE 支持多种语言，KDE 程序员来自许多国家。这就是为什么 KDE 程序有许多翻译的原因。在某些情况下，程序可能只提供少数语言的翻译。你可以通过选择第一种语言作为首选语言来设置你的语言偏好。如果程序不支持你的默认语言，KDE 将尝试为你的第二种首选语言找到翻译。第三种首选语言也是如此。你可以通过从三个组合框中选择它们或将它们保持在默认设置（即英语）来自定义你的语言偏好。

## Screensaver
Screensaver 节点用于配置屏幕保护程序的设置。你可以从 Screensavers 列表中选择要使用的屏幕保护程序。在你选择屏幕保护程序后，屏幕保护程序的预览会出现在预览监视器中。你可以通过点击 Screensaver 列表下方的 Setup 按钮来配置所选屏幕保护程序的设置（见图 24.16）。或者，你可以通过点击 Test 来测试你的屏幕保护程序设置。

FIGURE 24.16
你可以通过点击预览监视器的角落来配置你的屏幕保护程序使其处于活动状态。

![](img/659f91d9da7b29976c0625e2e9628511_490_0.png)

屏幕保护程序的常规设置如下：

- **Wait for—** 此字段设置屏幕保护程序启动前的延迟。
- **Require password—** 如果你勾选此复选框，屏幕保护程序启动后你必须输入密码。
- **Show password as stars—** 如果你必须输入密码，因为你的屏幕保护程序需要密码或你已锁定屏幕，如果启用此复选框，密码将以星号显示。
- **Priority—** 此滑块用于指示屏幕保护程序对系统的优先级。屏幕保护程序在高优先级下看起来会很好，但其他进程通常更重要。我们建议你将其设置为最小值。

Screensavers 节点中的预览监视器不仅用于预览所选屏幕保护程序，你还可以使用它来设置屏幕的角落，以便在该角落调用屏幕保护程序或立即锁定屏幕。如果你使用鼠标左键点击其中一个角落，会出现一个弹出菜单，其中包含以下值：

- **Ignore**— 如果你将鼠标指针移动到此角落，什么也不会发生。
- **Save screen**— 如果你将鼠标指针移动到此角落，屏幕保护程序将启动。
- **Lock screen**— 如果你将鼠标指针移动到此角落，屏幕将被锁定。
- **Style**— 此节点使你能够配置小部件的外观、非 KDE 应用程序的样式以及面板图标样式。
- **Draw widgets of the style of Window 95**— Qt 小部件可以使用 Windows 95 样式或 Motif 样式。将此复选框设置为你偏好的小部件集。KDE 1.1.x 使用 Qt 1.42+ 库，仅支持 Motif 和 Windows 95 的外观和感觉。然而，KDE 2.0 使用 Qt 2.0 库，使你能够将主题应用于小部件。KDE 2.0 将完全可主题化。
- **Menubar on top of the screen in the style of MacOS**— 此选项在屏幕顶部放置一个菜单。如果你习惯了 MacOS，你会觉得这个选项很熟悉。
- **Apply fonts and colors to non-KDE applications**— KDE 将尝试使非 KDE 应用程序尽可能与 KDE 应用程序相似。

图标样式使你能够更改在 Panel、KFM 和 Other 中使用的图标大小。通过选择相应的复选框将大小更改为你喜欢的设置。

## Information
在此分支中，你可以获取有关系统中已安装和正在工作的设备的的信息。此分支中的大部分信息都从 /proc 文件系统读取。使用此分支查询有关你的设备、系统内存、Samba 状态等的信息。

## Input Devices
KDE 使你能够控制系统输入设备的行为。此分支中的输入设备包括 International Keyboard、Joystick、Keyboard 和 Mouse。未来肯定会添加更多设备，但目前只有这些。每个节点的说明如下：

International Keyboard— 此节点使你能够将语言更改为你的母语（见图 24.17）。点击 Add 会出现可用语言的列表。选择你想要添加的语言，然后点击 OK。你可以通过点击 Up 和 Down 按钮来排列列表中的语言。

在 StartUp 选项卡中，将 International Keyboard 设置为 Autostart，以确保下次启动 KDE 时它会自动启动。你可以使其作为 dock 图标图标化，以便快速访问它。

FIGURE 24.17
要本地化你的 KDE，请使用 International Keyboard 快速从一种语言更改为另一种语言的设置。这也将适用于你的 KDE 应用程序的语言。

![](img/659f91d9da7b29976c0625e2e9628511_492_0.png)

- **Joystick**— 此节点使你能够校准你的 Joystick 轴。如果存在，它将加载 Joystick 驱动程序。
- **Keyboard**— 此节点使你能够设置你的键盘自动重复和按键点击音量。
- **Mouse**— 在此节点中，你可以配置鼠标设置。你可以使用滑块设置鼠标加速和鼠标阈值。在你设置鼠标速度设置后，你可以通过勾选 Right Handed 或 Left Handed 复选框来按你的喜好交换鼠标按钮。

## Keys
你可以使用此分支将 KDE 附带的键组合默认值更改为你的偏好。你还可以定义新的组合来执行某些 KDE 特定操作、启动程序或向正在运行的程序发送信号：

- **Global keys**— 这些是 KDE 桌面管理特定的键绑定（见图 24.18）。你可以根据自己的喜好修改它们。例如，如果你有一个 Microsoft Natural Keyboard 或兼容键盘，你可能希望将 Windows 键分配为打开 K 菜单而不是 Alt+F1。为此，请执行以下步骤：
  1. 从 Action 列表中选择 Pop-up System Menu。
  2. 点击 Custom Key 单选按钮。
  3. 取消选中 Shift、Ctrl 和 Alt 复选框。
  4. 点击键形按钮以激活它并按下键盘上的 Windows 键。键文本将根据你按下的 Windows 键更改为 Super_L 或 Super_R。

FIGURE 24.18
KDE 全局键用于创建将在 Windows 管理中使用的键组合。

![](img/659f91d9da7b29976c0625e2e9628511_493_0.png)

KHotKeys— 此节点使你能够配置 KHotKeys 程序设置（见图 24.19）。你可以使用 KHotKeys 运行程序或向正在运行的程序发送信号。点击 Add Action 创建新条目并编辑按下热键时要执行的操作的设置。

FIGURE 24.19
使用 KHotKeys，你可以创建启动你喜欢的程序的快捷方式。

![](img/659f91d9da7b29976c0625e2e9628511_493_1.png)

