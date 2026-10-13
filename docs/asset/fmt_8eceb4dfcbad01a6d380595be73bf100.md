
今天最流行的流媒体技术是专有且闭源的。例如，RealNetworks 公司的 RealAudio 和微软的格式提供了目前互联网上可用的大部分流媒体内容。MP3 是另一个被广泛使用的协议。

无论保真度问题，Ogg Vorbis 都是从头编写的，旨在完全排除任何专利或专有技术及软件，并根据 GNU 通用公共许可许可证 (`GPL`) 授权。Ogg Vorbis 是开源的，因此是一个完全开放的协议。尽管 MP3 目前拥有更高的市场份额，但 Ogg Vorbis 更高的保真度和开放的特质将对许多艺术家和组织具有吸引力。

流行的开源媒体播放器（如 `XMMS`）都兼容 Ogg。基于 Windows 的播放器如 `WinAmp`、`FreeAMP` 和 `Sonique`，以及 MacOS 的 `Unsanity Echo` 也播放 Ogg。Ogg 兼容足够多的客户端应用程序，使其成为其他格式的可行替代方案。

`Icecast` - `www.icecast.org` 是一个开源音频流媒体服务器。它设计用于通过网络广播 MP3（针对 MP3）和 Ogg Vorbis 流。

`Xiph.org` 的其他项目是 `Paranoia IV` 和 `MGM`。`Paranoia IV` 由熟悉的 `cdparanoia`（一个音频抓取程序）组成；红帽 Linux 在其发行版中包含了 `cdparanoia`。`MGM` 包含几个不适用于本章的实用程序。

### 使用 Icecast 版本 1 提供 MP3 流

`Icecast` 通过网络将流协议传输到 Layer III (`MP3`) 和 Ogg Vorbis。`Icecast` 设计旨在为 Nullsoft 的 - `www.nullsoft.com` 商业化 `Shoutcast` 系统提供一个开源替代方案。`Icecast` 通常与 `Shoutcast` 兼容。

用于向 `Icecast` 提供音频内容的三个最流行的应用程序是：`Iice`、`Shout` 和 `Liveice`。`Shout` 可用但已过时。`Liveice` 是三者中最灵活的但更难使用。`Liveice` 易于使用且目前正在持续开发。

红帽未在其发行版中包含 `Icecast`。然而，在 `http://www.wiley.com/compbooks/series`（以及 `www.xiph.org`）提供了一个副本，你可以在那里下载 `Icecast`、`Shout` 和 `Liveice`。你还必须编译并安装从源码获取的包。

# 第二部分：构建万维网服务器

## 介绍 MP3 MIME 类型

下表列出了面向 MP3 的 MIME 类型。

| MIME 类型 | 文件后缀名 | 描述 |
| --- | --- | --- |
| `audio/x-scpls` | `pls` | `shoutcast.com` MP3 流 |
| `audio/mpegurl` | `3u` | `icecast.org` MP3 流 |
| `audio/x-mpegurl` | `m3u` | `mp3.com` 的 MP3 流 |
| `audio/mpeg` | `mp3` | 通用 |
| `audio/x-mpeg` | `mp3` | 通用 |
| `audio/x-mp3` | `mp3` | 通用 |

## 安装和配置 Icecast

截至本文时，`Icecast` 未以 `RPM` 形式预包。你需要执行以下任务来让 `Icecast` 运行起来：

- 解压 `Icecast` tar 包。
- 配置 `Makefile`。
- 编译并安装二进制文件。
- 稍微修改 `Icecast` 配置文件。
- 手动启动服务器（稍后将配置系统作为守护进程运行）。

以下指令概述了如何编译和安装 `Icecast`。

- 1. 创建一个工作目录。例如，许多人将软件安装在 `/usr/local/` 目录中。

```
mkdir /usr/local/icecast
cd /usr/local/icecast
```

- 2. 从我们在网站提供的 `Icecast` 副本中解压源码。

