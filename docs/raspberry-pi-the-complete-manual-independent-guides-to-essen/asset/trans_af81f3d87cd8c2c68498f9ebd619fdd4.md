
## 修复权限

  03 我们刚刚复制的文件所有者将是 Pi 用户，这不是我们想要的。我们将把 music 目录及其所有子目录的所有权更改为 mpd 用户和 audio 组。

```
sudo chown -R mpd:audio /var/lib/mpd/music
```

## 配置守护进程

  04 我们需要编辑 /etc/mpd.conf。必须使用 sudo 来执行此操作，因此在终端中输入 `sudo nano /etc/mpd.conf`。第一项更改是让守护进程监听所有接口，这样我们就可以使用来自其他设备的 MPD 客户端了。通过将 `bind_to_address "localhost"` 这一行更改为 `bind_to_address "any"` 来实现这一点。

## 配置流媒体

  05 目前，唯一的音频输出是 Pi 上的 3.5mm 接口。要设置流媒体，向下滚动配置文件直到找到被注释掉的 httpd 流媒体输出部分。取消该条目的注释，并将 format 行更改为输出立体声而不是单声道。我们的条目如下所示：

```
audio_output {
type "http"
name "My HTTP Stream"
encoder "vorbis"
port "5600"
quality "5.0"
bitrate "128"
format "44100:16:2"
}
```

保存更改并通过以下方式重启守护进程：

```
sudo /etc/init.d/mpd restart
```

> “MPD 可以将音频输出到连接到系统的任何声卡，包括 iOS 和 Android 设备”

![](img/59caadfa348382a5c408c25137901e27_96_0.png)

## 播放音乐

  08 按下左下角的 Tribe 默认按钮。这将带你进入音乐库的艺术家部分。要播放某位艺术家的音乐，你只需要长按该艺术家，并选择“添加、替换并播放”。如果 Pi 连接了扬声器或耳机，你应该能听到音乐从中播放出来。你可能需要调整“正在播放”界面上的音量滑块，以适应你的需求。

## 设置客户端

  06 在各个不同的平台上使用客户端，仍然需要遍历 /etc/ 设置，但步骤相当容易翻译。对于 Linux，我们推荐 Sonata；对于 Android，我们推荐 MProid；对于 iOS，我们推荐 MPDroid。我们将要在 Android 上设置 MPDroid，所以请前往应用商店下载该应用。

## 连接到服务器

  07 进入 MProid 应用后，选择“MLAN 基于的连接”并选择你的接入点。然后在“Host”字段中填入你 Pi 的 IP 地址，并在“Streaming host”字段中填入相同的详细信息。其余部分应保持默认设置。完成这些设置后，前往“正在播放”界面。我们需要更新音乐库，因为它之前从未被扫描过。为此，按下“菜单”按钮，进入“设置”。然后选择带有“刷新 MPD 数据库”说明的“更新”选项。

## 进一步改进

  09 本文演示了一个非常简单的 MPD 设置。其他可能的改进包括：

- 将音乐放在外部硬盘驱动上，以获得更多的存储空间；
- 根据 Pi 的 CPU 调优流媒体设置，查看用户手册中的编码器插件部分（www.mp3help.org/doc/user/）；
- 设置一个 Samba 共享，以便通过网络访问音乐文件，该共享与所有主要操作系统兼容。

## 项目

### 使用 Python 制作 Pong 游戏克隆

#### 你需要...

- 最新 Raspbian 镜像
    - www.raspberrypi.org/downloads
- Pillow
    - https://github.com/python-imaging/Pillow
- SimpleGUIK
    - https://github.com/dholm/simplegui/

### 使用 Python 制作 Pong 游戏克隆

我们使用一个名为 SimpleGUIK 的新库，为 Linux 世代更新了复古经典游戏 Pong

![](img/59caadfa348382a5c408c25137901e27_97_0.png)

在“Tux for Two”中，这是一个很棒的小 Pong 克隆游戏，它使用了受人喜爱的 Linux 吉祥物 Tux 作为活动的中心。

树莓派是开始学习编程的绝佳方式。对于业余程序员来说，游戏编程是一个非常有益的区域，它能带来更具互动性的结果和更大的成就感。游戏编程还能教授创新能力和高级数学编码技巧。我们将使用 Python 中出色的 SimpleGUIK 模块，这是一种基于 Tkinter 创建图形界面的非常直接的方法。

#### Python 模块准备

1.  前往我们在“你需要”部分列出的网站，从 GitHub 页面下载源文件的压缩包。更新你的 Raspbian 软件包，然后安装以下内容：
    `sudo apt-get install python-dev python-setuptools tk8.5-dev tcl8.5-dev`
2.  打开终端，使用 `cd` 移动到解压后的 .zip 文件夹。进入该目录后，输入：
    `sudo python setup.py install`
    完成后，移动到 **simpleguiK** 文件夹并使用相同的命令安装它。
3.  启动 IDLE 2（而不是 IDLE 3），并打开一个新窗口。使用代码列表来创建我们的游戏“Tux for Two”。务必仔细跟随代码，确保你知道自己在做什么。这样，如果你愿意，就可以自行修改游戏规则。

#### SimpleGUIK 代码

