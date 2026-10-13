
```
appink      lxproxy     startx      xdm         xmodmap     xsm
dm          prefinfo    sysconfig   Xftconfig.README-OB SOLETE   xorg.conf
gdm         proxy.mgr   twm         xinit       Xresources
gdm         serverconfig x
```

*注意：原图像中的表格布局不同，其中 'dm' 和 'gdm' 在第一列，'prefinfo' 和 'proxy.mgr' 在第二列，'startx' 和 'twm' 在第三列，'xdm' 和 'xinit' 在第四列，'xmodmap' 和 'Xresources' 在第五列，'xsm' 在第六列。包含 'sysconfig' 和 'Xftconfig.README-OB SOLETE' 的行跨越多个列。此表示法是简化版本。*

从这个列表（没有颜色）中，你无法分辨条目是文件还是目录。要将目录和文件区分开，请像这样使用带 `-F` 选项的 `ls`：

```
ls -F
```

![](img/9f89727199836b0f871f1745838aa8b2_185_3.png)

![](img/9f89727199836b0f871f1745838aa8b2_185_4.png)

## 160 使用 Linux 命令导航文件系统

这次输出为你提供了更多关于文件类型的线索：

```
aplink/  lbxproxy/  start/here/  xadm/       Xmodmap  xsl/
dm/       prefndm*   ssysconf/  XftConfig.README-OBSSOLETE  xorg.conf
fs/       proxymngr/ 1wm/        xX11/      Xresources
gdm/      serverconfig/ X@      xkbD         xserver/
```

`ls -F` 的输出在目录名称后附加了一个斜杠（`/`）。普通文件名按原样显示。附加在文件名后的 `@` 符号（例如，请注意名为 `X@` 的文件）表示该文件是链接到另一个文件的快捷方式（换句话说，该文件名只是引用另一个文件；它是一个快捷方式）。星号（`*`）附加到可执行文件上（例如，参见列表中的 `prefndm` 文件）。Shell 可以运行任何可执行文件。

你可以使用 `-l` 选项查看有关文件和目录的更详细信息：

```
ls -l
```

对于 `/etc/X11` 目录，`ls -l` 的典型输出如下所示：

```
total 76
drwxr-xr-x 2 root root 4096 Mar 11 23:33 apling
drwxr-xr-x 3 root root 4096 May 20 20:19 dm
drwxr-xr-x 2 root root 4096 May 20 19:58 fs
drwxr-xr-x 8 root root 4096 May 20 20:19 gdm
drwxr-xr-x 2 root root 4096 May 20 20:11 lbxproxy
-rwxr-xr-x 1 root root 1166 May 7 00:29 prefndm
drwxr-xr-x 2 root root 4096 May 20 20:11 proxymngr
drwxr-xr-x 2 root root 4096 Mar 11 23:33 serverconfig
drwxr-xr-x 2 root root 4096 May 20 19:58 start/here
drwxr-xr-x 2 root root 4096 May 11 23:33 sysconfig
drwxr-xr-x 2 root root 4096 May 20 20:12 twm
lrwxrwxrwx 1 root root 24 May 20 20:30 X@ -> ../..i/usr/X11R6/bin/Xorg
drwxr-xr-x 2 root root 4096 May 20 20:04 xadm
-rw-r-r-- 1 root root 372 May 7 11:31 XftConfig.README-OBSSOLETE
drwxr-xr-x 3 root root 4096 May 7 11:31 xinit
lrwxrwxrwx 1 root root 27 Mar 20 20:11 xb@ -> ../..i/usr/X11R6/lib/X11/xkb
-rw-r-r-- 1 root root 613 Mar 31 02:10 Xmodmap
-rw-r-r-- 1 root root 2824 May 20 20:53 xorg.conf
-rw-r-r-- 1 root root 492 Mar 31 02:10 Xresources
drwxr-xr-x 2 root root 4096 May 20 20:11 xserver
drwxr-xr-x 2 root root 4096 May 20 20:11 xsm
```

