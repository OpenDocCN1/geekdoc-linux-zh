
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

我们需要做的第一件事是获取用户最新推文的列表。然后我们遍历每个推文并获取其创建时间作为一个字符串，该字符串随后被转换为 `datetime` 对象。然后我们检查该推文的时间是否比函数上次被调用的时间更新——如果是，则转发该推文。

### 06 主程序部分

主程序部分很简单。我们使用我们的令牌创建 `bot` 类的实例，然后进入无限循环。在这个循环中，我们检查我们要监控的用户是否有新的转发（我们可以用不同的用户运行转发任务），然后更新时间所有东西上次运行的时间，并休眠五分钟。

如果推文的时间比函数上次被调用的时间更新，我们就转发它

获取代码：`bit.ly/1RTgNSH`

## 10 个实用树莓派项目

![](img/a1548a579bd09ff29b2b92de3f565e63_21_0.png)

> Arduino 在处理诸如伺服电机和模拟输入之类的事情上更为擅长

## 使用树莓派编程你的 Arduino

在你的树莓派项目中享受 Arduino 微控制器的所有特性和优势

### 你需要什么

- Arduino Uno
- 互联网连接
- Numpy (`https://scp.org/numpy`)

你可能会想知道为什么你想在你的树莓派上连接一个 Arduino。虽然有很多原因，但最突出的可能是标准 Arduino Uno 提供的额外六个支持 PWM 的引脚和另外六个模拟引脚。

你看，虽然树莓派拥有一系列优秀的引脚和功能，但它开箱即用的情况下无法进行模拟和实时处理。有了 Arduino，像伺服电机、电位器和各种模拟传感器等附加组件触发和控制变得轻而易举。

最好的是你甚至不需要使用 Arduino 的准 C++ 语言编程。你只需要在树莓派和 Arduino 之间建立标准的 USB 连接，以及一个名为 `Nanpy` 的小型 Python 包。以下是如何做到的……

### 01. 获取一个 Arduino

在你能做任何事情之前，你需要一个 Arduino。我们推荐 Uno，因为它是具有最佳的功能、便利性和价格平衡的默认选择。由于你希望立即投入使用，我们建议投资一个包含 LED、伺服电机等有趣物品的“入门套件”。

### 02. 满足依赖项

我们假设你使用的是 Raspbian（推荐），所以打开你的终端，因为我们需要获取设置工具以便安装 `Nanpy`。在终端中，输入：

```bash
$ wget https://github.com/pypa/setuptools/raw/bootstrap/ez_setup.py
$ python ez_setup.py user
```

完成后，你就可以使用 `easy_install` 命令来安装 `pyserial`……

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
