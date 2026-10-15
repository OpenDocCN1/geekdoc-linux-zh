
### 故障排查

执行`/config`命令时遇到以下错误：

```
/config: cd: can't cd to k-crossword

Cannot find file: k-crossword
```

尽管`k-crossword.gz`文件确实位于文件夹中，但系统报告找不到该文件。“k-crossword not found”这条消息的具体含义是什么？

Valerie 对此错误信息感到困惑，希望获得更合理的解释。

![](img/dc2302183c6b3ebee0d18a3807d4d058_88_0.png)

## VirtualBox

**磁盘工具与 GParted 的使用建议**

上述磁盘（Disks）工具确实可以完成分区任务，尽管我们更倾向于使用`GParted`。

强烈建议更新发行版，以防止系统发生意外。这样你就不需要为了服务器运行而担心报告问题了。

**磁盘空间与数据擦除**

磁盘工具完全可以设置高达 2 GB 的空间。你正在处理的数据删除问题可能是因为：

你正尝试将 2 GB 放在任何位置的开头，但这会让擦除速度更快也更危险。

另一种可能性是某些东西正在改变你删除的内容。如果你有 4 GB 或接近 GB 的空间，这是很有可能的。但最好的办法是在删除任何内容之前传输任何数据。

## Live mail

**分区操作**

没有。我成功地使用 Ubuntu 的磁盘（Disks）工具对一个较大的驱动器进行了分区，那是我完成的一个奇迹。我现在不想丢失另一个分区，我只是看了看磁盘工具，被引导去正规地完成我的工作了。

我想创建一个 16 GB 的磁盘文件并设置 2 GB，这样我就可以把 1 GB 的数据复制粘贴到驱动器上来增加它。我只需要那个 GB 吗？

**教程搜索**

那太简单了！用户朋友，我不确定这整件事。在此之前，我搜索了教程，但没有找到任何不是过时的教程（如果你有好的教程，请留下链接）。有些`GParted`的教程列表看起来很复杂。

你不必害怕！在“点击”磁盘之前，设置一系列更改非常简单，你可以运行任何你想要的想法。

**内核与 VirtualBox**

我真的需要一点帮助。每当我用新内核破坏我的发行版时，我不得不推荐 VirtualBox 内核。我这样做是安全的，且和之前的一源一样：

Jim Alexander

| 关于程序 | 翻译 | 许可证 |
|---|---|---|
| K-crossword 1.2.3(2021) | | |

**编译问题解决方案**

这个问题有两个可能的解决方案。第一种可能是你没有正确下载大小。由于构建问题，找不到`cd`命令。所以请重新保存，并命名为明天的某个名字。

为你的系统下载`K-crossword-1.2.3-tar.gz`。

```
$ tar xvf k-crossword-1.2.3-tar.gz

$ cd k-crossword-1.2-src/

$ ./config

$ cd /games/

$ cd /k-crossword-1.2.3
```

最后你将找到`k-crossword` GUI。如果你有问题，请获取基础构建要求，即`Qt4`和`QtWebKit`的开发包。

## 问题与解答

联系我们...
网页：`www.linuxuser.co.uk`
邮件：`linuxuser@imagine-publishing.co.uk`

## 资产到 IP

我在 CentOS 64 位操作系统上设置了 OCS 清单服务器 2.1。所有细节都正确地到了我的 OCS 服务器，除了客户端的 IP 地址。

客户端库的清单运行在`ocs-inventory-2.7.1`。以下是我的配置文件（客户端侧）`ocs-inventory.cfg`；

```
# 服务器 URL，如果需要请取消注释

server=http://<SERVER_IP>:8080/ocs-inventory

base=/ocs/

logger=/usr/bin/ocs-inventory
```

```
# 如何记录，可以是 File,Stderr, Syslog 或 none

logger=stderr

logfile=/var/log/ocs-inventory/ocs-inventory.log
```

我目前正在监控这些。当我执行`/usr/bin/ocs-inventory-client`时，服务器给我的 IP 地址是正确的。但过了一段时间，当它们发送清单时，客户端的 IP 地址就会从服务器上消失。直到我手动执行`/usr/bin/ocs-inventory-command`，它们才会再次出现。

我设置了一个每六小时运行一次的 cron 任务来向服务器发送清单。当 cron 在那时运行时，IP 地址显示为空，但我可以看到清单确实不在那里。

请就这个问题指导我，因为我已经尝试了所有方法，但未能找到问题所在。

Tukasa

**解决方案**

这实际上是 Linux 的问题而不是 OCS 的：cron 任务不知道路径配置。解决方案是以如下方式输入 cron 任务：

```
* * * * * /etc/usr/local/bin/ocs-inventory-agent >/dev/null 2>&1
```

你可以通过从命令行运行`ocs-inventory-agent --local=/`然后从 cron 运行来检查这一点。具有正确路径的 cron 可以工作；而（没有路径的）cron 任务你会得到一个`<NETWORK>`部分。

## Q & A

```
$ make clean

$ make DESTDIR=/build html
```

它完全崩溃了，而且无法安装。是因为我正在使用 Linux 作为内核源吗？有没有人能帮我解决这个问题？

所以，是的，这就是导致当你告诉 VirtualBox 重启操作系统时，它完全停止虚拟机的原因。这有点烦人，但没有像你正在经历的那么糟糕。

有两个选项。首先，VirtualBox 有一种所谓的自修复方法，将设置新模块并使用它们。

```
$ sudo /etc/init.d/modules setup
```
