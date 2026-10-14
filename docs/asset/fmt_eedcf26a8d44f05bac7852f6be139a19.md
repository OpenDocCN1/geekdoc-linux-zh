
```bash
# dpkg-deb --info postfix_2.1.5-1_i386.deb
new debian package, version 2.0.
size 798936 bytes: control archive=42708 bytes.
191 bytes 7 lines
10997 bytes 355 lines * config #/usr/bin/perl
1076 bytes 22 lines control
7613 bytes 119 lines md5sum
12842 bytes 465 lines * postinst #/bin/sh
914 bytes 41 lines * postrm #/bin/sh
6702 bytes 251 lines * preinst #/bin/sh
960 bytes 43 lines * prerm #/bin/sh
109 bytes 4 lines shlibs
76002 bytes 1505 lines templates
Package: postfix
Version: 2.1.5-1
Section: mail
Priority: extra
Architecture: i386
Depends: lib6 (>= 2.3.21), libdb4.2, debconf (>= 0.5), netbase, adduser (>= 3.4), dpkg (>= 1.8.3),
Recommends: mail-reader, resolveconf
Suggests: procmail, postfix-mysql, postfix-mysql
```

# 5 Debian 包管理系统

- 2. `preinst` 脚本（如果存在）在安装前运行以配置相关部分。许多 `preinst` 脚本会停止相关服务以防止安装过程中出现问题。
- 3. `dpkg` 现在会将 `confiles` 文件中列出的所有文件提取到临时目录，并将它们移动到 `/etc` 下的相应位置。同时，它会附加 `dpkg-new` 扩展，以防覆盖已有的文件。
- 4. `dpkg` 在本地系统的根目录下解压剩余的 `data.tar.gz` 压缩包（该目录可以通过 `dpkg` 的 `--dir` 选项覆盖）。
- 5. 现在，控制文件被放置在 `/var/lib/dpkg/info`，每个文件都以包名和点号作为前缀：例如 `postfix.confiles`。控制文件不会被安装，而是用于更新包数据库。
- 6. 最后，`dpkg` 在包数据库中将该包标记为“已解包”（`unpacked`）（见第 5.3.4 节）。

软件包在仅解包时是无法满足依赖关系的（见第 5.7.3 节）。虽然所有文件（标记为 `confiles` 的文件除外）都安装在相应的位置，但不能保证软件能够运行。

## 配置软件包

解包后，软件包将有机会进行无法硬编码到包载荷中的修改。这在需要本地系统特定数据，或者用户可以在安装时影响软件的情况下可能会发生这种情况。当 `dpkg` 安装软件包时，此步骤通常会自动执行。也可以通过告诉 `dpkg` 配置单个包来显式请求此操作。与解包阶段不同，`dpkg` 需要知道包名（而不是 DEB 文件的文件名）。

```
# dpkg --configure postfix
Setting postfix (2.1.5-1) ... ]
```

配置包含以下步骤：

- 1. 对于每一个具有本地修改的配置文件，`dpkg` 询问管理员。根据管理员的决定，该配置文件要么被包中提供的版本覆盖，要么保持原样（见第 5.3.3 节）。

## 5.3 处理软件包：dpkg

- 2. 所有配置文件就绪后，将运行 `postscript` 脚本（如果存在）。
如果软件包使用了 `debconf`，这将导致 `config` 脚本运行。`config` 脚本使用 `debconf` 从用户处获取参数值，如果这些值尚未 `debconf` 数据库中。
- 3. `postscript` 文件处理无法直接包含在包中的系统更改。这包括执行用户通过 `debconf` 的配置参数，以及创建设备节点和用户等任务。此外，服务通常由 `postinst` 启动。
- 4. 最后，`dpkg` 在包数据库中将包标记为“已安装”（`installed`）（见第 5.3.4 节）。

完成配置阶段后，软件包已安装且软件可完全运行。如果要求 `dpkg` 配置之前已配置过的软件包，上述命令将退出而不报告错误。

也可以指示 `dpkg` 一次性配置所有未配置（已打包）的软件包。如果没有剩余需要配置的软件包，命令将不返回错误并立即退出。

```
# dpkg --configure -a
... ]
```

### 5.3.3 配置文件的处理

如前所述，软件包可能包含两种类型的文件：安装后随后由 `dpkg` 管理的文件，以及所谓的 `confiles` ——预期由用户修改的配置文件。当 `dpkg` 愉快地覆盖第一类文件时。然而，配置文件会被特殊处理：

- 1. 在软件包的解包阶段，`dpkg` 将所有标记为 `confile` 的文件安装到其目标位置，并每个文件赋予 `.dpkg-new` 扩展以防止与任何现有文件冲突。
- 2. 在配置软件包时，`dpkg` 检查每个现有配置文件是否有修改（使用一组 MD5 检查；见下文）。如果发现修改，管理员必须选择覆盖或保留本地文件。
- 3. 如果保留本地文件，新的配置文件（带有 `.dpkg-new` 扩展安装）将被重命名为 `.dpkg-dist` 扩展。
- 4. 如果本地文件要被包中的配置文件替换，将被赋予 `.dpkg-old` 扩展并留在原处作为备份。

例如，`abcde` 包提供了 `/etc/abcde.conf`，它被标记为配置文件。`dpkg` 妥善处理它：

```
# dpkg --unpack abcde-2.0.3-1-all.deb
(Reading database ... 目前安装了 59575 个文件和目录).
Preparing to replace abcde-2.0.2-1 (using abcde-2.0.3-1-all.deb) ...
Unpacking abcde ...
# ls -F /etc/abcde.conf*
/etc/abcde.conf -> /etc/abcde.conf.dpkg-new
# dpkg --configure abcde ...
Setting up abcde (2.0.3-1) ...
Installing new version of config file /etc/abcde.conf
```

如果管理员对文件做了更改，`dpkg` 将被询问采取任何操作（第一个命令只是向文件添加了一行，从而模拟了修改）：

```
# echo >> /etc/abcde.conf
# dpkg --unpack abcde-2.0.3-1-all.deb
(Reading database ... 目前安装了 59575 个文件和目录).
Preparing to replace abcde-2.0.2-1 (using abcde-2.0.3-1-all.deb) ...
Unpacking abcde ...
# dpkg --configure abcde ...
Setting up abcde (2.0.3-1) ...
Installing new version of config file /etc/abcde.conf
```

如果管理员对文件做了更改，`dpkg` 将被询问采取任何操作（第一个命令只是向文件添加了一行，从而模拟了修改）：

```
# echo >> /etc/abcde.conf
# dpkg --unpack abcde-2.0.3-1-all.deb
(Reading database ... 目前安装了 59575 个文件和目录).
Preparing to replace abcde-2.0.2-1 (using abcde-2.0.3-1-all.deb) ...
Unpacking abcde ...
# dpkg --configure abcde ...
Setting up abcde (2.0.3-1) ...
Installing new version of config file /etc/abcde.conf
```

如果管理员对文件做了更改，`dpkg` 将被询问采取任何操作（第一个命令只是向文件添加了一行，从而模拟了修改）：

```
# echo >> /etc/abcde.conf
# dpkg --unpack abcde-2.0.3-1-all.deb
(Reading database ... 目前安装了 59575 个文件和目录).
Preparing to replace abcde-2.0.2-1 (using abcde-2.0.3-1-all.deb) ...
Unpacking abcde ...
# dpkg --configure abcde ...
Setting up abcde (2.0.3-1) ...
Installing new version of config file /etc/abcde.conf
```

识别伪代码：
