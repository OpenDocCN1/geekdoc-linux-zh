
# Kali Linux 上 Foremost 的介绍与安装

> 原文：<https://blog.eldernode.com/introducing-install-foremost-on-kali-linux/>

![Introducing and Install Foremost on Kali Linux](img/5d146f83d7bd5305c38a5ba1f8265a19.png)

计算机世界中最困难和复杂的主题之一是数据存储和检索，这是非常专业的领域。我们的信息被无意或有意删除的情况已经发生了很多次，我们时常考虑如何找回这些信息。在许多情况下，我们要么求助维修人员，要么为数据安全而担忧。在下面的教程中，我们将介绍一个工具，通过它你可以自己恢复丢失的信息。这是最重要的工具之一，且属于专有工具。请注意，默认情况下，`foremost` 在 Kali Linux 中即可使用。我们正尝试在 Kali Linux 上进行介绍和安装。你可以访问 [Eldernode](https://eldernode.com/) 提供的包来购买 [Linux VPS](https://eldernode.com/linux-vps/) 服务器。

## 认识 Kali 中的 Foremost

`foremost` 是取证领域的一个强大工具，用于数据恢复和丢失信息恢复。该工具能够根据文件的页眉和页脚以及数据的内部结构检索各种格式的文件。该工具还能够处理图像文件，并且可以轻松处理 `dd`、`safe beach` 和 `encase` 等工具的输出。在本文的后续部分，我们将学习如何在 [Kali Linux](https://blog.eldernode.com/install-and-configure-kali-linux-on-vps/) 上安装 `foremost`。

### Foremost 的作用是什么？

数据恢复成功的关键之一是你没有将新的内容复制到硬盘，也就是所谓的“重写”。假设你的硬盘被无意格式化了，在这种情况下，数据恢复的几率非常高。但是，如果你在格式化后又复制了新内容，再想检索数据，你的机会就会大大降低。因为新的数据集会覆盖先前数据的存储空间，这就是所谓的“重写”。在这种情况下，能够恢复的数据会较少。

`foremost` 工具被设计为忽略文件系统类型，直接读取并复制驱动器部分内容到计算机内存中。它一次读取一段数据，并使用称为“文件雕刻”的过程在内存中搜索与 `foremost` 配置文件中定义的文件头类型相匹配的文件头。当找到一个匹配项时，它将该文件头及其后面的数据写入一个新文件，当找到页脚时停止，或者直到达到文件大小限制。

`foremost` 使用命令行界面，没有可用的图形用户界面选项。它能够恢复特定的文件类型，包括 `jpg`、`gif`、`png`、`bmp`、`avi`、`exe`、`mpg`、`wav`、`riff`、`wmv`、`mov`、`pdf`、`ole`、`doc`、`zip`、`rar`、`htm` 和 `cpp`。

### 如何在 Kali Linux 上安装 Foremost

在前面几节中，我们熟悉了 `foremost` 及其特性，现在该安装它了。要在 Kali Linux 上安装 `foremost`，你可以轻松地运行以下命令：

```
sudo apt-get install foremost
```

注意，通过执行上述命令，`foremost` 及其依赖的其他包也会一并安装。

## 结论

`foremost` 工具是法医领域最强大的工具之一。如前所述，该程序在 Kali Linux 操作系统上默认可用。要运行它，只需转到应用程序部分的“取证”分类，找到该工具；或者直接在终端中输入 `foremost` 命令来调用程序。在本文中，我们尝试对 `foremost` 进行介绍，并指导你在 Kali Linux 上完成安装。
