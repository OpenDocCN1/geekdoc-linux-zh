
# 系统管理员与 DevOps 的 Linux 指南

## 免责声明

本文中的信息基于公开文档以及作者的个人及专业经验。在任何情况下，作者对因使用或无法使用本文而引起的任何直接、间接、后果性、惩罚性、特殊或偶然性的损害（包括但不限于利润损失、业务中断或信息丢失造成的损害）均不承担责任，即使作者已被告知可能发生此类损害。作者对本文文档内容的准确性或完整性不作任何陈述或保证，并保留在任何时间无需通知更改本文的权利。作者不承诺更新本文中所包含的信息。

对于德国人 `Manon Niazi`，我仍然喜欢大学时代，就就像发生在昨天一样。

献给我的母亲和家人。

献给我已故父亲的灵魂。

感谢每个人。

## 引言

本书献给 `LINUX` 工程师、系统管理员和 `DevOps` 人员，他们可以在工作中的大多数日常任务中使用此书中所示的材料。

它可以让你从一个基础初级 `LINUX` 相关工程师，或一个没有 `LINUX` 环境经验的工程师，转变为经验丰富的高级 `LINUX` 专业人士。

![](img/Image960.jpg)

## 1 Linux 桌面、服务器与云镜像

### 1.1 什么是 Linux？

`LINUX` 是由 `LINUS TORVALDS` 在自由开源软件开发和分发模式下开发的社区开源操作系统。

`LINUX` 最初是为 `Intel® x86` 架构开发的。

`LINUX` 操作系统原本用于大型机和大型服务器系统，但现在运行在桌面电脑、平板电脑和智能手机上。

`Linux` 发行版基于以下 6 个发行版：

1. 基于 `Debian` 的
2. 基于 `Gentoo` 的
3. 基于 `Pacman` 的
4. 基于 `RPM` 的
5. 基于 `Slackware` 的
6. 独立的

书中大部分内容取决于 `LINUX DEBIAN UBUNTU`，且以编写本书时的版本为 15.04。

诚实地说，我选择这个发行版是因为它是所有 `Linux` 操作系统发行版中支持最好、最流行的发行版和变体，并在 `Linux` 家族中排名第一。

### 1.2 Linux GUI 与桌面电脑

如果你正在将 `LINUX` 与其他操作系统进行比较，是的，它拥有图形用户界面（`GUI`），因此非专业的计算机科学家和工程师可以轻松使用，是的，普通的非计算机专业终端用户也可以使用。

你可以在不同的桌面之间切换，浏览文件夹，共享文件，并在每天上面进行大部分基础的日常常规操作。

你可以操作文件夹、文件，创建镜像，浏览互联网等。

你还可以创建计算机网络，共享打印机和文件，你可以创建打印服务器，进行文字处理，并且你可以随心意愿地操作机器来完成工作日期间的任何任务，甚至在家里或手机上也可以。它现在可以管理你的电话，你还可以在平板电脑上创建并发送电子邮件、浏览互联网等……

![](img/Image967.jpg)

### 1.3 Linux 服务器与集群

`LINUX` 服务器是旨在为其他类型的计算机和设备（如桌面电脑、平板电脑和手机）提供机器。

它还可以管理你的存储设备、网络设备以及任何能够连接到计算机基础设施的机器。

本书学习的重点是构建服务器-客户端基础设施，以及包含桌面、平板、手机和服务器机器的 `LINUX` 环境管理。

![](img/Image976.jpg)

`LINUX` 服务器发行版配备终端屏幕作为用户界面，出于安全和性能考虑，通常不包含任何图形用户界面。

我们将在第六章“自定义 `LINUX` shell”中讨论什么是终端屏幕，你将获得更多关于 shell 环境和基础 shell 命令的信息。

你可以观察周围的环境，以注意服务器具备的能力，以及服务器能为你和你的环境做什么。

例如，如果你查看邮件服务，比如你公司的邮件服务，或者在互联网上提供免费邮件服务或营利邮件服务的免费服务提供商。

邮件服务器用于保存你发送、接收以及部分撰写并保存的所有邮件消息，这些消息存储在专门分配给邮件消息、附件、草稿等的大型存储介质上，并通过用户账户验证和授权以及安全机制，专门为每个使用用户的隐私而设计。

另一个服务器-客户端环境的例子是当你在任何云存储提供商在使用驱动器账户，或者在公司环境中使用映射的网络驱动器时，这简单就是在服务器机器上安装了 `FTP`、`SFTP` 协议的存储服务器，并映射到工作机器的网络驱动器。

示例服务器-客户端环境基础设施可以在图 1.1 所示。

![](img/Image984.jpg)

**图 1.1** 显示了示例网络基础设施环境

该基础设施包含普通 `PC` 电脑、笔记本电脑、平板电脑、手机、打印机、扫描仪、`ISP` 无线设备、调制器、存储路由器软件、存储磁带、集群、工作站等。

此基础设施中的客户端由 `PC`、笔记本电脑、扫描仪、打印机和平板设备代表，而服务器由集群、存储路由器、磁带和工作站代表。

还有在设备之间传输数据的网络介质，例如中间的无线设备和底部的调制器设备。

### 1.4 Linux 云镜像与虚拟机

`Linux` 云镜像是 `Linux` 发行版的精简版本，具有针对云环境优化的最小配置和功能。

`Linux` 云镜像的精简是为了性能和磁盘占用，这也允许用户去掉不符合其预期构建环境的空闲功能，例如，如果用户正在构建 `Web` 服务器环境，用户只需安装 `Web` 服务器环境的功能，而不需要所有其他 `Linux` 功能。

`Linux` 云镜像具有终端用户界面，其中不包含任何图形用户界面。

`Linux` 云镜像基于我们之前在“Linux 桌面？”节中提到的相同发行变体。

云镜像用于部署到虚拟机中，你也可以在虚拟机上部署完整的 `Linux` 镜像。

你可以将云镜像部署到 `OpenStack` 和 `AWS`（亚马逊云服务）`EC2`（弹性计算）或其他云提供商的云操作系统。

云镜像根据你使用的硬件处理器可以是 32 位和 64 位架构，你可以为该硬件处理器的虚拟机上安装相应的云镜像。

例如，云镜像可以从以下 `URL` 下载：

`https://cloud-images.ubuntu.com/`

`https://aws.amazon.com/marketplace/ref=mkt_ste_amis_redirect?b_k=291`

这些链接不是永久的，如果你在这些链接中发现变化，可以在互联网上搜索云镜像来下载任何这些镜像。

我们将在后的“Linux 虚拟机”主题中讨论虚拟机。

如之前在名为“什么是 LINUX?”的一个主题中提到的，我们可以知道 `LINUX` 发行版并没有不同的架构或性能差异，但它们在执行各种安装的发行版命令上有所不同，例如：

`UBUNTU®`：我们使用以下命令来更新操作系统：

```bash
sudo apt-get update
```

`FEDORA®`：我们使用以下命令来更新操作系统：

```bash
sudo yum install update
```

在其他发行版中，这些命令可能与上述有所不同，但所有这些命令执行的都是系统更新。

在不同发行版上安装的包名（程序名称）也可能不同，例如：

在 `Fedora` 上安装 `MySQL` 数据库服务器可能与在 `UBUNTU®` 上不同，如下：

`UBUNTU®`：我们使用以下命令安装 `MySQL` 服务器：

```bash
sudo apt-get install mysql-server
```

`FEDORA®`：我们使用以下命令安装 `MySQL` 服务器：

```bash
sudo yum install mysql-community-server
```

因此，包名从 `UBUNTU®` 仓库更改了 `FEDORA®` 仓库，从 `UBUNTU®` 的 `mysql-server` 变为 `FEDORA®` 的 `mysql-community-server`。

最后，你需要根据你正在工作的发行版来调整你的命令。

如果你正在安装一个包（程序），你需要知道你正在工作或执行此命令的发行版的确切包名；或者如果你正在执行操作系统优化命令，你也需要知道每个发行版上的每个命令，并执行适用于该发行版的命令。

### 1.6 自定义 Linux Shell

某些用户在执行任务时需要自定义 `LINUX` shell。

`LINUX` 终端或 shell 窗口如图 1.2 所示

![](img/Image991.jpg)

我们可以在此终端窗口中执行命令，正如你所看到的，它非常像一个用于输入安装和系统操作命令的简单文本编辑器。

此窗口可以根据用户需求进行自定义，例如更改背景颜色文本颜色。

此窗口还可以通过使用 `sudo` 关键字以管理员权限运行命令，或者通过使用命令 `sudo -s` 到当前工作会话的超级用户，这将你转移到 `root` 用户的 `sudo` 权限，你会发现你正在使用 `root@youroscomputername`。

![](img/Image999.jpg)

**图 1.3** 显示了如何在 `UBUNTU` 发行版上执行此命令。

通过这种方式，你可以使用权力用户（`sudoer`）、管理员或 `root` 用户执行所有命令。

### 1.7 基础 Linux 命令

```bash
sudo apt-get update --fix-missing && sudo apt-get upgrade --fix-missing && sudo apt-get dist-upgrade –fix-missing
```

你将在图 1.4 中看到此命令的输出

![](img/Image1008.jpg)

**图 1.4** 显示了 `UBUNTU LINUX` 发行的更新和升级过程。

此命令用于通过来自你使用发行版所在国家的 `LINUX` 仓库完全更新你的 `LINUX` 发行版。

**注意，我们使用 `--fix-missing` 键在发生任何故障时切换到替代包，如果可能，你也可以在其他命令中使用此键。**

如果你想使用主服务器仓库而不是特定国家的仓库，请运行以下命令：

```bash
sudo nano /etc/apt/sources.list
```

该命令的输出将如图 1.5 所示

![](img/Image1015.jpg)

你需要使用键盘上的方向键上下移动，到达你想编辑的行。

