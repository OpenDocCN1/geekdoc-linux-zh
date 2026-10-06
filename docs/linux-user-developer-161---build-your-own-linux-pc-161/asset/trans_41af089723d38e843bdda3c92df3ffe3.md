

# 完整代码列表

在启动程序之前，请确保你的 Pi 时钟已正确设置。

```python
import time
import os
import picamera
import subprocess
import RPi.GPIO as GPIO

GPIO.setmode(GPIO.BCM)
# 设置 PIR
PIR = 7
GPIO.setup(PIR, GPIO.IN)
# 设置 LEDPAROL
GPIO.output(10, GPIO.OUT)

global file_name = # 照片数量
global file_name = # 照片名称
File_Number = 1

def detect_self(): # 拍摄野兽的的照片
global File_Number
global current_time
time_of_photo = time.asctime(time.localtime(time.time()))
GPIO.output(10, GPIO.HIGH)
with picamera as camera:
    camera.start_record()
    time.sleep(5)
    camera.capture("Nature" + str(File_Number) + ".jpg")
    file_name = "Nature" + str(File_Number) + ".jpg"
    File_Number = File_Number + 1
GPIO.output(10, GPIO.LOW) # 关闭 LEDPAROL
```

time_of_photo = time.asctime(time.localtime(time.time()))

## 12 在图片中添加时间
如果你正在观察并等待野生动物触发相机，那么记录拍摄照片的时间是非常有意义的，而且你可以看到时间值。更好的解决方案是在图片上添加一个“时间戳”。这意味着当你查看图像时就能看到时间。添加的代码行是 `camera.annotate = "time"`。

## 13 总结
在完成之前，快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

## 14 拍摄视频
如果你倾向于在 PIR 触发时拍摄视频，可以调整程序录记录可能访问你花园的野生动物。例如，你可以更改代码使用 `camera.start_recording("/home/desktop/video.avi")` 来录制视频。如果你想录制例如 20 秒，在用 `camera.stop_recording("/home/desktop/video.avi")` 停止录制之前使用 `time.sleep(20)`。

```python
camera.start_preview()
camera.start_recording('/home/desktop/video.h264')
time.sleep(5)
camera.stop_recording()
```

## 15 自动启动你的项目
你构建可以在没有显示器或屏幕的情况下运行，这意味着你可能让程序启动。要做到这一点，将程序设置为在接入电源时自动启动。你需要在脚本中添加一行，例如，在 `/home/name/Night_Box.py` 文件中。通过终端和命令双重检查使用 `/home/name/Night_Box.py` 以获取正确的路径。

```bash
sudo nano /home/name/of_your_script.py
```

如果正确，这将显示你的 Python 代码内容。下一步是通过修改 'cron' 来创建一个任务。要这样做，请使用 `crontab -e`（这将为所有用户运行任务）。滚动到窗口顶部并添加以下行：

```bash
@reboot python /home/name/of_your_program.py &
```
末尾的 @ 将在后台运行代码并确保你的树莓派将正常启动。按 Ctrl+X 然后按 Y 保存文件，然后重启。

## 16 部署箱子
为了有效部署设置，你可能想为 PIR、LEDPAROL 创建箱子或支架。这将保护设备免受雨淋或风吹的损坏。你可能想为组件创建一个 3D 打印的结构。在上一步中，你使用了计划的 cron 在树莓派启动时自动启动程序。选择一个合适的位置并设置你的箱子。启动程序并在第二天查看什么访问了你的花园！

![](img/a54b3b473771472dd2321dd1014be1_66_0.png)

# 教程

# 使用蓝牙适配器构建 iBeacon

# 使用你的树莓派作为 DIY PiBeacon 掌握 Apple 的 iBeacon 技术

2002 年的电影《少数报告》基于菲利普·K·迪克的小说，设定在一个反乌托邦的未来，在那里，梦想在发生之前就会被预知，广告根据他们的身份和习惯对个人进行精准投放。这被视为许多未来元素之一，但快进到 2015 年，这就是这里的广告了。

### 01 准备你的 Pi
在完成之前，使用你的树莓派作为 DIY PiBeacon 掌握 Apple 的 iBeacon 技术。

2002 年的电影《少数报告》基于菲利普·K·迪克的小说，设定在一个反乌托邦的未来，在那里，梦想在发生之前就会被预知，广告根据他们的身份和习惯对个人进行精准投放。这被视为许多未来元素之一，但快进到 2015 年，这就是这里的广告了。 

在完成之前，快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

