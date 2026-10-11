

## 如何在 Linux 中设置 Python

虽然 Raspberry Pi 的操作系统包含最新稳定版的 Python，但其他 Linux 发行版并未预装 Python 3。如果你不打算采用 Pi 路线，以下是检查并在 Linux 中安装 Python 的方法。

### 企鹅与 PYTHON

Linux 是一个功能极其强大的操作系统，以至于往往很难确定某项操作的唯一执行方式。不同的发行版通过不同的方式安装软件，因此本教程将使用 Linux Mint。

- **步骤 1**  
首先，你需要确定当前 Linux 系统中安装了哪个版本的 Python。为此，可以从发行版的菜单进入终端会话，或按下 Ctrl+Alt+T 键。

![](img/4aefeb2d095f688b34af6207870c5f39_9_0.png)

- **步骤 2**  
接着在终端中输入 `python --version`。你应该会在显示中看到与 Python 2.x 版本相关的输出。默认情况下，大多数 Linux 发行版同时自带 Python 2 和 3，因为目前仍有许多 Python 2 的代码可用。然后输入：`python3 --version`。

![](img/4aefeb2d095f688b34af6207870c5f39_9_1.png)

- **步骤 3**  
在我们这个案例中，Python 2 和 3 均已安装；只要安装了 Python 3.x，我们教程中的代码就可以运行。检查发行版是否已更新至最新版本总是值得的，因此输入 `sudo apt-get update && sudo apt-get upgrade` 来更新系统。

![](img/4aefeb2d095f688b34af6207870c5f39_9_2.png)

- **步骤 4**  
更新和升级完成后，再次输入 `python3 --version` 以查看 Python 3.x 是否已更新或安装；只要你拥有 Python 3.x，你就正在使用最新的重大版本。3. 后面的数字表示补丁和进一步的更新。通常这些是不必要的，但可能包含重要的新元素。

![](img/4aefeb2d095f688b34af6207870c5f39_9_3.png)

![](img/4aefeb2d095f688b34af6207870c5f39_10_0.png)

然而，如果你想要最新的前沿版本，你需要从源代码构建 Python。首先将这些命令输入到终端中：

- **步骤 5**

```bash
sudo apt-get install build-essential checkinstall
sudo apt-get install libssl-dev liblz2-dev libncurses5-dev libssl-dev libgdbm libsqlite3-dev tk-dev
libtcl-dev-dev libbz2-dev libg2z2-dev
```

![](img/4aefeb2d095f688b34af6207870c5f39_10_1.png)

- **步骤 6**

打开你的 Linux 网络浏览器，前往 Python 下载页面：www.python.org/downloads。点击 Downloads，然后是 Python Source 窗口下方的按钮。这将打开一个下载对话框；选择一个位置并开始下载过程。

![](img/4aefeb2d095f688b34af6207870c5f39_10_2.png)

- **步骤 7**

在终端中，通过输入 `cd Downloads/` 进入 Downloads 文件夹。然后使用 `tar -xvf Python-3.Y.Y.tar.xz` 解压下载的 Python 源代码内容，将 Y 替换为你下载的版本号。现在使用 `cd Python-3.Y.Y/` 进入新解压的文件夹。

![](img/4aefeb2d095f688b34af6207870c5f39_10_3.png)

- **步骤 8**

在 Python 文件夹内，输入：

```bash
./configure
sudo make altinstall
```

根据计算机速度，这可能花费一些时间。完成后，输入 `python3.7 --version` 以检查安装的最新版本。你现在已安装了 Python 3.7，与较旧的 Python 3.x.x 和 Python 2 并存。

![](img/4aefeb2d095f688b34af6207870c5f39_10_4.png)

- **步骤 9**

对于 GUI IDLE，你需要在终端中输入以下命令：

```bash
sudo apt-get install idle3
```

然后可以使用命令 `idle3` 启动 IDLE。请注意，IDLE 运行的版本与从源代码安装的版本不同。

![](img/4aefeb2d095f688b34af6207870c5f39_10_5.png)

- **步骤 10**

你还需要 PIP（Pip Installs Packages），它是一个帮助你安装更多模块和附加组件的工具。

输入：`sudo apt-get install python3-pip`

当 PIP 安装完成后，使用以下命令检查最新更新：`pip3 install --upgrade pip`

完成后，关闭终端，Python 3.x 将通过发行版菜单中的 Programming 部分可用。

