
# 电子学

![](img/a1548a579bd09ff29b2b92de3f565e63_109_0.png)

SainSmart 的 9 英寸 HDMI/VGA 触摸屏（bit.ly/YGuk48）拥有出色的显示效果，非常适合各种树莓派项目。随 SainSmart 屏幕附带的控制面板可以方便地更改显示设置（如亮度、对比度等）以及输入源（如 HDMI、VGA、AV1 等）。

Adafruit 的终极 GPS 开发板套件为 Navit 和天气功能提供了它们所需的位置数据。除了主控制板外，触摸屏连接到一个四线 USB 控制器，该控制器随后插入树莓派的 USB 端口。

## 嵌入屏幕

我们之前已经讨论过 PiFTF 和 HDMI 树莓派，但这里使用的 SainSmart 触摸屏特别适合许多嵌入式项目。它比 PiFTF 大，但没有 HDMI 树莓派那样大的边框——而且它非常薄——因此它非常适用于安装项目，无论是像真实相框中的照片幻灯片这样简单的东西，还是嵌入到衣柜门中的家庭自动化控制界面。

## 10 校准触摸屏

此时，你可以通过输入以下命令轻松校准触摸屏：

```bash
cd /etc/X11
sudo mkdir xorg.conf.d
cd xorg.conf.d
sudo nano 99-calibration.conf
```

...加入以下内容：

```
Section “InputClass”
    Identifier “calibration”
    MatchProduct “eGalac Inc. USB TouchController”
    Option “SwapAxes” “1”
    Option “InvertX” “1”
EndSection
```

由于坐标轴已被交换，InvertX 实际上反转的是 Y 轴。为了让这些更改生效，请再次进行校准。现在校准大致正确了，请下载 Adafruit 已经打包好的输入校准器。

```bash
wget http://adafruit-download.s3.amazonaws.com/x-input-calibrator_0.7.5-1_armhf.deb
sudo dpkg -i xinput-calibrator_0.7.5-1_armhf.deb
DISPLAY=:0.0 xinput_calibrator
```

`DISPLAY=:0.0` 很有用，因为你可以从任何终端（包括 SSH 会话）运行该程序，并使其出现在触摸屏上。按照提示触摸屏幕上的点。程序完成后，你应该会得到类似以下内容的输出：

```text
Option    “Calibration”    “84 1957 270 1830”
```

将其添加到我们之前创建的 `99-calibration.conf` 文件中，位于其他 Option 条目下方。

## 11 下载地图

