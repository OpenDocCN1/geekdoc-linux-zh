
```
nazeem@linux:~ > ftp ftp.us.kernel.org
Connected to ftp.us.kernel.org.
220 elijah.nodomainname.net FTP server (Version wu-2.5.0(1) Wed Aug 25 14:13:56 EDT 1999) ready.
Name (ftp.us.kernel.org:nazeem): ftp
331 Guest login ok, send your complete e-mail address as password.
Password:
230-Welcome to the FTP site of NoDomainName Networks! Look in /pub for
230-all available downloads, including mirrors of RedHat, the Linux
230-Kernel archives, Internet RFCs, the Interactive Fiction archive, and
230-the GNU Project, as well as software from NoDomainName Networks.
230-
230-You are user 19 out of 100.
230-
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
```

内核位于`/pub/linux/kernel/`下。对于你想要的内核，你将进入`/pub/linux/kernel/v2.2`，这就是可以找到 2.2.x 系列的地方。现在你面临两个选择，你可以下载整个内核源代码，或仅下载一个补丁来将你的内核升级到新版本。这取决于你拥有的内核版本。例如，如果你有内核版本 2.2.10 并想升级到 2.2.11，那么安全的做法是仅下载`patch-2.2.10-2.2.11.gz`文件，这是一个对你内核的补丁。如果你想从 2.2.1 升级到 2.2.13，更有意义的是获取整个内核而不是补丁。原因在于你将不得不从 2.2.2 下载所有补丁一直到 2.2.13，因为你不能将 2.2.13 补丁直接应用到 2.2.1 内核上；它只能应用于 2.2.12。

> TIP
>
> 你会在下载内核的 FTP 目录中找到每个文件的两个副本：一个以`bz2`结尾，另一个以`gz`结尾。这两种不同的程序用于压缩内核源代码以使其下载大小更小。在大多数情况下，建议你获取`bz2`（`bzip2`）副本，因为它比`gz`（`gzip`）副本的尺寸更小。

## 解包内核源代码

下载内核后，你需要解包它并开始编译它。为此你需要知道解包的位置。在此我们需要指出，你必须以`root`身份登录才能执行以下操作。内核通常位于`/usr/src/`下的一个名为`linux`的目录中。`linux`目录是符号链接，指向实际包含内核的目录，该目录通常命名为`linux-x.x.x`以表示版本。你需要替换该内核。你必须先删除符号链接。然后在该目录中解包内核，并创建一个新的符号链接指向你的内核目录。因此，你执行以下操作：

1. 进入编译目录`/usr/src/`。然后使用以下命令删除符号链接：

2. 解包内核（`gz`版本）：

3. 解包内核（`bz2`版本）：

4. 内核解包到名为`linux`的目录下，所以你需要将其重命名为更易理解的名称：

```
# rm linux
```

```
# tar xvfz /path/where/you/downloaded/the/kernel/linux-2.2.13.tar.gz
```

```
# tar xvjf /path/where/you/downloaded/the/kernel/linux-2.2.13.tar.bz2
```

```
# mv linux linux-2.2.13
```

5. 接下来你用一个名为`linux`的符号链接指向它：

```
# ln -s linux-2.2.13 Linux
```

6. 最后，如果你是从旧内核升级，将之前的内核配置导入到新内核中很有用。内核的配置保存在一个名为`.config`的隐藏文件中。

要导入旧内核的配置，只需将该文件从旧内核目录复制到新内核目录即可。例如，如果你的旧内核是 2.2.10 而你升级到 2.2.13，你将拥有以下两个目录：

`/usr/src/linux-2.2.10`

`/usr/src/linux-2.2.13`

7. 要复制配置，你发出以下复制命令：

```
# cp /usr/src/linux-2.2.10/.config /usr/src/linux-2.2.13
```

## 使用补丁升级内核

