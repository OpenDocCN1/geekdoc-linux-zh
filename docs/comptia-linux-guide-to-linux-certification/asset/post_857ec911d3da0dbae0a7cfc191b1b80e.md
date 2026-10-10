
  在你的虚拟化软件中，确保为Ubuntu Server Linux虚拟机挂载的DVD连接了Ubuntu Server 14.04的ISO镜像（ubuntu-14.04.1-server-amd64.iso）。然后，使用虚拟化软件启动并连接你的Ubuntu Server Linux虚拟机。

  在语言界面，确保选择**English**并按下**Enter**。

  在Ubuntu欢迎界面，导航到**Rescue a broken system**选项并按下**Enter**。

  在“Select a language”页面，确保选择**English**并按下**Enter**。

  在“Select your location”界面，确保选择**United States**并按下**Enter**。

  在“Configure the keyboard”界面，选择**Yes**并按下**Enter**。按照提示完成检测。当检测到“us”键盘布局时，选择**Continue**并按下**Enter**。

  在“Configure the network”界面，查看默认的主机名，选择**Continue**，并按下**Enter**。

  在“Configure the clock”界面，确保显示正确的时间区，选择**Yes**，并按下**Enter**。或者，如果显示的时间区不正确，选择**No**，按下**Enter**，选择你的时间区，然后按下**Enter**。

  在“Enter rescue mode”界面，选择**/dev/UbuntuXX-vg/root**（其中XX是课程设置期间由你的老师分配给你的唯一编号），然后按下**Enter**。当提示是否也挂载/boot分区时，确保选择**Yes**并按下**Enter**。

  在“Enter rescue mode”界面，查看选项。选择**Execute a shell in /dev/UbuntuXX-vg/root**（其中XX是课程设置期间由你的老师分配给你的唯一编号），然后按下**Enter**。当提示时，确保选择**Continue**并按下**Enter**。这将使用**chroot**命令将根目录更改为硬驱动器上已挂载的/(root)文件系统。

  在命令提示符下，输入**df**并按下**Enter**以查看已挂载的文件系统。硬驱动器的根文件系统已挂载吗？

  在命令提示符下，输入**passwd root**并按下**Enter**。提供新的root用户密码**Secret123**，并在提示时（两次）按下**Enter**。

  在命令提示符下，输入**exit**并按下**Enter**。

  在“Enter rescue mode”界面，选择**Reboot the system**并按下**Enter**。

  在虚拟化软件的虚拟机设置中，确保DVD驱动器不再连接到Ubuntu Server ISO镜像。

  系统加载完成后，使用用户名**root**和密码**Secret123**登录到命令行终端（tty1）。

## Discovery Exercises

1.  通过查看`/proc`目录中的相应文件来确定以下关于你的系统的信息：
    - a. Linux内核在哪里？
    - b. 你的Linux内核版本是多少？
    - c. 你的Linux内核支持哪些文件系统？
    - d. 哪些模块已加载到内核中？
    - e. 收集关于你系统物理内存的信息。

2.  使用互联网收集有关三种不同的商用iSCSI SAN机箱的信息，这些机箱可用于托管Linux，并撰写一份简短报告，比较和对比它们的功能和成本。在哪些情况下你会使用每一种？

3.  使用互联网收集有关三种不同的商用硬件RAID控制器的信息，这些控制器执行RAID级别5，并撰写一份简短报告，比较和对比它们的功能和成本。在哪些情况下你会使用每一种？

4.  在互联网上搜索有关五个与本章节中描述的不同Linux安装问题的信息。其他人是如何解决这些问题的？如果你在安装过程中遇到了类似的困难，你会如何寻求帮助？

5.  Linux服务器通常存放在上锁的服务器机柜中，以防止未经授权的人员进行物理访问。鉴于你在项目6-4中执行的步骤，描述为什么这些物理限制是合理的。

6. 

![](img/c27875544958897d817484d558c208c8_326_0.png)

