

让我们来验证一下我们的理论，并执行上一条命令手动安装 KeePassXC。安装完成后，重新打开 Pop! Shop 并点击“已安装”选项卡。如果你向下滚动，应该能在已安装的应用程序和服务列表中找到 KeePassXC。点击该项目，注意屏幕的变化。Ubuntu（deb）选项现在确认该应用已安装，并提供了一个按钮选项来卸载它。下图显示了我的结果。

![](img/451a8c416cafc58e46802d06b4bc7b1a_25_0.png)

这并不意味着我总是更倾向于使用 Apt 安装而非 Flatpak。在这种场景下，选择这种方式是最优的，因为需要另一个应用程序（Firefox）才能连接到该程序。通过终端手动安装排除了 Pop! Shop 版本可能受到污染的风险。由于这是一个敏感应用程序，我希望仔细审查任何安装和更新选项。当我们执行本章末尾介绍的每周命令时，该应用程序将会被更新。

让我们对 Bitwarden 进行重复操作。在 Pop! Shop 中搜索 Bitwarden 只提供了一个安装选项，但并没有告诉我太多关于它的信息。Bitwarden 官网没有提及 Flatpak，而在线搜索告诉我 Flatpak 中的 Bitwarden 版本并非官方发布。虽然这个版本可能没有恶意意图，但我希望密码管理器直接来自官方来源。

与 KeePassXC 不同，对于 Bitwarden，我更倾向于 AppImage 安装方式。这是因为你可以从他们的网站下载官方应用程序，并且它可以自动获取更新，无需任何软件仓库。然而，存在一个新问题。Pop! OS 处理 AppImage 的默认方式会导致许多程序无法打开。下载、修改权限并执行后，很可能什么都不会发生。这就是为什么我更喜欢另一种名为 AppImageLauncher 的 AppImage 管理器。我在终端中执行了以下操作。

```bash
sudo add-apt-repository ppa:appimagelauncher-team/stable -y
sudo apt update
sudo apt install appimagelauncher -y
```

现在 AppImageLauncher 已安装，我们只需双击任何 AppImage 文件即可，包括直接从 Bitwarden 官网下载的程序。执行此操作时，你应该看到一个新的窗口，默认选项是可以接受的。首次通过此新应用程序启动 AppImage 时，系统会提示将 AppImageLauncher 集成到你的系统中。我选择了“集成并运行”。现在你应该会在应用程序菜单中看到嵌入的任何 AppImage 程序，并且可以右键点击这些条目来卸载它们或将它们固定到你的 Dock 中。我们现在可以在 Pop! Shop 中搜索 Bitwarden 来检查我们的工作。下图显示了我的结果。即使我已经安装并运行了该程序，Pop! Shop 仍只提供安装 Bitwarden 的选项。这就是我们知道我们没有安装 Flatpak 版本的原因。

![](img/451a8c416cafc58e46802d06b4bc7b1a_26_0.png)

你是否感到困惑？我知道第一次接触 Linux 时这可能会显得令人不知所措。我的软件安装策略很简单。我在网络浏览器中搜索任何敏感程序，访问该应用程序的官方网站，并根据其推荐确定官方的软件安装方式。如果可以提供 “deb” 或 “apt” 解决方案，我通常会更倾向于这样，以便将程序整合到我的系统中。如果官方网站和 Pop! Shop 上只有 Flatpak 选项，并且我确信该应用程序可以在完全隔离的环境中运行，那么我会安装该选项。如果自动更新程序的唯一方式是使用官方 AppImage 文件，我会复制我们刚才完成的教程。在接下来的指南其余部分中，我们将有更多的练习机会。

## 日历与联系人

Pop! OS 拥有默认的日历和联系人应用程序，可以从 Dock 中的“显示应用程序”图标访问。默认情况下，在这些程序中输入的任何数据都会存储在本地加密驱动器中。如果你只需要在 Linux 设备上使用日历和联系人，这些选项应该效果很好。然而，本地存储的数据可能不足以满足你的需求。大多数人希望跨多个设备同步其日历事件和联系人数据，尤其是与他们的手机同步。你有两个安全选项来实现这一点。

