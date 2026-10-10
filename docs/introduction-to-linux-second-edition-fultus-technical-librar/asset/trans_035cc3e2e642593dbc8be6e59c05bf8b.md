
## 9.3 使用 rsync

### 9.3.1 简介

rsync 程序是一个快速且灵活的远程备份工具。它在 UNIX 和类 UNIX 系统中很常见，易于配置并用于脚本中。虽然 rsync 中的 r 代表“远程”，但你不必将此字面意思完全当真。你的“远程”设备也可以是一个 USB 存储设备或硬盘上的另一个分区，你不需要有两台分离的机器。

### 9.3.2 示例：rsync 到 USB 存储设备

如第 3.1.2.3 节所述，我们必须先挂载该设备。可能需要以 root 用户身份执行此操作：

```
root@theserver# mkdir /mnt/usbstore
```

```
root@theserver# mount -t vfat /dev/sda1 /mnt/usbstore
```

#### 用户友好性

越来越多的发行版允许非特权用户访问可移动设备，并自动挂载 USB 设备、CD-ROM 等。

请注意，本指南要求系统中安装了 USB 支持。如果不起作用，请参阅 [USB 指南](http://www.linux-usb.org/USB-guide/) 寻求帮助。使用 dmesg 检查 /dev/sda1 是否确实是您要挂载的设备。

然后你可以开始实际的备份，例如对 /home/karl 目录进行备份：

```
karl@theserver:-> rsync -avg /home/karl /mnt/usbstore
```

通常，请参考手册页以获取更多详细信息。

## 9.4 加密

### 9.4.1 一般说明

#### 9.4.1.1 为什么你应该加密数据？

加密是保密的同义词。在备份的背景下，加密可能非常有用，例如，如果你需要将备份的数据存放在你无法控制访问权限的地方，比如你的服务提供商的服务器上。

除此之外，加密还可以应用于电子邮件：通常，邮件不加密，并且经常在网络上或互联网上公开发送。如果你的消息包含敏感信息，最好对其进行加密。

#### 9.4.1.2 GNU 隐私保护器

在 Linux 系统上，你会找到 GnuPG（GNU 隐私保护器），这是一套与商业可用的 PGP（Pretty Good Privacy）工具兼容的程序。

在本指南中，我们仅讨论加密工具非常简单的用法，并展示你需要生成加密密钥以及使用该密钥为自己加密数据所需的步骤，然后你可以安全地将这些数据存储在公共位置。更高级的使用说明可以在各种命令的手册页中找到。

### 9.4.2 生成密钥

在你开始加密数据之前，你需要创建一对密钥。这对密钥由一个私钥和一个公钥组成。你可以将公钥发送给通信方，他们可以使用它为你加密数据，然后你用你的私钥解密。你始终保留私钥，绝不与其他任何人共享，否则他们将能够解密仅发给你个人数据。为了确保不会发生意外，私钥受密码保护。使用以下命令创建密钥对：

```bash
willy@ubuntu:~$ gpg --key-gen
gpg (GnuPG) 1.4.2; Copyright (C) 2005 Free Software Foundation, Inc.
This is a free program, and you are welcome to redistribute it
under certain conditions.  See the file COPYING for details.

gpg: directory "/home/willy/.gnupg" created
gpg: new configuration file "/home/willy/.gnupg/gpg.conf" created
gpg: WARNING: options in "/home/willy/.gnupg/gpg.conf" are not yet
active during this run

gpg: keyring "/home/willy/.gnupg/secring.gpg" created
gpg: keyring "/home/willy/.gnupg/pubring.gpg" created
Please select what kind of key you want:
  (1) DSA and Elgamal (default)
  (2) DSA (sign only)
  (5) RSA (sign only)
Your selection? 1
DSA keypair will have 1024 bits.
GPG keys may be between 1024 and 4096 bits long.
What keysize do you want? (2048) 4096
Requested keysize is 4096 bits
Please specify how long the key should be valid.
         0 = key does not expire
        <n>  = key expires in n days
        <n>w = key expires in n weeks
        <n>m = key expires in n month
        <n>y = key expires in n years
Key is valid for: (0) 0
Key does not expire at all
```

是否正确？ (y/n) **y**

你需要一个用户 ID 来标识你的密钥：软件将用户 ID 构建为“真实姓名、注释和电子邮件地址”的形式：“Heinrich Heine (Der Dichter) <heinrichh@duesseldorf.de>”

真实姓名：**Willy** De Wandel  
电子邮件地址：**wdw@mvvg.vl**  
注释：**Willem**  
你选择的 USER-ID 为：  
“Willy De Wandel (Willem) <wdw@mvvg.vl>”

更改 (N)ame、(C)omment、(B)mail 还是 (O)key？(Q)uit？ **O**

你需要一个密码来保护你的私钥。

密码：

现在输入你的密码。这可以是一个短语，越长越好，唯一的要求是你随时都能记住它。为了验证，你需要再次输入相同的短语。

现在密钥对是由一个生成随机数的程序生成的，该程序除了其他因素外，还由系统的活动数据提供输入。因此，现在启动一些程序、移动鼠标光标或在终端窗口中键入一些随机字符是个好主意。这样，生成包含许多不同数字的随机数的机会会更大，密钥将更难破解。

### 9.4.3 关于你的密钥

当你的密钥创建完成后，你会收到一条关于*指纹*的消息。这是一串 40 位十六进制数字，它非常长，使得在任何计算机上两次生成相同密钥的可能性极低。你可以相当确信这是一个唯一的序列。此密钥的简短形式由你的姓名 followed by 最后 8 位十六进制数字组成。

你可以按以下方式获取关于你密钥的信息：

```
willy.ubuntu:~$ gpg --list-keys
/home/willy/./.gnupg/pubring.gpg
-----------------------------------
pub 1024D/BF5C3DBB 2006-08-08
uid Willy De Wandel (Willem) <wdw@mvvg.vl>
sub 4096g/A3449CF7 2006-08-08
```

该密钥的*密钥 ID* 是 "BF5C3DBB"。你可以将你的密钥 ID 和你的姓名发送给*密钥服务器*，以便其他人获取你的这些信息并使用它为你加密数据。或者，你可以直接将你的公钥发送给需要的人。你的密钥的公部分是一长串数字，当你使用 `gpg` 命令的 `--export` 选项时可以看到：

```
gpg --export -a
```

然而，就本指南而言，我们假设你只需要你的密钥来为自己加密和解密数据。如果你想了解更多，请阅读 gpg 手册页。

### 9.4.4 加密数据

现在你可以加密 .tar 归档文件或压缩归档文件，然后再将其保存到备份介质或传输到备份服务器。按如下方式使用 gpg 命令：

```
gpg -e -r (part of) uidarchive
```

-e 选项告诉 gpg 进行加密，-r 选项指示为谁加密。请记住，只有跟随在此 -r 选项后面的用户名才能再次解密该数据。示例：

```
willy@ubuntu:~$ gpg -e -r Willy /var/tmp/home-willy-20060808.tar
```

### 9.4.5 解密文件

使用 -d 选项，你可以解密为你加密的文件。数据会在你的屏幕上滚动，但加密副本将保留在磁盘上。因此，对于纯文本以外的文件格式，你可能希望保存解密后的数据，以便你可以用相应的程序查看它们。这是通过使用 gpg 命令的 -o 选项完成的：

```
willy@ubuntu:~$ gpg -d -o /var/tmp/home-willy-decrypt.tar /var/tmp/home-willy-20060808.tar.gpg
```

你需要一个密码来解锁用户 "Willy De Wandel (Willem) <wdwmwg.vl>" 的私钥 4096 ELG-E key, ID A3449CF7, created 2006-08-08 (main key ID BF5C3DBB)

```
gpg: encrypted with 4096-bit ELG-E key, ID A3449CF7, created 2006-08-08 "Willy De Wandel (Willem) <wdwmwg.vl>"
```

![](img/996aa590a5237ef824c7c29efdbb64f8_213_0.png)

#### 没有密码 = 没有数据

如果你记不起你的密码，数据就会丢失。即使是系统管理员也无法解密数据。这就是为什么重要密钥的副本有时会被存放在银行的安全保险箱中。

## 9.5 总结

以下是涉及文件备份的命令列表：

