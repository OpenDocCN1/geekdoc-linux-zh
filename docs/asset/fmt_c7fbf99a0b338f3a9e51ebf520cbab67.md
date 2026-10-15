
代码清单 7.2 在不同的系统上，相同的命令提供略有不同的详细信息，尽管基本信息保持不变。

## 使用 df 查看文件系统

如果你习惯于 Windows 或 Macintosh（OS X 之前）操作系统，你可能习惯于拥有单独的硬盘驱动器（Windows 用户的`C:`、`D:`、`E:`，或 Mac 的真实名称），它们只是不同的存储空间。在 Unix 系统中，不同的存储空间被嫁接在整体树结构上——附加到已有的结构上，没有任何明确的区分来指示实际磁盘驱动器位于何处。例如，如果你在 Windows 计算机上有一个文件夹，你知道其中的所有子文件夹和文件都位于同一硬盘驱动器上。在 Unix 中，一切都位于根目录内，但任何不同的目录都可能位于不同的物理硬盘驱动器上。你可以把它想象成在人造圣诞树上嫁接一个新的分支。

这些被嫁接的存储空间称为文件系统。特别是如果你正在运行一个 Unix 系统（而不是仅仅使用它），你可能需要找出正在使用的文件系统（在技术术语中称为已挂载到系统），它们有多少空间，以及它们连接到 Unix 系统的位置（或其挂载点在哪里）。你可以使用`df`找到这些信息，如代码清单 7.3 和 7.4 所示。

如果你是系统管理员，你可以使用这些信息来帮助诊断系统出现的问题。如果你是好奇心高于平均水平的普通用户，你可以使用这些信息来满足你的好奇心或提醒系统管理员注意问题。例如，如果你在使用特定程序时遇到奇怪的错误或不可预测的结果，使用`df`可能会显示`/home`文件系统已满，或者你可能没有你认为已安装并挂载的`/dev/cdrom`文件系统。嗯！

### 提示

- 使用`df -k /home`确保使用情况以 1 Kbyte 块报告，而不是 512 字节块。添加`-k`标志还将确保你获得与代码清单 7.3 中所示类似的输出。

- 使用`df -h`获取“人类可读”的输出。这适用于大多数命令（例如`ls`）输出的边际可读文件信息。

- 你可以使用`df`指定特定目录来获取包含该目录的文件系统的状态报告。例如，你可能会使用`df /usr/local/src`来找出该目录挂载在何处以及其上有多少可用空间。

```
xmision- df
/               (/dev/dsk/c0t0d0s0): 154632 blocks      71721 files
/usr            (/dev/dsk/c0t3d0s0): 225886 blocks      144820 files
/proc           (/proc          ): 0 blocks             7830 files
/dev/fd         (fd             ): 0 blocks             0 files
/var            (/dev/dsk/c0t1d0s0): 1001142 blocks      962598 files
/tmp            (swap           ): 123682             95277 files
/usr/local      (/dev/dsk/c0t1d0s5): 630636 blocks      457211 files
/archive        (/dev/dsk/c0t1d0s3): 1180362 blocks      1789487 files
/var/mail       (mail.xmission.com:/var/mail): 2776576 blocks 143385 files
/home           (krunk1.xmission.com:/home): 20091072 blocks 13066932 files
/.web           (krunk1.xmission.com:/.web): 1019408 blocks 470095 files
/var/mail/lists (lists.xmission.com:/var/mail/lists): 293744 blocks 89732s
xmision-
```

代码清单 7.4 该大型 ISP 的文件系统要复杂得多。

## 使用 du 确定磁盘使用情况

另一个你可以获取的信息是 Unix 系统中磁盘空间的使用情况。你可以使用`du`来做到这一点，如代码清单 7.5 所示：

在 shell 提示符下，输入`du`。如代码清单 7.5 所示，你将获得有关当前目录以及所有子目录的磁盘使用信息。数字通常以 1 Kbyte 块为单位进行测量（如`df`所述）。你实际上可以通过使用`du -h`来读取输出。

### 提示

- 如果你在一个执行磁盘空间配额的系统上（大多数 ISP 都是如此），你可以找出你的配额是多少以及你离达到配额有多近。只需在 shell 提示符下输入`quota -v`即可。

- 你可以使用`du`加上路径名来检查单个目录或子目录中的磁盘使用情况（参见代码清单 7.6）。`du`会在打印结果时按子目录汇总使用情况。

- 使用`du -s`，可选择指定目录，只打印所用空间量的摘要。

```
[ejr@hobbes ejr]$ du
2 ./Mail
1 ./nsmail
1 ./netscape/cache/0F
3 ./netscape/cache/1A
22 ./netscape/cache
1 ./netscape/archive
172 ./netscape
1 ./Projects
28 ./wprc
3 ./axhome
5 ./groups
1 ./manipulate/empty
154 ./manipulate
1 ./mail
1 ./unixvqs/ch6
2 ./unixvqs
6 ./dupgroups
255 ./compression/Folder
670 ./compression/temp/BackupFolder
1921 ./compression/temp
670 ./compression/BackupFolder
4657 ./compression
5 ./clean
1 ./elm
15 ./editors
5619 .
[ejr@hobbes ejr]$
```

代码清单 7.5 `du`命令会详尽地报告当前目录及其子目录中的磁盘使用情况。

```
[ejr@hobbes ejr]$ du /home/ejr/compression
255 /home/ejr/compression/Folder
670 /home/ejr/compression/temp/BackupFolder
1921 /home/ejr/compression/temp
670 /home/ejr/compression/BackupFolder
4657 /home/ejr/compression
[ejr@hobbes ejr]$
```

代码清单 7.6 使用`du`并指定目录名可以得到更有针对性的结果。

## 使用 file 查找文件类型

如果你来自 Windows、Macintosh 或 DOS 背景，你可能习惯于访问文件并能够看到它们是什么类型的文件——HTML 文件、GIF、文档或任何其他类型。在 Unix 中，通过列出文件或显示目录内容通常无法判断文件类型。这时`file`就派上用场了，如代码清单 7.7 所示。

在 shell 提示符下，输入`file`，后跟路径（如果必要）和文件名，例如`file /usr/bin/pico`。你会看到与代码清单 7.7 中类似的输出。

### 提示

- 并非所有文件都具有使`file`正常工作的“魔术”信息，但大多数都有。在没有的情况下，你会得到一个最佳猜测的响应，就像代码清单 7.7 中的第二个响应一样。不幸的是，你无法通过查看来判断它是确定信息还是猜测，但如果它很简略（如第二个响应），请谨慎对待。

```
[ejr@hobbes ejr]$ file /usr/bin/pico
/usr/bin/pico: ELF 32-bit LSB executable,
  Intel 80386, version 1, dynamically ld
[ejr@hobbes ejr]$ file temp.htm
temp.htm: ASCII text
[ejr@hobbes ejr]$
```

代码清单 7.7 `file`命令提供了有关特定文件中包含何种数据的有用信息。

## 使用 finger 查找用户信息

使用`finger`命令，你可以查出当前谁登录到 Unix 系统，以及他们在做什么、登录了多久，以及其他一些窥探性的、可能与你无关的信息（代码清单 7.8）。

### 使用 finger 查找谁已登录：

1. `finger`

   在 shell 提示符下，输入`finger`以查看还有谁登录到系统并获取有关他们的一些信息（代码清单 7.8）。

2. `finger @stc.org`

   输入`finger @`，后跟主机名（在本例中为 stc.org）以查找另一个主机上谁已登录。
