
```sh
#!/bin/sh
#
# 清理 .bash_history
if [ -f source=KNOOPPIX/.bash_history ]; then
    rm source=KNOOPPIX/.bash_history
fi
if [ -f source=KNOOPPIX/home/dsl/.bash_history ]; then
    rm source=KNOOPPIX/dsl/.bash_history
fi

# 检查是否需要 .bash_profile
if [ -f source=KNOOPPIX/.bash_profile ]; then
    cp .bash_profile source=KNOOPPIX/.bash_profile
fi

# 拷贝发布信息。
cp -f release.txt source=KNOOPPIX/usr/share/doc/dsl/.
#
mkisofs -r -U -hide-rd-moved-cache-no-bak -pad
source/KNOOPPIX | nice -5 create_compressed_fs -best 65536 >
master/KNOOPPIX/KNOOPPIX
#
sync
sync
```

`makeimage` 脚本执行以下操作：

- 第 4-9 行删除了所有在 chroot 环境下记录的内容的内容。
- 第 12-14 行删除了你可能使用的任何 ssh 连接的引用。
- 第 17-19 行检查是否需要 `.bash_profile`。
- 第 21 行使用直接方法写入发布信息。
- 第 23 行从你的 `source/` 目录创建新的压缩 `KNOOPPIX/KNOOPPIX` 镜像并将其写入 `master/` 目录。

## 官方 Damn Small Linux 籍

根据你的机器资源，运行 `makeimage` 脚本可能需要很长时间。在成功构建新的压缩镜像后，你必须将启动文件、内核、初始内存磁盘和压缩的运行时镜像结合。此过程会在 `iso/` 目录中创建实际的 ISO 镜像。ISO 文件准备好刻录到 CD-R CD-ROM 上。如果你添加了可选参数 `cd`，脚本会记录镜像。

## makeiso 脚本

在清理 chroot 环境后，下一阶段将新创建 `KNOOPPIX` 文件与启动镜像文件合并成单一的 CD 或 DVD 镜像。

