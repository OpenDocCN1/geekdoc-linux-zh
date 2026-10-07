
```
[root@packaging ~] yum -y install rpm-build
Loaded plugins: fastestmirror
Setting up mirror
Loading mirror list from cache
* base: centros.com
* extras: mirrorlist
* updates: mirroring
Resolving Dependencies
Running transaction check
--> Package rpm-build.x86_64 0:4.8.0-47.el6 will be installed
--> Processing Dependency: patch >= 2.5 for package: rpm-build-4.8.0-47.el6
--> Processing Dependency: elutils >= 128 for package: rpm-build-4.8.0-47.el6
--> Processing Dependency: xz for package: rpm-build-4.8.0-47.el6
--> Processing Dependency: unzip for package: rpm-build-4.8.0-47.el6
--> Processing Dependency: system-config for package: rpm-build-4.8.0-47.el6
--> Processing Dependency: threads for package: rpm-build-4.8.0-47.el6
--> Processing Dependency: Queue for package: rpm-build-4.8.0-47.el6
--> Processing Dependency: GetOpt for package: rpm-build-4.8.0-47.el6
--> Processing Dependency: Type for package: rpm-build-4.8.0-47.el6
--> Processing Dependency: Basename for package: rpm-build-4.8.0-47.el6
--> Processing Dependency: lz for package: rpm-build-4.8.0-47.el6
--> Processing Dependency: /usr/bin/perl/add-index for package: rpm-build-4.8.0-47.el6
Running transaction check
--> Package elutils.x86_64 0:161-3.el6 will be installed
--> Package gdb.x86_64 0.7-83.el6 will be installed
--> Package patch.x86_64 2.6-6.el6 will be installed
--> Package perl.x86_64 4:5.10.1-141.el6 will be installed
--> Processing Dependency: perl-libs = 4:5.10.1-141.el6 for package: 4:5.10.1-141.el6
--> Processing Dependency: perl-libs for package: 4:5.10.1-141.el6.x86_64
--> Processing Dependency: perl(version) for package: 4:5.10.1-141.el6.x86_64
--> Processing Dependency: perl(Pod::Simple) for package: 4:5.10.1-141.el6.x86_64
--> Processing Dependency: perl(Module::Pluggable) for package: 4:5.10.1-141.el6.x86_64
--> Processing Dependency: libperl.so(64bit) for package: 4:5.10.1-141.el6.x86_64
--> Processing Dependency: redhat-rpm-config noarch:9.0.3-44.el86.centos will be installed
-- Package unzip.x86_64 0:6.0-2.el86 will be installed
-- Package xz.x86_64 0:4.999.9-0.5.beta.20091007git.el6 will be installed
-- Package xz-lzma-compat.x86_64 0:4.999.9-0.5.beta.20091007git.el will be installed
Running transaction check
-- Package perl-Module-Pluggable.x86_64 1:3.90-141.el86 will be installed
-- Package Dependency:perl-Pod-Simple.x86_64 1:3.13-141.el86 will be installed
-- Processing Dependency:perl(Pod::Escapes) >= 1.04 for package: 4:perl-Pod-Simple-3.13-141.el86_64 4:5.10.1-141.el86 will be installed
-- Package perl-version.x86_64 3:0.77-141.el86 will be installed
Running transaction check
-- Package perl-Pod-Escapes.x86_64 1:1.04-141.el86 will be installed
-- Finished Dependency Resolution
```

## Dependencies Resolved

| Package Arch Version Repository Size |
|=======================================|
| Installing:rpm-build.x86_64 4.8.0-47.el6 base 130 k |
| Installing for dependencies:
elutils.x86_64 0:161-3.el6 base 237 k |
| gdb.x86_64 0.7-83.el6 base 2.3 M |
| patch.x86_64 2.6-6.el6 base 90 k |
| perl.x86_64 4:5.10.1-141.el6 base 10 M |
| perl-Module-Pluggable.x86_64 1:3.90-141.el86 base 40 k |
| perl-Pod-Escapes.x86_64 1:1.04-141.el86 base 33 k |
| perl-Pod-Simple.x86_64 1:3.13-141.el86 base 213 k |
| perl-libs x86_64 4:5.10.1-141.el86 base 578 k |
| perl-version x86_64 3:0.77-141.el86 base 52 k |
| redhat-rpm-config noarch 9.0.3-44.el86.centos base 59 k |

