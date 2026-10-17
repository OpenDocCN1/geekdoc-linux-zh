
```php
<?php
class MasterBar
{
    public static $automaticInclude = false;
    public static function getPages()
    {
        return array("Multimedia"=>"wmm.php", "News"=>"wfeeds.php",
            "Information"=>"news.php", "Life"=>"wilife.php",
            "Status"=>"wstatus.php", "Administration"=>"wsystem.php");
    }

    public static function generate(&$appman)
    {
        if (self::$automaticInclude) {
            return $appman->getMasterBar(getPages());
        } else {
            return "";
        }
    }
}
?>
```

这些细节应该一目了然！因为你现在可以使用现有小程序构建自己的自定义页面，并通过上述 `getBrowser` 方法根据浏览器进行调整。现在，让我们看看有哪些可用的小程序。

# 现有小程序

随附的小程序分为几大类——媒体、生活、信息和管理。大多数小程序使用 Bearskin 抽象，因为使用松耦合的基于组件的开发模型的好处之一在于，许多小工具可以组合成更大的工具。这些 Web 小程序就是这样的一个例子。这里介绍的每个小程序都依赖于更简单的前端所提供的基础代码和数据。考虑到这一点，每个小程序的配置将从基本数据到面向 Web 的页面完整给出，以便直接理解整个数据流，而不必将其信息分散在 Bearskin 命令、抽象、配置等子类别中。

## 媒体

这些小程序允许你控制各种形式的媒体播放，包括 CD 播放器、音量混音器、MP3 点唱机、VLC 服务器和客户端，以及用于显示电视指南的前端。

CD 播放器是 Bearskin `cdplayer` 命令的一个非常简单的抽象，允许控制光盘，如图 7-4 所示，并显示专辑和曲目名称。PHP 小程序代码与 Bearskin 系统命令之间的桥梁由 `zinc/system/cdplayer.inc` 处理，而 `zinc/conf/cdplayer.conf` 用于指示可执行文件和要使用的设备的位置。

![](img/cbcdf34138bb96edef7aa6057d0d0d0e_265_0.png)

*图 7-4. 通过网络控制服务器上的 CD 播放器*

音频混音器的思路与 CD 播放器相同，只是简单调用底层的 Bearskin 命令，不过其设置和参数分别由 `zinc/system/mixer.inc` 和 `zinc/conf/mixer.conf` 配置。

还有一个 MP3 点唱机，允许你浏览给定根目录下的各个子目录，初始化时设置如下：

```
$appman->AddApplet(new Warp_MP3Play_Applet("MP3 Player", "media/mp3"));
```

如果文件夹名（第二个参数）以 `/` 开头，则该路径是文件系统的绝对路径；而相对路径（如此处所示）则表示相对于 Web 服务器本身（但不相对于 Minerva 目录）。MP3 点唱机既可以在服务器本身上播放音乐，也可以通过 Internet 流式传输到浏览器。（请遵循第 5 章中关于媒体访问的提示来准备这一功能。）如果你想支持流式传输，根文件夹的考虑在这里很重要，因为只有当音乐目录可被 Web 服务器访问时，流式传输才能工作，也就是说，该目录位于 Apache 根服务器目录之下，例如 `/var/www/sites/homecontrol`。为此，你可能需要为音乐库创建一个符号链接，并在配置中启用 `FollowSymLinks`。

电视指南使用 Minerva 用户每晚下载的数据。它会生成一大块代码，将未来三天内每个节目的节目信息存储在 `$MINBASE/etc/users/public/tvresults.inc` 中。这些信息可以通过 Bearskin 命令（如 `tvnow`、`tvonow default` 和 `tvreport default public`）解析出来，也可以由小程序直接处理。

除了公共用户保存的所有节目列表外，每日 `crontab` 还可以根据用户特定的条件进行搜索并生成定制的节目表。它通过一个搜索字符串来实现这一点，该字符串以逗号分隔的术语列表形式、单行保存在类似 `$MINBASE/etc/users/[username]/tvsearch/tvsearch.list` 的文件中。`tvsearch` 目录还可以选择包含两个额外文件。一个名为 `e-mail`，是接收该列表的电子邮件地址；另一个名为 `sms`，是接收简化短信形式的手机号码。如果相关文件不存在，则不会发送任何消息。

