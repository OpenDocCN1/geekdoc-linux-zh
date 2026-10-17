
```python
import skywriter
import signal

@skywriter.tap(repeat_rate=1)## 提高下限
def tap(position):
    if position == 'north':
        MoveArm(1,16,0) # 肘向上
        print("Elbow Up")
```

## 27 添加更多移动

现在向程序中添加一些移动。使用下一行并缩进一个带有 `flick` 语句的 `if` 语句来检查南部位置（第 1 行）。如果在板底部（南部）触摸，它将注册并向下移动手臂（第 2 行）。按 `F` 保存程序，然后运行并测试。

```python
elif position == 'south':
MoveArm(1,32,0) # 肘向下
```

# 教程

![](img/90ce260f8df0a9c6339df2d60332346d_75_0.png)

# 28 为夹爪添加控制

继续构建你制作的手势。在原先的一行代码下方添加另一个 `else-if` 语句来检查新的西侧位置（第 1 行），然后使用手臂命令代码打开夹爪（第 2 行），通过触摸 Skywriter 行来关闭夹爪（第 3 行），然后添加代码到夹爪中（第 4 行）。

```
elif position2 == 'west':
    MoveArm(1,8,0) #夹爪关闭
elif position2 == 'east':
    MoveArm(2,8,0) #夹爪打开
```

# 29 使用任务 (Tasks)

任何 Skywriter 手势都可用于控制手臂。在新的一行中，创建一个新变量将其值设置为 1，然后重复可能任务的速率。创建一个名为 `position1` 的新变量，用以停止 Skywriter 覆盖之前的变量（例如，当你想要移动手臂但保持左转开启时）。在第 4 行检查位置，然后移动将产生效果的位置（第 5 行，这是可选的）。结合上一步，为手臂分配移动代码；例如移动肩膀（第 6 行），

```
@skywriter.tap(repeat_rate=1)
def tap(position):
    print('Tap!')
    if position == 'north':
        print "Shoulder Up!"
        MoveArm(1,64,0,0) #肩膀向上
```

# 30 肩部向下

要让肩膀向下移动，使用与第 27 行相似的格式。在下一行，即与 `if` 语句缩进齐的位置，添加一个 `else-if` 语句来检查对肩膀位置的点击（第 1 行）。添加一个可选语句来显示点击已记录（第 2 行），并添加移动肩膀的命令（第 3 行）。保存并运行你的程序。

![](img/9090ce260f8df0a9c6339df2d60332346d_75_1.png)

```
if position1 == 'south':
    print "Shoulder Down"
    MoveArm(1,28,0) #肩膀向下
```

# 31 汇总

继续以类似的方式创建你的程序，如步骤 26 到 30 所示。首先选择你想要使用的手势类型，然后设置一个变量实体以及 Skywriter 上的手势部分位置，例如：北、南、西。我们可以使用条件语句、`if` 和 `else` 语句来检查位置，并根据完整列表相应地移动手臂。使用教程中的程序作为你想法的基础设置，然后进行扩展和自定义以添加你自己的动作。

# Ryanteck LTD

在 Linux 上使用树莓派扩展板、HAT 和 GPIO。（同时也支持 Windows 和 Mac）

# RTK.6GP10

`https://ryanteck.xyz`

预计于 12 月发货

关注进度请：

`http://ryanteck.com/rtkgpi10`

# MODMYPI

# 树莓派的一切！

树莓派商店 - 我们提供系列转接板、树莓派组合包、SD 卡、外壳、黑客套件和组件 - 全球发货！

`WWW.MODMYPI.COM`

# IQaudio

适用于树莓派的发烧友级配件

# Pi-DAC+

- 树莓派 HAT，无需焊接
- 全高清音频（最高 24bit/192MHz）
- 德州仪器 `PCM5122`
- 可变输出，达 2.1rms
- 耳机放大器 / 3.5mm 插座
- 开箱即用
- 集成硬件音量控制
- 访问树莓派 GPIO
- 连接 Hi-Fi 输入/输出
- 行业标准格式 (`RCA`) 接口
- 支持 `Pi-AMP+`

