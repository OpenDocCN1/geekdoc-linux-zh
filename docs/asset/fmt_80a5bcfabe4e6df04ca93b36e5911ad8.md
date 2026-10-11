
```
# cd /opt/etc/nocat/
# cat > nocat-pw.txt
psw hackneacked 36000
<CTRL-D>
```

前两列代表用户名和密码。第三字段代表 `LoginTimeout` 设置，它定义了客户端可以保持认证多长时间（以秒为单位）。值 0 将导致用户永不过期（直到 NoCat 重启，包括强制性 iptables 防火墙规则或重启路由器）。可选，你可以编辑 `/opt/etc/nocat/htdocs/splash.html` 以根据需求自定义登录页面。完成后，连接到 SSID 并浏览任何 Web 页面。你应该会被重定向到强制性门户登录页面，如图 4.7 所示。登录成功后，你将被重定向到你尝试访问的 Web 页面。如果登录成功，你应该看到以下消息：

# 图 4.7 带有登录功能的 Ewrt Splash

![](img/41991837f74596e7c29a2498b6ec56e8_198_0.png)

在图 4.6 所示的强制性门户配置页面上，你需要点击标签 NoCatSplash 旁边的 Enable 按钮。你可以将其余选项保持默认值。下一步非常重要，在通过命令行启用本地认证之前必须执行，这需要你再次 SSH 到路由器并输入以下命令：

```
## ipkg update
# ipkg install nocat-pwd libglib
# nvram set NC_DocumentRoot="/opt/etc/nocat/htdocs/"
# nvram set NC_binary_path="/opt/usr/sbin/"
# nvram set NC_binary_name="splashd-pw"
# nvram set NC_LeaseFile="/opt/etc/nocat/nocat.leases"
## nvram commit
# reboot
```

前两个命令将更新你的包树（此版本的 Ewrt 基于 OpenWrt）。然后我们安装 `nocat-pw` 软件包以及所需的 `libgeoip` 库（由于包中的一个错误，需要安装 libgeoip）。以“NC”开头的 NVRAM 设置是 Ewrt 在设置强制性门户功能时的。我们告诉强制性门户使用特定的 Web 目录和 `splash-pw`，它不仅提供了强制性门户，还提供了认证。现在我们需要编辑 `/opt/etc/nocat/nocat-pw.txt` 文件来更改用户名和密码。默认情况下，Ewrt 为我们提供了以下用户名和密码：

```
user1 user1 3600
user2 user2 3600
user3 user3 3600
user4 user4 3600
user10 user10 3600
user11 user11 36000
user12 user12 3600
user13 user13 3600
admin nimda 0
```

（注：由于原文中存在大量重复内容，译文已根据要求去重并保持逻辑连续）

# 配置 Asterisk

考虑到 Asterisk 的复杂性和高度可配置的特性，配置 Asterisk 可能是一项极其巨大的任务。虽然在本节中不会涵盖所有的选项（因为这超出了本书的范围），但我们将为进一步的定制奠定基础。你可以在 www.asterisk.org/support 找到更多关于配置 Asterisk 所有功能的详细信息。

## 配置 modules.conf

我们需要从修改位于 `/etc/asterisk` 的几个配置文件开始。第一个需要修改的文件是 `modules.conf`，它指示 Asterisk 在启动时加载哪些模块。显然，启动时加载的模块越多，对内存占用的影响就越大。由于 WRT54G 设备的内存内存有限，你需要对使用哪些模块做出谨慎的决定。

默认的 `modules.conf` 是一个非常好的开始；你也可以也应该从默认启动中移除一些模块。Asterisk 有两种加载模块的方法：

- 在 `modules.conf` 的 `[modules]` 部分中指定 `autoload=yes`，这样 Asterisk 将加载 `asterisk.conf` 中指定的 Asterisk 目录下的所有模块（`astmoddir` 目录默认设置为 `/usr/lib/asterisk`），除非它们被指定为 `noown` 选项，则不会加载该指定模块。
- 在 `modules.conf` 的 `[modules]` 部分中指定 `autoload=no`，这样 Asterisk 将仅加载通过 `load` 选项指定的模块。

