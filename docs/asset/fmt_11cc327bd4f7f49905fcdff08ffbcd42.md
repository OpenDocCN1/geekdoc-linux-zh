
在整书中，环境变量 `LFS` 将被多次使用。你应该确保该变量在整个构建过程中始终已定义。它应该被设置为你构建 LFS 的目录——我们将以 `/mnt/lfs` 为例，目录的选择由你决定。如果你在单独分区上构建 LFS，此目录将是挂载点。选择一个目录位置并使用以下命令设置变量：

```
export LFS=/mnt/lfs
```

设置此变量是有益的，例如 `mkdir -v $LFS/tools` 这样的命令可以直接字面输入。shell 在处理命令行时会自动将 `$LFS` 替换为 `mnt/lfs`（或你设置的任何值）。

> 注意

每当你离开并重新进入当前工作环境（例如切换到 root 或用户）时，不要忘记检查 `$LFS` 是否已设置。使用以下命令检查 LFS 变量是否设置正确：

```
echo $LFS
```

确保输出显示你 LFS 系统构建位置的路径，如果按照示例操作，应该是 `/mnt/lfs`。如果输出不正确，使用本页之前的命令将 LFS 设置为正确的目录。

确保 `$LFS` 变量始终设置的一种方法是编辑个人主目录以及 `/root/` 下的 `.bash_profile`，并确保包含上面的 `export` 命令。此外，`/etc/passwd` 文件中所有需要 LFS 变量的用户的 shell 都需要是 `bash`，以确保 `/root/.bash_profile` 作为登录过程的一部分被包含。

## 2.7. 挂载新分区

现在文件系统已经创建，需要让该分区变得可访问。为了做到这一点，需要将分区挂载到选定的挂载点。就本书而言，假设文件系统已挂载在上一节所述的 LFS 环境变量指定的目录下。

运行以下命令创建挂载点并挂载 LFS 文件系统：

```
mkdir -pv $LFS
mount -t ext4 /dev/<xxx> $LFS
```

将 `<xxx>` 替换为 LFS 分区的标识。

如果为 LFS 使用了多个分区（例如，一个用于 `/`，另一个用于 `/usr`），请使用以下命令挂载：

```
mkdir -pv $LFS
mount -t ext4 /dev/<xxx> $LFS
mdir -v $LFS/usr
mount -v ext4 /dev/<ggg> $LFS/usr
```

将 `<xxx>` 替换为相应的分区名称。

确保该分区的挂载权限不会过于严格（例如使用了 `nosuid` 或 `nodev` 选项）。在不带任何参数的情况下运行 `mount` 命令，以查看 LFS 分区设置了哪些选项。如果设置了 `nosuid` 和/或 `nodev`，则需要重新挂载分区。

> 警告

上述指令假设在整个 LFS 过程中不会重启计算机。如果你关闭了系统，则你需要在每次重启构建过程时重新挂载 LFS 分区，或者修改宿主机的 `/etc/fstab` 文件以便在启动时自动重新挂载。例如：

```
/dev/<xxx> /mnt/lfs ext4 defaults 1 1
```

如果你使用了额外的可选分区，请确保也将它们添加。

如果你正在使用交换分区（swap），请确保使用 `swapon` 命令将其启用：

```
/sbin/swapon -v /dev/<zzz>
```

将 `<zzz>` 替换为交换分区的名称。

现在已经建立了一个工作区域，是时候下载软件包了。

# 第 3 章 软件包与补丁

### 3.1. 引言

本章列出了构建基础 Linux 系统需要下载的软件包列表。列出的版本号对应于已知良好的软件版本，本书也基于这些版本。我们强烈建议不要使用更新的版本，因为一个版本的构建命令可能无法适用于较新的版本。最新的软件包版本可能存在需要规通措施的问题。这些规通措施将在本书的开发版本中开发并稳定。