| unzip.x86_64 0:6.0-2.el86 base 149 k |
| xz.x86_64 0:4.999.9-0.5.beta.20091007git.el6 base 137 k |
| xz-lzma-compat.x86_64 0:4.999.9-0.5.beta.20091007git.el base 16 k |

## 下载软件包：

| (1/14) | elfutils-0.161-3.el6 | 27 KB | 00:00 |
| (2/14) | gdb-7.2-83.el86.x86 | 2.3 MB | 00:07 |
| (3/14) | patch-2.6-6.el16.x86 | 90 KB | 00:00 |
| (4/14) | perl-5.10.1-141.el6 | 10 MB | 00:04 |
| (5/14) | perl-Module-Pluggable | 40 KB | 00:00 |
| (6/14) | perl-Pod-Escapes-1.0 | 33 KB | 00:00 |
| (7/14) | perl-Pod-Simple-3.13 | 213 KB | 00:00 |
| (8/14) | perl-libs-5.10.141 | 578 KB | 00:01 |
| (9/14) | perl-version-0.77 | 52 KB | 00:02 |
| (10/14) | redhat-rpm-config-9 | 59 KB | 00:00 |
| (11/14) | rpm-build-4.8.0.0 | 130 KB | 00:00 |
| (12/14) | unzip-6.0.2.el6.x | 140 KB | 00:00 |
| (13/14) | xz-4.999-9.0.5. | 137 KB | 00:00 |
| (14/14) | xz-lzma-compat-4.99 | 16 KB | 00:00 |

总计 114 kB/s | 14 MB | 02:07

warning: rmpts_HdrFromHeader: Verify VSA/RSA Signature, key ID c01b5b9de:nkey

正在从 `/etc/pki/rpm/RPM-GPG-KEY-CentOS-6` 获取密钥

导入密钥 C01b5b9de:
用户 ID : CentOS-6 (CentOS 6 官方签名密钥) <centos-key@centos.org>
软件包 centos-release-6.7.el6.102.3.x86_64 (anaconda-CentOS15080422.x86_64/7)

来自： `/etc/pki/rpm/RPM-GPG-KEY-CentOS-6`
正在运行 rpm_check_debug
正在运行事务测试
事务成功
正在运行事务

- 正在安装：xz-4.999-9.0.5.beta.20091007 1/14
- 正在安装：xz-lzma-compat-4.999-0.5.b 2/14
- 正在安装：perl-Pod-Escapes-1.04.141.el6 3/14
- 正在安装：perl-version-0.77-141.el6 4/14
- 正在安装：perl-Module-Pluggable-3.90 5/14
- 正在安装：perl-libs-5.10.1-141.el6 6/14
- 正在安装：perl-Pod-Simple-3.13-141.el6 7/14
- 正在安装：perl-libs-5.10.141.el6.x86_64 8/14
- 正在安装：redhat-rpm-config-9-9.0.3.a 9/14
- 正在安装：unzip-6.0.2.el6.x86_64 10/14
- 正在安装：patch-2.6-6.el16.x86 11/14
- 正在安装：elfutils-0.161-3.el16.x86_64 12/14
- 正在安装：gdb-7.2-83.el86.x86 13/14
- 正在安装：rpm-build-4.8.0-47.el86.x86 14/14
- 正在验证：perl-Pod-Simple-3.13-141.el6 1/14
- 正在验证：gdb-7.2-83.el86.x86 2/14
- 正在验证：elfutils-0.161-3.el16.x86_64 3/14
- 正在验证：perl-version-0.77-141.el6 4/14
- 正在验证：perl-Module-Pluggable-3.90 5/14
- 正在验证：xz-lzma-compat-4.999-0.5.b 6/14
- 正在验证：patch-2.6-6.el16.x86 7/14
- 正在验证：unzip-6.0.2.el6.x86_64 8/14
- 正在验证：xz-4.999-9.0.5.beta.20091007 9/14
- 正在验证：perl-Pod-Escapes-1.04.141.el6 10/14
- 正在验证：perl-libs-5.10.1-141.el6 11/14
- 正在验证：4:perl-libs-5.10.1-141.el.x 12/14
- 正在验证：redhat-rpm-config-9.0.3-44.e 13/14
- 正在验证：4:perl-5.10.1-141.el6.x86_64 14/14

已安装：
rpm-build.x86_64 0:4.8.0-47.el6

