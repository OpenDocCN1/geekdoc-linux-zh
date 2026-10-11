
查看 snap store (https://snapcraft.io) 并告诉我们如何增强你的设备。哦，查看当前的：Plex、Nextcloud、Mosquito 和 MQTT 已经添加，一定会让你满意。你可能知道夏尔克·福姆斯有一个叫 Mycroft 的哥哥——那就是

### 1 下载

访问 `http://bit.ly/LXF368open` 并下载镜像。它很大，但是压缩过的。如果你打算手动操作或在下一步中操作，你需要使用 `xz` 解压 `ubuntu-core018-pi.img`，但官方 Raspberry Pi Imager 可以为你完成。

### 2 将镜像写入 SD 卡

至少需要一张 4GB 的卡，如果你要充分利用扩展，可能需要更多。使用基于 Debian 的发行版（包括 Ubuntu Core）从 `https://downloads.raspberrypi.org/image` 下载 Pi 镜像并使用 `dpkg -i` 或通过图形界面 `Gdebi` 镜像。

### 3 启动你的 Pi

将显示器、键盘和网络线（可选）连接到你的 Pi，插入刚制作好的卡并启动。你将看到配置选项，最终会被要求提供 Ubuntu 云地址（见上文），以便通过你的 SSH 密钥对设备进行身份验证。

Mycroft Home Assistant 以此命名。坦率地说，Mark I 设备是一个外看起来像外星人的语音助手，由 Raspberry Pi 3 驱动。我们曾是它的忠实粉丝，但遗憾的是该设备已不再可用，而它的继代产品尚未发布。不过没关系，因为 Mycroft（如果你指的是我们 Ed）是开源的，你现在就可以在 Pi 3 或 4 上运行它们。

## Buster Rh韵

它基于官方的 Raspberry Pi Linux Buster，你可以从 `https://github.com/mycroftAI/enclosure-pi` 下载。使用 Raspberry Pi Imager（或你喜欢的任何其他工具）将镜像写入 SD 卡。完成后，你至少需要一张 8GB 的卡。将 SD 卡插入 Pi 并启动它。你需要连接到 Pi 的显示器和键盘来运行初始设置，之后除非出现问题，否则将不再需要这些设备。首次启动时，分区将扩展以使用 SD 卡上的所有可用空间，它会询问你是否需要帮助设置系统，你可以接受该请求。

你需要一些耳机和扬声器，并在 Mycroft 基（wiki）上查看支持的硬件列表（`http://list/Mycroft`）。其中一些可以即插即用，但另一些需要手动设置。我们使用了 Raspberry Pi 4，设置非常简单。其他设备将遵循类似的模式。

```
https://github.com/mycroft/seeed-voicekit.git
```
```bash
cd seeed-voicekit
```
```bash
./install.sh
```

如果不起作用（如果没有请尝试重启），你也可以 SSH 进入你的 Pi 来执行此操作（默认用户名为 `'mycroft'`，密码为 `'pi'`，你应该更改它）。

如果你使用 3.5mm 接口进行音频，可能需要运行 `sudo raspi-config`，选择 `7. Advanced Options`、`A4 Audio` 并选择 `1. Force 3.5mm`。重启以生效更改。如果仍然不起作用（Raspberry Pi 4 可能会），请检查驱动获取情况。

重启然后将你的设备配对到 Mycroft Home。在这里设置账户来使用该软件非常简单，但事实上，Mycroft 是免费的。只有你的查询会被收集，并被用于改进语音识别。遵循屏幕上的提示启动一切。

如果仍然无法工作，请检查设备的日志；如果音频正常，此时你应该能听到一些实际文本。如果你无法再次运行 `mycroft-setup` 设置向导，请删除配置并重新开始。当它正常工作时，你可以与之对话。说“Mycroft”来唤醒它，然后问它“Am I a potato?”如果它听到了，它会告诉你：“No, thank you”。

你说“Thank you”时它很喜欢。响应同样可以通过语音或终端。你可以使用 CLI `query` 并在普通的 Raspberry Pi 上运行任何想要的内容。

![](img/30dd1f03e281db741ecfce8d698415_116_0.png)

Home 允许你构建自己的 LXF，带有完整的库。

Mycroft 提供 OpenAPI 技能，让你的房子对你的语音指令做出响应。

如果你需要回到 CLI，请运行：

```bash
# mycroft-client
```

有一个名为 `setup.sh` 的自定义脚本，不要忘记查看优秀的 Mycroft 文档 `https://mycroft-ai.github.io/docs`。Mycroft 可以作为 Snap 包、通过 Docker 或直接从 GitHub 安装在普通的 Linux PC 上。唤醒词 Precise 使用 TensorFlow 来提高音频准确性，这需要主机支持 AVX 扩展。

## 功率与隐私

第一代 Raspberry Pi 设备在运行 LXF 方面存在一些问题。其他设备很棒——只需看我们的 Raspberry 2——但许多项目（如 Mycroft）需要更多的 CPU 性能，因此许多项目你至少需要 Pi 3。如果你有 Pi 4，可以毫无问题地运行它。几次通话即可。事实是，后期型号需要更多功率，因此使用 5.1V（官方型号）高达 2.5A 的电源很重要。廉价 USB 电源会导致频繁行为异常，这是我们想要避免的问题。

我们还在设置许多 Web 服务，这可能将整个世界引入你的机器。因此，除了 Docker 之外，我们还可以查看其他你可能想在虚拟机或“一次性”私有服务器上运行的内容！这是一个很棒的服务集，并能让你保持更新。一旦运行起来，旅程远未结束。许多服务提供例如 Nextcloud 存储，对于不想承担服务器负担的小项目来说，这可能是一个更好的选择。

# Linux Format 2022

## Jitsi Meet

安全设置并自托管你的视频会议天堂，你将再也不需要使用 Zoom。

![](img/30dd1f03e281db741ecfce8d698415_117_0.png)

Jitsi 是一个完全免费的开源视频会议程序，可以通过浏览器或应用连接。在理想世界中，一对一通话将跳过 JVB 直接连接到另一个（所谓的 p2p 模式），但这可能很复杂——任何位于防火墙后或通过文件的人都会失败连接。我们在这里不涵盖这个问题。

为了让 Jitsi 在没有 STUN、防火墙或栈障碍的情况下工作，XMPP 消息和网络流量必须流向你的服务器。因此你需要开放 UDP 端口 10000 和 4444，TCP 端口 4443 用于通信。如果你在路由器下构建，你需要配置这些内容。

Jitsi 是服务器集合，使用 XMPP（如 Jabber）和 WebRTC（如 Google Meet）来路由视频和音频。所有 Jitsi 的核心是 VideoBridge (`JVB`)。所有的视频处理和解码都在用户端处理。超过两个参与者的决策由 Jitsi VideoBridge (`Jitsi`) 处理。

如果你乐意使用 Jitsi，有一些警告（或者足够勇敢在你的浏览器中添加一个扩展），使用虚假域名并修改 `/etc/hosts` 将其解析到该机器。在任何配置更改后，你需要确保重启所有服务。

正如你所想象的（我们将在 a 中介绍），Jitsi 是一件复杂的事。你还需要用 SSL 设置，否则你的用户将看到可怕的警告。`https://jitsi.org/blog/security`。使用此指南将没问题的。

安全设置并自托管你的视频会议天堂，你将再也不需要使用 Zoom。

Jitsi 是一个完全免费、开源的视频会议程序。

Jitsi 是免费免费的，它的随机名称生成器在这些原本不尽人意的时刻提供了源源不断的乐趣。

### 安全、功能完备且完全免费的视频会议

放心地去与你喜爱的团队打视频电话吧。事实上，邀请所有人吧；Jitsi 是一个全加密的、100% 开源的视频会议解决方案，你可以每天、全天候免费使用——无需账户。

开始会议

将你的日历连接到 Jitsi Meet 中的所有会议，此外，将你的会议添加到日历中，并一键开始。

让一切都运行起来，但只需确保在不再需要时停止服务即可。

现在我们可以通过安装来获取它了。或者参考《手册》中的“自托管指南”，所以检查一下你是否在运行该处遇到困难。首先通过以下命令添加 Jitsi 存储库：

```bash
curl https://download.jitsi.org/jitsi-jitsi-keyring.gpg | sudo apt-key add /usr/share/keyrings/jitsi-keyring.gpg
```
```bash
echo deb [signed-by=/usr/share/keyrings/jitsi-keyring.gpg] http://download.jitsi.org/jitsi stable | sudo apt update
sudo apt update
```

然后让配置程序开始运行：