![](img/4aefeb2d095f688b34af6207870c5f39_10_6.png)

## 首次启动 Python

如果你使用的是新款 Raspberry Pi 及其最新发布的 Pi OS，你需要手动安装 Python IDLE。这是因为 Pi 团队移除了核心 Python IDLE，转而采用他们自己的代码文本编辑器。

### 启动 PYTHON

对于使用 Pi4 和新的 Raspbian 的用户，进入终端并输入：`sudo apt-get install idle3`。旧版本的 Raspbian 已预装官方 Python IDLE。

- **步骤 1**

加载 Raspbian 桌面后，点击 Menu 按钮，然后选择 Programming > Python 3 (IDLE)。这将打开 Python 3 Shell。Windows 和 Mac 用户可以在 Windows 开始按钮菜单内以及通过 Finder 找到 Python 3 IDLE Shell。

![](img/4aefeb2d095f688b34af6207870c5f39_11_0.png)

- **步骤 2**

Shell 是你可以输入代码并查看代码响应和输出的地方。这是一种沙箱，你可以在此尝试一些简单的代码和过程。

![](img/4aefeb2d095f688b34af6207870c5f39_11_1.png)

- **步骤 3**

例如，在 Shell 中输入：`2+2`。按下回车后，下一行将显示答案：4。基本上，Python 接受了“代码”并产生了相关的输出。

![](img/4aefeb2d095f688b34af6207870c5f39_11_2.png)

- **步骤 4**

Python Shell 的行为非常像计算器，因为代码基本上是与系统的一系列数学交互。整数（无限序列的整数）可以轻松地相加、相减、相乘等。

![](img/4aefeb2d095f688b34af6207870c5f39_11_3.png)

- **步骤 5**

虽然这很有趣，但并不特别令人兴奋。相反，请尝试这个：

`print("Hello everyone!")`

只需像前几步一样将其输入到 IDLE 中即可。

![](img/4aefeb2d095f688b34af6207870c5f39_12_0.png)

- **步骤 6**

这更有意思，因为你刚刚编写了第一段代码。Print 命令相当直观，它打印内容。Python 3 需要括号和引号才能将内容输出到屏幕，在本例中是 `Hello everyone!` 部分。

```python
>>> print("Hello everyone!")
Hello everyone!
>>> 
```

- **步骤 7**

你可能已经注意到 Python IDLE 内的颜色编码。这些颜色代表 Python 代码的不同元素。它们如下：

黑色 – 数据和变量  
绿色 – 字符串  
紫色 – 函数  
橙色 – 命令  
蓝色 – 用户函数  
深红色 – 注释  
浅红色 – 错误消息

#### IDLE 颜色编码

| 颜色 | 用途 | 示例 |
| :--- | :--- | :--- |
| 黑色 | 数据与变量 | `23 . 6` `<area` |
| 绿色 | 字符串 | `"Hello World"` |
| 紫色 | 函数 | `len() print()` |
| 橙色 | 命令 | `if for else` |
| 蓝色 | 用户函数 | `get_area()` |
| 深红色 | 注释 | `#Remember VAT` |
| 浅红色 | 错误消息 | `SyntaxError:` |

- **步骤 8**

Python IDLE 是一个可配置的环境。如果你不喜欢颜色表示的方式，你始终可以通过 Options > Configure IDLE 并点击 Highlighting 选项卡来更改它们。然而，我们不建议你这样做，因为你看到的效果将与我们截图中的不同。

![](img/4aefeb2d095f688b34af6207870c5f39_12_1.png)

- **步骤 9**

与大多数可用的程序一样，无论操作系统如何，都有许多快捷键可用。这里没有空间列出所有快捷键，但在 Options > Configure IDLE 的 Keys 选项卡下，你可以看到当前绑定列表。

![](img/4aefeb2d095f688b34af6207870c5f39_12_2.png)

- **步骤 10**

Python IDLE 是一个强大的接口，实际上是用 Python 编写的，使用了可用的 GUI 工具包之一。如果你想知道 Shell 的许多细节，我们建议花几分钟时间查看 www.docs.python.org/3/library/idle.html，其中详细说明了 IDLE 的许多功能。

```
25.5.5. IDLE
Source code: Lib/idle
This file is part of Python's Integrated Development and Learning Environment...
* **25.5.1. Main menu**
* **25.5.1.1. File menu (Shell and Editor)**
* **25.5.1.2. Edit menu**
```

