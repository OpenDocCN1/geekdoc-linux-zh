
![](img/19f01d8418c50f8361fc6069e917f628_80_0.png)

这是一个精巧的小视频编辑器，提供了一些常见的视频编辑功能，但不支持批量处理。

![](img/19f01d8418c50f8361fc6069e917f628_80_1.png)

与其本质相符，该应用具有直观的界面。使用文件按钮选择要编辑的视频。一旦加载，你就可以根据需要使用控件进行编辑。

你可以通过更改预览窗口和时间轴中的更改来调整视频及其长度。同样，你可以通过长度、宽度和像素调整视频尺寸。此外，你还可以根据要求增加或减少帧率。

调整后，你可以以任何流行的容器格式导出视频，包括 WebM、MP4、MKV 或 GIF。

![](img/19f01d8418c50f8361fc6069e917f628_80_2.png)

一旦按需要调整了登录管理器，你可以使用该应用固定设置并将其导入不同的基于 Gnome 的发行版中。

## 登录自定义

### 登录管理器设置 (Login Manager Settings)

版本：3.2

官方网站：https://gdm-settings.github.io

花了一些时间，我们已经习惯了重新设计的 Gnome 桌面的方式。然而，有一件事让我们无法接受：缺乏自定义选项。诚然，桌面有一个额外的架构来帮助我们根据需要管理桌面，但在进行调整以获取登录管理器设置应用时，桌面环境的表现仍不尽如人意。

尽管具有非对齐的性质，但该应用更适合 Gnome，并使我们能够调整各种 Gnome 设置。例如，你可以应用主题、更改登录界面背景、更改光标和图标主题、应用亮色和设置等。它既提供 AppImage 也提供 Flatpak 格式，尽管开发者自己说在某些条件下可能无法正常工作。这就是为什么最好通过 Flatpak 安装该应用：`flatpak install github.io/adham3310/Gnome-Login-Settings`。

该应用非常直观，自定义内容组织为九个部分：外观、字体、背景、声音和主题、登录界面、屏幕预览等。你可以在这些部分之间跳转，滚动查看选项，并根据你的意愿进行调整。某些设置是特定于发行版的，可能对你的发行版没有影响。调整后，点击“应用”。你需要重新登录或重启使更改生效。

## 热门推荐

### APPIMAGE 管理器

#### Gear Lever

版本：1.0.8 网页：https://github.com/mijorus/gearlever

AppImages，或者说 Flatpaks，它们已经简化了跨 Linux 发行版的安装过程，消除了处理不同软件工具和封装格式的复杂性。

但这并不是唯一的缺点。对于 AppImages 而言，最大的问题是它们无法集成到发行版的应用程序菜单中。这正是 Gear Lever 的用武之地，它可以帮助通过几次点击将 AppImages 集成到你的工作流中。

有趣的是，Gear Lever 可用并可以通过 `flatpak install flathub.org/gearlever` 安装。

AppImages 出现时是空白的。你可以将 AppImage 拖入界面进行进行管理，或者点击 `+` 图标从文件管理器中选择。导入后，你必须确认安装。Gear Lever 还允许查看文件的 MD5 校验和，帮助你验证 appimage 的完整性。

![](img/19f01d8418c50f8361fc6069e917f628_81_0.png)

当你将应用添加到应用程序菜单后，Gear Lever 会显示一个按钮，允许你从菜单中移除该应用。

一旦添加了应用，Gear Lever 会为你提供两个按钮：一个用于启动应用，另一个用于将其添加到发行版的应用程序菜单中。

如果你也有一堆应用，可以使用 Gear Lever 将它们都放在一个地方。默认情况下，所有的 AppImages 都通过 `~/AppImages` 管理。

你可以从应用的“偏好设置”菜单更改位置。默认情况下，Gear Lever 通过将原始文件复制到文件夹来帮助节省空间，但你可以选择保留原始文件并在目标文件夹中创建副本。

![](img/19f01d8418c50f8361fc6069e917f628_81_1.png)

与传统的 apt 相比，Nala 更加现代且直观。例如，`sudo nala list` 会列出所有将安装和升级的包以及升级的范围。

## 包管理器

### Nala

版本：0.13.0 网页：https://gitlab.com/volian/nala

`apt` 在基于 Debian 的发行版上很好地完成了包管理，但仍有改进空间。`Nala` 成功填补了这一角色。

`Nala` 由 Fedora 的 DNF 包管理器编写，得益于并行下载，提供了更易读的输出。

在官方的 Debian Testing 和 Ubuntu 22.04 中，它预装了 `apt nala`。

如果你使用的是旧版本的 Ubuntu，仍然可以通过第三方仓库成功安装 Nala。参考我们的教程在 Ubuntu 上安装 Nala：

```bash
sudo echo "deb [arch=amd64,arm64,armv7] http://sources.github.com/volian/archive-scar-unstable stable" | sudo tee /etc/apt/sources.list.d/volian-archive-scar-unstable.list
```

获取 GPG 验证密钥：

