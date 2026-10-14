

## 25.3.3 卸载软盘

使用 umount 卸载软盘，将其挂载的目录名称作为参数使用。

- 要卸载挂载在 `/floppy` 上的软盘，请输入：

```
$ umount /floppy RET
```

*NOTE:* 如果你的当前工作目录，即你所在的目录，在该磁盘的目录树中的某个位置，则无法卸载磁盘。(34) 在这种情况下，尝试卸载磁盘会给出 `/floppy` 文件系统正在使用的错误；切换到不在 `/floppy` 目录树中的其他目录，然后你就可以卸载磁盘了。

有时在你卸载软盘时，软盘驱动器的灯会亮起，并在卸载后保持亮起几秒钟。这是因为 Linux 有时会将对文件的更改保存在内存中，然后再写入磁盘；它正在确保软盘上的文件是最新的。只需等待灯熄灭后再从驱动器中取出软盘即可。

## 25.4 CD-ROM

与软盘一样，在系统上使用数据 CD（光盘）之前，必须先将其挂载到一个空目录上。然后在从 CD-ROM 驱动器弹出 CD 之前，必须先从该目录卸载它（你也可以使用软件弹出光盘----参见章节 Ejecting an Audio CD）。

*NOTE:* 要使用音频 CD，请参见 Audio Compact Discs。

### 25.4.1 挂载 CD-ROM

### 25.4.2 卸载 CD-ROM

## 25.4.1 挂载 CD-ROM

要将 CD-ROM 挂载到系统上，请使用带有 `/cdrom` 选项的 mount。(35)

- 要将 CD-ROM 挂载到系统上，请输入：

```
$ mount /cdrom RET
```

此命令使 CD-ROM 的内容可从 `/cdrom` 目录树访问。你可以使用任何 Linux 文件命令操作 CD-ROM 上的文件和目录，但你无法写入 CD-ROM——CD-ROM 格式是只读的，因此你可以读取光盘但不能写入。

与 `/floppy` 目录一样，使用 `/cdrom` 目录是一种标准做法且方便，但不是必需的——你可以将磁盘挂载到任何你喜欢的空目录中。（例如，你甚至可以将 CD-ROM 驱动器的光盘挂载到 `/floppy`，并将软盘挂载到 `/cdrom`，但谁会这么做呢！）

要将 CD-ROM 挂载到特定目录，请使用 mount 并给出作为参数的 CD-ROM 驱动器在 `/dev` 中的设备文件名，以及要挂载到的目录名。此目录必须已存在于文件系统中，并且必须为空。如果不存在，请先使用 mkdir 创建它（参见章节 Making a Directory）。

大多数 Linux 系统都设置成第一个 CD-ROM 驱动器的设备文件为 `/dev/cdrom`，但设备文件的名称可能不同，特别是如果你有 SCSI CD-ROM 驱动器。

- 要将 CD-ROM 驱动器中的光盘挂载到 `/usr/local/share/clipart` 目录，请输入：

```
$ mount /dev/cdrom /usr/local/share/clipart RET
```

CD-ROM 驱动器中光盘的内容将可通过 `/usr/local/share/clipart` 目录树访问，然后你就可以像使用其他任何文件一样使用 CD-ROM 上的文件和目录。例如：

The Linux Cookbook: Tips and Techniques for Everyday Use:

- 要浏览 CD-ROM 内容的目录树图，请输入：

```bash
$ tree /usr/local/share/clipart | less RET
```

- 要切换到 CD-ROM 的根目录，请输入：

```bash
$ cd /usr/local/share/clipart RET
```

- 要列出 CD-ROM 根目录的内容，请输入：

```bash
$ ls /usr/local/share/clipart RET
```

## 25.4.2 卸载 CD-ROM

使用 umount 卸载 CD-ROM；给出其挂载的目录名称作为参数。

- 要卸载挂载在 `/cdrom` 上的 CD-ROM 驱动器中的光盘，请输入：

```bash
$ umount /cdrom RET
```

> **NOTE:** 与卸载任何类型的文件系统一样，请确保光盘上的文件没有被使用，否则你将无法卸载它。例如，如果 shell 中的当前工作目录位于 `/cdrom` 目录树内部，你将无法在切换到其他目录之前卸载 CD-ROM。

