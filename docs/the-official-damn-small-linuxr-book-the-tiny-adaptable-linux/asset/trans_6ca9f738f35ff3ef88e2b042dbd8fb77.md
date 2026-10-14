

其他尺寸或分辨率将无法工作。你可以使用 Gimp MyDSL 扩展来编辑和/或创建启动映像文件。

- **f2 和 f3：** 这些是按下初始启动提示符处的 F2 和 F3 功能键时显示的帮助文件。这些是文本文件，可以用任何文本编辑器编辑。
- **minirt24.gz：** 这是用于引导 DSL 的初始 ramdisk。

> **注意**
> 
> Syslinux 版本将这些文件打包到一个软盘大小的映像中。这称为 `boot.img`。该映像文件的解包和打包将在后面讨论，具体在“创建 Syslinux ISO 映像”部分。

## 默认启动选项

默认的启动时选项存储在 `isolinux.cfg` 或 `syslinux.cfg` 中，具体取决于你选择的 CD-ROM 主类型。对于基于 Isolinux 的重新制作，文件位于 `master/boot/isolinux/isolinux.cfg`。这是一个简单的文本文件，可以轻松编辑。启动选项在 APPEND 行中指定。

## 启动闪屏

启动闪屏包含在启动时显示的图像。这是显示在 boot: 提示符上方的图像。该图像非常难以创建，因为它采用 LSS16 格式。我已在 CD-ROM 上的 `chapter11/remaster/gnu` 目录中提供了实用程序。

通常的流程是将图像文件 `logo.16` 复制到运行 X Windows 系统的机器上的工作目录。要将 LSS16 转换为 Gimp 可以显示的格式，请使用以下命令：

```
# lss16toppm < logo.16 > logo.ppm
# gimp logo.ppm
```

编辑或创建新的图像文件后，使用 `chapter11/remaster/gnu` 目录中提供的实用程序之一：`giftoppm`、`pngtoppm` 或 `bmptoppm`。然后，转换回 LSS16 格式。例如，如果在 Gimp 中将图像保存为 `.bmp`，请使用

```
# bmptoppm < logo.bmp > logo.ppm
# ppmto lss16 < logo.ppm > logo.16
```

完成对基础系统的所有更改后，你就可以创建新的压缩 KNOPPIX/KNOPPIX 文件了。

## makeimage 脚本

makeimage 脚本位于随附 CD-ROM 的 chapter11/remaster 目录中。脚本应从你的工作目录中运行。以下是脚本的内容，已添加行号：

```
1. #!/bin/sh
2. #
3. # Clean up .bash_history
4. if [ -f source/KNOPPIX/.bash_history ]; then
5. rm source/KNOPPIX/.bash_history
6. fi
7. if [ -f source/KNOPPIX/home/ds1/.bash_history ]; then
8. rm source/KNOPPIX/home/ds1/.bash_history
9. fi
10. #
11. # Clean up any ssh hosts
12. if [ -d source/KNOPPIX/root/.ssh ]; then
13. rm -rf source/KNOPPIX/root/.ssh
14. fi
15. #
16. # Check to see if need .bash_profile
17. if [ ! -f source/KNOPPIX/.bash_profile ]; then
18. cp .bash_profile source/KNOPPIX/.bash_profile
19. fi
20. # Copy over the release info.
21. cp -f release.txt source/KNOPPIX/usr/share/doc/ds1/.
22. #
23. mkisofs -R -U -hide-rr-moved -cache-inodes -no-bak -pad source/KNOPPIX | nice -5 create_compressed_fs -best - 65536 > master/KNOPPIX/KNOPPIX
24. #
25. sync
26. sync
```

makeimage 脚本执行以下操作：

- 第 4-9 行删除在 chroot 环境中记录的所有引用。
- 第 12-14 行删除你可能使用过的任何 ssh 连接的引用。
- 第 17-19 行检查是否需要 .bash_profile。
- 第 21 行使用直接方法写入发行版信息。
- 第 23 行从你的 source/ 目录创建新的压缩 KNOPPIX/KNOPPIX 映像并写入 master/ 目录。

根据你的机器资源运行 makeimage 脚本可能需要很长时间。成功构建新的压缩映像后，你必须下一步将启动文件、内核、初始 ramdisk 和压缩运行时映像组合起来。此过程会在你的 iso/ 目录中创建实际的 ISO 映像文件。ISO 文件已准备好刻录到 CD-R CD-ROM 上。如果添加可选参数 cd，脚本会记录映像。

## makeiso 脚本

清理 chroot 环境后，下一个阶段实际创建 ISO 映像。此阶段将新创建的 KNOPPIX 映像文件与启动映像文件合并为单个可启动的 CD 或 DVD 映像。

```
1. #!/bin/sh
2. RELEASE=`cat release.txt`
3. #
4. if [ -f master/KNOPPIX/boot.img ]; then
5.   rm master/KNOPPIX/boot.img
6.   tar -zxvf boot/isolinux.tgz
7. fi
8. #
9. mkisofs -pad -l -r -J -v -V KNOPPIX -no-emul-boot -boot-load-size 4 -boot-info-table -b boot/isolinux/isolinux.bin -c boot/isolinux/boot.cat -hide-rr-moved -o iso/"$RELEASE".iso master
10. #
11. sync
12. sync
13. if [ -n "$1" ]; then
14.   if [ "$1" == "cd" ]; then
15.     cdrecord -v speed=4 dev=0,0,0 -data iso/"$RELEASE".iso
16.   fi
17. fi
18. cd iso
19. md5sum "$RELEASE".iso > "$RELEASE".iso.md5.txt
20. sync
21. md5sum -c "$RELEASE".iso.md5.txt
22. cd ../.
```

makeiso 脚本可在随附 CD-ROM 的 chapter11/remaster 目录中找到。脚本应从你的工作目录中运行。请注意以下几点：

- 第 2 行提供你的 ISO 映像文件和校验和文件的名称。
- 第 4 行至第 7 行允许处理 DSL 的 Isolinix 和 Syslinux 版本。Syslinux 使用 boot.img 用于启动文件，而 Isolinix 使用目录。这些行提供了一种备份/恢复你的 Isolinix

