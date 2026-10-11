
## 用 Python 制作游戏

### 03 编写你的代码

启动 IDLE 2 而不是 IDLE 3，并打开一个新窗口。使用代码列表创建我们的游戏“Tux for Two”。请仔细跟随代码操作，确保你清楚自己在做什么。这样，如果你愿意，就可以对游戏规则进行自己的修改。

### 04 设置游戏

代码的开头没有什么开创性的地方：设置了 Tux 和球拍的初始位置，以及 Tux 的初始速度和方向。这些值也用于得分后重置比赛场地。每次生成时，方向和速度会被设置为随机值。

### 05 SimpleGUI 代码

绘制函数中的重要部分包括 `draw.line`、`draw.image` 和 `draw.text` 函数。这些专门来自 SimpleGUI，允许你轻松地在屏幕上放置这些对象，并指定其位置、大小和颜色。不过，你需要将它们绑定到一个对象上——在本例中是 `canvas`。

### 06 SimpleGUI 设置代码

最后的部分纯粹用于界面。我们告诉代码当按键被按下然后释放时要做什么，并给它一个框架来运行。然后告诉框架哪些函数处理图形、按键等功能。最后，我们调用 `frame.start()` 使其开始运行。

### 完整代码列表

![](img/a1548a579bd09ff29b2b92de3f565e63_26_0.png)

```python
import simplegui as simplegui
import random

w = 600
h = 400
tux_r = 20
pad_w = 8
pad_h = 80

def tux_spawn(right):
 global tux_pos, tux_vel
 tux_pos = [0,0]
 tux_vel = [0,0]
 tux_pos[0] = w/2
 tux_pos[1] = h/2
 if right:
  tux_vel[0] = random.randrange(2, 4)
 else:
  tux_vel[0] = -random.randrange(2, 4)
 tux_vel[1] = -random.randrange(1, 3)

def start():
 global paddle1_pos, paddle2_pos, paddle1_vel, paddle2_vel
 global score1, score2
 tux_spawn(random.choice([True, False]))
 score1, score2 = 0,0
 paddle1_vel, paddle2_vel = [0,0]
 paddle1_pos, paddle2_pos = h/2, h/2

def draw(canvas):
 global score1, score2, paddle1_pos, paddle2_pos, tux_pos, tux_vel
 if paddle1_pos > (h - (pad_h/2)):
  paddle1_pos = (h - (pad_h/2))
 elif paddle1_pos < (pad_h/2):
  paddle1_pos = (pad_h/2)
 else:
  paddle1_pos += paddle1_vel
 if paddle2_pos > (h - (pad_h/2)):
  paddle2_pos = (h - (pad_h/2))
 elif paddle2_pos < (pad_h/2):
  paddle2_pos = (pad_h/2)
 else:
  paddle2_pos += paddle2_vel
 canvas.draw.line([w / 2, 0], [w / 2, h], 4, "Green")
 canvas.draw.line([0, paddle1_pos + (pad_h/2)], [pad_w/2, paddle1_pos - (pad_h/2)], pad_w, "Green")
 canvas.draw.line([w - (pad_w/2), paddle2_pos - (pad_h/2)], [w - (pad_w/2), paddle2_pos + (pad_h/2)], pad_w, "Green")
 tux_pos[0] += tux_vel[0]
 tux_pos[1] += tux_vel[1]
 if tux_pos[1] < tux_r or tux_pos[1] > h - tux_r:
  tux_vel[1] = -tux_vel[1]
 if tux_pos[0] < pad_w + tux_r:
  if (paddle1_pos + (pad_h/2)) >= tux_pos[1] >= (paddle1_pos - (pad_h/2)):
   tux_vel[0] = -tux_vel[0]
   tux_vel[1] = -tux_vel[1]
  else:
   score2 += 1
   tux_spawn(True)
 elif tux_pos[0] >= w - pad_w - tux_r:
  if (paddle2_pos + (pad_h/2)) >= tux_pos[1] >= (paddle2_pos - (pad_h/2)):
   tux_vel[0] = -tux_vel[0]
   tux_vel[1] = -tux_vel[1]
  else:
   score1 += 1
   tux_spawn(False)
 canvas.draw_image(tux, (265 / 2, 314 / 2), (265, 314), tux_pos, (45, 45))
 canvas.draw_text(str(score1), [150, 100], 30, "Green")
 canvas.draw_text(str(score2), [450, 100], 30, "Green")

def keydown(key):
 global paddle1_vel, paddle2_vel
 acc = 3
 if key == simplegui.KEY_MAP["w"]:
  paddle1_vel += acc
 elif key == simplegui.KEY_MAP["s"]:
  paddle1_vel -= acc
 elif key == simplegui.KEY_MAP["down"]:
  paddle2_vel += acc
 elif key == simplegui.KEY_MAP["up"]:
  paddle2_vel -= acc

def keyup(key):
 global paddle1_vel, paddle2_vel
 acc = 0
 if key == simplegui.KEY_MAP["w"]:
  paddle1_vel = acc
 elif key == simplegui.KEY_MAP["s"]:
  paddle1_vel = acc
 elif key == simplegui.KEY_MAP["down"]:
  paddle2_vel = acc
 elif key == simplegui.KEY_MAP["up"]:
  paddle2_vel = acc

frame = simplegui.create_frame("Tux for Two", w, h)
frame.set_draw_handler(draw)
frame.set_keydown_handler(keydown)
frame.set_keyup_handler(keyup)
tux = simplegui.load_image("http://upload.wikimedia.org/wikipedia/commons/a/f/tux.png")
start()
frame.start()
```

