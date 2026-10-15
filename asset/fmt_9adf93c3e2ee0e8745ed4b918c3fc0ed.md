
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```
[/content]

Wait that's example. Need actual processing.

Let's redo properly.

[content]
| `-U username` | 使用此标志，你可以指定连接到资源时的用户名。如果没有此标志，服务器将使用 `USER` 或 `LOGNAME` 环境变量的内容；如果这些内容为空，则不会向服务器提供用户名。你可以在用户名后加一个百分号 (`%`) 后面紧跟密码，来向服务器发送密码：`-U username%password` |

| `-W workgroup` | 此标志指定连接到服务器时使用的组。 |

| `-T tar options` | 此标志允许你将数据移动到本地 Linux 系统上的 tar 文件中或从中。例如 `-Tx backup.tar` 将文件从 `backup.tar` 恢复到远程服务器，而 `-Tc backup.tar` 创建包含远程服务器上所有文件和目录的 `backup.tar` 文件。 |

举例，让我们根据这些信息构建一个 `smclient` 命令：

```
$ smclient //server/resourcename -U username%password -W workgroup
```

此命令尝试连接到名为 `workgroup` 组的服务器上的 `resourcename`，使用用户 `username` 和密码 `password`。

## 文件资源的可用操作

一旦计算机连接到文件资源，就有许多命令可以来回传输数据。这些命令在表 29.3 中列出。

### 表 29.3: 文件操作命令

| 操作 | 描述 |
| --- | --- |
| `cd directory` | 切换到 SMB 共享资源上的另一个目录。 |
| `del file` | 删除服务器上的指定文件。（你也可以使用 `rm` 命令）。 |
| `dir` | 显示服务器上的当前目录列表。（你也可以使用 `ls` 命令）。 |
| `get file` | 从远程服务器获取指定文件并以相同名称保存到本地系统的当前目录中；可选地，你可以为本地系统上的文件指定不同的名称：`get file localfilename` |
| `lcd directory` | 切换到本地系统上的指定目录。 |
| `mget filemask` | 获取远程服务器上匹配指定文件掩码的所有文件。 |
| `mkdir directory` | 在远程服务器上创建指定的目录。（你也可以使用 `md` 命令）。 |
| `mput filemask` | 将本地目录中匹配指定文件掩码的所有文件放入远程服务器的当前目录中。 |
| `prompt` | 切换多个文件操作（`mput` 和 `mget`）提示的开启和关闭。开启时，用户将收到每个被复制文件的提示。 |
| `put file` | 将本地目录中的指定文件复制到远程服务器，并保持文件名不变；远程服务器上的文件名也可以更改：`put file remotename`。 |
| `quit` | 退出 `smbclient`。（你也可以使用 `exit` 命令）。 |
| `recurse` | 切换多个文件操作（`mput` 和 `mget`）目录递归的开启和关闭。开启时，命令在复制时会搜索当前目录下的所有目录。 |
| `rmdir directory` | 从远程服务器上删除指定的目录。（你也可以使用 `rd` 命令）。 |

让我们来看一些示例：

- 要将本地目录更改为子目录 `foo`，使用命令 `cd foo`。
- 要将远程目录更改为目录 `../foo`，使用命令 `cd ../foo`。

## 打印机资源的可用操作

- 要将本地目录中的文件 `foo` 复制到远程共享并命名为 `newfoo`，使用命令 `put foo newfoo`。
- 要从远程共享的当前目录获取所有以 `.txt` 结尾的文件，使用命令 `mget *.txt`。
- 要在远程共享上创建一个名为 `foo` 的新目录，使用命令 `mkdir foo`。

当你使用 `smclient` 连接到打印机资源时，可以使用以下命令与打印机进行操作：

- `print file` 根据 `printmode` 指定的模式，使用当前资源打印指定的文件。
- `printmode 选项` 根据指定的选项设置打印机模式；可能的选项有图形或文本，其中图形模式表示任何二进制数据。
- `queue` 显示远程打印队列的当前状态。
- `quit` 或 `exit` 退出 `smbclient`。

当然，这操作起来有点笨拙。如果有人想打印一个文本文件，他们不能像通常使用 Unix 打印队列那样直接从创建该文件的应用程序中打印。相反，他们需要用 `smclient` 连接到打印机，然后发出命令 `printmode text`，最后执行 `print filename`。打印更复杂的打印机格式会变得困难。

例如，如果打印机是 PCL 打印机，而软件只生成 PostScript 输出（这在 Unix 世界中很常见）呢？在这种情况下，用户需要打印到一个文件，通过 `gs` 将此文件转换为 PCL，用 `smclient` 连接打印机，设置打印模式，然后打印该文件。

## 使用 smclient

`smclient` 是一个允许你从命令行与 SMB 共享交互的工具。它对于脚本编写以及没有图形界面的用户特别有用。

## 从 Linux 访问 Windows 文件和打印机

从 Linux 访问 Windows 文件和打印机的常用方法是通过 Samba 软件包件。该套件允许你将 SMB 共享挂载为本地目录，并打印到 Windows 托管的打印机上。

`ncpfs` 和 `mars_nwe` 共同提供了最接近完整的 Linux NetWare 解决方案。`ncpfs` 软件包可以从 `ftp.gwdg.de/pub/linux/misc/ncpfs` 获取，而 `mars_nwe` 软件包可以从 `http://www.compu-art.de/download/mars_nwe.html` 获取。虽然大部分文档（尤其是关于 `mars_nwe` 的文档）是德语，但在 `IPX-HOWTO` 中也有良好的说明，该文档可以在 `http://www.linuxdoc.org/HOWTO/IPX-HOWTO.html` 在线查看。

