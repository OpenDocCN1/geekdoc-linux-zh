

## 编写你自己的推特机器人

创建你自己的推特机器人，让它能够转发来自 Linux User & Developer 的精华内容。

### 你需要什么

- 互联网连接
- 最新版本的 Raspbian
- www.raspberrypi.org/downloads

推特是与世界分享信息的有用方式，也是我们快速方便地表达观点的最爱方法。数百万人通过他们的电脑、移动设备使用这个博客平台，甚至可能在他们的电视上也有它。

不过，你不需要一直按那个转发按钮。加上一点 Python，你可以让树莓派为你完成这件事。以下是如何创建你自己的推特机器人……

### 01 安装所需软件

使用用户名 Pi 和密码 **raspberry** 登录 Raspbian 系统。使用命令 `sudo apt-get update` 获取最新的软件包列表。然后使用 `sudo apt-get install python-pip` 安装 Python 包安装器。完成后，运行 `sudo pip install twython` 安装我们将使用的推特库。

### 02 在推特注册

我们需要使用 OAuth 在推特上进行身份验证。在此之前，你需要访问 [https://dev.twitter.com/apps](https://dev.twitter.com/apps) 并登录你希望你的树莓派用来发推的账号。点击“创建一个新应用程序”按钮。我们将我们的应用程序命名为“LUD Pi Bot”，给出了相同的描述，并将网站设置为 http://www.linusers.co.uk/。回调 URL 是不需要的。你将需要同意开发者规则，然后点击创建按钮。

![](img/a1548a579bd09ff29b2b92de3f565e63_19_0.png)

通过创建自动化转发器来节省你的鼠标点击

### 03 创建访问令牌

转到设置选项卡，将访问类型从“仅读取”更改为“读取和写入”。然后点击“更新此推特应用程序的设置”按钮。下一步是创建访问令牌。为此，点击“创建我的访问令牌”按钮。如果你刷新详情页面，你应该有一个消费者密钥、一个消费者密钥秘密和访问令牌，以及一个访问令牌秘密。这是我们在推特上进行身份验证所需的一切。

### 04 在推特上进行身份验证

我们将把我们的机器人创建一个类，在构造函数中我们在推特上进行身份验证。我们将前面步骤中的令牌作为参数，并使用它们来创建 Twython API 的实例。我们还有一个变量，last_run，它被设置为当前时间。这用于稍后检查是否有新的推文。

#### 完整代码列表

```python
#!/usr/bin/env python2

# A Twitter Bot for the Raspberry Pi that retweets any
# content from @LinuxUserMag. Written by Liam Fraser for a Linux User &
# Developer article.

import sys
import time
from datetime import datetime
from twython import Twython

class bot:
    def __init__(self, c_key, c_secret, a_token, a_token_secret):
        # Create a Twython API instance
        self.api = Twython(c_key, c_secret, a_token, a_token_secret)

        # Make sure we are authenticated correctly
        try:
            self.api.verify_credentials()
        except:
            sys.exit("Authentication Failed")
        self.last_run = datetime.now()

    @staticmethod
    def timestr_to_datetime(timestr):
        # Convert a string like Sat Nov 09 09:29:55 +0000
        # 2013 to a datetime object. Get rid of the timezone
        # and make the year the current one.
        timestr = timestr[:18] + timestr[23:]
        timestr = timestr + str(datetime.now().year)
        # We now have Sat Nov 09 09:29:55 2013
        return datetime.strptime(timestr, "%a %b %d %H:%M:%S %Y")

    def retweet_task(self, screen_name):
        # Retweets any tweets we've not seen from a user
        print("Checking for new tweets from {}".format(screen_name))

        # Get a list of the users latest tweets
        timeline = self.api.get_user_timeline(screen_name = screen_name)

        # Loop through each tweet and check if it was
        # posted since we were last called
        for t in timeline:
            tweet_time = bot.timestr_to_datetime(t['created_at'])
            if tweet_time > self.last_run:
                print("Retweeting {}".format(t['id']))
                self.api.retweet(id = t['id'])

if __name__ == "__main__":
    # The consumer keys can be found in your application's
    # Details page located at https://dev.twitter.com/apps (under OAuth settings')
    c_key = ""
    c_secret = ""
    # The access tokens can be found in your application's
    # Details page located at https://dev.twitter.com/apps (located under Access token')
    a_token = ""
    a_token_secret = ""
    # Create an instance of the bot class
    twitter = bot(c_key, c_secret, a_token, a_token_secret)
    # Retweet anything new @LinuxUserMag every 5 minutes
    while True:
        # Update the time after each retweet task so we're
        # only retweeting new stuff
        twitter.retweet_task("LinuxUserMag")
        twitter.last_run = datetime.now()
        time.sleep(5 * 60)
```

### 05 转发用户

我们需要做的第一件事是获取用户最新推文的列表。然后我们遍历每个推文并获取其创建时间作为一个字符串，该字符串随后被转换为 datetime 对象。然后我们检查该推文的时间是否比函数上次被调用的时间更新——如果是，则转发该推文。

### 06 主程序部分

主程序部分很简单。我们使用我们的令牌创建机器人类的实例，然后进入无限循环。在这个循环中，我们检查我们要监控的用户是否有新的转发（我们可以用不同的用户运行转发任务），然后更新时间所有东西上次运行的时间，并休眠五分钟。

如果推文的时间比函数上次被调用的时间更新，我们就转发它

获取代码：bit.ly/1RTgNSH

## 10 个实用树莓派项目

![](img/a1548a579bd09ff29b2b92de3f565e63_21_0.png)

> Arduino 在处理诸如伺服电机和模拟输入之类的事情上更为擅长

## 使用树莓派编程你的 Arduino

在你的树莓派项目中享受 Arduino 微控制器的所有特性和优势

### 你需要什么

- Arduino Uno
- 互联网连接
- Numpy (https://scp.org/numpy)

你可能会想知道为什么你想在你的树莓派上连接一个 Arduino。虽然有很多原因，但最突出的可能是标准 Arduino Uno 提供的额外六个支持 PWM 的引脚和另外六个模拟引脚。

你看，虽然树莓派拥有一系列优秀的引脚和功能，但它开箱即用的情况下无法进行模拟和实时处理。有了 Arduino，像伺服电机、电位器和各种模拟传感器等附加组件触发和控制变得轻而易举。

最好的是你甚至不需要使用 Arduino 的准 C++ 语言编程。你只需要在树莓派和 Arduino 之间建立标准的 USB 连接，以及一个名为 Nanpy 的小型 Python 包。以下是如何做到的……

### 01. 获取一个 Arduino

在你能做任何事情之前，你需要一个 Arduino。我们推荐 Uno，因为它是具有最佳的功能、便利性和价格平衡的默认选择。由于你希望立即投入使用，我们建议投资一个包含 LED、伺服电机等有趣物品的“入门套件”。

### 02. 满足依赖项

我们假设你使用的是 Raspbian（推荐），所以打开你的终端，因为我们需要获取设置工具以便安装 Nanpy。在终端中，输入：

```bash
$ wget https://github.com/pypa/setuptools/raw/bootstrap/ez_setup.py
$ python ez_setup.py user
```

完成后，你就可以使用 easy_install 命令来安装 pyserial……

### 03 最终准备

由于 Arduino 和树莓派之间的通信将通过 USB 串行连接发生，我们需要获取 Python-serial 库。在终端中，输入：

```bash
$ easy_install pyserial
```

我们还需要安装 Arduino 软件，以便 Pi 知道当设备插入时如何处理它。在终端中，输入：

```bash
$ sudo apt-get update
$ sudo apt-get install arduino
```

### 04 安装 Nanpy

配置中只剩下两步。首先，我们需要获取并安装 Nanpy 包在 Pi 上。我们喜欢的方式是通过 Git 克隆它。在终端中导航到你的主文件夹（cd ~）并按顺序在终端中执行以下操作。

```bash
$ easy_install nanpy
$ sudo apt-get install git
$ git clone https://github.com/nanpy/nanpy.git
```

### 05 配置你的 Arduino Uno

为什么我们要克隆原始的 Git 仓库？Nanpy 依赖于 Arduino 固件的更新才能正确工作，因此你需要从 nanpy 项目目录访问固件文件夹来完成它。在将以下内容输入终端之前，请将你的 Arduino Uno 插入树莓派的备用端口。小心：以下操作需要一些时间！

```bash
$ cd nanpy/firmware
$ export BOARD=uno
$ make
$ make upload
```

### 06 用你的 Pi 测试 Arduino

安装终于完成后，我们可以测试设置以确保它正常工作。在我们对右侧代码段进行真正的“你好世界！”应用程序之前，让我们首先确保 Nanpy 已正确安装并且 Pi 和 Arduino 之间的连接正在工作。从你的主文件夹（cd ~），在终端中输入以下命令：

```bash
$ nano nanpy_test.py
```

在 nano 编辑器中，只需写入：

```python
from nanpy import Arduino
```

现在按 Ctrl+X，Y，然后按 Enter 保存你的新文件。最后，在终端中输入：

```bash
$ python nanpy_test.py
```

如果你没有看到错误，那么一切都应该正常工作。现在你可以开始跨页面玩代码，开始学习如何操作 Nanpy。

#### 完整代码列表

```python
# Like all good hardware-based 'Hello, World!' applications, we'll start
# by making the light on the Arduino board flicker off and on.
from nanpy import Arduino
from time import sleep

Arduino.pinMode(13, Arduino.OUTPUT)
for i in range(10):
    Arduino.digitalWrite(13, Arduino.HIGH)
    sleep(2)
    Arduino.digitalWrite(13, Arduino.LOW)
    sleep(2)

# This will make the light controlled by pin 13 on the Arduino
# turn on and off every two seconds ten times.

# You can also assign pins a name, to make your code more readable.

light = 13
Arduino.pinMode(light, Arduino.OUTPUT)

# You can also assign multiple pins at the same time:

red_pin = 3
green_pin = 5
blue_pin = 9

for pins in (red_pin, green_pin, blue_pin):
    Arduino.pinMode(pins, Arduino.OUTPUT)

# if you've got an LED screen for your RASPi you'll probably
# find it works out of the box with Nanpy. Just make sure you
# assign the right pin numbers for your screen:

from nanpy import (Arduino, Lcd)

screen = Lcd([7, 8, 9, 10, 11, 12], [16, 2])
screen.printString('Hello, World!')

# If you're using potentiometers, buttons or analog sensors,
# you'll need to assign them as inputs
knob = 0
Arduino.pinMode(knob, Arduino.INPUT)

value = Arduino.analogRead(knob)
for i in range(10):
    print ('The value of the knob is:', value)
    sleep(1)

# Sometimes you want to delay what the arduino does.
# This can help you get consistent, solid readings
def get_value():
    value = Arduino.analogRead(knob)
    Arduino.delay(100)
    return value
for i in range(10):
    print('The value is:', get_value())
```

![](img/a1548a579bd09ff29b2b92de3f565e63_22_0.png)

**你将学到**
**1. 发挥优势**
虽然 RASPi 比 Arduino 强大得多，但在与真实世界交互方面，Arduino 更具优势。利用它们两者的优势来创建更好的项目。

