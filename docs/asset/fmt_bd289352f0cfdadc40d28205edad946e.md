
# `pkg_info`

`ImageMagick-5.2.7_2` An X11 package for display and interactive manipulation of

`analog-4.16` An extremely fast program for analyzing WWW logfiles

`apache-1.3.19` The extremely popular Apache http server. Very fast, very

`arc-5.21e_8` Create & extract files from DOS `.ARC` files

`aub-2.0_5` Assemble uasent binaries

`autoconf-2.13` Automatically configure source code on many Un*x platforms

`dict-1.4_9` Dictionary Server Protocol (RFC2229) client

`elm-2.4ME+68` A once-popular mail user agent, unofficial clone

`emacs-19.34b` GNU editing macros

您还可以通过 `-v` 开关获取任何单个软件包的大量信息。与 RPM 一样，FreeBSD 中的软件包名称由多个部分组成，以连字符分隔——先是软件包名称，然后是版本。然而，RPM 文件往往面向多个平台，因此软件包名称中的“平台”部分未被使用。相反，FreeBSD 软件包文件采用 `name-version.tgz` 的形式。这里有一个例子：`bzip-0.21.tgz`

软件包通常是 `.tgz` 文件（称为 `tarbals`），这是 `.tar.gz` 的简称。使用 tarbals 是 Unix 下归档目录结构的传统方式——您首先使用 `tar` 将目录打包到一个文件中，然后使用 `gzip` 对其进行压缩。要使用诸如 `pkg_info -v` 之类的工具，您需要指定完整的软件包名称，包括版本，如清单 14.2 所示。

## 列表 14.2 pkg_info 的详细输出

```
# pkg_info -v pgp-2.6.3ia

Information for pgp-2.6.3ia:

Comment:

PGP MIT or International version - Public-Key encryption for the masses

Depends on:

Description:

PGP (Pretty Good Privacy) is a public key encryption package

to protect E-mail and data files. It lets you communicate securely

with people you've never met, with no secure channels needed for

prior exchange of keys. It's well featured and fast, with sophisticated

key management, digital signatures, data compression, and good ergonomic

design.

WWW: http://www.pgpi.org/

Packing list:

Package name: pgp-2.6.3ia

CWD to /usr/local

File: man/man1/pgp.1.gz

Comment: MD5:a0ab17d1fe83aafl59cb80fa1abf5462

File: bin/pgp

Comment: MD5:625e99562f936a9d9b0c3c5d5a94ba9

File: lib/pgp/pgp.hlp

Comment: MD5:d5da3783ea26cb6f04b7584df4227866

File: lib/pgp/pgpdocl.txt

Comment: MD5:260ca85cd0263275cb7df6cd276e2b9f

File: lib/pgp/pgpdoc2.txt

Comment: MD5:e3defe467bf5c5c4809f8b5c13404a1

File: lib/pgp/language.txt

Comment: MD5:bce0f56b207846725fe7e4a612083ef

File: lib/pgp/config.txt

Comment: MD5:b2518ad2566a9a4bce071936311d3c93

Deinstall directory remove: lib/pgp

UNEXEC 'if [ -f %D/info/dir ]; then if sed -e '1,/Menu:/d'

_%D/info/dir | grep -q '^[*] '; then true; else rm %D/info/dir; fi; fi'
```

此列表告知您有关该包的所有必要信息——从它的长描述，到它的依赖项，再到它的打包列表（每个文件都列有“指纹”MD5 校验和，显示在其注释字段中）。某些文件附有额外信息，例如“卸载脚本”，这是包管理器在您移除此包时需要执行的任务。在此列表中，指定本地目录树（例如，`/usr/local/lib/pgp`）内的目录 `lib/pgp` 会在卸载时被删除。由此可以推断，该包在 `/usr/local/lib` 中为其自身的共享库创建了一个完整的文件夹；之所以能做到这一点，是因为共享库目录是递归搜索的。类似地，包管理器将把 `UNEXEC` 行作为 shell 脚本运行，以便在满足某些条件时删除 `/usr/local/info/dir` 文件。如您所见，编写良好且行为规范的包（几乎所有的包都是行为规范的）在移除时会干净地清除其系统痕迹，几乎不留下任何踪迹。

您如何知道此版本是最新的？您可以轻松通过使用 `pkg_version` 工具来确定这一点。它仅当安装了 ports 集合时才能工作——除非磁盘空间严重不足，否则应该安装 ports 集合。您将在本章稍后了解有关 ports 集合的更多详细信息，但理解 `pkg_version` 只需知道：ports 集合（如果保持最新）包含每个包当前版本的列表。`pkg_version` 工具将已安装的所有包的版本与在 ports 集合中找到的版本进行比较，并告诉您您的包是否已更新（参见列表 14.3）。

## 列表 14.3 pkg_version 的示例输出

```
# pkg_version -v

ImageMagick-5.2.7_2       <    needs updating (port has 5.2.9_1)

apache-1.3.19               =    up-to-date with port

arc-5.21e.8                 =    up-to-date with index

aub-2.0.5                   =    up-to-date with index

autoconf-2.13               =    up-to-date with index

bash-2.04                   *    multiple versions (index has 1.14.7,2.04)

bsc-2.8.2                   =    up-to-date with index

bulk_mailer-1.12            <    needs updating (index has 1.13)

bzip2-0.9.5d                <    needs updating (index has 1.0.1)

cclicant-4.8                <    needs updating (index has 2000c)

csup-16.1                   =    up-to-date with index

demonriser-1.0              =    up-to-date with index
```
