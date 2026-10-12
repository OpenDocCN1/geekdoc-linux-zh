
```bash
# cd ..
# umount /root/
# gzip -9 minirt24
```

- 2. 将压缩后的内存盘移回 boot 挂载点：

```bash
# mv minirt24.gz boot/
mv: overwrite 'boot/minirt24.gz?' y
```

- 3. 卸载 boot 挂点并移除工作目录：

```bash
# umount boot
# rmdir boot/ /root/
```

## 构建 DSL Qemu 嵌入版本

虚拟化目前非常流行。DSL 整合了许多功能，使得在沙箱独立虚拟环境中运行 DSL 变得非常简单。使用工作目录下的 `mkqemu` 自动化脚本，创建 zip 镜像也非常简单。

### makeqemu 脚本

`makeqemu` 脚本位于光盘的 `chapter11/ remaster` 目录下。该脚本与其他脚本一样，从你的工作目录基础运行。以下是 `makeqemu` 脚本的内容：

```bash
1. #!/bin/bash
2. RELEASE=$(cat release.txt)
3. rm iso/ $RELEASE-embedded.zip
4. cd qemu
5. pwd
6. cp ../master/KNOPPIX/ knoppix/
7. /gnu/zip -r ../RELEASE-embedded.zip
8. cd ../iso
9. md5sum $RELEASE-embedded.zip > $RELEASE-embedded.md5.txt
10. sync
11. md5sum -c $RELEASE-embedded.md5.txt
12. cd ../
```

注意关于 makeqemu 脚本的：

- 行 2 命名发行文件。
- 行 3 移除任何已存在的发行文件。
- 行 6 将镜像拷贝到 qemu/ 目录。

### 官方 Damn Linux 书

- 行 7 使用 GNU 版本的 制作兼容的 zip 文件。
- 行 9 生成校验和文件。
- 行 11 验证校验和完整性。

## 构建 DSL VMware

另一个流行的虚拟化系统是 VMware。DSL 也通过发布 VMX 版本支持这一点。在工作目录中运行 `makevmx` 脚本可以实现此过程。

### makevmx 脚本

`makevmx` 脚本同样位于光盘的 `chapter11/ remaster` 目录下。该脚本与其他脚本一样，从你的工作目录基础运行。以下是 `makevmx` 脚本的内容：

```bash
#!/bin/bash
RELEASE=$(cat release.txt)
rm iso/"$RELEASE"-vmx.zip
cd vmware
pwd
sed "s/XXXXXX/$RELEASE/" ../dsl.vmx > dsl.vmx
cp ../iso/"$RELEASE".iso
gnu/zip -r iso/"$RELEASE"-vmx.zip
rm "$RELEASE".iso
cd iso
md5sum "$RELEASE"-vmx.zip > "$RELEASE"-vmx.zip.md5.txt
sync
md5sum -c "$RELEASE"-vmx.zip.md5.txt
cd ..
```

> 注意 makevmx 脚本：
- 行 2 命名发行文件。
- 行 3 移除任何已存在的发行文件。
- 行 6 更新此版本的 VMware 配置。
- 行 7 将完整的 ISO 镜像拷贝到 vmware/ 目录。
- 行 8 使用 GNU 版本的 制作兼容的 zip 文件。
- 行 11 生成校验和文件。
- 行 13 验证校验和完整性。

# 第 11 章 设置完全重制环境

## 为 DSL 使用内核

到本章为止，你已经看到了如何从普通的 DSL 系统创建一个自定义的可启动 MyDSL 光盘。你已经看到了如何从启动到运行级别2的 DSL 光盘重制所有 DSL 镜像。如何在 DSL 中更改内核？像一样，有很多方法可以完成此任务。然而，发现从传统的硬盘安装中执行此任务是最好的。

通过硬盘安装，你可以确保权限正确。可以使用标准的 make 程序。你可以在传统环境中轻松测试你的新内核和模块。最后，在彻底测试后，你可以将新内核和模块拷贝到 DSL 光盘系统所需的布局中。

