
```python
Fig 02

# 在内存中缓冲区中启动摄像头
with picamera.ArrayOutputBuffer() as buffer:
    cam.capture(buffer)
    buffer.seek(0)
    for frame in buffer:
        # 处理每一帧
        if GPIO.input(BUTTON_PIN) == False:
            break
```

当事件被缓冲区（循环缓冲区）移出时，我们使用最后几帧的平均值来过滤背景噪声。这有助于于

当程序运行时，你会在摄像头中看到你的手。你应该看到缩略图打印出的运动检测算法的任何查看；通过缓慢移动，你可能可以做到。分辨率将控制算法的灵敏度，并且

根据经验，运动检测的分分辨率是有限制的。在低分辨率下（如 1640），脚本运行速度快得多并产生合理的结果，如果你想检测人类或动物的运动）仍然占据了视野的很大一部分。

然而，如果你想在响应检测时捕捉图像或录制视频

## `picamera`：使用 `Python` 控制摄像头模块

![](img/2d03d34861423ee052621659d1149047_62_0.png)

左侧是一个接线设置示例，显示摄像头快门按钮连接到 `GPIO` 引脚 17。

你可以使用树莓派摄像头实现的最强大的算法之一是运动检测（安全摄像头的典型需求），你可能想要比 160x120 更高的分辨率。这就是为什么你的脚本将摄像头设置为高分辨率（1280x720），然后使用 `resize` 捕获方法来最大化运动检测算法所需的图像质量。

需要注意的一点是，使用基于视频端口的方法提供了相当的捕获率（视频帧率高达 30 ），但对于摄像头而言，这会导致视野狭，请参见第 62 页的“视野”部分了解如何缓解。上面的代码中有几个配方仅在检测到运动时才使用摄像头。

```python
#!/usr/bin/env python
from __future__ import (
import time
import picamera
import cv2
import numpy as np
import io

class MotionDetector:
    def __init__(self, camera, resolution=(160,120), threshold=20):
        self.camera = camera
        self.resolution = resolution
        self.background = None
        self.threshold = threshold
        self.raw_bytes = None
        self.erosion = None

    def _get_erosion(self, frame):
        kernel = np.ones((3,3), np.uint8)
        return cv2.erode(frame, kernel, iterations=2)

    def process(self, frame):
        stream = io.BytesIO()
        self.camera.capture(stream, format='jpeg')
        stream.seek(0)
        frame = cv2.imdecode(stream.read(), np.uint8)
        data = cv2.cvtColor(frame, cv2.COLOR_BGRGRAY)
        image = cv2.resize(data, self.resolution)
        if self.background is None:
            self.background = image
            return frame
        diff = cv2.absdiff(image, self.background)
        diff = diff.astype(np.uint8)
        _, diff = cv2.threshold(diff, self.threshold, 255, cv2.THRESH_BINARY)
        diff = cv2.dilate(diff, None)
        count = cv2.countNonZero(diff)
        if count > 500:
            self.background = image
        return frame
```

## 延伸阅读

- `picamera` 的 `GitHub` 主页，你可以在此处关注更新
- `Pi cases` 外壳的安装说明
- 摄像头支架（用于树莓派）非常有用
- `GorillaPod` 是一个出色的脚架
- `YUV` 图像编码被树莓派内部使用，它是最常见的格式

## 网络与共享你的键盘和鼠标

![](img/2d03d34861423ee052621659d1149047_64_0.png)

### 02 启动

在主机计算机上启动并选择“服务器（`Server`）”选项学习如何将其作为客户端使用，之后学习如何将树莓派作为鼠标和键盘的服务器。

### 05 启动与连接

设置完成后，客户端将能够接受连接。要从树莓派连接，

### `Synergy` 允许你共享鼠标和键盘

### 03 加密与密码

然后你可以设置连接是否加密。这对于共享键盘以同步你的信息非常有用，或者可以防止由于被连接并劫持你的鼠标导致的记录。提供密码并点击完成。

### 06 `Synergy` 自动启动

为了确保每次打开树莓派时它都会启动，使用以下命令创建一个 `LXDE` 自动启动项：

```bash
$ sudo mkdir --config ~/.1xsession/LXDE/autostart
$ sudo touch --config ~/.1xsession/LXDE/autostart
$ sudo nano --config/.1xsession/LXDE/autostart
```

![](img/2d03d34861423ee052621659d1149047_64_1.png)

然后将以下内容添加到：

```bash
~/.synergy.sh
```

![](img/2d03d34861423ee052621659d1149047_64_2.png)

### 08 权限

最后，你需要运行：

```bash
$ chmod 777 ~/.synergy.sh
```

这将会在你每次打开树莓派时自动连接。树莓派客户端运行有点慢，所以如果你遇到问题，可能需要从源码编译最新版本。

![](img/2d03d34861423ee052621659d1149047_64_3.png)

### 04 服务器命名

进程完成后，转到“配置（`Configuration`）”。你的主机计算机将被虚拟放置在显示器的中心，你可以用任何鼠标拖动它。双击服务器更改其名称，使其更容易记忆，最后“添加新屏幕（`Add a new screen`）”并点击。

### 07 启动文件

打开并填充 `synergy` 文件：

```bash
$ nano ~/.synergy.sh
```

```bash
#!/bin/bash

killall synergy
synergy -name pi [IP address of host]
exit 0
```

### 09 `Pi`（树莓派）

将树莓派设置为服务器涉及稍微更复杂的 `synergy` 命令。它允许你监听特定地址的客户端。你可能需要创建一个配置文件来安排显示器，不过你也可以从另一台电脑加载并编辑它。

`www.linuxuser.com`

# 教程：制作 `Pivaders` 第 2 部分：动画与声音

![](img/2d03d34861423ee052621659d1149047_65_0.png)

## 得分 50

### 需要学习的技能

- **1 `Python`**

  你需要具备 `Python` 基础才能跟上代码，尝试：`www.codeacademy.com`

- **2 类（`Classes`）**

  希望这篇文章能展示类对于轻松创建和操作多个对象是多有用的。

`Russell Barnes` 是《`Linux User & Developer`》杂志的编辑，曾是一名名 `Python` 程序员和树莓派黑客。

![](img/2d03d34861423ee052621659d1149047_65_1.png)

## 制作 `Pivaders` 第 2 部分：动画与声音

在用 300 行 `Python` 写了一个《`太空侵入者`》克隆版本后，本月我们预计包含动画和声音。

- 你需要的
  - **`Raspbian`** `www.raspberry.org/downloads`
  - **`Python`** `www.python.org/doc`
  - **`Pygame`** `www.pygame.org/docs`
