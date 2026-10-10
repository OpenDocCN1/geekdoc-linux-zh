
我们讨论了如何使用 `NTLOADER` 作为 Linux 上的启动加载程序。要做到这一点，首先安装 Windows。然后安装 Linux。通常，大多数 Linux 安装程序都会检测到 Windows 安装并自动为您创建一个 `GRUB` 菜单项。如果没有，您将需要通过编辑您的 `GRUB` 配置文件来手动创建一个菜单项，该文件看起来类似于：

```
title Windows

chainloader (hdx,y) +1
```

我们讨论了如何使用 `NTLOADER` 作为 Linux 上的启动加载程序。要做到这一点，首先安装 Windows。然后安装 Linux。通常，大多数 Linux 安装程序都会检测到 Windows 安装并自动为您创建一个 `GRUB` 菜单项。如果没有，您将需要通过编辑您的 `GRUB` 配置文件来手动创建一个菜单项，该文件看起来类似于：

```
title Windows

chainloader (hdx,y) +1
```

我们讨论了如何使用 `NTLOADER` 作为 Linux 上的启动加载程序。要做到这一点，首先安装 Windows。然后安装 Linux。通常，大多数 Linux 安装程序都会检测到 Windows 安装并自动为您创建一个 `GRUB` 菜单项。如果没有，您将需要通过编辑您的 `GRUB` 配置文件来手动创建一个菜单项，该文件看起来类似于：

```
title Windows

chainloader (hdx,y) +1
```