### 编译新内核

按照我从已知状态开始的通常建议，让我们在这个任务中也这样做：

- 1. 使用 install 菜单从 DSL 光盘启动：

  boot: `install`

- 2. 安装到 Linux 分区。建议你进行完整安装并使用 Grub 引导程序。我还建议你编辑 grub 菜单启动到运行级别2。
- 3. 创建并进入典型的源码目录：

  `# mkdir /usr/src`

  `# cd /usr/src`

- 4. 加载工具和编译器（这些可以在附的光盘上找到）：

  `# mydsl-load /cdrom/`

  `# mydsl-load /cdrom/`

- 5. 从光盘加载源码：

  `# tar -xzf /cdrom/`

- 6. 配置内核：

  `# menuconfig`

- 7. 编译内核：

  `# make`

- 8. 编译模块：

  `# make`

- 9. 安装内核：

  `# make install`

- 10. 更新模块：

  `# modprobe -a`

## 第 11 章 设置完全重制环境

这应该是运行 DSL 所需的最小配置。当然，你可能想要或需要为你的特定硬件编译特殊模块。

安装内核后，你应该重启硬盘。图 11-11 显示了检查驱动程序是否正常的新模块。

![](img/f6ecb623fe81208d8ad14db9eda3a259_0.png)

最后的过程是在实时光盘环境下编译新内核和模块。编译新（更新）内核通常会导致内核太大而无法放入单张软磁盘。这就是为什么 DSL 一直留在目前的光盘上。对于单张软磁盘太大意味着 Syslinux 版本的光盘。因此，许多旧电脑将无法启动 Syslinux 光盘。因此，下面的讨论仅针对使用 Syslinux 版本的 DSL 设置。

让我们再次从标准的 DSL 光盘启动，并在安装 DSL 并拥有新内核和模块的同一分区上设置你的重制工作目录。假设它是硬盘分区 hda4。简单回顾一下，遵循以下步骤：

- 1. 以最小选项启动 DSL：

  boot: dsl 2 base norestore legacy

- 2. 挂载硬盘安装分区并进入 /tmp 目录：

  `# mount /mnt/hda4`

  `# cd /mnt/hda4`

- 3. 创建重制目录并进入：

  `# mkdir remaster`

  `# cd remaster`

- 4. 从附的光盘拷贝重制脚本：

  `# cp -a /cdrom/chapter11/remaster/* .`

  `# cp /cdrom/chapter11/remaster/.bash_profile .`

- 5. 设置工作目录环境：

  `# ./setupFromCd`

# 糟糕的小型 Linux 教程

正如之前在工作目录重制方法中所过的，初始内存磁盘（initial ramdisk）包含了启动模块和内核。为你的 live CD-ROM 安装新内核和模块的第一步是解 `minirt24.gz`。请记住该文件位于重制工作目录的 `master/boot/isolinux` 下。回解包此文件以访问模块目录的操作：

- 1. 切换到初始内存磁盘文件，解压并挂载它：

```bash
# cd master/boot/isolinux

# gunzip minirt24.gz

# mkdir moot

# mount minirt24 moot/ -o loop
```

- 2. 切换到启动模块目录：
- 3. 复制新的 cloop 模块并选择性复制所需的 SCSI 模块：

```bash
# cp /mnt/hda4/lib/modules/2.4.31/kernel/drivers/block/cloop.o

# cd scsi
```

- 4. 卸载、重新打包并清理此过程：

```bash
# cd ../..

# umount moot

# gzip -9 minirt24

# rmdir moot
```

- 5. 复制新内核：

```bash
# cp /mnt/hda4/boot/vmlinux-2.4.31 linux

# cd ../..
```

- 6. 复制运行时镜像中的剩余模块：

```bash
# cp -a /mnt/hda4/lib/modules/2.4.31 source/KNOPPIX/lib/modules/.
```

- 7. 更新系统映射：

```bash
# cp /mnt/hda4/boot/System.map-2.4.31 source/KNOPPIX/boot/

# chroot source/KNOPPIX
```