如果你使用 Proton Mail、Tutanota 或 Skiff Mail 作为你的电子邮件，所有存储的联系人和日历条目都经过端到端加密以保护你的隐私（Proton Mail 不对姓名和电子邮件地址进行加密，以便其系统正常运行，但电话号码和备注受到保护）。这将允许你在网络浏览器和移动设备电子邮件应用中看到你的数据。然而，这些服务均无法将你的数据同步到标准的 Linux 日历和联系人应用程序（或移动等效应用）。在移动设备上，这意味着电话应用和活动通知无法访问这些数据。为了完全的安全同步，我们需要 EteSync。

EteSync (etesync.com) 是一项提供端到端加密日历、联系人和笔记数据的服务。每月 $2，他们会在服务器上以安全方式存储你的数据，使其无法访问你的任何数据。然后你可以将 EteSync Bridge 软件下载到你的 Linux 机器和移动设备上。该软件将你的加密 EteSync 数据连接到任何日历或联系人应用程序。在这些应用中所做的任何更改都会立即反映在 EteSync 数据中。然后你可以将此数据与其他设备（如智能手机）同步。一次性设置可能会有些麻烦，但应无需重复。如果你想在 Linux 中使用能够安全同步到其他设备的传统日历和联系人应用程序，EteSync 是最佳选择。让我们安装它。

首先，在 https://pim.etesync.com/signup 创建一个免费试用账户。这允许一周内无限制访问。建立服务凭据后，登录你的账户并创建新的日历和地址簿。标题可以随意命名，然后导航至 https://github.com/etesync/etesync-dav/releases/latest 并下载标题为 "linux-amd64-etesync-dav" 的文件。获取文件后，在终端中执行以下操作。

```bash
cd Downloads
chmod +x linux-amd64-etesync-dav
./linux-amd64-etesync-dav
```

这应该会启动你的浏览器并跳转到一个接受你免费试用 EteSync 凭据的页面。你需要“添加”你的账户，然后使用相同的信息登录。现在你已经与 EteSync 服务器同步。

接下来，你需要一个应用程序来连接你的新安全 EteSync 账户并以可查看的形式同步数据。为此，我更喜欢 Thunderbird。Thunderbird 是一个集电子邮件、日历和联系人于一体的一体化解决方案，我们将用它完成几项任务。按以下步骤安装和配置它。

- 打开 Pop! Shop 并搜索 "Thunderbird"。
- 点击条目以查看应用程序详情。
- 将 Flatpak 安装选项更改为 "Pop! OS (deb)"。
- 点击 "安装"。
- 启动 Thunderbird 并取消任何向导或欢迎窗口。
- 如果提示，选择暂时不使用电子邮件使用 thunderbird 的选项。
- 点击左侧菜单中的日历图标，然后点击 "Calendar" 旁边的 "+"。
- 选择 "On the Network" 并点击 "Next"。
- 输入你的 EteSync 用户名。
- 返回浏览器中 http://localhost:37358/web 页面。
- 点击 "Collection Lists" 链接。
- 右键点击你的日历链接并选择 "Copy link"。
- 返回 Thunderbird 并将此链接粘贴到位置字段中。
- 点击 "Find Calendars"，并在提示时提供你的 EteSync 密码。
- 点击 "OK" 并允许连接完成。
- 识别出日历后，点击 "Subscribe"。

让我们测试所有内容。打开你的浏览器并导航到 https://pim.etesync.com。登录你的账户并点击日历选项卡。在今日日期中创建一个新条目，标签为 "Test"。现在打开 Thunderbird 并确保你在日历部分。你应该看到你的 EteSync 日历以及 "Home" 默认日历。下图显示了我自己的结果。如图所示，我的 Thunderbird 日历显示了新条目。如果你的没有显示，请右键点击你的 EteSync 日历并选择 "Synchronize Calendars"。

