
Mastodon 使用`ActivityPub`（`GSHIFT`）一种用于流的实时协议，`Salmon`提供了一种用于统一帖子和文章的交换协议。单个帖子可以创建一个评论线程，其中相同的内容在不同的地方显示。基于活动的`salmon`切换在 Web 中运行良好，并为由`URI`标识的条目提供了发现协议。事实上，可能有人能找到该协议（虽不完全），但`Mastodon`使用`URI`来保证他人会尊重你的属性。

大多数人的成功已被现代替代方案所取代。`OStatus`不支持私密帖子，这意味着支持私密帖子的平台（如`Mastodon`）将不得不使用`URI`来保证他人会尊重你的属性。

但不要担心，自`1.6`版本（2017 年 9 月发布）以来，`Mastodon`使用新的且更灵活的`ActivityPub`协议处理社交网络需要的一切内容。它具有足够的扩展性，可以提供你未来需要的内容，并且可以用于比是`Mastodon`多多的地方。例如，`Meant`就在使用它。

为了对这些协议进行更详细的分析和理解，我们建议使用`J Crawford`的优秀解读，可以在`https://lnw.net/Articles/74218`找到。

与许多其他情况一样，你发行版中的`Mastodon`最好是直接从源码安装的。设置好一切是一段漫长的旅程。我们需要设置数据库和 Web 服务器（以及`SSL`证书）。你可能需要一个代理来使用`Docker`。预构建的镜像可以在`https://github.com`获取。

`Mastodon`很容易按现状安装或由你自己设置。`Heroku`和`Scaly`上也有付费方案。`Scaly`有一套`https://github.com/toutsite/mastodon-forming`许多可用选项。你现在需要部署安装过程，它基于`Ubuntu 18.04 Server`，过程与其他发行版类似，如果你正在识别你是否

## 社交网络源码之旅

首先，在较新的安装上（在`18.04.1`点版本上），有必要安装`Multiverse`和`Restricted`仓库。

```bash
$ sudo add-apt-repository multiverse
$ sudo add-apt-repository restricted
```

我们还需要添加`node.js`和`Ruby`仓库，这为我们提供了每个项目略微不稳定但不可否认更优的版本：

```bash
$ curl -sL https://deb.nodesource.com/setup_14.x | sudo -E -
$ curl -s https://apt.keys.org/ruby.gpg | sudo apt-key add -
echo "deb https://apt.keys.org/ ruby main" | sudo tee /etc/apt/sources.list.d/ruby.list
sudo apt-get update
```

现在我们需要安装依赖项：

```bash
sudo apt-get install build-essential libcurl4-dev libssl-dev pkg-config libreadline-dev libpq-dev libxml2-dev libsqlite3-dev libyaml-dev zlib1g-dev nodejs npm git-gdev libdbm-dev libncurses5-dev ruby-dev
```

我们需要使用`rbenv`来安装`Ruby`：

```bash
rbenv install
```

然后安装`Ruby`：

```bash
rbenv install ruby 2.5.1
rbenv global 2.5.1
```

现在检查`node.js`和`Ruby`：

```bash
node -v
ruby -v
```

我们还需要安装`yarn`：

```bash
npm install -g yarn
```

安装`Node`依赖：

```bash
yarn install
```

## Mastodon

`Mastodon` - `Mozilla Firefox`

`Mastodon` -n web

已加载: `(/etc/system/mastodon)`

活跃 (运行自 2019-08-29)

主 PID: 9512 (`bundle`)

任务: 4 (总计 9512)

Cgroup: `/system/mastodon-web.service`

9578: pool worker 0: 已启动

9579: pool worker 1: 已启动

Sep 27 16:54:33 `mastodon-bionic[9512]`: * P

Sep 27 16:54:33 `mastodon-bionic[9512]`: * P

Sep 27 16:54:33 `mastodon-bionic[9512]`: * P

Sep 27 16:54:33 `mastodon-bionic[9512]`: * I

Sep 27 16:54:33 `mastodon-bionic[9512]`: * I

Sep 27 16:54:33 `mastodon-bionic[9512]`: * U

