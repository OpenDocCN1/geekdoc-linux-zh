
我已经提到过救援操作菜单中的“Reinstall GRUB boot loader”选项。这会将 GRUB 重新安装到你选择的磁盘或分区上，但有时 GRUB 本身已安装，但其配置文件丢失或损坏。当这种情况发生时，启动时你可能看不到 GRUB 菜单，什么都看不到。要修复此问题，请选择菜单选项在你的根分区内执行一个 shell。进入后，运行

```bash
update-grub
```

此选项将根据你可用的内核创建一个新的 `/boot/grub/grub.cfg` 文件。完成后，你可以输入 `exit` 返回主菜单并重新启动系统。

## Repair the Root File System

通常救援光盘会尝试挂载根文件系统（如果可能）。如果它能够挂载根文件系统，那么你将无法卸载它并在其上运行 `fsck` 等工具。当然，如果救援光盘能够挂载文件系统，你现在就不需要对它进行 `fsck` 了，对吧？如果根文件系统已损坏且救援光盘无法挂载它，那么进入安装程序 shell 并运行

```bash
fsck -y /dev/sda1
```

将 `/dev/sda1` 替换为你的根分区的路径。如果 `fsck` 抱怨超级块损坏，请按照 Ubuntu Recovery Mode 下“文件系统损坏”部分中的步骤操作。否则，根据文件系统损坏的程度，你可能会看到 `fsck` 在尝试修复时输出它找到的错误。

除了我上面列出的特定救援步骤外，你应该能够从 GRUB 恢复模式执行所有恢复步骤。只需从恢复操作菜单中选择“Execute a shell in /dev/ubuntu/root”（它会将 `/dev/ubuntu/root` 替换为你选择的根分区）并按照相同的步骤操作即可。

## Ubuntu Desktop Live CD

有一些系统救援操作需要你在服务器之外启动。任何系统映像、根分区 `fsck` 命令，或任何需要卸载 `/` 的情况，你都需要某种救援光盘。虽然我已经提到过如何使用 Ubuntu Server 安装光盘作为救援光盘，但不幸的是你受限于该光盘上的工具。有许多不同的 live CD 提供相同的一套工具，例如 Knoppix 和 DSL，但由于我假设你更可能手头有 Ubuntu Desktop 安装光盘，而且它也可用作 live CD，我讨论了一些可以从光盘上执行的高级恢复技术。

## Boot the Live CD

第一步是启动 live CD 进入标准的 GNOME 桌面。不要担心你的服务器没有复杂的显卡，因为我描述的大部分内容都可以通过命令行完成。

## Add the Universe Repository

一旦 live CD 启动到桌面，你需要将 universe 仓库添加到其软件包仓库列表中。我在这里使用的所有工具都来自 universe 仓库中的软件包，因此要么点击 `System_Administration_Software Sources` 并确保已勾选 Community-maintained Open Source software (`universe`) 选项，要么打开一个终端

`Applications_Accessories_Terminal`，然后以 root 身份使用你喜欢的文本编辑器编辑 `/etc/apt/sources.list` 并将

```
deb http://us.archive.ubuntu.com/ubuntu lucid main restricted
```

改为

```
deb http://us.archive.ubuntu.com/ubuntu lucid main restricted universe
```

当然，如果你运行的是比 Lucid 更新的 live CD，你可能会在这里看到其他名称，因此请根据你的 Ubuntu live CD 进行修改。然后在同一个终端中运行

```
sudo apt-get update
```

以更新可用软件包列表。现在你可以为以下任何救援技巧安装工具。

## 恢复已删除文件

这对我们所有人来说都曾发生过。我想每个系统管理员在职业生涯中都曾不小心删除过错误的文件。很长一段时间我都以为一旦在 Linux 下删除文件就无法恢复，但事实并非完全如此。当你在 Linux 上删除文件时，文件系统会将这些块返回到可用空间。在另一个文件使用这些块之前，旧文件的数据仍然存在并且可能可恢复。关键是在删除文件后尽快停止向该文件系统写入。这样可以降低数据被覆盖的概率。