4.  代码开头没有特别复杂的内容，“Tux”和包体的初始位置被设置，同时也设置了 Tux 的初始速度和方向。这些设置也在得分时和重置游戏场地时使用。每次生成时，方向和速度都会设置为随机值。
5.  代码中的关键部分是 **draw**、**line**、**draw**、**image** 和 **draw_text** 函数。这些函数专门来自 SimpleGUIK，允许你轻松地根据位置、大小和颜色在屏幕上放置这些对象。不过，你需要将它们关联到一个对象——在本例中是 **canvas**。这告诉软件我们希望在屏幕上显示这些项目供人们查看。
6.  最后一部分纯粹是为了界面。我们告诉代码在按键按下和释放时要做什么，并给它一个工作的框架。框架是一个实心的白色区域，函数处理图形、按键功能等。最后，我们调用 **frame.start()** 让它开始运行。

#### 安装模块

#### 编写你的代码

#### 设置游戏

#### SimpleGUIK 设置代码

### 使用 Python 制作 Pong 游戏克隆

项目

#### 完整代码列表

```python
import simplegui as simplegui
import random

w, h = 600, 400
tux_r = 20
pad_w = 8
pad_h = 80


def tux_spawm(right):
    global tux_vel, tux_pos
    if right:
        tux_vel = [0, 0]
        tux_pos[0] = w / 2
        tux_pos[1] = h / 2
    else:
        tux_vel = [0, 0]
        tux_pos[0] = w / 2
        tux_pos[1] = h / 2


def tux_spawn(right):
    global tux_vel
    if right:
        tux_vel[0] = random.randrange(2, 4)
        tux_vel[1] = random.randrange(2, 4)
        tux_vel[1] = -random.randrange(1, 3)
    else:
        tux_vel[0] = -random.randrange(2, 4)
        tux_vel[1] = -random.randrange(1, 3)


def start():
    global paddle1_vel, paddle2_vel, score1, score2
    paddle1_vel = 0
    paddle2_vel = 0
    paddle1_pos = [20, h / 2]  # approx. paddle1 position
    paddle2_pos = [w - 20, h / 2]  # approx. paddle2 position
    score1 = 0
    score2 = 0


def draw(canvas):
    global score1, score2, paddle1_pos, paddle2_pos, tux_pos, tux_vel
    if paddle1_pos > (h - (-pad_h / 2)):
        paddle1_pos = (h - (-pad_h / 2))
    if paddle1_pos < (pad_h / 2):
        paddle1_pos = (pad_h / 2)
    else:
        paddle1_pos = paddle1_vel
        paddle2_pos = paddle2_vel
    canvas.draw_line(h / 2, 0, h / 2, h, 4, "Green")
    canvas.draw_line(pad_w / 2, paddle1_pos, pad_h, paddle1_pos + pad_h, pad_w / 2, "Green")
    canvas.draw_line(w - (pad_w / 2), paddle2_pos, w - (pad_w / 2), paddle2_pos + pad_h, pad_w / 2, "Green")
    tux_pos[0] += tux_vel[0]
    tux_pos[1] += tux_vel[1]
    if tux_pos[0] < tux_r or tux_pos[1] > pad_h:
        tux_vel[1] = -tux_vel[1] * 1.1
    if tux_pos[1] < pad_h or tux_pos[0] > pad_w:
        tux_vel[0] = -tux_vel[0] * 1.1
    if tux_pos[0] < pad_w + tux_r:
        if paddle1_pos < (pad_h / 2) or paddle2_pos > (pad_h / 2):
            tux_vel[0] = -tux_vel[0] * 1.1
            tux_vel[1] *= 1.1
            score2 += 1
            tux_spawn(True)
    elif tux_pos[0] > w - pad_w - tux_r:
        if paddle2_pos < (pad_h / 2) or paddle1_pos > (pad_h / 2):
            tux_vel[0] = -tux_vel[0] * 1.1
            tux_vel[1] *= 1.1
            score1 += 1
            tux_spawn(False)
    canvas.draw_image(tux, (265, 2 / 3, 3 / 4, 1 / 2, 3 / 4, 3 / 4), tux_pos, (45, 45))
    canvas.draw_text((str(score1)), [5 / 8, 1 / 8], 4, "Green")
    canvas.draw_text((str(score2)), [3 / 8, 1 / 8], 4, "Green")


def keydown(key):
    global paddle1_vel, paddle2_vel
    if key == simplegui.KEY_MAP['w']:
        paddle1_vel = -acc
    elif key == simplegui.KEY_MAP['a']:
        paddle1_vel = -acc
    elif key == simplegui.KEY_MAP['d']:
        paddle1_vel = acc
    elif key == simplegui.KEY_MAP['s']:
        paddle1_vel = acc
    elif key == simplegui.KEY_MAP['up']:
        paddle2_vel = -acc
    elif key == simplegui.KEY_MAP['down']:
        paddle2_vel = acc
    elif key == simplegui.KEY_MAP['u']:
        paddle2_vel = acc


def keyup(key):
    global paddle1_vel, paddle2_vel
    if key == simplegui.KEY_MAP['w']:
        paddle1_vel = acc
    elif key == simplegui.KEY_MAP['a']:
        paddle1_vel = -acc
    elif key == simplegui.KEY_MAP['d']:
        paddle1_vel = acc
    elif key == simplegui.KEY_MAP['s']:
        paddle1_vel = -acc
    elif key == simplegui.KEY_MAP['up']:
        paddle2_vel = -acc
    elif key == simplegui.KEY_MAP['down']:
        paddle2_vel = acc
    elif key == simplegui.KEY_MAP['u']:
        paddle2_vel = -acc


# frame
frame = simplegui.create_frame("Tux for Two", w, h)
frame.set_draw_handler(draw)
frame.set_keydown_handler(keydown)
frame.set_keyup_handler(keyup)
tux = simplegui.load_image("http://upload.wikimedia.org/wikimedia/commons/a/af/Tux.png")
start()
frame.start()
```
