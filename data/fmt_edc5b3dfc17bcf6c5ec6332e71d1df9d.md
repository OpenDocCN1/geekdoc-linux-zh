
`-rw-r--r-- root root 16384 Oct 14 17:31 __db.001`

`-rw-r--r-- root root 1318912 Oct 14 17:31 __db.002`

`-rw-r--r-- root root 4587552 Oct 14 17:31 __db.003`

`-rw-r--r-- root rpm 1179648 Oct 14 19:53 Durnames`

`-rw-r--r-- root rpm 5521408 Oct 14 19:53 Filemd5`

`-rw-r--r-- root rpm 24576 Oct 14 19:53 Group`

`-rw-r--r-- root rpm 204660 Oct 14 19:53 Installid`

`-rw-r--r-- root rpm 40566 Oct 14 19:53 Name`

`-rw-r--r-- root rpm 41070592 Oct 14 19:53 Packages`

`-rw-r--r-- root rpm 348160 Oct 14 19:53 Providance`

`-rw-r--r-- root rpm 983304 Oct 14 19:53 Providversion`

`-rw-r--r-- 1 rpm rpm 12288 Oct 14 19:53 Pubkeys`

`-rw-r--r-- 1 rpm rpm 237568 Oct 14 19:53 Requirename`

`-rw-r--r-- 1 rpm rpm 176128 Oct 14 19:53 Requireversion`

`-rw-r--r-- 1 rpm rpm 94208 Oct 14 19:53 Shaheader`

`-rw-r--r-- 1 rpm rpm 49152 Oct 14 19:53 Sigmd5`

`-rw-r--r-- 1 rpm rpm 12288 Oct 14 19:53 Triggename`

已安装软件的主数据库包含在名为 `Packages` 的文件中。如前一个示例所示，如果你完整安装了 Fedora Core Linux（超过 4GB 的软件），该数据库可能会增长到 33MB（甚至更大）。在安装 Fedora Core Linux 后，`rpm` 和相关命令将在软件管理操作中使用此目录。

## 使用 RPM 进行软件管理

## 命令行和图形化 RPM 客户端

作为 Fedora Core Linux 系统管理员，你将使用 `rpm` 命令或 Fedora Core 图形客户端来执行五项基本任务之一。这些操作必须由 root 操作员执行，包括以下内容：

- 安装新软件
- 擦除或移除过时或不需要的包
- 升级已安装的软件包
- 查询以获取软件包的信息
- 验证包的安装或完整性

`rpm` 命令有超过 60 个不同的命令行选项，但它们可以按功能进行分组。`rpm` 的基本格式如下：

```bash
# rpm -i (安装)

# rpm -e (擦除/移除)

# rpm -U (升级)

# rpm -q (查询)

# rpm -v (验证)
```

### RPM 选项表格

| 选项 | 用途 |
| :--- | :--- |
| -i | 安装包 |
| -e | 擦除（移除）包 |
| -U | 升级已安装的包 |
| -q | 查询包的信息 |
| -v | 验证安装/完整性 |
| -l | 列出包中的文件 |
| -K | 使用 GPG 签名验证包 |
| -nodeps | 忽略依赖关系 |
| -f | 哪个包拥有该文件 |
| -whatprovides | 确定包提供什么 |
| -whatrequires | 确定包需要什么 |

## 在命令行使用 rpm

由于新的图形化 RPM 客户端只能安装和卸载包（承诺提供更多功能），你最终将从命令行管理 RPM 包。本节介绍了如何执行这些操作。它还提供了如何安装、验证、查询、移除和升级软件包的示例。

```bash
warning: /var/tmp/rpm-xfer.48amVs: V3 DSA signature: NOKEY, key ID 8df56d05

Preparing...

########################################### [100%]

unace

########################################################### [100%]
```

此示例使用了 `v` 和 `h` 选项，这些选项提供了更详细的输出，并显示哈希标记以展示安装进度。该示例还演示了 `rpm` 使用 HTTP 或 FTP 获取文件以进行安装的能力。它还展示了 `rpm` 可以使用 GPG 密钥来验证文件。（示例中未安装密钥）。

在安装软件包后，你也可以使用 `rpm` 查询其数据库以验证安装情况。使用 `-V` 选项并配合软件包名称来验证系统的安装状态。例如，要验证 `unace` 归档包，可以使用 `rpm` 命令：

```bash
# rpm -V unace
```

> 注意
如果你的安装无误，在运行 `-rpm -V` 命令后，系统将不会显示任何响应；只有出现问题才会显示。

你可以从程序输出看到，通过在 `-v` 选项上添加额外的验证选项（例如再两个 `v -s`），可以获取有关软件包的更多信息。要获取已安装软件包的更多信息，请使用一种或多种形式的 `rpm` 查询选项。例如，要显示已安装软件包的简要信息，使用 `-q` 选项配合 `i` 选项和已安装软件包名称，如下（请注意你的版本将与此处不同）：

```bash
# rpm -qi unace
```

| Field | Value |
| :--- | :--- |
| Name | unace |
| Relocations | (not relocate) |
| Version | 2.2 |
| Vendor | Penguin Liberation Front |
| Release | 2plf |
| Build Date | Sat 01 Mar 2003 12:13:48 PM EST |
| Install date | Tue 02 Sep 2003 03:46:28 PM EDT |
| Build Host | baader.submission.alt |
| Group | Archiving/Compression |
| Source RPM | unace-2.2-2plf.src.rpm |
| Size | 401368 |
| License | freeware |
| Packager | Guillaume Rousseau <guillomovitch@zar.org> |
| URL | http://www.winace.com |
| Summary | Decompressor for .ace formats |

`Unace` 是一个用于提取、查看和测试 ACE 归档内容的实用程序。

# 使用 RPM 进行软件管理

这种形式的 `rpm` 查询提供了有关软件包的一些信息。
（你也可以通过提供软件包的路径在安装前对其进行查询。）

如果此软件包不是最新的，你可以通过下载新版本并使用 `rpm -U` 或 `upgrade` 选项来快速地升级软件包：

```bash
# rpm -Uvh unace-2.2-2plf.i586.rpm

Preparing... ########################### [100%]

1:unace ########################################### [100%]
```

请注意，不需要移除当前已安装的软件——`U` 选项会移除软件的旧版本（保留配置文件），然后自动安装新版本。

你还可以使用 `rpm` 命令的 `-F` 或 `"freshen"` 选项来升级系统软件，它将从远程 FTP 或 HTTP 服务器获取指定的软件包。例如，要升级 `fetchmail-config`，可以使用 `rpm`：

```bash
# rpm -Fv ftp://ftp.tux.org/linux/redhat/updates/9/en/os/i386/initscripts-7.14.i386.rpm
```

使用 `-e` 选项配合软件包名称，可以使用 `rpm` 从你的系统中移除或删除软件。例如，要移除 `unace` 归档包，可以使用 `rpm` 命令：

```bash
# rpm -e unace
```

请注意，如果操作成功，系统将不会显示任何消息。你可以通过将 `rpm -qa` 的输出通过给 `grep` 和 `sort` 来快速搜索已安装软件包的名称（参见第 5 章“Fedora 的第一步”获取有关 `grep` 和 `sort` 的更多信息）；搜索方法如下：

```bash
# rpm -qa | grep | sort

mailcap-2.14-1.1

mail-8.1.1

mozilla-1.4.1

procmail-3.22-1

sendmail-8.12-1.1
```