# Working with the BASH Shell

完成本章后，你将能够：

- 重定向命令的输入和输出
- 识别和操作常见的shell环境变量
- 创建和导出新的shell变量
- 编辑环境文件以在shell启动时创建变量
- 描述shell脚本的目的和性质
- 创建和执行基本的shell脚本
- 有效使用shell脚本中常见的决策构造

对shell功能的深刻理解对管理者和用户都至关重要，因为他们必须每天与shell交互。本章的第一部分描述了shell如何使用重定向和管道shell元字符来操作命令的输入和输出。接下来，你将探索登录后BASH shell中存在不同类型的变量，以及它们的目的和用法。最后，本章以对创建和执行BASH shell脚本的介绍结束。

## Command Input and Output

BASH shell负责提供用户界面并解释在命令行上输入的指令。此外，如果用户在命令行上的命令旁边指定了特定的shell元字符，BASH shell也可以操作命令的输入和输出。命令的输入和输出由称为**file descriptors**的标签表示。对于每个可由BASH shell操作的命令，有三个file descriptors：

- Standard Input (stdin)
- Standard Output (stdout)
- Standard Error (stderr)

**Standard Input (stdin)**指的是命令执行期间处理的信息；这通常采取在键盘上输入的用户输入的形式。**Standard Output (stdout)**指的是命令的正常输出，而**Standard Error (stderr)**指的是命令生成的任何错误消息。Standard Output和Standard Error默认都显示在终端屏幕上。所有这三个组成部分都在图7-1中描绘。

如图7-1所示，每个file descriptor由一个数字表示，stdin由数字0表示，stdout由数字1表示，stderr由数字2表示。虽然所有三个descriptor都对任何命令可用，但并非所有命令都使用每个descriptor。在图7-1中使用的`ls /etc/hosts /etc/h`命令将Standard Output（/etc/hosts文件的列表）和Standard Error（指示/...

![](img/c27875544958897d817484d558c208c8_327_0.png)

Output（/etc/hosts文件的列表）和Standard Error（指示/etc/h文件不存在的错误消息）输出到终端屏幕，如下面的输出所示：

```
[root@server1 ~]# ls /etc/hosts /etc/h
ls: cannot access /etc/h: No such file or directory
/etc/hosts
[root@server1 ~]# _
```

## Redirection

你可以使用BASH shell将Standard Output和Standard Error从终端屏幕重定向到文件系统上的文件。要做到这一点，包括> shell元字符后跟文件的绝对或相对路径名。例如，要将图7-1中使用的命令的Standard Output重定向到名为goodoutput的文件，你在文件descriptor编号（1）后附加重定向符号>以及要重定向Standard Output的文件（goodoutput），如下面的输出所示：

```
[root@server1 ~]# ls /etc/hosts /etc/h 1>goodoutput
ls: cannot access /etc/h: No such file or directory
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_328_0.png)

> 你可以在>元字符后包含一个空格字符，但这不是必需的。

在上面的输出中，Standard Error仍然显示在终端屏幕上，因为它没有被重定向到文件。/etc/hosts的列表没有显示；相反，它被重定向到当前目录中名为goodoutput的文件。如果在运行上述输出中的命令之前goodoutput文件不存在，它会自动创建。然而，如果在重定向之前goodoutput文件已经存在，BASH shell会在执行命令前清除其内容。要查看Standard Output已重定向到goodoutput文件，你可以运行以下命令：

```
[root@server1 ~]# ls -F
Desktop/  goodoutput
[root@server1 ~]# cat goodoutput
/etc/hosts
[root@server1 ~]# _
```

同样，你可以将命令的Standard Error重定向到文件；只需指定file descriptor编号2，如下面的输出所示：

```
[root@server1 ~]# ls /etc/hosts /etc/h 2>badoutput
/etc/hosts
[root@server1 ~]# cat badoutput
ls: cannot access /etc/h: No such file or directory
[root@server1 ~]# _
```
