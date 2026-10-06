
2. 输入 `mv Downloads/pywings\*.gz pywings` 并按 ENTER，将 pyWings tar 包移动到该文件夹。

你可以从这一步看到，你使用了星号 (*) 来减少手指的负担。星号是一个通配符，在这种情况下，它告诉你的系统移动任何以 pywings 开头并以 .gz 结尾的文件。幸运的是，你只有一个符合这些标准的项目。

3. 输入 `cd pywings` 并按 ENTER，进入新的 pyWings 文件夹。

4. 现在开始使用 `tar` 命令解压 tar 包本身了。要执行此操作，输入 `tar -xvf pywings\*` 并按 ENTER。

再次注意，你使用了星号来减少键盘击击次数，尽管你完全可以输入 `-1.1.tar`。

5. 最后，输入 `cd` 并按 ENTER，将终端带回主目录（Home folder）。

## 8B-5: 将 pyWings 文件夹移动到你的 LocalApps 文件夹

解压过程现在已完成。在继续运行 pywings 之前，让我们到第 144 页“8B-3：为 pyWings 创建 LocalApps 文件夹”中创建的新 LocalApps 文件夹。要执行此操作，输入以下命令并按 ENTER：

```
mv pywings LocalApps
```

## 8B-6: 运行 pyWings

现在你已经准备好了 pyWings 准备就绪，让我们现在就启动这个伟大的神谕，这样你就能更好地了解处理困扰你的生活的各个方面。

在终端中，确保你处于主目录，输入以下命令，然后按 ENTER：

```
~/LocalApps/pywings/pywings.py
```

由于 pywings.py 是一个 Python 脚本而不是应用程序，你是在引起 pyWings 的注意，Python 将知道它需要处理该脚本。如果一切进展顺利，pyWings 很快就会让你成为赢者。

## 8B-7: 为 pyWings 创建一个可启动的链接

你刚刚使用的运行 pyWings 的方法足够用了。然而，每当你想知道命运安排了什么时，都要打开终端并输入那段相当长的命令，这很麻烦。让我们找到一种以后更容易的方法。

要从终端运行应用程序，你通常输入该应用程序的名称，或者准确地说，输入你的程序可执行文件的名称；应用程序的名称充当了某种命令。然而，为了让你的系统识别该命令，命令（可执行文件或指向它的链接）必须位于系统可以找到它的位置。每当你运行任何类型的命令时，你的系统都会检查一系列位置（大部分是 bin 文件夹，可执行文件位于那里）来查找该命令。

你可以通过在新终端窗口中输入 `echo $PATH` 并按 ENTER 轻松找到这些位置。你会发现，在你的 Ubuntu 系统上，这些位置如下：

```
/n/usr/lib/lightdm/lightdm
/usr/local/sbin
/usr/local/bin
/usr/sbin
/usr/bin
/bin
/usr/games
```

`echo $PATH` 命令的结果不会像这里显示的（更易读的）咒语那样按行划分，而是以冒号分隔的单行显示：终端中的实际输出为 `/usr/lib/lightdm/lightdm:/usr/local:/usr/local/bin:/usr/sbin:/sbin:/bin:/usr/games`。

如果你输入的命令位于这些位置之一，程序或脚本将运行。但你毫无疑问，pyWings 不在这些任何位置中。它在 `/home/username/LocalApps/pyWings`，因此在某种意义上，它在你系统的视野之外。

为了弥救这种情况，你可以将 pyWings 脚本的路径添加到系统检查运行命令的路径列表中，以便系统感知你新应用程序的存在。然而，让我们尝试另一种我认为更简单的方法。你要做的是在你系统检查的位置之一中创建一个指向 pyWings 的链接，一种类似于可启动的别名。

要创建此链接，你将使用三个命令：`cd`（更改目录）、`sudo`（赋予自己对目标文件夹的写入权限）和 `ln -s`（创建链接）。

