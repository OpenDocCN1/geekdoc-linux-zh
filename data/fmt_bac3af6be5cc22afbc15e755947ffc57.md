
您可以用 RPM 查询做更多事情，如表 7-3 所述。请注意查询与 `-q` 或 `--query` 相关联；像 `--query` 这样的全词开关通常与双破折号相关联。

### 软件包签名

RPM 使用多种方法来检查软件包的完整性。您已经看到如何导入 GPG 签名。这些方法中的一些显示在 `rpm --checksig pkgname` 命令的输出中。(`-K` 开关等同于 `--checksig`。) 例如，如果您从第三方（如假设的 `pkg-1.2.3-4.noarch.rpm` 软件包）下载了一个软件包，并希望将其与导入的 GPG 签名进行检查，请运行以下命令：

```
# rpm --checksig pkg-1.2.3-4.noarch.rpm
```

如果成功，您将看到类似以下的输出：

```
pkg-1.2.3-4.noarch.rpm: rsa sha1 (md5) pgp md5 OK
```

**表 7-3**
**rpm --query 选项**

| rpm 查询命令 | 含义 |
|---|---|
| rpm -qa | 列出所有已安装的软件包。 |
| rpm -qf /path/to/file | 识别与 /path/to/file 关联的软件包。 |
| rpm -qc packagename | 仅列出 packagename 的配置文件。 |
| rpm -qi packagename | 显示 packagename 的基本信息。 |
| rpm -ql packagename | 列出 packagename 的所有文件。 |
| rpm -qR packagename | 注意所有依赖项；如果没有它们，就无法安装 packagename。 |

您可能已经认识到用于验证软件包完整性的算法：

- **rsa** 以其创建者 Rivest、Shamir 和 Adleman 命名，它是一种公钥加密算法。
- **sha1** 160 位消息摘要安全哈希算法；一种加密哈希函数。
- **md5** 消息摘要 5，一种加密哈希函数。
- **pgp** PGP，由 GPG 在 Linux 中实现。

### 文件验证

已安装软件包的验证将该软件包的信息与系统上的 RPM 数据库中的信息进行比较。`--verify`（或 `-v`）开关检查软件包中每个文件的大小、MD5 校验和、权限、类型、所有者和组。验证可以以多种方式完成。以下是一些示例：

- 验证所有文件。当然，这可能需要很长时间。 （当然，`rpm -Va` 命令执行相同的功能。）
- 将软件包中的所有文件与下载的 RPM 进行验证。
- 验证与特定软件包关联的文件。

```
# rpm --verify -a
```

```
# rpm --verify -p vsftpd-2.2.2-6.el6.i686.rpm
```

```
# rpm --verify --file /bin/ls
```

如果文件或软件包的完整性得到验证，您将看不到任何输出。任何输出意味着文件或软件包与原始版本不同。如果出现某些更改，无需惊慌；毕竟，管理员确实会编辑配置文件。有八项测试。如果发生更改，输出是一串最多八个失败代码字符，每个字符告诉您在每次测试中发生了什么。如果看到点 (.)，则该测试通过。以下示例显示 `/bin/vi` 的组 ID 分配不正确：

```
# rpm --verify --file /bin/vi
```

```
.....G  /bin/vi
```

表 7-4 列出了失败代码及其含义。

**表 7-4**
**rpm --verify 代码**

| 失败代码 | 含义 |
|---|---|
| 5 | MD5 校验和 |
| S | 文件大小 |
| L | 符号链接 |
| T | 文件修改时间 |
| D | 设备 |
| U | 用户 |
| G | 组 |
| M | 模式 |

现在这里有一个有趣的实验：当您安装了一个软件包的某个版本时，使用 `rpm --verify -p` 命令与同一软件包的第二个版本进行比较。找到这样的软件包应该不会太困难，因为 Red Hat 经常为功能更新、安全补丁，当然还有错误修复而更新软件包。例如，当我为 RHEL 6 编写本书时，我同时拥有 `vsftpd-2.2.2-1.el6.i686.rpm` 和 `vsftpd-2.2.2-6.el6.i686.rpm`。当安装后者版本时，我运行了以下命令：