```bash
$ wget -qO- https://keys.github.com/volian/scar.key | sudo gpg --dearmor -o /etc/apt/gpg.d/volian-archive-scar.gpg
```

![](img/19f01d8418c50f8361fc6069e917f628_81_2.png)

最后，安装 Nala 的旧版本：

```bash
$ sudo apt update
$ sudo apt install nala-legacy
```

`Nala` 是 Apt 的一个前端，兼容大多数 apt 命令。它还有一些可以处理的新命令。

```bash
sudo nala fetch
```

可以帮助你找到最快的镜像以加速包的安装。

此外，Nala 提供了历史记录（参见 Fedora DNF 包管理器历史记录），它记录了更新期间期间的更改，并允许你进行回滚。

```bash
sudo nala history
```

显示最近的操作。它以 ID 形式列出，你可以使用该 ID 来撤销操作，如下：

```bash
sudo nala history undo <id>
```

## 第一人称射击游戏

### Alien Arena

版本：7.71.4 网页：https://alienarena.org

![](img/19f01d8418c50f8361fc6069e917f628_82_0.png)

如果你像我们一样喜欢第一人称射击游戏，你会喜欢 Alien Arena。近二十后，该游戏的科幻主题以及受 Quake 和 Unreal 启发的死斗模式仍然流行，因为它拥有大量的角色、大量的地图和多种可玩类型。

该游戏可以在多个发行版的官方仓库中获得（如 Ubuntu），但为了确保你拥有最新版本，请从 Flatpak 下载：`flatpak install flathub.org/alienarena`。

节奏非常快，尽管它有一个离线练习模式帮助你针对机器人磨练技巧。要玩，你必须先通过可以解锁的地图和角色列表。

游戏支持多种游戏模式，最流行的是抢夺旗帜，其他如死斗、团队核心突击、自由死斗等。

游戏背景设定在一个未来主义宇宙中。

![](img/19f01d8418c50f8361fc6069e917f628_82_1.png)

使用几个人类和外星角色作为你的化身。每个玩家角色的尺寸、可见度和概况大致相同，彼此之间没有优劣之分。当你加入服务器时，你可以选择加入生成地图中的两个竞争队伍之一，虽然人类和外星看起来不同，但它们的行为是完全相同的。

在开始游戏之前，请记住使用游戏的配置选项。通过鼠标和键盘，你还可以更改多种影响游戏性能、画质、可见度以及屏幕显示内容的设置。

![](img/19f01d8418c50f8361fc6069e917f628_82_2.png)

某些 Alien Arena 地图包含陷阱，例如致命陷阱，这为玩家带来了危险。

## 游戏启动器

### Cartridges

版本：2.0.4 网页：https://github.com/lutris/lutris

如果你也有一堆应用，可以使用 Gear Lever 将它们都放在一个地方。默认情况下，所有的 AppImages 都通过 `~/AppImages` 管理。

你可以从应用的“偏好设置”菜单更改位置。默认情况下，Gear Lever 通过将原始文件复制到文件夹来帮助节省空间，但你可以选择保留原始文件并在目标文件夹中创建副本。

![](img/19f01d8418c50f8361fc6069e917f628_81_1.png)

与传统的 apt 相比，Nala 更加现代且直观。例如，`sudo nala list` 会列出所有将安装和升级的包。

![](img/19f01d8418c50f8361fc6069e917f628_81_2.png)

## 热门推荐

### 自定义演示制作

### Cubic

版本：2023.05 网页：https://github.com/Pj-Singh/Cubic

![](img/19f01d8418c50f8361fc6069e917f628_83_0.png)

## 磁盘空间管理器

### Filelight

版本：2023.04 网页：https://apps.kde.org/filelight/

# 你能帮助启发下一代代码爱好者吗？

Code Club 是一个全国性的志愿者主导网络，为 9-11 岁的儿童提供课后俱乐部服务。

我们一直在寻找具备编程技能的人员来担任志愿者，每周在当地的小学、图书馆或社区中心运营一小时俱乐部。

你可以与同事结伴，会有一位老师在场为你提供支持，而且我们会提供你所需的所有材料，帮助激发孩子们对数字制作的兴趣。

有很多参与方式！如需了解更多信息，请访问 www.codeclub.org.uk 加入我们。

# 编程学院 (CODING ACADEMY)

## LXF 冒险之旅

致谢：https://github.com/azuregate

## 文本冒险战斗机制

通常让它看起来像是在玩游戏而不是战争，但这个月 Nate Drake 将我们的互动式冒险带向了一条黑暗、暴力的道路。

我一直在关注之前关于创建你的 Python 文本冒险的教程，你现在应该已经有一个能够让玩家在任意数量房间之间移动并与物品交互的脚本。

这没问题，但大多数地下城通常包含某些风险元素。当然，代码需要创建一个房间让玩家玩，游戏通常会给你每个属性提供一定数量的生命或分数，你必须保护它们。

子类（subclass）具有相同的属性，但也允许你添加你自己的其他属性。我们将使用这个方便工具创建一个名为 `StatItem` 的新类。

### StatItem(Item):

