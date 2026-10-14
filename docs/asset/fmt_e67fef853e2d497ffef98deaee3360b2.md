
# 步骤 5

你输入的所有命令都以相同的方式运行：你输入命令，包含任何扩展命令用途的参数，然后按回车执行你输入的命令。在终端中输入：`uname` 并按回车。这将显示关于 Mint 的某些系统信息。

# 步骤 8

查看和搜索选项允许你更改终端窗口的大小，当然还可以在终端内搜索任何特定的关键词。

![](img/f8aca09bc266ba3d122c77a820ff023b_46_0.png)

# 步骤 6

在我们输入命令之前，让我们花点看看终端提供了哪些菜单。文件（File）菜单允许你打开一个新的终端，创建一个新的配置文件，在其中你可以更改终端的大小、颜色和行为，添加新标签页并关闭所有当前的活动会话。

# 步骤 9

编辑（Edit）项扩展了配置文件的编辑和大小调整，并允许将其设置为只读（Read Only）模式，这会阻止你在终端中输入任何命令。当你需要永久显示内容时这很好。

![](img/f8aca09bc266ba3d122c77a820ff023b_46_1.png)

# 步骤 7

编辑（Edit）选项允许你在终端和其他源之间复制粘贴命令；如果你想从网页上复制非常长且复杂的命令，这非常方便。它还允许你编辑配置偏好。

最后，帮助（Help）选项显示终端的内容和版本号，或者我们将来简称为终端。内容（Contents）值得快速读一遍，以帮助熟悉终端是如何工作的。

![](img/f8aca09bc266ba3d122c77a820ff023b_46_2.png)

![](img/f8aca09bc266ba3d122c77a820ff023b_46_3.png)

# 通过终端更新 Mint

到目前为止一直在使用盾牌图标启动 Mint 更新管理器来更新系统和当前安装的应用程序、工具和其他元素。然而，你也可以从终端完成整个系统的更新和升级。

## 使用 APT-GET

更新和升级终端你使用 APT（高级软件包工具）是一个强大的命令，并根据其使用组合不同的元素。

- 步骤 1 通过打开一个新的终端，或者如果你已经打开了一个，通过命令清理内容来从干净的状态开始。
- 步骤 3 `apt-get` 用于升级 Mint 以及其他基于 Debian 的发行版。使用 `apt-get` 获取新软件包并更新源列表。升级下载并安装最新版本。要启动升级过程，输入：`sudo apt-get` 然后输入你的密码。
- 步骤 2 输入 `apt-get` 进入终端。这会带来最常用的命令列表，以及该命令作用的简要描述。
- 步骤 4 注意 `sudo` 命令的添加。管理员用户（super User）使用 APT（高级软件包工具）来获取更新。现在使用：`sudo apt-get upgrade`。

```
david@david-mint: $
```

![](img/f8aca09bc266ba3d122c77a820ff023b_47_0.png)

```
david@david-mint: ~ Search

apt 1.2.7 (ubuntu)

(apt-get) [options] command

Reading lists... Done

1 http://archive.ubuntu.com/ubuntu focal [26841 kB]

2 http://archive.ubuntu.com/ubuntu-updates [71522 kB]

3 http://archive.ubuntu.com/ubuntu-security [14522 kB]

Reading package list... Done

Building cache... Done

Reading dependency tree: Done

Reading sources: Done

Reading packages: 15 upgraded, 0 new installed, 0 to remove and 0 not upgrade

15 packages can be upgraded. Run 'apt-get'.
```

```
david@david-mint: ~ Search

apt 1.2.7 (ubuntu)

(apt-get) [options] command

Reading lists... Done

1 http://archive.ubuntu.com/ubuntu focal [26841 kB]

2 http://archive.ubuntu.com/ubuntu-updates [71522 kB]

3 http://archive.ubuntu.com/ubuntu-security [14522 kB]

Reading package list... Done

Building cache... Done

Reading dependency tree: Done

Reading sources: Done

Reading packages: 15 upgraded, 0 new installed, 0 to remove and 0 not upgrade

15 packages can be upgraded. Run 'apt-get'.
```

# 通过终端更新 Mint

- 步骤 5 根据你的更新状态，如果你有任何安装内容，想要应用 `sudo apt-get upgrade` 命令的结果，按 Y 接受。这里发生的是 apt-get 有一些更新需要应用到 Mint，你已经准备好了。
- 步骤 7 有趣的是，根据可用软件包列表，系统现在是最新的。你可以运行一次该过程，检查一切一切正常。总结一下：`sudo apt-get update` 然后输入：`sudo apt-get upgrade`。

```
File Edit View Search Help

davidhaus-mint~

01: /archive.ubuntu.com/ubuntu main

02: /archive.ubuntu.com/ubuntu-updates [182 KB]

03: /archive.ubuntu.com/ubuntu-backports

04: /archive.ubuntu.com/ubuntu-security [182 KB]

05: /archive.ubuntu.com/ubuntu focal-universe

06: /archive.ubuntu.com/ubuntu focal-updates [182 KB]

07: /archive.ubuntu.com/ubuntu focal-universe [182 KB]

08: /archive.ubuntu.com/ubuntu focal-security

09: /archive.ubuntu.com/ubuntu focal-updates [182 KB]

10: /archive.ubuntu.com/ubuntu focal-security

11: /archive.ubuntu.com/ubuntu focal-universe [182 KB]

12: /archive.ubuntu.com/ubuntu focal-updates [182 KB]

13: /archive.ubuntu.com/ubuntu focal-security

14: /archive.ubuntu.com/ubuntu focal-universe [182 KB]

15: /archive.ubuntu.com/ubuntu focal-updates/focal-updates [182 KB]

16: /archive.ubuntu.com/ubuntu focal-security

17: /archive.ubuntu.com/ubuntu focal-universe [182 KB]

18: /archive.ubuntu.com/ubuntu focal-updates [182 KB]

19: /archive.ubuntu.com/ubuntu focal-security

20: /archive.ubuntu.com/ubuntu focal-universe [182 KB]

21: /archive.ubuntu.com/ubuntu focal-updates [182 KB]

22: /archive.ubuntu.com/ubuntu focal-security

23: /archive.ubuntu.com/ubuntu focal-universe [182 KB]

24: /archive.ubuntu.com/ubuntu focal-updates [182 KB]

25: /archive.ubuntu.com/ubuntu focal-security

26: /archive.ubuntu.com/ubuntu focal-universe [182 KB]

27: /archive.ubuntu.com/ubuntu focal-updates [182 KB]
```
