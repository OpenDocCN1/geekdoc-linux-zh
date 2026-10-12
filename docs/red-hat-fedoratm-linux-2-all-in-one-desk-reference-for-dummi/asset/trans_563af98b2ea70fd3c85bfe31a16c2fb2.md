
2. 输入以下命令，进入 RPM 所在的目录：

   ```
   cd /mnt/cdrom/Fedora/RPMS
   ```

3. 使用 `ls` 命令查看列表。例如，若要查看名称以 `cups` 开头的 RPM，请输入：

   ```
   ls cups*
   ```

你会看到类似这样的列表：

```
cups-1.1.20-6.i386.rpm
cups-libs-1.1.20-6.i386.rpm
```

从列表中你可以猜到，RPM 文件的名称以 `.rpm` 扩展名结尾。为了理解文件名的各个部分，请考虑以下 RPM：

```
cups-1.1.20-6.i386.rpm
```

该文件名包含以下部分，用连字符（-）分隔：

- **软件包名称：** `cups`
- **版本号：** `1.1.20`
- **发行版号：** `6`（由 Red Hat 分配的发行版号）
- **架构：** `i386`（此软件包适用于 Intel 80386 兼容处理器）

通常，软件包名称描述得足够清楚，让你可以猜测该 RPM 可能包含什么。版本号与软件包的当前版本号相同（即使它是以其他形式分发的，例如 tar 文件）。开发人员分配发行版号以跟踪更改。对于你要在装有 Intel x86 兼容处理器的 PC 上安装的 RPM，架构为 `i386` 或 `noarch`。

## 了解 RPM

在安装软件包时，`rpm` 命令会构建一个已安装 RPM 的数据库。你可以使用 `rpm -q` 命令查询此数据库，以查找系统中已安装软件包的信息。

例如，若要查找系统中安装的 Linux 内核的版本号，请输入以下 `rpm -q` 命令：

```
rpm -q kernel
```

你会看到类似于以下的响应：

```
kernel-2.6.5-1.358
```

响应是内核 RPM 的名称（此版本是内核的可执行版本，而非源文件）。名称与 RPM 文件名相同，只是最后一部分 — .i386.rpm — 未显示。在这种情况下，RPM 的版本部分告诉你内核是 2.6.5。

你可以通过使用以下命令查看所有已安装 RPM 的列表：

```
rpm -qa
```

你会看到一长串 RPM 列表在屏幕上滚动。若要逐屏查看列表，请输入：

```
rpm -qa | more
```

如果你想搜索特定的软件包，请将 rpm -qa 的输出传递给 grep 命令。例如，若要查看所有名称中包含 kernel 的软件包，请输入：

```
rpm -qa | grep kernel
```

结果取决于系统中安装了内核 RPM 的哪些部分。例如，在我的系统中，此命令显示以下内容：

```
kernel-2.6.5-1.358
kernel-source-2.6.5-1.358
```

使用 rpm -q 命令，你可以查询软件包版本号以外的许多信息。通过添加单字符选项，你可以查找其他有用信息。例如，尝试以下命令以查看内核软件包中的文件：

```
rpm -ql kernel
```

以下是此命令输出中的几行：

```
/boot/System.map-2.6.5-1.358
/boot/config-2.6.5-1.358
/boot/vmlinux-2.6.5-1.358
/lib/modules/2.6.5-1.358
/lib/modules/2.6.5-1.358/build
/lib/modules/2.6.5-1.358/build/.config
/lib/modules/2.6.5-1.358/build/Makefile
/lib/modules/2.6.5-1.358/build/arch
/lib/modules/2.6.5-1.358/build/arch/alpha
/lib/modules/2.6.5-1.358/build/arch/alpha/Kconfig
/lib/modules/2.6.5-1.358/build/arch/alpha/Makefile
/lib/modules/2.6.5-1.358/build/arch/alpha/boot
/lib/modules/2.6.5-1.358/build/arch/alpha/boot/Makefile
/lib/modules/2.6.5-1.358/build/arch/alpha/kernel
/lib/modules/2.6.5-1.358/build/arch/alpha/kernel/Makefile
(其余列表已省略)
```

以下是 rpm -q 命令的几个其他实用形式，用于查询软件包的信息（使用这些 rpm -q 命令中的任何一个时，请输入该命令，后跟软件包名称）：

- `rpm -qc`：列出软件包中的所有配置文件。
- `rpm -qd`：列出软件包中的所有文档文件。这些通常是联机手册页（也称为 man 页面）。
- `rpm -qf`：显示指定文件所属的软件包名称（如果有的话）。
- `rpm -qi`：显示关于软件包的详细信息，包括版本号、大小、安装日期和简短描述。
- `rpm -ql`：列出软件包中的所有文件。对于某些软件包，你会看到非常长的列表。
- `rpm -qs`：列出软件包中所有文件的状态。

