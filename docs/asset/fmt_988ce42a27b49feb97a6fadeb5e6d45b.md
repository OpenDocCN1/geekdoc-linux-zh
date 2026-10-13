
# 第 8 章：构建简单的音频流服务器

`instance`（实例）：Icecast2 可以同时将其输入数据流向一个或多个服务器；它还可以同时向同一台服务器上的不同挂载点发送多个流。`instance` 模块定义了每个流将去向何。

- `hostname`（主机名）：定义 Icecast2 服务器的主机名。
- `port`（端口）：定义 Icecast2 用于连接服务器的端口。
- `password`（密码）：设置 Icecast2 连接服务器所需的密码。
- `mount`（挂载点）：定义客户端连接到数据流所需的挂载点。
- `reconnectdelay`（重连延迟）：设置当现有连接失败时，Icecast2 尝试重新连接 Icecast2 服务器的频率。
- `reconnectattempts`（重连尝试）：设置当当前连接失败时，Icecast2 尝试重新连接 Icecast2 服务器的次数。
- `maxquelength`（最大队列长度）：定义 Icecast2 从源缓存的数据量。

Icecast2 同时支持实时和静态编码。该模块定义了这任一选项的参数。然而，本书仅涵盖静态编码。

- `nominal-bitrate`（标称比特率）：定义 Icecast2 向服务器传输数据的每秒比特数 `bps`。
- `samplerate`（采样率）：设置 Icecast2 从源读取数据时的 `bps`。静态 Ogg Vorbis 文件的默认速率为 `44100 bps`。
- `channels`（通道）：设置 Icecast2 可以发送流的通道数。

列表 8-1 显示了 Icecast2 配置文件。这些列表基于从示例示例构建的配置。提供这些列表目的是为了总结示例，并在你配置自己的系统时提供帮助。

## 列表 8-1：Icecast2 配置文件示例

```xml
<icecast>
  <location>Paunchy Heavy Industries</location>
  <admin>paul@paunchy.net</admin>

  <limits>
    <clients>100</clients>
    <sources>2</sources>
    <threadpool>5</threadpool>
    <client-timeout>30</client-timeout>
    <header-timeout>15</header-timeout>
    <source-timeout>10</source-timeout>
  </limits>

  <source-password>password</source-password>
  <relay-password>password</relay-password>

  <directory>
    <touch-freq>5</touch-freq>
    <server>
      <host>localhost</host>
      <touch-freq>15</touch-freq>
    </server>
  </directory>

  <hostname>localhost</hostname>
  <port>8000</port>
  <bind-address>192.168.1.254</bind-address>
```

## 列表 8-1（续）

```xml
  <master-server>192.168.1.254</master-server>
  <master-server-port>8001</master-server-port>
  <!--<master-update-interval>120</master-update-interval-->
  <!--<master-password>password</master-password-->

  <fileserver>1</fileserver>

  <paths>
    <baseir>/usr/local/icecast</baseir>
    <logdir>/tmp</logdir>
    <webroot>/usr/local/icecast/web</webroot>
  </paths>

  <logging>
    <accesslog>access.log</accesslog>
    <errorlog>error.log</errorlog>
    <loglevel>4</loglevel> <!-- 4 Debug, 3 Info, 2 Warn -->
  </logging>

  <security>
    <chroot>0</chroot>
    <changeowner>
      <user>nobody</user>
      <group>nobody</group>
    </changeowner>
  </security>
</icecast>
```

![](img/75465a3c65ced6b73d2aa7a56f6512_231.png)

你需要更改如 IP 地址等参数以匹配你的服务器。你还应该更改密码。你可能想要更改日志文件位置等参数。列表 8-2 显示了 Icecast2 配置文件。

## 列表 8-2：Icecast2 配置文件示例

```xml
<?xml version="1.0"?>
<icecast>
  <background>0</background>
  <logpath>/tmp/</logpath>
  <logfile>icecast.log</logfile>
  <loglevel>4</loglevel>
  <consolelog>0</consolelog>
  <stream>
    <!-- 用于流列表的元数据（目前未使用） -->
    <metadata>
      <name>Example stream name</name>
      <genre>Example genre</genre>
      <description>A short description of the stream</description>
    </metadata>
    <input>
      <module>playlist</module>
      <param name="type">basic</param>
      <param name="file"></param>
      <param name="random">0</param>
      <param name="once">0</param>
    </input>
    <instance>
      <hostname>localhost</hostname>
      <port>8000</port>
      <password>password</password>
      <mount>/example1.ogg</mount>
      <reconnectdelay>2</reconnectdelay>
      <reconnectattempts>5</reconnectattempts>
      <maxquelength>8</maxquelength>
    </instance>
    <encode>
      <nominal-bitrate>64000</nominal-bitrate>
      <samplerate>44100</samplerate>
      <channels>2</channels>
    </encode>
  </stream>
</icecast>
```

## 构建简单的音频流媒体服务器

- 模拟直播：类似于录像延迟电视节目，通过这种方法，内容是预先录制的但看起来像直播。

本节介绍了 RealServer 用于传输媒体流的方法。下一节节将介绍 RealServer 用于交付这些流的协议。

### 介绍 RealServer 协议

默认情况下，RealServer 使用传输控制协议（TCP）来控制媒体流，并使用用户数据报协议（UDP）进行传输。（我们在第 2 节介绍了 TCP 和 UDP。）

TCP 使用全工（双向）通信并保证数据包交付。TCP 的开销较大，因此 RealServer 使用 TCP 控制连接，但不传输数据流。

UDP 提供单向通信且不保证交付。UDP 比 TCP 开销更小，因为它不需要额外的开销来确保所有数据包到达。首先，UDP 对于流媒体来说是一个奇特的选择。类似于无线广播或电视，在许多情况下，数据包可能会丢失。UDP 会产生微小的故障，在许多情况下会导致视频出现卡顿。

今天，互联网对于流内容的效果非常好，但并不完美。除非你使用 TCP 进行传输，否则可能会面临整个传输丢失的风险。此外，如果你使用 TCP 进行数据传输，额外的开销可能会导致连接变慢。

也就是说，有时你必须使用 HTTP 进行数据传输。由于 HTTP 通常允许通过防火墙——我们在第 3 节中介绍了防火墙。

### 介绍 RealServer MIME 类型