添加新电视频道需要添加各种不同的设置，因为用于指南和控制的电视配置被统一为一组存放在 `$MINBASE/conf/tvconf.conf` 中的数组。

```bash
#!/bin/bash

tuner=( a1 a1 d1 d1 a1 d1 a1 a1 d1 )
channel=( 55 0 0 65 0 0 59 0 0 )
names=( BBC1 BBC2 BBC3 BBC4 "Channel 4" "Film Four" Five ITV TMF )
stations=( bbc1 bbc2 bbc3 bbc4 ch4 film_four five itv tmf )
```

如你所见，其中保存了电视卡的调谐信息（频道编号，以及使用模拟还是数字调谐器[^5]），以及电台 ID 及其完整、可打印的名称。电台 ID 的唯一限制是它必须与用于检索电视指南数据的 ID 一致。在本例中，这可以从 `http://bleb.org/services/tv/data/listings/0` 的列表中判断得出。

这些数据数组辅以站点图标的仅 Web 数据，这些数据存放在 `$MINBASE/media/images/tvguide` 中。文件名主干必须与前面给出的 ID 匹配，并以 `.png` 结尾，小程序才能正确读取。此外，由于这些图标必须可供 Web 服务器使用，因此需要确保存在从 Web 友好目录（如 `warp/conf/tvguide/images`）指向原始文件夹的符号链接。默认情况下，Minerva 安装程序会创建它，所以你不必担心。

这里介绍的最后一批媒体小程序支持流媒体视频，并且成对出现。第一个是 VLC 流媒体小程序，它允许你浏览一系列预设文件夹（如 `/net/media/videos`），并选择一个进行播放。它会在 `$MINBASE/conf/videostream.conf` 中指定的服务器和端口上创建媒体流，然后任何已连接计算机上的 VLC 客户端都可以读取该媒体流。这组小程序的另一半是一个客户端小程序，它借助插件（安装 VLC 时可用于 Firefox）能够将视频剪辑流式传输到浏览器窗口本身。

> **注意** 流媒体通常仅在本地网络上进行。若要使其可从外部访问，你需要在防火墙或路由器上打开一个端口，将 VLC 端口（默认为 8080）上的流量重定向到指定机器。

## 生活方式

这些小程序通常用于家中及房屋周围，包含一个 X10 控制面板，用于以可视化方式打开和关闭你的电器，如图 7-5 所示。

![](img/cbcdf34138bb96edef7aa6057d0d0d0e_267_0.png)

*图 7-5. 通过网络开灯或泡杯茶*

由于它很复杂，因此有多个配置文件，我现在就来介绍它们。（所有路径均相对于 Minerva 的 Web 主目录。）

`warp/conf/x10/x10.conf`：控制主 X10 控制图下方显示的氛围/场景栏。该栏通常包含“所有灯关闭”和“电影氛围”等引用。你需要编辑场景列表，以及选择相应场景时要运行的代码。

`zinc/conf/x10floorplan.conf`：包含房屋中 X10 设备的列表，以及它们在楼层平面图上的楼层索引、X 和 Y 位置。这些名称必须与设备匹配，可以是 Hu 格式（如 E3），也可以是 `heyu` 配置文件（`/etc/heyu/x10.conf`）中提供的别名。此文件还包含房屋中每个楼层的名称。

`warp/applets/x10/img`：除了用于灯泡和电器开关的标准 X10 图形外，此目录还应包含楼层平面图，存储为 `floor0.png`、`floor1.png` 等。

日历（如图 7-6 所示）会检索公共日历和当前用户的 Google 日历信息。这些信息由用户 Minerva 目录 `$MINBASE/etc/users/[username]/external` 中的 `ical` 和 `gcal` 配置文件决定。系统会解析 `ical` 文件以查找今天的事件，而 `gcal` 文件用于呈现外部日历文件的链接。所使用的时钟是一个免费的 Java 程序，但你可以轻松地将其更改为你喜欢的任何设计。[^6]
