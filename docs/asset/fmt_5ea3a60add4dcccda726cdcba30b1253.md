
```
Upgrading liblinux-system-virtualization:amd64 liblinux-system-virtualization (0.26.0-ubuntu3.1) 152 kB
Download http://archive.ubuntu.com/ubuntu/pool/main/l/liblinux/liblinux-system-virtualization_0.26.0-ubuntu3.1_amd64.deb 152 kB
Fetched 152 kB in 1s (152 kB/s)
Setting up archives...

Setting up archives... Done
Unpacking liblinux-system-virtualization:amd64 liblinux-system-virtualization (0.26.0-ubuntu3.1)
Setting up liblinux-system-virtualization:amd64 (0.26.0-ubuntu3.1)
Processing triggers for archive (0 not configured)
Processing triggers for archive (0 not configured) Done
```

```
File Edit View Search Terminal
davidhavd-mint
sudo@mint:~$ sudo apt-get update sudo apt-get upgrade
get:1: /archive.ubuntu.com/ubuntu xenial main
get:2: /archive.ubuntu.com/ubuntu-backports [release=xenial] main
get:3: /archive.ubuntu.com/ubuntu-security main
get:4: /archive.ubuntu.com/ubuntu-updates [release=xenial] main
get:5: /archive.ubuntu.com/ubuntu security main
:6: http://mirrors.ubuntu.org/ubuntu/pool/ubuntu-relicts-main
:7: /archive.ubuntu.com/ubuntu-updates [release=xenial] main
:8: /archive.ubuntu.com/ubuntu-security [release=xenial] 102)
Reading package lists...
Reading package lists... Done
Building package list...
Building package list... Done
Reading packages...
Reading packages... Done
Calculating upgrade...
Calculating upgrade... Done
Checking process...
Checking process... Done
0 packages up to date. 0 new to be installed, 0 to be removed and 0 failed to install
```

## 终端 VS 更新管理器

为什么使用终端？Linux 上安装应用程序和程序有多种方法。你可以选择图形界面路线使用软件管理器，也可以使用终端。通常，终端对安装的软件提供更好的控制，有时你没有选择。通过使用终端，`apt-get`会处理版本之间的依赖关系，因此你可以保持最新。从用户角度来说，如果你在寻找最新的软件包，最好使用软件管理器。

## 通过终端安装应用 - 第一部分

### 命令行安装

- **第 1 步** 从终端安装应用程序通常相对简单。首先，你需要确保系统是最新的。在终端中执行此操作并输入：`sudo apt-get update && sudo apt-get upgrade`。输入你的密码并接受任何更新。
- **第 2 步** 正如所示，使用 `sudo apt-get update`/`sudo apt-get upgrade` 等命令可以升级系统中已安装的软件。你想安装更多应用吗？事实证明这非常简单。首先，你需要一个要安装的应用，我们用 Stella 吧。输入：`sudo apt-get install`。
- **第 3 步** 你需要输入 y 来确认安装，这将占用约 5.5MB 的存储空间。Stella 安装完成后，你可以看到 Mint 在菜单中自动生成了“游戏”类别以及快捷方式。
- **第 4 步** 有时在安装软件时，你需要添加应用的仓库（Repository）。仓库（简称 repo）就是存放软件的远程服务器，以及它所有的依赖项（它运行所需要的关键库和书籍）。从这里开始：`sudo add-apt-repository ppa:peter-levi/ppa` 按回车添加该 PPA（个人软件包存档）。

```
File Edit View Search Terminal
davidhavd-mint ~ %
$ sudo add-apt-repository ppa:peter-levi for the variety wallpaper changer
More info: https://launchpad.net/~peter-levi/ubuntu/ppa
Press Enter to continue or to cancel.
```

## 通过终端安装应用 - 第一部分

### 步骤 5

这为 Variety 壁纸切换器应用添加了软件仓库，它可以自动更换壁纸。这是一个基于 Ubuntu 的应用程序，可以在 Mint 中运行并安装。现在仓库已安装，输入：`sudo apt-get update` 以更新新信息并将内容添加到包管理器。

### 步骤 6

现在安装 Variety，输入：`sudo apt-get install variety`。按 y 接受并继续安装。安装完成后，你可以更改类型来运行该程序。

```
sudo apt-add-repository ppa:variety/ppa
sudo apt-get update
sudo apt-get install variety

# 如果遇到关于 apt-get-repository 的错误，请安装：
sudo apt-get install software-properties-common
# 然后运行：
sudo apt-add-repository ppa:variety/ppa
sudo apt-get update
sudo apt-get install variety
```

```
Reading package lists ...
Building dependency tree ...
Reading state information ... Done
The following NEW packages will be installed
variety 1.2.1-1 ubuntu-focal [612 KB]
libavcodec58:2.8.18-0ubuntu0.0 [2.1 MB]
libavformat58:5.8.53-0ubuntu0.0 [1.1 MB]
libavscale5:5.8.100-0ubuntu0.0 [1100 KB]
4 new packages will be installed, 4.3 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Unpacking...
Selecting previously selected variety 1.2.1-1 ubuntu-focal (612 KB)
Setting up libavcodec58 (2.8.18-0ubuntu0.0) (2.1 MB).
Setting up libavformat58 (5.8.53-0ubuntu0.0) (1.1 MB).
Setting up libavscale5 (5.8.100-0ubuntu0.0) (1100 KB).
Setting up variety (1.2.1-1 ubuntu-focal) (612 KB).
Variety 1.2.1 is now the version.
```

## 移除应用

除了安装之外，`apt`命令还可以用于移除任何应用，保持系统整洁并释放资源。

### 步骤 1

要卸载并移除 Variety 应用，输入以下内容：`sudo apt-get remove variety`。输入 y 继续卸载应用；同时注意由于移除该应用，你的硬盘上释放了多少空间。
