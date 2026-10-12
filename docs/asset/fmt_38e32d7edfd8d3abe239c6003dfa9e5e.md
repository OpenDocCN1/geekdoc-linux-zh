
你可能需要重启 XAMPP 来完成恢复。

# 第 16 章 在 DSL 中设置 XAMPP Web 服务器

同样，你需要输入 MySQL root 密码才能将文件恢复到 MySQL 数据库。文件恢复后，如消息所示，你可能需要重启 MySQL 服务器以完成恢复（输入 `/opt/lampp/lampp restart`）。

## 总结

XAMPP 是一个强大的 Web 服务器解决方案，它结合了提供内容所需的组件，包括脚本语言（PHP、PEAR 和 Perl）、数据库表（MySQL）、FTP 服务（ProFTPD）以及理当然的 HTTP 服务（Apache）。XAMPP 的所有部分都包含在一个目录结构中，由于有 Linux 版本，它在 Damn Small Linux 中几乎可以开箱即用。

本章描述了如何在 Damn Small Linux 中获取和安装 XAMPP。它还告诉了如何配置 XAMPP、添加 Web 内容并保存所有设置，以便服务器在重启后继续工作。特别是，本章中的描述可以帮助你将 DSL XAMPP 服务器和所有内容存储在小于 256MB 的 USB 闪存上。

本页故意留白

# 第五部分

# 附录

- 附录 A CD 上的 341
- 附录 B 使用 MyDSL 扩展 345

本页故意留白

# 附录 A

# 在 CD 上

随书附赠的 CD 代表了 Damn Small Linux 项目制作的不同版本的 Damn Small Linux 的整合。它包含一些用于重新制作 Damn Small Linux 的额外工具，以及一些对于构建书中描述的项目特别有 MyDSL 扩展。

该 CD 部分是可启动的 Damn Small Linux，部分是 Damn Small Linux 软件仓库。它的设计不仅可以直接启动作为一个普通的 Damn Small Linux 镜像，还可以启动增强版本的 Damn Small Linux，用于创建在书中提到的不同项目。

> 注意：如果你无法从随书的 CD 启动 Damn Small Linux，请尝试禁用阻止启动过程的硬件项目。添加启动帮助屏幕上显示的选项（按 F2）或如 `acpi=off` 或 `nodma` 等选项。如果失败，请尝试搜索 `www.damnsmalllinux.org` 你的电脑型号，看看其他人在该类型电脑上使用 DSL 是否遇到了问题。

CD 还包含你可以在 Windows 桌面环境中运行 DSL 的软件（只需插入 CD 并选择正确的 `.bat` 文件运行）。还有一些工具可以帮助你重新制作 DSL。

341

官方 Damn Small Linux 教程

以下列表描述了 CD 中包含的软件：

- **官方 Damn Small Linux (`dsl-3.3.iso`)**——只需在启动提示符处按回车或输入 `dsl`，标准的 Damn Small Linux 就会启动。这是 Damn Small Linux 的 olinux 版本，意味着它可以启动大多数近年的 BIOS 电脑。按 F2 或 F3 功能键查看你可以添加到 `dsl` 启动命令的选项，以不同方式运行 Damn Small Linux。另有说明，这就是你应该使用的版本。

# 附录 B MyDSL 扩展

| 标题 | 描述 / 版本 / 站点 / 大小 | 备注 |
| --- | --- | --- |
| 扩展 | | | |
| `abiword.ds1` | AbiWord 文本处理器 / 2.0.1 / http://www.abisource.com/ 8.4MB | 一个免费的文字处理程序。类似于 Microsoft Word。 |
| `antiword.ds1` | Word 文转换器 / 0.32-2 / http://www.winfield.demon.nl/index.html / 86KB | 将 6, 7, 97 和 2000 版本的 doc 转换为文本或窗口的 PostScript。该包没有菜单项，因为它通过命令行调用。 |

# 官方 Damn Small Linux 书

| 标题 | 描述 / 版本 / 站点 / 大小 | 备注 |
| --- | --- | --- | --- |
| 扩展 | | | |
| `gtkfind.dsl` | 文件系统搜索工具 / 25KB | | 根据名称、访问时间、修改时间、类型和所有者搜索文件。 |

