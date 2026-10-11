
死胡同。
你处于一条道路的尽头。道路向东延伸。你可以看到它最终会分叉。一条路通往皇宫，你感到很惊。
这里有一个铲子。
输入 `shovel`

- **MOON BOGGY** 基于经典的 1982 年街机游戏《月球巡逻》（Moon Patrol），Moon Boggy 出现在 1985 年的家用电脑上。它是一款了 Atari 游戏，可以通过 Linux 终端输入 `sudo apt-get install moon-boggy` 获取。
- moon-boggy

- **让它下雪** 在终端拥有它不是你每天都会遇到的。但如果你感兴趣，请输入：

```
wget https://github.com/comusercontent/1505843/raw/70d2716a57e69fb526322fee09f42c7533614d2/snowjob.sh
chmod +x snowjob.sh
./snowjob.sh
```

享受吧。

# Linux 技巧与技巧

## 内存大户

如果你删除了一个文件，并想查看 Linux 上占用内存最多的程序，只需输入：

```
ps aux --sort -rn4
```

这会根据系统内存对输出进行排序。

## BBS

在拨号上网时代，在线世界是由公告板系统（BBS）组成的。这些远程服务器是用户聊天、交换代码、玩游戏的地方。使用 Telnet，我们仍然可以连接到一些活跃的 BBS。

```
telnet localbestarrabs.dynds.org
```

有无数 BBS 可用，请访问 https://www.telnetbbs.com/bbs/list/detail/ 了解更多。

![](img/383b23573296234863a9f25dc7161abc_64_0.png)

![](img/383b23573296234863a9f25dc7161abc_64_1.png)

## 碎器

当你想要确保软件无法检索回文件时，为了安全且永久地删除文件，请使用：

```
shred -zvu filename.txt
```

将 `REPLACE` 替换为要删除的文件。

## 目录树

如果你想创建一个包含整个目录（文件夹）树，可以使用：

```
mkdir -p New-Dir/{subfolder1,subfolder2,subfolder3,subfolder4}
```

这会创建一个包含四个子文件夹的 New-Dir。

![](img/383b23573296234863a9f25dc7161abc_64_2.png)

![](img/383b23573296234863a9f25dc7161abc_64_3.png)

## ASCII

ASCII 应用于某些图像时效果非常显著。然而，使用以下命令从现有的图像创建出色的 ASCII Art 是困难的：

```
img2txt install NAMEOFIMAGE.png
```

将 `NAMEOFIMAGE` 替换为系统中的实际文件名。安装 `img2txt` 使用：

```bash
sudo apt-get install caca-utils.
```

## 遗忘的命令

记住所有的 Linux 命令并不容易。幸运的是，我们可以使用 `apropos` 在这里帮助我们，并带有命令描述：

```
apropos "copy files"
apropos "rename files"
```

![](img/383b23573296234863a9f25dc7161abc_64_4.png)

![](img/383b23573296234863a9f25dc7161abc_64_5.png)

## Linux 与大爆炸

![](img/383b23573296234863a9f25dc7161abc_65_0.png)

Linux 是碰撞粒子，因此我们可以此理解宇宙是如何运作的。

## 你知道吗...

![](img/383b23573296234863a9f25dc7161abc_66_0.png)

你知道吗...

Linux 是大型对撞加速器背后科学的核心？通过结合 Red Hat 和 CentOS（一种基于 Red Hat 基础构建的超稳定发行版），科学家和工程师开发了不同版本的自己的 Linux 发行版来帮助各个方面。最著名的是 SLC，也称为 CERN。根据报告，有超过 600 台和超过 15,000 台正在运行。

## 编写脚本

Bash 脚本简单来说是一系列运行以完成特定任务的命令。取决于情况，它们可以很简单，也可以非常复杂。

## 创建 Bash 脚本 – 第一部分

最终，由于你在 Linux Mint 中工作，你将想要开始创建自己的自动化任务。这些本质上是 Shell 脚本，工作方式与 DOS 批处理文件或其他任何编程语言相同。

- **步骤 1** 你正在终端中使用文本编辑器工作。文本编辑器有其他方案，为了每个起见，我们稍后查看。在开始之前，运行：
```bash
mkdir scripts
cd scripts/
```
- **步骤 2** 我们有几种方法可以创建 Bash 脚本：Vi、Nano、GNU 等。归根结底取决于个人偏好。倾向于使用编辑器会让你更容易阅读下面的脚本。
- **步骤 3** 为了开始，在你开始编写任何脚本之前，你需要创建一个文件夹将所有脚本放在其中。这将是我们的工作文件夹，你可以在这里创建子文件夹。
- **步骤 4** Windows 用户会知道，为了批处理文件工作，它需要有 BAT 扩展名。Linux 是没有扩展名的操作系统，但习惯是创建 sh 脚本。

![](img/383b23573296234863a9f25dc7161abc_67_0.png)
```bash
mkdir scripts
cd scripts/
```

![](img/383b23573296234863a9f25dc7161abc_67_1.png)
```bash
ls
touch script2.sh
```
- **步骤 5** 从一个向终端输出内容的简单脚本开始。我们创建一个名为 `helloworld.sh` 的文件。在编辑器中，它将启动并输入内容：`#!/bin/bash`，然后新起一行：`echo Hello World!`
- **步骤 6** `#!/bin/bash` 行告诉系统你将变成什么，在这种情况下。Bash 中的 # 表示注释行，系统会忽略该行，感叹号 (!) 表示跳过命令检查并将强制脚本将该行作为命令执行。这也被称为 Hash-Bang（井号）。
- **步骤 7** 当你再次输入 `ls` 时，你可以发现 `helloworld.sh` 现在从蓝色变成了绿色，这意味着它现在是一个可执行文件。换句话说，在脚本中，它执行了你输入的内容：`./helloworld.sh`。

```bash
ged helloworld.sh
ls
chmod +x helloworld.sh
ls
./helloworld.sh
```
- **步骤 8** 你可以保存文件，点击文件 -> 保存，回到终端。
- **步骤 9** 输入 `ls` 后，你可以看到 `helloworld.sh` 现在已经从蓝色变成了绿色。
- **步骤 10** 将 `echo` 视为打印命令。它显示文本，例如当前日期。尝试示例：`echo Hello World! $(date)`。

```bash
#!/bin/bash
echo Hello World! Today is $(date)
```
echo Hello World! Today is %s

## 创建 Bash 脚本 – 第二部分

之前我们查看了创建第一个脚本 Hello World 并添加系统变量。现在你可以扩展这些内容并看看当你开始尝试创建自己的变量时可以做什么。

## 变量

就像其他编程语言一样，Bash 脚本可以存储和调用系统变量，无论是全局还是用户的。

- **步骤 1** 让我们从创建一个名为 `helloworld.sh` 的新脚本开始；`ged helloworld.sh`。在里面：`#!/bin/bash`，然后 `echo Hello World!` 保存文件并退出。在终端中赋予脚本执行权限：`chmod +x helloworld.sh`。
- **步骤 2** 你可以重命名变量。修改 `hello.sh` 脚本如下：`firstname=$1 surname=$2 Hello $firstname $surname`。将每个语句放在新行。
- **步骤 3** 输出现在将是 Hello David。这是因为 Bash 自动为用户分配变量，这些变量会被持有并传递给脚本。`$1` 现在持有 David。你可以通过输入其他内容来更改变量：`./helloworld.sh Mint`。
- **步骤 4** 你可以重命名变量。修改 `hello.sh` 脚本如下：`firstname=$1 surname=$2 Hello $firstname $surname`。
