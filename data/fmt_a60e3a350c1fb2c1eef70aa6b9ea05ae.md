
```
sudo mv briscola /usr/share/games/briscola
```

当提示输入密码时，输入并按回车。

## 8C-5：为 Briscola 创建可启动的链接

尽管你已经将 Briscola 移动到了全局位置，但你仍然无法通过简单的单词命令运行它，因为 `briscola.tk` 文件不在系统的命令路径中。就像你对 pyWings 执行的那样，现在你为 Briscola 创建一个可启动的链接来解决这个问题。以下是步骤：

- 1. 在终端中，输入 `cd /usr/games` 并按回车。
- 2. 输入 `sudo ln -s /usr/share/games/briscola/briscola.tk briscola` 并按回车来创建链接。
- 3. 输入 `cd` 并按回车返回终端的个人主目录。

你可以通过在终端中输入 `Briscola` 并按回车来轻松运行 Briscola。

## 你能对 pyWings 执行同样的操作吗？

可以。如果你想将 pyWings 移动到全局位置，只需按照你对 Briscola 执行的移动文件夹和创建链接的步骤操作，当然要进行必要的替换。不过，你必须通过输入以下命令并按回车移除之前创建的 pyWings 链接：

```
sudo rm /usr/games/pywings
```

之后，输入 `sudo mv ~/LocalApps/usr/share/games/pywings` 并按回车将 pywings 文件夹移动到全局区域。当提示密码时，输入并按回车。然后你可以通过 `cd /usr/games` 并按回车，输入 `sudo ln -s /usr/share/games/pywings/pywings.py pywings` 并再次按回车来创建可启动链接。

## 玩 Briscola

如前所述，Briscola 非常简单——它是最简单的纸牌游戏之一。这是一种吃牌游戏（trick-taking game），意味着你出一张牌，对手也出一张牌，点值最高的人赢得这一回合。得分根据该回合涉及的牌来计算。回合的获胜者将进入下一回合，这意味着获胜者下一次出牌。当所有牌都打完后，计算每个玩家的分数，分高者胜。这样描述要简单得多。

如果你想查看更详细的 Briscola 规则（以及世界上任何其他纸牌游戏），请查看 http://www.pagat.com/。YouTube 上也有视频教程，我最喜欢 http://www.youtube.com/watch?v=jpXMbNPN8c。

## 项目 8D：从源码编译并安装程序——Xmahjong

尽管在早期更常见，但“从源码编译程序”这个短语在 Linux 世界听起来比在任何任何地方多。对于初学者来说，仅仅是提到从源码编译程序似乎就让人望而却畏。“编译”和“源码”这两个词似乎会在新用户心中产生一种不安感。至少对我来说确实是这样。

你可以不理会任何事情也能生活富荣，你也可以通过更方便的 Ubuntu 软件中心安装程序。尽管如此，一旦进入 Linux 世界，你很可能会产生好奇，特别是当你进入社区中更极客的部分时。

## 什么是源码？

为了开始，理解什么是源码可能是一个好主意，以便了解程序是如何从程序员计算机上的原始状态蜕变为你机器上运行的应用程序的。首先，程序员用编程语言编写一个程序。你可能以某种形式见过源码。

源码是程序的可读版本。计算机无法直接执行它；它必须先翻译成机器码，即处理器可以理解的一系列 0 和 1。这种翻译过程被称为编译。

将源码翻译成机器码有几种不同的方法。一种方法是使用编译器，它一次性翻译整个程序。另一种方法是使用解释器，它逐行翻译并执行代码。编译器通常比解释器快，因为翻译只进行一次。然而，解释型程序通常更容易调试和修改，因为代码是实时翻译的。

总结来说，源码是所有软件的基础。它是程序员编写、测试和维护程序时编写的人类可读指令。通过理解源码，你可以更好地理解软件是如何工作的，以及如何自己创建它。

发行版，你会发现这种方式对眼睛友好得多，而且色彩更加丰富（访问项目网站 http://www.lcdf.org/xmahjongg/ 可以一略其全彩模式的盛丽）。

