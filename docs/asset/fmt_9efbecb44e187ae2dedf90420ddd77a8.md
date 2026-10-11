
```
$ apt source set
Reading package lists... Done
NOTICE: 'set' is maintained in the 'Git' version control system at https://gitlab.com/kalilinux/packages/set
Please use: git clone https://gitlab.com/kalilinux/packages/set
to retrieve the latest (possibly unreleased) updates to the package.
Need to get 2.3 MB of source.
dpkg-source: warning: failed to verify signature on ./set_7.4.4.dsc
dpkg-source: info: extracting set in set-7.4.4
dpkg-source: info: unpacking set-7.4.4.orig.gz
dpkg-source: info: unpacking set-7.4.4.xz
dpkg-source: info: applying config
$ wget https://github.com/trusted/social-engineer-toolkit/archive/7.4.5.tar.gz -O set_7.4.5.tar.gz
$ tar xvf set_7.4.5.tar.gz social-engineer-toolkit/set-7.4.5/src/wireless/attack.py
$ cp -a set-7.4.4/debian social-engineer-toolkit/set-7.4.5/debian
$ cd social-engineer-toolkit/set-7.4.5
$ dch -v 7.4.5-1 "New upstream release"
```

这就是你现在构建更新包的方法。根据上游版本引入的更改，你可能还需要更改构建运行时依赖并安装新文件。

### 9.1.4 开始构建

当所有更改应用到源码后，你可以开始生成实际的二进制包或 `.deb` 文件。整个过程由 `dpkg-buildpackage` 命令管理，看起来如下：

```
$ dpkg-buildpackage -us -b
dpkg-package: source package libfree
dpkg-package: source version 0.4.0-1
dpkg-package: distribution RELEASE
dpkg-package: created by Raphael Hertzog <raphael@kali.org>
dpkg-package: host architecture amd64
debuild
dpkg-deb: building package 'libfree-dbgsym' in .../libfree-dbgsym_0.4.0-1.amd64.deb
dpkg-deb: building package 'libfree' in .../libfree_0.4.0-1.amd64.deb
dpkg-deb: building package 'libfree-dev' in .../libfree-dev_0.4.0-1.amd64.deb
dpkg-deb: building package 'libfree-bin-dbgsym' in .../libfree-bin-dbgsym_0.4.0-1.amd64.deb
dpkg-deb: building package 'libfree-bin' in .../libfree-bin_0.4.0-1.amd64.deb
dpkg-deb: building package 'libfree-doc' in .../libfree-doc_0.4.0-1.all.deb
dpkg-changes -b ./libfree-doc_0.4.0-1.all.deb
dpkg-changes: binary-only upload (no source included)
dpkg-source -after-build libfree-0.4.0-1
dpkg-package: binary-only upload (no source included)
```

`-uc` 选项静用了某些生成文件（`.dsc`）的签名，因为如果你没有与 `changelog` 文件中身份相同的 GNU 密钥，操作将失败。`-b` 选项请求“仅二进制构建”。在这种情况下，不会创建源码包（`.dsc`），只会创建二进制包（`.deb`）。使用此方法可以避免源码包构建期间的失败：如果你没有在补丁管理系统中正确记录你的更改，它可能会报错并中断构建过程。

如 `dpkg-dev` 消息所示，生成的二进制包现在位于父目录中（源码包上目录）。你可以用 `dpkg -i` 或 `apt install` 安装它们。

```
$ sudo apt install ../libfree_0.4.0-1.amd64.deb \
../libfree-bin-0.4.0-1.amd64.deb
```

Reading package lists... Done

Building dependency tree

Reading state information... Done

Note, selecting 'libfree' instead of '../libfree0_0.4.0-1.amd64.deb'

Note, selecting 'libfree-bin' instead of './libfree-bin_0.4.0-1.amd64.deb'

The following packages will be upgraded:

libfree libfree0

2 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.

Need 0 B/69.4 KB of archives.

After this operation, 2048 B of additional disk space will be used.

我们更倾向于使用 `apt install dpkg -i`，因为它能优雅地处理生成的文件。但在此之前，你必须使用 `dpkg`，因为无法处理任何仓库之外的 `.deb` 文件。

| `dpkg-buildpackage` 包装器 | 多数情况下，Debian 开发者使用更高级的程序 `debbuild`；它像通常一样运行 `dpkg-buildpackage`，但还会调用一个程序（Lintian），该程序运行多次以验证生成的包是否符合 Debian 策略。该脚本会清理环境，防止本地环境变量污染包构建。默认命令是 `devsucripts` 中的工具之一，它们共享一些一致性和配置，以简化维护者的工作。 |

> ³https://www.debian.org/doc/debian-policy/

# 9.2. 重新编译 Linux 内核

Kali 提供的内核包含了尽可能的功能以及最大数量的驱动程序，以覆盖最广泛的现有硬件配置。这就是为什么某些用户倾向于重新编译内核，以便仅包含他们特定需要的内容。这种选择有两个原因：首先，这是优化内存消耗的一种方法，因为所有的内核代码即使从不使用，也会占用物理内存。由于内核的静态编译部分永远不会移动到交换空间（`swap space`），构建了从未使用的驱动程序和功能会导致系统性能整体下降。其次，减少驱动程序和内核功能的数量可以减少安全问题的风险，因为运行的只是可用内核代码的一小部分。

> 重要提示
>
> 如果你选择编译自己的内核，你必须接受后果：Kali 无法为你的自定义内核提供安全更新。通过保留 Kali 提供的内核，你将受益于 Debian 项目准备的更新。

如果你想使用某些以补丁形式提供（未包含在标准内核中）的功能，也需要重新编译内核。

| 《Debian 内核手册》 |  |
|---|---|
| http://kernel-handbook.alioth.debian.org | Debian 内核团队维护着《Debian 内核手册》（也可通过 `debian-kernel-handbook` 包获取），其中包含了关于大多数内核相关任务以及官方 Debian 内核包处理方式的全面文档。如果你需要比本节提供的更多的信息，这是你应该首先查找的地方。 |

## 9.2.1. 简介与准备工作

惊讶的是，Debian 和 Kali 以软件包的形式管理内核，而这并不是传统编译和安装内核的方式。由于内核仍然受软件包系统的控制，因此它可以被干净地删除，或者部署在多台机器上。此外，与这些包相关的脚本自动化了与引导程序（`bootloader`）和 `initrd` 生成器的交互。