找到我文件中每行中的所有国家区域，在这里每行中都是 `eg.` 并将其完全删除。例如将 `deb [http://eg.archive.ubuntu.com/ubuntu/] vivid-updates main restricted` 改为 `dev htp://archive.ubuntu.com/ubuntu/ vivid-updates main restricted` 即可继续。

在对文件执行这些更改后，按下键盘上的 `CTRL+X` 关闭文件。注意它会提示你保存文件并选择文件名。你只需在键盘上按 `Y` 并按回车即可保存到相同的文件名和相同的目录。

继续你的 `LINUX` 环境的基础命令，我们还可以了解其他在日常系统管理任务非常有用的命令。

要获取你 `LINUX` 发行版上所有运行的程序和进程，请在终端窗口输入以下命令：

```bash
ps aux | less
```

该命令的输出将如图 1.6 所示：

![](img/Image1023.jpg)

你可以通过按键盘上的 `ENTER` 键每行进入下一行，然后可以使用 `CTRL + Z` 退出此命令输出屏幕并返回终端原始提示符。

另一个最受欢迎的命令之一是如何创建一个 `SWAP` 文件，用于增强计算机性能，`LINUX` 将其用作 `RAM`，如下：

```bash
sudo dd if=/dev/zero of=/swapfile bs=1G count=4
```

此命令将在你 `LINUX` 发行版的根目录下创建一个 `SWAP` 文件，该文件将包含 4 个部分 `[count=4]` 并被分为 4 个分区，每个分区为 1 G 字节 `[bs=1G]`。

该命令的输出如图 1.7 所示。

![](img/Image1031.jpg)

通过这种方式，你创建了 `SWAP` 文件，下一步是使用它并让它对你的 `LINUX` 发行版可用：

通过使用命令显示显示的创建的输出：

```bash
sudo chmod 600 /swapfile
```

此命令没有任何输出，它将显示提示符。

你需要使用以下命令调整我们创建的文件的权限和所有权，使其仅对授权用户可用：

```bash
sudo mkswapfile
```

此命令没有任何输出，它将你返回提示符。

最后我们使用此命令启用 `SWAP` 文件：

```bash
sudo swapon /swapfile
```

此命令的输出如图 1.8 所示，确认命令执行成功。

但我们可以通过此命令确认文件已成功分配：

![](img/Image1048.jpg)

现在命令输出确认文件已成功创建并按要求工作。

继续我们的基础命令部分，我们仍然可以执行对日常管理员任务非常有用的终端任务：

在 `LINUX` 机器上管理服务，以及在列出所有进程后识别你需要杀掉的哪个进程，将在接后的章节中介绍。

通过运行此命令，你将能够识别 `LINUX` 机器上运行的所有进程，并如下使用进程识别每个进程：

```bash
sudo swapon -s
```

通过运行此命令，你将获得一个带有进程 ID `PID` 的进程列表，图 1.9 显示了此命令的输出

通过 `PID` 识别进程后，你可以使用以下命令终止此进程：

```bash
sudo kill -9 PID
```

![](img/Image1055.jpg)

如图 1.10 所示，你需要将 `PID` 替换为你想要停止的进程 ID，在我的案例中，我使用 `PID` `14846` 停止了 `mysqld`。

![](img/Image1062.jpg)

最后你可以使用以下命令启动、停止和重启任何你服务：

```bash
sudo service apache2 start

sudo service apache2 stop

sudo service apache2 restart
```

此命令不会产生任何输出或表示成功的文本，但如果发生失败，你将收到一个通知，根据你正在管理的特定服务，该通知将指示失败及其原因。

在我的情况下，我的发行版中安装了 `apache2`，并且我通过这三个命令对它进行了启动、停止和重启。

接下来的部分将包含关于如何操作 `LINUX` shell 的有用链接。

