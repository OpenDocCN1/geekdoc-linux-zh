

这应该是你在新环境中运行 DSL 所需的最低配置。当然，你可能希望或需要为特定的硬件编译特殊的模块。

安装 cloop 模块后，你应该重新启动硬盘安装。这可以很好地测试新内核和模块，特别是新的 cloop 模块。图 11-11 显示了新的 2.4.31 内核和 cloop 模块被成功用于加载 xchat.uci。

![](img/af53325d7f38f1cdafca9f44568e4ab8_259_0.png)

**图 11-11**  加载 MyDSL 扩展 (xchat.uci) 以检查 cloop 驱动是否正常工作。

最后一步是将新的内核和模块复制到 live CD-ROM 环境中。编译大多数较新的内核通常会导致内核过大而无法放入单张软盘。这就是 DSL 仍沿用当前内核的原因之一。过大而无法放入单张软盘意味着没有 Syslinux 版本的 DSL CD-ROM。这意味着许多较旧的计算机将无法启动 Isolinux CD-ROM。因此，以下讨论仅涉及使用 Isolinux 版本设置 DSL。

让我们再次从标准 DSL CD-ROM 启动，并在你安装 DSL 且拥有新内核和模块的同一分区上设置你的 remaster 工作目录。假设它是硬盘分区 hda4。简要回顾一下，请按以下步骤操作：

1. **使用最小选项启动 DSL：**

    ```
    boot: dsl 2 base norestore legacy
    ```

2. **挂载硬盘安装分区并更改目录到 `/tmp`：**

    ```
    # mount /mnt/hda4
    # cd /mnt/hda4
    ```

3. **创建 remaster 目录并进入：**

    ```
    # mkdir remaster
    # cd remaster
    ```

4. **从随附的 CD-ROM 复制 remaster 脚本：**

    ```
    # cp -a /cdrom/chapter11/remaster/* .
    # cp /cdrom/chapter11/remaster/.bash_profile .
    ```

5. **设置工作目录环境：**

    ```
    # ./setupFromCD
    ```

如前所述的工作目录 remaster 方法中所述，初始 ramdisk 包含启动时模块和内核。安装新内核和模块以供 live CD-ROM 使用的第一步是解包 minirt24.gz。请记住，该文件位于你的 remaster 工作目录 master/boot/isolinux 中。解包该文件以访问 modules 目录的步骤如下：

1. 更改目录到初始 ramdisk 文件，解包并挂载它：

    ```
    # cd master/boot/isolinux
    # gunzip minirt24.gz
    # mkdir mroot
    # mount minirt24 mroot/ -o loop
    ```

2. 更改目录到启动时模块：

    ```
    # cd mroot/modules
    ```

3. 复制新的 cloop 模块并有选择地复制所需的 SCSI 模块：

    ```
    # cp /mnt/hda4/lib/modules/2.4.31/kernel/drivers/block/cloop.o .
    # cd scsi
    # cp /mnt/hda4/lib/modules/2.4.31/kernel/drivers/scsi/* .
    ```

4. 卸载、重新打包并清理此过程：

    ```
    # cd ../../..
    # umount mroot
    # gzip -9 minirt24
    # rmdir mroot
    ```

5. 复制新的内核：

    ```
    # cp /mnt/hda4/boot/vmlinuz-2.4.31 linux24
    # cd ../../..
    ```

6. 将剩余模块复制到运行时映像中：

    ```
    # cp -a /mnt/hda4/lib/modules/2.4.31 source/KNOPPIX/lib/modules/.
    ```

7. 更新运行时系统映射：

    ```
    # cp /mnt/hda4/boot/System.map-2.4.31 source/KNOPPIX/boot/.
    # chroot source/KNOPPIX
    # cd /boot
    # rm System.map-2.4.26
    # ln -sf System.map-2.4.31 System.map
    ```

8. 删除对 2.4.26 模块的引用：

    ```
    # cd /lib/modules
    # rm -rf 2.4.26/
    ```

9. 可选地删除运行时映像中不需要的模块：

    ```
    # cd 2.4.31/
    # rm -rf kernel/drivers/atm
    # rm -rf kernel/drivers/isdn
    # rm -rf kernel/drivers/telephony
    # rm -rf kernel/net/atm
    # rm -rf kernel/net/ipv6
    # rm -rf kernel/fs/affs
    # rm -rf kernel/fs/coda
    # rm -rf kernel/fs/cramfs
    # rm -rf kernel/fs/freefs
    # rm -rf kernel/fs/hpfs
    # rm -rf kernel/fs/ncpfs
    # rm -rf kernel/fs/qnx4
    # rm -rf kernel/fs/romfs
    ```

10. 退出 chroot 环境：

    ```
    # exit
    ```

### NOTE

> 在开始复制任何要添加的新模块之前，你应该先从初始 ramdisk 中删除现有的 SCSI 模块。你只需要复制实际启动系统所需的模块。如果你的系统不使用 SCSI，此区域可以大幅减少。启动 DSL 所需的最小模块是 ide-scsi.o。

前述的模块删除基于实际的 DSL v2.x 系统。你选择删除哪些模块完全取决于你。如果你不需要防火墙，可以删除 netfilter 模块。如果你不需要 SCSI，通过删除 SCSI 模块可以节省大量空间。DSL 的挑战在于为公众提供足够的模块。你不能说：“反正我这里能用！” DSL 中的模块经过了多年众多用户的考验。

至此，升级内核和模块的过程已完成。继续按照之前讨论的正常完整 remastering 过程进行。要从工作目录制作 ISO，只需依次运行 ./makeimage 脚本和 ./makeiso 脚本即可。

## SUMMARY

本章已全面涵盖了 remastering DSL 的内容。你已看到它可以有多么简单——从启动你典型的经过充分测试的 frugal 系统，生成一个完整的可启动 MyDSL CD-ROM，到使用工作目录方法进行完整 remastering。

通过完整 remastering，你看到了如何更好地控制默认设置和添加应用程序。你也应该对

