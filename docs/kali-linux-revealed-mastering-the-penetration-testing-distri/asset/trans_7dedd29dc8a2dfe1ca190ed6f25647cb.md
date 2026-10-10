
默认变更日志文件通常是合适的；将“初始发布”替换为更详细的说明应该就足够了：

```
offsec-defaults (1.0) unstable; urgency=medium

* Add salt minion's configuration file.
* Add an APT's sources.list entry and an APT's trusted GPG key.
* Override the settings schema defining the background picture.

-- Raphaël Hertzog <buxy@kali.org>  Thu, 16 Jun 2016 18:04:21 +0200
```

在示例中，我们将修改控制文件。我们会将 `Section` 字段改为 *misc*，并移除 `Homepage`、`Vcs-Cgit` 和 `Vcs-Browser` 字段。最后，我们将填写 `Description` 字段：

```
Source: offsec-defaults
Section: misc
Priority: optional
Maintainer: Raphaël Hertzog <buxy@kali.org>
Build-Depends: debhelper (>= 9)
Standards-Version: 3.9.8

Package: offsec-defaults
Architecture: all
Depends: ${misc:Depends}
Description: Default settings for Offensive Security
 This package contains multiple files to configure computers
 owned by Offensive Security.
.
 It notably modifies:
 - APT's configuration
 - salt-minion's configuration
 - the default desktop settings
```

rules 文件通常包含一组规则，用于在专用子目录（以生成的二进制包命名）中配置、构建和安装软件。然后，该子目录的内容会被归档到 Debian 包中，就像它是文件系统根目录一样。在这种情况下，文件将被安装到 `/etc/debian/offsec-defaults/` 子目录中。例如，为了使包最终安装 `/etc/apt/sources.list.d/offsec.list`，需要将文件安装到 `debian/offsec-defaults/etc/apt/sources.list.d/offsec.list`。rules 文件被用作 Makefile，其中包含一些标准目标（包括分别用于清理源目录和生成二进制包的 `clean` 和 `binary`）。

## 什么是 Makefile 文件？

你可能已经注意到，在 `dh_make` 输出的末尾有关于缺失 Makefile 的提示，以及提到它类似于 rules 文件。Makefile 是 make 程序使用的脚本文件；它描述了一组文件之间相互构建的规则以及依赖关系树。例如，程序可以从一组源文件构建而成。Makefile 文件以下列格式描述这些规则：

```
target: source1 source2 ...
	command1
	command2
```

此类规则的解读如下：如果某个源文件比目标文件更新，则需要使用 command1 和 command2 来生成目标文件。

注意，命令行必须以制表符（Tab）字符开头；还要注意，当命令行以短横线字符（-）开头时，命令失败不会中断整个过程。

虽然这个文件是过程的核心，但它仅包含使用 debhelper 工具提供的标准命令集所需的最少内容。`dh_make` 生成的文件就是这种情况。要安装大多数文件，我们建议通过创建以下 `debian/offsec-defaults.install` 文件来配置 `dh_install` 命令的行为：

```
apt/offsec.list apt/apt/sources.list.d/
apt/offsec.gpg etc/apt/trusted.gpg.d/
salt/offsec.conf etc/salt/minion.d/
images/background.png usr/share/images/offsec/
```

你也可以使用此文件来安装 gsettings 覆盖文件，但 debhelper 为此提供了一个专用工具（`dh_installgsettings`），因此你可以依赖它。首先，将你的设置放在 `debian/offsec-defaults.gsettings-override` 中：

```
[org.gnome.desktop.background]
picture-options='zoom'
picture-uri='file:///usr/share/images/offsec/background.png'
```

接下来，在 `debian/rules` 中覆盖 `dh_installgsettings` 调用，以将优先级提高到组织覆盖所期望的级别（根据手册页，这是 90）：

```bash
#!/usr/bin/bmake -f

%:
	dh $@

override_dh_installgsettings:
	dh_installgsettings --priority=90
```

至此，源包已准备就绪。剩下的工作只是使用之前用于重新构建包的相同方法来生成二进制包：在 `offsec-defaults-1.0` 目录内运行 `dpkg-buildpackage -us -uc` 命令：