# Pi-AMP+

- `Pi-DAC` 配件，无需焊接
- 全高清音频（最高 24bit/192MHz）
- 德州仪器 `TPA318`
- 高达 25W 的功率注入
- 为树莓派供电
- 支持软开关
- 使用 `Pi-DAC` 耳机时自动静音
- 输入电压 12-19V
- 支持 4-8 欧姆扬器

# Pi-DigiAMP+

- 树莓派 HAT，无需焊接
- 全高清音频（最高 24bit/192MHz）
- 德州仪器 `TAS5756`
- 高达 25W 的功率注入
- 开箱即用
- 集成硬件音量控制
- 为树莓派供电
- 软件管理
- I/O (`I2c`, 3v, 5v, 0v, `GPIO22/23/24/25`)
- 只需添加扬声器即可完成 Hi-Fi
- 输入电压 12-19V
- 支持 4-8 欧姆扬声器

# 教程

# 使用 Onion Pi 将你的 Pi 变成 Tor 代理

## 将树莓派变成无线访问点以访问匿名 Tor

![](img/90ce260f8df0a9c6339df2d60332346d_77_0.png)

`Nate Drake` 是一位专攻网络安全的科技记者。他为各种杂志编写教程，他的志心是能够负担得起比他的朋友更好的树莓派。

![](img/90ce260f8df0a9c6339df2d60332346d_77_1.png)

```
iptables-persistent

当前规则可以保存到配置文件
/etc/iptables/rules.v4。这些规则将在启动时自动加载。
如果你想保存规则，在安装期间运行 `iptables-save`
```

`iptables-persistent` 会询问你是否保存更改。

# 02 安装必要软件

运行命令 `apt-get update` 然后 `apt-get install isc-dhcp-server iptables` 来安装必要的软件。`iptables-persistent` 会询问你是否保存，两者都选择 `Yes`。在无处不在的监控时代，这比任何时候都要防止广告商和政府监控你的移动。如果你通过 Tor 连接，你的连接是加密的，并通过一系列名为 'onion' 的代理。这减慢了你的连接，但增加了你的隐私。

# 03 配置 DHCP 服务器

运行 `nano /etc/dhcpd.conf`。找到开头的 `domain-name` 和 `interface eth0`。去掉每行的 `#`。按照本教程的步骤将你的 Pi 变成名为 `Onion_Pi` 的无线访问点 (AP)。完成后，使用 `whatismyip.com` 等网站查看你的位置是否已更改。在文件末尾粘贴此。按 `Ctrl+X`，`Y` 然后返回编辑器。

```
subnet 192.168.1.0 mask 255.255.255.0 {
  range 192.168.1.10 192.168.1.200;
  option router 192.168.1.42;
  option default-lease-time 600;
  option domain-name "local";
}
```

Tor 如何工作？

Tor 网络是由志愿者运行的服务器（节点）组成的。当你启动 Pi 时，它会创建电路。每个节点只知道哪里以及去哪里。Tor 每几分钟变换一次身份，追踪你的位置变得极其困难。

![](img/90ce260f8df0a9c6339df2d60332346d_77_2.png)

# 04 编辑 interfaces

运行 `nano /etc/interfaces`。滚动到 `INTERFACES` 部分并插入 `interface eth0 dhcp`。确保 "wan0" 在标记内。运行命令 `sudo systemctl restart networking` 和 `sudo systemctl restart isc-dhcp-server` 让你的更改在启动时生效。如果你的 IP 地址不同不要担心。

# 01 连接到 Pi

将你的 Pi 连接到网线，然后开启接口或连接。运行命令 `ifconfig -a`。你应该看到 `wlan0` 显示模块已启用。

# 05 设置静态 IP

运行 `nano /etc/network/interfaces`。找到 `allow-hotspot wlan0` 并在开头添加 `#` 将其注释掉。将以下行替换为：

```
iface wlan0 static address 192.168.1.2 netmask 255.255.255.0
```