在此示例中，我假设你已停止包含已删除文件的主机并已启动 Ubuntu live CD。CD 启动后并且你已添加 universe 仓库后，使用软件包管理器安装 `sleuthkit` 软件包或打开终端并输入

```
sudo apt-get install sleuthkit
```

`Sleuth Kit` 是一套取证工具，用于协助调查系统入侵。恢复已删除文件对于取证调查来说非常有价值。

`Sleuth Kit` 为此提供了 `icat` 工具——它类似于 `cat` 命令，只是它接受 inode 作为参数。要恢复此文件，我输入

```
sudo icat -f ext -r -s /dev/sda1 2094 > /home/ubuntu/recovery/shadow
```

如果文件确实可以恢复，命令完成后我将在 `/home/ubuntu/recovery/shadow` 下看到我的 `shadow` 文件的副本。然后我可以从救援盘挂载 `/dev/sda1` 文件系统并从这里恢复 `/etc/shadow`。现在如果你想恢复多个文件，你可以多次运行此命令一次恢复一个文件，也可以编写脚本来为你完成。有许多此类脚本在线上，而以下内容基于最初在 http://forums.gentoo.org/viewtopic-t-365703.html 找到的脚本，我随后对其进行了整理和改进：

```
#!/bin/bash

DISK="/dev/sda1" # disk to scan
RESTOREDIR="/home/ubuntu/recovery" # directory to restore to

mkdir -p "$RESTOREDIR"
cat $1 |
while read line; do
  filetype=`echo "$line" | awk '{print $1}'`
  filename=`echo "$line" | awk '{print $3}'`
  filename=${filename%:*}
  filename=${filename%(}
  filename=`echo "$line" | cut -f 2`

echo "$filename"

if [ $filetype == "d/d" ]; then
  mkdir -p "$RESTOREDIR/$filename"
else
  mkdir -p "$RESTOREDIR/"dirname $filename."
  icat -f ext -r -s "$DISK" "$filenode" > "$RESTOREDIR/$filename"
fi
done
```

将此文件保存到 `/home/ubuntu/restore` 并将 `DISK` 和 `RESTOREDIR` 变量分别更改为要扫描的分区和要恢复到的目录。然后要使用脚本，请赋予其执行权限并以已删除文件的完整列表的路径作为参数运行它：

```
sudo chmod a+x /home/ubuntu/restore
sudo /home/ubuntu/restore /home/ubuntu/recovery/deleted_files.txt
```

脚本将然后系统地遍历 `deleted_files.txt` 文件中的所有文件并尝试将它们恢复到 `RESTOREDIR`。它也会在必要时创建目录，因此完成后你应该在 `RESTOREDIR` 内看到与已删除文件匹配的目录结构。

## 恢复分区表

分区表是硬盘开头 512 字节的区域，即主引导记录中的 64 字节部分。这些 64 字节包含你在磁盘上创建的任何主分区或扩展分区的设置。分区表很容易被视为理所当然。毕竟，要擦除或损坏它确实需要一些努力。话虽如此，只需在错误的驱动器上运行一次 `fdisk` 命令，就可能使服务器的硬盘无法读取。

好消息是，即使分区表被擦除，每个分区的数据仍然在磁盘上。你需要做的只是弄清楚每个分区开始和结束的位置，然后你就可以重建分区表并恢复你的数据。当然，这手动操作起来可能相当困难，但 Linux 有一个名为 `gpart` 的工具（全称 Guess Partition），可以为你完成繁重的工作。

`gpart` 的工作方式是扫描整个磁盘，寻找与某种类型分区开头或结尾相匹配的区域。当它找到这些区域时，它会记录下来然后继续。`gpart` 完成后，它就有了它认为的磁盘的完整分区表。

在介绍如何使用 `gpart` 恢复分区表之前，值得讨论一下 `gpart` 的一些局限性。它主要的局限性在于扩展分区。虽然 `gpart` 在查找主分区方面做得很好，但扩展分区更难识别，因此如果你的磁盘有扩展