```
$ dpkg-buildpackage -us -uc
dpkg-buildpackage: info: source package offsec-defaults
dpkg-buildpackage: info: source version 1.0
dpkg-buildpackage: info: source distribution unstable
dpkg-buildpackage: info: source changed by Raphaël Hertzog <buxy@kali.org>
dpkg-buildpackage: info: host architecture amd64
  dpkg-source --before-build offsec-defaults-1.0
fakeroot debian/rules clean
dh clean
  dh_testdir
  dh_auto_clean
  dh_clean
dpkg-source -b offsec-defaults-1.0
dpkg-source: info: using source format '3.0 (native)'
dpkg-source: info: building offsec-defaults in offsec-defaults_1.0.tar.xz
dpkg-source: info: building offsec-defaults in offsec-defaults_1.0.dsc
  debian/rules build
dh build
  dh_testdir
  dh_update_autotools_config
  dh_auto_configure
  dh_auto_build
  dh_auto_test
fakeroot debian/rules binary
dh binary
  dh_testroot
  dh_prep
  dh_auto_install
  dh_install
  dh_installdocs
  dh_installchangelogs
  debian/rules override_dh_installdsettings
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

既然你拥有了自定义软件包，就可以通过 APT 软件包仓库进行分发。使用 reprepro 创建所需的仓库并填充它。这个工具相当强大，其手册页绝对值得一读。

软件包仓库通常托管在服务器上。为了将其与服务器上运行的其他服务适当分离，最好创建一个专门用于此服务的用户。在该专用用户账户中，你可以托管仓库文件，以及用于签名软件包仓库的 GnuPG 密钥：

```bash
# apt install reprepro gnupg
[...]
# adduser --system --group pkgrepo
Adding system user `pkgrepo' (UID 136) ...
Adding new group `pkgrepo' (GID 142) ...
Adding new user `pkgrepo' (UID 136) with group `pkgrepo' ...
Creating home directory `/home/pkgrepo' ...
# chown pkgrepo ${tty}
# su - -s /bin/bash pkgrepo
$ gpg --gen-key
gpg (GnuPG) 2.1.11; Copyright (C) 2016 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

gpg: directory `/home/pkgrepo/.gnupg' created
gpg: new configuration file `/home/pkgrepo/.gnupg/dirmngr.conf' created
gpg: new configuration file `/home/pkgrepo/.gnupg/gpg.conf' created
gpg: keybox `/home/pkgrepo/.gnupg/pubring.kbx' created
Note: Use "gpg --full-gen-key" for a fully featured key generation dialog.

GnuPG needs to construct a user ID to identify your key.

Real name: Offensive Security Repository Signing Key
Email address: repoadmin@offsec.com
You selected this USER-ID:
"Offensive Security Repository Signing Key <repoadmin@offsec.com>"

Change (N)ame, (E)mail, or (D)key/(Q)uit?  o

We need to generate a lot of random bytes. It is a good idea to perform some other action (type on the keyboard, move the mouse, utilize the disks) during the prime generation; this gives the random number generator a better chance to gain enough entropy.
[...]
gpg: /home/pkgrepo/.gnupg/trustdb.gpg: trustdb created
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

请注意，当提示输入密码短语时，你应该输入空值（并确认你不想保护你的私钥），因为你希望能够非交互式地签名仓库。还要注意，gpg 需要对终端进行写访问才能安全地提示输入密码短语；这就是为什么在作为 pkgrepo 启动 shell 之前，你更改了虚拟终端的所有权（由于你最初以 root 用户身份连接，因此它由 root 拥有）。

现在你可以开始设置仓库。reprepro 需要一个专用目录，在该目录内部，你必须创建一个 `conf/distributions` 文件，其中记录了软件包仓库中可用的分布版本：

```
$ mkdir -p reprepro/conf
$ cd reprepro
$ cat >conf/distributions <<END
Codename: offsec-internals
AlsoAcceptFor: unstable
Origin: Offensive Security
Description: Offsec's Internal packages
Architectures: source amd64 i386
Components: main
SignWith: F8FE22F74F1B714E38DA6181B2F74F7B4EFD20D
END
```

必需的字段是 `Codename`，它给出分布的名称；`Architectures`，它指示哪些体系结构将在分布中可用（并且在输入端被接受）；以及 `Components`，它指示分布在中的各种组件（com-
