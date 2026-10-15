
在 `ices` 启动之后，播放列表（`/home/chris/myces/playlist.txt`）被读取，列表中的第一首歌应该开始播放（来自`/usr/local/share/music/Chris-Album`目录的`10-Lots_Of_Rain.ogg`）。音频流被定向到 Icecast 服务的计算机网络接口（`10.0.0.3:8000`），名称为`myplaylist.ogg`。你还可以看到所选的编码数据（2通道，44100 Hz，标称 64000）。

如果你没有看到像示例这样的消息，你可能需要检查`ices-playlist.xml`文件中的设置，或者找出 Icecast 服务器是否正常运行并能够接受连接。

如果你对从播放列表流音频的配置满意，可以跳转到“第 4 步：制作你的网络电台”或“第 5 步：收听你的网络电台”。要创建实时音频流，请继续下一节。

## 实时提供音频

多流引擎 (MuSE) 提供了命令行和图形界面，用于配置到你的 Icecast 服务器的音频流传输。使用`MuSE`，你可以从声卡以及多达六个编码后的音频流中获取输入。输出可以定向到 Icecast 服务器。从那里，它可以通过互联网进行流式传输。

以下步骤提供了一个使用`MuSE`（图形模式）从声卡将音频流到你的 Icecast 服务器的示例。使用`MuSE`，你还可以将额外的流合并到一个输出中发送到你的 Icecast 服务器。

1. **启动 `MuSE`。** 要在图形 (gtk) 模式启动`MuSE`，输入以下命令：

   ```
   # muse -g gtk2
   ```

   出现`MuSE`窗口。然后你可以选择麦克风图标，让`MuSE`从设置为捕捉音频的声卡设备获取输入。

2. **准备传输。** 从`MuSE`窗口中选择插头图标 (Lets Stream) 并选择 Ogg/Vorbis Streaming 标签。`MuSE Add Server`窗口与主`MuSE`窗口一起出现，如图 10-3 所示。

   ![](img/1b8a24a162893627b8005ac678b79236_306_0.png)

   图 10-3：从`MuSE`窗口配置 Icecast 信息。

## 第 10 章 — 使用 Icecast 2 运行互联网广播电台

3. **创建 Icecast 配置。** 填入许多你在配置 Icecast2 时输入过的相同信息。在本示例中，你需要的关键信息包括：

   - **主机/端口（Host/port）。** 输入运行 Icecast 服务器的计算机的 IP 地址和端口号（很可能是 `8000`）。

   - **识别挂载点（Identify a mount point）。** 这是给音频播放器进入以播放流时使用的流名称。

   - **名称/URL/描述（Name/URL/Descriptions）。** 为流添加名称和描述，以及任何你希望与流关联的 URL。在这种情况下，URL 是已建立的网站的 URL，而不是流流的 URL。

   - **登录类型/密码（Login type/password）。** 我们在这里正在使用 Icecast 2 服务器。你需要输入与 Icecast 服务器关联的源密码，以便能够将此音频流连接到它上。

4. **连接。** 点击 Icecast 配置窗口上的按钮。在`Muse`主窗口上，你应该能看到类似`starting on http://10.0.0.7:8000`的消息。

5. **测试连接。** 从另一台计算机，你可以使用支持 Icecast 的任何播放器测试流是否正常工作。在 Linux 系统上，你可以输入以下内容连接到你创建的流：

   ```
   $ egg123 http://10.0.0.7:8000/live.ogg
   ```

## 从 Windows 传输音频

你的 Icecast 服务器可能运行在德克萨斯州的托管服务上，而你正坐在威斯星州某人的系统上。别担心。如果你有到服务器的网络连接，你可以使用 Oddcast 媒体工具从 Windows 系统传输音频内容到 Icecast 服务器。

以下是在`Winamp`中使用`Oddcast`插件通过麦克风广播到 Windows 系统的步骤：

1. **下载`Winamp`。** 在 Windows 系统上下载并安装`Winamp`。你可以从`.winamp.com`获取。

2. **下载`Oddcast`。** 从`Oddcast`网站(`www.oddcast.org/tools/oddcast3`)下载并安装`Oddcast` `Winamp`插件（至少版本 3）。

3. **启动`Winamp`。** 从 Windows 系统的开始菜单启动`Winamp`。

4. **配置`Oddcast`。** 要配置`Oddcast`，从`Winamp`窗口中选择`Options -> Preferences`。在出现的`Oddcast`配置窗口中，右键点击`Encoder Settings`框中的`Vorbis`条目并选择`Configure`。会出现一个配置窗口，如图 10-4 所示。

   ![](img/1b8a24a162893627b8005ac678b79236_308_0.png)

   图 10-4：在`Oddcast`配置窗口中配置 Icecast 设置。

5. **Icecast 设置。** 输入连接到你的 Icecast 服务器所需的设置。你应该能从上次配置 Icecast 时认这些设置。当设置成你想要的方式后，点击`OK`。

6. **开始录制。** 要开始录制，点击`Live Recording`中的麦克风图标，然后点击`Connect`按钮。音频立即开始流向你的 Icecast 服务器。

## 第 4 步：让你的广播电台公开

到目前为止，你已经有一个如`http://example.com:8000/live.ogg`这样的 URL 来代表你的互联网广播电台。有很多方法可以让你那些忠实的电台粉丝更容易访问该 URL。例如，你可以在 Icecast 流目录上广告你的服务器，或者你可以创建一个你自己的广播电台网站。

> 虽然“YP Directory”一词在 Icecast 配置文件中经常用于标识 Icecast 流目录，但在向使用流目录的人员标识这些目录之一时，始终使用“Stream Directory”一词。随着时间的推移，YP 术语预计将在配置文件中淘汰。

## 流目录 (Stream Directories)

Icecast 服务器可以在 Icecast 流目录中注册它们的音频流。这些目录允许人们从数百个互联网音频广播者中选择。默认情况下，你的 Icecast 音频流没有注册到任何流目录服务器。但你可以修复这个问题。

首先，你可以编辑`icecast.xml`文件，通过移除围绕目录列表项的`<!--`和`-->`字符来取消目录列表项，使它们出现在以下代码中。启用的目录条目将允许任何源客户端允许你的 Icecast 服务器上的流目录列表位于`Xiph.org`流目录和`odddock.org`流目录中：

```
<directory>

  <yp-url-timeout>15</yp-url-timeout>

  <yp-url>http://dir.xiph.org/cgi-bin/</yp-url>

</directory>

<directory>

  <yp-url-timeout>15</yp-url-timeout>

  <yp-url>http://www.oddsock.org/cgi-bin/</yp-url>

</directory>
```