有时使用补丁升级内核更容易。补丁是一个包含两个内核版本之间差异的文件。当你将补丁应用到内核时，该补丁会用新内核中的差异编辑你的内核文件，从而升级它。补丁通常比下载整个内核快得多。

要应用补丁，请使用名为`patch`的实用程序。补丁通常被`gzip`（`*.gz`）或`bzip2`（`*.bz2`）压缩。请按照以下步骤操作：

1. 你需要做的第一件事是将补丁移动到`/usr/src`目录并解包它：

   `linux:/usr/src # cp /path/to/patch/patch-2.2.x.gz /usr/src/`

   `linux:/usr/src # gzip -d patch-2.2.x.gz`

2. 解包补丁后，你应该应用它。使用以下命令很容易：

   `linux:/usr/src # patch -p0 < patch-2.2.x`

程序将把补丁应用到内核，并且状态信息会快速滚动。最好给`patch`加上`-s`选项，这样它只报告错误而不是所有内容。完成后，内核已升级到下一个版本。当然，所有这些都可以一步完成——或者正如 UNIX 大师所说的，一行命令：

```
linux:/usr/src # gzip -c /path/to/patch/patch-2.2.x.gz | patch -p0 -s
```

该命令解压缩补丁并即时将其通过管道传递给`patch`程序。

如果想要反向应用一个补丁？这使用的是同一个补丁程序。要反转补丁的效果并恢复原始文件，请使用`-R`选项运行`patch`：`patch -R < patch-2.2.x`这将撤销已应用补丁的效果。就这样！你已在正确的位置解压了内核并导入了旧的配置。现在你已准备好开始配置和编译你的内核。

## SuSE 特定更改

如果你从 SuSE 以外的来源下载了内核，你需要对其中一个内核文件——`makefile`——做一个小的修改。请按照以下步骤操作：

- 1. 使用你喜欢的编辑器打开文件`/usr/src/linux/Makefile`。

- 2. 找到一行写着`INSTALL_PATH=/boot`的行。该行前面会有井号（`#`）。

- 3. 删除该井号并确保该行写着`INSTALL_PATH=/boot`。

- 4. 保存文件并退出。现在内核已准备好在 SuSE 上安装。

现在是时候做正事了，配置内核。

## 配置你的内核

这是整个过程中最重要的步骤，即内核配置步骤。它并不困难；只是需要集中注意力。现在你已解压内核并将其放置在正确的位置，是时候配置它了。为此你运行内核配置实用程序。

内核附带三种不同版本的配置实用程序，其中两种基于文本，一种是图形（GUI）。其中最用户友好的是图形版，其次是基于菜单的文本版，然后是完全基于文本的版本。三种都有完全相同的内核配置选项集；只是每个的显示方式不同。

在我们继续解释如何运行和使用这三种不同的实用程序之前，我们将提供配置/编译整个过程的快速概述。

### 内核配置/编译快速入门

配置和编译内核的步骤如下：

- 1. 以`root`身份登录。

- 2. 决定是否使用图形或基于文本的实用程序。如果你选择图形版本，则运行 X Windows。如果你想使用基于文本的版本，则不必运行 X Windows。但如果你运行也没关系，因为你可以在 X 终端中运行基于文本的实用程序。

3. 进入包含内核源代码的以下目录：

`# cd /usr/src/linux`

4. 使用以下其中一个运行配置实用程序：

- `# make xconfig`用于图形实用程序

- `# make menuconfig`用于基于菜单的实用程序

- `# make config`用于完全基于文本、无菜单的实用程序

5. 配置各种内核参数。

6. 保存配置然后退出实用程序。

7. 开始编译内核，通过按顺序执行以下命令或在一行中用分号分隔：

`# make dep`

`# make clean`

`# make bzImage`

`# make modules`

`# make modules_install`

8. 重新启动系统以加载新内核。

就完成了。现在是详细版本....

## 运行图形内核配置实用程序
