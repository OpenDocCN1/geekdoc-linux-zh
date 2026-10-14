
team and introduce yourself on their mailing list. If you are interested, one thing in particular that you should look out for is Ubuntu OpenWeek, where all of the Ubuntu teams hold talks and tutorials on IRC. Check out https://wiki.ubuntu.com/UbuntuOpenWeek/ to see when the next one will be.

![](img/f7cef0df22f9dba5a41777808c98eece_411_0.png)

图 20-13：会议上 Ubuntu 的众多贡献者中的一小部分
[image created by Kenneth Wimer; used under Creative Commons license; original can be found at http://en.wikipedia.org/wiki/File:Uds_karmic.jpg]

## 21

## WOUNDED WINGS

修复常见问题

![](img/f7cef0df22f9dba5a41777808c98eece_412_0.png)

与死亡和税收一样，计算机问题是不可避免的生活事实。Ubuntu 也免不了各种烦恼，虽然我感觉在 Ubuntu 上修复问题花费的时间远比以前在 Windows 上少，但最好不要忽视你某天可能会遇到硬件故障或软件卡顿的可能性。

本章的目的是为你提供一些通用提示、技巧和故障排除建议。你会找到修复若干具体问题的明确说明，但总体上我尽量保持讨论的概括性。这是因为解决某些问题的方式会高度依赖于你系统的特殊性，而根本没有足够大的书架来容纳一本能以足够细节覆盖每一种可能情况的指南。幸运的是，互联网上藏有大量与 Ubuntu 相关的指南，所以即使你在这里找不到确切的答案，我也希望你能利用我的提示在网络上找到正确的信息。

如果你遇到了问题，翻阅本章看看是否有能帮上忙的内容。我涵盖了安装、启动、声音和视频、互联网和网络连接、硬盘和存储、显示器和显卡的问题，以及程序冻结或拖慢计算机等令人讨厌的软件问题。如果你没有特定的计算机难题，也可以浏览本章，以便在未来不幸发生时知道该怎么做。或者，你也可以走我偏爱的那条路：为自己泡一杯热饮，然后回到游戏章节（第 17 章）好好放松一下。

### I Can’t Get Ubuntu Installed

无法安装 Ubuntu 是一个特别令人沮丧的问题，因为这意味着你可能错过了本书前 20 章的所有乐趣！不用担心；你可以做很多事情来让 Ubuntu 安装到你的电脑上，如果你仍在挣扎，还可以尝试像从 USB 棒启动这样的替代安装方法，我已在附录 A 中介绍过。

### My Computer Won’t Boot from the CD

如果你尝试从 Ubuntu 安装光盘启动电脑，但从未进入紫色的启动画面（参见第 12 页的“Going for a Dip”），或者电脑每次都直接启动到 Windows，尝试以下选项之一：

**Check the boot order** 当你的电脑启动时（*boots*），它会按设定的顺序检查一系列设备，看它们是否上有操作系统。一旦找到操作系统，电脑就会从该设备启动，并且不会再检查其他设备。这意味着如果硬盘在启动顺序中排在光驱之前，电脑就会从硬盘启动而不是光驱。要从光盘启动，你需要确保光驱在启动顺序中排在最前面。参见第 12 页的“Going for a Dip”以了解如何正确设置启动顺序。

**Check the integrity of the CD** 你可能有一张有故障或损坏的光盘，电脑无法从中启动。可以通过进行 *checksum* 测试来检查光盘是否有故障。校验和有点像指纹；你取出你的 Ubuntu 光盘的校验和，并与已知无故障的 Ubuntu 光盘的校验和进行比较。如果两张光盘之间有哪怕一个微小的差异，校验和也会不同——指纹不匹配。Ubuntu 使用 MD5SUM

