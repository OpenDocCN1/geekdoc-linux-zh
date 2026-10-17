
密切关注 [http://github.com/russb78/pi-motion](http://github.com/russb78/pi-motion) 以获取该项目未来的更新……

## 设置相机模块

01 首先，你需要确保树莓派已更新到最新版本。在终端中，输入：

```bash
sudo apt-get update && sudo apt-get upgrade
```

接下来，我们需要更新树莓派的固件并确保激活相机模块。请记住，这需要一些时间。

```bash
sudo rpi-update
sudo raspi-config
```

## 完整代码列表

第一项工作是导入我们将与项目一起使用的库，并设置一些关键变量。

接下来我们初始化 Pygame，以便在我们的项目中使用它，并设置一些围绕它的关键变量。

```python
import pygame, picamera, os, sys

pics_taken = 0
current_alpha, next_alpha = 128, 255
fps = 5
```

```python
pygame.init()
res = pygame.display.list_modes() # 返回适合你显示器的最佳分辨率
width, height = res[0]
print "Reported resolution is:", width, "x", height
start_pic = pygame.image.load(os.path.join("data", "start_screen.jpg"))
start_pic_fix = pygame.transform.scale(start_pic, (width, height))
screen = pygame.display.set_mode((width, height))
pygame.display.toggle_fullscreen()
pygame.mouse.set_visible = False
```

Pi-Motion 目前在 GitHub 上可通过 [https://github.com/nsbd2/Pi-Motion](https://github.com/nsbd2/Pi-Motion) 获取

![](img/59caadfa348382a5c408c25137901e27_102_0.png)

# 使用摄像头板制作定格动画

接下来，我们将使用 `picamera` 库创建我们的摄像头对象并创建第一个函数

```python
play_clock = pygame.time.Clock()
camera = picamera.PiCamera()
camera.resolution = (width, height)

def take_pic():
    global pics_taken, prev_pic
    pics_taken += 1
    camera.capture(os.path.join('pics', 'image_' + str(pics_taken) + '.jpg'), use_video_port = True)
    prev_pic = pygame.image.load(os.path.join('pics', 'image_' + str(pics_taken) + '.jpg'))

def delete_pic():
    global pics_taken, prev_pic
    if pics_taken >= 1:
        pics_taken -= 1
        prev_pic = pygame.image.load(os.path.join('pics', 'image_' + str(pics_taken) + '.jpg'))
```

我们可以使用 `animate()` 函数预览我们的动画

```python
def animate():
    camera.stop_preview()
    for pic in range(1, pics_taken):
        anim = pygame.image.load(os.path.join('pics', 'image_' + str(pic) + '.jpg'))
        screen.blit(anim, (0, 0))
        play_clock.tick(fps)
        pygame.display.flip()
        play_clock.tick(fps)
    camera.start_preview()
```

我们需要更新显示屏，以便在屏幕上显示我们拍摄的新图像

```python
def update_display():
    screen.fill((0, 0, 0))
    if pics_taken > 0:
        screen.blit(prev_pic, (0, 0))
    play_clock.tick(30)
    pygame.display.flip()
```

```python
def make_movie():
    camera.stop_preview()
    pygame.quit()
    print("\nQuitting Pi-Motion to transcode your video.")
    os.system("avconv -r " + str(fps) + " -i " + str(os.path.join('pics', 'image_%d.jpg')) + " -vcodec libx264 video.mp4")
    sys.exit()
```

这里的函数对于确保 Pi-Motion 能够输出视频并干净地关闭至关重要

```python
def change_alpha():
    global current_alpha, next_alpha
    camera.stop_preview()
    current_alpha, next_alpha = next_alpha, current_alpha
    return next_alpha

def quit_app():
    camera.close()
```
