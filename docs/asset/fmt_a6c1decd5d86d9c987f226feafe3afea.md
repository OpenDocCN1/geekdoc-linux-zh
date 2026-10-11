
下载：https://github.com/slicer69/sysvisnit/releases/3.06/sysvisnit-3.06.tar.xz

MD5: 9677da8831c51199830ea48b59ca

## Tar (1.34) - 214 KB:

主页：https://www.gnu.org/software/tar/

下载：https://ftp.gnu.org/gnu/tar/tar-1.34.tar.xz

MD5: 9a08d2a9ac47271305b708347c0cff5f

## Tcl (8.6.13) - 10581 KB:

主页：http://tcl.sourceforge.org/

下载：https://downloads.sourceforge.net/project/tcl/tcl8.6.13-sc.tar.gz

MD5: 0e4358ade2fd5b8ba6f2d9481ec2

## Tcl Documentation (8.6.13) - 1165 KB:

下载：https://downloads.sourceforge.net/tcl/tcl8.6.13-html.tar.gz

MD5: 4452ff26d575598ca1b7786d68eb

## Texinfo (7.0.2) - 4762 KB:

主页：https://www.gnu.org/software/texinfo/

下载：https://ftp.gnu.org/gnu/texinfo/texinfo-7.0.2.tar.xz

MD5: be9500f3a361552622850ecb1lb1fc024

## 时区数据 (2022) - 430 KB

主页：https://www.iana.org/time-zones

下载：https://www.iana.org/time-zones/releases/tzdata2022g.tar.gz

MD5: 884250f2d3a8a5563229004a94db93fb

## Udev-lfs 压缩包 (udev-lfs-20211102.tar.xz) - 11 KB:

下载：https://anduin.linuxfromscratch.org/Udev-lfs/

MD5: 27cd8f28f9a61422e186b9d6759ddf1634

## Util-linux (2.3.1) - 7321 KB:

主页：https://git.kernel.org/pub/scm/util-linux/util-linux.git/

下载：https://www.kernel.org/pub/linux/kernel/util-linux/v2.38/util-linux-2.38.tar.xz

MD5: cd11456ff4d3dd117bfbd99488c0c0d02

## Vim (9.0.1273) - 10892 KB:

主页：https://www.vim.org

下载：https://anduin.linuxfromscratch.org/LFS/vim-9.0.1273.tar.xz

MD5: 9c80755d29d5ec4ef713f6657671797

> 注意
>
> `vim` 的版本会发生。要获取最新版本，请访问 https://github.com/vim/vim/tags。

## Wheel (0.38.4) - 66 KB:

主页：https://pypi.org/project/wheel/

下载：https://pypi.org/packages/source/wheel/wheel-0.38.4.tar.gz

MD5: 83bb4e7bd4d6d87d398733f341a64ab91

- XML::Parser (2.46) - 24 KB:

  主页：https://github.com/chorny/XML-Parser

  下载：https://cpan.metacpan.org/authors/id/TO/TDDOR/XML-Parser-2.46.tar.gz

  MD5 和：80bb18a8e6240fc7ec2f7b57601c170

- XZ Utils (5.4.1) - 1451 KB:

  主页：https://tukaani.org/xz

  下载：https://tukaani.org/xz/xz-5.4.1.tar.xz

  MD5 和：478d31c659e94071d5dd384d0d1led4c6

- Zlib (1.2.13) - 126 KB:

  主页：https://www.zlib.net/

  下载：https://www.zlib.net/zlib-1.2.13.tar.xz

  MD5 和：79dc1cd778aefa38fe9bb77d00c3d

- Zstd (1.5.4) - 111 KB:

  主页：https://github.com/facebook/zstd

  下载：https://github.com/facebook/zstd/releases/v1.5.4.tar.gz

  MD5 和：235b2bf19cc74464104bb3d440ced

这些软件包的总大小：462 MB

## 所需补丁

除了软件包外，还需要若干补丁。这些补丁修复了软件包中应该由维护者修复的错误。补丁让对软件包的微调变得更容易。使用以下补丁我们需要构建 LFS 系统：

- BZip2 补丁 - 1.6 KB:

  下载：https://www.linuxfromscratch.org/patches/lfs/11.3/bzip2-1.0.8-install-patch

  MD5 和：6a5ac7eb9791ae55de0f749516f2

- Coreutils 国际化修复 - 166 KB:

  下载：https://www.linuxfromscratch.org/patches/lfs/11.3/coreutils-9.1-i18-patch

  MD5 和：c1acdec7f095027460165776da95

- Glibc FHS 补丁 - 2.8 KB:

  下载：https://www.linuxfromscratch.org/patches/lfs/11.3/glibc-2.37-fhs-patch

  MD5 和：9a5997c3452909b17691875eff2

- GRUB 上游修复补丁 - 8 KB:

  下载：https://www.linuxfromscratch.org/patches/lfs/11.3/grub-2.06-upstream-fixes-patch

  MD5 和：da389057110bbcbfc7bd7346ff9174

- Kbd 退格/删除补丁 - 12 KB:

  下载：https://www.linuxfromscratch.org/patches/lfs/11.3/kbd-2.5-backspace-patch

  MD5 和：f75cca16a38dacaa7d5215f7316895

- Readline 上游修复补丁 - 1.3 KB:

  下载：https://www.linuxfromscratch.org/patches/lfs/11.3/readline-8.2-upstream-fix-patch

  MD5 和：dd176b844fca6b67f44978218a75da

- Sysvinit 整合补丁 - 2.5 KB:

  下载：https://www.linuxfromscratch.org/patches/lfs/11.3/sysvinit-3.06-consolidated-patch

  MD5 和：17ffccbb8e18c39e8ced32046f3a75

这些补丁的总大小约为194.2 KB

除了上述必需补丁外，还有由 LFS 社区创建的可选补丁。这些补丁解决了小问题或启用了默认未开启的功能。请浏览 https://www.linuxfromscratch.org/patches/downloads/ 上的补丁数据库，根据系统需求获取任何额外补丁。

# 第4章 准备工作

## 4.1 引言

在本章中，我们将执行一些额外任务来准备构建临时系统。将在 LFS 中创建一组目录（我们在其中安装工具），添加一个无权限用户，并为该用户创建一个合适的构建环境。我们还将解释时间单位（我们使用 `SBU` 来衡量构建 LFS 软件包所需的时间），并提供有关软件包测试套的信息。

## 4.2 在 LFS 文件系统中创建受限的目录布局

在本节中，我们开始向 LFS 文件系统填充构成 Linux 系统的组件。第一步是创建一个受限的目录布局，以便第 6 章编译的程序（以及第 5 章的 `libstdc++`）安装在它们的最终位置。我们这样做是为了让这些临时程序在第 8 章构建最终版本时被覆盖。

以 `root` 身份运行以下命令创建所需的目录布局：