## Raspberry Pi 定格动画

认为自己会是下一个尼克·帕克（Nick Park）吗？搭建这个 DIY 定格动画工作室，看看你能创作出什么作品。

### 所需材料

- 最新版本的 Raspbian www.raspberrypi.org/downloads
- picamera Python 模块 picamera.readthedocs.org
- RasPi 相机模块
- Pygame www.pygame.org

Pi-Mation 可通过 GitHub 上的 https://github.com/russb78/pi-mation 获取

Raspberry Pi 相机模块为你的 Pi 项目敞开了摄影和电影制作的大门。我们将两者结合，创建一个功能齐全的定格动画应用程序 Pi-Mation，让创建令人印象深刻的 HD 动画变得极其简单。

这个项目是用 Python 编写的，它依赖于两个你需要安装的库。Picamera (picamera.readthedocs.org) 是 Raspberry Pi 相机模块的纯 Python 接口，是所有相机模块拥有者的必备工具。Pygame (www.pygame.org)，确保我们的图像可以随时显示。

### 01 设置相机模块

首先，你需要确保你的 Raspberry Pi 是最新的。在终端中输入：

```bash
sudo apt-get update && sudo apt-get upgrade
```

接下来，我们需要更新 Pi 的固件并确保相机模块已激活。请记住，这需要一些时间。

```bash
sudo rpi-update
sudo raspi-config
```

### 02 安装其他依赖项

接下来，我们将确保 Pygame 和 picamera 已安装：

```bash
sudo apt-get install python-setuptools
easy_install -user picamera
```

最后，要安装 Pygame 和视频应用程序，请输入：

```bash
sudo apt-get install python-pygame
sudo apt-get install libav-tools && sudo apt-get install omplayer
```

![](img/a1548a579bd09ff29b2b92de3f565e63_27_0.png)

### 03 最终设置

我们将使用 Git 安装 Pi-Motion，所以请确保它已安装：

```bash
$ sudo apt-get install git
```

打开终端，导航到你的主目录（使用 `cd ~`），然后输入：

```bash
$ git clone https://github.com/russb78/pi-motion.git
```

如果你操作代码并弄坏了它，可以使用以下命令将其恢复到原始状态：

```bash
$ git checkout pi-motion.py
```

### 04 运行和测试 Pi-Motion

现在进入 pi-motion 文件夹并使用以下命令运行应用程序：

```bash
$ python pi-motion.py
```

按下空格键会调用主()循环中的 `take_pic()`，它保存一张图像并创建一个预览，该预览由 `update_display()` 加载。Tab 键被编码为通过要求两个变量切换值来在两种状态之间切换。

