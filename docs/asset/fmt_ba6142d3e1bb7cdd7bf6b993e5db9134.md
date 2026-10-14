
```
# shutdown -h now "The system is being shut down now!" [RET]
```

## A.2.2 在特定时间关机

要使系统在特定时间关机，请以 24 小时格式给出该时间作为参数。

⇒ 这里有两种使用方法。

- 要在凌晨 4:23 关机然后重新启动系统，输入：

  `# shutdown -r 4:23 [RET]`

- 要在晚上 8:00 关机并停止系统，输入：

  `# shutdown -h 20:00 [RET]`

要使系统在一定分钟数后关机，请在数字前加上加号（`+`）。

⇒ 要在五分钟后关机并停止系统，输入：

```
# shutdown -h +5 [RET]
```

在时间后加上一个引号消息，以便显示在所有已登录用户的终端上。

⇒ 要在午夜关机并停止系统，并向所有已登录用户发送警告消息，输入（全部在一行上）：

```
# shutdown -h 00:00 "The system is going down for maintenance at midnight" [RET]
```

## A.2.3 取消关机

如果你已下达关机指令，但最终决定并不想关机，可以再次运行 `shutdown` 并使用 `-c` 选项。此命令会停止正在进行的任何关机。

⇒ 要取消任何待处理的关机，输入：

`# shutdown -c RET`

与正常系统关机一样，你可以在取消时发送解释性消息以显示给所有用户。

⇒ 要取消任何待处理的关机并向所有已登录用户发送解释性消息，输入：

`# shutdown -c "Sorry, I hit the wrong key!" RET`

此命令会取消任何待处理的系统关机，并在所有已登录用户的终端上显示消息“Sorry, I hit the wrong key!”。

NOTES： 如果关机过程已进行到所有终端都停止的程度，你将无法运行此命令。

## A.2.4 进入维护模式

有时进入单用户维护模式很有用——也许是为了在硬盘分区上运行 `e2fsck` 或执行其他系统诊断。通过关闭系统，然后提供 `root` 密码进入维护模式即可实现。

⇒ 要进入维护模式，输入：

```
# shutdown now RET
... shutdown messages ...
Give root password for maintenance: abracadabra RET
#
```

此命令会将你置于控制台上的 `root` shell 中，在那里你可以运行 `e2fsck` 或执行你打算做的事情。在示例中，`root` 用户的密码很简单，为 "abracadabra"。

要退出 shell，输入 `CTRL-D`；根据你所做操作，你可能希望再次使用 `CTRL-ALT-DEL` 重启。

## A.3 管理软件

所有 Linux 发行版都附带大量软件程序（也称为二进制文件，因为程序通常包含在一个可执行二进制文件中）。

## A.3.2 为你的 Linux 发行版安装软件包

Linux 发行版将软件程序放在软件包中，软件包是单个文件，通常是压缩的，包含该特定程序所需的所有文件的归档。发行版具有用于安装和维护软件包的软件管理系统；在安装时，软件包首先会检查它可能依赖的其他软件包以正确运行（其依赖项）。这样，你可以确保安装在系统上的软件能够正常运行。

Linux 世界中有两种主要的软件包格式：Debian 的 `DEB` 格式，以及 Red Hat 的 Package Manager 格式 `RPM`。前者被 Debian 和 Knoppix 发行版使用；后者被 Red Hat、Mandrake、SuSE 等使用。还有其他发行版可能根本不使用软件包，或使用源软件包（请参阅以下配方）。

你系统所需的大多数软件将采用你发行版的软件包格式，但你并不局限于此。你始终可以安装源软件包，甚至安装以其他发行版格式打包的软件：Debian 很早就能够通过特殊软件读取和安装 `RPM` 软件包，而默认使用 `RPM` 的发行版（包括 Fedora 和 Red Hat Enterprise）同样具有使用 `DEB` 的工具。我有点老派，不喜欢将打包系统与发行版混合，但有些人可能需要这样做。

