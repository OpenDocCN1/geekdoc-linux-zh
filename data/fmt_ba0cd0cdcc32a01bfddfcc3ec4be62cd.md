
*(注：由于原文文本中存在部分内容重复和截断，上述译文已根据逻辑进行了对齐并确保了翻译的连贯性。以下为原文后续部分的完整翻译：)*

在尝试挂载它们之前，我们可能想知道每个分区是什么类型的文件系统。我们可以使用 `file` 命令来做到这一点²⁴。记住我们之前的练习，`file` 命令通过查找“文件头”信息来确定文件类型。

²⁴ 请记住，`file` 命令依赖魔数文件（magic file）来确定文件类型。如果该命令在后续对你不起，那么很可能是因为你系统上的魔数文件不包含文件系统类型的头部。

### v.4.33
Linux 作为数字取证平台的全面入门指南

```
barry@forensic1:~$ file able_3.part*
able_3.part1.raw: Linux rev 1.0 ext4 filesystem data, UUID=ca05157e-f7b3-4c6a-
9b63-235c4cad7b73 (extents) (huge files)
able_3.part2.raw: Linux rev 1.0 ext4 filesystem data, UUID=ca4ac4c0-f9d2-4d26-
9e16-10583b607372 (extents) (huge files)
able_3.part3.raw: Linux rev 1.0 ext4 filesystem data, UUID=c7f78b2-3a38-44e9-
a43-f924955bfdd (extents) (huge files)
```

之前，我们能够通过 `dfdisk` 的输出确定分区是“Linux” 分区。现在 `file` 告诉我们文件系统类型是 `ext4`⁵。我们可以利用这些信息来管理分区。记住你需要 root 权限来挂载分区，所以先切换到 root，然后依次挂载每个分区，直到找到包含 `fstab` 的 `/etc` 目录：

```
barry@forensic1:~$ su -
Password:
root@forensic1:~# mount -t ext4 -o ro,loop ~berry/able_3/able_3.part1 /mnt/evid
root@forensic1:~# ls /mnt/evid
config-huge-4.4.14 onlyblue.dat
README.initrd
elio-ia32.efi* slack.bmp
System.map0 vmlinuz
System.map-generic-4.4.14 elio-x86_64.efi* tuxlo.bmp
System.map-huge-4.4.14 grub/tuxlogo.dat
boot.0800 inside.dat vmlinuz-generic
boot_message.txt inside.dat vmlinuz-generic-4.4.14
coffee.dat map vmlinuz-()
config onlyblue.bmp
config-generic-4.4.14 vmlinuz-huge
```