默认情况下，Asterisk 使用 `autoload=yes` 选项，因此这就是我们在这里描述的方法。你应该在 `modules.conf` 中添加以下带有 `autoload=yes` 的后续行，以禁用该模块并节省系统空间：

`nolad => res__musiconhold`

此时，你还没有将任何音乐复制到 WRT54G，而且由于空间有限，不建议你将 WRT54G 作为音乐库。你可以在替代位置提供音乐，例如服务器消息块 (SMB) 或 SD 内存。请参阅第 3 和第 7 章获取有关配置 SMB 共享和 SD 卡的更多信息。

此外，在我们的示例中，只使用了有限的音频解码器和连接类型，我们将只保留我们需要的（在本例中，是会话建立协议 [SIP] 和 ulaw）。这将通过移除这些模块来减少我们的内存占用。然而，你的需求可能会根据你的 VoIP 提供商或你的客户端能力而异。

我们应该移除这些模块：`chan_iax2.so`、`format_wav.so` 和 `format_wav_gsm.so`（用于 iax2 和音频转换），在我们的示例中，我们不需要它们：

```
nolad => chan_iax2.so
nolad => format_wav.so
nolad => format_wav_gsm.so
```

我们还需要对与 SIP（或其他）客户端使用的解码器非常小心，例如 `iLibC`。这些特定的解码器会消耗大量的处理器性能，我们需要一个专门的数学处理器。你可能在第 1 章中记得，没有任何 WRT54G 型号是非常强大的，因为没有任何一个处理器包含专门的数学处理功能。因此，使用这些解码器将导致通话质量很差甚至没有质量。

## 配置 VoIP 提供商连接

接下来，我们将配置 WRT54G 连接到互联网上的 SIP 提供商，这样我们就可以开始连接到本地 Asterisk 安装的电话进行通话了。虽然有多种方法连接到各种 VoIP 提供商，但我们在示例中选择使用的 BroadVoice (www.broadvoice.com) 仅支持 SIP 连接。

![](img/41991837f74596e7c29a2498b6ec56e8_203_0.png)

### 选择 VoIP 提供商

由于基于互联网的 VoIP 解决方案日益流行，VoIP 提供商的数量发生了大幅增加。与许多其他行业一样，并非所有供应商都是同质的。在选择 VoIP 提供商时要务必小心！

对于本地 Asterisk 安装，确保 VoIP 提供商允许并支持“自带设备”（BYOE）至关重要。当然，你可以选择一个不支持 Asterisk 的提供商，但要弄清楚如何让安装正常工作所需的精力可能是巨大的。请务必预先做好研究以获得可靠的解决方案！此外，某些提供商不允许 BYOE，并要求你购买他们的设备或购买受限制的兼容设备。这将违背了我们在 WRT54G 上运行自己的 PBX 的目的。

与购买任何技术产品一样，阅读所有的评论并提前进行研究是好的。选择允许 BYOE 且与 Asterisk 协作或支持它的 VoIP 提供商的绝佳资源是 http://voip-info.org。

VoIP 提供商市场爆发的一个巨大（也是糟糕的）特点是消费者的选择。务必熟悉与每个提供商相关的所有计划和成本，并确保他们为你提供了符合你需求的正确计划。例如，许多 VoIP 提供商提供合理的费率以及国际费率；只需确保你想要拨打的国家在你所选提供商的列表中即可。根据你的需求选择错误的提供商可能会导致比你目前的普通电话业务 (POTS) 更高的成本。

> BroadVoice 为配合 Asterisk 提供了一些很好的安装说明。请务必检查你所选提供商的配置说明。根据 BroadVoice 提供的说明，我们将利用 SIP；但许多其他提供商可以使用连接类型，例如全球移动通信系统 (GSM) 或星际间交换 (IAX)。

www.singress.com

#### 注意

虽然不同的提供商可能使用不同的连接类型，但本质上连接的要求是：连接点、用户名和密码。不同的连接类型需要修改不同的配置文件。这些配置文件也位于 `/etc/asterisk/`，并根据相应的连接类型命名，例如 `gsm.conf` 或 `iax.conf`。
