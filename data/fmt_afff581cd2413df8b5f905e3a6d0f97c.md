
### 06 我们如何判断玩家是否找到了钻石？

我们不断重复“`while true`”内部的代码块，直到玩家的位置距离钻石不到两个方块为止。如果玩家紧挨着钻石，可以合理假设他们看到了它，因此我们可以停止计时，告知他们成功并确切告知他们找到钻石所花费的时间。这是一个非常快速且简单的游戏，但它充分展示了 `API` 工具的功能。祝你制作自己的项目时玩得开心！

![](img/59caadfa348382a5c408c25137901e27_86_1.png)

```python
return randomBlockPos

def main(): # the main function of Hide & Seek
    global lastPlayerPos, playerPos
    seeking = True
    lastPlayerPos = playerPos

    randomBlockPos = randomBlock()
    mc.setBlock(randomBlockPos, block.DIAMOND_BLOCK)
    mc.postToChat("A diamond has been hidden somewhere nearby!")

    lastDistanceFromBlock = distanceBetweenPoints(
        randomBlockPos, lastPlayerPos)
    timeStarted = time()

    # This is the main loop of the game
    while seeking:
        # Get players position
        playerPos = mc.player.getPos()
        # Has the player moved?
        if lastPlayerPos != playerPos:
            distanceFromBlock = distanceBetweenPoints(
                randomBlockPos, playerPos)

        if distanceFromBlock < 2:
            #Found it!
            seeking = False
        else:
            if distanceFromBlock > 4:
                mc.postToChat("Warmer " + "🔥"*3 +
                    str(int(distanceFromBlock)) + " blocks away")
            else:
                mc.postToChat("Colder " + "🔥"*1 +
                    str(int(distanceFromBlock)) + " blocks away")

        lastDistanceFromBlock = distanceFromBlock

    sleep(2)

    timeTaken = time() - timeStarted
    mc.postToChat("Well done " + str(int(timeTaken)) +
        "seconds to find the diamond!")

if __name__ == "__main__":
    main()
```

## 编写你自己的 Twitter 机器人

## 你需要什么...

- 互联网连接
- 最新版本的 Raspbian
- www.raspberrypi.org/downloads

![](img/59caadfa348382a5c408c25137901e27_87_0.png)

创建你自己的 Twitter 机器人，它可以转发来自他人的智慧片段

Twitter 是与世界分享信息的有用方式，也是我们快速、便捷地表达观点的首选方法。数百万人通过电脑、移动设备甚至电视使用该微博平台。

不过，你不必一直点击那个转发按钮。只需少许 Python 代码，就可以让树莓代劳。以下是创建你自己的 Twitter 机器人的方法...

## 安装所需的软件

**01** 使用用户名 `Pi` 和密码 `raspberry` 登录 Raspbian 系统。使用命令 `sudo apt-get update` 获取最新的软件包列表。然后使用 `sudo apt-get install python-pip` 安装 Python 包安装器。

完成后，运行 `sudo pip install tweepy` 安装我们将使用的 Twitter 库。

## 在 Twitter 上注册你的“应用程序”

**02** 我们需要使用 OAuth 进行 Twitter 身份验证。在此之前，你需要前往 https://dev.twitter.com/apps 并使用你希望树莓派发推的账户登录。点击“Create a new application”按钮。我们将应用程序命名为“LUD Pi Bot”，并将网站设置为 www.linuxuser.co.uk。

### 完整代码列表
