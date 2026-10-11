
星体的数量会根据显示分辨率进行调整

## 完整代码列表

![](img/0fc17bd4c29dc437e3ac28a53f7559db_76_0.png)

## 10 放置玩家

是时候确定玩家绘制的位置并调整视角了。玩家的位置会在两个不同位置进行计算并取平均值，以匹配多边形和平行视差效果。圆上某点的位置计算如下：

```
x = cos( angle ) * radius
y = sin( angle ) * radius
```

正弦和余弦的零值中心位于原点，因此我们需要在玩家的 X 和 Y 坐标中加入屏幕中心点。玩家中心是通过半径乘以玩家角度的余弦值，再加上屏幕中心计算得出的。

## 11 固定速度

`moveCount` 和 `moveDelay` 变量用于固定玩家在游戏关卡中的移动速度，无论关卡包含多少个部分。

下一节代码检查玩家位于屏幕的哪个象限，并相应地移动中心点。游戏区域每帧移动几个像素，直到受到以下限制：

```
if centerX < ( gwidth / 2 ) + ( gwidth / 20 )
```

最后，使用 `polypot` 命令计算并绘制玩家的位置。角度被固定，使得玩家面向中心，并且大小会根据显示分辨率进行缩放。

## 12 构建多边形

`polystart` 命令允许通过一系列线条构建多边形并自动填充。

与其在每个 `polystart` 语句中的每个绘图操作中计算自动求和，我们提前使用 c = cos( pAngle + 90 ) 和 s = sin( pAngle + 90 ) 进行了计算，u 则是飞船相对于显示分辨率的比例。

## 13 多边形方程

多边形上的每个 X 坐标点基于（比例 * 线长）乘以 cos( playerAngle + 90 )，减去（比例 * 线长）乘以 sin( playerAngle + 90 )，再加上 playerX。对于 Y 坐标，则是（比例 * 线长）乘以 sin( playerAngle + 90 ) 加上（比例 * 线长）乘以 cos( playerAngle + 90 ) 再加上 playerY。

## 14 实验变量

最后底部的 `update` 语句将临时帧缓冲区复制到屏幕显示…… 搞定！

有很多变量可以实验，不妨随意更改数字看看会发生什么。这样做能让你深入了解内部机制。

下个月我们将添加敌人、开火功能，也许还会加上一些音效。粒子激光棒极了！

```
# Calculate player position
pX = ( ( radius * cos( pAngle - ( gap / 2 ) ) + centerX ) +
( ( radius * cos( pAngle + ( gap / 2 ) ) + centerX ) ) / 2
pY = ( ( radius * sin( pAngle - ( gap / 2 ) ) + centerY ) +
( ( radius * sin( pAngle + ( gap / 2 ) ) + centerY ) ) / 2
angle = 0

if moveCount > 0 then
    moveCount = moveCount - 1
end
```

```
# move the center of closer objects more
if pX + 2 < gwidth / 2 then // check the players position
    if centerX < ( gwidth / 2 ) + ( gwidth / 20 ) then
        centerX = centerX + 4
        centerY2 = centerY2 + 2
    end
end

if pX - 2 > gwidth / 2 then
    if centerX > ( gwidth / 2 ) - ( gwidth / 20 ) then
        centerX = centerX - 4
        centerY2 = centerY2 - 2
    end
end

if pY + 2 < gheight / 2 then
    if centerY < ( gheight / 2 ) + ( gheight / 20 ) then
        centerY = centerY + 4
        centerY2 = centerY2 + 2
    end
end

if pY - 2 > gheight / 2 then
    if centerY > ( gheight / 2 ) - ( gheight / 20 ) then
        centerY = centerY - 4
        centerY2 = centerY2 - 2
    end
end

colour = yellow
c = cos( pAngle + 90 ) // correct the view angle by 90 degrees
s = sin( pAngle + 90 )
u = gheight / 80 // scale the player ship to the resolution
```

```
# rotate & scale coordinates; draw player ship
polystart
polypot((u*(5 * c) - (u*5 * s) + pX), (u*(5 * s) + (u*(5 * c) + pY))
polypot((u*(5 * c) + pX), (u*(5 * s) + pY))
polypot((0 - (u*2 * s) + pX), (u*(-2 * s) + pY))
polypot((u*(-4 * c) + pX), (u*(-5 * s) + pY))
polypot((u*(-5 * c) - (u*(5 * s) + pX), (u*(-5 * s) + (u*(5 * c) + pY))
polypot((0 - (u*4 * s) + pX), (u*(-4 * s) + pY))
polypot((u*(-7 * c) + pX), (u*(-7 * s) + pY))
polypot((u*(7 * c) + pX), (u*(7 * s) + pY))
polyend
update
repeat
end
```

## 中奖！FUZE 特别版

### 报名截止日期
2016 年 2 月 10 日

拥有鲜明复古风格的 FUZE 是一款屡获殊荣的可编程计算机和电子工作站。它源于对编程的热情和对电子学的热爱，坚固的铝合金机身集成了键盘、专为设计的 GPIO 接针以及用于简单电子电路的洞洞板。树莓派被安全地安置在键盘下方，FUZE 出厂时已预装 FUZE BASIC 操作系统。

FUZE BASIC 是 BASIC 编程语言的高级现代化版本，被广泛认为是最容易教学和最易上手的编程语言。它具备重新设计界面和高级图形支持，包括精灵和图片缩放、角度和透明度控制以及旋转功能，FUZE BASIC 已全面适配所有型号的树莓派。整个 FUZE 系统流畅且直观，完全能够胜任网页和移动游戏的编程开发。