![](img/d35fa962e6f9664d66dc83916f426418_190_0.png)

图 8-15：Xmahjongg 游戏

Xmahjongg可以通过 Ubuntu 软件中心获取，因此没有绝对必要按照你正准备的方式进行安装，但这样做提供了一个学习如何从源码编译程序的绝佳机会。源代码的量并不大，但编译不会花费太多时间，而且不需要任何费心。

要开始操作，你必须下载 Xmahjongg 的源码。你可以从 Xmahjongg 项目页面 http://www.lcdf.org/xmahjongg/ 获取。下载 tar 包 `xmahjong-3.7.tar`，或者如果有更新的版本则下载新版本。不要下载该页面上提供的任何其他类型的文件。

如果你愿意，也可以使用你在第 148 页“8C-1: 获取 Briscola”中学习的 `wget` 命令来下载 Xmahjongg tar 包。只需打开终端窗口，输入以下命令：

```
wget http://www.lcdf.org/xmahjongg/xmahjongg-3.7.tar.gz
```

一旦文件已在你的硬盘上，请解压 `xmahjongg-3.7.tar.gz` 文件。你可以像在本章早些时候学的那样使用命令行，也可以通过双击文件将其内容拖入适当的文件夹中。为了方便你跟随我提供的说明，请务必将解压后的 Xmahjongg 文件夹放在你的家目录（Home folder）中。然后你就可以准备运行了。

通常情况下，你会查看该文件夹以寻找一些处理该包的说明，就像你之前在本章中处理 Briscola 时做的那样。在大多数源码包中，这些信息都包含在 `INSTALL` 文件中，例如 `xmahjongg-3.7` 文件夹中的那个文件（图 8-16）。要读取 `INSTALL` 文件，只需双击它，它将在文本编辑器中打开。

## xmahjongg-3.7

| Devices | Home xmahjongg-3.7 | pywings |

| --- | --- | --- | --- |

| 127 GB ... | | include | libcdf | share |

| Computer | | | | |

| Home | images | | | |

| Desktop | | | | |

| Documents | | | | | |

| Downloads | src | aclocal.m4 | configure |

| Music | | | | |

| Pictures | | config.h.h | | | |

| File System | configure.in | depcomp | INSTALL | install-sh |

| Trash | | # Make # # C C | | NEWS |

| Network | Makefile.am | Makefile.file | missing | | | |

| Browse... | | TODO | | xmahjongg.6 | xmahjongg.spec |

| | | | | | |

| | "INSTALL" selected (7.5 kB) | | | | |

8-16：识别包的 INSTALL 文件

在这种情况下，你可以直接关闭 `INSTALL` 文件，因为其所规定的步骤和我接下来列出的步骤相同。然而，在将来当你从源码安装其他程序时，你需要遵循随源文件的 `INSTALL` 文件中的说明。坦率地说，`INSTALL` 中的说明将与我要描述的过程匹配。

当然，很有可能在你查看了 `INSTALL` 文件的内容后，开始好奇它是用什么外星语言编写的。当你完全不知道 `INSTALL` 文件在说什么时，只需在包文件夹中寻找 `configure` 文件。如果你找到了一个，就应该能够按照该项目的说明进行操作。

## 8D-3：为 Xmahjongg 运行 configure 和 make

现在你已经下载并提取了 `xmahjongg` tar 包，安装过程就非常标准了。以下是你需要做的操作：

- 1. 打开终端并输入 `cd xmahjongg` 然后按回车进入新文件夹。下一步是某种的设置阶段，`xmahjongg-3.7` 文件夹中的 `configure` 脚本会检查它需要的文件、编译器和其他内容，然后搜索你的电脑以查看这些内容是否存在；如果是的话，它将根据这些信息写入一个名为 `Makefile` 的文件，这是一组指令，将告诉后续步骤中的 `make` 命令如何专门为你的系统进行设置。
