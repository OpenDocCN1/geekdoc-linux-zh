
图 1.3 在你的 Linux 安装光盘上使用 RawWrite 将救援镜像拷贝到 A: 盘。

从救援软盘启动，并将启动分区拷贝到软盘，格式为：

`diff=<Linux partition> of=<name of file> bs=512 count=1`

让我们逐步检查命令：

- `if`—开始拷贝的位置。在这种情况下，我们从 Linux 分区的开始处。
- `of`—输出文件的文件名。
- `bs`—块大小。引导扇区为 512 字节。
- `count`—块的数量。

## 在 Windows 中访问 ext2 分区

有两种工具可以通过 DOS 访问 ext2（Linux Native）文件系统。一个是 ext2 tools，它提供只读访问，可以在这里：`ftp://sunsite.unc.edu/pub/Linux/system/filesystems/ext2/`。还有 `ltools`，它提供了对 ext2 分区的读写访问。

`ltools` 提供了命令行工具、一个可以通过浏览器访问的 Web 服务器以及一个 Java 工具。命令行工具模拟了许多 DOS 实用程序的功能，可以在 DOS 和所有版本的 Windows (`3x`, `9x` 和 `NT`) 中运行。它们应该也能兼容 Windows-2000，尽管尚未对其进行过广泛测试。

> 使用 `ltools` 向 ext2 文件系统写入数据时会出现一些异常行为。任何写入操作都会将文件系统设置为“干净（clean）”。这会导致问题，除非在下次系统启动时运行 `fsck`（Linux 的磁盘检查工具）。

此外，在 Windows 9x DOS 框中运行 `ltools` 时，硬盘在使用期间会被锁定。这要求你的系统中有一张软盘，即使不使用它。软盘驱动器会旋转，但对其不会进行任何更改。

`ltools` 使用 Linux 风格的正斜杠（`/`）表示目录和 DOS 风格的驱动器。对于 `/root` 目录下的所有文件，表示为 `/root/*`

`ltools` 包含以下程序：

- `ldir [-h -v | ? [-part]] [-s/dev/hd..] [Linux_Directory]`—功能类似于 DOS 或 Linux 中的 `dir` 命令。切换开关的含义如下：
  - `-h?`—帮助屏幕。
  - `-v`—版本信息。
  - `-s`—驱动器名称，例如 `/dev/hda1` 等。
  - `-part`—列出驱动器上的所有分区。
  - `Linux_Directory`—ext2 文件系统上的目录。默认是 `/`。

- `lread [-h |-v |?] [-s/dev/hd..] Linux_File [DOS_File]`—列出或复制文件。工作类似于 DOS 中的 `type` 或 `copy`。切换开关用于表示：
  - `-h?`—帮助屏幕。
  - `-v?`—版本信息。
  - `-s?`—Linux 驱动器名称，例如 `/dev/hd1` 等。
  - `Linux_File`—要查看或复制的 Linux 文件。
  - `DOS_File`—要复制的 DOS 文件。必须是有效的 DOS 文件名。Windows 9x 支持长文件名。

- `ldrive /dev/hd..`—设置默认的 Linux 分区。如果命令中没有给出分区，将默认使用此分区。例如，要将默认分区设置为 `hda1`，命令为 `ldrive /dev/hd1`。

- `lcd directory`—设置 Linux 分区的默认目录。否则将使用系统默认值。例如，要将默认目录设置为 `/root`，命令为 `lcd /root/`。

- `ldel [-h |-v |?] [-s/dev/hd..] Linux_File`—使用以下开关删除文件、目录或链接：
  - `-h?`—帮助。
  - `-v?`—版本。
  - `-s?`—Linux 分区。

- `lchange [-h |-v |?] [-s/dev/hd..] [-fMODE] [-uUID] [-gGID] Linux_File`—
  - `-h?`—帮助。
  - `-v?`—版本。
  - `-s?`—Linux 分区。
  - `-f?`—更改 Linux 文件的属性，类似于 `chmod`。使用八进制数字。请查看你的 `chmod` 手册。
  - `-u?`—更改用户 ID。查看你的 `chown` 手册。
  - `-g?`—更改组 ID。查看你的 `chown` 手册。

- `lwrite [-fMODE] [-uUID] [-gGID] DOS_Path_DOS_File_Linux_File`—复制文件。开关与 `lchange` 相同。

