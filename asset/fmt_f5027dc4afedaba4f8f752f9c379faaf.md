
`Kespueduel` 包含许多配置选项，用于设置燃料使用情况、飞船速度、重力引力等（见图 24.3）。

图 24.3 `Kespueduel` 包含了速度、重力、能量等配置选项。

![](img/ba933c244f3be8993f8191427d25c74c_124_0.png)

一个名为 `xinvaders` 的 Linux 版《太空入侵者》，包含在 CD 盘的 `/Source/Games/Arcade` 源目录中。它不需要 `KDE` 或 `Gnome`，但可能需要一些编程知识才能使其正确编译。祝你好运。

![](img/ba933c244f3be8993f8191427d25c74c_124_1.png)

## 在 Linux 上玩飞行模拟器

`Sabre` 飞行模拟器在 Linux 中提供了非常真实且令人震撼的飞行体验。你可以从许多不同的场景和飞机中进行选择，并可以使用演示模式观看模拟器飞行。

一个专门用于 `Sabre` 的网站位于 `http://sabre.cobite.com/`，提供了软件和游戏玩法的用户指南及更新。该网站表示，目前 `Sabre` 团队正在开发朝鲜战争时期的战斗机，例如 `F-86` 天雷式战斗机和 `MiG-15`。`Sabre` 菜单中还可以选择 `F-84` 闪电式和 `F-51` 野马式。如果你喜欢，还可以与中队一起享受飞行。

`Sabre` 位于 CD 盘的 `/Source/Games/Arc`。`Sabre` 不是一个 `X Window` 程序。它利用底层的图形工具（`svg` 库）创建在视觉和感受上与基于 `DOS` 的游戏相似的内容。在使用 `Sabre` 之前，你需要编译它。这里显示了基本命令，尽管在执行这些某些命令后会出现大量的文本。你可能还想在解压归包后在 `Sabre` 目录中运行 `INSTALL` 文件。

![](img/ba933c244f3be8993f8191427d25c74c_125_0.png)

```
$ cp /mnt/cdrom/Source/Games/Arcade/sabre-0_2_4.tar.gz /home/nwell/part6

$ cd /home/wells/part6

$ tar xvzf sabre-0_2_4.tar.gz

$ cd sabre-0.2.4

$ ./configure

$ make

$ make install

$ /usr/local/bin/sabre
```

你可能需要以 `root` 身份登录以执行 `install` 命令。一旦你编译并运行了 `Sabre`，其结果将令人印象深刻（见图 24.4）。

另一个值得尝试的飞行模拟器是 `FlightGear`。该项目包含一个充满场景和其他图形的独立包，以及一个文档包。

`FlightGear` 需要一张 3D 显卡。构建它的完整源码包位于 CD 盘的 `/Source/Games/FlightGear`。

![](img/ba933c244f3be8993f8191427d25c74c_125_1.png)

## 图 24.4 `Sabre` 在 Linux 上提供了令人印象深刻的飞行模拟体验。

![](img/ba933c244f3be8993f8191427d25c74c_126_0.png)

与 `Sabre` 一样，由飞行模拟器爱好者创建的网站位于 `http://www.flightgear.org/`，拥有完整的文档、大量的图像以及邀请其他爱好者参与开发的邀请。

## 运行游戏

许多街机游戏使用不同的主题，在游戏场上移动、捕捉物体、吃东西等。其中最广名户晓的是吃豆人（`Pacman`）。Linux 上有多个版本的吃豆人供选择。`pacman` 程序（用于 `KDE`）与原始街机游戏非常相似（见图 24.5）。然而，它包含了幽灵组、水果和许多小点，并遵循了吃豆人中使用的原始游戏模式。

![](img/ba933c244f3be8993f8191427d25c74c_126_1.png)

## 图 24.5 `Pacman` 是适用于运行 `KDE` 系统的吃豆人克隆版。

![](img/ba933c244f3be8993f8191427d25c74c_127_0.png)

`Pacman` 位于 CD 的 `/Binaries/Games/`。按照以下步骤将其安装在你的 `Red Hat` 6 系统上：

```
$ cp /mnt/cdrom/binaries/pacman/pacman-binary.tgz /home/nwell/part6

$ cd /home/nwells/part6

$ tar xzvf pacman-binary.tgz

$ cd pacman-0.2.4

$ make install
```

你可能需要以 `root` 身份登录以使用 `make` 命令。会出现许多屏幕文本。

## 街机上的 LINUX

许多街机游戏使用不同的主题，在游戏场上移动、捕捉东西、吃东西等。其中最广为人知的之一是吃豆人。Linux 有多个版本的吃豆人可用。`pacman` 程序（用于 `KDE`）与原始街机游戏惊人地相似（见图 24.5）。然而，它包含了幽灵组、水果以及许多小点，并使用了吃豆人中使用的原始游戏模式。

![](img/ba933c244f3be8993f8191427d25c74c_126_1.png)

## 街机上的 Linux

你可能需要以 `root` 身份登录才能使用 `install` 命令。随着游戏的所有组件安装到你的系统上，会出现许多满屏文本的界面。此归包是为 `Red Hat` 6 设计的。如果你使用的是其他发行版，则应该从源码包编译游戏。文件安装完成后，启动游戏：

```
$ kespueduel
```

`Kespueduel` 包含许多配置选项，用于设置燃料使用情况、飞船速度、重力引力等（见图 24.3）。

图 24.3 `Kespueduel` 包含了速度、重力、能量等配置选项。

![](img/ba933c244f3be8993f8191427d25c74c_124_0.png)

一个名为 `xinvaders` 的 Linux 版《太空入侵者》，包含在 CD 盘的 `/Source/Games/Arcade` 源目录中。它不需要 `KDE` 或 `Gnome`，但可能需要一些编程知识才能使其正确编译。祝你好运。

![](img/ba933c244f3be8993f8191427d25c74c_124_1.png)

## 在 Linux 上玩飞行模拟器

`Sabre` 飞行模拟器在 Linux 中提供了非常真实且令人震撼的飞行体验。你可以从许多不同的场景和飞机中进行选择，并可以使用演示模式观看模拟器飞行。

一个专门用于 `Sabre` 的网站位于 `http://sabre.cobite.com/`，提供了软件和游戏玩法的用户指南及更新。该网站表示，目前 `Sabre` 团队正在开发朝鲜战争时期的战斗机，例如 `F-86` 天雷式战斗机和 `MiG-15`。`Sabre` 菜单中还可以选择 `F-84` 闪电式和 `F-51` 野马式。如果你喜欢，还可以与中队一起享受飞行。

`Sabre` 位于 CD 盘的 `/Source/Games/Arc`。`Sabre` 不是一个 `X Window` 程序。它利用底层的图形工具（`svg` 库）创建在视觉和感受上与基于 `DOS` 的游戏相似的内容。在使用 `Sabre` 之前，你需要编译它。这里显示了基本命令，尽管在执行这些某些命令后会出现大量的文本。你可能还想在解压归包后在 `Sabre` 目录中运行 `INSTALL` 文件。

![](img/ba933c244f3be8993f8191427d25c74c_125_0.png)

```
$ cp /mnt/cdrom/Source/Games/Arcade/sabre-0_2_4.tar.gz /home/nwell/part6

$ cd /home/wells/part6

$ tar xvzf sabre-0_2_4.tar.gz

$ cd sabre-0.2.4

$ ./configure

$ make

$ make install

$ /usr/local/bin/sabre
```
