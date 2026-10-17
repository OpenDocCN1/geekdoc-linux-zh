
```
make[1]: Entering directory '/home/rhertzog/kali/kali-book/samples/offsec-defaults-1.0'

dh_installdsettings --priority=90

make[1]: Leaving directory '/home/rhertzog/kali/kali-book/samples/offsec-defaults-1.0'

  dh_perl

  dh_link

  dh_strip_nondeterminism

  dh_compress

  dh_fixperms

  dh_installdeb

  dh_gencontrol

  dh_md5sums

dh builddeb

dpkg-deb: building package 'offsec-defaults' in '../offsec-defaults_1.0_all.deb'.

dpkg-genchanges  >../offsec-defaults_1.0_amd64.changes

dpkg-genchanges: info: including full source code in upload

dpkg-source --after-build offsec-defaults-1.0

dpkg-buildpackage: info: full upload; Debian-native package (full source is included)
```

## 10.3.3. 为 APT 创建软件包仓库

既然你拥有了自定义软件包，就可以通过 APT 软件包仓库进行分发。使用 `reprepro` 创建所需的仓库并填充它。这个工具相当强大，其手册页绝对值得一读。

软件包仓库通常托管在服务器上。为了将其与服务器上运行的其他服务适当分离，最好创建一个专门用于此服务的用户。在该专用用户账户中，你可以托管仓库文件，以及用于签名软件包仓库的 GnuPG 密钥：

```bash
apt install reprepro gnupg
```

```bash
adduser --system --group pkgrepo
```

Adding system user `pkgrepo` (UID 136) ...

Adding new group `pkgrepo` (GID 142) ...

Adding new user `pkgrepo` (UID 136) with group `pkgrepo` ...

Creating home directory `/home/pkgrepo` ...

```bash
chown pkgrepo ${tty}
```

```bash
su - -s /bin/bash pkgrepo
```

```bash
gpg --gen-key
```

gpg (GnuPG) 2.1.11; Copyright (C) 2016 Free Software Foundation, Inc.

This is free software: you are free to change and redistribute it.

There is NO WARRANTY, to the extent permitted by law.

gpg: directory `/home/pkgrepo/.gnupg` created

gpg: new configuration file `/home/pkgrepo/.gnupg/dirmngr.conf` created

gpg: new configuration file `/home/pkgrepo/.gnupg/gpg.conf` created

gpg: keybox `/home/pkgrepo/.gnupg/pubring.kbx` created

Note: Use "gpg --full-gen-key" for a fully featured key generation dialog.

GnuPG needs to construct a user ID to identify your key.

Real name: Offensive Security Repository Signing Key

Email address: repoadmin@offsec.com

You selected this USER-ID:

"Offensive Security Repository Signing Key <repoadmin@offsec.com>"

Change (N)ame, (E)mail, or (D)key/(Q)uit?  o

We need to generate a lot of random bytes. It is a good idea to perform some other action (type on the keyboard, move the mouse, utilize the disks) during the prime generation; this gives the random number generator a better chance to gain enough entropy.

...

gpg: `/home/pkgrepo/.gnupg/trustdb.gpg`: trustdb created

gpg: key B4EFD20D marked as ultimately trusted

gpg: directory '/home/pkgrepo/.gnupg/openpgp-revocs.d' created

gpg: revocation certificate stored as '/home/pkgrepo/.gnupg/openpgp-revocs.d/F8FE22F74F1B714E38DA6181B2F74F7B4EFD20D.rev'

public and secret key created and signed.

gpg: checking the trustdb

gpg: marginals needed: 1  complete needed: 1  trust model: PGP

gpg: depth: 0   valid:   1  signed:   0  trust: 0- 0q, 0m, 0m, 0f, 1u

pub  rsa2048/B4EFD20D 2016-06-17 [S]

     Key fingerprint = F8FE 22F7 4F1B 714E 38DA  6181 B2F7 74F7 B4EF 20D0

uid          [ultimate] Offensive Security Repository Signing Key <repoadmin@offsec.com>

sub  rsa2048/38035F38 2016-06-17 []
```

请注意，当提示输入密码短语时，你应该输入空值（并确认你不想保护你的私钥），因为你希望能够非交互式地签名仓库。还要注意，`gpg` 需要对终端进行写访问才能安全地提示输入密码短语；这就是为什么在作为 `pkgrepo` 启动 shell 之前，你更改了虚拟终端的所有权（由于你最初以 root 用户身份连接，因此它由 root 拥有）。

现在你可以开始设置仓库。`reprepro` 需要一个专用目录，在该目录内部，你必须创建一个 `conf/distributions` 文件，其中记录了软件包仓库中可用的分布版本：

```bash
mkdir -p reprepro/conf
cd reprepro
cat >conf/distributions <<END
Codename: offsec-internals
AlsoAcceptFor: unstable
Origin: Offensive Security
Description: Offsec's Internal packages
Architectures: source amd64 i386
Components: main
SignWith: F8FE22F74F1B714E38DA6181B2F74F7B4EFD20D
END
```
