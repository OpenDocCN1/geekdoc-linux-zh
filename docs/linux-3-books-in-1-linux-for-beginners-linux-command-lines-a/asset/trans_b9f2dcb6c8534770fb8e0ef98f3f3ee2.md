

```bash
local myarray
myarray=(`echo "$@"`)
echo "This the new value of the array: ${myarray[*]}"
```

thisarray=(1 2 3 4 5 6 7 8 9 10)
echo "This the original value of the array ${thisarray[*]}"
testingfunction ${thisarray[*]}
```bash -f main.sh```

该数组的原始值：1 2 3 4 5 6 7 8 9 10

该数组的新值：1 2 3 4 5 6 7 8 9 10

名为 $thisarray 的变量包含各个数组值，将它们放置在函数的命令行中。然后，该函数使用命令行参数构建数组变量，一旦进入函数内部，你就可以像使用其他数组一样使用该数组。

```bash
$ cat test11
#!/bin/bash
function addingthearray {
    local sum=0
    local thisarray
    thisarray=(`echo "$@"`)
    for values in ${thisarray[*]}
    do
    sum=$[ $sum + $values ]
    done
    echo $sum
}

iarray=(1 2 3 4 5 6 7 8 9 10 11 12 13)
echo "This is the original value of the array: ${iarray[*]}"
arg1=`echo ${iarray[*]}`
therealresult="addingthearray $arg1"
echo "This is the final result : $therealresult"
bash -f main.sh
```

该数组的原始值：1 2 3 4 5 6 7 8 9 10 11 12 13

最终结果：91

## 处理用户输入

你已经学习了如何编写在 Linux 操作系统上与数据、文件和变量交互的 shell 脚本。然而，有时你需要编写必须与运行脚本的人员进行交互的脚本。Shell 提供了几种从人员处获取数据的方法，包括一些命令行参数、命令行选项以及从键盘读取输入。本章将指导你如何在 bash shell 脚本中结合不同的方法，以从运行脚本的人那里获取数据。

称为位置参数的变量由 bash shell 分配给命令行参数，包括由 shell 执行的程序名称。我们对位置参数变量使用标准数字 - $0 是程序名称，$1 是第一个参数，$2 是第二个参数，依此类推，直到 $9。

## 结论

既然你已到达本书的末尾，你应该已经很好地掌握了 Linux 命令行和 shell 脚本编程。与其他操作系统不同，Linux 操作系统较为复杂。你不会看到一个可以操作鼠标的图形界面。正是这种“全键盘”特性使得 Linux 难以学习。然而，带着这本书在口袋里，它并没有那么难。你可以随时将这本书作为参考指南，操作 Linux 命令行或跳转到编辑器编写 shell 脚本时都可以使用。保持一致并定期练习代码将帮助你比仅仅阅读脚本更快地学习命令和代码。

把这本书放在手边，你就随时可以触手可及地使用键盘快捷方式和命令。现在，让我们开始探索 Linux！

## 参考书目

- 22 best Linux text editors for coding (2020 Reviews). (2020, July 12). Knowledge Base by phoenixNAP. https://phoenixnap.com/kb/best-linux-text-editors-for-coding
- Bash while loop examples. (2020, November 5). nixCraft. https://www.cyberciti.biz/faq/bash-while-loop/
- Blum, R. (n.d.). Linux Command Line and Shell Scripting. https://inf.ocs.ku.ac.th/Download/Wiley_Linux_Command_Line_and_Sh
- Broida, R. (2017, February 9). How to install Linux. CNET. https://www.cnet.com/how-to/how-to-install-linux/
- Ward, B. (n.d.). How Linux Works. index-of.es/. https://index-of.es/Varios-2/How%20Linux%20Works%20What%20Every%20Superuser%20Sh

# LINUX 安全与管理

Andy Vickler

## 简介

![](img/aae83b54a1b1783f3f5369bd9062b27c_264_0.png)

如果你是 Linux 的新手，将很难在线找到正确的信息。本书包含你安装操作系统所需的所有信息，并指导你如何在你的系统或虚拟系统上使用它。本书还提供了关于如何配置用户访问权限和其他信息以维护 Linux 系统中网络和服务器安全的信息。你不需要在使用之前了解任何 Linux 知识，因为书中的信息将指导你每一步！

