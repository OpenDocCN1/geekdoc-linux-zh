
如你所示，通过 RPM 安装软件包可以非常简单。

提示 如果如果你好奇的话，`lynx` 是一个基于文本的浏览器。你只需在 shell 提示符处输入 `lynx` 即可启动。要退出 `lynx`，只需按 `q` 键。你会在终端右下角看到一个提示，询问你是否要退出。按 `ENTER` 键确认。

如你所示，通过 RPM 安装软件包可以非常简单。但有时安装软件包可能会更加复杂，通常是因为依赖项失败或缺失。例如，在成功安装 `lynx` 之前，系统可能需要先安装 `Bash` 软件包。

![](img/10063bc94c89912e4f6ac282fcb6714_124_0.png)

提示 你可以通过挂载 ISO 文件来轻松访问第 2 章中使用的操作系统镜像内容。例如，将名为 `Fedora-Server-DVD-x86_64-23.iso` 的 Fedora DVD 镜像挂载到现有的 `/media/iso` 目录，你可以输入：

```
# mount Fedora-Server-DVD-x86_64-23.iso /media/iso/
```

让我们通过一遍安装一个更复杂的软件包，看看 RPM 如何处理依赖项的。假设你仍位于本章节所有工作文件的目录中（或者在 DVD 介质的 Package 目录中），通过以下操作：

- 1. 输入以下命令安装 `gcc` 软件包：
```
[root@fedora-server-chapter-04]# rpm -ivh gcc-*.rpm

error: Failed dependencies:

  binutils >= 2.* is needed by gcc-5.*.x86_64

  cpp 5.* is needed by gcc-5.*.x86_64

  glibc-devel >= 2* is needed by gcc-5.*.x86_64

  isl * is needed by gcc-5.*.x86_64

  libmpc.so.3) (64bit) is needed by gcc-5.*.x86_64

  libmpfr.so.4) (64bit) is needed by gcc-5.*.x86_64
```
输出看起来并不好。它告诉我们 `gcc-5.*` 依赖（需要）其他软件包和库：`binutils`、`cpp`、`glibc-devel`、`isl`、`libmpc` 和 `libmpfr`（由 `mpfr*.rpm` 提供）。

- 2. 幸运的是，由于我们在同一个目录下访问指定的软件包，我们可以轻松地将额外的包包含安装列表中，例如：
```
[root@fedora-server-chapter-04]# rpm -ivh \
gcc-* binutils-* cpp-* glibc-devel-* isl-* libmpc-* mpfr-*

error: Failed dependencies:

  glibc-headers-* is needed by glibc-devel-*

  glibc-headers = 2* is needed by glibc-devel-*
```
哦呀。看来这个特定的软件包并不容易移动。输出告诉我们 `glibc-devel-*` 软件包依赖于另一个名为 `glibc-headers-.*` 的软件包。

- 3. 将最新的依赖项添加到安装列表：
```
[root@fedora-server-chapter-04]# rpm -ivh \
gcc-* binutils-* cpp-* \
glibc-devel-* isl-* libmpc-* mpfr-* glibc-headers-*

error: Failed dependencies:

  kernel-headers-* is needed by kernel-headers-*

  kernel-headers >= 2* is needed by glibc-headers-*
```
在我们对这种关系付出了所有努力后，得到的只是更多的抱怨。最后一个要求是 `kernel-headers-*`。

- 4. 既然我们已经考虑了这些，我们将最后一个包添加到安装列表中：
```
root@fedora-server chapter-04# rpm -ivh \
gcc-* binutils-* cpp-* \
glibc-devel-* isl-* libmpc-* mpfr-* glibc-headers-*

Preparing...

###################### [100%]

Updating / installing... 1:binutils-*###################### [100%]

2:cpp-*###################### [100%]

3:glibc-devel-*###################### [100%]

4:isl-*###################### [100%]

5:libmpc-*###################### [100%]

6:mpfr-*###################### [100%]

7:glibc-headers-*###################### [100%]

8:kernel-headers-*###################### [100%]

9:gcc-*###################### [100%]
```
如你所示，通过 RPM 安装软件包可以非常简单。

某些地方可能异常——例如，如果 `/bin/ls` 命令被替换为了伪版本——那么 `verify` 的输出可能如下：
```bash
[root@fedora-server ~]# rpm -Vf /bin/ls

SM5....T. /usr/bin/ls
```

如果出现问题（如示例所示），RPM 将通知你哪些测试失败了。一些示例测试包括 MD5 校验测试、文件大小和修改时间。这个故事的寓意是，RPM 是你发现系统问题的得力助手。

表 4-1 提供了各种错误代码及其含义的摘要。

| 代码 | 含义 |
|---|---|
| S | 文件大小不同 |
| M | 模式不同（包括权限和文件类型） |
| 5 | MD5 和不同 |
| D | 设备主/从设备号不匹配 |
| L | readLink-路径不匹配 |
| U | 用户所有权不同 |
| G | 组所有权不同 |
| T | 修改时间 (mtime) 不同 |

### 表 4-1 RPM 验证错误属性