这些软件包格式的管理在本文档附录的后面部分有描述：Recipe A.4 [Managing DEB Packages]，第 709 页 和 Recipe A.5 [Managing RPM Packages]，第 714 页。

## A.3.3 安装源软件包

通常源软件包以压缩的 tar 归档形式分发，作为单个文件，其文件名扩展名为 `.tar.gz` 或 `.tgz`。² 这个文件集合通常被称为计算机程序的源代码。

这些文件通常放在 `/usr/local/src` 中并解压到各自的目录中。如果它们是源代码分发，则软件必须进行编译。通常，软件包目录中的名为 `INSTALL` 或 `README` 的文件会指示你如何操作。许多源软件包附带一个名为 `configure` 的脚本，用于配置编译过程

2 这就像任何文件名一样，只是约定。除了约定（和常识）之外，没有任何东西能阻止你将压缩的 tar 文件命名为 `.EXE` 扩展名，或将 Debian `DEB` 格式文件命名为 `.rpm`，或完全省略文件扩展名。

your system, and then `make` is run with either `install` or `all` as an argument, depending on what the package’s particular documentation instructs.

⇒ To compile and install a software package from its source directory, you generally type:

```shell
# ./configure RET

... configuration messages ...

# make install RET

... compilation messages ...

... installation messages ...

#
```

当你在系统上安装源码包时，就称之为安装本地软件——文件保存在 `/usr/local` 目录树中。二进制文件放在 `/usr/local/bin`，库放在 `/usr/local/lib`，手册页放在 `/usr/local/man`，文档放在 `/usr/local/doc` 或 `/usr/local/share/doc`。

## A.3.4 Installing a Shell Script

当你有一个想要安装到系统上的 shell 脚本时，你首先要确保该脚本文件是可执行的（参见 Recipe 6.3.6 [Making a File Executable], page 170）。

通常，管理员会将新的 shell 脚本安装在 `/usr/local/bin` 目录中。如果你在一个多用户系统上，并且你是有可能运行某个特定脚本的唯一用户，你可以将其放在你的主目录树中的一个特殊目录——这里的标准建议是 `~/bin` 目录——然后将该目录添加到你的路径中（参见 Recipe 3.5.7 [Adding to Your Path], page 81）。

并非所有可执行的脚本文件都是 shell 脚本。脚本的第一行包含用于解释和执行脚本的 shell 或其他程序的完整路径名；有时该路径在你的系统上可能与脚本编写时的路径不同，因此你可能需要更改这一行。

例如，一个脚本可能以以下行开头：

```shell
#!/usr/local/bin/perl
```

这一行意味着脚本是用 `perl` 语言编写的；“#!”之后的内容是 `perl` 程序的完整路径名，在本例中为 `/usr/local/bin/perl`。如果脚本第一行中工具的位置与你系统上的位置不同，它将无法工作（参见 Recipe 7.5 [Finding Where a Program Is Located], page 185）。例如，如果 `perl` 在你的系统上位于 `/usr/bin/perl`，你将不得不编辑此脚本的第一行，使其与该实际位置相匹配。

如果你尝试执行此脚本，并且系统报告找不到文件错误，你将不得不更改该第一行以对应系统上 `perl` 二进制文件的位置。`which` 工具会输出此位置。

⇒ 要找出 `perl` 在你的系统上安装在哪里，输入：

```
# which perl [RET]
```

如果此命令返回 `/usr/bin/perl` 或除 `/usr/local/bin/perl` 之外的某个路径名，你将不得不将脚本第一行中的位置更改为给出的路径名：

```
#!/usr/bin/perl
```

NOTES: 如果 `which` 命令的输出为空，这意味着 `perl` 程序根本未安装在你的系统上；在这种情况下，你应该安装 `perl` 软件以便运行脚本。

## A.4 Managing DEB Packages

+ Dpkg

+ DEB: `dpkg`

+ or

+ Apt

+ DEB: `apt`

`DEB` 是 Debian 系统上的原生包格式。这些包可在 `http://packages.debian.org/` 上通过网络获取。
