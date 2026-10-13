

这种方案包含两个密钥：一个私钥，由你自己保管；以及一个公钥，分发给他人。公钥——无论是你的，还是你想要发送加密文件的对象——被用来加密文件，只有关联私钥的持有者才能解密。第三个密钥——会话密钥——是自动生成的，用于加密和解密。然而，由于它在后台自动处理，在整个过程中很少被认为有贡献。

公钥加密系统最大的问题是资源密集。解密加密消息所涉及的数学运算非常庞大——远超单密钥方法（该方法中双方拥有完全相同的私钥，没有公钥——私钥用于加密和解密文件），而且处理速度明显更慢。单密钥方法的数学运算没有那么复杂，因为不需要在公钥和私钥之间建立数学关系。交换两端的单密钥匹配，因此不需要额外的数学计算。

两个采用公钥加密的加密软件包是Pretty Good Privacy（PGP）——正逐渐被GPG（GNU隐私卫士，PGP的一个开源实现）取代——以及OpenSSH（一个开源安全外壳）。有关OpenSSH的更多信息，请参见第37章“远程管理”。两者都可用于UNIX变体（如Linux）以及其他平台（每种都有Windows和Mac版本）。虽然只有将计算机断开连接并锁在储物柜里才能确保数据免受攻击，但在日常操作中使用加密可以大大降低数据受损的可能性。

本书将讨论GNU隐私卫士，因为随书附带的分发包中带有GPG。如果你用过PGP（尤其是2.6版）并习惯了它的语法，GnuPG RPM包含一个名为pgpgpg的兼容程序，它可以让你继续使用PGP语法，但会将其转换为gpg。

GnuPG（GPG）的主要用途是文件加密。它不在本地和远程系统之间建立安全通道，也不使用服务器/客户端拓扑。它只是对要与特定个人共享的数据进行加密，并设置用于在文件交换接收端确定数据完整性的标准。尽管GPG可用的各种平台都有许多界面，但GPG本身是命令行驱动的。可以传递给GPG的参数列表相当广泛，这里不会全部覆盖，只介绍更常见的功能。完整的命令和选项列表请参阅手册页。

## 设置GPG以供使用

安装了GPG后，你的第一个任务是为自己创建一对合法的公钥/私钥。请在以你计划最常登录的用户身份登录时执行此操作，或者以你打算在用GPG加密时使用的用户身份登录。确保在你的主目录下创建了.gnupg子目录（如果不存在，请使用mkdir创建一个）。如果你没有先创建目录，GPG会在第一次运行时创建它，但会中止，你必须再次运行该命令。

以下是用于生成密钥对的命令：

```text
gpg --gen-key
```

清单25.1是假用户Sherman T. Potter（其机器为rumble.fish.net）的密钥生成会话示例。

### 清单25.1 生成密钥对

```text
[stp@rumble stp]$ gpg --gen-key
gpg (GnuPG) 1.0.1; Copyright (C) 1999 Free Software Foundation, Inc.
This program comes with ABSOLUTELY NO WARRANTY.
This is free software, and you are welcome to redistribute it
under certain conditions. See the file COPYING for details.

gpg: /home/stp/.gnupg: directory created
gpg: /home/stp/.gnupg/options: new options file created
gpg: you have to start GnuPG again, so it can read the new options file
[stp@rumble stp]$ gpg --gen-key
gpg (GnuPG) 1.0.1; Copyright (C) 1999 Free Software Foundation, Inc.
This program comes with ABSOLUTELY NO WARRANTY.
This is free software, and you are welcome to redistribute it
under certain conditions. See the file COPYING for details.

gpg: /home/stp/.gnupg/secring.gpg: keyring created
gpg: /home/stp/.gnupg/pubring.gpg: keyring created
Please select what kind of key you want:
    (1) DSA and ElGamal (default)
    (2) DSA (sign only)
    (4) ElGamal (sign and encrypt)
Your selection?
DSA keypair will have 1024 bits.
About to generate a new ElG-E keypair.
              minimum keysize is 768 bits
                 default keysize is 1024 bits
        highest suggested keysize is 2048 bits
What keysize do you want? (1024)
Requested keysize is 1024 bits
Please specify how long the key should be valid.
             0 = key does not expire
            <n> = key expires in n days
           <n>w = key expires in n weeks
           <n>m = key expires in n months
           <n>y = key expires in n years
Key is valid for? (0)
Key does not expire at all
Is this correct (y/n)? y

You need a User-ID to identify your key; the software constructs the user id
from "Real Name, Comment and Email Address in this form:
    "Heinrich Heine (Der Dichter) <heinrich@duesseldorf.de>"

Real name: Sherman T. Potter
Email address: stp@fish.net
Comment:
You selected this USER-ID:
    "Sherman T. Potter <stp@fish.net>"
```

### 清单25.1（续）

```text
Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
You need a Passphrase to protect your secret key.

Enter passphrase:
Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
You need a Passphrase to protect your secret key.
Enter passphrase:
Reenter passphrase:

We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
++.++++++++++++++++++++++++++++++++++++.++++++++++.+++++++++++.++++++++.
................................................++++

Not enough random bytes available. Please do some other work to give
the OS a chance to collect more entropy! (Need 12 more bytes)
;Jaksjdf
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
++++++++++++++.+++++.++++++++++++++++++++.++++++++++.++++++++++.++++++++++++.
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++.++++++++++++^^^

public and secret key created and signed.
```

此时，私钥/公钥对已经可以使用。这两个文件——pubring.gpg（公钥环）和secring.gpg（秘密密钥环）——以二进制形式存储在$HOME/.gnupg目录中。保留所有这些文件不动，放在$HOME/.gnupg目录中。

## 操作公钥/私钥密钥环

如果没有人为你加密任何内容，这一切对任何人都没有多大用处。为了实现这一点，你必须共享你的公钥。

如果你最终经常使用GPG，你需要考虑将公钥发送到互联网上的一些公钥服务器；这样，人们就可以向你发送加密文件，而不用为你的公钥烦扰你。否则，你可以随身携带一份公钥副本，以备有人索要。

公钥可以采用两种形式：二进制和纯文本。默认情况下，你的pubring.gpg文件是二进制的，因此其中的所有密钥也是二进制的。默认提取过程会提取二进制版本的公钥。你可能需要ASCII装甲版本，因为即使允许将二进制写入屏幕也可能扰乱你的终端设置。以下命令可以做到：

```text
gpg -a --export youserid > youserid.pub.key.asc
```

youserID部分可以稍微调整，使其包含足够的字符来标识你想要提取的密钥。例如，如果Sherman T. Potter决定他想