### 01 准备你的 Pi
在完成之前，使用你的树莓派作为 DIY PiBeacon 掌握 Apple 的 iBeacon 技术。

在完成之前，快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

### 02 设置你的 Pi
在完成之前，使用你的树莓派作为 DIY PiBeacon 掌握 Apple 的 iBeacon 技术。

在完成之前，快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

### 01 准备你的 Pi
在完成之前，使用你的树莓派作为 DIY PiBeacon 掌握 Apple 的 iBeacon 技术。

在完成之前，快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

### 01 准备你的 Pi
在完成之前，使用你的树莓派作为 DIY PiBeacon 掌握 Apple 的 iBeacon 技术。

在完成之前，快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

### 01 准备你的 Pi
在完成之前，使用你的树莓派作为 DIY PiBeacon 掌握 Apple 的 iBeacon 技术。

在完成之前，快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

### 01 准备你的 Pi
在完成之前，使用你的树莓派作为 DIY PiBeacon 掌握 Apple 的 iBeacon 技术。

在完成之前，快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

### 01 准备你的 Pi
在完成之前，使用你的树莓派作为 DIY PiBeacon 掌握 Apple 的 iBeacon 技术。

在完成之前，快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

### 01 准备你的 Pi
在完成之前，使用你的树莓派作为 DIY PiBeacon 掌握 Apple 的 iBeacon 技术。

在完成之前，快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

### 01 准备你的 Pi
在完成之前，使用你的树莓派作为 DIY PiBeacon 掌握 Apple 的 iBeacon 技术。

在完成之前，快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

### 01 准备你的 Pi
在完成之前，使用你的树莓派作为 DIY PiBeacon 掌握 Apple 的 iBeacon 技术。

在完成之前，快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

### 01 准备你的 Pi
在完成之前，使用你的树莓派作为 DIY PiBeacon 掌握 Apple 的 iBeacon 技术。

在完成之前，快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

### 01 准备你的 Pi
在完成之前，使用你的树莓派作为 DIY PiBeacon 掌握 Apple 的 iBeacon 技术。

在完成之前，快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

``` 
[content]

# Tutorial

# Build an iBeacon with a Bluetooth dongle

# Get grips with Apple's iBeacon technology using your Raspberry Pi as a DIY PiBeacon

[/content]

# Tutorial

# Build an iBeacon with a Bluetooth dongle

# Get grips with Apple's iBeacon technology using your Raspberry Pi as a DIY PiBeacon

The 2002 movie Minority Report, based on Philip K Dick novel, is set in a dystopian future, where dreams before they happen and adverts are targeted individuals based on their identity and habits. It was seen as one of many futuristic elements, but fast-forward to 2015, and that is advertising here.

### 01 Prepare your Pi
To finish you finish, a quick recap on the features and setup: the PIR module is attached to the Pi in the dark. This requires an infrared light source, which is provided by the LEDPAROL. A PIR attached is used to sense changes in heat, which turns the LED and triggers the camera to capture a picture. The current time is recorded for future reference. The caption on the pages showing views for the LEDPAROL and PIR are

## 12 Add the time to the picture
Recording the time a picture is taken is relevant if you are watching and waiting for wildlife to trigger the camera, and you can see the time value. A better solution is to add a "time stamp" to the picture. This means when you view the image you see the time. The line of code added is camera.annotate = "time".

## 13 Recap
Before you finish, a quick recap on the features and setup: the PIR module is attached to the Pi in the dark. This requires an infrared light source, which is provided by the LEDPAROL. A PIR attached is used to sense changes in heat, which turns the LED and triggers the camera to capture a picture. The current time is recorded for future reference. The caption on the pages showing views for the LEDPAROL and PIR are

## 14 Taking a video
If you would prefer to take a video when the PIR is triggered, you could adapt the program to record video of wildlife that might visit your garden. For example, you could change the code to record video using the camera.start_recording("/home/desktop/video.avi"). If you want to record for say, 20 seconds, use time.sleep(20) before stopping the recording with camera.stop_recording("/home/desktop/video.avi").

```python
camera.start_preview()
camera.start_recording('/home/desktop/video.h264')
time.sleep(5)
camera.stop_recording()
```

## 15 Automatically start your project
The project you have built can run without a monitor or screen, meaning that you can want the program to start. To do this, set the program to start automatically when the power supply is plugged in. You will have to add a line to your script, for example, in the /home/name/Night_Box.py file. Double-check if you'd use /home/name/Night_Box.py to get the correct path by the Terminal and command.

```bash
sudo nano /home/name/of_your_script.py
```

If correct, this will display the contents of your Python code. The next step is to create a job by modifying the 'cron'. To do this, use crontab -e (which will run the task for all users). Scroll to the top of the window and add the following line to:

```bash
@reboot python /home/name/of_your_program.py &
```
The @ at the end will run code in the background and ensure your Raspberry Pi will boot up as normal. Save the file by hitting Ctrl+X followed by Y, and then reboot.

## 16 Deploy the Box
To deploy the setup effectively you will want to create a box or holder for the PIR, LEDPAROL. This will protect the equipment from getting damaged if it rains or blows. You may want to create a 3D-printed structure for the components. In the previous step you used a scheduled cron to start the program automatically when the Raspberry Pi is booted. Choose a suitable location and set up your box. Start the program and check back the next day to see what visits your garden present!

![](img/a54b3b473771472dd2321dd1014be1_66_0.png)

[/content]

[content]

# 完整代码列表

在启动程序之前，请确保你的 Pi 时钟已正确设置。

```python
import time
import os
import picamera
import subprocess
import RPi.GPIO as GPIO

