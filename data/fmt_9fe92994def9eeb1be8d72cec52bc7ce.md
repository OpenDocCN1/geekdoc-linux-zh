
要配置 BOINC 如何使用 Pi 的资源，首先启用 Advance View，然后前往 Tools > Computing preferences。

已创建，请继续为 Jasper 创建用户配置文件以了解你。切换到 `~/jasper/` 客户端目录并使用 `python populate.py` 运行配置文件填充脚本。该脚本会询问你的姓名、联系方式等信息。Jasper 使用这些信息与你沟通并更准确地回应你的查询。还请记住 Jasper 会要求你输入电子邮件账户的密码，然后将其以明文未加密的形式存储。详细信息存储在 `profile.yml` 文件中。按照项目网站上的文档集成其他服务，如 Facebook 和 Spotify。在运行完配置文件创建脚本后再次重启 Pi。

当它重新启动后，Jasper 会用你在创建配置文件时选择的语音合成器向你问好。你现在可以通过说“Jasper”开始与你的新助手互动。如果它捕捉到该短语，Jasper 会用一声蜂鸣作出回应。你现在可以说出你的命令，例如“现在几点了？”或“我有新邮件吗？”。同样，如果 Jasper 能听到你，它会用答案作出回应。取决于你的麦克风质量和操作员的口才，你与 Jasper 的最初对话可能不会很愉快。

## Hack #10: Minecraft Pi Edition

Minecraft Pi Edition 是热门口袋版的精简版本，但包含足够多的组件来释放你的创造力。你可以探索随机生成的世界并使用建造模式来构建自己的作品。

最好的地方在于其 API，可以使用 Python 访问。你可以编写 Python 脚本来移动玩家以及创建和销毁方块。这使你可以在几秒钟内创建出手工制作需要数小时才能完成的建筑。API 还允许你创建交互式对象，如时钟，并赋予你传送能力。你可以在玩乐中学习编程。

要安装 Pi 版，请前往 pi.minecraft.net 并下载压缩归档。然后在你的主目录下使用 `tar zxvf minecraft-pi.tar.gz` 解压它。这将在 `~/minecraft` 目录下展开归档。切换到该目录并使用 `./minecraft-pi` 启动游戏。如果你不熟悉 Minecraft，你可以用鼠标和 WASD 键控制移动。1-8 键选择快速栏中的物品，空格键使你跳跃，双击空格键切换飞行能力。

你可以使用 API 连接到正在运行的 Minecraft 实例。然而，在使用 Python API 接管控制之前，最好先从 `~/minecraft` 文件夹内的 Python API 文件夹制作一个副本到新位置。在终端中，输入 `mkdir ~/mycraft` 创建一个文件夹并使用以下命令将其复制到其中：

```
cp -r ~/minecraft/api/python/mcpi ~/mycraft/minecraft
```

我们现在将在 `~/mycraft` 目录内保存自定义脚本。在游戏运行时，按 Alt+Tab 键切换回终端。在终端中打开一个新标签页并进入 `mycraft` 目录。启动一个文本编辑器并使用 `nano ~/mycraft/demo.py` 创建一个新的 `demo.py` 脚本并复制以下内容到其中：

```
### Demo script to interact with the Minecraft environment
import minecraft.minecraft as minecraft
import minecraft.block as block
import time
#Connect to minecraft by creating the minecraft object
mc = minecraft.Minecraft.create()
#Post a message to the minecraft chat window
```

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_44_0.png)

```
mc.postToChat("Hello, this is a demo of Minecraft API.")
time.sleep(2)
playerPos = mc.player.getPos() #Find your player’s position.
#Change your players position
mc.player.setPos(playerPos.x, playerPos.y + 50, playerPos.z)
### wait for 10 seconds while you fall back
time.sleep(10)
### - create a STONE block in front of you
playerPos = mc.player.getTilePos()
mc.setBlock(playerPos.x+1, playerPos.y+1, playerPos.z,
block.STONE)
time.sleep(5)
### - Now change that block into WOOD
mc.setBlock(playerPos.x+1, playerPos.y+1, playerPos.z,
block.WOOD_PLANKS)
time.sleep(5)
### - Now let’s create a tower by stacking block
for top in range(0, 10):
mc.setBlock(playerPos.x+3, playerPos.y+top, playerPos.z,
block.STONE)
time.sleep(5)
### - Let’s now teleport you to the top of the tower
mc.player.setPos(playerPos.x+1, playerPos.y+10, playerPos.z)
```

Save the script and while Minecraft is running, fire up the script with `python ~/mycraft/demo.py`. If you haven’t made any typos, you’ll see the welcome message in the game as defined in the `postToChat` string. We then find your player’s position with `getPos` and store it in the `playerPos` variable. The players position is defined with the X and Y and Z coordinates that you can see in the top-left corner of the screen. We then use `setPos` to change your position and teleport you into the sky. When you fall back down, we use the `setBlock` parameter to create a stone block (`block.STONE`) in front of you and then after five seconds replace it with a wooden block (`block.WOOD_PLANKS`). We then use a For loop to stack ten stone blocks a little further away, and then place you on top of it before ending the demo.

作为在 LXP186 中可以做什么的示例，Jonni 展示了如何在 Minecraft 中建造大炮并炸毁东西。

这只是一个使用 Python API 可以实现的功能的演示。下载这个不错的 PDF 速查表 (`http://bit.ly/MinecraftPyCheatSheet`) ，其中包含 API 中的参数以及示例和简要说明。使用 Python 控制 Minecraft 极其强大，提供了如此多的灵活性，以至于我们不可能在这里全部演示。然而，如果你感兴趣，请查看 Jonni 在 Linux Format 杂志档案中的 Minecraft Python 教程（见 Coding Academy，第 83 页，LXP185 起）。

## Arduino：坎巴拉太空计划

为坎巴拉制作自定义控制器并非火箭科学，我们来教你如何做。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_45_0.png)
