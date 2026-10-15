
移除注释可使 `<user>` 和 `<group>` 指令生效，并强制 Icecast2 以用户和组 `nobody` 的身份运行。如果您不移除注释，Icecast2 将以启动它的进程的用户和组身份运行。由于您是以 `root` 身份登录的，因此在步骤 10 中启动时，Icecast2 将以 `root` 用户身份运行。以 `root` 身份运行服务可能会危及计算机的安全性。

- **10. 点击 `Save` 按钮保存您的更改。**

选择 `File→Quit`，Gedit 窗口将关闭。

- **11. 通过点击 GNOME 菜单并选择 `System Tools:: Terminal` 来打开终端模拟器窗口。**

- **12. 输入以下命令创建 Icecast2 日志文件目录：**

```bash
mkdir /var/log/icecast
```

- **13. 使用以下命令使 `nobody` 用户拥有新目录：**

```bash
chown nobody.nobody /var/log/icecast
```

- **14. 输入以下命令以启动 Icecast2 服务器：**

```bash
icecast -c /usr/local/etc/icecast.xml &
```

您刚刚启动了您的多媒体服务器，但尚未传输任何内容。现在处于静音状态。因为您不希望触犯 FCC，所以下一节将描述如何配置并启动 Ices2 服务器，以便您向 Icecast2 服务器提供内容。

### 配置 Ices2

配置 Ices2 与配置 Icecast2 类似。按照以下步骤配置 Ices2，然后向 Icecast2 提供音频流：

- **1. 打开 GNOME 终端窗口。**

- **2. 切换到 `/usr/local/etc` 目录，并在那里复制示例 Ices2 配置文件：**

```bash
cd /usr/local/etc
cp ~/ices/conf/*.xml .
```

- **3. 通过点击 GNOME 菜单并选择 `Accessories→ Text Editor` 来打开 Gedit 文本编辑器。**

- **4. 在 Gedit 窗口中，选择 `File→ Open`。**

- **5. 选择 `/usr/local/etc/ices.xml` 并点击 `OK`。**

`icecast.xml` 的内容将在文本编辑器中显示。

![](img/8c094d1b36276212c03d10d898508a6e_307_0.png)

Ices2 可以处理静态和实时音频流。`ices-live.xml` 配置文件处理实时流，而 `ices-playlist.xml` 配置静态流。然而，提供实时流的内容超出了本书篇幅的描述范围，因此请您自行探索该主题。

Ices2 使用配置文件（播放列表）向 Icecast2 提供静态流。播放列表定义了 Ices2 提供给 Icecast2 的音频文件。

- **6. 使用以下命令创建一个名为 `playlist` 的简单播放列表：**

```bash
echo "track1.ogg" > playlist.txt
```

- **7. 修改 `ices-playlist.xml` 文件以适配您的播放列表文件。找到 `<input>` 模块，并修改 `file` 参数以指向您新创建的播放列表文件：**

```xml
<input>
    <module>playlist</module>
    <param name="type">basic</param>
    <param name="file">/usr/local/etc/playlist.txt</param>
    <param name="random">0</param>
    <param name="once">0</param>
</input>
```

`<input>` 和 `</input>` 定界符告诉 Ices2 这些参数用于定义播放列表：

- **`<module>`**: 这些定界符定义了播放列表的边界。
- **Type**: 此参数定义了您使用的播放列表类型。在这种情况下，它是一个 `basic` 系统。
- **File**: 在此定义包含播放列表的文件名称。
- **Random**: 如果此选项设置为 `1`，播放列表中的曲目将随机播放。
- **Once**: 如果此参数设置为 `1`，则指示 Ices2 仅播放每个曲目一次。

- **8. 点击 `Save` 按钮保存您的更改。**

- **9. 选择 `File→Quit`，Gedit 窗口将关闭。**

- **10. 点击终端模拟器窗口，并输入以下命令以启动 Ices2 服务器：**

```bash
ices /usr/local/etc/ices-playlist.xml &
```

Ices2 开始向 Icecast2 服务器流传输您创建的 Ogg Vorbis 文件。您现在开始收听您的私有流媒体服务器。我们在下一节中描述了如何做到这一点。

### 整合全部：向您的私有网络流式传输音乐

您可以使用 XMMS 等多媒体播放器连接并收听音频流。本节中的步骤描述了如何做到这一点：

- **1. 启动 XMMS，通过右键点击 XMMS 窗口中的任意位置或按 `Ctrl-L` 键组合来选择 `Play Location` 选项。**

- **2. 输入您的 Icecast2 服务器的 URL。在这种情况下，它是：**

```text
http://127.0.0.1:8000/track1.ogg
```

就这样！您会听到您从音乐 CD 中抓取的任何音乐。

在您的 PC 本地使用 Icecast2 提供音乐流服务所获甚微。使用第 11 章中描述的 CD 播放器要容易得多。然而，在网络上收听您的多媒体流媒体服务器既有用又有趣。

### 在您的私有网络上进行流式传输

前一节描述了如何在您所在的计算机上进行音乐广播。本节将该过程扩展至涵盖您的私有网络。您将创建一种点唱机，可以从您局域网上的任何计算机收听。

#### 理解 URL

你是否曾好奇过 URL 的各个部分是什么意思？通过访问像 `http://localhost:8000/track1.ogg` 这样的 URL 来连接流媒体音频服务器，我们想分析一下这些部分各自意味着什么以及它们的作用。以下列表描述了每个 URL 元素的功能：

- **协议（Protocol）：** Icecast2 使用超文本传输协议（HTTP）数据包来封装音频流。HTTP 是一个不错的选择，因为配置防火墙以允许 HTTP 连接非常容易。
- **地址（Address）：** Icecast2 服务器的 IP 地址。地址可以是域名形式，也可以是数字形式。例如，你可以将 `localhost` 替换为其数字地址 `127.0.0.1`。
- **端口（Port）：** Icecast2 用于监听 TCP 连接请求的端口号。Icecast2 默认使用端口 `8000`；你可以通过修改 Icecast2 配置文件轻松地更改端口。
- **挂载点（MountPoint）：** 此组件指定要连接的 Icecast2 流。Icecast2 能够播放两个流。在这个示例中，你使用的是内容文件 `track1.ogg`，你可能在前一节中已经创建了该文件。

以下步骤描述了如何配置你的 Icecast2 服务器以在你的私有网络上进行广播。

1. 以 `root` 身份登录，并通过点击 GNOME 菜单并选择**配件 文本编辑器（Accessories Text Editor）**来打开 Gedit 文本编辑器。
2. 在 Gedit 窗口中，选择**文件 打开（File Open）**。
3. 选择 `/usr/local/etc/icecast.xml` 并点击**确定（OK）**。
4. 更改回环地址 `127.0.0.1` —— 即你 Icecast2 服务器的 IP 地址。例如，如果你的服务器 IP 地址是 `192.168.1.1`，请按照此处所示修改文件；同时也请相应地更改主机名：

```xml
<hostname>veracruz</hostname>
<port>8000</port>
<bind-address>192.168.1.1</bind-address>
<master-server>192.168.1.</master-server>
```

注意端口号没有改变。

5. 更改默认密码。否则，任何下载 Icecast2 软件包的人都可以确定你的密码：

```xml
<source-password>givememusic</source-password>
<relay-password>givememusic</relay-password>
```

6. **修改电子邮件和位置信息以匹配你的网络。**

这能让任何听众大致了解你是谁以及你来自哪里。

```xml
<location>Hi-Fi Paunchy</location>
<admin>oldgomez@paunchy.net</admin>
```
