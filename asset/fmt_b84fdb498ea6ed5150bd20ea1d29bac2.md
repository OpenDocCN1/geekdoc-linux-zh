
- 如果需要，允许使用相同的Linux密码进行驱动器加密。这更方便，但可能存在安全风险。如果你想要额外的保护层，可以为驱动器加密和Linux分别指定唯一密码，但这对大多数用户来说可能过于繁琐。我对两个选项使用相同的密码。

- 允许过程完成并点击“Restart Device”。

当计算机重新启动时，应该会显示一个屏幕，要求你用密码解锁加密磁盘。这是Pop!_OS默认的底层保护。同样的保护也可以在安装Ubuntu或其他系统时配置。解锁驱动器只是允许访问它。然后你应该看到Pop!_OS的用户选择和密码输入屏幕。这会解锁你的Pop!_OS版本并启动机器。按照以下步骤继续完成一次性设置。

- 选择你的布局选项并点击“Next”。
- 选择你的顶栏选项并点击“Next”。
- 点击两次“Next”以继续通过菜单。
- 选择你期望的外观并点击“Next”。
- 选择你的Wi-Fi（如果可用），提供密码并点击“Next”。
- 保持位置服务禁用并点击“Next”。
- 选择你期望的时区并点击“Next”。
- 点击“Skip”以跳过任何在线账户，然后点击“Start Using Pop!_OS”。

有些人对每次启动都需要输入两次相同密码感到烦恼。我不介意，但我尊重关于冗余性的疑问。如果你知道解密驱动器的密码，我认为如果禁用登录Pop!_OS的次要密码，并不会带来巨大的安全问题。这可以通过以下步骤完成，且随时可以撤销，但请注意我稍后将给出的警告。

- 启动位于Dock右下角的设置应用程序。
- 在左侧菜单中选择“Users”。
- 点击“Unlock”并输入你的密码。
- 启用“Automatic Login”开关。
- 关闭设置，点击左上角菜单栏并选择“Power Off / Log Out” > “Restart” > “Restart”来重启计算机。

现在你应该只需输入解密密码即可。一旦通过该屏幕，Pop!_OS应该正常启动。**我想强调这是可选的。** 如果你为解密和登录选择了不同的唯一密码，你不应该启用自动登录。由于Linux密钥环的解锁方式，这也可能导致某些程序比手动输入密码时更频繁地要求你输入密码。始终根据你的需求确定便利性和安全性之间的适当平衡。启用自动登录不会抹去账户密码，或在需要密码时降低安全性，但它可能比每次启动都输入密码带来不便，而后者是我所做的。

Pop!_OS默认比Ubuntu更注重隐私，但我仍然喜欢做一些修改。我在每次新安装后进行以下操作。

- 启动位于Dock右下角的设置应用程序。
- 点击左侧菜单中的“Bluetooth”并禁用开关。
- 点击左侧菜单中的“Privacy”并禁用“Connectivity Checking”。
- 点击“File History & Trash”并禁用所有选项。

虽然以下内容与隐私或安全无关，但我认为这些修改增强了我对Linux的使用体验。你的偏好可能不同。

- 点击“Screen”并将“Blank Screen Delay”更改为较长的时间段。
- 返回主屏幕，点击左侧菜单中的“Power”并禁用“Automatic Screen Brightness”和“Dim Screen”。
- 点击“Automatic Suspend”并禁用所有选项。
- 启用“Show Battery Percentage”。

与Ubuntu类似，Pop!_OS提供许多图像用作我们的背景壁纸。在桌面上右键点击会显示一个菜单，其中有“Change Background”选项。然而，我更喜欢没有图像的纯色背景。与Ubuntu类似，Pop!_OS没有提供将背景更改为纯色的菜单选项。让我们修复这个问题。以下Terminal命令完全移除背景图像，在桌面上留下纯蓝色背景。你可以从Dock底部的黑色图标启动Terminal。

```
gsettings set org.gnome.desktop.background picture-uri ''
```

这更好了，但我更喜欢稍微柔和的蓝色，我用以下Terminal命令更改它。这个命令和本章中的其他命令应该作为单个命令在一行内执行。你的PDF查看器可能会拆分行，你需要将每个命令中的所有移动同一行。