```
# rpm --verify -p vsftpd-2.2.2-1.el6.i686.rpm
```

并得到了一长串已更改的文件，如图 7-3 所示。该命令提供了 vsFTP 服务器软件包不同版本之间发生了什么变化的信息。

![](img/9139201cfcaf4292284a0eed074928e5_417_0.png)

### 不同已安装软件包的数据库

已安装 RPM 有两个基本数据库。通过 RHEL 5，基本列表存储在 `/var/log/rpmpkgs` 中。然而，由于该数据库每天仅更新一次，因此最好只使用以下命令获取已安装软件包的当前列表：

```
# rpm -qa
```

`/root/install.log` 文件包括 RHEL 在此系统上安装时包含的所有软件包。安装后它不会更新。因此，一旦安装了新的或更新的软件包，该文件就会过时。如果需要，您可以通过安装 `rpm-cron` 软件包在 RHEL 6 中设置相同的 `/var/log/rpmpkgs` 数据库。

## 认证目标 7.03

### 依赖关系和 yum 命令

`yum` 命令使向系统添加和删除软件包变得容易。它维护一个关于如何正确添加、升级和删除软件包的数据库。这使得使用单个命令相对简单地添加和删除软件。该单个命令克服了被称为“依赖地狱”的问题。

`yum` 命令最初是为 Yellow Dog Linux 开发的。名称基于 Yellow Dog updater 的修改。鉴于依赖地狱带来的麻烦，Linux 用户受到了寻找解决方案的激励。它在杜克大学开发人员的帮助下被改编用于 Red Hat 发行版。

`yum` 的配置取决于称为存储库的软件包库。 Red Hat 存储库通过 RHN 进行配置。由于第三方重建发行版的存储库不能使用 RHN（没有订阅），它们使用公开可用的服务器。在任何情况下，了解 `yum` 命令的工作原理都很重要，它如何安装和更新单个软件包以及软件包组。

### 依赖地狱的一个例子

为了更了解 `yum` 命令的必要性，请查看图 7-4。该图中列出的软件包是构建 RPM 所需的。虽然构建 RPM 软件包是 RHCE 要求，但相关软件包很好地说明了 `yum` 的必要性。

### 图 7-4

构建 RPM 所需的软件包

```
[root@server1 SPECS]# rpmbuild -bp --target=`uname -m` kernel.spec

Building target platforms: x86_64

Building for target x86_64

error: failed build dependencies:

gcc >= 3.4.2 is needed by kernel-2.6.32-71.7.1.el6.x86_64

redhat-rpm-config is needed by kernel-2.6.32-71.7.1.el6.x86_64

patchutils is needed by kernel-2.6.32-71.7.1.el6.x86_64

elfutils-libelf-devel is needed by kernel-2.6.32-71.7.1.el6.x86_64

zlib-devel is needed by kernel-2.6.32-71.7.1.el6.x86_64

binutils-devel is needed by kernel-2.6.32-71.7.1.el6.x86_64

hmaccalc is needed by kernel-2.6.32-71.7.1.el6.x86_64

[root@server1 SPECS]#
```

你可以尝试使用 `rpm` 命令安装这些软件包中的每一个。为此，请执行以下步骤：

- 1. 插入 RHEL 6 DVD。将光盘插入其驱动器，或确保它包含在目标虚拟机的配置中。
- 2. 除非它已挂载，否则使用以下命令挂载该 DVD。当然，可以用不同的空目录替换 `/media`。
```
# mount /dev/sr0 /media
```
- 3. 导航到 DVD 挂载的目录，即 `/media` 或 `/media` 的某个子目录。
- 4. RHEL 6 DVD 上的 RPM 软件包可以在 DVD 的 `Packages/` 子目录中找到。导航到该子目录。
- 5. 输入 `rpm -ivh` 命令，然后输入图 7-4 中列出的软件包名称。为此，使用命令补全可能最简单；例如，如果你要输入：
```
# rpm -ivh gcc-
```