- `ren [-h |-v |?] [-s/dev/hd..] [-fMODE] [-uUID] [-gGID] Linux_File_old_name Linux_File_new_name`—重命名文件、目录或符号链接。开关与 `lchange` 相同。

- `lmdir [-h |-v |?] [-s/dev/hd..] [-fMODE] [-gGID] new_Linux_directory`—创建 Linux 目录。开关与 `lchange` 相同。

- `ln [-h |-v |?] [-s/dev/hd..] [-fMODE] [-gGID] LinkTarget`—创建符号链接。符号链接类似于 Windows 中的快捷方式。开关与 `lchange` 相同。

### 2.3 使用 Windows 9x 访问 ext2 分区

### 2.2 ltools 的图形界面

`ltools` 带有两个图形界面：`LREADsrv` 和 `LREADgui`。如果你需要 Windows 9x、NT 或 2000 的图形界面，有更好的工具可用。`LREADsrv` 是 `ltools` 的一部分，让你能使用浏览器读写 ext2 分区。它还需要一些 `.GIF` 和 `.HTML` 文件。当 `ltools` 提取时，会将 `/bin` 目录下的所有必要文件使命令行工具正常工作。如果你的 PC 上已经有一个 Web 服务器，就不需要加载 `LREADsrv`。你可以通过输入主机名或 IP 地址访问远程驱动器。`LREADsrv` 仍有许多 Bug：

1. 它不是多用户程序。多个用户会导致文件或目录损坏！
2. 它的错误检查功能很弱。错误通常出现在浏览器窗口中。`LREADgui` 需要较快的机器来操作（慢速会被认为很慢！）。在列出目录时屏幕可能会闪烁。这些问题更多与 `LREADgui` 本身有关。

`FSDEXT` 允许从 Windows 只读访问 ext2 分区。它不再活跃开发，但可以工作，可以在 `http://www.linux.uk/` 获取。对于读写访问，请检查 `Explore2fs`。它看起来像 Windows Explorer，并兼容 Windows 9x 和 NT。`Explore2fs` 支持广泛的功能，包括：

- 拖放。
- 支持所有块大小。
- 支持软盘（1.44MB 和 1.2MB）。
- 支持 Jaz 驱动器。
- 支持 Windows 98 扩展分区。
- 快速写入支持。很快，如果比读取快。
- 导出文件。
- 导出为文本。
- 导出目录。
- 执行文件。
- 查看符号链接。
- 导入文件。
- 导入目录。
- 新文件的 Umask。
- 删除文件。
- 删除目录。
- 创建目录。
- 重命名。
- 修改文件模式（通过属性框）。
- 更改 uid 和 gid。
- 创建设备节点。
- 创建符号链接。
- 支持硬盘。

未来版本将添加的功能：

- 格式化文件系统。
- 导入 `.tgz` 文件。这是 UNIX 的原生压缩格式，Windows 使用 ZIP。
- 语言支持。

当 `Explore2fs` 首次启动时，处于只读模式。要启用写入支持，转到 `View -> Options`，然后选择 Debug 标签页。有一个复选框启用写入支持。重启程序以启用写入支持。

`Explore2fs` 只显示 ext2 分区。要操作 ext2 分区上的文件，请右键点击文件。这将弹出一个包含以下项的菜单：

- Properties
- Export File
- Export as Text
- Rename
- Import File
- Create

要安装 Ext2fsnt，

接下来，合并 `ext2.reg`。要执行此操作，转到开始->运行并输入 `regedit`。然后选择注册表并 导入注册表文件。找到 `ext2.reg` 文件。

重启计算机以激活驱动程序。编辑 `go.cmd` 以添加你的 ext2 分区，然后运行 `go.cmd`。

在 Windows NT 系统上，你可以将 `%systemroot%\system32\drivers\rs_rec.sys` 文件替换为 Ext2fsnt 自带的版本，而无需运行 `go.cmd`。不要在 Windows 2000 系统上替换此驱动程序！该驱动程序在 Windows 2000 上不支持完全支持。

安装后，将 ext2 分区设置为 Windows 驱动器。对于 Windows NT，将它们添加到注册表中。例如，要将第一个硬盘上的第二个分区设置为 E:，请在注册表中添加以下行：

```
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SessionManager\DOS Devices]
"E":"\\\\Harddisk0\\\\\Partition2"
```
