
# 第三方模块

### 示例（使用 setuptools 安装 simplejson）：

```python
kunal@ubuntu:~$ sudo easy_install simplejson
Searching for simplejson
Reading http://pypi.python.org/simple/simplejson/
Reading http://undefined.org/python/#simplejson
Best match: simplejson-2.0.9
Downloading http://pypi.python.org/packages/0.9/2/simplejson-2.0.9.tar.gz#md5=af5ee67a39c3a408563411d357e6dd5e47
Processing simplejson-2.0.9.tar.gz
Running simplejson-2.0.9/setup.py -q dist_epg --dist-dir /tmp/easy-install-1fyiNL/simplejson-2.0.9/egg-dist-tmp-23w6Gv
Adding simplejson 2.0.9 to easy-install.pth file
Installed /usr/local/lib/python2.6/ dist-packages/simplejson-2.0.9-py2.6- linux-1686.egg
Processing dependencies for simplejson
Finished processing dependencies for simplejson
```

# 47 写入系统日志

您可以使用 `syslog` 模块写入系统日志。`syslog` 充当 UNIX syslog 程序的接口。

**示例：**

```python
import syslog
syslog.syslog("mygeekapp: started logging")
for a in ['a', 'b', 'c']:
    b = "mygeekapp: I found letter " + a
    syslog.syslog(b)
syslog.syslog("mygeekapp: the script goes to sleep now, bye, bye!")
```

**输出：**

```text
$ python mylog.py
$ tail -f /var/log/messages
Nov 8 17:14:34 ubuntu -- MARK --
Nov 8 17:22:34 ubuntu python:
mygeekapp: started logging
Nov 8 17:22:34 ubuntu python:
mygeekapp: I found letter a
Nov 8 17:22:34 ubuntu python:
mygeekapp: I found letter b
Nov 8 17:22:34 ubuntu python:
mygeekapp: I found letter c
Nov 8 17:22:34 ubuntu python:
mygeekapp: the script goes to sleep now, bye, bye!
```

# 48 生成 PDF 文档

“ReportLab” 是一个用于从 Python 生成 PDF 的非常流行的模块。

**请执行以下步骤来安装 ReportLab：**

```bash
$ wget http://www.reportlab.org/ftp/ReportLab_2_3.tar.gz
$ tar xvzf ReportLab_2_3.tar.gz
$ cd ReportLab_2_3
$ sudo python setup.py install
```

**安装成功时，您应该会看到类似以下信息：**

```text
########################SUMMARY INFO############
@Attempting install of _rL_accel, spmlob & pyPNG
@Attempting install of renderPM
# installing with freetype version 21
```

**示例：**

```python
>>> from reportlab.pdfgen.canvas import Canvas
# Select the canvas of letter page size
letter
>>> from reportlab.lib.pagesizes import letter
>>> pdf = Canvas('bond.pdf', pagesize=letter)
# import units
>>> from reportlab.lib.units import cm, mm, inch, pica
>>> pdf.setFont("Courier", 60)
>>> pdf.setFillColorRGB(1, 0, 0)
>>> pdf.drawCentredString(letter[0] / 2, inch * 6, "M6 CLASSIFIED")
>>> pdf.setFont("Courier", 40)
>>> pdf.drawCentredString(letter[0] / 2, inch * 5, "For M07's Eyes Only")
# Close the drawing for current page
>>> pdf.showPage()
# Save the pdf page
>>> pdf.save()
```

**输出：**

![pdf.png](img/pdf.png)
*PDF 输出*

# 49 使用 Twitter API

您可以使用 “Python-Twitter” 模块连接 Twitter。

**请执行以下步骤来安装 Python-Twitter：**

```bash
$ wget http://python-twitter.googlecode.com/files/python-twitter-0.6.tar.gz
$ tar xvzf python-twitter*
$ cd python-twitter*
$ sudo python setup.py install
```

**示例（获取关注者列表）：**

```python
>>> import twitter
# Use your own twitter account here
>>> myvi = twitter.Api(username='kunal eo', password='xxxxxx')
>>> friends = myvi.getFriends()
>>> print [u_name for u in friends]
['Matt Llegend Gemmell', u'jono wells', u'IH8anO', u'MN Big Blog', u'Manish Mandal', u'IH8anO', u 'IIndiaI/ideGamer.com', u'FakeAaroen Hiligass', u'ChaosCode', u'nileshp', u 'Frank Jennings ...']
```

# 50 进行雅虎新闻搜索

您可以使用雅虎搜索 SDK 从 Python 访问雅虎搜索 API。

**请执行以下步骤来安装它：**

```bash
$ wget http://developer.yahoo.com/download/files/yss-2.12.zip
$ unzip yss*
$ cd Yahoo! Python/search/
$ sudo python setup.py install
```

**示例：**