本书介绍了在虚拟系统上使用 Linux 的理念，并提供了关于不同 Linux 发行版的信息。你可以使用这些信息来确定哪些发行版最适合你，并将其下载到你系统中。你还将学习 root 账户的重要性以及服务器上的其他账户。本书还提供了关于控制用户访问权限方法的信息。你将学习如何授予和撤销用户权限以帮助你保护数据。

本书涵盖了如何保护操作系统中的信息、文件和文件夹。你将接触到一系列可用于保护系统中数据的工具，以及如何使用这些工具加密和解密信息。如有需要，你还可以使用密码来加密和解密服务器和网络上的文件和文件夹。

由于 Linux 是一个操作系统，而数据存储于服务器或网络上，因此你需要测试网络和服务器强度。本书将阐明你可以使用的方法来识别系统中的任何漏洞。它还将让你知道如何使用扫描来识别系统中的漏洞。你可以使用本书中的信息来确定如何克服这些漏洞。

感谢购买本书。希望你能进一步了解 Linux 以及如何在文件和文件夹中保护信息。

## 第一章：在虚拟机上使用 Linux

你曾经想过使用 Linux 但不想在系统上直接使用吗？如果使用双启动，你的系统可能会出现麻烦，最好的办法是在虚拟机上使用 Linux。如果你使用 Windows，在虚拟机上使用 Linux 很简单。步骤很直接。在本章中，我们将查看在虚拟机（特别是 VMware Workstation）上安装和使用 Linux。

如果你想使用虚拟机，你需要找到一台允许使用虚拟化的 PC。你可能曾尝试使用 CD 在系统上安装 Linux，但可能不确定是否适合双启动。你应该在 PC 上安装 Linux 操作系统，但使用虚拟机来实现。

虚拟机是复制设备硬件条件的工作环境。该环境镜像了个人计算机中的一切，并受系统不同组件的限制。这意味着你不能期望在一个只有两个核心的处理器上拥有四核 CPU。你可以在多个系统上实现虚拟化，结果在支持虚拟化的 CPU 计算机上会更优越。

你可以使用不同的虚拟机在计算机上安装 Linux 操作系统。VMware 是虚拟机和应用的主要制造商之一。在本章中，我们将查看如何使用 VMware 设计的工作站播放器在 Windows 上安装 Linux OS。

### 安装工作站播放器

如果你想要工作站播放器，你需要从 VMware 网站下载最新版本。他们不断升级工作站播放器应用程序和工具。在这个例子中，我们将使用 VMware workstation 15 player，该文件大小为 150 MB。最新版本可能更大，因此请确保你有良好的互联网连接。

这些工作站播放器可用于家庭、非商业和个人用途，且免费。非营利组织和学生可以使用此版本，因为他们无需在安装操作系统时花费任何费用。VMware 工作站播放器执行标准虚拟机必须具备的所有功能。你还可以使用 VMware 产品，因为每个产品都提供了广泛的可视化解决方案，你可以用于任何业务。如果你想了解他们的产品，可以在其网站上阅读。下载 VMware 工作站播放器后，点击安装程序并按照安装向导步骤设置你的虚拟工作站。建议你在安装期间下载增强键盘驱动程序，因为你现在可能不需要但稍后会需要。完成安装并在向导提示时重启系统。

### 选择正确的发行版

你应该阅读可用的不同 Linux 发行版，并选择最适合你的那个。某些 Linux 发行版最适合在虚拟机上运行，而其他发行版则无法在虚拟机上运行。所有 64 位和 32 位版本的 Linux 在虚拟机上运行良好。你不能在虚拟机上运行 Raspberry Pi 和其他 ARM 架构的 Linux 发行版等 Linux 发行版。如果你想在 Windows 机器上使用 ARM Linux 环境，应该尝试 QEMU。如果你不知道该选择哪个发行版，请从下表中选择任意一个：

### Linux 发行版

由于有很多选择，你可能发现很难为你的系统选择合适的 Linux 发行版。你怎么知道那是你应该用于系统的最佳选择呢？如果你想使用 Linux 发行版玩游戏怎么办？你想使用使用与 macOS 相同结构的漂亮发行版吗？

在本节中，我们将查看可用的不同 Linux 发行版列表。这些发行版在过去几年中被各种个人积极使用。最好下载一个你可以安全用于系统的 Linux 发行版。你还应检查你使用的发行版是否定期使用安全补丁进行更新。