![](img/9f89727199836b0f871f1745838aa8b2_491_0.png)

这些 rpm 命令仅提供关于已安装软件包的信息。如果你想查找未安装的 RPM 文件的信息，请在每个命令的命令行选项中添加字母 p。例如，若要查看名为 rdist-6.1.532.i386.rpm 的 RPM 文件中的文件列表，请转到该文件所在的目录，然后输入以下命令：

```
rpm -qpl rdist-*.rpm
```

当然，此命令仅在当前目录包含该 RPM 文件时有效。

![](img/9f89727199836b0f871f1745838aa8b2_491_1.png)

两个方便的 rpm -q 命令可以让你查找提供特定文件的 RPM 文件以及哪些 RPM 需要指定的软件包。若要查找提供文件的 RPM 的名称，请使用以下命令：

```
rpm -q --whatprovides 文件名
```

例如，若要查看哪个 RPM 提供文件 /etc/yum.conf，请输入：

```
rpm -q --whatprovides /etc/yum.conf
```

RPM 随后会打印提供该文件的软件包名称，如下所示：

```
yum-2.0.7-1,1
```

## 466 使用 Red Hat 软件包管理器

如果你提供软件包名称而不是文件名，RPM 会显示包含指定软件包的 RPM 软件包名称。

另一方面，若要查找需要特定软件包的 RPM 名称，请使用以下命令：

```
rpm -q --whatrequires `软件包名称`
```

例如，若要查看哪些软件包需要 `openssl` 软件包，请输入：

```
rpm -q --whatrequires openssl
```

以下是此命令的典型输出，显示所有需要 `openssl` 的 RPM 软件包：

```
libcap-0.8,3-3
sendmail-8.12.11-4.6
curl-7.11.1-1
mod_ssl-2.0.49-4
openssl-devel-0.9.7a-35
dovecot-0.99.10.4-4
```

## 安装 RPM

要安装 RPM，请使用 `rpm -i` 命令。你必须提供 RPM 文件的名称作为参数。一个典型的例子是安装来自本书附带 DVD-ROM 中的 RPM，该 DVD 包含 Fedora Core RPM。通常，你必须挂载 DVD-ROM 并切换到 RPM 所在的目录。然后使用 `rpm -i` 命令安装 RPM。如果你想查看 RPM 安装的进度，请使用 `rpm -ivh`。在软件包解包时，会显示一系列井号（#）。

例如，要从附带 DVD-ROM 安装 `kernel-source` RPM（其中包含 Linux 操作系统的源文件），我插入 DVD，在其挂载后，输入以下命令：

```
cd /mnt/cdrom/Fedora/RPMS
rpm -ivh kernel-source*
```

![](img/9f89727199836b0f871f1745838aa8b2_492_0.png)

你不必输入完整的 RPM 文件名——你可以使用名称开头的几个字符后跟一个星号（*）。请确保你输入足够的名称以唯一标识该 RPM 文件。

如果你试图安装一个已经安装的 RPM，`rpm -i` 命令会显示错误消息。例如，这是我在我的系统上输入以下命令以安装 `man` 软件包时发生的情况：

```
rpm -i man-1*
```

我从 `rpm -i` 命令获得以下错误消息：

```
package man-1.5m2-6 is already installed
```

若要强制 `rpm` 命令即使在存在错误的情况下也安装软件包，只需在 `rpm -i` 命令中添加 `--force`，如下所示：

```
rpm -i --force man-1*
```

## 删除 RPM

如果你意识到你并不真正需要该软件，你可能想要删除（卸载）软件包。例如，如果你安装了 X 窗口系统开发软件包，但发现你对编写 X 应用不感兴趣，你可以轻松通过使用 `rpm -e` 命令删除软件包。

在你删除软件包之前，你必须知道软件包的名称。查找名称的一个好方法是使用 `rpm -qa` 配合 `grep` 来搜索适当的 RPM 文件。例如，若要定位 X 窗口系统开发 RPM，请尝试以下命令：

```
rpm -qa | grep xorg
```

`xorg-x11-devel` 恰好是 X 窗口系统开发 RPM 的软件包名称。要删除该软件包，请输入：

```
rpm -e xorg-x11-devel
```

要删除 RPM，你不需要完整的 RPM 文件名；你只需要软件包名称——文件名中版本号前的连字符（-）之前的第一部分。

`rpm -e` 命令不会删除其他软件包所需的软件包。例如，若要删除 `vim-common` 软件包，我输入以下命令：

```
rpm -e vim-common
```

然后我获得以下错误消息：

```
error: Failed dependencies:
    vim-common is needed by (installed) vim-enhanced-6.2.457-1
```

## 升级 RPM

使用 `rpm -U` 命令来升级 RPM。你必须提供包含新软件的 RPM 文件的名称。例如，如果我在系统中安装了 Apache `httpd`（Web 服务器）版本 2.0.48，但我想