```python
def __init__(self, name, itemdesc, uproomdesc, portable, wearable, usedin, us,
roomadditems, roomusdesc, userodesc,
self.hp, change):
    super().__init__(self, name, itemdesc, uproomdesc,
portable, wearable, usedin,
roomadditems, roomusdesc,
disposable)
```

### 击我

为了让我们的英雄足够强大，我们首先需要更新 `Player` 类以引入 HP 属性。

如你所见，这是原始的 `Item` 类。我们添加了一个新属性 HP。如果 HP 发生变化，游戏将使用 `StatItem`。这表示你的 HP 变化了多少。如果是负值，StatItem 同时涵盖了健康和伤害物品（注意，这有点风险）。

### class Player:

```python
def __init__(self, name, current, keyring, hp):
    self.name = name
    self.current = current
    self.hp = hp
    self.inventory = inventory
```

这意味着我们还需要在脚本开始时为玩家分配攻击次数的变化（现在称为 HP）：

如果你下载了脚本（见下方的“小贴士”），玩家的背包已更改为 `StatItem` 列表：`['Bread', 'Sabred', 'None', 'O']`。现在你可以使用 Sabred 了。这种感觉非常清爽。, None, One, None, True。

```python
self.inventory = [StatItem(name, [0], [1])
```

在这种情况下，我们决定今天免费为玩家增加 10 点 HP 以改变变化，这并不危险，也取决于你想要让你的冒险变得简单还是困难。

我们的玩家现在拥有一个特别显著的物品，因为游戏中没有东西可以伤害到他们！

我们可以更新 `Item` 类来添加此属性，但除非我们使用它，否则很难区分不同类型的物品。在 Python 中，我们有一个子类网络可以做到，它允许我们创建子类。一个

# 我们的专家

Nate Drake 想要决定这一系列老爸，他们曾告诉他，没有人会付钱让他留下来玩游戏。

# 小贴士 (QUICK TIP)

你可以从 https://github.com/azuregate/pythontext adventure/adventure/script.py 下载一个可以更改玩家分数的代码示例

86 LXF 杂志 2023年11月

www.infformat.com

# 文本冒险编程学院

在修改脚本之前，如果玩家能够创建自己的 HP，可能可能有所帮助。最好的做法是更新背包程序：

```python
def inventory():
    print(name)
    print("HP:", hp)
    print("You are carrying:")
    if not inventory:
        print("nothing")
```

在后续系列中，你将知道主冒险中这个脚本包含一个大型金属格栅，你无法移动它。这是因为格栅的 `portable` 属性被设置为 false。不过，并不是让格栅变得不可移动，如果玩家尝试通过拉动它

> 小贴士

> 在编程圈中，从其他类派生新类的方法被称为“继承”。第一个例子就是我们最初创建的文本冒险。

为了做到这一点，我们需要将格栅更改为静态的（Static）

```python
grill = Static("grill", "格栅很旧且生锈了，但有一些锋利的边缘。", None, None, None, 尝试拉并移动格栅，无论你如何努力都会抓伤你的手。它有 3 点 HP, None
```

花点时间回顾一下。在第一情况下，玩家使用 `LOOK` 来检查它，它只是警告那里有一些肉。肉也是通过玩家尝试移动格栅时的受伤产生的。在这种情况下，他们损失了 HP。

```python
if not inventory:
    print("nothing")
else:
    for item in inventory:
        print(item)
```

现在是时候运行脚本或修改后的脚本了。首先，运行 `inventory` 查看玩家 HP 的输出。看板在玩家的背包里。最后，运行 `inventory` 看看你的英雄现在有了 HP

# 承担风险 (Taking risks)

到目前为止，脚本会更改玩家的分数。如果 HP 发生变化，游戏将使用 `StatItem`。这表示你的 HP 变化了多少。如果是负值，StatItem 同时涵盖了健康和伤害物品（注意，这有点风险）。

```python
class Player:
    def __init__(self, name, currentroom, keyring, hp, inventory=[]):
        self.name = name
        self.currentroom = currentroom
        self.keyring = keyring
        self.hp = hp
        self.inventory = inventory
        self.weapon = weapon
```

不要忘记修改玩家对象，但现在保持无武器状态：

```python
player = Player("name", room[1], [10], [bread])
```

由于武器有特殊属性，最好是将它们作为字典列表：

```python
class Weapon(Item):
    def __init__(self, name, itemdesc, updatable, portable, realizable, usedin, 
    removesitem, addsroomitem, usable, damage=0):
        super().__init__(name, itemdesc, updatable, portable, realizable, usedin,
        removesitem, addsroomitem, usable)
        damage = damage
        self.damage = damage
```

正如如此，`Weapon` 子类继承了所有的 `Item` 属性，并在伤害的情况下添加了另一个。这是一个非常有用的技巧，你可以将其用于游戏中的其他特殊物品。

现在你已经创建了它，可以创建自己的武器了。如果你需要一些灵感，看看我们在示例脚本中创建的那个：

`sword = Weapon("Sword", "一把锋利的剑和坚固的刀刃", True, True, False, 2)`
