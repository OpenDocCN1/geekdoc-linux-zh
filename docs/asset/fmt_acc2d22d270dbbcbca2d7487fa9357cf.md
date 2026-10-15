
密钥存储在 Unix 上的 `~/.gnupg/` 中，在 Windows 上通常存储在 `C:/Documents and Settings/%USERNAME%/Application Data/gnupg/`。

```
~/.gnupg/pubring.gpg        # Contains your public keys and all others imported
~/.gnupg/secring.gpg        # Can contain more than one private key
```

最常用选项的简短提醒：

- `-e` 加密数据
- `-d` 解密数据
- `-r NAME` 为收件人 `NAME` 加密（或 '全名' 或 'email@domain'）
- `-a` 创建密钥的 ascii 护甲输出
- `-o` 用作输出文件

示例中使用 'Your Name' 和 'Alice' 作为密钥，它们通过电子邮件或全名或部分名称引用。例如我可以使用 'Colin' 或 'c@cb.vu' 来引用我的密钥 `[Colin Barschel (cb.vu) <c@cb.vu>]`。

# 仅用于个人加密

无需导出/导入任何密钥，你已经拥有两者。

```
# gpg -e -r 'Your Name' file          # Encrypt with your public key
# gpg -o file -d file.gpg              # Decrypt. Use -o or it goes to stdout
```

## 使用密钥加密 - 解密

首先你需要导出你的公钥供他人使用。你还需要导入例如来自 Alice 的公钥来为她加密文件。你可以以简单的 ascii 文件处理密钥或使用公钥服务器。

例如 Alice 导出她的公钥而你导入它，你就可以为她加密文件。只有 Alice 才能解密它。

```
# gpg -a -o alicekey.asc --export 'Alice'     # Alice exported her key in ascii file.
# gpg --send-keys --keyserver subkeys.pgp.net KEYID  # Alice put her key on a server.
# gpg --import alicekey.asc                     # You import her key into your pubring.
# gpg --search-keys --keyserver subkeys.pgp.net 'Alice' # or get her key from a server.
```

一旦密钥导入，加密或解密文件就非常容易：

```
# gpg -e -r 'Alice' file          # Encrypt the file for Alice.
# gpg -d file.gpg -o file          # Decrypt a file encrypted by Alice for you.
```

### 密钥管理

```
# gpg --list-keys                     # list public keys and see the KEYIDS
The KEYID follows the '/' e.g. for: pub 1024D/D12B77CE the KEYID is D12B77CE
# gpg --gen-revoke 'Your Name'         # generate revocation certificate
# gpg --list-secret-keys               # list private keys
# gpg --delete-keys NAME               # delete a public key from local key ring
# gpg --delete-secret-key NAME         # delete a secret key from local key ring
# gpg --fingerprint KEYID              # Show the fingerprint of the key
# gpg --edit-key KEYID                 # Edit key (e.g sign or add/del email)
```

## 10 加密分区

`Linux with LUKS (p31)` | `Linux dm-crypt only (p32)` | `FreeBSD GELI (p32)` | `FBSD pwd only (p33)`

还有（许多）其他替代方法来加密磁盘，我在这里只展示我知道并使用的方法。请记住安全性只有在操作系统未被篡改时才有效。入侵者可以很容易地从键盘事件中记录密码。此外，当分区挂载时数据可以自由访问，在这种状态下无法阻止入侵者访问它。

### 10.1 Linux

这些说明使用 Linux `dm-crypt`（device-mapper）功能，可在 2.6 内核上使用。在此示例中，让我们加密分区 `/dev/sdc1`，它可以是任何其他分区或磁盘，或 USB 或使用 `losetup` 创建的文件基础分区。在这种情况下我们将使用 `/dev/loop0`。参见文件映像分区。设备映射器使用标签来标识分区。我们在此示例中使用 `sdc1`，但它可以是任何字符串。

#### 使用 LUKS 的 dm-crypt

`LUKS` 与 `dm-crypt` 具有更好的加密，并使同一个分区可以有多个密码或轻松更改密码。要测试 `LUKS` 是否可用，只需输入 `# cryptsetup --help`，如果没有关于 `LUKS` 的内容显示，请使用下面的 Without LUKS 说明。首先如有必要创建分区：`fdisk /dev/sdc`。

##### 创建加密分区

```
# dd if=/dev/urandom of=/dev/sdc1    # Optional. For paranoids only (takes days)
# cryptsetup -y luksFormat /dev/sdc1  # This destroys any data on sdc1
```

```
# cryptsetup luksOpen /dev/sdc1 sdcl
# mkfs.ext3 /dev/mapper/sdcl      # create ext3 file system
# mount -t ext3 /dev/mapper/sdcl /mnt
# umount /mnt
# cryptsetup luksClose sdcl        # Detach the encrypted partition
```

##### 挂载

```
# cryptsetup luksOpen /dev/sdc1 sdcl
# mount -t ext3 /dev/mapper/sdcl /mnt
```

##### 卸载

```
# umount /mnt
# cryptsetup luksClose sdcl
```

#### 不使用 LUKS 的 dm-crypt

```
# cryptsetup -y create sdcl /dev/sdc1      # or any other partition like /dev/loop0
# dmsetup ls                               # check it, will display: sdcl (254, 0)
# mkfs.ext3 /dev/mapper/sdcl               # This is done only the first time!
# mount -t ext3 /dev/mapper/sdcl /mnt
# umount /mnt/
# cryptsetup remove sdcl                   # Detach the encrypted partition
```

要重新挂载分区，请完全重复上述操作（不包括 `mkfs` 部分！）。如果密码不正确，`mount` 命令将失败。在这种情况下只需移除映射 `sdcl`（`cryptsetup remove sdcl`）并重新创建它。

### 10.2 FreeBSD

FreeBSD 两个流行的磁盘加密模块是 `gbde` 和 `geli`。我现在使用 `geli`，因为它更快并且也使用 crypto 设备进行硬件加速。参见 The FreeBSD handbook 第 18.6 章了解所有细节。`geli` 模块必须加载或编译到内核中：

```
options GEOM_ELI
device crypto                         # or as module:
# echo 'geom_eli_load="YES"' >> /boot/loader.conf   # or do: kldload geom_eli
```

#### 使用密码和密钥