GPIO.setmode(GPIO.BCM)
# 设置 PIR
PIR = 7
GPIO.setup(PIR, GPIO.IN)
# 设置 LEDPAROL
GPIO.output(10, GPIO.OUT)

global file_name = # 照片数量
global file_name = # 照片名称
File_Number = 1

def detect_self(): # 拍摄野兽的的照片
global File_Number
global current_time
time_of_photo = time.asctime(time.localtime(time.time()))
GPIO.output(10, GPIO.HIGH)
with picamera as camera:
    camera.start_record()
    time.sleep(5)
    camera.capture("Nature" + str(File_Number) + ".jpg")
    file_name = "Nature" + str(File_Number) + ".jpg"
    File_Number = File_Number + 1
GPIO.output(10, GPIO.LOW) # 关闭 LEDPAROL
```

time_of_photo = time.asctime(time.localtime(time.time()))

## 12 在图片中添加时间
如果你正在观察并等待野生动物触发相机，那么记录拍摄照片的时间是非常有意义的，而且你可以看到时间值。更好的解决方案是在图片上添加一个“时间戳”。这意味着当你查看图像时就能看到时间。添加的代码行是 `camera.annotate = "time"`。

## 13 总结
在完成之前在完成之前，快速回顾一下功能和设置：PIR 模块在黑暗中连接到 Pi 上。这需要一个红外光源，该光源由 LEDPAROL 提供。连接的 PIR 用于感应热量变化，从而打开 LED 并触发相机拍照。会记录当前时间以备日后参考。显示 LEDPAROL 和 PIR 视图的页面上的标题为

## 14 拍摄视频
如果你倾向于在 PIR 触发时拍摄视频，可以调整程序录记录可能访问你花园的野生动物。例如，你可以更改代码使用 `camera.start_recording("/home/desktop/video.avi")` 来录制视频。如果你想录制例如 20 秒，在用 `camera.stop_recording("/home/desktop/video.avi")` 停止录制之前使用 `time.sleep(20)`。

```python
camera.start_preview()
camera.start_recording('/home/desktop/video.h264')
time.sleep(5)
camera.stop_recording()
```

## 15 自动启动你的项目
你构建的可以在没有显示器或屏幕的情况下运行，这意味着你可能让程序启动。要做到这一点，将程序设置为在接入电源时自动启动。你将需要在脚本中添加一行，例如，在 `/home/name/Night_Box.py` 文件中。通过终端和命令双重检查使用 `/home/name/Night_Box.py` 以获取正确的路径。

```bash
sudo nano /home/name/of_your_script.py
```

如果正确，这将显示你的 Python 代码内容。下一步是通过修改 'cron' 来创建一个任务。要这样做，请使用 `crontab -e`（这将为所有用户运行任务）。滚动到窗口顶部并添加以下行到：

```bash
@reboot python /home/name/of_your_program.py &
```
末尾的 @ 将在后台运行代码并确保你的树莓派将正常启动。按 Ctrl+X 然后按 Y 保存文件，然后重启。

## 16 部署箱子
为了有效部署设置，你可能想为 PIR、LEDPAROL 创建箱子或支架。这将保护设备免受雨淋或风吹的损坏。你可能想为组件创建一个 3D 打印的结构。在上一步中，你使用了计划的 cron 在树莓派启动时自动启动程序。选择一个合适的位置并设置你的箱子。启动程序并在第二天查看什么访问了你的花园！

![](img/a54b3b473771472dd2321dd1014be1_66_0.png)

