
```python
@staticmethod
def update():
    errstr = "Error getting weather data"
    lat, lon = WeatherClient.latlon()
    if lat == None or lon == None:
        return
    api_req = ("http://api.worldweatheronline.com/free/v2/weather.ashx?"
               "q={0}%2C{1}&format=json&key={2}").format(lat, lon,
                                                            WeatherClient.apikey)
    r = None
```

#### 13 声音配置

在为 Navit 配置语音支持之前，先配置外部声卡。你需要停止 Broadcom 模块的加载并移除一些 Raspberry-Pi 专用的 ALSA（高级 Linux 声音架构）。为此，使用 `sudo` 编辑 `/etc/modprobe` 并注释掉（即以 `#` 为前缀）：

- `snd-bcm2835`

然后运行：

- `sudo rm /etc/modprobe.d/alsa*`

重启使更改生效。使用 `alsamixer` 来设置音量，如果它太安静的话。

#### 14 下载语音

语音合成软件需要一个语音和一个专有二进制文件。你可以通过完成以下步骤获得两者：

- `sudo mkdir -p /usr/share/mbrola/voices/`
- `wget http://www.tcts.fpms.ac.be/synthesis/mbrola/dba/en1/en1-980910.zip`
- `unzip en1-980910.zip`
- `sudo cp en1/en1 /usr/share/mbrola/voices`
- `wget http://www.tcts.fpms.ac.be/synthesis/mbrola/bin/raspberrypi/mbrola.tgz`
- `tar zxvf mbrola.tgz`
- `sudo mv mbrola /usr/local/bin/`

#### 15 创建语音脚本

Navit 通过运行外部脚本并将要朗读的文本作为参数传递来支持语音。使用以下命令创建它：

- `cd /home/pi/.navit`
- `wget http://liamfraser.co.uk/lud/carpi/chime.wav`
- `touch speech.sh`
- `chmod +x speech.sh`

现在编辑 `speech.sh`：

```bash
#!/bin/bash
aplay -r 44100 /home/pi/.navit/chime.wav
espeak -vmb-en1 -s 110 -a 150 -p 50 "$1"
```

最后，使用以下命令测试它：

- `./speech.sh "Hello World"`

### 完整代码列表

```python
try:
    r = requests.get(api_req)
except requests.exceptions.RequestException as e:
    return errstr

return WeatherClient.usefuldata(r.json())

class CarLauncher:
    def __init__(self):
        pygame.init()
        pygame.mixer.quit() # Don't need sound
        screen_info = pygame.display.Info()
        self.screen = pygame.display.set_mode((screen_info.current_w,
                                               screen_info.current_h))
        pygame.display.set_caption('Car Launcher')
        self.titlefont = pygame.font.Font(None, 100)
        self.wfont = pygame.font.Font(None, 30)
        self.w_text = None # Weather Text

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
        # btns maps Text -> Rectangles we can do collision detection on
        self.btns = {'Music' : None, 'NAV' : None, 'Weather' : None}
        item_num = 1
        for key in self.btns:
            text = self.titlefont.render(key, 1, (255,255,255))
            textpos = text.get_rect()
            max_width = self.background.get_rect().width / len(self.btns)
            center_offset = max_width * 0.5
            # This maps btns buttons just below the title
            textpos.centery = self.background.get_rect().centery / 2
            textpos.centerx = (max_width * item_num) - center_offset
            self.btns[key] = textpos
            self.screen.blit(text, textpos)
            item_num += 1
        pygame.display.flip()

    def select_rect(self, rect, text):
        # Colour red to green when clicked in green
        surface = pygame.Surface((rect.w, rect.h))
        surface.fill((0, 255, 0))
        # Now we have to draw the text over it again
        t = self.titlefont.render(text, 1, (255,255,255))
        surface.blit(t, (0,0))
        self.screen.blit(surface, rect)
        pygame.display.flip()
```

## 使用 Python 与 Pi

![](img/3b256f430f51c98f1315671f6e4eec19_171_0.png)

上方 Navit 软件在其菜单层级中内置了大量选项

![](img/3b256f430f51c98f1315671f6e4eec19_171_1.png)

上方 `pympdtouchgui` 是音乐播放器的前端，功能出乎意料地丰富

### 你需要为 CarPi 编写自己的启动器