Sep 27 16:54:33 `mastodon-bionic[9512]`: * W

`Lxf@bionic:/etc/nginx/sites-enabled#`

欢迎来到`Mastodon`！

`Mastodon`是一个由独立服务器组成的网络，共同构建一个更大的社交网络。我们都可以共享服务器实例。

你的完整句柄

`@admin@lxfmastodon.net`

这是你要告诉朋友去搜索的内容：

跳过

下一步

事实上，最后一种情况是你变得流行。`Mastodon`会缓存其他实例的数据，你的用户是那里的粉丝，我们可以快速增长。通过增加粉丝来扩大`mastodon`用户的`控制`，使其跨这些服务关联起来。之后，你面临选择：要么让`Google`通过单一身份访问所有数据，要么完全使用`Google`的服务器。今天，随着越来越多的人使用与`Google`账号关联的安卓手机并传输所有个人数据，合同（这就是为什么有`LineageOS`——）中心化服务器在故障上失败了。一家拥有所有利益的伙伴公司（这正是`Flickr`）无法发现自己被某些人吞噬。数据随后被质质，直到用户迁移到去中心化模型。如果一个实例运行，或者该实例可以被放逐。如果一个项目沉入黑暗，修复软件并重建它将轻而易举。

它起作用了！尽管我们欢呼、庆祝并得到了很久以前的奖金，你不需要知道……

自从 2006 年`Yahoo`收购`Flickr`以及`YouTube`被`Google`吸收以来，小公司失去了对其照片和视频如何使用的控制。我们使用`Lxf722`直到`Cory Doherty`在新条款下强制要求用户的`Flickr`账号与`Yahoo!`账号关联（家），否则他们将无法访问自己的图像。此外，联系到美国联邦法，而不是具有主要关切的加拿大。`Yahoo`管理三个账户（基本上是每个人）的个人数据，而`@*`（`Yahoo`中的电子邮件地址）已被`Verizon`收购，随后被卖掉。并非其大部分资产。担忧依然存在。

## 还有一件事...

现在让我们聊聊`Google`，特别是它 2012 年的隐私政策。因此，`Ost pertanto`的服务（当时大约有 60 个，更多人至少使用一个）不仅是简单使用，还提供了惊人的自由。以前，访问每个服务都是卖的，而它仍在通过扫描邮件（它不再这样做了）、大量的搜索以及在`YouTube`上运行各种算法来收集大量数据，却没有一个尊重用户隐私的`gnocial`社交政策。

| 公开 | 用户目录 |
| :--- | :--- |
| | 在`gnocial.net`上按名称、位置或兴趣搜索人员。根据可能显示的三个或更多对结果进行分类： |
| 群组 | |
| 最近标签 | `[关键词] 自由软件 搜索` |
| 热门 | |
| 创建 | 订阅 | 笔记 |

| :--- | :--- | :--- |
| `rms` (`Richard M. Stallman`) | 2016年5月15日 | 2914 |
| 马萨诸塞州剑桥市 | 自由软件基金会创始人 |
| | 回复 | |

## FOSS (开源软件)

如果你不喜欢在`OpenEra`中眯眼睛看微小的爆炸和精灵，那么像素倍增选项非常方便。

爆炸桶

## 开源

## 游戏引擎

就像《毁灭战士 2》中的幽灵战士一样，`Jonni Bidwell`利用一点`FOSS`让丢失的视频游戏尸复活。我们中的一些人回到年轻时的模样。我们中的一些人记得一些精彩的游戏：`Exile`、`Respite`、`Speedball`和`The Chaos`。仅仅谈论它们就让我们想要启动模拟器，但模拟可能很笨拙，而且获取`ROM`也很棘手。得益于开源的魔力，我们可以做得更好。许多经典游戏的引擎已经过逆向工程和翻新，使得原始资产可以无缝地在现代系统上使用。这可以带来完全真实的体验，或者允许添加新功能（更好的图形、网络对战）。更重要的是，如果这能让我们向那些年轻人展示在游戏内聊天中跑动的日子。

## 法律的狭小地带
