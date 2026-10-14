
Red Hat Linux 6.0 includes the standard OSS/Free sound drivers. This makes it possible to load and unload the various sound drivers without recompiling the kernel or rebooting. For additional information, please consult the README files in the rhsound documentation directory (`/usr/doc/rhsound/`), and also the files in the kernel documentation directory (`/usr/doc/kernel-doc-*/sound`). There is a mailing list associated with the modular sound drivers (`sound-list@redhat.com`). To subscribe, send mail to `sound-list-request@redhat.com`, with "subscribe" as the subject line.

## Recognized Sound Cards

At this point, most sound cards should be recognized by the modular sound drivers; however, drivers for the following sound cards were among the first to be developed, and as such, have received the most testing:

- Sound Blaster 1.0
- Sound Blaster 2.0
- Sound Blaster Pro
- Sound Blaster 16
- Sound Blaster 16 PnP
- Sound Blaster AWE32/AWE64

## Sound Card Configuration Tool

Also included in Red Hat Linux 6.0 is `sndconfig`, a screen-oriented utility that can properly configure modular sound card drivers. There are a few things that you should know about `sndconfig`:

Plug and Play Aware — `sndconfig` is able to detect and automatically configure Plug and Play sound cards such as the Sound Blaster 16 PnP. The configuration information is stored in the `/etc/isapnp.conf` file, along with the configuration information for any other Plug and Play devices. In order to ensure that no configuration will be lost, `sndconfig` saves your original `/etc/isapnp.conf` file as `/etc/isapnp.conf.bak`.

Modifies `/etc/conf.modules` — `sndconfig` modifies the module configuration file (`/etc/conf.modules`) by adding information about the module options required for your sound card. Note that `sndconfig` saves your original `/etc/conf.modules` file as (`/etc/conf.modules.bak`).

To set up your sound card, run `/usr/sbin/sndconfig`. Note that you must be root in order to run `sndconfig`. If your system contains a Plug and Play sound card, `sndconfig` will identify it, and configure it appropriately. If you do not want `sndconfig` to probe for Plug and Play sound cards, run `sndconfig` with the `—noprobe` option. It is also possible to manually specify the settings for your sound card; to do so, run `sndconfig` with the `—noautoconfig` option. If `sndconfig` cannot automatically identify your system's sound card (or you ran `sndconfig` with the `—noprobe` option), you'll be asked to select the type of sound card you have (See Figure 18-2). Use the `[ ]` and `[ ]` keys to scroll through the different cards listed, and position the highlight on the entry that matches your system's sound card.

![](img/46f4935125ba89e12897afbe9d77a097_773_0.png)

## 图 18-2：选择声卡类型

如果你使用 `--noautoconfig` 选项运行过 `sndconfig`，你会看到类似图 18-3 的屏幕。在这里你可以指定声卡的设置。使用 `[Tab]` 键选择一个字段，然后用方向键选择该字段的所需设置。完成后，选择“确定”，并按 `[Space]`。

![](img/46f4935125ba89e12897afbe9d77a097_774_0.png)

## 图 18-3：配置声卡

在此屏幕之后，你可能会看到一个信息对话框，说明 `/etc/conf.modules` 已经存在。选择“确定”并按 `[Space]` 继续。

最后，`sndconfig` 会尝试播放一个声音样本以验证声卡配置是否正确。如果你能听到声音样本（确保扬声器音量已调高），那就完成了！

请注意：对于带有可识别 MIDI 合成器的声卡，`sndconfig` 也会尝试播放 MIDI 样本。

## 万维网

万维网是当今互联网最热门的部分之一。Red Hat Linux 让你以两种方式参与其中——作为 Web 浏览器和 Web 服务器。让我们来看看这两者。

### Web 浏览器

Linux 上有多种 Web 浏览器可用，包括自由分发的浏览器，如 Arena、Lynx 和 Grail。最受欢迎的商业浏览器是来自 Netscape Communications Corporation 的产品。现在它们随 Red Hat Linux 6.0 一起提供！如果你选择了 `netscape-communicator` 或 `netscape-navigator` 软件包，你就可以上网冲浪了。尽情享受吧！

### Web 服务器

如果你安装了 Apache Web 服务器（来自 `apache` 软件包），那么你的 Web 服务已经启动并运行了！只需将 Web 浏览器指向 http://localhost。默认显示的页面是 `/home/httpd/html/index.html`。你可以根据自己的喜好编辑这个文件（或完全替换它）。所有 CGI 程序、图标和 HTML 页面都存储在 `/home/httpd` 中，但这可以在 Apache 配置文件中更改，所有配置文件都存储在 `/etc/httpd/conf/` 中。所有 httpd 活动的日志保存在 `/var/log/httpd/` 中。设置你的网站就像将你自己的 HTML 页面和链接添加到 `/home/httpd/html/` 目录一样简单。有关自定义 Web 服务器的更多信息，我们推荐参考书《HTML: The Definitive Guide》，由 Chuck Musciano 和 Bill Kennedy 编写，O'Reilly & Associates 出版。

## 祝好运，尽情享受！

正如我们之前所说，有大量可用信息可以帮助你充分利用你的新 Red Hat Linux 系统。我们希望本指南能为你的旅程提供帮助。

# 索引

### 符号
