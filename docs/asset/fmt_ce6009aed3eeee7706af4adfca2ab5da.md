
```
# 首先设置如何与 Twitter 交互

import tweepy, serial, time
API_key = "Ghqh235FJy8wfZrJ1HJ6zg"
API_secret = "9jIbap2o5enkKtS26AWXvXMPAp8jt3HynWZLl9AgDhctLM4"
Access_token = "2392807940-131SoaGQm38NtVjYeURx265P2PEwZGfYbC5vYub1"
Access_token_secret = "1V4aD21s4oerZCaPzAeCPnzRDmE3LSlUiBjYoHYAcWJYk16RJ"
auth = tweepy.OAuthHandler(API_key, API_secret)
auth.set_access_token(Access_token, Access_token_secret)
api = tweepy.API(auth)

# 打开一个 com 端口（你的可能略有不同）
ser = serial.Serial('COM3', 9600)
# 一个无限循环，用于检查传感器警报
while True:
  SerialInput = ser.read(1)
  if SerialInput == 'a--D02HIGH--':
    TimeNow = datetime.datetime.now()
    DS = TimeNow.strftime('%H:%M:%S %d-%b-%Y')
    AlertText = ALERT LLAM device -- Flood sensor triggered @ ' + DS
    print(AlertText)
    api.update_status(AlertText)
    time.sleep(10) #stop fast re-triggering
    ser.flushInput()
```

![img/a1548a579bd09ff29b2b92de3f565e63_48_2.png](img/a1548a579bd09ff29b2b92de3f565e63_48_2.png)

## 打造由树莓派驱动的Bigtrak

取一个玩具、一块树莓派和一个PS3手柄；再添加一点`Python`代码和一些焊料，即可获得一款完美的遥控装置……

![](img/a1548a579bd09ff29b2b92de3f565e63_49_0.png)

![](img/a1548a579bd09ff29b2b92de3f565e63_49_1.png)

#### 所需材料

- Bigtrak

  www.bigtrawktr.co.uk/shop/bigtrak

- 面包板和连接线

- 电机驱动器

  bit.ly/1OnFug

- USB电池包

  amzn.to/1h2PSjl

- PS3 DualShock手柄

树莓派是一款小型、低成本的计算机，旨在培养人们对计算和编程的兴趣——但它不必局限于正经的计算机应用。事实上，在本文中，我们将展示如何使用它把Bigtrak改造成一个机器人。这难道不很有教育意义吗？

Bigtrak是一款能够接收一系列简单指令（前进、左转、右转）并执行它们的玩具。为了让事情更有趣，我们将拆除现有的电路，并用树莓派进行替换，同时使用小型电机驱动器来安全地控制Bigtrak中的电机，然后将其设置为由PlayStation 3 DualShock手柄控制。

软件端所需的一切均已预装在最新的Raspbian OS镜像中，因此我们唯一需要做的，就是编写一个使用`Pygame`和`RPi.GPIO`模块的小型`Python`脚本，将手柄的输入转换为电机的动作。

### 01 打开Bigtrak —— 简单部分

在对Bigtrak进行任何改动之前，我们需要进入其内部。首先，将Bigtrak翻转过来，拆下边缘周围的九颗螺丝。这些螺丝大部分都很容易拆卸，但前面的几个可能需要更细的螺丝刀才能触及。

![](img/a1548a579bd09ff29b2b92de3f565e63_50_0.png)

### 02 打开Bigtrak —— 困难部分

最后两颗螺丝位于背面灰色格栅下方。该格栅由四个塑料卡扣固定，需要将其向内推入，同时使格栅从Bigtrak上滑开。由于额外腾出双手协助的空间有限，这可能比较棘手。你可以在侧面塞入一些薄塑料物品（例如吉他拨片），以保持那两颗卡扣未锁定，同时用手指向内推底部的两个卡扣，使格栅向上滑动，从而拆卸螺丝。

![](img/a1548a579bd09ff29b2b92de3f565e63_50_1.png)

### 03 拆下顶盖

将Bigtrak翻回轮子着地，然后轻轻松开顶盖并向上提起。顶盖通过排线和开关与底座相连，因此只需将顶盖提起足够高的位置，使其倾斜至一侧，即可露出内部。

在顶盖倾斜于一侧的情况下，拆下固定开关的螺丝并将其从顶盖上拆下。接下来，需要拧下PCB板上固定排线的两颗螺丝，让排线滑脱。

