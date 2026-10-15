
# 第 10 章 — 使用 Icecast 2.79 运行网络广播电台

## 第 2 步：设置音频输入或列表

### 配置声卡

`Icecast` 源客户端在稍后描述中可以通过 `OSS` 或 `ALSA` 系统传输音频。在启动计算机时，声卡应该被检测到并配置。输入：

```bash
# lspci -vvv | grep -i audio
```

如果声卡无法工作，可以在 `ALSA` 项目（`www.alsa.org`）中找到信息。如果你的声卡运行正常，你需要使用如 `amixer` 等应用程序来更改电平。

请查看第 5 章获取有关 `amix` 的使用信息

### 设置列表

`Icecast` 源客户端可以从列表将 `Ogg Vorbis` 流到 `Icecast`。如果歌曲在 `Ogg Vorbis` 中包含了元数据，信息将随音频文件一起传输。这样，连接到你 `Icecast` 服务器的音频播放器就可以显示艺术家歌曲。

原始 Linux 包含一个 `Ogg Vorbis` 格式的播放机项目。存储的歌曲包含元数据。

如果你感兴趣查看 `Ogg Vorbis` 音频文件中包含的元数据，可以使用带有 `vorbis-tools` 软件包的 `vorbiscomment` 工具。这里有一个例子：

```bash
# vorbiscomment -l "01-My_Song.ogg"

TITLE=My Music Song
ARTIST=Chris Negus
TRACKNUMBER=1
TRACKTOTAL=18
ALBUM=Greatest Open Source Hits
GENRE=Classical
```

使用 `vorbiscomment` 工具，你还可以附加或修改 `Ogg Vorbis` 文件的注释。要获取 `Ogg Vorbis` 文件的其他信息（例如比特率和播放时间），你可以使用 `ogginfo` 命令。

## 第 3 步：将音频流到 Icecast

随着 `Icecast` 服务器的运行，你现在可以将流媒体内容引导到不同的工具（称为源客户端）。`Icecast` 项目本身提供了带有 `Ice2` 的 `icesream` 音频命令（用于从列表或输入流音频）。然而，你也可以使用其他工具。为了提供可用源客户端工具的良好交叉，本步骤描述了如何从以下位置输送音频源：

- Linux 系统上的播放列表 `IceS2`
- Linux 系统上使用 `Muse`（`http://muse.dyne.org`）的声卡
- Windows 系统上使用 `Oddcast` `Winamp` 插件（`www.oddsock.org/tools/oddcastv3`）的麦克风

### 从播放列表提供音频 (`IceS2`)

要使用 `ices` 命令和播放列表来提供音频，你需要编辑 `ices-playlist.xml` 文件。创建一个目录来存放你的播放列表，并按如下方式复制 `ices-playlist.xml` 文件：

```bash
# mkdir $HOME/myces
# cd $HOME/myces
# cp /usr/share/doc/ices-* /ices-playlist.xml $HOME/myces/
```

### 启动 Icecast

注意，在此操作中，我将 `icecast` 目录的所有者更改为了 `nobody`。如果你是以另一个用户运行 `Icecast`，你应该将 `icecast` 目录的所有者更改为该用户。

**4. 启动 `Icecast`。** 在示例中，不要直接以 `root` 用户身份运行 `Icecast` 服务器，而是以 `icecast` 用户身份运行。当你以 `root` 或或其他用户启动 `icecast` 时，这会自动发生：以非 `root` 用户运行 `Icecast` 的原因在于，如果 `Icecast` 服务被利用，执行利用的人将获得计算机的完全访问权限。

作为 `root` 启动 `icecast` 服务器，这将导致它以名为 `icecast` 的用户运行。

```
/usr/bin/icecast -c /etc/icecast.xml
```

此命令为用户 `nobody` 打开一个 `bash` 终端，并使用 `icecast.xml` 配置文件执行 `icecast` 命令。（如果你之前创建了用于运行 `icecast` 的用户账户，只需在此过程中将该用户替换为 `nobody` 即可。）

**5. 检查 `icecast` 是否正在运行。** 如果 `Icecast` 无法启动，你将收到一条错误消息，且 `icecast` 进程将退出。回到你的 `icecast.xml` 文件并尝试调试该问题。如果 `Icecast` 看起来似乎正在运行，请通过 `Firefox` 或或其他浏览器打开以下位置来检查它：

```
http://localhost:8000/admin/stats.xml
```

当提示时，输入用户名 `admin` 以及你早些添加到 `icecast.xml` 文件中的关联密码。（作为替代方案，你只需输入 `http://localhost:8000` 即可查看显示信息较少的基本状态页，但不需要验证。）如果出现了 `Icecast` 状态页（如图 10-2 所示），则服务器运行正常。

![Icecast 状态页](img/1b8a24a162893627b8005ac678b79236_300_0.png)

**10-2:** 如果你看到 `Icecast` 页面，说明 `Icecast` 服务器正在运行。

**6. 远程检查 `Icecast`。** 接下来，你想检查你的 `Icecast` 服务器是否可以从网络访问。如果你的计算机连接到局域网（`LAN`），你可以尝试从局域网上的另一台计算机上打开 `Icecast` 状态页。否则，如果你的 `Icecast` 服务器连接到互联网，你可以尝试从互联网上的任何计算机进行测试。

使用你的 `icecast` 服务器的 `IP` 地址或主机名，在可以访问你服务器的计算机的任何 Web 浏览器地址栏中输入 `Icecast` 状态页的地址。例如：

```
http://10.0.0.3:8000/admin/stats.xsl
```

这显示了 `Icecast` 服务器的一个私有 `IP` 地址（`10.0.0.3`）示例。如果你的计算机具有完全限定域名，`10.0.0.3` 可能会被替换为类似 `icecast.linuxto.net` 的内容。像你之前做一样，输入 `admin` 名称和密码来访问该页面。

如果你无法访问 `Icecast` 状态页，请按照检查任何机器可访问性的标准步骤进行操作。从另一台计算机，检查你是否可以 `ping` 通该机器（`ping 10.0.0.3`）。如果可以，请确保你的防火墙已配置为允许访问 `8000` 端口。

**7. 添加音频内容进行测试。** 为了测试客户端是否可以从你的 `Icecast` 服务器播放内容，你可以简单将一个支持格式的文件（我建议使用 `Ogg Vorbis` 格式）复制到服务器的 Web 目录中。例如，从服务器上的目录复制 `test.ogg` 文件以便在 `Icecast` 客户端上访问，输入以下命令：

```bash
# cp test.ogg /usr/share/icecast/web
```

要播放你刚刚添加到 `Icecast` 服务器上的内容，你可以从“第 5 步：听你的广播电台”中描述的任何音频播放器输入以下 `URL`：

```
http://10.0.0.3:8000/test.ogg
```

如果一切顺利，你的 `Icecast` 服务器应该已经准备好开始接收到互联网或其他网络的音频流。下一步是设置带有你将要流向 `Icecast` 服务器的内容源。