已安装依赖：
elfutils.x86_64 0:0.161-3.el6
gdb.x86_64 0:7.2-83.el86
patch.x86_64 0:2.6-6.el16
perl.x86_64 0:5.10.1-141
perl-Module-Pluggable.x86_64 0:3.90
perl-Pod-Escapes.x86_64 0:1.0-141
perl-Pod-Simple.x86_64 0:3.13-141
perl-libs.x86_64 0:5.10.1-141
perl-version.x86_64 0:0.77-141
redhat-rpm-config.noarch 0:9.0.3-44
unzip.x86_64 0:6.0.2.el6
xz.x86_64 0:4.999-9.0.5.beta.20091007
xz-lzma-compat.x86_64 0:4.999-0.5.b

你现在拥有了创建 RPM 的必要工具。

# 第 2 章：创建一个 RPM

RPM 有两种类型：源 RPM（称为 SRPM）和二进制 RPM（后者是执行代码）。二进制 RPM 不包含任何源代码，它是最终的软件包。

开始之前，我们将为 RPM 构建创建一个目录：

```bash
mkdir -p ~/rpmbuild/BUILD ~/rpmbuild/RPGS ~/rpmbuild/RPMS ~/rpmbuild/SOURCES
```

然后进入该目录：

```bash
cd ~/rpmbuild
```

现在我们将创建一个 spec 文件。该文件是 RPM 的核心，告诉 `rpmbuild` 如何构建软件包。

```bash
vi my-rpm.spec
```

在 spec 文件中，添加以下内容：

```spec
Name: my-rpm
Version: 1.0
Release: 1
Summary: 这是一个测试 RPM
License: none
Description:
我的测试 RPM
```

保存 spec 文件后，我们将运行 `rpmbuild` 来创建 RPM：

```bash
rpmbuild -bb my-rpm.spec
```

这将 RPM 文件创建在 `~/rpmbuild/RPMS/` 目录下。

现在我们可以使用 `rpm -q` 命令检查该 RPM 文件：

```bash
rpm -q ~/rpmbuild/RPMS/x86_64/my-rpm-1.0-1.x86_64.rpm
```

输出将显示我们刚刚创建的 RPM 文件的元数据。

# 第 3 章：rpmbuild 的输出

`rpmbuild` 命令的输出将显示它构建软件包时正在执行的步骤。以下是输出示例：

（请参见上方的输出）

## 第 3 章：创建一个实用的二进制 RPM

现在你可以创建一个 RPM 文件了，你可以开始向其中添加文件，并开始为软件包指定各种看起来很专业的元数据。我们将从元数据开始。上一节末尾显示的许多 `rpm -qip` 输出看起来，这些 RPM 就像是由一个几乎不会制作 RPM 的人创建的，而且只要弄出一个稍微有点能用的东西就停止了。我们可以做得好得多，而且这并不困难！

在 `rpm -qip` 输出的左侧列中，我们的情况还不错。我们可以指定该包属于哪个包组（建议组的列表请参见附录 D）。

第二列是更多的管理信息，包括许可信息。许可这个主题值得稍微题题一下：

### 许可

在第二列中，我们没有指定供应商（Vendor）或许可类型（License）。如果打包者（Packager）与供应商不同，也可以指定打包者（例如，红帽公司可能会对 Apache 软件基金会创建的软件进行打包，以将其包含在 Red Hat Enterprise Linux 中，使 ASF 为供应商，而 Red Hat 为打包者）。对于软件包的第一个版本，我们实际上指定了许可为“none”，因为如果你不放入任何文本，`rpmdbbuild` 将拒绝创建软件包。在没有某种许可的情况下分发任何东西是没有意义的。GPL 和 BSD 许可是 GNU/Linux 发行版中最常见的。你也可以同样地在这里指定专有软件许可。通常情况下使用“Proprietary”一词。无论许可是什么，在软件包中包含一个许可文本文件是常见的。在基于 Red 的系统中，这通常位于 `/usr/share/doc/{name}-{version}/LICENSE`。例如，Red 6 上的 `ethtool` 包带有这些文件：

```
[rpmpackaging SPECS]$ rpm ql ethtool
/sbin/ethtool
/usr/bin/ethtool
/usr/share/doc/ethtool-3.5/AUTHORS
/usr/share/doc/ethtool-3.5/COPYING
/usr/share/doc/ethtool-3.5/ChangeLog
/usr/share/doc/ethtool-3.5/LICENSE
```
