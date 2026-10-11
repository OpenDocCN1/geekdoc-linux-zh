
如果你为 LFS 使用了多个分区（例如，一个用于 `/`，另一个用于 `/home`），请按如下方式挂载：

```
mkdir -pv $LFS
mount -v -t ext4 /dev/<xxx> $LFS
mkdir -v $LFS/home
mount -v -t ext4 /dev/<yyy> $LFS/home
```

将 `<xxx>` 和 `<yyy>` 替换为相应的分区名称。

确保你的文件系统挂载权限不是过于严格（例如 `nosuid` 或 `nodedev` 选项）。运行不带任何参数的 `mount` 命令以查看 LFS 分区设置了哪些选项。如果设置了 `nosuid` 或 `nodedev`，则必须重新挂载该分区。

> 上述指令假设你在整个 LFS 过程中不会重启计算机。如果你关闭了系统，则每次重新启动构建过程时都需要重新挂载 LFS 分区，或者修改主机系统的 `/etc/fstab` 文件以便在重启时自动重新挂载。例如，你可以在你的 `/etc/fstab` 文件中添加此行：

| /dev/<xxx> | /mnt/lfs ext4 | defaults | 1 | 1 |

如果你使用了额外的选项，请确保也添加它们。

如果你正在使用交换分区，请确保使用 `swapon` 命令将其启用：

```
/sbin/swapon -v /dev/<zzz>
```

将 `<zzz>` 替换为 `swap` 分区的名称。

现在新的 LFS 分区已经可以使用了，是时候下载软件包了。

# 第 3 章 软件包与补丁

## 3.1. 引言

本章包含了构建基础 Linux 系统需要下载的软件包列表。列出的版本号对应于已知良好的软件版本，本书基于这些版本编写。我们强烈建议不要使用不同的版本，除非 LFS 错误说明或安全公告指定了该版本，否则一个版本的构建命令可能无法适用于另一个版本。最新的软件包也可能存在需要变通措施的问题。这些变通措施将在本书开发版本中开发并稳定。

对于某些软件包，发布压缩包（release tarball）和发布的（Git 或 SVN）仓库快照的压缩包可能具有相似的文件名。发布压缩包包含了生成的文件（例如，由 autoconf 生成的 `configure` 脚本），外还有仓库快照的内容。本书尽可能使用发布压缩包。使用仓库快照而不是发布压缩包将给你带来麻烦。

下载位置可能无法访问。如果自本书出版以来，包的下载位置发生了变化，Google（https://www.google.com/）为软件包提供了实用的搜索引擎。如果此类搜索失败，请尝试从 https://linuxscratch.org/mirrors 的其他替代方案下载。下载的软件包和补丁需要存放在整个构建过程中方便访问的地方。可以使用 `$LFS/sources` 作为存储压缩包和补丁的工作目录。要创建此目录，请在开始下载之前，使用 root 权限执行以下命令：

```
mkdir -v $LFS/sources
```

将此目录设置为粘位（"Sticky"），这样如果多个用户对目录具有写权限，只有文件所有者才能删除它。以下命令将启用写和粘位模式：

```
chmod -v a+wt $LFS/sources
```

有几种方法可以获取构建 LFS 需要的所有软件包：

- 可以如后续章节描述的那样单独下载文件。
- 对于本书的稳定版本，可以从 https://linuxscratch.org/mirrors 的其中一个站点下载所有所需文件的压缩包。
- 可以如下文所示使用 `wget-list` 下载文件：

```
wget --file=wget-list --directory-prefix=$LFS/sources
```

此外，在 LFS-0 中，有一个单独的文件 `md5sums`，可用于验证所有正确的软件包均可用。将该文件放在 `$LFS/sources` 并执行：

```
pushd $LFS/sources
md5sum -c md5sums
```

如果以非 root 用户身份下载软件包，它们将属于你。为了避免此问题，请将所有者更改为 root：

```
chown root $LFS/*
```

## 3.2. 所有软件包

在下载软件包之前阅读安全公告，以确定是否应使用软件包的更新版本。上游移除了旧版本，特别是那些存在漏洞的版本。如果某个 URL 不可用，请尝试从镜像下载。

下载以下软件包：

- acl (2.3.2) - 363 KB

  首页：https://savannah.gnu.org/projects/acl

  下载：https://download.savannah.gnu.org/releases/acl-2.3.2.tar.xz

  MD5 校验：590765daee5907dc3c856cf725bd69

- Attr (2.5.2) - 484 KB

  首页：https://savannah.gnu.org/projects/attr

  下载：https://download.savannah.gnu.org/releases/attr-2.5.2.tar.gz

  MD5 校验：22043ac2f6ca030948d5517

- Autoconf (2.72) - 1360 KB

  首页：https://www.gnu.org/software/autoconf

  下载：https://ftp.gnu.org/autoconf/autoconf-2.72.tar.xz

  MD5 校验：1be79f7106ab676f18391c5e22be701

- Automake (1.16.5) - 1565 KB

  首页：https://www.gnu.org/software/automake

  下载：https://ftp.gnu.org/automake/automake-1.16.5.tar.xz

  MD5 校验：4017a968f89fca45a946f1c5db6be71

- Bash (5.22.1) - 1096 KB

  首页：https://www.gnu.org/software/bash

  下载：https://ftp.gnu.org/gnu/bash/bash-5.21.tar.gz

  MD5 校验：ad5b38410e3bf0e9bcc20e2765f5e3f9

- Bc (6.7.5) - 460 KB

  首页：https://git.gavinourd.com/gallon/bc

  下载：https://github.com/gavinourd/bc/releases/download/6.7.5/bc-6.7.5.tar.xz

  MD5 校验：e249b1f8f868d6bf71c157f72653dd3d

- Binutils (2.42) - 26,922 KB:

主页: https://www.gnu.org/software/binutils/

下载: https://www.gnu.org/pub/binutils/releases/binutils-2.42.tar.xz

MD5 和: a075178a9464551379bf63404087715

- Bison (3.8.2) - 2,752 KB:

主页: https://www.gnu.org/software/bison/

下载: https://ftp.gnu.org/gnu/bison/bison-3.8.2.tar.xz

MD5 和: c28b119f405a2340ffa7cccdc6629713

- Bzip2 (1.0.8) - 792 KB:

下载: https://www.gnu.org/pub/bzip2/bzip2-1.0.8.tar.gz

MD5 和: 67e05152680dc475a73382ef27500d0e5

- Check (0.15.2) - 760 KB:

主页: https://libcheck.github.io/

下载: https://github.com/libcheck/check/releases/download/0.15.2/check-0.15.2.tar.gz

MD5 和: 50faccede5a380415b12e9c574e0b2

- Coreutils (9.4) - 5,840 KB:

主页: https://www.gnu.org/software/coreutils/

下载: https://ftp.gnu.org/gnu/coreutils/coreutils-9.4.tar.gz

MD5 和: 459e9546074d28834aefe541f250025

- DejaGNU (1.6.3) - 608 KB:

主页: https://www.gnu.org/software/dejavnu/

下载: https://ftp.gnu.org/gnu/dejavnu/dejavnu-1.6.3.tar.gz

MD5 和: 68c5205c58236ea4447d6d1326b8221

- Diffutils (3.10) - 1,587 KB:
