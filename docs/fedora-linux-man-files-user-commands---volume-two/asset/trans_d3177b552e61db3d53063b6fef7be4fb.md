
## HPPA 说明

要为 HPPA 制作一张可启动光盘，至少必须指定引导加载程序文件（**-hppa-bootloader**）、内核映像文件（32位、64位或两者，具体取决于硬件）以及引导命令行（**-hppa-cmdline**）。某些系统可以启动 32 位或 64 位内核，如果两者都存在，固件将自动选择一个。可选地，可以使用 **-hppa-cmdline** 指定 ramdisk 作为根文件系统。

## JIGDO 说明

Jigdo 是一个帮助分发大型文件（如 CD 和 DVD 映像）的工具；请参阅 [Jigdo](https://jigdo.sourceforge.net/) 获取更多详细信息。Debian 的 CD 和 DVD ISO 映像以 jigdo 格式发布在网络上，以便最终用户可以更有效地下载它们。

要从 **genisoimage** 创建的 ISO 映像旁边创建 jigdo 和模板文件，首先必须生成将使用的文件列表，格式如下：

MD5sum 文件大小 路径 32 位字符 12 位字符 直到行尾

MD5sum 必须用标准十六进制表示法书写，文件大小必须列出文件的字节大小，路径必须列出文件的绝对路径。例如：

```
00006cdc58ff0756c36d2efae21be376 14736 /mirror/debian/file1
000635c69b254a1be8badec3a8d05c1 211822 /mirror/debian/file2
00083436a3899a09633fc1026ef1e66e 22762 /mirror/debian/file3
```

拥有此文件后，调用 **genisoimage** 并附上所有正常的命令行参数。使用 **-jigdo-jigdo** 和 **-jigdo-template** 指定 jigdo 文件和模板文件的输出文件名，并使用 **-md5-list** 传入 MD5 列表的位置。

如果有不希望添加到 jigdo 文件中的文件（例如，如果它们经常更改），请使用 -jigdo-exclude 指定它们。如果希望在文件写入映像时验证其中一些文件，请使用 -jigdo-force-md5 指定它们。如果有任何文件不匹配，**genisoimage** 将中止操作。这两个选项都接受正则表达式作为输入。还可以根据大小进一步限制将使用的文件集 – 使用 -jigdo-min-file-size 选项。

最后，jigdo 代码需要知道如何将其获得的文件映射到镜像风格的配置。使用 **-jigdo-map** 指定路径映射方式。使用 `Debian:="/mirror/debian"` 将使所有以 `/mirror/debian` 开头的路径映射为输出 jigdo 文件中的 `Debian:<file>`。

## 示例

要在文件 `cd.iso` 中创建一个标准的 ISO9660 文件系统映像，其中目录 `cd_dir` 将成为 CD 的根目录，请调用：

```
% genisoimage -o cd.iso cd_dir
```

要为源目录 `cd_dir` 创建一个带有 Rock Ridge 扩展的 CD：

```
% genisoimage -o cd.iso -R cd_dir
```

要为源目录 `cd_dir` 创建一个带有 Rock Ridge 扩展的 CD，其中所有文件至少具有读取权限，且所有文件都属于 *root*，请调用：

```
% genisoimage -o cd.iso -r cd_dir
```

要将 tar 归档直接写入稍后包含简单 ISO9660 文件系统的 CD（其中包含该 tar 归档），请调用：

```
% tar cf - . | genisoimage -stream-media-size 333000 |\
  wodim dev=sd -dao tsize=333000s -
```

要从源目录 `cd_dir` 创建一个带有 Joliet 和 Rock Ridge 扩展的 HFS 混合 CD：

```
% genisoimage -o cd.iso -R -J -hfs cd_dir
```

要从包含 Netatalk Apple/Unix 文件的源目录 `cd_dir` 创建一个 HFS 混合 CD：

```
% genisoimage -o cd.iso -netatalk cd_dir
```

要从源目录 `cd_dir` 创建一个 HFS 混合 CD，根据列在文件“mapping”中的文件扩展名为所有文件指定 CREATOR 和 TYPES：

```
% genisoimage -o cd.iso -map mapping cd_dir
```

要从源目录 `cd_dir` 和 *another_dir* 创建带有 ISO9660 的 Apple 扩展的 CD。所有已知 Apple/Unix 格式的文件将被解码，其他文件则根据文件 *magic* 中给出的魔数指定 CREATOR 和 TYPE：

```
% genisoimage -o cd.iso -apple -magic magic -probe \
  cd_dir another_dir
```

以下示例在 CD 上放置了不同的文件，它们都命名为 README，但在作为 ISO9660/Rock Ridge、Joliet 或 HFS CD 查看时内容不同。
当前目录包含：

```
% ls -F README.hfs README.joliet README.Unix cd_dir/
```

以下命令将目录 $cd\_dir$ 的内容以及三个 README 文件放在 CD 上 – 但在三个文件系统视图中只能看到一个：

```
% genisoimage -o cd.iso -hfs -J -r -graft-points \
    -hide README.hfs -hide README.joliet \
    -hide-joliet README.hfs -hide-joliet README.Unix \
    -hide-hfs README.joliet -hide-hfs README.Unix \
    README=README.hfs README=README.joliet \
    README=README.Unix cd_dir
```

也就是说，文件 README.hfs 将在 HFS CD 上显示为 README，而其他两个 README 文件将被隐藏。Joliet 和 ISO9660/Rock Ridge CD 的情况也类似。通过组合隐藏选项，可能会出现各种奇怪的结果...

## 说明

**genisoimage** 可以安全地安装为 **suid root**。这在创建多会话映像时可能是必要的，以便允许 **genisoimage** 读取前一个会话。

如果 **genisoimage** 正在创建带有 Rock Ridge 属性的文件系统映像，且源目录树的目录嵌套层级对 ISO9660 来说过深，**genisoimage** 将执行深层目录重定位。这会导致 CD 根目录中出现一个名为 **RR_MOVED** 的目录。无法避免此目录。

不同平台的许多引导代码选项是互斥的，因为引导块不能共存，即不同的平台共享映像中的相同数据位置。请参阅 [相关文档](https://www.gnu.org/software/genisoimage/) 以获取详细信息。

## 错误

具有指向未复制到 ISO9660 文件系统树的文件的硬链接的文件，其文件引用计数将不正确。

它不会检查根目录中 `.` 条目的 SUSP 记录，以验证 Rock Ridge 增强功能的存在。此问题存在于多会话模式下读取旧会话时。

它在多会话模式下添加数据时不会正确读取重定位的目录。如果新会话未包含深层目录，任何重定位的深层目录都会丢失。

它在从 *TRANS.TBL* 进行多会话操作时不会重用 *RR_MOVED*。

它在多会话模式下不会为 *RR_MOVED* 创建 *whole_name* 条目。

可能还有其他错误。请向维护人员报告这些问题。

## HFS 问题/限制

我不得不做出一些关于修改后的 libhfs 例程如何工作的假设，然而可能存在我未曾想到或遇到这些假设失效的情况。因此，我无法保证 **genisoimage** 会按预期工作（尽管我尚未遇到重大问题）。大多数 HFS 功能运行正常，但有些未完全测试。这些在上述中标记为 *Alpha*。

虽然 HFS 文件名似乎支持大写字母和小写字母，但文件系统是不区分大小写的，即，文件名 *aBc* 和 *Abc* 是相同的。如果在目录中找到具有相同 HFS 名称的文件，**genisoimage** 将通过在其中一个文件名后添加 `'_` 字符来尝试生成唯一名称。

共享前 31 个字符的 HFS 文件/目录名称将用 `'_N'`（十进制数字）替换最后几个字符以生成唯一名称。

在“嫁接”Apple/Unix 文件或目录时必须小心（请参阅上述相关方法和语法）。无法为 Apple/Unix 编码的文件/目录使用新名称。例如，如果要向 CD 添加名为 *oldname* 的 Apple/Unix 编码文件，则不能使用命令行：

```
genisoimage -o output.raw -hfs -graft-points newname=oldname cd_dir
```

**genisoimage** 将无法解码 *oldname*。但是，只要不尝试如上所述给他们起新名称，就可以嫁接 Apple/Unix 编码的文件或目录。

在使用多会话选项创建 HFS 卷时，**-M** 和 **-C**，只有最后一个会话中的文件将位于 HFS 卷中。即 **genisoimage** 无法*添加*来自以前会话的现有文件到 HFS 卷中。

但是，如果使用 **-part** 创建每个会话，每个会话在 Mac 上挂载时将显示为单独的卷。在这种情况下，值得使用 **-V** 或 **-hfs-volid** 为每个会话指定唯一的卷名，否则每个“卷”将以相同的名称出现在桌面上。

符号链接（与其他所有非常规文件一样）不会被添加到 HFS 目录中。

混合卷可能比包含相同数据的纯 ISO9660 卷更大。在某些情况下（例如 DVD 大小的卷），差异可能很大。随着 HFS 卷变大，分配块大小（文件可以占据的最小空间量）也会增加。对于 650MB CD，分配块为 10kB，对于 4.7GB DVD 约为 70kB。

HFS 卷中的最大文件数约为 65500 – 尽管实际限制会略低于此数值。

可以使用 hfsutils 例程在 Unix 机器上访问生成的混合卷。然而，由于卷被设置为 **locked**，因此无法对其进行检查。