此列表显示了关于每个目录条目的相当多的信息——每个条目可以是文件或另一个目录。查看从右向左的一行，你会发现最右边的列显示目录条目的名称。名称之前的日期和时间显示了该文件最后一次修改的时间。日期和时间的左边是文件的大小，单位为字节。

文件的组名和所有者出现在显示文件大小的列的左侧。再往左的数字指示指向该文件的链接数。

（*链接* 就像 Windows 中的快捷方式。）最后，最左边的列显示文件的权限设置，它决定了谁可以读取、写入或执行该文件。

最左边列的第一个字符具有特殊含义，如下列表所示：

- 如果第一个字符是 `l`，则该文件是*符号链接*（快捷方式），指向另一个文件。
- 如果第一个字符是 `d`，则该文件是一个目录。
- 如果第一个字符是破折号（`-`），则文件是普通文件。
- 如果第一个字符是 `b`，则文件表示块设备，例如磁盘驱动器。
- 如果第一个字符是 `c`，则文件表示字符设备，例如串行端口或终端。

在第一个字符之后，最左边的列显示一串九个字符，当每个字符都存在时，它们表现为 `rwxrwxrwx`。每个字符指示特定的权限。字母位置的连字符（`-`）指示对该文件的特定操作没有权限。将这些九个字母视为三组三个字母（`rwx`），解释如下：

- 最左边的 `rwx` 组控制文件所有者的*读取*、*写入*和*执行*权限。换句话说，如果你在此位置看到 `rwx`，文件的所有者可以读取（r）、写入（w）和执行（x）该文件。字母位置的连字符表示没有权限。但是字符串 `rw-` 表示所有者具有读取和写入权限，但没有执行权限。虽然可执行程序（包括 shell 程序）通常具有执行权限，但目录将执行权限视为等同于*使用*权限——用户必须在目录上具有执行权限，然后才能打开并读取目录的内容。
- 中间的三个 `rwx` 字符控制属于该文件组的任何用户的读取、写入和执行权限。
- 最右边的 `rwx` 字符组控制所有其他用户（统称为*世界*）的读取、写入和执行权限。

因此，权限设置为 `rwx------` 的文件仅可由文件所有者访问，而权限设置 `rwxr--r--` 使文件可被世界（所有用户）读取。

`ls` 命令的一个有趣特性是它不会列出任何以句点开头的文件。要查看这些文件，你必须使用带 `-a` 选项的 `ls` 命令，如下所示：

```bash
ls -a
```

在你的主目录中尝试这条命令（然后将结果与你未使用 `-a` 选项时所看到的内容进行比较）：

- 1. **输入 `cd` 切换到你的主目录。**
- 2. **输入 `ls -F` 查看主目录中的文件和目录。**
- 3. **输入 `ls -aF` 查看所有内容，包括隐藏文件。**

大多数 Linux 命令接受单字符选项，每个选项前都有一个减号（可以将此符号视为连字符）作为前缀。当你想要使用多个选项时，输入一个连字符并将选项字母*串联*（拼接）在一起，依次排列。因此，`ls -al` 等价于 `ls -a -l` 以及 `ls -l -a`。

![](img/9f89727199836b0f871f1745838aa8b2_188_0.png)

### 用于更改权限和所有权的命令

你可能需要更改文件的权限设置以保护它免受他人影响。使用 `chmod` 命令来更改文件或目录的权限设置。

为了有效使用 `chmod`，你必须指定权限设置。一种好方法是将表 3-4 中各列的字母按照所示顺序（谁/操作/权限）串联起来。

*注意：* 你只从每一列使用单个字符——括号中的文本仅用于解释。

**表 3-4 文件权限的字母代码**

| *谁* | *操作* | *权限* |
|---|---|---|
| u (用户) | + (添加) | r (读取) |
| g (组) | - (移除) | w (写入) |
| o (其他人) | = (分配) | x (执行) |
| a (所有) | s (设置用户 ID) | |