断开开关和排线后，顶盖即可分离，最终可以从Bigtrak底座上完全拆除。

### 04 剪断电线

剪断通向主PCB的电线。开关和电源的电线应靠近PCB剪断（以便稍后重新使用），而LED和扬声器的电线则可以在任何位置剪断。

### 05 拆除引擎

将Bigtrak翻转过来，拆下固定引擎的四颗螺丝（这样可以降低电烙铁对主车身造成损坏的可能性）。小心地将Bigtrak翻回正面并提起，直到引擎脱落。

![](img/a1548a579bd09ff29b2b92de3f565e63_50_2.png)

### 硬件部分

电线长度需足以触及Bigtrak的背面，因此要预留足够长度！

![](img/a1548a579bd09ff29b2b92de3f565e63_51_0.png)

![](img/a1548a579bd09ff29b2b92de3f565e63_51_1.png)

![](img/a1548a579bd09ff29b2b92de3f565e63_51_2.png)

### 06 重新接线电机

拆除连接PCB与电机的焊锡（此处使用吸锡带会很方便），然后移除PCB。移除PCB后，我们现在可以连接电线至电机，以便从树莓派而不是机身上的指令驱动电机。电线长度需足以触及Bigtrak的背面，所以要预留足够长度——毕竟，将过长的电线修剪至合适长度比完全替换过短的电线要容易得多！安装好所有电线后，即可将引擎装回Bigtrak。

### 07 连接电机驱动器

电机就位后，我们现在需要搭建电路，以便从树莓派驱动电机。我们使用排线将树莓派的`GPIO`引脚连接至面包板，然后连接至双电机驱动器 [http://proto-pic.co.uk/motor-driver-1a-dual-tb6612fn] 以实际驱动电机。这使得电机所需的高电压远离敏感的`GPIO`引脚。

面包板上的连接如下表所列。这些数值在编写软件时需要用到，且可能因所使用的扩展板和树莓派版本而异。

| 树莓派 GPIO | 电机驱动器 |
| :------- | :----------- |
| 24 | AIN2 |
| 17 | AIN1 |
| 18 | STBY |
| 21 | BIN1 |
| 22 | BIN2 |

将`PWM A`和`PWM B`引脚直接连接到3.3V电源轨后，电机在激活状态下将始终以全速运行。

### 08 安装面包板

面包板将安装在Bigtrak内部电池仓的上方，因此电机的电线应引至装置背面并用扎带固定。电池的电线也可以引至相同位置，以帮助保持整洁。

### 09 将所有部件连接起来

为了轻松连接电机和电池到面包板，我们在电线末端焊接了模块化插头，使其可以直接推入到位（这些插头可从www.maplin.co.uk/modular-connectors-5348 购得）。

安装好面包板（将其粘在适当位置以固定）后，我们可以再次仔细检查所有连接，然后将电机和电源插入。为了知道电机何时被激活（并降低意外移动的可能性），可以将LED连接到面包板，使“待机”引脚激活时LED亮起，并使用电阻确保其不会汲取过多电流而烧毁。

### 10 供电

树莓派的电力由安装于引擎上方的USB电池包提供，该电池包可通过几个扎带或魔术贴固定。这种电池通常作为便携式手机或iPad充电器出售——此处使用的是8000mAh电池，可为树莓派供电长达八小时。

### 11 连接树莓派 —— 添加线缆

由于树莓派将安装在Bigtrak的顶部，我们需要通过外壳顶部将排线和电源线引出。为此，将Bigtrak顶盖翻转过来，并释放固定深灰色塑料的前两个卡扣——这提供了足够大的间隙，以便排线和USB电源线穿过。务必确保排线的红色边缘与面包板连接器正确对齐，以免需要在外壳内部扭转线缆。

### 12 连接树莓派 —— 最后步骤

Bigtrak顶盖复位后，现在可以放置树莓派，保持`GPIO`引脚朝向前面，以便排线轻松连接。至于电池包，我们用扎带和粘胶垫片将其固定。理论上，可以将裸树莓派直接附着在Bigtrak上，但这样做可能导致SD卡边缘受到挤压而弯曲，因此建议使用外壳保护树莓派。

将排线和电源线连接到树莓派，打开电源，它现在就可以接受指令了。在设置软件时，此时连接键盘和显示器到树莓派可能更容易。

### 13 连接PS3手柄