```sh
1. #!/bin/sh
2. RELEASE=`cat release.txt'
3. #
4. if [ -f master/KNOOPPIX/boot.img ]; then
5. rm master/KNOOPPIX/boot.img
6. -tar xf boot/isolux.tgz
7. fi
8. #
9. mkisofs -pad -l -r -v -V KNOOPPIX -no-emboot -boot-load-size
10. boot-info-table b boot/isolinux/isolinux.bin -c
boot/isolinux/boot.cat -hide-moved -o iso/"RELEASE".iso master
11. #
12. sync
13. sync
14. if [ -n "$1" ]; then
15. if [ "$1" == "cd" ]; then
16. ddrecord -v speed=4 dev=0,0,0 -iso/"RELEASE".iso
17. fi
18. fi
19. cd iso
20. mdsum "$RELEASE".iso > "$RELEASE".iso.md5.txt
21. sync
22. mdsum -c "$RELEASE".iso.md5.txt
23. cd ../
```

`makeiso` 脚本可以在附带 CD-ROM 的 `chapter11-remaster` 目录下找到。该脚本应在工作目录下运行。注意：

- 行 提供了你的 ISO 镜像名称和校验和文件。
- 第 4-7 行处理 Isolinux 和 Syslinux 版本的 DSL。Syslinux 使用 `boot.img` 启动文件，而 Isolinux 使用目录。这些行提供了备份/恢复目录的机制。Syslinux `.img` 是标准软磁盘镜像，因此不需要包含在备份/恢复过程中。
- 第 9 行创建实际的 ISO。它将 `master/` 目录中的文件合并到 `iso/` 目录的 ISO 镜像中。
- 第 13-17 行检查启动脚本是否带有 `cd` 参数。脚本默认到 CD-ROM 刻字机位置 0,0,0。使用此选项将新的 ISO 镜像写入 CD-R。
- 第 19 行创建网络传输和验证的 md5 校验文件。
- 第 21 行验证校验的一致性。

## 创建 Syslinux ISO 镜像

许多旧电脑无法启动基于 Isolinux 的 CD-ROM。这些旧电脑仅限于实际软磁盘大小的启动镜像。Syslinux 启动加载程序使用这种机制。

## makesys 脚本

`makesys` 脚本可以在附带 CD-ROM 的 `chapter11-remaster` 目录下找到。该脚本应从工作目录运行以创建 Syslinux 可启动 ISO 镜像。以下是该脚本的内容：

```sh
1. #!/bin/sh
2. RELEASE=`cat release.txt`
3. #
4. if [ -d master/boot ]; then
5. tar -czvf boot.isolinux.tgz master/boot/
6. rm -f master/boot
7. fi
8. cp boot.img KNOOPPIX/
9. mkisofs -pad -l -r -j KNOOPPIX/boot.img -c KNOOPPIX/boot.cat -hide-moved -o iso/"RELEASE".syslinux.iso master
10. sync
11. sync
12. if [ "$1" = "1" ]; then
13. if [ "$2" = "cd" ]; then
14. dd -v speed=4 dev=0,0,0 -iso/"RELEASE".syslinux.iso
15. fi
16. fi
17. cd iso
18. md5sum "$RELEASE".syslinux.iso > "$RELEASE".syslinux.iso.md5.txt
19. sync
20. md5sum -c "$RELEASE".syslinux.iso.md5.txt
21. cd ..
```

## 官方 Damn Small Linux 籍

关于 `makesys` 脚本的注意：

- 行 2 提供了你的 ISO 镜像名称和校验和文件。
- 第 4-7 行处理 Isolinux 和 Syslinux 版本的 DSL。Syslinux 使用 `boot.img` 作为启动文件，而 Isolinux 使用目录。这些行提供了备份/恢复 Isolinux 目录的机制。Syslinux `boot.img` 是标准 DSL 软磁盘镜像，因此不包含在备份/恢复过程中。
- 行 8 拷贝 DSL 标准启动软磁盘以替换 `isolinux/` 目录。
- 行 9 创建实际的 ISO。它将 `master/` 目录中的文件和 `boot.img` 合并到 `iso/` 目录的 ISO 镜像文件中。
- 第 12-16 行检查脚本是否带有 `cd` 参数。脚本默认到 CD-ROM 刻字机设备位置 0,0,0。使用此选项将新的 ISO 镜像写入 CD-R。
- 行 18 创建网络传输和验证的 md5 校验文件。
- 行 20 验证校验的一致性。

## 内存

要更改 Syslinux 版本的初始内存磁盘，请使用以下步骤：

- 1. 切换目录到 `master/KNOPPIX`。在那里你可以找到一个名为 `boot.img` 的文件。该文件与从软磁盘启动 DSL 时使用的 `bootfloppy.img` 相同。
- 2. 创建挂载点并挂载软磁盘镜像：

```sh
# mkdir boot
# mount boot.img boot/ -t mdos -o loop
```

- 3. 拷贝并解压 `minirt24.gz` 初始内存磁盘：

```sh
# cp boot/minirt24.gz
# gunzip minirt24.gz
```

- 4. 创建挂载点并挂载初始内存磁盘：

```sh
# mkdir mroot
# mount minirt24 mroot/ -t ext2 -o loop
```

- 5. 与之前的 Isolinux 版本一样，进入 `mroot` 并按照之前的描述对启动模块或启动脚本更改进行必要的编辑。只需注意 Syslinux 版本的初始内存磁盘必须在物理软磁盘的大小范围内。

## 第 11 章 设置完全重制环境

要逆转过程并将初始内存盘（ramdisk）及相关文件重新封装回 `boot.img` 文件，请执行以下操作：

- 1. 退出 root 目录，卸载并压缩初始内存盘：