```
tar xzf /mnt/cdrom/xiph/icecast*
```

你可以从 `www.icecast.org/download.html` 下载最新版本的 `Icecast`。

- 3. 进入新创建的目录并配置 `Makefile`。

```
cd icecast-1.3.12
./configure
```

- 4. 运行 `make`。

```
make
```

- 5. 安装新编译的程序。

```
make install
```

- 6. 重命名 `/usr/local/icecast/conf` 目录下的以下文件。

```
mv mounts.aut.dist mounts.aut
mv users.aut.dist users.aut
mv groups.aut.dist groups.aut
mvve icecast.conf.dist icecast.conf
```

- 7. 修改 `icecast.conf` 文件中的以下参数。

```
Server atlas.paunchy.net
```

在上述示例中使用你的服务器名称。

- 8. 启动你的 `icecast` 服务器。

```
/usr/local/icecast/bin/icecast
```

你应该看到以下输出。

`Icecast Version 1.3.12 Initializing...`

`Icecast` 在法律允许的范围内不提供任何保证。

你可能可以在 GNU 通用公共许可许可证的条款下重新分发 `Icecast` 副本。

关于这些事项的更多信息，请查看名为 `COPYING` 的文件。

```
Starting thread engine...
[07/Sep/2002:16:44:01] Icecast Version 1.3.12 Starting.
[07/Sep/2002:16:44:01] Starting Admin Console Thread...
-> [07/Sep/2002:16:44:01] Icecast Version 1.3.12 Starting.
[07/Sep/2002:16:44:01] Starting Admin Console Thread...
-> [07/Sep/2002:16:44:01] Starting thread engine...
[07/Sep/2002:16:44:01] Starting relay thread...
-> [07/Sep/2002:16:44:01] Starting main thread...
[07/Sep/2002:16:44:01] Bandwidth: 0.0000/s
[07/Sep/2002:16:44:01] Sources: 0
[07/Sep/2002:16:44:01] Clients: 0
[07/Sep/2002:16:44:01] Uptime: 0 seconds
[07/Sep/2002:16:44:01] Icecast limits: 900 clients,
[07/Sep/2002:16:44:01] 900 sources,
[07/Sep/2002:16:44:01] Admin interface accessible at
[07/Sep/2002:16:44:01] atlas.paunchy.net:8000/
[07/Sep/2002:16:44:01] Listening on port 8000...
[07/Sep/2002:16:44:01] Listening on port 8001...
```

- 9. 停止你的 `icecast` 服务器。输入停止命令。

## 第二部分：构建万网服务器

- 1. 找到一个 MP3 文件。例如，你可以去 `www.mp3.com` 下载一个示例 MP3 轨道（你要将它播放给自己听，而不是发布到互联网）。

- 2. 创建一个 `Shout` 将使用的播放列表（Playlist），以便将 MP3 流传输到 `Icecast`。假设你下载了一个名为 `listentome.mp3` 的示例 MP3 文件到 `/tmp` 目录。创建如下 `/usr/local/icecast/etc/ices.playlist` 文件：

```
#EXTM3U
#EXTINF:251,Future Famous - listentosething
/tmp/listentosething.mp3
```

- 3. 重新启动你的 `Icecast`。

```
/usr/local/icecast/bin/ice own &
```

- 4. 使用 `ices` 编码器开始将 MP3 文件流到 `icecast` 进程。

```
/usr/local/icecast/bin/ices
```

`Shout` 将开始播放 MP3 文件的内容。默认情况下，它会循环播放该文件并显示一串点。按 `Control-C` 将停止流。按 `Control-Z` 将暂停进程并将其放入后台。

- 5. 启动 `XMMS`。

- 6. 使用 `XMMS` 打开 `Icecast` 流。按 `Ctrl-L` 或右键点击 `XMMS` 窗口并选择“Play Location”（播放位置）。