FUZE 特别版向 20 世纪 80 年代的经典家用计算机（如 BBC Micro）致敬，并附带一套可与项目集成的机械臂套件。FUZE 特别版还为您提供项目包并引导您访问 FUZE Lair 上的丰富在线资源，为您提供所需的一切以开始您的项目。更多信息请访问 www.fuze.co.uk。

### 参与比赛

想要赢取 FUZE T2-SE —— 即附带机械臂套件的特别版，请点击下方链接。回答该网页上的简单问题，然后添加您的联系方式即可参与比赛。三名获奖者将在新年揭晓 —— 祝您好运！

![](img/0fc17bd4c29dc437e3ac28a53f7559db_77_0.png)

教孩子们编程

回答该网页上的问题，赢取奖品！

www.linuxuser.co.uk/news/win-a-fuze-se

**条款与细则**
本比赛面向英国和爱尔兰居民开放。Imagine Publishing 有权将奖品更换为价值相同或更高的类似物品。Imagine Publishing 的员工（包括自由职业者）、其亲属或任何代理人不符合参赛资格。编辑的决定为最终决定，恕不接受通讯咨询。奖品不可兑换现金。完整条款和细则可随时索取。参与比赛即表示您同意 Imagine Publishing 向您发送每月电子邮件通讯和偶尔的特别优惠。您可以随时通过点击任何收到的邮件中的退订链接取消订阅。

## 物联网？

无线设备含税低至 £9.99

![](img/0fc17bd4c29dc437e3ac28a53f7559db_78_0.png)

wirelessthings.net/lxu-offer
@wirelessthings

## PCI Express 有限公司

![](img/0fc17bd4c29dc437e3ac28a53f7559db_79_0.png)

TBS 是数字电视调谐器的专业制造商

其产品包括：

- DVB-S/S2 (标清卫星 & 高清卫星)
- DVB-T/T2 (标清地面波 & 高清地面波)
- DVB-C (标清有线电视)
- IPTV 流媒体播放器
- USB 电视调谐器

提供多种选择：
单调谐器、双调谐器、四调谐器
通用接口 (CI)
以及全新的 MINI 调谐器（7220 见下文）

所有 TBS 调谐器均兼容 Windows 7 媒体中心，并支持最新内核的 Linux。

## 为您的 PC 获取最好的数字电视调谐器！

![](img/0fc17bd4c29dc437e3ac28a53f7559db_79_1.png)

兼容 EUMETSAT

### TBS 6908 专业级高清 DVB-S2 四调谐器 PCIe 卡

TBS6908 是一款具有 PCI Express 接口的专业级数字卫星电视调谐器卡。它不仅支持普通卫星接收机支持的常规 DVB-S2/DVB-S QPSK、BPSK，还支持大多数卫星接收设备无法支持的 CCM、ACM、VCM、多输入流、16APSK、32APSK 和通用流模式。
使用专用的 TBS 工具，可以捕获这些特殊流。Windows BDA 驱动程序和 Linux 驱动程序（支持到最新内核 3.X）均已就绪。
建议零售价 £329.95

![](img/0fc17bd4c29dc437e3ac28a53f7559db_79_2.png)

### TBS 6905 高清 DVB-S2
四调谐器 PCIe 卡

TBS6905 是一款 PCI Express 接口的数字卫星电视调谐器卡，配备四个调谐器，用于在 PC 上观看和录制 FTA（免费收看）卫星电视。四个调谐器允许您同时观看来自一个转发器或卫星的电视频道，并接收来自不同转发器/卫星的另外三个频道。它兼容 Windows 7 媒体中心以及 MediaPortal、DVBlink、DVBDream、DVBViewer、ProgDVB、SkyNet、T$reader、XBMC 和 MythTV 等流行软件。
建议零售价 £179.95

![](img/0fc17bd4c29dc437e3ac28a53f7559db_79_3.png)

### TBS 6290 DVB-T2/T/C
双调谐器双 CI PCIe 卡

TBS6290 是最新的 DVB-T2/T PCI Express 调谐器，它配备双调谐器和双 CI 插槽，允许您同时享受两个实时的地面波电视频道和两个不同的频率，并且支持 FTA（免费收看）电视频道和加密电视频道的接收。TBS6290 可作为数字视频录像机使用，用于录制支持全高清的无线数字电视和有线电视程序，具备时间平移功能。
建议零售价 £179.95

![](img/0fc17bd4c29dc437e3ac28a53f7559db_79_4.png)

我们最小的卡！

### TBS 7220 DVB-T2/T/C mini PCIe 卡

TBS 7220 DVB-T2/T/C 电视调谐器 mini PCIe 卡是一款添加了 DVB-C 功能的数字地面波调谐器卡，允许您在 PC 上享受免费收看 (FTA) 的数字地面波/有线电视和数字立体声广播。TBS 7220 可作为数字视频录像机使用，用于录制支持全高清的数字地面波/有线电视程序。它还允许您使用时间平移功能暂停实时广播并从中断处继续观看。它是观看英国 Freeview 标清和高清的理想选择。建议零售价 £69.95

## 请访问我们的网站了解更多精彩的 TBS 产品
WWW.TBSCARDS.CO.UK

## 独家优惠

在 www.tbcards.co.uk 在线购买，使用代码：LINUXUD 可享受任何 TBS 产品 9 折优惠

欢迎垂询商务事宜
E: mike@pcixex.co.uk

在线购买：
www.radtv.co.uk
www.valueav.co.uk
www.amazon.co.uk