本页特意留白

# 索引

# 数字

- `7color-theme.tar.gz` 扩展名, 385
- `8211.o` 扩展名, 406
- `855patch` 扩展名, 407

# A

- `abe-sd1.dsl` 扩展名, 354
- `abiword.dsl` 扩展名, 346
- `abs-guide.uci` 扩展名, 387

# B

- `bc.dsl` 扩展名, 346
- `bittorrent-cli.dsl` 扩展名, 372
- `blender223.dsl` 扩展名, 365

# C

- `camserv.dsl` 扩展名, 365
- `cbb-gtk2-0.79.dsl` 扩展名, 362
- `cdparanoia-9.8` 扩展名, 365

# D

- `dsl-3.3.iso` 文件, 342
- `dsl-config.zip`, 228
- `dsl-cube.tar.gz` 扩展, 356

# E

- `e16.uci` 扩展, 389
- `easytag-1.0.dsl` 扩展, 365
- `eboard.dsl` 扩展, 356

# F

- `feh.unc` 扩展, 403
- `festival.unc` 扩展, 403
- `figurine.dsl` 扩展, 347

# G

- `gaim-1.5.0.unc` 扩展, 403
- `gambas.dsl` 扩展, 347

# H

- `httpd.conf` 文件, 326-327

# I

- `inform.uci` 扩展, 391
- `install` 命令, 156

# J

- `jhead.uci` 扩展, 391
- `jpilot.dsl` 扩展, 348

# K

- `k3b.dsl` 扩展, 367
- `kjvbible.dsl` 扩展, 348

# L

- `lame.dsl` 扩展, 367
- `latex2rtf.dsl` 扩展, 348
- `lifelines.dsl` 扩展, 348

# M

- `madwifi.dsl` 扩展, 381
- `makeimage` 脚本, 231-232
- `makeiso` 脚本, 232-233
- `man.uci` 扩展, 392

# N

- `nedit-5.5.uci` 扩展, 399
- `nmap-4.03.uci` 扩展, 399

# O

- `octave.tar.gz` 扩展, 349
- `openoffice-1.1.4-tar.gz` 扩展, 349

# P

- `p7zip-4.42.ds1` 扩展, 382
- `php-4-monkey-0.9.1.tar.gz` 扩展, 382
- `php.tar.gz` 扩展, 382

# Q

- `qiv.dsl` 扩展, 368
- `quake2.dsl` 扩展, 359

# R

- `rar.ds1` 扩展, 382
- `reiserfsprogs.ds1` 扩展, 382
- `ruby.ds1` 扩展, 382

# S

- `scite.dsl` 扩展, 351
- `soundmodem.dsl` 扩展, 351

# T

- `tcc.dsl` 扩展, 383
- `tcl_lib-blt.tar.gz` 扩展, 383
- `terminus_font.tar.gz` 扩展, 384

# U

- `uci` 扩展, 389-398
- `unionfs.ds1` 扩展, 384

# V

- `vba.dsl` 扩展, 361
- `vgui.ds1` 扩展, 384

# W

- `wine-0.9.22.dsl` 扩展, 384
- `wipe.ds1` 扩展, 385

# X

- `XFree86.ds1` 扩展, 385
- `xmms.dsl` 扩展, 370
- `xine.dsl` 扩展, 370

# 附录 B MySQL 扩展

| 标题 | 描述 / 版本 / 站点 / 大小 | 备注 |
| --- | --- | --- |
| 系统扩展 | | | |
| `libssh-0.11.dsl` | SSH 库 / 0/11 / http://0xbad0de.be | 这是一个 C 语言编写的 SSH 库。 |

# 官方 Damn Small Linux Book

| 标题 | 描述 / 版本 / 站点 / 大小 | 备注 |
| --- | --- | --- |
| 系统扩展 | | | |
| `p7zip-4.42.ds1` | Linux 版的 7-zip / 4.42 / http://www.7zip.org / 2.5MB | 强大的全功能归档工具。 |

本页特意留白
