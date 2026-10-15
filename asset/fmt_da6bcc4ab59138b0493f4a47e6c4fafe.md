
## 使用加密卷

通常，服务器上的文件必须防止那些试图从远程未经授权访问的人。然而，如果有人成功获取了服务器的物理访问，情况就会不同。一旦以 root 登录，就可以访问服务器上的所有文件。在下一章中，你将学到以 root 身份登录并不困难——即使你没有 root 密码。

通常服务器受到了良好的保护，未经授权的人不允许访问它。但如果 Linux 安装在笔记本电脑上，情况就更糟了，你可能会把笔记本忘在火车或其他任何其他公共场所，熟练的人可以轻易获取你笔记本电脑上的所有数据。这就是为什么加密驱动器可能很有用的原因。

在本节中，你将学习如何使用 LUKS（Linux 统一密钥设置）创建一个加密卷。遵循以下六个步骤的操作：

- 1. 首先，你需要创建一个想要加密的设备。它可以是一个 LVM 逻辑卷或分区。
- 2. 创建设备后，你需要将其格式化为加密设备。执行此操作请使用 `cryptsetup luksFormat /dev/device` 命令。在此操作期间，你还将设置解密密码。务必记住这个密码，因为一旦设备加密，它是访问设备的唯一方法！
- 3. 一旦设备格式化为加密设备，你需要在对其进行任何操作之前打开它。打开时，为加密设备分配一个名称。该名称出现在 `/dev/mapper` 目录下，因为整个过程由 Device Mapper 管理。
- 4. 设备打开后，你就可以用文件系统对其进行格式化。
- 5. 设备格式化后，你可以挂载它。
- 6. 完成后，你应该卸载并关闭加密设备。

## 练习 5.12

### 创建加密卷

在此练习中，你将学习如何使用 `cryptsetup` 创建加密卷。接下来，你将在该文件上使用 `luksFormat` 和 `luksOpen` 对其进行格式化并开始使用。最后，你将其放入 `/etc/fstab` 以确保它在下次重启服务器时被激活。

- 1. 使用 `cryptsetup luksFormat /dev/sdb` 创建加密卷。当询问你是否真的要这样做时，输入 `YES`。
- 2. 使用 `cryptsetup luksOpen /dev/sdb confidential` 打开加密卷。
- 3. 使用 `mkfs.ext4 /dev/mapper/confidential` 格式化文件系统。
- 4. 使用 `mount /dev/mapper/confidential /mnt` 挂载设备。
- 5. 使用 `unmount /mnt` 卸载设备。
- 6. 使用 `cryptsetup luksClose confidential` 关闭卷。

#### 列表 5.18：创建并打开加密卷

```
[root@hn1]# cryptsetup luksFormat /dev/sdb

WARNING!

==========

This will overwrite data on /dev/sdb.

Are you sure? (Type YES) YES

Enter passphrase for /dev/sdb:

Verify passphrase:

[root@hn1]# cryptsetup luksOpen /dev/sdb confidential

Enter passphrase for /dev/sdb:

[root@hn1]# ls /dev/mapper

confidential  control-loop-0

[root@hn1]# mkfs.ext4 /dev/mapper/confidential

[root@hn1]# mount /dev/mapper/confidential /mnt

[root@hn1]# unmount /mnt

[root@hn1]# cryptsetup luksClose confidential
```

# 第 5 章 配置与管理存储

`/etc/crypttab` 中的两个字段：加密设备打开后的名称，以及底层的真实设备名称，如下例所示：
`confidential /dev/sdb8`

在确保你已经创建了 `/etc/crypttab` 文件后，你可以在 `/etc/fstab` 中添加一行，将加密设备以其在打开 `/dev/mapper` 目录后存在的形式进行挂载。这意味着你将不会挂载 `/dev/sdb8`，而是挂载 `/dev/mapper/confidential`。接下来的行显示了 `/etc/fstab` 中的行应该是什么样：

```
/dev/mapper/confidential /confidential ext4 defaults 1 2
```