- 1. 在终端中，输入 `cd /usr/games` 并按 ENTER。这让你置于你输入命令时会搜索的文件夹之一。
- 2. 输入 `sudo ln -s /home/username/LocalApps/pywings/pywings.py pywings` 并按 ENTER。（注意在该命令字符串末尾 `pywings.py` 和 `pywings` 之间有一个空格）

命令字符串末尾的 `pywings` 是你赋予链接的名称；因此链接的名称将成为你运行应用程序时使用的命令。如果你什么都不输入，链接将命名为 `pywings.py`，这意味着你每次启动程序都要敲击三次键盘。
- 3. 在提示时输入你的密码，然后按 ENTER。
- 4. 现在通过更改权限让你的启动器变为可执行：输入 `sudo chmod +x pywings` 并按 ENTER。
- 5. 输入 `cd` 并按 ENTER 返回终端到主目录。

## 8B-8: 再次运行 pyWings

现在你已经创建了链接，你应该能够更轻松地运行 pyWings 程序了。要尝试一下，退出 pyWings（如果它仍在运行），在终端窗口中输入 `pywings` 并按 ENTER。你的 pyWings 神谕应该再次出现。
你成功减少了从终端运行 pyWings 所需的击键次数。然而，如果你真的喜欢这个 pyWings 并且经常运行使用它，那么在你的面板、抽屉或应用程序菜单中添加一个启动器可能是最方便的。

## 项目 8C: 使用 Briscola 进行命令练习复习

现在你想强化在在上项目中用到的技能，为什么不尝试一下欧洲大陆风格的 Briscola（纸牌）呢？Briscola 是一种简单、非常传统的意大利纸牌游戏（见图 8-13），在克罗地亚和波斯尼亚黑塞的亚德里亚地区也以 briskula 之名广泛流行，在西班牙和墨西哥也被称为 briscas。与 Python 脚本的 pyWings 不同，Briscola 是一个不同风格的脚本。它用一种名为 T 的脚本语言编写，并使用 Tk 创建其图形界面——与 pyWings 界面使用的是相同的 Tk。

![](img/d35fa962e6f9664d66dc83916f42641f)

图 8-13：Briscola

## 8C-1：获取 Briscola

你正准备好“安装”Briscola，但在那之前，你必须获取它。你可以通过访问 http://www.rigacci.org/wiki/doku.php/technica/download/local_software 以传统方式来获取 Briscola，但由于我们正在使用命令，让我们用新命令 `wget` 来获取 Briscola。

要执行此操作，只需打开终端窗口，输入以下命令字符串并按 ENTER：

```
wget http://www.rigacci.org/comp/software/briscola/briscola-4.1.tar.gz
```

在终端中，你会看到 wget 在运行，它连接到存储 Briscola 的站点并下载文件。完成后，你将在主目录下找到 Briscola tar 包。

## 8C-2：解压 Briscola tar 包并重命名 Briscola 文件夹

解压 Briscola tar 包的过程与 pyWings 基本相同。不同在于 Briscola 已经封装在文件夹中，所以你不需要为它创建一个特殊的文件夹。

你知道该做什么：只需打开终端窗口，输入以下命令并按 ENTER：

```
tar -xzvf briscola.*
```

一个新的文件夹 `Briscola-4.1` 将出现在主目录下，包含所有的 Briscola 文件。为了方便以后处理，让我们文件夹名称缩短为简单的 `briscola`。你已经知道如何通过右键方法执行此操作，这次让我们尝试通过命令行完成。你可能感到惊讶地使用了 `mv` 命令，后面跟着你要更改的文件名，然后是新文件名。

输入以下命令并按 ENTER 进行尝试：

```
mv briscola-4.1 briscola
```

## 8C-3：准备 Briscola 脚本

大多数以 tar 形式提供的应用程序都包含一个 README 文件，其中包含了安装和使用该应用程序的信息。如果你在文件管理器的 `briscola` 文件夹中双击 README 文件，你会看到“如何启动”（HOW TO START）部分告诉你指向你的 Tk 壳，并调整 `briscola.tk` 脚本的第二行以指向各种 Briscola 文件所在的目录。

