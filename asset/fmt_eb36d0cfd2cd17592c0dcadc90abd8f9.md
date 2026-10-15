
你肯定已经注意到，为了创建子文件夹`sub`，你在`command_exp`后面使用了一个斜杠（`/`）。基本上，当你使用斜杠时，你是在告诉系统在斜杠右侧的位置执行命令，并且告诉系统该文件位于斜杠左侧的文件夹中。在本章的剩余部分，你还将看到更多关于斜杠用法的示例。

### `$ cd`

直到现在，你一直在主文件夹中使用命令行。通过`cd`（change directory，改变目录）命令，你可以在控制台中通过输入该命令后跟你想进入的文件夹名称，从一个文件夹切换到另一个。为了试一试，让我们通过输入`cd command_exp`并按 ENTER 进入`command_exp` 文件夹。如果你做对了，控制台中的提示符现在应该显示为`username@computer-name:~/command_exp$`。如果是这样，你可以自我鼓掌了。

### `$ cp`

`cp`（copy & paste，复制和粘贴）命令允许你一次性复制文件并将其粘贴到新位置。为此，命令需要知道你要复制的文件在哪里、它叫什么名字，以及你想把它复制到哪里。要尝试一下，请复制你主文件夹中碰巧有的任何文件，并将其粘贴到你的`command_exp` 文件夹中。例如，在我的情况下，我想把主文件夹中名为`tawas.png` 的文件复制到我的`command_exp` 文件夹中。因此我输入`cp tawas.png command_exp/` 并按 ENTER，然后我将在我的`command_exp` 文件夹中拥有`tawas.png` 的一个副本。`cp` 命令后的第一个表达式是你正在复制的文件（`tawas.png`）；第二个表达式这是粘贴目标位置（`command_exp/`）。尝试操作后，请查看你的`command_exp` 文件夹内部，确认你复制的文件确实在那里。

那么，如果你想复制的文件不在你的主目录（Home folder）中会发生什么？举个例子，假设你的`tawas.png` 文件位于`command_exp` 文件夹中，而你想将它的副本放置在一个同样位于`command_exp` 文件夹内的`happy_pics` 文件夹中。嗯，实际上你有几种方法可以做到这一点。

一种方法是先使用你刚才学到的`cd` 命令进入`command_exp` 文件夹。然后输入`cd command_exp`，接着按下 ENTER，此时你就位于`command_exp` 文件夹中。接着使用`cp` 命令复制`tawas.png` 文件并将其粘贴到`happy_pics` 文件夹中，方法是输入`cp tawas.png happy_pics/`，然后按下 ENTER。

第二种替代方案是仅使用`cp` 命令，一口气完成所有操作。要采用这种路径，请输入`cp command_exp/tawas.png command_exp/happy_pics/`，然后按下 ENTER。这条路径同样有效，尽管需要多输入一些内容。

### `rm`

正如名称所示，`rm`（remove）命令用于删除文件和空文件夹——这类似于将项目移至废纸篓的命令行版本。`rm` 命令虽然非常有用且易于使用，但应谨慎使用。一旦使用此命令删除文件，就无法回头——文件将永久消失。

为了安全起见，让我们通过清理刚才移动到`command_exp` 文件夹中的那个新文件副本来试用`rm` 命令。基本的`rm` 命令结构由命令本身`rm` 组成，后跟你要删除的文件名。假设你的控制台显示你当前位于主目录，你可以通过输入`rm command_exp/` 并点击 `⏎ ENTER` 键来删除该文件。文件随后将消失，并且永久消失。

如果文件不在主目录中，只需使用`cd` 命令移动到存放该文件的文件夹，然后在那里使用`rm` 命令。与`cp` 命令一样，你可以通过输入`rm foldername/filename` 并按下 ENTER 一次性完成同样的操作。

既然基本上已经完成了实验过程，你不妨把`command_exp` 文件夹也删掉。但是，由于该文件夹包含一个子文件夹（`sub`），`rm` 命令无法完成此任务。这是因为，正如我之前提到的，该命令仅用于删除文件和空文件夹。若要删除文件夹及其内容，你需要添加递归标志`r`。为此，只需输入`rm -r command_exp`，然后按下 ENTER。你的`command_exp` 文件夹及其内部的子文件夹将只成为一段记忆。

