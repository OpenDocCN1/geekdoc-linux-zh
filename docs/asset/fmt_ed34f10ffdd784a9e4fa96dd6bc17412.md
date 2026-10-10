
# 第 9 章：使用互联网和 Web 379

- DjVu 插件 (`djvu.sourceforge.net`) — 使用 DjVu 图像压缩技术显示图像。此插件供 AT&T 使用。
- Macedia Flash Player (`www.macromedia.com`) — 显示多媒体矢量图形和动画。此插件来自 Macromedia, Inc。Fedora 适用于 Flash Player，但 Macromedia Shockwave 插件在 Linux 上不可可用。
- MPlayer 插件 (`http://mplayerplugin.sourceforge.net`) — 此插件实现了流行的 `mplayer` 视频播放器，用于将视频内容嵌入到浏览器窗口中。该插件的 RPM 软件包 (`mplayerplugin`) 可从 `http://rpm.livna.org` 获取。有关使用 `rpm.livna` 的更多信息，请参阅第 5 章。
- Java 运行时环境 (`java-1.7.0-icedtea`) —— 为了能够在浏览器中播放 Java 和 JavaScript 内容，你需要一个提供与 Sun Microsystems 提供的 Java Runtime Environment Web 插件（`http://java.com/en/download/index.jsp`）相同功能的插件。Fedora 项目没有使用 Sun 的专有代码，而是通过结合 OpenJDK 项目和 IcedTea 项目的软件添加了一个完全免费的对应版本（`http://fedoraproject.org/wiki/Features/IcedTea`）。

要使插件生效，请重启 Firefox 并在内容位置输入 `about:plugins`。你将看到 GCJ 浏览器插件处理的 Java 内容列表。你也可以尝试其他包含 Java内容的网站来测试你的 Java 插件。例如，你可以访问 Java.com 测试页面：

```
http://java.com/en/help/testvm.xml
```

如果你无法看到 Java 内容，请打开软件包更新（Package Updater）窗口并查找更新后的 `usnpluginwrapper` 包。安装该包并重启 Firefox 浏览器应该就能让你看到 Java 内容。

要使插件生效，请重启 Firefox 并在内容位置输入 `about:plugins`。你将看到由 GCJ 浏览器插件处理的 Java 内容列表。

> 注意：如果你担心 IcedTea 目前的实验性性质，在 Fedora 中还有其他方法可以让 Java 运行时环境插件工作。你可以从 `d.wers.com` Fedora 存储库获取可用软件的 RPM 软件包。其他人从 `www.jppackage.org` 获取软件也取得了成功。过去，我曾直接从 `sun.com` 获取包并使其运行，但发现在最新的 Fedora 版本中运行变得更加困难。由于 Linux 中运行的 Java 运行时环境软件是一个不断变化的目标，因此你可能想要构建自己的 RPM（参见 `.fedorafaq.org/#java`）。

- CrossOver 插件 (`www.codeavers.com`) — 某些最有趣且流行的插件没有 Linux 插件。QuickTime 5、Shockwave Director 多媒体内容以及各种 Microsoft 电影、文件和数据格式将无法在 Firefox 中播放。CodeWeavers 在基于 x86 的处理器上使用使用为 WINE for Linux 构建的软件创建了 CrossOver 插件。虽然它不再作为单独独立产品提供（你必须花费 39.95 美元购买 Crossover Office），

## 第二部分：使用 Fedora 或 RHEL

CrossOver 插件让你能够运行某些在 Linux 中无法 otherwise使用的内容。（从 `www.codewavers.com/site/products/download_trial` 下载演示版。）

安装 CrossOver 插件后，你将看到一个友好的插件设置窗口，让你能够选择性地为 QuickTime、Windows Media Player、Shockwave、Flash、iTunes 和 Lotus Notes，以及 Microsoft Word、Excel 和 PowerPoint 查看器安装插件。在你阅读此内容时，可能已经提供了对这些内容格式后续版本的支持。你还可以安装其他多媒体插件，以及用于这些插件的各种字体。

对于某些插件，系统会提示你想要将插件放在何处。你可以选择将其安装为供系统上的所有用户可用，或仅供当前用户可用。要仅为当前用户添加插件，请将其放置在 `~/.mozilla/plugins` 目录中。要让系统中所有运行 Firefox 的用户都能使用插件，请将插件放在 `/usr/lib/firefox-*plugins` 目录中。

