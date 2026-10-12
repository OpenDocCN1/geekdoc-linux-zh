
另参

- > 关于符号链接和使用 `ln` 命令的更多信息，请参第 46 页。
- 要了解更多关于 shell 环境变量的信息，请参第 100 页。

# 使用 Netscape Communicator

Netscape Communicator 有近三十种不同的命令行选项。与大多数良好的 X11 客户端一样，该程序还支持若干 X11 工具包选项，例如几何形状设置。例如，如果你想要较小的窗口，请指定几何设置。

## 从命令行启动 Netscape

1. 使用 Navigator 的 `--help` 查看支持的命令行选项列表：
```
# netscape --help
```
如果列表对你的终端来说太大，请将标准输出重定向到文件：
```
# netscape --help > netscape.options
```
`netscape.options` 文件包含 `--help` 的输出。

2. 要使用特定的窗口大小启动 Netscape，请使用 X11 工具包 `-geometry`，后跟水平和垂直像素的窗口大小：
```
# netscape -geometry 600x400
```

## 设置 Navigator 偏好

1. 设置 Navigator 的偏好，将光标移动到“编辑”（Edit）菜单并选择“偏好”（Preferences）项。出现对话框，如图 19.5 所示。

2. 要配置 Communicator 启动特定组件，选择“外观”（Appearance）设置下的组件之一。要配置 Communicator 组件栏的外观，选择“工具栏”（Toolbar Bar）设置。

3. 点击“字体”（Fonts）或“颜色”（Colors）设置，自定义菜单字体大小以及 Communicator 使用的背景或前景颜色。

304

4. Netscape 的大部分行为可以在 Navigator 偏好设置中修改。将鼠标光标移动到类别列表下的 Navigator 项目（如图 19.6 所示）。点击 Navigator 项目。出现 Navigator 设置，如图 19.6 所示。

5. 选择 Communicator 启动方式、默认主页以及缓存或历史记录设置的偏好。然后将鼠标光标移动到类别列表下的 Navigator 项目。点击 Navigator 单词左侧的小三角形。偏好对话框将列出“语言”（Languages）和“应用程序”（Applications）菜单项。点击“应用程序”菜单项，Navigator 偏好对话框将发生如图 19.7 所示的变化。

305

# 第四部分 连接到您的互联网服务提供商

# 第19章 使用网页浏览器

| 类别 | 应用程序 | 描述 | 处理方式 |
| --- | --- | --- | --- |
| 外观 | | | xterm -e limit %H %p |
| 颜色 | xterm3270 application | xterm -e -#3270 n |
| 导航器 | login | | xterm -e login %n |
| 语言 | | 用用户登录 | xterm -e login %n -I %n|
| 邮件与群组 | | 插件帮助详情 | |
| 组合器 | application/form-id | 未知提示用户 |
| 高级 | RealAudio | rplayer |
| | Unix 手册页 | 未知提示用户 |
| | TROFF 文档 | 未知提示用户 |
| | TROFF Forward | 默认 |

图 19.7
Navigator应用程序设置用于为外部程序或插件（如 RealPlayer）添加支持。

Netscape Communicator 支持插件，即可以为浏览器添加功能的额外程序。其中之一是名为 `rplayer` 的 RealPlayer 插件，你可以用它通过互联网听音频或视频广播（当你点击网页上的音频或视频链接时，音频或视频将自动播放）。

## 为 Netscape 安装互联网视频支持

1. 若要支持 RealPlayer 插件，请继续上一步步骤并滚动应用程序列表。选择 RealAudio 应用程序，然后用左鼠标点击 Edit（编辑）按钮。出现一个对话框，如图 19.8 所示。

另请

- > 若要了解更多关于 Linux 的多媒体工具，请参阅第 15 章，“使用图形和多媒体工具”。

2. 将文件名扩展名 `.rm` 添加到列表中，编辑 Handled by Application（应用程序）字段为 `realplay %s`，然后点击 OK（确定）按钮。再次点击 OK 按钮退出并保存你的 Navigator 选项。

![](img/b916e6553833e904f268fdbef0cc11e9_326_0.png)

图 19.8
使用 Navigator 编辑对话框为 RealPlayer 添加特定支持。

- 若要测试 `rvplayer` 插件，请确保它已安装在你的系统中（在 `/usr/local/RealPlayerG2` 目录下查看 `realplay` 程序），然后使用 Navigator 读取你硬盘上的 `rvplayer` 示例视频：
```
# netscape file:/usr/local/RealPlayerG2/audiosig.rm
```
当 Navigator 显示初始窗口后，RealPlayer 将启动并播放一段短的音乐和视频片段，如图 19.9 所示。

要获取 Linux 的最新 RealPlayer 应用程序，请访问：
http://www.real.com/products/player/linux.html

有关使用 Communicator 辅助程序的更多信息，请访问：
http://home.netscape.com

![](img/b916e6553833e904f268fdbef0cc11e9_327_0.png)

图 19.9
当你使用 Netscape Navigator 时，RealPlayer 插件会在你的上网会期间播放音频和视频片段。

# 第20章 使用 telnet 和互联网中继聊天 (IRC)

## 使用 telnet 命令

- 与互联网中继聊天聊天

`telnet` 命令用于登录互联网上的远程计算机。使用 `telnet` 登录（通常需要用户名和密码），并运行程序、查看文件或下载数据。`telnet` 命令在命令行中使用，后跟主机名（或远程计算机系统的名称）以启动 `telnet` 会话。

例如，要连接到美国环保保护局（它在多个远程计算机系统上运行开放信息服务），请如下使用 `telnet` 命令：

```
# telnet tnbbs.rtpnc.epa.gov
```