然而，这两个产品都有局限性。例如：

- 两者都仅兼容 NetWare 3.x 的 bindery（目录服务），这意味着你可能只能在 bindery 模拟模式下使用 NetWare 4.x 和 5.x。
- `ncpfs` 与 NetWare 2.x 服务器后兼容。
- `ncpfs` 不支持某些 NetWare 兼容服务器，例如 Windows NT 3.51。

### 展望

在本章中，你学习了如何将 Linux 集成到 Windows 局域网中，实现了 Linux 和 Windows 之间的共享。

在第30章“红帽 Linux 7.1 与 DOS/Windows”中，你将关注今天企业世界的一个重要课题：在 Linux 中运行 DOS 和 Windows 软件的能力。

令人惊讶的是，Linux 能够通过其 `dosemu` 软件支持 DOS 应用。此外，尽管仍处于早期阶段，但正在编写一个名为 Wine 的 Windows 模拟器，能够运行 16 位和 32 位的 Windows 应用。虽然 Wine 尚未准备好企业环境的日常工作工具，但它目前可以运行 Microsoft Word 和其他流行的 Windows 应用。第30章将讨论这些兼容包的功能和用途。

第30章还将介绍 VMware，这是一种商业应用程序，允许你建立一个虚拟机，在其中运行你选择的操作系统，包括几乎任何版本的 Microsoft Windows 和 Linux。

# 第三十章

# 红帽 Linux 7.1 与 DOS/Windows

- 在 Linux 中运行 DOS 应用
- VMware
- 为什么不使用 Wine？

反对将 Linux 作为文字处理等生产力任务的日常操作系统的最大理由之一是 Linux 缺乏此类应用程序。这一论点的问题在于，Linux 本身实际上可以运行大多数 DOS 应用程序。将这一承诺变为真实的两个商业产品是 VMware 和 Win4Lin，后者可以在 Linux 内运行 Microsoft Windows。虽然 Win4Lin 限于 Windows 95/98，但 VMware 可以运行所有版本的 Microsoft Windows（直到2000）。本章将介绍 Linux 版 VMware Workstation 的基础安装。

Linux 支持 DOS 已经有一段时间了，只需少量精力即可在 Linux 下运行许多 DOS 应用程序。此外，目前还有其他努力致力于提供完整的 Windows 兼容性。也许这项工作的领导者是 Wine。秉着真正的 Linux 精神，一个开发者团队承担了将 Wine 作为一种免费提供的、比商业软件包更好的工具的任务，供用户快速将其 Windows 应用移植到 Linux 上。对 DOS 应用的支持是 Linux 中最强的兼容性，并包含在大多数发行版中。在 DoseMu 环境下，可以安装并运行 DOS（包括 DOS 6.2 等版本，甚至是 Windows-95/98 自带的 DOS），然后运行大多数应用程序。当然，这也有局限性，包括影响某些图形和字体操作，但总体而言，运行状况良好。此外，DOS 可以在 X 的独立窗口中运行，使得运行 DOS 程序变得简单。Dosemu 提供的功能包括：

- 支持多个用户同时运行 DOS