Navit 需要地图；请从 [maps.navit-project.org](http://maps.navit-project.org) 下载。你可以使用树莓派上的 web 浏览器，或者从另一台机器下载地图并使用 scp 复制过来。使用预定义区域选项选择你居住的地方。你选择的区域越小，需要处理的数据就越少。例如，英国的地图大小为 608 MB。现在将地图移动到 navit 文件夹：

```bash
mkdir -p /home/pi/.navit/maps
mv /home/pi/Downloads/Your_map /home/pi/.navit/maps/country.bin
```

例如：

```bash
mv /home/pi/Downloads/osm_bbox~9,7,49,6,2,2,61,2.bin /home/pi/.navit/maps/UK.bin
```

## 12 Navit 配置

使用你喜欢的编辑器以 sudo 身份编辑 `/etc/navit/navit.xml`。搜索 openstreetmaps。现在禁用上面的示例地图，启用 openstreetmap 地图集，并将 data 变量设置为你刚才移动地图的位置。在这种情况下，它看起来像这样：

```xml
<!-- Mapset template for openstreetmaps -->
<mapset enabled="yes">
  <map type="binfile" enabled="yes" data="/home/pi/.navit/maps/UK.bin"/>
</mapset>
```

然后搜索类似于以下的 osd 条目：

```xml
<osd enabled="yes" type="compass"/>
```

...并启用你想要的那些——我们建议全部启用。你可能希望比默认地图布局更近距离放大。放大值 64 很有用。

## 构建树莓派车载电脑

## 13 声音配置

在为 Navit 配置语音支持之前，先配置外部声卡。你必须停止加载 Broadcom 模块并删除一些树莓派特有的 ALSA（高级 Linux 声音架构）。为此，以 sudo 身份编辑 /etc/modprobe 并注释掉（即，在前面加上 #）：

```
# snd-bcm2835
```

然后运行：

```bash
sudo rm /etc/modprobe.d/alsa*
```

重启以使更改生效。如果声音太小，请使用 alsamixer 设置声卡的音量。

## 14 下载语音

语音合成软件需要语音和一个专有二进制文件。你可以通过完成以下步骤获取两者：

```bash
sudo mkdir -p /usr/share/mbrola/voices/
wget http://www.tcts.fmsa.ac.be/synthesis/mbrola/voices/en1/en1-980910.zip
unzip en1-980910.zip
sudo cp en1/en1 /usr/share/mbrola/voices/
wget http://www.tcts.fmsa.ac.be/synthesis/mbrola/bin/raspberry-pi/mbrola.tgz
tar zxf mbrola.tgz
sudo mv mbrola /usr/local/bin/
```

## 15 创建语音脚本

Navit 通过运行外部脚本并将要朗读的文本作为参数传递来支持语音。使用以下方法创建一个：

```bash
cd /home/pi/navit
wget http://11iamfraser.co.uk/lud/carsi/chime.wav
touch speech.sh
chmod +x speech.sh
```

现在编辑 speech.sh：

```bash
#!/bin/bash
aplay -r 44100 /home/pi/navit/chime.wav
# espeak -v mb-en1 -s 110 -a 150
# -p 50 "$1"
```

最后，使用以下命令测试它：

```bash
./speech.sh 'Hello World'
```

## 完整代码列表

```python
try:
    r = requests.get(api_req)
except requests.exceptions.RequestException as e:
    return e

return WeatherClient.usedata(r.json())

class CarLauncher:
    def __init__(self):
        pygame.init()
        pygame.mixer.quit() # Don't need sound
        screen_info = pygame.display.info()
        self.screen = pygame.display.set_mode((screen_info.current_w, screen_info.current_h))
        pygame.display.set_caption('Car Launcher')
        self.titlefont = pygame.font.Font(None, 100)
        self.wfont = pygame.font.Font(None, 30)
        self.w_text = None # Weather text

    def clean_background(self):
        background = pygame.Surface(self.screen.get_size())
        self.background = background.convert()
        self.background.fill((0, 0, 0))

        # Render title centered
        text = self.titlefont.render("CarPi Launcher", 1, (255, 255, 255))
        textpos = text.get_rect()
        textpos.centerx = self.background.get_rect().centerx
        self.background.blit(text, textpos)

        self.screen.blit(self.background, (0,0))
        pygame.display.flip()

    def main_menu(self):
        # Since maps text -> Rectangles we can do collision detection on
        self.bttns = {'Music' : None, 'NAV' : None, 'Weather' : None}

        item_num = 1
        for key in self.bttns:
            text = self.titlefont.render(key, 1, (255,255,255))
            textpos = text.get_rect()
            max_width = self.background.get_rect().width / len(self.bttns)
            center_offset = max_width * 0.5
            # This y pos puts buttons just below title
            textpos.centery = self.background.get_rect().centery / 2
            textpos.centerx = (max_width * item_num) - center_offset
            self.bttns[key] = textpos
            self.screen.blit(text, textpos)
            item_num += 1

        pygame.display.flip()

    def select_rect(self, rect, text):
        # Colour a rect the user has clicked in green
        surface = pygame.Surface(rect.w, rect.h)
        surface.fill((0, 255, 0))
        # Also need to draw the text over it again
        t = self.titlefont.render(text, 1, (255,255,255))
        surface.blit(t, (0,0))
        self.screen.blit(surface, rect)
        pygame.display.flip()
```

![](img/a1548a579bd09ff29b2b92de3f565e63_111_0.png)

*上方 Navit 软件内置了大量选项，包含在其菜单层级中*

![](img/a1548a579bd09ff29b2b92de3f565e63_111_1.png)

![](img/a1548a579bd09ff29b2b92de3f565e63_111_2.png)

*上方 音乐播放器 pymidouchigui 前端出乎意料地功能丰富*

## 你需要为 CarPi 编写自己的启动器

## 使其移动化

最好在一个干净的工作区中组装这个项目，这样你可以清楚地看到你在操作什么，并确保所有接线和焊接都正确。但是，这个项目的目的是使这个设置可移动，这样你就可以把它放在车里并在路上使用。你可以将所有设备安装在一个手工制作的外壳中，或者自定义一个大瓶子外壳，也可以将各个部件固定在内，例如你的手套箱或车门内。你还需要用电源包为屏幕和树莓派供电，并确保 GPS 天线固定在一个信号良好的位置。

## 16 配置 Navit 语音

最后一部分很简单。编辑 Navit 配置文件（再次 `/etc/navit/navit.xml`）并替换以下行：

```xml
<speech type="cmdline" data="echo tag in navit.xml to let Navit say: “%s” cps="15"/>
```

...替换为：

```xml
<speech type="cmdline" data="/home/pi/navit/speech.sh %s" cps="10" />
```

现在你可以使用 `DISPLAY=:0.0 navit` 运行 Navit 并进行有趣的实验。

## 17 安装音乐播放器

MPD 是音乐播放器后端，`pymidouchigui` 是需要手动安装的前端：

```bash
sudo apt-get install mpd ncmpcpp
wget http://www.spida.net/projects/software/pymidouchigui/pymidouchigui-0.320.tgz
tar zxvf pymidouchigui-0.320.tgz
cd pymidouchigui-0.320/
sudo python setup.py install
# Fix hard coded path in software
sudo ln -s /usr/local/share/pymidouchigui/ /usr/share/pymidouchigui
```

## 18 复制音乐

这里使用 scp（安全复制协议）来复制音乐。首先运行 `ip addr` 获取树莓派的 IP 地址。然后运行 `sudo passwd` 为 root 设置密码。从一台存有音乐的电脑上，运行：

```bash
scp -r music_folder root@pi_ip_address:/var/lib/mpd/music
```

然后在树莓派上，更改你刚复制的音乐的所有权：

```bash
sudo chown -R mpd:audio /var/lib/mpd/music
```

## 19 更新 mpd 音乐库

`Ncmpcpp` 是 `mpd` 的命令行客户端。输入 `ncmpcpp` 并按 U 更新库。按 3 浏览库并检查音乐是否存在，按 Q 退出。按 1 将选择帮助屏幕，如果你想做更多操作。

## 20 安装 awesome 窗口管理器

现在你需要为 CarPi 编写自己的启动器，它将以全屏运行。为了确保每个应用程序都被强制全屏，请使用 awesome 窗口管理器的全屏模式。

```bash
sudo apt-get install awesome
sudo rm /etc/alternatives/x-session-manager
sudo ln -s /usr/bin/awesome /etc/alternatives/x-session-manager
```

更改默认 x-session-manager 时，awesome 将在启动时自动启动，而不是 LXDE。如果你重启树莓派，awesome 应该会自动加载。

