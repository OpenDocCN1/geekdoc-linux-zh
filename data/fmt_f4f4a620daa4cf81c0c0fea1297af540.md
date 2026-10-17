
一旦完成这些操作，我们将编辑 Grub 的配置文件 `/boot/menu.lst`，并对其进行定制。这项操作之所以复杂，是因为由于等因素，特别是涉及到硬盘磁盘的命名法变化；为了识别特定文件所在的设备，我们将在进入 Grub 命令行模式后，使用 `grub` 使用 `find` 命令。因此，例如，如果我们想找到一个必须在 Grub 配置文件中指定位置的文件（例如 `/vmlinuz`），应该按照以下步骤操作：

```
brau:-# grub version 0.91 (640K lower / 3072K upper memory) [ Minimal BASH-like line editing is supported. For the first word, TAB lists possible command completions. Anywhere else TAB lists the possible completions of a device/filename. ] grub find /vmlinuz (hd2,0)
```

Grub 还有许多命令，要获取这些列表，只需在命令行中按 Tab 即可获得以下内容：

```
grub> Possible commands are: blocklist boot chainloader cmp color configfile deb device displayamem end findstest geometry halt help imps robe inittrd installprobe kernel lock keepactive md5crypt moduleno unzip partition partytype password pause quit read reboot root notoverify savede fault setkey setup terminal testload testvbe uppermem vbeprobe grub>
```

要获取任何特定命令的详细信息，我们都必须在键盘上输入 `help` 后紧跟命令名。处理我们的 Grub 配置文件 `/boot/menu.lst` 的良好方法是在不同的 tty 中打开一个新会话，并在处理 Grub 界面时逐渐修改该文件。

一旦我们完成了配置文件的编辑，并在驱动器中插入一个空磁盘，我们应该使用键盘输入以下行，将 `x` 替换为硬盘编号，将 `y` 替换为相应的分区：

```
grub> install (hdX,Y)/boot/stage1 d (fd0) (hdX,Y)/boot/stage2 p (hdX,Y)/boot/menu.lst
```

通过上述行，我们传输了 MBR Grub 及其命令行界面（stage2）的信息。

正如我们看到的，Grub 相当复杂，这就是为什么我们认为非常有必要阅读 http://www.gnu.org/software/grub 的文档。

## 9.3. 软件包系统

现在我们将分析并学习使用 Debian 软件包系统。在接下来的小节中，我们将学习如何配置数据库、如何使用它、安装不同的软件包以及更新它们。这里有许多实现相同结果的方法，有两个主要目标：首先是读者能够选择使用哪一种，其次是让读者在其中一种方法失效时总有其他方案。

### 活动

为了全面理解 软件包系统，我们推荐：

- APT HOWTO: http://www.debian.org/doc/manuals/apt-howto/index.html
- http://www.debian.org/doc/manuals/debian-faq/ch-pkgbasics.en.html
- http://www.debian.org/doc/manuals/debian-faq/ch-pkgtools.en.html
- `apt`, `apt-cache`, `apt-get`, `sources.list`, `dpkg` 和 `dselect` 的 man手册

为了方便阅读，我们可以等到配置好打印机后学习打印 man 手册。

### 9.3.1. /etc/apt/sources.list

`/etc/apt/sources.list` 文件是 Debian 软件包系统配置的核心。它是一个文本文件，就像 UNIX 类型系统中大多数配置文件一样，我们可以手动编辑它，或使用某些为此目的设计的工具。该文件的内容在很大程度上取决于互联网连接的速度（假设我们有连接）。然而，在我们修改文件后，我们永远不要忘记以 root 身份运行以下命令：

```
brau:/etc/apt# apt-get update
```

如果我们忽略了这一点，那么我们所做的任何更改都不会产生任何影响。

此文件的每一行都引用一个包源，包之间用空格分隔。首先，我们必须指定该源是二进制包 `deb` 还是源码 `deb-src`。第二个字段用于指定如何访问这些包：CD-ROM、`http`、`ftp`，后跟地址。剩余的字段指的是我们希望通过此行访问的包类型。

在理想情况下，我们应该有一个快速的互联网连接。这可能允许我们通过互联网进行基础系统的安装，并让我们获得最新版本的软件包。此外，这是处理软件包最舒适的方式，因为我们甚至不需要担心插入正确的 CD 来执行安装。

然而，在做任何事情之前，我们必须确保 `/apt/sources.list` 的内容是正确的。例如：

```
deb http://ftp2.de.debian.org/debian/debian/ stable main non-free contrib deb-src

http://ftp2.de.debian.org/debian/debian/ stable main non-free \ contrib deb

http://non-us.debian.org/debian/non-US stable/non-US main \ contrib non-free deb-src

http://non-us.debian.org/debian/non-US stable/non-US \ contrib non-free deb

http://security.debian.org/updates main contrib-freefree
```

上述所有地址都是官方的；换句话说，它们是 Debian 认可的。除了这些源，我们还可以使用非官方的包；仅仅因为它们是非官方的，并不意味着它们的质量不足以将它们包含在我们的配置文件中。查找这些包位置信息的良好地址是 http://www.aptget.org。

一旦我们编辑并保存了该文件，就应该运行 `apt-get update` 命令；几分钟后，软件包系统将配置其数据库并在屏幕上显示已执行的操作，之后我们就可以访问新包了。

如果我们没有互联网连接，或者连接太慢，我们不应该犹豫使用发行版的 CD/DVD 集合来安装不同的包。如果在到目前为止的安装过程中我们还没有插入 CD 或 DVD，现在是插入它们的时候了。我们应该将第一张 CD-ROM/DVD 放入驱动器中，并使用 `apt-cdrom add` 命令将其内容包含在数据库中：

```
brau:/etc/apt# apt-cdrom add Using CD-ROM mount point /CD-ROM/ . . . Repeat this
```