```
gsettings set org.gnome.desktop.background primary-color 'rgb(66, 81, 100)'
```

你可以更改数字以创建适合你桌面的完美颜色。https://www.w3schools.com/colors/colors_rgb.asp 网站应能提供帮助。

我喜欢的下一个修改是将Dock从底部移动到左侧，使用以下Terminal命令。

```
gsettings set org.gnome.shell.extensions.dash-to-dock dock-position LEFT
```

接下来，我更喜欢缩小图标的默认大小，因为我很快将添加许多程序。你可以使用以下Terminal命令将数字更改为适合你屏幕大小的任何大小。

```
gsettings set org.gnome.shell.extensions.dash-to-dock dash-max-icon-size 30
```

当你右键点击文件或文件夹以删除它时，你目前有一个“Move to Trash”选项。以下Terminal命令在Trash条目下方添加一个新的标题为“Delete Permanently”选项。这允许我完全绕过Trash，直接消除任何期望的内容。

```
gsettings set org.gnome.nautilus.preferences show-delete-permanently true
```

默认情况下，大多数Linux操作系统隐藏“hidden”文件。这些通常是系统文件，但也可能包括我们需要访问的缓存和配置文件。因此，我执行以下两个Terminal命令，以便随时使这些有价值的文件可见。

```
gsettings set org.gnome.nautilus.preferences show-hidden-files true
gsettings set org.gtk.Settings.FileChooser show-hidden true
```

你可能有待处理的操作系统更新，现在应该应用它们。

- 点击Dock栏中设置旁边的“Pop!_Shop”图标。
- 点击“Installed”标签页，然后点击“Update All”。

一旦我们开始安装应用程序，你将在这个菜单中看到额外的更新选项。我通常每周至少启动一次Pop!_Shop以应用所有更新。

虽然你可能会受到诱惑开始安装你期望的所有应用程序，但请稍等。下一章将讨论防火墙，它能帮助我们屏蔽来自设备的非必要传出流量。这是保护隐私和安全的关键步骤。

# 第四章：DNS 配置

只要你为任何设备启用互联网连接，系统就会开始向各种服务器发送信息。这可能包括无害的数据，例如检查更新、时间同步或检索待处理的消息。

虽然大多数 Linux 操作系统不会像微软和苹果那样发送侵入性的遥测数据，但第三方应用程序可能会这样做。我们信任的许多应用实际上正在我们背后发送关于我们的使用信息。我的目标是提供能够减少或消除这种暴露的选项。我们可以通过使用第三方 DNS 服务来实现这一点。

如果你读过我的 macOS 指南，你会知道该章节侧重于使用软件防火墙而非 DNS。虽然 Linux 上存在一个名为 Open Snitch 的防火墙应用程序，但我目前不推荐它。它长期以来都存在相当多的错误，并且在 Ubuntu 或 Pop!_OS 中运行时，每次启动该应用程序都需要调整执行方式才能正常工作。虽然我坚持认为 macOS 设备需要软件防火墙，但我并不认为 Linux 有必要这样做。我在 macOS 上使用 Little Snitch 的主要目的是阻断与 Apple 的连接。Linux 并不存在这些问题。然而，我认为我们确实需要某种形式的内容过滤。

首先，我们应该理解域名系统（DNS）的性质。DNS 可能是一个令人望而生畏的主题。用最基本和简单的解释来说，DNS 将域名（如 inteltechniques.com）转换为 IP 地址，以定位适当的内容。在典型配置中，你的家庭或移动互联网服务提供商（ISP）会在没有你参与的情况下静默处理你的 DNS 查询。换句话说，无论你是否使用 SSL 加密，你的 ISP 都知道你访问过的每一个网站域名，并且知道你的计费详情。如果你不是匿名购买互联网或蜂窝服务的，那么他们也知道你的身份。ISP 通过这种方式收集大量有关你的有价值信息，并经常将这些详细信息出售用于营销目的。我要阻止这种行为。

默认情况下，你的 Linux 设备依赖于你所连接的网络提供的 DNS 服务。这可能是你的家庭 Wi-Fi 或蜂窝提供商的服务。你可以选择为设备生成的所有查询指定不同的 DNS 服务器。我为所有客户的桌面设备和手机都实施了 NextDNS（nextdns.io）服务。