### 05 开始动画

main() 循环在每秒大约更新屏幕 30 次之前检查键盘事件。由于相机的实时预览独立于该循环工作，`update_display()` 只需要担心更新预览图像 (prev_pic)。空格键调用 `take_pic()` 并添加到 `pics_taken`，只显示最新拍摄的照片。`animate()` 函数本质上是 `update_display()` 的微流。当按下 P 键时，实时预览暂停，对于所有拍摄的照片 (pics_taken)，每一张都会在主窗口上“位块传输”（更新）。

### 完整代码列表

```python
import pygame, picamera, os, sys

pics_taken = 0
current_alpha, next_alpha = 128, 255
fps = 5

pygame.init()
res = pygame.display.list_modes() # return the best resolution for your monitor
width, height = res[0]
print('Reported resolution is:', width, "x", height)
start_pic = pygame.image.load(os.path.join('data', 'start_screen.jpg'))
start_pic_fix = pygame.transform.scale(start_pic, (width, height))
screen = pygame.display.set_mode(width, height)
pygame.display.toggle_fullscreen()
pygame.mouse.set_visible = False
play_clock = pygame.time.Clock()
camera = picamera.PiCamera()
camera.resolution = (width, height)

def take_pic():
    global pics_taken, prev_pic
    pics_taken += 1
    camera.capture(os.path.join('pics', 'image_' + str(pics_taken) + '.jpg'), use_video_port=True)
    prev_pic = pygame.image.load(os.path.join('pics', 'image_' + str(pics_taken) + '.jpg'))

def delete_pic():
    global pics_taken, prev_pic
    if pics_taken >= 1:
        pics_taken -= 1
        prev_pic = pygame.image.load(os.path.join('pics', 'image_' + str(pics_taken) + '.jpg'))

def animate():
    camera.stop_preview()
    for pic in range(1, pics_taken):
        anim = pygame.image.load(os.path.join('pics', 'image_' + str(pic) + '.jpg'))
        screen.blit(anim, (0, 0))
        play_clock.tick(fps)
        pygame.display.flip()
    camera.start_preview()

def update_display():
    screen.fill((0,0,0))
    if pics_taken > 0:
        screen.blit(prev_pic, (0, 0))
        play_clock.tick(30)
        pygame.display.flip()

def make_movie():
    camera.stop_preview()
    print("\nQuitting Pi-Motion to transcode your video.")
    os.system('avconv -r ' + str(fps) + ' -i "pics/image_%d.jpg" -vcodec libx264 video.mp4')
    sys.exit(0)

def change_alpha():
    global current_alpha, next_alpha
    camera.stop_preview()
    current_alpha, next_alpha = next_alpha, current_alpha
    return next_alpha

def quit_app():
    camera.close()
    pygame.quit()
    print("You've taken", pics_taken, "pictures. Don't forget to back them up!")
    sys.exit(0)

def intro_screen():
    intro = True
    while intro:
        for event in pygame.event.get():
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_ESCAPE:
                    quit_app()
                elif event.key == pygame.K_F1:
                    camera.start_preview()
                    intro = False
            screen.blit(start_pic_fix, (0, 0))
            pygame.display.update()

def main():
    intro_screen()
    while True:
        for event in pygame.event.get():
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_ESCAPE:
                    quit_app()
                elif event.key == pygame.K_SPACE:
                    take_pic()
                elif event.key == pygame.K_BACKSPACE:
                    delete_pic()
                elif event.key == pygame.K_RETURN:
                    make_movie()
                elif event.key == pygame.K_TAB:
                    camera.preview_alpha = change_alpha()
                elif event.key == pygame.K_F1:
                    camera.start_preview()
                elif event.key == pygame.K_p:
                    camera.stop_preview()
                    intro_screen()
                elif event.key == pygame.K_p:
                    if pics_taken > 1:
                        animate()
        update_display()

if __name__ == '__main__':
    main()
```

![](img/a1548a579bd09ff29b2b92de3f565e63_28_0.png)