## 项目 20A：命令练习——播放加密 DVD

正如你在第 15 章中学到的，Xandros 出于法律原因，默认不包含加密 DVD 的播放支持，这确实给事情带来了障碍，因为大多数商业 DVD 都是加密类型的。好消息是你可以安装加密 DVD 播放的支持。然而，唯一的方法是透过命令行，这是一个很好的例子，说明了命令有时如何派上用场。如果你需要或想要播放 DVD，并借此机会练习命令行操作，只需跟随这个简短项目的剩余部分即可。

### 20A-1：下载并安装 libdvdread3

要播放加密 DVD，你需要安装`libdvdcss`，你可以从包含在`libdvdread3` 包中的脚本获取它。该系统可能已经安装了此包，所以首先查看它是否存在是个好主意。如果没有，你可以轻松通过 Xandros Networks 安装它。以下是你需要做的：

1. 打开一个控制台窗口，输入`locate libdvdread3`，然后按下 ENTER。
2. 如果各种 `libdvdread3` 文件的位置作为搜索结果被列出，请继续前往第 20A-2 部分。否则，如果没有任何内容显示，你需要安装`libdvdread3` 包，可以通过运行 Xandros Networks 应用程序来实现，在其搜索框中输入：`libdvdread3`，点击`Search`，然后点击结果下方面板中`libdvdread3` 旁边的`Install`。

### 20A-2：下载并安装 libdvdcx

如前所述，仅凭`libdvdread3` 包无法让你播放加密 DVD。相反，它是一种用于下载和安装`libdvdcx` 的手段，而后者才是此处的关键所在。由于`libdvdcx` 必须通过（控制台）下载，你在执行以下操作时必须连接到互联网：

1. 通过输入`su`，按下 ENTER，在提示时输入你的 root 密码，然后再次按下 ENTER 来获得 root 权限。
2. 输入`/usr/share/doc/libdvdread3/examples/install-css.sh` 并按下 ENTER。

这个相当长的命令字符串告诉你的系统运行名为`install-css.sh` 的脚本，它位于`examples` 文件夹中，`examples` 文件夹位于`libdvdread3` 文件夹中，`libdvdread3` 文件夹位于`doc` 文件夹中，`doc` 文件夹位于`share` 文件夹中，`share` 文件夹位于`usr` 文件夹中。哇！哦，并且命令字符串开头的正斜杠（`/`）告诉你的系统`usr` 文件夹位于文件系统的根目录下，而不是在你的主目录中。

> **注意**
> 如果你处于防火墙后面，且必须在 Internet 应用程序中指定代理服务器，请在步骤 1 之后输入`export http_proxy=http://yourproxyserveraddress:portnumber/`（示例：）`export http_proxy=http://proxy.jellyfish.me:3128/`，在继续到步骤 2 之前按下 enter。

随后，下载和安装的进度将在控制台窗口中显示。当你再次看到用户提示符时，你就知道安装已完成。之后，你应该能够通过启动菜单（应用程序 ▶ 多媒体 ▶ 视频播放器）运行 Xine，并播放几乎任何你想看的 DVD（除了区域编码限制外），不过在此之前重启机器可能是个好主意。

## 项目 20B：更多关于 Briscola 的命令练习

如果你想更多地练习使用我们涵盖的命令，并了解命令行如何让你访问通过 Xandros Networks 不可用的其他程序，何不尝试一下这个项目。你将在这个项目中安装的程序是一个简单但非常传统的意大利纸牌游戏，叫做 Briscola（见图 20-5）。

![](img/3badae5570de77b990135448f8a8a1cc_439_0.png)

图 20-5：Briscola

### 20B-1：获取 Briscola 文件

好的，现在你几乎准备好开始安装 Briscola 了，但在此之前，你必须获取你需要的文件。首先，你需要 Briscola 本身，你可以从项目的主页`www.rigacci.org/~comp/software` 获取。如果你在那里获取文件遇到困难，你也可以从我为这本书建立的网站获取一份副本：`www.edgy-penguins.org/LME`。