你可以使用以下命令来验证系统上安装的所有软件包：
```bash
[root@fedora-server ~]# rpm -Va
```

此命令会验证系统上安装的所有软件包。由于文件非常多，你可能需要留一些时间来完成。

## 软件包验证

RPM 的另一个功能是允许对软件包进行数字签名。这提供了一种内置的身份验证机制，允许用户确认其拥有的软件包确实是由预期的（信任的）实体生成的，并且软件包在传输过程中的某处没有被篡改。

你有时需要手动告诉系统信任哪些数字签名。这解释了为什么在之前的安装尝试过程中，你可能会看到如下警告信息：`warning: lynx-2.*rpm Header V3/SHA256 Signature, key ID 34ba*`

为了防止此消息，你应该将 Fedora 的数字密钥导入系统的密钥环中，如下所示（将 `<VERSION>` 替换为你的 Fedora 版本）：

```bash
[root@fedora-server ~]# rpm --import \
/etc/pki/rpm-gpg/RPM-GPG-KEY-<VERSION>-fedora
```

你可能还需要将其他供应商的密钥导入密钥环。为了额外确保即使是你拥有的本地密钥不是伪造，你可以直接从供应商的网站导入密钥。例如，要从 Fedora 项目网站站点导入密钥，你需要将下一个命令中的 `<KEY_FILE>` 替换为正确的值。

```bash
[root@fedora-server ~]# rpm --import \
https://getfedora.org/static/<KEY_FILE>
```

你可以在 Fedora 项目网站的此处找到下载公钥文件的 URL 列表：https://getfedora.org/keys/
例如，对于 Fedora 23 版本，rpm import 命令的完整语法为

```bash
[root@fedora-server ~]# rpm --import \
https://getfedora.org/static/34EC9CBA.txt
```

表 4-2 列出了一些常用的 rpm 命令选项，仅供快速参考。

## 命令行选项

| 选项 | 描述 |
| --- | --- |
| --install | 安装新软件包 |
| --upgrade | 升级或将当前安装的软件包升级到新版本。 |
| --erase |移除或删除已安装的软件包。 |
| --query | 用于查询或检索有关已安装（或未卸载）软件包各种属性的信息。 |
| --force | 告诉 RPM 跳过任何合理检查并直接执行，即使它认为你正在尝试将方头插入圆孔。请谨慎使用此选项；它是安装中的“大锤”。通常情况下，当你知道要安装一种奇特或异常的配置，而 RPM 的保护机制试图阻止你时使用它。 |
| -h | 打印哈标记以指示安装过程中的进度。配合 -v 选项使用可美化显示。 |
| --percent | 打印完成百分比以指示进度。如果你从另一个程序（如 Perl 脚本）中运行 RPM，并想知道安装状态，这非常方便。 |
| -nodeps | 如果 RPM 抱怨缺少文件，但你仍希望进行安装，则导致 RPM 不执行任何依赖检查。 |
| -q | 查询 RPM 系统信息。 |
| --test | 检查在不执行实际安装的情况下安装是否会成功。如果预见到会有问题，将显示问题是什么。 |
| -V | 验证系统上的 RPM 或文件。 |
| -v | 告诉 RPM 详细输出其操作。 |

## Yum

Yum 是 RPM 比较流行的软件包/更新工具之一，具有极大的增强。它已经存在一段时间，现在已经非常成熟。Yum 改变并增强了基于 RPM 的系统的传统软件包管理方法。作为开源软件仓库的流行大型网站不得不进行轻微调整以适应“Yum 化”的存储库。