[`help.ubuntu.com/community/UsingTheTerminal`](https://help.ubuntu.com/community/UsingTheTerminal)

[`www.fedorafaq.org/basics/`](http://www.fedorafaq.org/basics/)

### 1.8 Shell 编程基础

`Shell` 编程是一种专门为 `LINUX` 机器指定的编程语言，用于执行与你的 `LINUX` 操作系统环境相关的特定任务。

在本节中，我们需要熟悉编程以及如何使用 `LINUX` shell 来编写一个包含终端要执行某些任务的 shell 脚本。

让我们从了解什么是编程开始：

编程是一一组指令、控制和结构语句，目的是让机器能够理解并执行。它必须遵循标准的语法格式以便机器能够理解。它必须按顺序一个接一个地执行，你必须检查哪个语句应该第一个、第二个、第三个执行，以便计算机完成你需要它完成的任务。

首先，我们需要识别什么是 shell 脚本文件以及我们如何创建这样的文件，然后我们将执行特定任务的命令列入此文件中，然后按照如下所示在终端窗口中运行此文件：

1. `touch helloworld.sh`
2. `nano helloworld.sh`
3. `echo “Hello World"`
4. 按 `CTRL + X`，然后输入 `y` 然后按下键盘上的回车键。
5. `sh helloworld.sh`

这将在你的终端窗口屏幕上输出 `Hello World`。

我们现在所做的是一种 shell 脚本文件，其中包含一个命令，告诉计算机输出 `Hello World` 句子。

- 首先，我们使用命令 `touch helloworld.sh` 创建了一个名为 `helloworld.sh` 的文件。
- 第二，我们使用名为 `nano` 的程序通过命令 `nano helloworld.sh` 编辑了该文件。
- 第三，我们在文件中添加了一行，通过终端中的 `echo` 命令使用命令 `echo “Hello World"` 告诉计算机向屏幕输出 `Hello World` 句子。
- 第四，我们使用键盘上的 `CTRL + X` 保存文件，并通过输入 `Y` 确认，然后按回车使用相同的文件名和目录。
- 最后，我们使用 `sh` 命令指向我们在前面的步骤中创建的文件名使用命令 `sh helloworld.sh` 执行了此脚本，输出如图 1.11 所示：

![](img/Image1070.jpg)

通过这种方式，你创建一个 shell 脚本文件，在其中输入了一个命令并执行了该命令。你可以在执行 `nano` 命令并开始编辑 shell 脚本文件后，在该文件中列出一系列相邻的命令来执行之前的步骤。

让我们创建一个带条件迭代的循环：

循环用于在满足条件时让计算机执行某任务或一组任务，并在不满足条件时停止，如下：

1. `touch iterationofdays.sh`
2. `nano iterationofdays.sh`
3. `i=1`
4. `weekdays=”Mon Tue Wed Thu Fri"`
5. `for day in $weekdays`
6. `do`
7. `echo “Weekday $day"`
8. `done`
9. 在键盘上按 `CTRL + X`，随后按 `Y`，然后按回车退出。
10. `sh iterationofdays.sh`

在这个示例中，我们执行了一系列命令，将在下面的点中说明：

第一：我们像上一个示例一样使用 `touch` 命令创建了 shell 脚本文件。

第二：我们使用 `nano` 编辑器编辑了文件。

第三：我们插入了名为 `i` 的变量并赋予它默认值 `1`。

第四：我们创建了一个名为 `weekdays` 的列表，并添加了用空格分隔的星期值，并用双引号括起来。

第五：我们启动了一个 `for` 语句来处理迭代，该迭代将受 1 个条件的限制，循环到我们在第四步中创建的列表结束。

第六：我们使用 `do` 命令开始指示计算机只要第五步中的 `for` 语句在循环，它就执行某些操作。

第七：我们给计算机了一些指令，通过我们给它的命令在屏幕上输出星期几名称。



第八：我们使用`done`关键字结束了我们给计算机执行的命令。

第九：我们关闭并保存了第一步中创建的 shell 脚本文件。

第十：我们使用命令`sh iterationofdays.sh`执行了该文件。

![](img/Image1078.jpg)

**图 1.12** 显示了我们创建的脚本输出以及我们在上述的操作。

现在我们需要更多地了解我们在创建的文件中添加的内容：

变量是内存中一个可以保存数据的地方，之所以称为变量，是因为我们可以将其中存储的数据更改为我们想要的任何值。我们使用`$`符号来调用我们创建的变量，并将其用于脚本中任何语句中。

## 1.9 安装命令和包配置

安装命令可能根据你想要安装的目标程序或包而变化。可以使用以下命令示例来安装不同的包：

`sudo apt-get install apache2`

此命令将会在你的机器上安装`apache2`服务器。

`sudo java -jar`

此命令将为你安装 jar 类型文件。

`sudo sh netbeans.sh`

此命令将会在你的终端上安装 shell 类型文件。这些命令也根据你安装文件的位置而变化，示例如下：

`sudo sh /home/username/Downloads/netbeans.sh`

在这种你从互联网下载了文件到机器上，且文件现在位于：

`/home/username/Downloads/filename.sh`

在 Linux 终端可以使用一些快捷方法，例如：如果你想直接访问 LINUX 机器上的默认目录，只需输入`~/Downloads/filename.sh`。通过这种方式你通过使用`~/`消除了`/home/username/`。另一个快捷示例是使用`~/Desktop/filename.sh`访问位于桌面目录的文件。

```bash
ls -l /path/to/directory/
```

显示此命令如何工作及其输出的示例将在下一图 1.13 中。

还有一点需要注意，当你执行`java -jar`文件安装或执行时，你首先需要在机器上安装 java sdk，可以通过以下命令完成：

`sudo apt-get install openjdk-8-jre`

如果你想要 Oracle 版本的 java，可以使用以下命令进行安装：

`sudo add-apt-repository ppa:webd8team/java -y`

`sudo apt-get update`

`sudo apt-get install oracle-java8-installer`

在安装这些命令时要非常小心，并在执行安装步骤之前检查要安装的内容。

## 1.10 操作仓库

在 UBUNTU 终端操作仓库是简单且可配置的。你可以添加仓库、管理仓库并在你的安装和系统更新这些仓库。

仓库是组合在一起的安装和更新文件的集合，带有一个唯一的 URL，可以通过一个名为`sources.list`的文件绑定到你的系统，该文件可以使用普通的文本编辑器编辑，也可以通过终端进行修改。

首先让我们使用此命令向我们的`sources.list`文件添加仓库：

`sudo add-apt-repository ppa:webd8team/java -y`

此命令的输出如图 1.14 所示。

![](img/Image1093.jpg)

此命令已向`sources.list`文件添加了 java 安装存储库，以便操作系统能够识别我们想要安装的`java-sdk`程序的包名。

我们可以使用以下命令编辑`sources.list`文件：

```bash
nano /etc/apt/sources.list
```

该命令将列出存储库列表，操作系统会在这些列表中查找包名，并识别下载和更新这些包的位置。

你可以在文件中进行编辑、添加、更新或删除任何你需要的记录，但在处理此文件时要务非常小心，因为它包含了许多关于操作系统包更新和升级的敏感数据。

## 1.11 更新、升级和发行版升级

更新你的机器并不是一项困难的任务，除非你在上面安装了太多的程序和软件包，因为`LINUX`会尝试更新除了操作系统初始安装时已包含的系统包之外的你所安装的所有包。

你可以使用以下命令更新系统：

```bash
sudo apt-get udpate
```

该命令的输出是之前在`Basic LINUX Commands`章节`#Image7|graphic`中所示输出的一部分。

你可以使用此命令升级你的`LINUX`系统：

```bash
sudo apt-get upgrade
```

该命令的输出也是之前在`Basic LINUX Commands`章节`#Image7|graphic`中所示输出的一部分。

你可以使用此命令升级你的`LINUX`发行版（仅限）：

```bash
sudo apt-get dist-upgrade
```

该命令的输出也是之前在`Basic LINUX Commands`章节`#Image7|graphic`中所示输出的一部分。

在执行更新、升级和`dist-upgrade`时，如果使用`--fix-missing`键，你可能会遇到损坏的链接或其他更新问题。

基本上，这里是`LINUX`桌面服务器部分 1 的结束，包含了`LINUX`机器运行的通用概念。让我们移动到第 2 部分。

# Linux 基础架构

## 2.1 安装 DNS 和 DHCP

让我们通过`BIND9`的安装。在`UBUNTU`上使用以下命令安装`BIND9`：

```bash
sudo apt-get install bind9
```

运行此命令将输出如图 2.1 所示确认：

![](img/Image1093.jpg)

当你按下`Y`并按回车键时，安装将继续，直到完成`bind`配置并运行。

配置`bind9`我们运行以下命令：

```bash
sudo nano /etc/bind/named.conf.options
```

编辑此文件时，找到包含`forwarders`的行：

```text
forwarders {
0.0.0.0;
}
```

将括号之间的数字更改为你的 IP 地址。在这种情况下，我的 IP 地址是`192.168.0.2`。

因此`forwarders`部分变为：

```text
forwarders {
192.168.0.2;
}
```

现在，你需要输入以下命令编辑另一个名为`named.conf.local`的文件：

```bash
sudo nano /etc/bind/named.conf.local
```

然后你需要做的是添加以下条目或更改当前条目：

```text
zone “manon.com” {
  type master;
  file “/etc/bind/db.manon.com”;
};

zone “0.168.192.in-addr.arpa” {
  type master;
  file “/etc/bind/db.192”;
};
```

按下`CTRL + W`退出，使用`Y`确认，然后按回车键。

现在，你需要执行以下命令使用`cp`关键字从原始位置创建一个适用于此配置的文件：

```bash
sudo cp /etc/bind/db.local /etc/bind/db.192
```

复制的文件位于`/etc/bind/db.local`并复制到了`/etc/bind/db.192`。

复制文件后，你应该使用以下命令编辑复制后的文件：

```bash
sudo nano /etc/bind/db.192
```

之后你将看到文件内容，编辑文件内容使其符合你的需求如下：

```text
;
; BIND reverse data file for local loopback interface
;
```

![](img/Linux_for_system_3.jpg)

你会发现需要编辑的区域，你可以根据需要对其自定义，并注意最后一行开头的数字`2`将是你的 IP 地址的最后一个字节。

当你完成后，需要使用此命令开始复制另一个文件：

```bash
sudo cp /etc/bind/db.local /etc/bind/db.manon.com
```

此命令将文件从`/etc/bind/db.local`复制到目标`/etc/bind/db.manon.com`。

不要忘记将目标文件`db.manon.com`更改为你想要的服务器字符串主机名。

完成后，我们需要编辑`db.manon.com`文件并其内容如下：

```bash
sudo nano /etc/bind/db.manon.com
```

然后你需要将文件内容更改如下：

```text
manon.com
```

![](img/Linux_for_system_4)

`192.168.0.2`

`192.168.0.0`

`1`

我们还需要做的另一件事是编辑`/etc/default/bind9`的内容：

```bash
sudo nano /etc/default/bind9
```

现在，你需要在`/etc/default/bind9`中搜索：

```text
RESOLVCONF=yes
```

通过这种方式，你需要使用`CTRL + X`退出编辑器并使用`Y`确认文件，然后按回车返回终端。

我们需要重启名为`bind9`的服务：

```bash
sudo service bind9
```

重启服务后，请运行此命令检查你的服务器是否响应并运行：

```bash
sudo dig 192.168.0.2
```

如果你收到了如附 2.2 所示的响应：

![](img/Image1110.jpg)

那么你成功安装了 DNS。

但如果你没有看到此消息，请检查关于你的`LINUX`机器的故障排除章节。在执行之前的步骤之前，请确保你查看了附录 B。

我们的下一步是在`LINUX`机器上安装 DHCP：

```bash
sudo apt-get install isc-dhcp-server
```

这意味着什么？如果任何计算机要像书中图`#Image4|graphic`所示的加入该域（该图包含了已连接的计算机、打印机、平板电脑等基础设施示例），这些设备中的每台设备都将在你在 DHCP 服务器中指定的范围内获得一个 IP 地址。

除了之前的安装之外，还有一件事是使用以下命令重启 DHCP 服务器：

```bash
sudo service isc-dhcp-server restart
```

通过这样，我们就完成了在`UBUNTU`上对 DHCP 服务器的安装。

接下来的图 2.4 显示了我们做的 2 次安装，以及它们与你正在构建的网络设施的关系：

![](img/Image1132.jpg)

我们在此处的`LINUX`发行版将安装在数据中心 RAC 的集群控制器机器上。我们的 DHCP 服务器将安装在这台机器上，它的功能是将 IP 地址分发到连接到`BUS`拓扑结构的 PC、大塔式 PC 和打印机上。

如果你仔细观察数据中心 RAC，`SAN ISCSI`存储磁盘在后续章节中安装文件服务器时，也可以由集群节点节点管理。

在你的`LINUX`机器上安装 Kerberos 将是下一步。Kerberos 是一个处理`LDAP`的服务器，这是一个轻量级目录访问协议。要在你的机器上安装 Kerberos，我们将执行此命令：

```bash
sudo apt-get install krb5-kdc-ldap
```

你将会被提示输入`REALM`名称，例如，如果你在 DNS 安装步骤中将 DNS 名称设为`manon.com`，那么域名称将是大写的`MANON.COM`。

之后，你将被提示输入你的域的 Kerberos 服务器和管理服务器，如下：

Kerberos 服务器：`KRB.MANON.COM`

管理服务器：`ADMIN.MANON.COM`

![](img/Image1139.jpg)

**图 2.5** 显示了 Kerberos 包的安装过程。

在之前的安装之后，我们需要使用以下命令安装`LDAP`工具，它将作为我们稍后在此安装安装的`PHP`前端的后端：

```bash
sudo apt-get install slapd ldap-utils
```

这包含 2 个要安装的包：`slapd`和`ldap-utils`。当你完成此安装后，我们需要使用以下命令重新配置包`slapd`：

```bash
sudo dpkg-reconfigure slapd
```

运行此命令后，你将看到以下内容：

- 当提示要跳过`ldap`服务器配置时：选择`no`。
- 请输入 DNS 域名：在我的情况下为：`manon.com`。
- 当涉及到管理员密码时，请输入你在之前的安装步骤中使用的密码。
- 当涉及到要使用的数据库类型时：选择`HDB`。
- 当在清除`slapd`时删除数据库时：选择`no`。
- 当涉及到移动旧数据库时：选择`yes`。
- 最后，当提示允许`ldapv2`协议时：选择`no`。

当你完成这些操作后，运行以下命令：

```bash
sudo apt-get install phpldapadmin
```

这将成为我们的`LDAP`服务器的前端，并将作为管理`LDAP`用户和组的用户界面。安装完成后，我们需要使用`nano`编辑以下文件：

```bash
sudo nano /etc/phpldapadmin/config.php
```

找到以下条目：

```php
$servers->setValue(‘server’,’host’,’manon.com’);
```

你需要根据你的环境更改的字段已用黄色标亮。你还需要找到这一行：

```php
$servers->setValue(‘server’,’base’,array(‘dc=manon,dc=com’));
```

同样需要更改的字段也用黄色标亮。最后一步是找到以下代码行并更改为以下值：

```php
$servers->setValue(‘login’,’bind_id’,’cn=admin,dc=manon,dc=com’);
```

需要编辑的字段已用黄色标亮。完成后，请打开浏览器并指向以下地址，并考虑根据你的环境规范进行更改：

[`manon.com/phpldapadmin/`](http://manon.com/phpldapadmin/)

![](img/Image1149.jpg)

**图 2.6** 显示了`PHP LDAP`管理前端。打开此屏幕后，你将看到用户名和密码，你需要按照如下方式输入用户名，并考虑环境中的更改：

`cn=admin,dc=manon,dc=com`

需要更改的字段已用黄色标亮。现在，我们已经在`DNS`上完全安装了`LDAP Kerberos`，剩下的是安全部分，我们将在**LINUX 安全安全**章节中应用它。

## 2.2 管理用户和组

### 添加新用户

如果你想添加一个新用户，请运行以下命令：

```bash
sudo adduser manon
```

你需要将`manon`单词更改为你环境中需要的用户名。它将提示你输入用户的详情并确认这些详情是否正确。

如果你想让此用户成为管理员并能够执行各种任务，请通过以下命令操作：

```bash
sudo visudo
```

你将在编辑器中找到我们之前通过`adduser`命令创建的用户，并修改如下：

```text
manon ALL=(ALL) ALL
```

如果你想删除该用户，可以使用以下命令：

```bash
sudo deluser manon
```

如果你想删除属于该用户的所有文件，可以使用以下命令：

```bash
sudo deluser --remove-home manon
```

再次执行相同的命令：

```bash
sudo visudo
```

然后将其注释掉使其失效：

```text
#manon ALL=(ALL) ALL
```

### 创建组

如果你想创建一个组，你需要执行此命令：

```bash
sudo addgroup manons
```

这样，你已经在你的`LINUX`机器上添加了一个新组。如果你想将用户加入此组，请执行以下命令：

```bash
sudo adduser manon manons
```

这样，我们将用户`manon`加入了`manons`组。如果你想更改用户访问或拒绝访问目录、文件等权限，你需要前往**安装和管理 FTP、SFTP**章节，我们将讨论文件服务器以及允许用户通信的协议。

## 2.3 安装和管理 Linux 防墙

防火墙是一种通过过滤输入输出来保护机器的方法，防止访问你不希望披露的敏感数据。要在`LINUX`上安装防火墙，需要在终端执行以下命令：

```bash
sudo apt-get install ufw
```

此命令可能会提示软件包已安装且为最新版本，因为它可能随操作系统默认安装。如果你完成了包的安装，我们需要通过发布以下命令启用它：

```bash
sudo ufw enable
```

要显示防火墙状态，你需要执行以下命令：

```bash
sudo ufw status verbose
```

![](img/Image1156.jpg)

你将看到一个类似于之前的 2.7 图的屏幕，显示上一个命令的结果。现在我们确保了防火墙已安装并运行。要在你的机器上开启端口号，我们将执行以下命令：

```bash
sudo ufw allow 53
```

此命令将允许流量通过端口`53`进出。在加固`LINUX`发行版、安装 Web 服务器以及安装`ssh`和文件服务器时，我们还将学习什么是端口，因为这些服务的每项安装都需要使用 1 个或多个端口号。

这些服务中的任何一个都可以通过允许或拒绝它被添加到我们正在使用的防火墙规则中。

![](img/Image1164.jpg)

要拒绝一个端口号，可以使用以下命令：

```bash
sudo ufw deny 53
```



这将拒绝端口 53，且上一个命令的结果与我们为启用相同端口而发布的命令完全相同。

如果你想通过特定协议允许或拒绝特定端口，需要执行以下命令：

```bash
sudo ufw allow 53/tcp
```

此命令将使端口 53 仅允许使用 TCP 协议。

如果你想禁用相同协议的相同端口，需要按照如下方式执行命令：

```bash
sudo ufw deny 53/tcp
```

还有一点，如果你想在任何端口上启用 UDP 协议，可以执行以下命令：

```bash
sudo ufw allow 53/udp
```

如果你想禁用任何端口的 UDP 协议，可以执行以下命令：

```bash
sudo ufw deny 53/udp
```

最后，如果我们想完全禁用防火墙，我们需要执行以下命令：

```bash
sudo ufw disable
```

现在，我们管理了我们的 LINUX 防火墙，并学习了启用、禁用和管理端口，以在特定端口上接受或拒绝特定协议，或者普遍接受或拒绝所有端口协议。

## 2.4 安装和管理 Web 服务器

Web 服务器用于在你的机器上托管网站。

如果你想安装最流行的 Web 服务器，那么就是 Apache，它可以服务 PHP、MySQL、Java 甚至 Python 页面。

Apache® Web 服务器在世界 Web 服务器统计排名中位第一，这就是为什么我们将重点关注在我们的 LINUX 机器上安装一个名为 LAMP 的服务器栈。

LAMP 的缩写代表 LINUX、Apache、MySQL 和 PHP。

要在你的 UBUNTU LINUX 机器上安装 LAMP 栈，我们将执行以下命令：

```bash
sudo apt-get install tasksel
```

当此执行完成后，我们需要执行如下命令来安装栈本身：

```bash
sudo tasksel install lamp-server
```

此命令将要求我们之前安装的 `tasksel` 安装 `lamp-server` 软件包。

系统将提示你输入密码并为你的 MySQL 数据库服务器确认。

之后，当你完成上一个命令的操作步骤后，我们将安装一个名为 PHPMyAdmin 的 GUI 来管理我们的数据库服务器。

PHPMyAdmin 是一个用于管理 MySQL 数据库、执行查询、管理用户等功能的强大工具。

要安装 PHPMyAdmin，我们需要执行如下命令：

```bash
sudo apt-get install phpmyadmin
```

执行该命令将引导你输入 MySQL 密码，请输入与你在上一个命令中安装 LAMP 服务器时相同的密码，你也可以为管理系统账户使用相同的密码。

你可以在被提示时选择 yes，允许 PHPMyAdmin 在 MySQL 服务器上创建它自己的数据库。

通过这种方式，我们安装了 LAMP 栈，以及一个我们可以在我们的 UBUNTU LINUX 机器上托管应用程序的 Web 服务器。

为了测试我们的安装，我们需要创建一个名为 `index.php` 的文件并将此文件放在以下目录：

`/var/www/html/`

要创建此文件，我们需要执行以下命令：

```bash
sudo nano /var/www/html/index.php
```

这将在终端窗口中打开一个文本编辑器以添加文本。

我们需要在文件中添加如下所示代码：

```php
<?php
echo phpinfo();
```

然后，我们需要按下 `CTRL + X` 关闭文件，通过输入“Y”然后按回车键来确认更改，以确认路径和文件名。

完成所有要求后，我们需要打开浏览器并将地址指向以下 URL：

`http://localhost/`

这将使你看到下面的图 2.9，它将包含你 PHP 安装的所有服务器配置设置。

![](img/Image1172.jpg)

如果你遇到任何问题，请查阅*附录 F* 排除你的 LINUX Web 服务器故障。

## 2.5 安装和管理邮件服务器

在安装我们的 DNS 之后，我们将按照以下步骤在 DNS 上集成我们的邮件服务器：

1. 我们需要在我们的 UBUNTU LINUX 系统上安装名为 `POSTFIX` 的软件包。  
   通过执行以下命令完成安装：
   ```bash
   sudo apt-get install postfix
   ```
   你可以简单接受默认，因为我们将重新配置该软件包。

2. 我们需要按照如下方式重新配置软件包以应用特定的环境数据：
   ```bash
   sudo dpkg-reconfigure postfix
   ```
   你将看到一系列屏幕，你需要应用如下设置：
   * Internet（互联网站点）。
   * 当前配置中没有请求。
   * 系统邮件名将是 `manon.com`，你需要将其更改为安装 DNS 时选择的域名。
   * `mostafa` #将其调整为你的用户名。
   * `manon.com, localhost, localhost.localdomain` #在安装 DNS 时将 `manon.com` 调整。
   * No。
   * `192.168.0.2` #将其调整为你的 IP 地址。
   * Yes
   * 0
   * +

   现在我们需要运行以下系列命令来继续配置过程：

   ```bash
   sudo postconf -e ‘home_mailbox = Maildir/’
   sudo postconf -e ‘mailbox_command =’
   sudo postconf -e ‘smtpd_sasl_local_domain =’
   sudo postconf -e ‘smtpd_sasl_auth_enable = yes’
   sudo postconf -e ‘smtpd_sasl_security_options = noanonymous’
   sudo postconf -e ‘broken_sasl_auth_clients = yes’
   sudo postconf -e ‘smtpd_recipient_restrictions = permit_sasl_authenticated,permit_mynetworks,reject_unauth_destination’
   sudo postconf -e ‘inet_interfaces = all’
   sudo apt-get install postfix-tls sasl2-bin libsasl2 libsasl2-modules
   sudo nano /etc/default/saslauthd
   ```

   或更改：
   * `START=yes`
   * `MECHANISMS="pam"`

   ```bash
   sudo nano /etc/postfix/sasl/smtpd.conf
   ```

   添加：
   * `pwcheck_method: saslauthd`

   ```bash
   sudo nano /etc/postfix/main.cf
   ```

   添加：
   * `smtpd_sasl_auth_enable = yes`
   * `smtpd_sasl_security_options = noanonymous`
   * `broken_sasl_auth_clients = yes`
   * `smtpd_recipient_restrictions = permit_sasl_authenticated,permit_mynetworks,reject_unauth_destination`
   * `inet_interfaces = all`（等待，原文有一些重叠/混乱的步骤，我将遵循提供文本的逻辑）。

   *基于提供文本的修正：*
   文本列出了：
   - `sudo nano /etc/default/saslauthd` -> 添加 `START=yes`, `MECHANISMS="pam"`
   - `sudo nano /etc/postfix/sasl/smtpd.conf` -> 添加 `pwcheck_method: saslauthd`
   - `sudo nano /etc/postfix/main.cf` -> 添加 `smtpd_sasl_auth_enable = yes`, `smtpd_sasl_security_options = noanonymous`, `broken_sasl_auth_clients = yes`, `smtpd_recipient_restrictions = permit_sasl_authenticated,permit_mynetworks,reject_unauth_destination`, `inet_interfaces = all`。

   ```bash
   sudo service postfix restart
   ```

接下来，我们需要安装以下软件包来完成我们 POSTFIX 邮件服务器的安全配置：

```bash
sudo apt-get install libsasl2-2 sasl2-bin libsasl2-modules
```

接下来，我们需要编辑文件 `/var/spool/postfix/var/run/saslauthd` 中的以下值：

```bash
sudo nano /var/spool/postfix/var/run/saslauthd
```

删除 `START=yes` 一行前面的哈希符号 `#`。

在我们刚才编辑过的上一行旁边，添加以下行内容：

```bash
PWDIR="/var/spool/postfix/var/run/saslauthd"
PARAMS="-m ${PWDIR}"
PIDFILE="${PWDIR}/saslauthd.pid"
```

之后，我们需要将文件末尾的 `OPTIONS` 行修改为：

```bash
OPTIONS="-c -m /var/spool/postfix/var/run/saslauthd"
```

接下来，我们需要执行以下命令：

```bash
sudo dpkg-statoverride --force --update --add root sasl 755 /var/spool/postfix/var/run/saslauthd
```

如果上一个命令产生警告或错误，请忽略错误，因为报告的目录将在后续步骤中自动创建。

接下来，我们需要执行以下命令：

```bash
sudo ln -s /etc/default/saslauthd /etc/saslauthd
```

最后，我们需要重启服务：

```bash
sudo service saslauthd restart
```

为了测试我们的安装，我们需要执行以下命令：

```bash
telnet localhost 25
```

或者

```bash
telnet manon.com 25 # 将 manon.com 替换为你自己的 DNS 字符串。
```

然后在连接建立后，执行以下命令：

```bash
ehlo localhost
```

或者

```bash
ehlo manon.com
```

通过这种方式，我们完成了邮件服务器的安装，并将其集成到我们的 LAMP Web 服务器中，发送我们的第一封 HTML 格式的网页邮件。

执行以下命令编辑 `PHP.ini` 配置文件：

```bash
sudo nano /etc/php5/apache2/php.ini
```

在文件中搜索名为 `sendmail_path` 的条目，将其更改为 `sendmail_path = "/usr/sbin/sendmail -t -i"`。

现在执行以下命令创建一个名为 `sendMail.php` 的文件，以便使用以下命令发送你的第一封邮件：

```bash
sudo nano /var/www/html/sendMail.php
```

将以下内容输入到你的文件中：

```php
<?php
$to = "mailofpersontosendto@hotmail.com, anothermailtosendto@gmail.com";
$subject = "HTML Mail Subject";
$message = "

<html>
<head>
<title>Title of the E-Mail</title>
</head>
<body>
<p>This is an HTML E-Mail Message !!!</p>
<table>
<tr>
<th>Column 1 Header</th>
<th>Column 2 Header</th>
</tr>
<tr>
<td>Content of Column 1 in HTML E-Mail</td>
<td>Content of Column 2 in HTML E-Mail</td>
</tr>
</table>
</body>
</html>

";
$headers = "MIME-Version: 1.0" . "\r\n";
$headers .= "Content-type:text/html;charset=UTF-8" . "\r\n";
$headers .= 'From: mostafa@manon.com' . "\r\n";
$headers .= 'Cc: manonmanager@manon.com' . "\r\n";

if(mail($to,$subject,$message,$headers)){
    echo 'Mail have been send successfully as desired.';
}else{
    echo 'We have encountered some error, please consult <br />Appendix G Troubleshooting your LINUX Mail Server';
}
```

现在将你的浏览器指向以下 URL：

`http://manon.com/sendMail.php`

或者

`http://localhost/sendMail.php`

访问此 URL 后，你将注意到邮件是否已发送。

如果你遇到任何错误，请查阅：

`Appendix G` Troubleshooting your LINUX Mail Server。

现在，我们已经完全安装了 LINUX 邮件服务器，你可以享受发送邮件了。

## 2.6 安装和管理 FTP, SFTP

让我们尝试安装我们的文件服务器。安装文件服务器将让你能够通过 `FTP`、`SFTP` 协议在你的机器上保存、更新和删除文件：

```bash
sudo apt-get install vsftpd
```

安装完成后，请运行以下命令配置你的 FTP 服务器设置：

```bash
sudo nano /etc/vsftpd.conf
```

完成后，编辑以下行并使其保持一致：

```ini
anonymous_enable=NO
local_enable=YES
write_enable=YES
chroot_local_user=YES
```

按下 `CTRL X` 保存并退出，然后按键盘上的 Enter。

现在，如下所示创建一个目录：

```bash
sudo mkdir /home/manon/files # 将 manon 更改为你操作系统的用户名。
```

然后，我们需要更改所有权：

```bash
sudo chown root:root /home/manon
# 将 manon 更改为为你操作系统的用户名
```

现在，我们需要执行以下命令重启服务：

```bash
sudo service vsftpd restart
```

现在，通过在终端执行以下命令连接到你的 FTP 服务器：

```bash
sudo ftp localhost
```

我们使用执行之前任务时使用的操作系统用户名，然后输入该账户的密码。

完成后，在终端输入 `exit` 终止 ftp 会话。

现在，让我们如下安装 FTP 客户端应用程序：

```bash
sudo apt-get install filezilla
```

安装完成后，启动你的 filezilla 应用程序并在主机字段中输入：`ftp://manon.com/`

用户名：`manon`

密码：`*******`

完成后，点击连接，现在你已经连接到了你的文件服务器。

你可以在服务器上创建目录、创建文件并对其进行管理。

现在，让我们如下在 Windows® 机器上映射网络驱动器：

打开开始菜单并在搜索框中输入“映射网络驱动器”（map network drive）。

在位置字段中，输入 FTP 服务器名称即 `ftp://manon.com/`。

在提示时，输入我们刚才提到的用户名和密码。

为了安装 FTP 的安全层即 `SFTP`，我们需要执行以下命令：

```bash
sudo a2ensite default-ssl.conf
```

然后，我们需要执行命令：

```bash
sudo service apache2 restart
```

接着，我们需要安装 ssh：

```bash
sudo apt-get install ssh
```




安装完成后，我们将能够使用 URL 通过 SFTP 连接到服务器：

`sftp://manon.com` # 将 manon.com 更改为你的 DNS 名称。

现在，让我们使用我们的平板设备。

我将使用一个支持 iOS 的平板设备浏览商店应用并找到一个名为 FTPManager® 的应用程序。

在 iPad 或 iPhone 上安装应用程序后，你会在应用程序的主菜单看到一个用于添加服务器的 `+` 符号。

等待，用于添加服务器的应用程序主菜单。

输入服务器地址 `ftp://manon.com/` 或 `sftp://manon.com`。

选择协议 `ftp` 或 `sftp`。

在下方输入你的用户名和密码。

现在，我们已经连接到文件服务器并可以移动和添加文件。

你也可以从服务器下载文件。

现在，我们涵盖了文件服务器的安装和配置。

## 2.7 安装和配置 SAMBA 并管理共享

SAMBA 是另一种安装文件服务器的方式。为了安装 SAMBA，我们需要通过以下步骤：

```bash
sudo apt-get install samba
```

```bash
sudo nano /etc/samba/smb.conf
```

在文件末尾添加以下内容：

```ini
[share]
comment = Ubuntu File Server Share
path = /srv/samba/share
browsable = yes
guest ok = yes
read only = no
create mask = 0755
```

执行以下命令创建共享目录：

```bash
sudo mkdir -p /srv/samba/share
```

完成后，为共享目录赋予适当权限：

```bash
sudo chown nobody:nogroup /srv/samba/share/
```

执行以下命令应用配置更改：

```bash
sudo service smbd restart
sudo service nmbd restart
```

通过这种方式，我们完成了 SAMBA 文件服务器的配置并创建了共享。如果你在任何 Windows 机器的网络选项浏览网络计算机，会发现我们的服务器共享对所有 Windows 用户可见。

## 2.8 安装 GIT 服务器

你有一个项目并想要创建一个本地 GIT 服务器而不是推送到公共 GIT 控制系统，这里有一个创建自己的 git 服务器的解决方案，让你与团队成员一起在本地机器上推送项目。

执行以下命令：

```bash
sudo apt-get install git
```

```bash
git config --global user.email "mostafa@manon.com"
```

之后，我们需要为任何人分配一个用户名，以便其可以使用以下命令连接到机器：

```bash
git config --global user.name "mostafa"
```

现在，让我们通过执行此命令，添加我们在安装 Web 服务器时创建的 Web 目录来创建第一个仓库：

```bash
git init --bare /var/www/html/
```

如果你在执行上一个命令时遇到任何问题，你需要执行以下命令：

```bash
cd /var/www/html/ && git init .
```

现在，我们使用用户名和密码克隆该仓库：

```bash
git clone mostafa@localhost:/var/www/html/
```

然后，我们需要执行以下命令：

```bash
cd /path/to/repository
```

接着，我们进行所谓的 commit（提交）操作并为其提供消息，或者留空，如下所示：

```bash
git commit -a
```

或者：

```bash
git commit -m "Contents are Finished"
```

然后，我们按照如下方式将任何更改推送到仓库：

```bash
git push origin master
```

### 安装另一个 GIT 服务器

还有另一个 git 服务器，其功能与我们安装的上一个 GIT 服务器相同。让我们按照以下步骤完成该服务器的安装过程：

```bash
sudo apt-get install gitolite
```

完成后，通过执行以下命令向系统中添加一个名为 `GIT` 的新用户：

```bash
sudo adduser --system --shell /bin/bash --group --disabled-password --home /home/git git
```

现在，我们需要查阅关于在机器上安装 SSH 服务器和客户端的文章，并遵循以下命令：

```bash
ssh-keygen -t rsa
```

接受默认设置并一直按键盘回车键直到完成，然后执行以下命令：

```bash
cp ~/.ssh/id_rsa.pub /tmp/$(whoami).pub
```

然后，我们需要使用以下命令登录我们创建的用户：

```bash
sudo su - git
```

```bash
gl-setup /tmp/*.pub
```

现在，你需要通过执行以下命令退出已登录的用户会话：

```bash
exit
```

最后，我们需要按照如下方式克隆仓库：

```bash
git clone git@manon.com:gitolite-admin.git
```

你需要做的是：将 `manon.com` 替换为你在安装 DNS 服务器时选择的计算机 DNS 名称（即黄色高亮部分）。

现在你可以使用以下命令浏览项目内容：

```bash
cd gitolite-admin
ls -l
```

要将仓库添加到现有项目，你可以执行如下所示命令：

```bash
git remote add gitolite git@$manon.com:manonproject.git
```

现在，我们已经完成了 GIT 服务器和客户端的安装、配置和使用。

# 3 Linux 安全安全

## 3.1 安装 SSH

`SSH` 服务器用于通过带有加密机制的安全套接层（如使用私钥和公密钥对）连接到你的机器。

私钥和公钥对的概念用途如下：

私钥保留在目标机器上，采用标准的加密格式，通常配合 `SHA-256` 加密机制以及 `SHA-2` 和 `RSA` 等基础加密机制。

要安装 SSH 服务器，请按照以下步骤操作：

```bash
sudo apt-get install openssh-server
```

接下来，我们安装 `openssh-client` 以获得完整的客户端功能。

```bash
sudo apt-get install openssh-client
```

要生成密钥对，我们需要执行以下命令：

```bash
ssh-keygen -t rsa
ssh-copy-id mostafa@manon.com
```

然后，我们为密钥目录赋予足够的权限，以确保一切安全。

```bash
chmod 600 .ssh/authorized_keys
```

如果你想通过浏览器访问你的 shell，我们需要安装以下软件包并按照如下所示进行编辑和配置：

```bash
sudo apt-get install ajaxterm
sudo sed -i 's:PasswordAuthentication.*:PasswordAuthentication yes:' /etc/ssh/sshd_config
```

接下来，我们使用以下命令重启服务：

```bash
sudo service ssh restart
```

现在，打开浏览器并使用如下 URL 指向你的机器：

`http://manon.com:8022/`

将 `manon.com` 替换为你自己的 IP 或你在 DNS 安装机器上使用的 DNS 字符串，你也可以使用 `localhost` 代替。

输入你的用户名，然后按键盘上的回车键。

输入你的密码，然后按键盘上的回车键。

你当然输入的是你操作系统的用户名和密码。

图 3.1 显示了上一步安装的结果。

![](img/Image1181.jpg)

## 3.2 使用 SSL 创建证书

在下一节中，我们将介绍创建自签名证书并对其签名。

我们还将通过自签名证书并将其附加到 Web 服务器作为使用这些证书的示例，步骤如下：

我们需要执行以下命令来创建一个密钥：

```bash
openssl genrsa -des3 -out server.key 2048
```

注意，`server.key` 可以更改为你使用的任何文件名。

现在我们为我们的密钥文件分配 `RSA` 加密，并将结果输出到一个不安全的文件，如下：

```bash
openssl rsa -in server.key -out server.key.insecure
```

现在我们按照如下所示创建我们的安全密钥：

```bash
mv server.key server.key.secure
```

然后我们按照如下方式移动密钥：

```bash
mv server.key.insecure server.key
```

现在，我们使用以下命令创建证书签名请求（CSR）：

```bash
openssl req -new -out server.csr
```

输入你的用户名，然后按键盘上的回车键。

输入你的密码，然后按键盘上的回车键。

你当然输入的是你操作系统的用户名和密码。

图 3.1 显示了上一步安装的结果。

![](img/Image1181.jpg)

## 3.2 使用 SSL 创建证书

在下一节中，我们将介绍创建自签名证书并对其签名。

我们还将通过自签名证书并将其附加到 Web 服务器作为使用这些证书的示例，步骤如下：

我们需要执行以下命令来创建一个密钥：

```bash
openssl genrsa -des3 -out server.key 2048
```

注意，`server.key` 可以更改为你使用的任何文件名。

现在我们为我们的密钥分配 `RSA` 加密，并将结果输出到一个不安全的文件，如下：

```bash
openssl rsa -in server.key -out server.key.insecure
```

现在我们按照如下所示创建我们的安全密钥：

```bash
mv server.key server.key.secure
```

然后我们按照如下方式移动密钥：

```bash
mv server.key.insecure server.key
```

现在，我们使用以下命令创建证书签名请求（CSR）：

```bash
openssl req -new
```

在之前的过程中，会出现一些提示，例如密码、国家名称、用户文件名以及城市和州值。你当然可以使用你自己的值，或者针对你特定需求的值。

当你完成所有操作后，浏览你的 `https://manon.com/` 服务器并确认你的安全异常，以将网站添加到信任站点，直接点击地址 `https://manon.com/` 旁的小图标，你会发现打开了一个窗口，点击 `more information`（更多信息），如果默认未启用，则转到 `security`（安全）选项卡，然后点击 `view certificate`（查看证书），你将发现证书已填充了你的协议以及服务器名称 `manon.com`，如下图 3.3 所示：

![](img/Image1196.jpg)

## 3.3 使用 SELinux 和访问控制

`SELINUX` 是一个用于启用和禁用服务并通过你的系统控制端口号和访问的网关。

在 UBUNTU LINUX 机器上安装 SELINUX，我们使用以下命令：

```bash
sudo apt-get install selinux
```

有 2 个主要选项来配置 SELINUX 软件包，我们将按照如下方式介绍如何启用每一个：

- **Permissive**：`manon.com` 最常用的选项，启用此选项的命令是：

  ```bash
  sudo sed -i ‘s/SELINUX=.*/SELINUX=permissive/’ /etc/selinux/config
  ```

- **Enforcing**：最安全的选项，启用此选项的命令是：

  ```bash
  sudo sed -i ‘s/SELINUX=.*/SELINUX=enforcing/’ /etc/selinux/config
  ```

UBUNTU 默认已安装的另一个防火墙软件包是：

`UFW`

正如我们所述，`UFW` 是默认安装的，我们将按照如下方式介绍它的配置和操作命令。

要启用该服务，我们需要运行以下命令：

```bash
sudo ufw enable
```

要对你正在使用的服务（如 `HTTP` 或 `HTTPS`）上启用或禁用端口，我们需要执行以下命令：

```bash
sudo ufw allow 8080 # 启用 HTTP 端口 8080
sudo ufw allow 80 # 启用 HTTP 端口 80
```

之前的端口号 8080 和 80 是 UBUNTU 用于 `HTTP` 协议的主要使用端口号。如果你禁用了其中一个端口，你将无法从其他机器浏览 `http://localhost/` 或 `http://manon.com/`。

```bash
sudo ufw deny 8080 # 禁用 HTTP 端口 8080
sudo ufw deny 80 # 禁用 HTTP 端口 80
sudo ufw allow 22 # 在端口 22 上启用 HTTPS
sudo ufw deny 22 # 在端口 22 上禁用 HTTPS
```

你也可以按照如下方式删除你创建的规则：

```bash
sudo ufw delete deny 22
sudo ufw delete deny 80
sudo ufw delete deny 8080
```

你也可以使用以下命令通过服务名调用 `allow`、`deny` 服务：

```bash
sudo ufw deny http
sudo ufw deny https
sudo ufw deny Samba
```

最后，我们可以使用以下命令启用和禁用服务：

```bash
sudo service ufw start
sudo service ufw stop
sudo service ufw restart
```

## 3.4 连接到 Linux 机器

在下一节中，我们将按照如下学习使用 `SSH` 协议连接到你的 LINUX 机器：

```bash
ssh localhost
```

我们使用此命令在本地网络内本地连接到机器。

如果我们从服务提供商处获得了静态 IP 地址服务并将其应用于我们的 LINUX 连接，我们就能使用以下命令从任何地方连接到我们的机器：

```bash
ssh 192.168.0.2
```

将 `192.168.0.2` 替换为你将获得的 ISP IP 地址。

你也可以使用我们在为你的 UBUNTU LINUX 机器安装 DNS 时使用的 DNS 字符串连接到你的机器：

```bash
ssh manon.com
```

你需要一个用户名和密码来访问机器，如果你安装了像我们在 `#Creating Certificates using SSL` 章节中提到的公钥-私钥对（该章节中包含了我们创建的密钥文件）。

要使用密钥文件，我们需要执行以下命令：

```bash
ssh -l mostafa -i /etc/ssl/certs/manon.com.pem manon.com
```

或者：

```bash
ssh -l mostafa -i /etc/ssl/certs/manon.com.pem localhost
```

输入你在创建文件时使用的短语（pass phrase）。

输入你用于登录系统的操作系统密码。

然后，你将看到如图 3.4 所示的屏幕。

![](img/Image1205.jpg)

通过这种方式，你可以远程控制你的机器并在上面执行任何任务。

我们现在已经涵盖了如何使用 `SSH` 服务连接到你的机器。

## 3.5 在 Linux 中保护你的 Web 服务器

为了在 LINUX 中保护你的 Web 服务器，我们需要检查一个清单，我们在进入 Web 服务器安全主题时将按照如下方式进行：

1. 在进入 Web 服务器安全主题时，按照如下方式执行连接。
2. 使用以下工具进行 `HTTP` 和 `HTTP` 扫描：
   - `Httrack`
   - `Burp Suite`
   - `Web Scarab`
3. 部署应用时使用 `.htaccess` 文件，通过以下命令禁用索引：

   ```bash
   sudo nano /var/www/html/.htaccess
   ```

   在文件中添加以下代码：

   ```apache
   Options -Indexes
   ```

   使用 `CTRL + X` 保存文件。当你打开 Web 服务器上的空目录时，将得到拒绝访问错误。

## 3.6 在 Linux 中保护你的数据库服务器

为了保护我们安装的 `MySQL` 数据库服务器，我们需要按照如下方式进行以下安装和配置：

输入以下命令：

```bash
mysql_secure_installation
```




在提示时输入`root`密码。

在`change password`提示中，你可以根据环境输入`Y`或`N`来更改。

在`remove anonymous users`提示中，输入`Y`并按回车。

在`disallow root remotely`提示中，为了安全选择`Y`，不要让同一网络中的其他机器登录数据库服务器。

在`remove test database and access to it`提示中，选择`Y`并按回车。

现在在`reload privilege table`，选择`Y`并按回车。

![Image16](img/Image16.jpg)

注意，在我们配置结束时，你将看到如图 3.5 所示的屏幕。

但注意在我的状态下，我允许了远程登录尝试以便远程访问服务器，这种选项适用于云镜像安装，如果你在云环境中使用 UBUNTU，你将使用此选项，因为你要远程连接到数据库服务器。

## 3.7 保护你的 Linux 虚拟机

保护 LINUX 虚拟机与保护 LINUX 机器完全一样，只是需要考虑到虚拟机被远程访问。因此，在进行安全措施时，你需要考虑到公共访问多于本地访问。

图 4.1 显示了`listing interfaces`命令的输出。

我们也可以使用以下命令获取当前可用网络接口列表，该命令将为提供关于每个接口的详细信息。

```bash
ip addr
```

![Image1234](img/Image1234.jpg)

图 4.2 显示了更详细的列出接口输出。

现在，我们需要按照如下方式配置网络适配器：

```bash
sudo vi /etc/network/interfaces
```

如果你想配置你的网络适配器使用静态 IP 地址，那么我们需要在正在编辑的文件中添加以下行：

```text
auto eth0
iface eth0 inet static
address 192.168.0.2
netmask 255.255.255.0
network 192.168.0.1
broadcast 192.168.0.255
gateway 192.168.0.1
dns-nameservers 192.168.0.1
```

![Image1242](img/Image1242.jpg)

图 4.3 显示了我们必须应用到网络适配器的上述配置设置。

然后，我们需要按照如下方式重启网络：

```bash
sudo ifdown -a && sudo ifup -a
```

通过这种方式，我们配置了有线网络适配器使用我们分配的静态 IP 地址。

## 4.2 Linux 中的无线网络

为了开始使用无线网络适配器，我们需要执行以下命令列出适配器，以获取我们将要使用的适配器名称：

```bash
sudo ls /sys/class/net
```

或者更详细地，我们可以执行以下命令：

```bash
ip addr
```

在我的情况下，无线适配器的名称为`wlan0`。

在大多数 LINUX 机器的系统中，这是你所使用的无线适配器的默认名称，如果你在机器上安装了多个适配器，你会发现它们被命名为`wlan1`、`wlan2`、`wlan3`等。

我们需要执行以下命令来编辑网络接口并按如下方式调整静态 IP 地址：

```bash
sudo vi /etc/network/interfaces
```

现在我们通过添加这些配置行来编辑文件：

```text
auto wlan0
iface wlan0 inet static
address 192.168.0.2
netmask 255.255.255.0
network 192.168.0.2
broadcast 192.168.0.255
gateway 192.168.0.2
dns-nameservers 192.168.0.2
```

现在按`CTRL + X`保存文件，使用相同的路径和文件名进行确认。

现在我们需要按照如下方式重启网络适配器：

```bash
sudo ifdown -a && sudo ifup -a
```

或者我们可以使用以下命令：

```bash
sudo service network-manager restart
```

或者

```bash
sudo service NetworkManager restart
```

## 4.3 Linux 中的 Network Manager

为了管理你的网络管理器，我们需要执行以下操作：

```bash
sudo service network-manager start
sudo service network-manager stop
sudo service network-manager restart
sudo service NetworkManager start
sudo service NetworkManager stop
sudo service NetworkManager restart
```

前 3 条命令用于在某些 UBUNTU LINUX 发行版和 FEDORA 发行版中启动、停止并重启服务。

后 3 条命令用于在其他 UBUBU 发行版中启动、停止并重启服务。

如果你在使用 UBUNTU 或 FEDORA 的云镜像，或者无论你使用的是什么发行版，都可以按照如下方式安装网络管理器服务：

```bash
sudo apt-get install network-manager
```

要在 GNOME 发行版中安装指示器，可以使用以下命令：

```bash
sudo apt-get install network-manager-gnome
```

## 4.4 Linux 中的网络监控

如果你想安装带宽监控工具，我们将按照如下方式安装带图表的`bandwidthd`：

```bash
sudo apt-get install bandwidthd
```

完成后，我们需要按照如下方式将安装链接到我们的 Web 服务器：

```bash
sudo ln -s /var/lib/bandwidthd/htdocs /var/www/bandwidth
```

最后我们可以重启 apache 服务以完成整个过程：

```bash
sudo service apache2 restart
```

完成后，通过指向以下 URL，我们现在一切都正常运行：

[`manon.com/bandwidthd/`](http://manon.com/bandwidthd/)

![Image1249](img/Image1249.jpg)

图 4.4 显示了网络带宽监控工具的控制台。

## 4.5 Linux 中的网络扫描

我们首先需要了解什么是网络上的端口扫描和 IP 扫描：

端口扫描是一种了解我们进行扫描的每个设备上开启了哪些端口的方法。

IP 扫描是一种了解我的网络中哪些 IP 地址正在运行并处于在线状态的方法。

执行方式如下所示：

我们需要按照如下方式在你的 UBUNTU LINUX 机器上安装`nmap`服务协议：

```bash
sudo apt-get install nmap
```

完成后，我们需要按如下方式进行 IP 扫描以查看网络中哪些设备是在线的：

```bash
sudo nmap -sn 192.168.0.0/24
```

扫描结果如下所示：

- 192.168.0.1
- 192.168.0.2
- 192.168.0.3
- 192.168.0.4
- 192.168.0.5
- 192.168.0.6
- 192.168.0.7
- 192.168.0.8
- 192.168.0.9
- 192.168.0.10
- 192.168.0.11
- 192.168.0.12
- 192.168.0.13
- 192.168.0.14
- 192.168.0.15
- 192.168.0.16
- 192.168.0.17
- 192.168.0.18
- 192.168.0.19
- 192.168.0.20
- 192.168.0.21
- 192.168.0.22
- 192.168.0.23
- 192.168.0.24
- 192.168.0.25
- 192.168.0.26
- 192.168.0.27
- 192.168.0.28
- 192.168.0.29
- 192.168.0.30
- 192.168.0.31

接下来，我们需要检查每个主机上哪些端口是开启的：

```bash
sudo nmap 192.168.0.1
```

扫描结果如下：

- 192.168.0.1:80/tcp open (http)
- 192.168.0.1:443/tcp open (https)
- ...
- 192.168.0.1:8080/tcp open (http-proxy)

# 5 Linux 中的私有云

## 5.1 安装 Openstack

Openstack 是由一家名为 Redhat 的公司创建的操作系统，它是云行业中拥有巨大市场份额的公司（如 Canonical, IBM, Rackspace, Dell, HP, CISCO, SUSE, Nebula 和 VMware）。

为了开始安装，让我们输入以下命令。如果你还没有完成 git 的安装，请前往 git 章节并安装 git 以运行此命令：

```bash
sudo git clone https://git.openstack.org/openstack/devstack
```

让我们使用管理工具安装。下载完成后，我们需要按如下方式更改下载内容的权限：

```bash
sudo chmod 777 -R ~/devstack
```

完成后，我们需要按照如下方式启动安装：

```bash
cd ~/devstack
```

然后启动安装脚本：

```bash
./stack.sh
```

在提示时，输入你安装 LAMP 服务器时使用的相同密码。如果你没有安装任何数据库服务器，可以使用任何新密码，建议使用字母和数字。

最后，我们需要通过执行此脚本自动完成一系列下载和安装程序，然后我们以如下屏幕结束：

![Image1274](img/Image1274.jpg)

图 5.1 显示了包含服务 URL 和凭据（用户名和密码）的确认屏幕

完成后，你将看到如何访问我们安装的服务的屏幕，如前一个图所示。

现在打开浏览器并指向以下任一 URL：

[`manon.com/auth/login/?next=/`](http://manon.com/auth/login/?next=/)
[`manon.com/auth/login/`](http://manon.com/auth/login/)
[`manon.com/`](http://manon.com/)

你需要将上述之前的 URL 域名更改为你的 DNS 字符串，或者如果你使用同一台机器，可以使用 localhost 或你的 IP 地址。

![Image1281](img/Image1281.jpg)

如果您已完成用户名（demo 或 admin）以及安装期间输入的密码输入，并点击连接（connect），您将看到仪表板。

通过这种方式，我们已经完全安装并运行了我们的 OpenStack 服务。

## 5.2 使用 Openstack Keystone

首先，我们将学习到的是关于`keystone`的身份验证和授权。

我们将按照以下步骤创建一个项目、用户名和密码，创建一个角色，并将用户添加到该角色中：

使用终端创建项目，请输入以下命令：

```bash
sudo openstack project create --description ‘New Project’ --os-username=admin --os-password=INSTALLATIONPASSHERE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin manon
```

您最终将看到一个类似于图 5.3 所示的屏幕

![Image1289](img/Image1289.jpg)

使用终端创建用户，请输入以下命令：

```bash
sudo openstack user create --project admin --password PASSWORDHERE manon --os-username=admin --os-password=INSTALLATIONPASSHERE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin
```

运行此命令时，我们将看到下所示图 5.4 所示的确认屏幕：

![Image1298](img/Image1298.jpg)

通过这种方式，我们在我们的 OpenStack 服务中创建了一个新用户，现在可以使用我们创建的新凭据进行登录了。

将您的浏览器指向之前的 URL：

- [`localhost/`](http://localhost/)
- [`manon.com/`](http://manon.com/)
- [`127.0.0.1/`](http://127.0.0.1/)

然后填写您在上一个命令中使用的用户名和密码即可开始。

要禁用该用户，我们可以执行以下命令：

```bash
sudo openstack user set manon --disable --os-username=admin --os-password=INSTALLATIONPASSHERE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin
```

要列出用户，我们可以执行以下命令：

```bash
sudo openstack user list --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin --os-username=admin --os-password=INSTALLATIONPASSHERE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin
```

![Image1309](img/Image1309.jpg)

**图 5.5** 显示了我们拥有的用户，包括我们创建的用户（用黑色背景高亮）。

要启用我们已经禁用的用户，我们需要执行以下命令：

```bash
sudo openstack user set manon --enable --os-username=admin --os-password=INSTALLATIONPASSHERE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin
```

要删除用户，我们可以执行以下命令：

```bash
sudo openstack user delete manon --os-username=admin --os-password=INSTALLATIONPASSHERE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin
```

要创建一个角色，我们可以执行以下命令：

```bash
sudo openstack role create rolename --os-username=admin --os-password=INSTALLATIONPASSHERE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin
```

![Image1322](img/Image1322.jpg)

**图 5.6** 显示了上一个命令的输出，如下所示：

要将用户添加到角色，我们可以执行以下命令：

```bash
sudo openstack role add --user manon --project manon manonrole --os-username=admin --os-password=INSTALLATIONPASSPHRASE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin
```

上一个命令的输出与图 5.6 的输出相同。

要禁用一个项目，您可以执行以下命令：

```bash
sudo openstack project set manon --disable --os-username=admin --os-password=INSTALLATIONPASSPHRASE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin
```

要启用一个项目，您可以执行以下命令：

```bash
sudo openstack project set manon --enable --os-username=admin --os-password=INSTALLATIONPASSPHRASE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin
```

要更新项目名称，我们可以执行以下命令：

```bash
sudo openstack project set manon --name mannew --os-username=admin --os-password=INSTALLATIONPASSPHRASE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin
```

要显示项目的详情，我们可以执行以下命令：

```bash
sudo openstack project show manon --os-username=admin --os-password=INSTALLATIONPASSPHRASE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin
```




要删除项目，我们可以执行以下命令：

```bash
sudo openstack project delete manon --os-username=admin --os-password=INSTALLATIONPASSPHRASE --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin
```

我们也可以使用相同的密钥来编辑环境。这些密钥是强制性的，必须在命令中使用。操作方法如下：

```bash
touch adminrc
sudo nano adminrc
```

在文件中，输入以下值：

```bash
OS_USERNAME=manon
OS_PASSWORD=password
OS_AUTH_URL=http://localhost:5000/
OS_PROJECT_NAME=admin
```

您必须按 `CTRL + X` 退出文本界面并回车确认文件。然后执行以下命令：

```bash
source adminrc
openstack project set manon --name mannew
```

现在，我们已经完成了 OpenStack 身份服务的管理操作。

## 5.3 使用 OpenStack Heat

让我们了解 OpenStack Heat。Heat 是用于编排 OpenStack 服务的编排引擎，现在我们将了解它的功能以及它能为云环境做什么。

现在，以 root 用户身份登录 MySQL 服务器：

```bash
sudo mysql -uroot -p
```

然后您需要输入安装数据库时输入的密码。之后，您将看到下面的屏幕。

完成后，我们需要创建一个名为 `heat` 的新数据库并授予访问权限：

```sql
CREATE DATABASE heat;

GRANT ALL PRIVILEGES ON heat.* TO 'heat'@'localhost' IDENTIFIED BY 'INSTALLATIONHERE';

GRANT ALL PRIVILEGES ON heat.* TO 'heat'@'%' IDENTIFIED BY 'INSTALLATIONHERE';
```

现在，输入 `exit`，您将看到退出信息。

接下来，我们创建一个委托给 Heat 编排服务的用户：

```bash
sudo openstack user create --project admin --password PASSWORDHERE heat
```

之后，我们需要按照如下方式创建 Heat 服务：

```bash
sudo openstack role add --user heat --project manon manonrole
```

最后，在处理 Heat API 时，我们需要创建两个端点。端点是两个或多个服务之间集成网关工作的地方，或用于一个系统与另一个系统的通信。

我们创建的第一个端点是 `heat`，适用于我们创建的 `heat` 用户和 `heat` 角色，如下所示：

```bash
sudo openstack endpoint create --publicurl http://192.168.0.2:8004/v1/fc38a412004b4664a55fd9a975e40085 --internalurl http://192.168.0.2:8004/v1/fc38a412004b4664a55fd9a975e40085 --adminurl http://192.168.0.2:8004/v1/fc38a412004b4664a55fd9a975e40085 --region regionOne --os-username=admin --os-password=manon1982 --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin heat
```

我们需要创建的第二个端点是 `heat-cfn`：

```bash
sudo openstack endpoint create --publicurl http://192.168.0.2:8004/v1/83dace3c2f44444fb8780576f341b64d --internalurl http://192.168.0.2:8004/v1/83dace3c2f44444fb8780576f341b64d --adminurl http://192.168.0.2:8004/v1/83dace3c2f44444fb8780576f341b64d --region regionOne --os-username=admin --os-password=manon1982 --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin heat-cfn
```

接下来，我们按照以下步骤进行安装：

```bash
sudo apt-get install heat-api heat-api-cfn heat-engine python-heatclient
```

接下来，我们需要对名为 `heat.conf` 的文件进行配置更改：

```bash
sudo nano /etc/heat/heat.conf
```

我们需要根据我们的环境修改以下变量。

在数据库部分 `[DATABASE]` 中，我们需要修改以下行：

`connection = mysql://heat:HEAT_DBPASS@controller/heat`

然后，我们需要在 `[DEFAULT]` 部分中修改以下内容：

`rpc_backend = rabbit`

`rabbit_host = localhost`

`rabbit_password = guest`

`heat_metadata_server_url = http://localhost:8000`

`heat_waitcondition_server_url = http://localhost:8000/v1/waitcondition`

然后，我们需要在名为 `[keystone_authtoken]` 的部分中修改内容：

`auth_uri = http://localhost:5000/v2.0`

`identity_uri = http://localhost:35357`

`admin_tenant_name = admin`

`admin_user = heat`

`admin_password = PASSWORDHERE`

然后，我们需要在 `[ec2authtoken]` 部分中编辑以下行：

`auth_uri = http://localhost:5000/v2.0`

然后，我们需要通过执行以下命令来填充我们的数据库：

```bash
sudo su -s /bin/sh -c “heat-manage db_sync” heat
```

最后，我们通过执行以下命令来完成解决方案：

```bash
sudo service heat-api restart
sudo service heat-api-cfn restart
sudo service heat-engine restart
```

如果你正在使用 `UBUNTU LINUX`，那么我们需要执行以下命令来删除未使用的数据库：

```bash
rm -f /var/lib/heat/heat.sqlite
```

要创建一个栈（stack），我们需要创建一个名为 `heatorchestrationtemplate.yaml` 的文件。

我们需要执行以下命令：

```bash
touch heatorehcstrationtemplate.yaml
```

然后，我们使用此命令编辑文件：

```bash
nano heatorchestrationtemplate.yaml
```

最后，我们需要向文件中添加以下内容，并根据我们的环境考虑任何更改：

```yaml
heat_template_version: 2013-05-23

description: Simple template to deploy a single compute instance

resources:

  my_instance:

    type: OS::Nova::Server

    properties:

      image: /path/to/image/downloaded_ubuntu_cloud_image.img

      flavor: m1.small

      key_name: keyfile.pem

    networks:

      - network: network-name
```

然后，我们需要调整高亮的数据以适应我们的环境。

最后，我们可以在以下命令中使用我们的文件来创建一个 Heat 编排栈：

```bash
sudo openstack stack create manon_stack -f heatorchestrationtemplate.yaml
```

现在，我们已经安装了 Heat 服务，进行了完整的配置以使其能够正常工作，并在 Heat 服务上创建了一个示例栈。

## 5.4 使用 OpenStack Swift

现在，让我们按照以下步骤安装 Swift 存储服务并启用复制：

```bash
sudo apt-get install swift swift-account swift-container swift-object xfsprogs
```

现在，让我们创建一个名为 `rsyncd.conf` 的文件：

```bash
sudo nano /etc/rsyncd.conf
```

然后，我们需要输入以下数据，并注意你需要根据你的环境进行更改：

```ini
uid = swift
gid = swift
log file = /var/log/rsyncd.log
pid file = /var/run/rsyncd.pid
address = 192.168.0.2

[account]
connections = 2
path = /srv/node/
read only = false
lock file = /var/lock/account

[container]
connections = 2
path = /srv/node/
read only = false
lock file = /var/lock/container

[object]
connections = 2
path = /srv/node/
read only = false
lock file = /var/lock/object
```

然后，我们需要编辑以下文件：

```bash
sudo nano /etc/default/rsync
```

我们找到包含以下内容的行并进行编辑：

```bash
RSYNC_ENABLE=true
```

然后我们必须启动 `rsync` 服务：

```bash
service rsync start
```

然后，我们需要执行以下命令：

```bash
sudo mkdir -p /var/swift
chown -R swift:swift /var/swift
```

现在，我们完成了存储服务的工作并完成了基础同步。

## 5.5 使用 OpenStack Glance

Glance 是我们用于在裸机硬件上创建虚拟机的镜像服务。它可以让多个操作系统进行相互通信。

首先，我们需要执行：

```bash
sudo apt-get install glance
```

然后，我们需要安装以下包以完成依赖：

```bash
sudo apt-get install python-glanceclient
```

现在按 `Y` 确认所有命令。

我们现在已经安装了 Glance 服务，现在我们需要从互联网上的 Ubuntu 云镜像目录下载我们的第一个镜像，地址如下：

[`cloud-images.ubuntu.com/wily/current/`](https://cloud-images.ubuntu.com/wily/current/)

这是由 Canonical 公司开发的 Ubuntu 最新版本。该发行版是最流行的云镜像之一。

我们现在可以使用此镜像将其导入我们的 OpenStack 私有云：

```bash
sudo openstack image create --name=”UBUNTU CLOUD IMAGE” --disk-format=qcow2 --container-format=bare --is-public=true < /home/mostafa/Downloads/ubuntu-14.04-server-cloudimg-i386/trusty-server-cloudimg-i386.img --os-username=admin --os-password=AMINPASSWORD --os-auth-url=http://192.168.0.2:5000/ --os-project-name=admin
```

现在我们已经完成了 OpenStack 服务的安装和配置。我们还使用了它的部分服务，学习了如何与 Linux 交互，并了解了发行版、仓库、基础命令以及 Linux 可以实现的大部分功能。我们还安装了来自第三方和其他供应商的一些进阶功能和组件的基础设施。

非常感谢，感谢你抽出宝贵的时间阅读本书。

希望你喜欢。

