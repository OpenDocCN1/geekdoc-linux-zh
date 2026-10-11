
纸质订阅：续订、更改地址、支付账单、查看账户详情或其他订阅咨询均可即时在线完成，适用于美国和加拿大。您可免费致电：`1-888-66-LINUX` (`54639`)，或发送电子邮件至 `subs@linuxjournal.com` 或 `2677-E`。也可以通过邮寄至：`Linux Journal, PO Box 986585, Houston, TX 77239-6835, USA`。请联系时务必附上您的姓名和地址。

数字订阅：`Linux Journal` 的数字订阅现已可用，以 `PDF` 形式全球交付，价格低廉。请访问 [www.linuxjournal.com/digital](http://www.linuxjournal.com/digital) 获取更多信息，或对上述任何数字杂志客户服务查询使用上述联系方式。

致编辑的信：我们欢迎您的来信，并鼓励您将其发送至 `letters@linuxjournal.com` 或邮寄至 `Linux Journal, 1752 New Market Street, #202, Seattle, WA 98107 USA`。来信可能会因篇幅和清晰度进行编辑。

为我们要写作：我们始终在寻找为杂志贡献的文章、教程和真实故事。作者指南、主题列表和创意示例可在网上找到。[www.linuxjournal.com/author](http://www.linuxjournal.com/author)

广告：`Linux Journal` 是读者和广告商的绝佳资源。请访问我们的网站请求媒体资料包，查看当前编辑日历和广告截止日期，或了解更多其他广告和市场机会。[www.linuxjournal.com/advertising](http://www.linuxjournal.com/advertising)。如需进一步信息，请直接联系我们。[ads@linuxjournal.com](mailto:ads@linuxjournal.com) 或 `+1 713-344-1956` 分机 `2`。

## 在线

网站：在 `Linux Journal` 网站上阅读独家和在线内容。[www.linuxjournal.com](http://www.linuxjournal.com)。此外，印刷版杂志中的一些文章也可在线获取。杂志订阅者（数字或纸质）可获得这些文章的完整访问权限，详情请联系客户服务。[sll@linuxjournal.com](mailto:sll@linuxjournal.com)

免费订阅简报：每周，`Linux Journal` 编辑将告诉您 `Linux` 世界的最新动态。接收突发新闻链接、技术技巧以及今日精选的深度报道提示。[www.linuxjournal.com](http://www.linuxjournal.com)/e-newsletters。

### 新！

**微型 WiFi 控制器**

**1.1 秒启动 Linux**

![](img/3c4d8a97b5d96c835281dc0dacbc8551_11_0.png)

- 仅 `CPU` 板 $129
- 如所示 $249
- 10 件起享批量折扣

### 200 MHz CPU

- `TS-7400` `CPU` 板
- 低功耗、低热量、长寿命
- 板载 `Flash` 最高 `128MB`
- 最高 `128M SDRAM`
- `SD Flash` 卡插槽
- 1 个外部 `USB` 端口
- 1 个 `10/100` 以太网
- `802.11g` 内部 `WiFi` 选项
- 一体式坚固铝制外壳选项，尺寸为 `1.1" x 4.9" x 9.1"`

> 与我们的工程师一起设计您的解决方案

- 超过 20 年经营历史
- 从未停产任何产品
- 工程师提供技术支持
- 提供定制配置和设计，价格优异，周转迅速
- 大多数产品有库存，可次日发货

> 访问我们的网站了解选项、外设和 `x86 SBC`

![](img/3c4d8a97b5d96c835281dc0dacbc8551_11_1.png)

## 技术系统（Technologic SYSTEMS）

我们使用我们的产品。

访问由 `TS-7200` 驱动的我们的网站

[www.embeddedARM.com/7400wifi](http://www.embeddedARM.com/7400wifi)

`(480) 837-5200`

### 经验、想象力与支持。

#### Pogo Linux 是为 Linux 构建的硬件解决方案，也是为您构建的。

如需开始使用，请拨打 `888.828.POGO` 或发送电子邮件至 `inquiries06@pogolinux.com` 与我们联系。

`Pogo Linux, Inc. 701 Fifth Ave. Suite 6850, Seattle, WA 98104`

`Intel`、`Intel` 标志、`Intel Inside` 标志、`Pentium`、`Xeon` 以及 `Xeon Inside` 是 `Intel` 公司或其子公司在美国和其他国家的商标或注册商标。有关更多条款和条件，请访问 `www.pogolinux.com`。

---

### 前沿

#### 新闻 + 趣味

#### diff -u

#### 内核开发中的新动态

如果几个遗留问题能够解决，内核很快将支持更大的编译二进制文件大小。`Eric Biederman` 已经有一些用于实现这一目标的补丁流传了一段时间，`IBM` 的 `Vivek Goyal` 一直在测试这些补丁。根据 `Vivek` 的说法，现在是时候将 `Eric` 的补丁（包含修改内容）展示给更广泛的受众，并将其纳入 `Andrew Morton` 的 `-mm` 树中。许多人似乎很高兴看到这些补丁，并且来自内核各方的人员正在投入大量额外工作。其中一些工作以清理的形式出现，但也有人正在处理这段代码与 `swapoff 软件挂起代码` 之间复杂的交互关系。看起来这些补丁迟早会完成并被接受进官方树中。

开源的 `ar5k 无线驱动程序` 已经排除了所有版权问题，至少根据 `软件自由法律中心` (`SFLC`) 的说法是这样。该驱动程序主要为 `OpenBSD` 开发，主要由 `Reyk Floeter` 开发，长期以来一直笼罩在 `Atheros`（支持其无线芯片组的制造商）的怀疑之下。尽管从未有证据表明 `ar5k` 开发人员存在问题，但“丑闻”足以阻止 `Linux` 人士将该驱动程序纳入 `Linux` 内核。随着 `SFLC` 的意见出台，最强烈的反对意见已被搁置，甚至完全消除，如今内核人士最大的抱怨是 `ar5k` 驱动程序可能写得不好或方法不当。目前，一些人支持将 `ar5k` 以当前形式或稍作修改后纳入内核，而另一些人则认为应该彻底废弃该驱动程序，仅将其作为全新驱动程序的硬件参考。无论辩论结果如何，可以明确的是，`Atheros` 无线芯片将很快拥有 `Atheros` 自家专有 `MadWiFi` 驱动之外的免费替代方案。

许多补丁已经出现，旨在移除内核中损坏或无人维护的部分，或在弃用期后计划移除它们。`Andrew Morton` 已计划在 2007 年 6 月移除 `FUTEX_FD`，并称该代码存在“无法修复的竞争条件”——这正是早年 `DevFS` 受到的指责。`Rusty Russell` 最初编写了该补丁，他对保留该代码没有兴趣。然而，他表示一旦移除，`futex` 代码可以简化很多。有了这样的一些朋友，`FUTEX_FD` 不需要敌人，而且很有可能连 `Andrew` 给它预留的时间都撑不到。

与此同时，`Adrian Bunk` 已提交补丁，移除一系列多年来被标记为损坏的旧驱动程序。这些包括 `VIDEO_ZR36120` 和 `SKMC` 驱动程序，以及 `MAC89x0`、`ATARI_BIONET` 和 `ATARI_PAMSTER` 驱动程序。对于后三者，`Geert Uytterhoeven` 可能有一个由 `Matthias Urlichs` 编写的补丁，用于修复 `MAC89x0` 驱动程序。但该补丁仍需测试和签署。与此同时，`Adrian` 已提交更多补丁，移除 `FB_CYBER_FB`、`FB_VIRGE`、`FB_RETINA23`、`FB_ATARI`、`FB_SUN3` 和 `FB_PM3` 驱动程序，但看起来 `James Simmons` 可能会接管维护它们，而且 `GEERT` 可能已经有一个修复 `FB_ATARI` 驱动程序的补丁。因此，这些帧缓冲驱动程序可能最终不会被移除。

同时，`sysctl 代码` 原本看似真的要被砍掉，但现在似乎得到了宽限。曾计划移除该代码的 `Eric Biederman` 发现了一些合法的 `sysctl` 用户。因此，该代码不仅不再被标记为弃用，而且在不久的将来还会默认编译到所有内核中。`Eric` 将与各个发行版合作，逐步消除 `sysctl` 的使用，并在一年或两年后再次考虑移除该代码。