根据 Yum 的网页 (http://yum.baseurl.org/ )：

“Yum 是 rpm 系统的自动更新程序和软件包安装/删除程序。它会自动计算依赖关系，并确定应该执行哪些操作来安装软件包。它使得维护机器组变得更加容易，无需手动更新”

（注：原文 OCR 文本在后半部分似乎有严重的损坏/乱码句子。已根据标准 Yum 文档上下文进行逻辑清理。）

## DNF

DNF 是计划在 Red Hat 类型系统中取代 Yum 的新包管理器

- 更好的性能和内存占用
- 更快、更简单的包管理器
- 更小的代码库
- 对插件有更好的支持

## GUI 软件包管理器

对于喜欢使用良好的 GUI 工具简化生活的人来说，有几种带有图形界面的软件包管理器。在基于 Red 的发行版中，在这些漂亮界面背后执行所有脏活工作的是 RPM。GUI 工具允许你完成相当多的事情，而无需强制你记住命令行参数。各种发行版或桌面环境自带的一些流行工具列在后面的章节中。

## Fedora

在 Fedora 中，你可以通过按下键盘上的 ALT-F2 组合键，在输入命令文本框中输入 `gnome-software` 并按回车键来启动 GUI 软件包管理工具（见图 4-1）。

## 推荐应用

![](img/10063bc94c89912e4f6ac282fcb67141_133_0.png)

## 编辑选择

简单扫描 (Simple Scan)

音乐 (Musique)

Calibre

地图 (Maps)

Inkscape

**图 4-1** Fedora GUI 包管理器

你也可以通过命令行输入以下命令启动 Fedora 包管理器：

```
[root@fedora-server ~]# gnome-software
```

## openSUSE 和 SLE

在 openSUSE 和 SUSE Linux Enterprise (SLE) 中，大部分系统管理是通过一个名为 YaST 的工具完成的，它的意思是“Yet Another Setup Tool”（又一个设置工具）。YaST 由不同的模块组成。要在系统中以图形化方式添加和删除软件包，相关的模块是 `sw_single`。因此，在运行 SUSE 发行版的系统命令行中启动此模块时，你需要输入

```
opensuse-server:~ #  yast2 sw_single
```

## Debian 软件包管理系统

Debian 软件包管理系统 (DPMS) 是在 Debian 及类 Debian 系统上管理软件的基础。正如任何软件管理系统所预期的，DPMS 提供了方便安装和删除软件包的功能。Debian 软件包名以 `.deb` 扩展结尾。

DPMS 的核心是 `dpkg`（Debian 软件包）应用程序。`dpkg` 在系统的后台运行，并编写了许多其他命令行工具和 GUI 工具来与之交互。Debian 中的软件包被亲切地称为“.deb 文件”（读音为 dot deb）。`dpkg` 可以直接操作软件包。此外还开发了各种其他封装工具来直接或间接地与 `dpkg` 交互。

## APT

APT 是一个备受推崇且功能复杂的工具集。它是直接与 `dpkg` 交互的封装工具的示例。APT 实际上是一个编程函数库，供其他中间工具（如 `apt-get` 和 `apt-cache`）调用，用于在类 Debian 系统上操作软件。已经开发了几个依赖于 APT 的用户态应用程序（用户态指的是非内核程序和工具）。此类应用的示例包括 `synaptic`、`aptitude` 和 `dselect`。用户态工具通常对用户友好。APT 也已成功移植到其他操作系统。

APT 和 `dpkg` 之间一个细微的区别是，APT 不直接处理 .deb 包；它通过配置文件指定的源（仓库）来管理软件。主文件是 `sources.list`。APT 使用 `sources.list` 文件来定位系统上使用的软件包分发存档（或仓库）。

需要注意的是，DPMS 的任何组件（`dpkg`、APT 或 GUI 工具）都可直接在类 Debian 系统上管理软件。选择哪种工具取决于用户对该工具的熟悉程度和熟练程度。

[图 4-2] 显示了可以被称为“DPMS 三角形”的内容。位于三角形顶端的工具（`dpkg`）最难使用但也最强大，其次是易于使用的工具（APT），然后是用户友好的用户态工具。

![](img/10063bc94c89912e4f6ac282fcb67141_134_0.png)

**图 4-2** DPMS 三角形

## Ubuntu 中的软件管理

如前提到的，Ubuntu 等类 Debian 发行版中，软件管理是通过 DPMS 以及围绕其构建的所有相关应用程序（如 APT 和 dpkg）完成的。在本节中，我们将介绍如何在类 Debian 发行版上执行基础软件管理任务。

## 查询信息

在你的 Ubuntu 服务器上，列出所有已安装软件的对应命令是

```
master@ubuntu-server:~$ dpkg -l
```

获取已安装 Bash 软件包基本信息的命令是

```
master@ubuntu-server:~$ dpkg -s
```

获取关于安装软件包的详细信息的命令是

```
master@ubuntu-server:~$ dpkg -S
```

查看软件包包含的文件列表的命令是

```
master@ubuntu-server:~$ dpkg -L
```

dpkg 的查询功能非常强大。要查询已安装软件包的大小，可以使用

```
master@ubuntu-server:~$ dpkg-query -W -f='${Size}\n'
```

## Ubuntu 中的安装软件

如前所述，在 Ubuntu 中使用 DPMS 及其所有相关应用程序（如 APT 和 dpkg）来管理软件。在 Ubuntu 中有多种方法安装软件。

使用 dpkg 直接安装 .deb 软件包：

```
master@ubuntu-server:~$ dpkg -i
```

使用 apt-get 安装软件包，这需要从仓库中下载软件：

```
master@ubuntu-server:~$ apt-get install
```

使用 apt-get 安装软件要方便得多，因为它会处理任何依赖问题。

## Ubuntu 中的移除软件

在 Ubuntu 中使用 dpkg 卸载软件（如 lynx）非常简单，只需输入：

```
master@ubuntu-server:~$ dpkg -r
```

你也可以通过使用 apt-get 的 remove 选项来移除软件。要使用 apt-get 移除 lynx，请输入

```
master@ubuntu-server:~$ apt-get remove
```

APT 卸载的另一种不常用方法是使用 install 参数，并在要移除的软件包名称前加上减号 (-)。这在你想一次性安装并移除另一个软件包时非常有用。

要使用这种方法移除已安装软件包并同时安装名为 lynx 的软件包，请输入

```
master@ubuntu-server:~$ apt-get install lynx-joe
```

APT 可以轻松地从系统中完全移除软件及其任何相关的配置文件。假设你想完全从系统中移除 lynx 程序，你需要输入

```
master@ubuntu-server:~$ apt-get --purge remove lynx
```
