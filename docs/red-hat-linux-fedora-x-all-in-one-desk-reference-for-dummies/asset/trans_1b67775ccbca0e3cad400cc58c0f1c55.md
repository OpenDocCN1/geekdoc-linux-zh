

# 466 使用 Red Hat 包管理器 (RPM)

如果你提供的是包名而不是文件名，RPM 将显示包含指定包的 RPM 包名称。

另一方面，要找到需要特定包的 RPM 名称，请使用以下命令：

```bash
rpm -q --whatrequires packename
```

例如，要查看哪些包需要 openssl 包，输入：

```bash
rpm -q --whatrequires openssl
```

以下是该命令的典型输出，显示了所有需要 openssl 的 RPM 包

```
libcap-0.8.3-3
sendmail-8.12.11-4.6
curl-7.11.1-1
mod_ssl-2.0.49-4
openssl-devel-0.9.7a-35
dovecot-0.99.10.4-4
```

## 安装 RPM

要安装 RPM，请使用 `rpm -i` 命令。你必须提供 RPM 文件名作为参数。一个典型的示例是从本书的附带 DVD-ROM 中安装 RPM，该光盘包含了 Fedora RPM。像通常一样，你必须挂载 DVD-ROM 并切换到 RPM 所在的目录。然后使用 `rpm -i` 命令安装 RPM。如果你想查看 RPM 安装的进度，请使用 `rpm -ivh`，一系列哈希符号 (#) 会随着包的解压而显示。

例如，要从附带的 DVD-ROM 安装内核源码 RPM（它包含 Linux 操作系统的源文件），我插入 DVD 并在挂载后，使用以下命令：

```bash
cd /mnt/cdrom/RPM
rpm -i kernel-source-*
```

你不需要输入完整的 RPM 文件名——你可以使用名称开头的几个字符后跟一个星号 (*)。确保你输入的名称足够长，以唯一标识该 RPM 文件。

![](img/d9230b719dc0efd80851f363d8c6f571_492_0.png)

如果你尝试安装一个已经安装的 RPM，`rpm -i` 命令将显示错误信息。例如，当你输入命令在系统上安装 man 包时，会发生这种情况：

```bash
rpm -i man-1*
```

## 使用 Red Hat 包管理器 467

我从 `rpm -i` 命令收到错误信息：
package man-1.5m2-6 is already installed

即使存在错误也强制 rpm 命令安装包，只需在 `rpm -i` 命令中添加 `--force`：

```bash
rpm -i --force man-1*
```

## 移除 RPM

如果你意识到自己不需要该软件，可以移除包。例如，如果你安装了 X Window 开发包但发现自己不再需要这些应用程序，可以使用 `rpm -e` 命令轻松删除该包。

在删除之前，你必须知道该包的名称。找到名称的好方法是使用 `rpm -qa` 配合 `grep`。例如，定位 X Window 开发包，尝试以下命令：

```bash
rpm -qa | grep xorg
```

xorg-x11-devel 正好是 X Window 开发包的名称。移除该包，输入：

```bash
rpm -e xorg-x11-devel
```

移除 RPM 不需要完整的 RPM 文件名——你只需要版本号之前的包名（第一部分）。`rpm -e` 命令不会移除所需的包。例如，要移除 vim-common 包，输入以下命令：

```bash
rpm -e vim-common
```

然后我收到错误信息：

```
error: Failed dependencies:
vim-common is needed by (installed) vim-enhanced-6.245-1
```

## 升级 RPM

使用 `rpm -U` 命令升级 RPM。你必须提供包含新软件的 RPM 文件。例如，如果我的系统中安装了 2.0.48  Apache httpd（Web 服务器），我想升级到 2.0.49，我从 Red Hat 更新站点（fedora.com/download/mirrors.html 列出）下载 httpd-2.0.49-4.rpm 并使用以下命令：

```bash
rpm -U httpd-2.0.49-4.rpm
```

rpm 命令通过移除旧版本的 httpd 包并安装新版本来执行升级。

![](img/d9230b719dc0efd80851f363d8c6f571_494_0.png)

尽可能升级而不是移除旧包再安装新包。升级会自动保存你的旧配置文件，省去在全新安装后重新配置软件的麻烦。当你升级包含就绪 Linux 内核的包时，使用 `rpm -i` 命令（而不是 `rpm -U` 命令）。这样就不会覆盖当前内核。

## 验证 RPM

你可能不会经常这样做，但如果你怀疑某个软件包没有正确安装，请使用 `rpm -V` 命令进行验证。例如，要验证内核包，输入：

```bash
rpm -V kernel
```

此命令导致 rpm 将包中每个的大小和其他属性与原始文件进行比较。如果一切验证正确，`rpm -V` 命令不会打印任何内容。如果发现任何差异，你会看到报告。例如，我修改了 Apache httpd Web 服务器的配置文件。这是我验证 httpd 包的内容：

```bash
rpm -V httpd
```

结果如下：

```
S.5....T c /etc/httpd/conf/httpd.conf
```

在这种情况下，rpm -V 的输出告诉我是配置文件已更改。该命令输出的每行有三部分：

- 八字符，每个字符表示发现的差异类型。例如，S 表示大小不同，T 表示最后修改时间。表 4-1 显示了每个字符及其含义。点号表示该特定属性与原始文件匹配。
- 对于配置文件，接下来会出现 c；否则，该字段为空。这就是你判断一个文件是否为配置文件的方法。
- 通常，如果配置文件发生了更改，你不需要担心；可能可能是你自己做的更改。
- 行的最后部分是文件的完整路径。从这部分，你可以准确判断文件的位置。

| 表 4-1 RPM 验证报告中使用的字符 |
| 字符 | 含义 |
| --- | --- |
| S | 大小已更改 |
| M | 权限和文件类型不同 |
| 5 | 使用 MD5 算法计算的校验和不同 |
| D | 设备类型不同 |
| L | 符号链接不同 |
| U | 文件用户不同 |
| G | 文件组不同 |
| T | 文件修改时间不同 |

## 从源文件构建软件包

许多开源软件包以源码形式发行，不包含可执行的二进制文件。在使用此类软件之前，你必须构建二进制文件。在本节中，我将展示如何从源文件构建包。

### 下载并解压软件

开源软件文件通常以压缩归档的形式发行。这些归档是由 tar 程序创建并用 gzip 程序压缩的。发行格式为单个文件 .tar.gz 或 .tgz，通常称为 tar 包。如果你需要该软件，必须下载并解压 tar 包。

使用匿名 FTP 或通过浏览器下载源文件（确保以 root 身份登录；否则无法保存到 /usr/local/src）。下载压缩 tar 文件后，使用以下命令检查内容：

```bash
tar ztf xmms*.gz | more
```

你会看到类似下面的列表：

```
xmms-1.2.0/
xmms-1.2.0/int/
xmms-1.2.0/int/ChangeLog
xmms-1.2.0/int/Makefile.in
xmms-1.2.0/int/config.charset
xmms-1.2.0/int/locale.alias
xmms-1.2.0/int/ref-add.sin
xmms-1.2.0/int/ref-del.sin
xmms-1.2.0/int/gmo.h
xmms-1.2.0/int/getextP.h
xmms-1.2.0/int/hash-string.h
xmms-1.2.0/int/loadinfo.h
其余输出未显示
```

此命令的输出显示了归档中的内容，并让你了解解压归档后将创建哪些目录。在这种情况下，当前目录下会创建一个名为 xmms-1.2.0 的目录，在我的案例中是 /usr/local/src。从列表中，你也可以学习编写该包时使用的编程语言。

要提取压缩 tar 归档的内容，输入以下命令：

```bash
tar xvf xmms*.gz
```

你会再次看到长文件列表，将其从归档中提取并复制到硬盘上相应的目录。

现在你准备好构建软件了。

