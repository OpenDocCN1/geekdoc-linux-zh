

package in the control file described previously. Sure enough, this is exactly where this metadata has been extracted.

当然，输出的大部分由之前示例中省略的长格式描述组成。还有一些可能感兴趣的其他字段，包括“Original-Maintainer”或在 Debian 中打包该系统的人，“Maintainer”或负责处理有关该软件包的问题或疑问的人员或团体，以及大小和哈希值（如 MD5Sum、SHA1 和 SHA256），它们描述了识别特定版本的软件包是否已正确下载且未被修改的方法。

不带参数调用时，Aptitude 还可以为用户提供基于 Curses 的文本界面，允许更交互地浏览所有可用的软件包。对于熟悉 Synaptic 的用户，可以将其视为 Synaptic 界面的文本版本。在此模式下，许多搜索结果可以通过箭头键进行导航，并且可以对不同的应用程序进行“标记”以便安装。

在结束对搜索和浏览软件包选项的介绍之前，值得指出的是 http://packages.ubuntu.com 网站。该界面让用户可以以与我在此展示的一些工具相似的方式进行搜索，但还提供了几个额外的有用选项。特别是，该网站允许用户在 Ubuntu 的任何软件包中搜索特定文件。通常，用户只能在系统上安装了该软件包的情况下才能够查出哪个软件包“拥有”某个文件。如果例如你需要某个特定的头文件或共享库，而你只知道文件名，你可以在该网站上对 Ubuntu 档案中的所有软件包搜索该文件名。

## 安装和移除

安装和移除软件包是另一项你会经常执行的简单任务。要安装软件包，你可以以类似的方式调用 apt-get 或 Aptitude，不过与搜索不同，用户必须以 root 权限运行才能执行此操作。推荐的做法是使用 sudo 命令。由于在这一节的每个命令前加上 sudo 会很繁琐，我假设用户是 root，虽然用户以 root 登录并不被认为是最佳做法。如果我想安装 most，我只需以 root 身份运行以下命令：

```
# aptitude install most
Reading package lists... Done
Building dependency tree
Reading state information... Done
Reading extended state information
Initializing package states... Done
Writing extended state information... Done
The following NEW packages will be installed:
libslang2(a) most
0 packages upgraded, 2 newly installed, 0 to remove and 0 not upgraded.
Need to get 0B/509kB of archives. After unpacking 1323kB will be used.
Do you want to continue? [Y/n/?] y
Writing extended state information... Done
Selecting previously deselected package libslang2.
(Reading database ... 362131 files and directories currently installed.)
Unpacking libslang2 (from .../libslang2_2.1.3-3ubuntu1_i386.deb) ...
Setting up libslang2 (2.1.3-3ubuntu1) ...
Selecting previously deselected package most.
(Reading database ... 362143 files and directories currently installed.)
Unpacking most (from .../most_5.0.0a-1_i386.deb) ...
Processing triggers for man-db ...
Setting up most (5.0.0a-1) ...

Reading package lists... Done
Building dependency tree
Reading state information... Done
Reading extended state information
Initializing package states... Done
Writing extended state information... Done
```

你可以在上面的命令输出中看到 libslang2 与 most 一起被安装。在这种情况下，Aptitude 看到 most 需要 S-Lang 库，但它尚未安装。Aptitude 提示我确认是否安装额外的软件包（我已批准），下载了两个软件包，然后在我的系统上安装并配置它们。

移除软件包同样简单。如果我决定移除 most，我可以运行以下命令来执行：

```
# aptitude remove most
```

在这种情况下，libslang2 不会被移除（因为我没有要求移除它）。如果我改为尝试移除 libslang2，Aptitude 会提示我并解释说移除 libslang2 还需要移除所有依赖它的软件包——在此系统上那只是 most，但在其他软件包或系统上可能有相当多的软件包。这种类型的依赖管理意味着，例如，用户不应（也无法轻易）移除核心或必要的软件包。额外的“未使用”软件包可以使用命令 apt-get autoremove 移除。

最后，虽然这些示例都使用了 Aptitude，但软件包的安装和移除也可以使用更底层的工具 dpkg 来完成。事实上，在这两种情况下，Aptitude 只是在幕后对下载的软件包文件调用 dpkg。Aptitude——或 apt-get——总会先下载软件包并解决依赖关系，然后再转向 dpkg。如果你已经安装了现有的依赖项，你可以使用 -i 命令并将软件包文件名作为参数，直接用 dpkg 安装一个 DEB。例如，如果我得到一个 most 的 DEB 文件，我可以用如下命令安装它：

```
$ dpkg -i most_5.0.0a-1_i386.deb
```

dpkg 会检查依赖关系，并在缺少依赖时产生错误，但不会自动下载或安装软件包，因为它不包含执行此操作的功能。我可以用命令 dpkg -r most 用 dpkg 卸载 most。

## 操作已安装的软件包

dpkg 提供了数十种查询、搜索和操作已安装软件包的方法。它包含有关软件包的信息数据库