> 注意：当 Firefox 没有分配插件来处理特定数据类型时，会弹出一个窗口请求你使用桌面环境的默认应用程序来处理数据。GNOME 的 `/usr/share/applications/defaults.list` 文件定义了系统的默认应用程序。对于你自己的桌面，可以按照以下方法更改打开特定文件类型的默认设置：打开 Nautilus 文件管理器，右键点击任何你想要更改类型的文件；选择“属性”（Properties）；选择“打开”（Open）选项卡；从列表中选择你想要用于该文件类型的应用程序。如果你想要添加的应用程序不在列表中，点击“添加到列表”。

虽然可以使用插件来选择某些特定类型的内容，但扩展（extensions）可以用于为浏览器本身添加功能。

## 添加扩展

要扩展 Firefox 以处理由 Fedora 或 RHEL 交付的内容，请从 Mozilla Firefox 产品页面（`www.mozilla.org/products/firefox`）开始。从那里，通过链接进入 Firefox 扩展。以下是 Mozilla.org 提供的一些最流行的 Firefox 扩展：

> 注意：某些 Firefox 扩展已知会导致 Firefox 出现性能问题，例如消耗过多内存。如果你发现 Firefox 性能不佳，请关闭所有 Firefox 窗口，然后在终端中输入以下命令从安全模式下重启 Firefox：

```
firefox -safe-mode
```

参阅：`http://kb.mozillazine.org/Safe_Mode` 了解更多关于使用安全模式调试 firefox 问题的信息。

- 下载工具 (`FlashGot`) — 如果你想从浏览器浏览器下载组文件，`FlashGot` 是一个非常实用的工具。安装 `FlashGot` 后，你可以选择下载单个文件、通过高亮网页上的链接来识别的文件，或从当前网页链接的所有文件。这还是一个构建功能，可以让你识别一个范围的文件名进行一次下载。安装 `FlashGot` 后，你可以通过选择工具 -> `FlashGot` 并从菜单中选择功能来自 Firefox 它。在 Fedora 中，`FlashGot` 将请求传递给 `kGet` 以完成下载。你可以获取 `wget` 等其他下载工具代替 `kGet`。
- 选择性拦截广告 (`Adblock`) — 使用 `Adblock`，你可以选择性地防止在你访问的网页上显示广告。安装 `Adblock` 后，`Adblock` 会出现在 Firefox 的右下角。点击该按钮可以看到一个包含当前页面上你想拦截的项目的窗口。右键点击图像并选择拦截图像，可以使用星号拦截来自特定网站的内容（例如 `www.example.com/*`）。通过工具 -> 设置打开 `Adblock` 偏好来查看、编辑或删除被拦截的网站。对于 Firefox 1.5 或更高版本，你应该使用 `Adblock`。
- 访问 FTP 服务器 (`Firefox`) — 包含一个在 Firefox 中运行的实用客户端程序。还有一个从工具栏访问 FTP 的 Firefox 插件
- 拦截 Flash 动画 (`Flashblock`) — 防止 Flash 动画在你的浏览器窗口中播放。这对于不想在访问的站点尝试播放内容时影响性能的拨号用户来说可能特别有用。
- 改进标签页浏览 (`Tabbrowser Preferences`) — 虽然 Firefox 已经提供了一些在 Firefox 窗口中打开多个页面的标签功能，但 `Tabbrowser Preferences` 更进一步。选择编辑 -> 设置 -> 标签页浏览。标签页选择可以精炼标签的工作方式（例如悬停而非点击）、将标签放在顶部内部或选择是否在新标签页中加载主页
- 关注你的天气 (`ForecastFox`) — 有了 `ForecastFox`，点击 Firefox 即可获取地区的最新天气。安装 `ForecastFox` 并重启 Firefox 后，会弹出一个窗口让你配置 `ForecastFox` 选项。至少选择查找代码，以选择你想关注天气的区域。保存选项后，天气图标将出现在 Firefox 的右下角。将鼠标悬停在上方可以查看当前天气的快速视图。双击图标可以从 `www.weather.com` 显示更详细的天气预报。

# 第二部分：使用 Fedora 和 RHEL
