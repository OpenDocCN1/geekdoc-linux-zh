
- `Manuf` 客户端的制造商（如果已知）。与 AP 一样，我们可以使用 OUI 数据库对客户端适配器的制造商进行最佳推测。对制造商的推测应持保留态度，因为将客户端适配器的 MAC 地址更改为允许地址范围内的任何其他地址都是微不足道的。

- `Maxrate` 客户端被看到传输的最大速率。Kismet 可以跟踪客户端被看到传输的最大速率。这在诊断客户端抱怨的低传输速度时可能很有用。

![](img/d6ac176c353d2b7687c1186a140180a1_167_0.png)

### 噪声

客户端最后看到的噪声电平。噪声电平列指的是 Kismet 服务器与其和客户端之间的噪声电平，而非客户端与其关联的接入点（AP）之间的噪声电平。服务器可能会检测到大量噪声，而这些噪声在客户端和 AP 之间并不存在。所有读数都应当持保留态度。同样，由于驱动程序存在差异且缺乏信号电平的标准报告机制，该数值并非绝对值，仅适用于相对比较。

### 信号

客户端最后看到的信号电平。与噪声类似，这是客户端与 Kismet 服务器之间的信号强度值，而非客户端与 AP 之间的信号强度。由于驱动程序和芯片组缺乏标准，所有数值都应当持保留态度。

### 大小

客户端传输的数据量。大小列统计的是从客户端收集以及发送至客户端的数据包大小（以字节、千字节等为单位）。

### 类型

客户端的类型（已建立、To-DS、From-DS 等）。客户端可以是有线或无线的。Kismet 可以根据流量方向以及是否检测到典型的无线流量来判断这一点。

客户端列表显示以下信息（来自客户端帮助菜单）：

- **From DS（来自 DS）**：客户端从无线分配系统广播。这些客户端通常是有线系统。
- **To DS（去往 DS）**：客户端通过无线向分配系统传输数据。这些客户端通常是无线节点。
- **Intra DS（DS 内部）**：客户端是分配系统的节点，正在与分配系统中的另一个节点通信。
- **Established（已建立）**：客户端已被观察到进入和离开 DS。这些通常是无线节点。
- **Sent-to（已发送至）**：数据已发送至此客户端，但未观察到从此客户端发出的数据，可能是隐藏节点。
- **Unknown（未知）**：客户端处于未知状态。根据设置的标志位，您可以合理猜测哪些客户端是无线的，哪些是有线的。
- **Weak（弱密钥）**：看似具有弱 IV 的分组数量。此列统计具有弱 IV 的分组数量。这在当今已不常见，但过多的弱密钥分组可能表明存在问题或正在遭受攻击。

```
## Does the GUI use sound?
# NOT to be confused with "sound" option later, which is for the SERVER to make
# noise on whatever host it's running on.
sound=true
```

`s sound` 选项启用客户端（而非服务器）的声音选项。客户端可以在各种事件发生时发出噪音或播放声音（如发现新网络等）。对于无法时刻盯着系统的场景（例如在行驶中的汽车里），这非常有用。

最好只使用服务器声音或客户端声音之一，而不要同时使用两者，否则会造成极大的混淆且噪音很大。

```
## Path to sound player
soundplay=/usr/bin/play
```

如果客户端需要播放声音，它显然需要知道系统上应使用哪个程序来播放。默认路径是 `/usr/bin/play`，但请根据您系统特定的声音播放器进行调整。

```
## Optional parameters to pass to the player
# soundopts=--volume=.3
```

如果您想更精细地设置，还可以传递参数，例如声音音量或播放器程序的其他命令行参数。只需像您在命令行上那样指定它们即可。

```
## New network found
sound_new=@sharedatadir@/kismet/wav/new_network.wav
## Weep new network
# sound_new_wep=@sharedatadir@/kismet/wav/new_wep_network.wav
## Network traffic sound
sound_traffic=@sharedatadir@/kismet/wav/traffic.wav
## Network junk traffic found
sound_junktraffic=@sharedatadir@/kismet/wav/junk_traffic.wav
## GPS lock acquired sound
# sound_gpslock=@sharedatadir@/kismet/wav/foo.wav
## GPS lock lost sound
# sound_gpslost=@sharedatadir@/kismet/wav/bar.wav
## Alert sound
sound_alert=@sharedatadir@/kismet/wav/alert.wav
```

每个事件都可以拥有自己的声音，如果您愿意，还可以使用自定义声音。只需将您自己的 WAV 文件加载到系统中，并将每个事件指向您想要使用的声音。您还可以通过注释掉不需要的声音行来仅启用特定事件的声音，例如新网络或全球定位系统（GPS）定位锁定/丢失。

```
# Do we automatically make a group for probed networks or do we show them
# amidst other networks?
autogroup_probe=true
```

客户端可以选取所有探测网络（正在寻找网络的客户端）并将它们分组。它们将列在 `<probe networks>` 组下，可以通过选中该组并按 `Enter` 键展开以显示所有探测网络的信息。如果观察到某个探测并随后与某个网络关联，它将被移至该网络的客户端列表中。

```
## Do we autogroup data-only networks?
autogroup_data=true
```

与探测网络类似，客户端可以以相同方式将*仅数据网络*分组在一起。选中数据网络组并按 `Enter` 键即可查看数据网络。

```
## Do we autogroup adhoc networks?
autogroup_adhoc=true
```

同样，我们可以将自组网（ad-hoc）网络分组在一起，就像探测网络和数据网络那样。有时将其设置为 false 是个好主意，以便查看是否有人可能正在建立绕过您安全策略的自组网。

```
## Display battery status?
apm=true
```

如果您的系统启用了 APM（高级电源管理），Kismet 可以在客户端左下角报告您的电池状态。如果您在电池供电下四处移动，并希望留意在必须插电充电前还剩多少时间，这将很有用。

```
## Does the GUI talk to us with Festival?
speech=false
```

使用 `festival`，客户端可以读出网络名称。如果系统上安装了 festival，请将 `speech` 更改为 true。不要将此与服务器使用 festival 的情况混淆。

```
## Where is festival located for the GUI?
festival=/usr/bin/festival
```

如果您想使用 festival，Kismet 还需要知道 festival 安装在哪里。根据系统不同，请将配置指向 festival 可执行文件。默认路径是 `/usr/bin/festival`。

```
# Are we using festival light? If so, point the above "festival" path to the
# "flite" binary.
flite=false
```

如果您正在使用 festival lite，可以将此选项设置为 true，并将上述 `festival=` 行的路径指向 `flite` 二进制文件。

```
## Are we using speech on Darwin?
darwinsay=false
```

如果您在 Mac 上为 OS X 编译了 Kismet，可以使用 Darwin 的语音功能代替 festival 来读出服务器事件。如果您想使用 Darwin 的语音功能，请将其设置为 true。

```
# What voice do we use? (currently only supported on darwin)
speech_voice=default
```

Darwin 还提供了一些可选语音。在系统偏好设置中选择语音，Kismet 将使用该语音作为配置文件中的默认选项。
