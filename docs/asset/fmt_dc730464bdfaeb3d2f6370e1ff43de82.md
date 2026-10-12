
如果你计划这样做，你可能会发现使用`Crouton`的`-n`选项为每个`chroot`命名更方便，否则它们只是以发行版命名。命名在安装多个发行版时很重要，因为运行启动命令时需要名称，否则`Crouton`只会加载第一个找到你指定目标的发行版。添加`-n`，如此，可以确保加载正确的发行版：

```
sudo startunity -n saucy
```

`Crouton`还安装了一些有用的工具，特别是`edit-chroot`。可用于备份`chroot`。

```
sudo edit-chroot -b saucy
```

在`~/Downloads`中创建备份文件，你可以用以下命令恢复：

```
sudo edit-chroot -r ~/Downloads/backup-file.tar.gz
```

将其复制到安全位置。即使执行完全重置/恢复，你也可以重新下载`Crouton`并运行以下命令来恢复它：

```
sudo sh -e ~/Downloads/crouton -f backup-file.tar.gz
```

你也可以使用`delete-chroot`删除`chroot`，这你自己也能想出来，或者你可以简单地从`/usr/local/chroots`删除其所在目录以返回原版`Chrome OS`。当然，前提是你想这么做。继续翻到下一页的步骤…

## 术语解释！

### chroot

程序被锁定在其中的目录。它无法看到

## 快速提示

尝试多个发行版或目标时，清理已完成使用的。每个都有数`GB`大小，你的存储很快就会消失。

## 安装发行版

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_57_0.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_57_1.png)

### 1 打开 shell

按`[Ctrl]`+`[Alt]`+`[T]`打开终端窗口。这将是一个在浏览器标签中运行的基础`Crosh` shell，其命令集有限——输入`list`可查看它们。其中一个命令是`shell`，它会给你一个完整的`Bash` shell，像其他发行版一样。没错——`Chrome OS`背后有一个真正的`Linux`操作系统。

### 2 选择发行版和目标

使用`-t list`运行`Crouton`会显示所有可用目标。你可能想要其中一个标准桌面环境。`Chromebook`相对性能较低，像`LXDE`这样轻量级桌面是不错的选择，而`Unity`更适合全屏运行所有内容。

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_57_2.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_57_3.png)

### 3 加密你的文件

在`Crouton`命令行中添加`-e`（这与`sh`后面的`-e`不同）会使你的`chroot`存储在加密目录中。选择一个合适的密码短语——这是保护你文件的一切，但请记住你大部分数据可能保存在云端，因为`Chromebook`存储空间非常有限。

### 4 安装发行版

因为`Crouton`只是一个安装程序，它需要在安装前下载发行版文件，因此请预留时间。即使连接很快，如果你选择了大型目标，下载和安装所有内容可能需要超过`30`分钟——大小显示在`crouton -t list`的输出中。

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_57_4.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_57_5.png)

### 5 添加包管理器

默认目标仅包含命令行包管理器`apt-get`。对大多数人来说，第一步是打开终端并用它安装更友好的选项，例如`Ubuntu`的`software-center`或`Ubuntu`/`Debian`的`Synaptic`。运行`sudo apt-get update`以确保获取当前版本，然后`sudo apt-get install synaptic`。

### 6 运行 Synaptic

安装`Synaptic`后，你可以轻松访问发行版仓库中的所有软件。大多数目标都被精简，以节省下载并加快安装，但你可以从这里安装任何想要的东西。可以使用‘搜索’按钮或直接浏览类别查看可用内容。

## 恢复磁盘

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_58_0.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_58_1.png)

### 1 备份到 USB

插入容量至少为`2GB`的`USB`闪存盘或`SD`卡，打开`Chrome`并在地址栏中输入`chrome://imageburner`。`Chrome OS`会为您的`Chromebook`下载并安装恢复镜像。如果您拥有多个型号的`Chromebook`，请分别对每个型号执行此操作；它会获取该设备的正确镜像。

### 2 创建恢复磁盘

下载完成后，镜像会被写入您的`USB`闪存盘。如果您不创建恢复磁盘，也可以通过另一台计算机获取此镜像并手动复制，按照`http://google.com/chromeos/recovery`处的说明操作，但您必须确保获取正确的镜像——它们特定于每个型号。

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_58_2.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_58_3.png)

### 3 紧急情况下

如果您损坏了`Chrome OS`并收到以下令人害怕的“`Chrome OS`缺失或损坏”消息，请插入您的恢复介质。您也可以强制恢复，如果您仍想继续恢复，可以通过按下硬重置按钮或键组合来实现，具体取决于型号。查看您的`Chromebook`文档，了解适用的说明。

## Crouton：利与弊

将`200`英镑的`Chromebook`与全尺寸笔记本电脑相比似乎不公平——它更处于上网本的价格范围，目标市场也类似——但我们还是要这么做。在`Chromebook`上运行`Ubuntu`或`Debian`就像在真正的笔记本电脑上运行一样。唯一的区别在于使用了`chroot`。

这意味着您必须先启动到`Chrome OS`，然后打开一个`shell`来启动`chroot`会话，但`Chromebook`设计为暂停而不是关机，因此这并不一定经常发生。因为它通过`Chrome OS`使用硬件，您需要在其中执行诸如设置网络连接之类的操作，但由于您可以随时在操作系统之间切换，因此这不是问题。这不是双启动；它是同时运行两个系统——方便得多。此设置的主要限制是存储空间不足以及对网络连接和云服务的依赖。虽然`Chrome OS`透明地处理了这一点，但您需要从`chroot`发行版设置某种在线同步，使用`OwnCloud`、`Spideroak`或`Dropbox`等服务。在`Chromebook`上安装`Linux`的方法还有其他方式，但`Crouton`的方式侵入性最小，保持现有操作系统不变（除了需要启用开发者模式）。尝试多种选项，并在完成后将其移除，也是这种方法的一个关键优势。其优势之一是`Crouton`由`Chrome OS`作者开发，而不是第三方黑客工具。`Chrome OS`的未来更新可能会暂时破坏您的`chroot`，但通过`Crouton`进行更新会修复它。

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_58_4.png)

## 自建 Steam Machine

爆炸性的`AAA`游戏已登陆`Linux`，可用游戏超过`1,000`款。打造自己的专用游戏主机从未如此简单。

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_59_0.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_59_1.png)

过去`Linux`上的游戏一直饱受困扰，通常是因为许多开发者仓促推出`Linux`支持——或完全不提供——而专注于`Windows`。残酷的事实是，`Microsoft`的操作系统存在于绝大多数游戏`PC`上（例如`Steam`的硬件调查（`2015`年`2`月）显示`Windows`用户占超过`1.25`亿活跃客户的`95.68%`），即使该公司留下了一连串的未兑现承诺，以及更加破碎的在线基础设施和`DRM`——试着向`PC`游戏玩家提到`Games for Windows Live`，看看他们是否会明显颤抖。
