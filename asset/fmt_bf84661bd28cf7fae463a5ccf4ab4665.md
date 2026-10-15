
# `/docker-arm/script/auto_join_swarm.sh`

你将在`docker ps`下看到运行的swarm。如果想查看输出，检查`docker logs`。在每个节点上重复此步骤。

```bash
# docker run -p 6379:6379 -d \
--name redis \
--link redis:1 \
alexis. redis
```

在`balancer`节点上最终运行：

![](img/f4a034c4fbc20906a013558fa4e058a2_73_0.png)

```bash
# DOCKER_HOST=tcp:// docker run -d --name=balancer -p 80:80 nginx
```

## 查询swarm

登录主节点并通过`swarm-arm`镜像查询`console`的地址：

![](img/f4a034c4fbc20906a013558fa4e058a2_73_1.png)

```bash
# docker run alexellisiz/swarm-arm console://192.168.0:2500/
```

### Apache Bench

使用10个并发线程和共1000次请求启动Apache Bench。在设置额外的树莓派后，我们开始操作。为了将Web服务从一个容器扩展到多个，请使用`docker`命令，并将`DOCKER_HOST`变量设置为你的swarm管理器地址：

```bash
# ab -n 1000 -c 10 http://192.168.0:2500/
```

并发级别：10
测试耗时：2.5 秒
每秒请求数：38（平均）

在单个树莓派上重复实验是每秒80次请求，共12秒。你也可以尝试将`-c`值增加到100。

![](img/f4a034c4fbc20906a013558fa4e058a2_73_2.png)

```bash
# export DOCKER_HOST=tcp://192.168.0:2000
```

现在查看我们有多少资源：

```bash
# docker info
```

节点：4
CPU：20
总内存：7 GB

# 示例：分布式 Web 应用程序

我们现在设置一个分布式数据库环境。我们将运行多个实例并使用`nginx`负载均衡来处理流量。然后可以使用Apache Bench进行测试。

## 将流量直连你的swarm

如果你在其中一个上拉取`docker`，可以使用`DOCKER_HOST`变量指向任何节点而无需登录树莓派。swarm创建并将Web服务从一个容器扩展到多个。这些容器需要按顺序启动，从`Redis`开始，最后是`nginx`。

```bash
# DOCKER_HOST=tcp://192.168.0:2000
# docker run -p 6379:6379 -d --name=redis-1 alexellisiz/redis-arm
# wget get.docker.com/builds/arm/v7 -O docker-compose
# docker-compose --version
```

`Docker Compose`是一个允许你定义多个容器的工具，让你无需手动即可将Web服务从一个扩展到多个。

```yaml
node:
  image: redis
  ports:
    - "3000"
nginx:
  image: nginx
  ports:
    - "80"
```

# 教程

## 创建 Minecraft 游戏

使用你的树莓派和`Python`知识在`Minecraft`中编写一个简单的迷你游戏。`Pi`镜像已预装了`Minecraft`和`Python`。如果你使用的是旧版本，建议下载并更新到新的`Raspberry`镜像。

## 更新和安装

更新你的树莓派，打开终端并输入：

```bash
sudo apt-get update
sudo apt-get upgrade
```

### 导入模块

加载你喜欢的编辑器并启动新窗口。你需要导入以下模块：`random`用于创建和生成位置，`time`用于向程序添加暂停和延迟。接下来，添加几行代码：`from mc import minecraft`和`mc = minecraft.Minecraft()`。这些创建了`Minecraft`和`Python`之间的链接。这使你能够写入“创建了`Minecraft`”。

```python
import random
import time
from mc import minecraft
mc = minecraft.Minecraft()
```

### 种花

下面的程序将向展示它是如何工作的。每个区块都有自己的`ID`数字，共有数百个。`x, y, z = mc.getPos()`获取玩家在世界中的位置并以元组形式返回。现在你知道自己在世界的什么位置，可以使用`mc.setBlock(x, y, flower)`放置区块。

```python
flower = 38
while True:
    x, y, z = mc.getPos()
    mc.setBlock(x, y, flower)
    time.sleep(1)
```

### 运行代码

减小`Minecraft`窗口的大小更容易看到代码和运行中的程序；在它们之间切换可能会很麻烦。`Tab`键可以隐藏`MC`窗口的键盘和鼠标。运行`Python`程序并等待加载——随着你的走动，花朵出现了！更改第一行的`ID`来更改区块类型，而不是花，尝试种植金、水或火光。

![](img/f4a034c4fbc20906a013558fa4e058a2_73_0.png)

### 向 Minecraft 世界发布消息

也可以向世界发布消息，这在游戏后期用于告知玩家分数和当前分数。在你的进度中，在代码行`flower = 38`添加以下内容，将其变为`mc.postChat("I grew some flowers with code")`。现在看到消息弹出。你可以更改消息，移动到下一步开始游戏。

### 创建地板

游戏在玩家当前所在的地板上进行，因此在运行程序之前建议飞到空中寻找平坦的地形。要创建地板，你需要编写一个循环并在世界中使用`x, y, z = mc.getPos()`运行程序。使用`mc.setBlock`代码放置构成地板的区块。

# 教程

![](img/f4a034c4fbc20906a013558fa4e058a2_77_0.png)

右侧 无
我“游戏结束”
很多
岩浆爆发

## 07 创建地雷

在上一步中，你找到了玩家在棋板上的位置。`x, y, z`数据可以重用在棋板上放置地雷。代码`mine_x = random.randint(0, 11)`生成一个1到10之间的随机数。将其与玩家的`x`位置结合并将随机数加到`x`位置上——这会在棋板上创建一个地雷。

```
mine_x = int(mine_x)
mine_y = int(mine_y)
mine_z = int(mine_z)
```

使用`setBlock`来放置地雷：`mc.setBlock(mine_x, mine_y, mine_z, 58)`。使用`y`确保方块放置在同一层，数字`58`是方块`ID`，你可以更改它来查看地雷的位置；这对于测试代码的其他部分是否运行正常非常有帮助。在游戏之前记得将其改回来！

构建棋板并放置地雷，你需要再次找到玩家的位置并将其存储为新变量——`x1, y1`和`z1`——否则棋板会随着玩家的移动而偏移。

```
x1, y1, z1 = mc.player.getPos()
```

## 10 得分

现在玩家有了一个方块，我们奖励一个分。这是一个将值加到变量`score`的简单操作。我们使用`score = score + 1`。由于它位于循环内部，玩家每次移动时它都会加一分。

```
time.sleep(0.1)
score = score + 1
```

## 08 创建变量

每当你留在地雷附近时，分数就会加1。为分数创建一个变量，并在游戏开始时将其设置为零。使用`postChat`函数宣布分数。注意`mc`无法在聊天框中打印值，因此在显示之前会将分数转换为字符串。

```
score = 0
pmc.postChat("score: " + str(score))
time.sleep(0.1)
```

## 11 紧张气氛增加

```
if (x1, y1, z1) == (mine_x, mine_y, mine_z):
```
