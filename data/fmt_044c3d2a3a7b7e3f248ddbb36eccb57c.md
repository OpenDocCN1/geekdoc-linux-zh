
以 `nobody` 用户运行服务器可以降低安全风险——入侵你的 Icecast2 服务器不会给黑客提供超级用户权限。

- 9. 移除 `<changeowner>` 参数之前和 `</changeowner>` 参数之后的注释：

```
<security>
  <chroot>0</chroot>

  <changeowner>
    <user>icecast</user>
    <group>icecast</group>
  </changeowner>

</security>
```

移除注释可使 `<user>` 和 `<group>` 指令生效，并强制 Icecast2 以用户和组 `nobody` 运行。如果你不移除注释，Icecast2 将以启动它的进程的用户和组身份运行。由于你以 `root` 身份登录，Icecast2 将以 `root` 用户身份运行。

![](img/41feae212f5c6612ff709354891f7b39_302_0.png)

以任何 `root` 权限运行任何服务都可能危及计算机的安全。

- 10. 点击“Save”（保存）按钮保存你的更改。

- 11. 通过选择 File → Quit（文件 → 退出）退出 Gedit。

你刚刚启动了多服务器，但还没有传输任何内容。现在处于静默状态。由于你不想触犯 FCC（联邦通信委员会），下一节将描述如何配置并启动 Ices2 服务器，以便向 Icecast2 服务器提供内容。

## 配置 Ices2

配置 Ices2 类似于配置 Icecast2。按照以下步骤配置 Ices2，然后向 Icecast2 提供音频流：

1. 运行以下命令打开 Gedit 文本编辑器：

`gedit /usr/local/etc/ices-playlist.xml`

Ices2 可以处理静态和实时音频流。`ices-live.xml` 配置文件用于处理实时流，而 `ices-playlist.xml` 则用于配置静态流。然而，提供实时流的内容超出了本书篇幅所能描述的范围，因此我们留给您去深入研究这一主题。

2. 将 `<logpath>` 指令更改为以下内容：

`<logpath>/var/log/icecast/</logpath>`

3. 修改 Ices2 以配合您刚刚提取的 Ogg 音频文件工作。找到 `<input>` 模块并修改文件参数，使其指向您新创建的播放列表文件：

```
<input>
    <module>playlist</module>
    <param name="type">basic</param>
    <param name="file">
        /usr/local/etc/playlist.txt
    </param>
    <param name="random">0</param>
    <param name="restart-after-reread">0</param>
    <param name="once">0</param>
</input>
```

`<input>` 和 `</input>` 分隔符告知 `ices2` 这些参数用于定义播放列表：

- `<module>`：这些分隔符定义了播放列表的边界。
- `Type`：此参数定义了您使用的播放列表类型。在此例中，它是基本系统。
- `File`：包含播放列表的文件名称在此处定义。
- `Random`：如果将此选项设置为 1，播放列表中的曲目将随机播放。
- `Once`：如果将此参数设置为 1，则告知 `ices2` 每首曲目仅播放一次。

4. 单击“保存”按钮以保存您的更改。

5. 选择“文件:: 退出”，Gedit 窗口将关闭。

Ices2 使用配置文件（在这种情况下，即*播放列表*）向 Icecast2 提供静态流。播放列表定义了 `ices2` 提供给 Icecast2 的音频文件。

![](img/41feae212f5c6612ff709354891f7b39_303_0.png)

Ices2 开始向您创建的 Ogg/Vorbis 文件所在的 Icecast2 服务器进行流式传输。您可以开始收听您的私人流媒体服务器了。我们在下一节中介绍具体操作方法。

## 将一切整合起来：向您的私有网络传输音乐

您可以使用 Rhythmbox 等多媒体播放器连接并收听音频流。以下步骤描述了如何操作（假设您仍以 Root 身份登录）：

1. **启动您的 Icecast2 服务器：**

`icecast -c /usr/local/etc/icecast.xml &`

2. **启动 Ices2 服务器：**

`ices /usr/local/etc/ices-playlist.xml &`

3. **启动 Rhythmbox 或 MPlayer 以播放流。例如，如下使用 MPlayer：**

`mplayer http://127.0.0.1:8000/example.ogg`。

就这样！您会听到从您的音乐 CD 中复制的任何音乐。

> **提示**
>
> 在尝试让 Ices2 正常工作期间，经常需要多次重启 Ices2。在这种情况下，您可能会占用 Ices2 和 Icecast2 用于通信的回环端口。在这种情况下，您会在 `/var/log/ices/ices.log` 文件中看到一个警告，指出它无法连接到端口 `127.0.0.1:8000`。您可以通过以 `root` 身份运行以下命令来解决该问题：`service network restart`。

使用 Icecast2 在您的 PC 上本地提供音乐流并没有什么好处。使用第 12 章中描述的 CD 播放机要简单得多。然而，当跨网络执行此操作时，收听您的多媒道流媒体服务器既有用又有趣。

## 在您的私有网络上进行流式传输

前一节描述了如何在您所在的计算机上广播音乐以及向该计算机广播。如果您已经创建了 Jukebox，现在是时候将 Jukebox 扩展为一个私有网络电台了。

以下步骤描述了如何配置您的 Icecast2 服务器以在您的私有网络上广播：

1. **以 root 身份登录**，通过点击 GNOME 菜单并选择“附件”：文本编辑器，打开 Gedit 文本编辑器。

2. 在 Gedit 窗口中，选择“文件”：打开。

3. 选择 `/usr/local/etc/icecast.xml` 并点击**确定**。

4. 将回环地址 `127.0.0.1` 更改为您 Icecast2 服务器的 IP 地址。

例如，如果您的服务器 IP 地址是 `192.168.1.1`，请按照此处所示修改文件；也要相应地更改主机名：

```xml
<hostname>cancun</hostname>
<!-- You can use these two if you only want a
single listener -->
<port>8000</port>
<bind-address>127.0.0.1</bind-address>

<!-- You may have multiple <listener> elements -->
<listen-socket>
  <port>8000</port>
  <bind-address>192.168.1.1
  </bind-address>
</listen-socket>
```

请注意，端口号保持不变。

5. 更改源密码，使其不同于默认值。否则，任何下载 Icecast2 包的人都可以确定您的密码：

```xml
<source-password>
  givememusic
</source-password>
```

6. **修改电子邮件和位置信息以匹配您的网络。**

此步骤可以让任何听众了解您是谁以及您来自哪里。

```xml
<location>Hi-Fi Paunchy</location>
<admin>olgoz@paunchy.net</admin>
```

7. 点击“保存”按钮以**保存您的更改**。

8. 在 Gedit 中打开 **Icecast2 配置文件** — `/usr/local/etc/ices-playlist.xml`。

## 理解 URL

您是否曾想过 URL 的各个部分意味着什么？使用诸如 `http://localhost:8000/track1.ogg` 这样的 URL 访问流媒体音频服务器，我们认为应该剖析这些部分各自的含义和功能。此列表描述了每个 URL 元素的功能：

- **协议**：Icecast2 使用超文本传输协议（HTTP）数据包来封装音频流。HTTP 是一个不错的选择，因为配置防火墙允许 HTTP 连接非常容易。
