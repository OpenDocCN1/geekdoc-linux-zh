

虽然看起来你已经覆盖了大部分网页视频的基础，但你可能会对实际结果感到失望。例如，虽然 Totem 被列为支持流行的 WMV 和 MOV 视频格式，但不仅仅是这样。

如果你还记得本章前面“Video Formats”部分的内容，播放一个视频文件需要两件软件。Firefox 包含用于播放各种视频类型的插件，但这些软件包还必须包含适当的编解码程序来播放特定的视频格式。

正如你可能猜到的那样，Ubuntu 不包含用于播放专有和许可视频文件的编解码器。这意味着 Ubuntu 不支持许多流行的互联网视频文件格式。

## Adding Plug-ins

Firefox 浏览器有大量免费的视频相关插件可用。Firefox 插件的集散地是 http://plugindoc.mozdev.org（Firefox 网络浏览器基于 Mozilla 开源浏览器）。去该网站看看所有可用的视频插件吧。

Mozilla 插件网站上列出的许多插件都作为软件包在 Ubuntu 仓库中提供。你可以使用第 13 章“Software Installs and Upgrades”中所示的技术来安装新的插件。

在查看你的插件列表时，你可能会注意到一种流行的视频格式缺失：Macromedia Flash（也称为 Shockwave Flash）。这种视频格式在 YouTube 和 Metacafe 等视频流媒体网站上很受欢迎。如果你想使用这些网站，你需要在 Firefox 中安装 Flash。以下是使用 Ubuntu Synaptic Package Manager 安装它的步骤：

- 1. 通过从顶部面板选择 System ▸ Administration ▸ Synaptic Package Manager 打开 Synaptic Package Manager。有关如何使用 Synaptic Package Manager 的详细信息，请参阅第 13 章。
- 2. 单击工具栏中的 Search 按钮，在文本框中输入 mozilla plugin，然后单击 Search 按钮。搜索结果会出现在软件包管理器右侧的软件列表窗口中，如图 12-6 所示。
- 3. 扫描软件包列表并找到 flashplugin-nonfree 的条目。单击软件包复选框并从弹出菜单中选择 Mark for Installation 选项。软件包名称中的 nonfree 部分并不意味着你必须为其付费。它只是意味着它不是开源产品。Adobe 保留 Flash 插件的权利，但免费提供其使用。
- 4. 单击顶部工具栏中的 Apply 按钮。软件包管理器会显示一个对话框，确认你安装新软件包的决定。
- 5. 软件包管理器下载并安装插件文件，然后生成一个对话框，表明安装已完成。单击 Close 按钮退出安装。

当你从 Firefox 访问 about:plugins URL 时，你应该会看到你拥有 Shockwave Flash 插件，如图 12-7 所示。

### Figure 12-6: The Package Manager package list.

### Installed plugins

Find more information about browser plugins at plugins.mozilla.org. Help for installing plugins is available from pluginsdoc.mozilla.org

### Shockwave Flash

File name: libflashplayer.so
Shockwave Flash 10.0 r112

### Totem Web Browser Plugin 2.24.3

File name: totem-browser-plugin.so
The Totem 2.24.3 plugin handles video and audio streams.

### Figure 12-7: The Shockwave Flash plug-in appearing in the Firefox plug-in list.

你现在应该能够在 Firefox 网络浏览器中查看你所有喜欢的 Flash 格式视频了。

## More Video Support

如果你还记得第 8 章，Firefox 还支持一种称为 *extensions* 的功能。扩展是提供 Firefox 浏览器额外功能的小型应用程序。如果你正在寻找更多视频支持，或只是一些花哨的视频功能，有大量扩展可以帮助你。扩展的官方 Mozilla 网站是 `https://addons.update.mozilla.org`（请注意，这是一个 https 网站）。

我最喜欢的扩展之一是 Fast Video Download，它允许你下载网站上的嵌入式流媒体视频内容，例如 YouTube 或 MySpace，并将其下载到你计算机上的视频文件。以下是加载和安装它的步骤：

- 1. 通过选择 Applications ➔ Internet ➔ Firefox Web Browser 打开 Firefox。你也可以通过单击顶部面板上的 Firefox 地球图标启动 Firefox。
- 2. 前往 `https://addons.update.mozilla.org` 网站，并在所有附加组件页面中搜索 Fast Video Download。目前它位于 `https://addons.update.mozilla.org/en-US/firefox/addon/3590`。
- 3. 单击 Fast Video Download 网页上的 Add to Firefox 链接。由于 Fast Video Download 扩展未签名，会出现一个对话框询问你是否要安装它，如图 12-8 所示。

![](img/39e65eeb4f54001ede08c6114ae3cc6c_335_0.png)

**Figure 12-8:** Installing the Fast Video Download extension in Firefox.