```python
# Importing news search API
>>> from yahoo.search.news import NewsSearch
>>> src = NewsSearch('YahoDemo', query='london')
# Fetch Results
>>> info = src.parse_results()
>>> info.total_results_available
41640
>>> info.total_results_returned
10
>>> for result in info.results:
.... print 'from %s' % (result['Title'], result['NewsSource'])
"'Afghan handler to be Planned at London Conference, Brown Says', from Bloomberg news"
```

# 编写一个石头、剪刀、布游戏

通过我们对一个简单的石头、剪刀、布游戏的分解，学习如何编写一些基本的 Python 代码。

本教程将指导您使用 Python 制作一个石头、剪刀、布游戏。代码应用了主课程中的知识点，并在此基础上进行了扩展，运行它不需要额外的 Python 模块，例如 Pygame。

石头、剪刀、布是展示 Python 具体能做什么的绝佳游戏。在制作一个可玩的版本时，使用了人类输入、比较、随机选择以及各种循环。它还足够简单，方便您根据自己的需求进行适应和扩展，添加规则和结果，甚至如果您愿意，还可以制作一个简陋的人工智能。

对于这个特定教程，我们还建议使用 IDLE：IDLE 是一个很好的 Python IDE，在大多数 Linux 发行版中都可以轻松获取，并且在树莓派的 Raspbian 上默认提供。它会通过突出显示代码中可能存在的问题来帮助您，并允许您轻松地运行代码以确认其正常工作。

![img/e016e192a91ffc1a9e474690a590742f_31_0.png](img/e016e192a91ffc1a9e474690a590742f_31_0.png)

- 允许 Python 脚本在终端中运行，且在 IDE 之外运行
- 使用整数形式的人类输入来比较动作并最终玩游戏
- 使用演绎法来确定三种结果之一
- 循环代码并重新开始
- 附加到整型变量以跟踪得分等内容

## 资源

- Python 2: www.python.org/download
- IDLE: www.python.org/idle

01 这部分导入了代码所需的额外 Python 函数 – 它们仍然是标准 Python 库的一部分，只是不属于默认环境。

02 游戏的最初规则在此处创建。定义了我们要使用的三个变量及其关系。我们还提供了一个变量，以便我们可以记录游戏得分。

03 我们通过定义每轮的开始来启动游戏代码。无论我们是否想再玩一次，每次游戏会话的结束都会回到这里。

04 游戏实际上包含在这里，要求玩家输入，获取计算机输入，并将这些传递给获取结果。在那之后，它会询问您是否想再玩一次。

05 玩家输入在此完成。我们向玩家提供关于如何玩这个特定版本游戏的信息，然后允许他们的选择用于下一步。我们还设置了机制，以防他们输入无效选项。

06 当我们显示结果时，正在发生几件事。首先，我们加入一个延迟以增加紧张感，将变量附加到一些打印文本中，然后比较玩家和计算机做了什么。通过 if 语句，我们选择要打印的结果以及如何更新得分。

07 我们现在请求文本输入，询问是否有人想再玩一次。根据他们的回答，我们返回开始，或结束游戏并显示结果。

```python
#!/usr/bin/env python2
# Linux User & Developer presents: Rock, Paper, Scissors: The Video Game
import random
import time
rock = 1
paper = 2
scissors = 3
names = { rock: "Rock", paper: "Paper", scissors: "Scissors" }
rules = { rock: scissors, paper: rock, scissors: paper }

player_score = 0
computer_score = 0

def start():
    print ("Let's play a game of Rock, Paper, Scissors.")
    while game():
        pass
    scores()

def game():
    player = move()
    computer = random.randint(1, 3)
    result(player, computer)
    return play_again()

def move():
    while True:
        print ("Make a move: ")
        player = raw_input ("Rock = 1\nPaper = 2\nScissors = 3\n")
        try:
            player = int(player)
            if player in (1,2,3):
                return player
            else:
                print ("Oops! I didn't understand that. Please enter 1, 2 or 3.")
        except ValueError:
            pass

def result(player, computer):
    print ("1, 2, 3...")
    time.sleep(1)
    print ("Shoot!")
    time.sleep(1)
    print ("Computer threw {0}!".format(names[computer]))
    global player_score, computer_score
    if player == computer:
        print ("It's a tie.")
    else:
        if rules[player] == computer:
            print ("Your victory has been assured.")
            player_score += 1
        else:
            print ("The computer laughs as you realise you have been defeated.")
            computer_score += 1

def play_again():
    answer = raw_input ("Would you like to play again? y/n: ")
    if answer in ("y", "Y", "yes", "Yes", "Of course!"):
        return True
    else:
        print ("Thank you very much for playing our game. See you next time!")
        return False

def scores():
    global player_score, computer_score
    print ("HIGH SCORES")
    print ("Player: ", player_score)
    print ("Computer: ", computer_score)

if __name__ == '__main__':
    start()
```