下载地址并不总是可以访问的。如果自本书出版以来下载地址发生了变化，Google（http://www.google.com/）为大多数软件包提供了搜索引擎。如果这种方法没有成功，请尝试在 http://www.linuxfromscratch.org/lfs/packages.html#packages 中讨论的替代方法。

下载的软件包和补丁需要存储在在整个过程中都方便访问的地方。还需要一个工作目录来解压源码并进行构建。`$LFS/sources` 既可以作为存储源码和补丁的地方，也可以作为工作目录。通过使用该目录，所需的元素将位于 LFS 分区上，并在构建过程的所有阶段都可用。

要创建此目录，请在开始下载会话之前以 root 用户身份执行以下命令：

```
mkdir $LFS/sources
```

将此目录设置为可写并设置粘位位（sticky）。“粘位”意味着即使多个用户对目录具有写入权限，只有文件的所有者才能删除粘位目录内的文件。以下命令将启用写入和粘位模式：

```
chmod -v awt $LFS/sources
```

下载所有软件包和补丁的简单方法是将 `wget-list` 作为 `wget` 的输入。例如：

```
wget --input-file=wget-list --continue --directory-prefix=$LFS/sources
```

此外，从 LFS-7.0 开始，有一个单独的文件 `md5sums`，用于在继续之前验证软件包是否正确。将该文件放在 `$LFS/sources` 并运行：

```
cd $LFS/sources
md5sum -c md5sums
```

### 2.2. 所有软件包

下载或获取以下软件包：

- ACL (2.2.53) - 513 KB:

  下载：http://download.savannah.gnu.org/releases/acl-2.2.53.tar.gz

  MD5 sum：007aab1dbbb55bcde52

- Attr (2.4.8) - 457 KB:

  主页：http://savannah.gnu.org/projects/attr

  下载：http://download.savannah.gnu.org/releases/attr-2.4.8.tar.gz

  MD5 sum：1e5cb59d6b24886f527d3d

- Autoconf (2.69) - 1186 KB:

  主页：http://www.gnu.org/software/autoconf

  下载：http://ftp.gnu.org/gnu/autoconf-2.69.tar.xz

  MD5 sum：50f974f159805e37469a73e263f2ee

- Automake (1.16.1) - 1499 KB:

  主页：http://www.gnu.org/software/automake

  下载：http://ftp.gnu.org/gnu/automake-1.16.1.tar.xz

  MD5 sum：53f3be67591a57c532dee682268e5b

- Bash (5.0) - 9989 KB:

  主页：http://www.gnu.org/software/bash

  下载：http://ftp.gnu.org/gnu/bash-5.0.tar.xz

  MD5 sum：2b4b4b7b905be16f4570964f67182b

- Bc (2.1.3) - 233 KB:

  主页：https://github.com/gowinard/bc

  下载：https://github.com/gowinard/bc/archive/bc-2.1.3.tar.gz

  MD5：2a882dc39c0ff8e36c12f59d54cc09

- Binutils (2.32) - 20288 KB:

  主页：http://www.gnu.org/software/binutils

  下载：http://ftp.gnu.org/gnu/binutils-2.32.tar.xz

  MD5 sum：0d174c52855721043f52

- Bison (3.4) - 2147 KB:

  主页：http://www.gnu.org/software/bison

  下载：http://ftp.gnu.org/gnu/bison-3.4.tar.xz

  MD5 sum：201286a5f7475202385f44

- Bzip (1.0) - 792 KB:

  主页：https://github.com/gowinard/bc

  下载：https://github.com/gowinard/bc/archive/bc-2.1.3.tar.gz

  MD5：67e0512344855721043f52

- Check (12.0) - 747 KB:

  主页：http://github.com/check

  下载：https://github.com/check/releases/download/12.0/check-12.0.tar.gz

  MD5 sum：31b17520344155119529

- Coreutils (8.31) - 5284 KB:

  主页：http://www.gnu.org/software/coreutils
