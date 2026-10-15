
如果你想执行的操作不需要新的元数据，可以让 `yum get-data` 仅从本地机器的缓存中获取。这将极大提高性能，但较小的风险是你正在查找的包信息可能自你上次更新元数据以来已经发生了变化。使用 `-c` 选项，你可以告诉 `yum` 使用元数据：

```
# yum -c info yum-utils
Setting up repositories
Reading metadata from local files
...
```

如果不使用 `-c`，如果该信息的本地缓存已过期超过 30 分钟（默认值），`yum` 将从存储库获取新的元数据。元数据的过期时间在 `/etc/yum.conf` 文件的 `metadata_expire` 选项中秒为单位设置（`metadata_expire=1800`）。

通过安装 `yum-utils` 软件包（`yum install yum-utils`），你可以使用一些实用的命令，用于访问和创建 yum 存储库。`repquery` 命令可用于列出 yum 存储库软件包软件包。例如：

```
# repquery -il tomcat5
# repquery --provides tomcat5
```

`yumdownloader` 有助于将软件包从 yum 存储库下载到本地磁盘。例如，以下命令将 `cacti` 软件包下载到本地目录：

```
# yumdownloader cacti
```

## 使用 rpm 管理软件

虽然 `yum` 已经取代 `rpm` 从在线存储库安装 RPM 包的工具，但 `rpm` 在查询 RPM 和验证已安装的 RPM 方面有一些特殊的选项。它也是安装、删除和验证计算机上可用 RPM 包的有用工具。

## 使用 rpm 命令

使用 `rpm` 命令，任何用户都可以查询本地 RPM 数据库。要使用该命令从系统中安装或删除软件，必须拥有 root 权限。

### 安装软件包

以下命令安装位于当前目录下的新软件包。该命令中的选项包括 `i` 表示安装，`v` 表示详细（verbose），以及 `h` 表示进度哈希标记。

```
# rpm -ivh rpmforge-release-0.2-2.2.fc5.rf.x86_64.rpm
Preparing... ########################### [100]
1:rpmforge-release ########################### [100]
```

以下示例了从互联网上安装新软件包。此方法适用于 http 和 ftp 协议：

```
# rpm -ivh http://ftp.belnet.net/packages/dries.ullysis.org/fedora/fc5/x86_64/RPM.dries/rpmforge-release-0.2-2.2.fc5.rf.x86_64.rpm
Retrieving http://ftp.belnet.net/packages/dries.ullysis.org/fedora/fc5/x86_64/RPM.dries/rpmforge-release-0.2-2.2.fc5.rf.x86_64.rpm
Preparing... ########################### [100]
1:rpmforge-release ########################### [100]
```

### 升级软件包

如果已经安装了旧版本的软件包，当你尝试安装它时会发生错误。使用 `-Uvh` 将现有软件包升级到新版本。

```
# rpm -Uvh flash-plugin-9.0.31.0-release.i386.rpm
```

### 删除软件包

要删除已安装的软件包，请如下使用 `-e` 选项：

```
# rpm -e rpmforge-release
```

有时在 64 位系统上，为了向后兼容性安装了 32 位软件包，你可能安装了两个或多个版本的软件包。如果你在尝试删除其中一个时遇到错误，你可能可以使用完整的包名或删除所有匹配的软件包来修复它：

```
# rpm -e avahi-0.6.11-3.fc5
# rpm -e avahi-0.6.11-3.fc5.i386
# rpm -e --allmatches avahi-0.6.11-3.fc5
error: Failed dependencies:
libavahi-client.so(3) (64bit) needed by (installed)
vino-2.13.5-2.2.x86_64
```

假设 `avahi` 软件包已安装，删除软件包的命令失败是因为安装了多个相同基础的包。第二个命令成功了（尽管它是静默执行的）。但请注意，最后一个命令因为依赖问题而失败了。解决依赖问题的最好方法是使用 `yum` 或手动处理依赖关系。然而，你可能会遇到必须强制安装或删除软件包的时刻。

警告！这样做是**危险的**，并可能导致系统不稳定。请确保你清楚自己在做什么。

在这里，你指定要删除 i386 版本的软件包并忽略依赖关系：

```
# rpm e --nodepops avahi-0.6.11-3.fc5.1386
```

### 查询 RPM 软件包信息

这显示了如何查询名为 `rsync` 的已安装软件包并显示该软件包的版本信息（你的版本号可能不同）：

```
# rpm -q rsync
sync-2.6.9-1.fc51
```

使用 `-qp` 选项获取当前目录中 RPM 的信息：

```
# rpm -qp rpmforge-release-0.2-2.2.fc5.rf.x86_64.rpm
```

要查看系统中所有安装软件包的列表，输入：

```
# rpm -qa
```

要查看 `rpmforge-release-0.2-2.2.fc5.rf.x86_64.rpm` 软件包的详细信息：

```bash
# rpm -qi rpmforge-release-0.2-2.2.fc5.rf.x86_64.rpm
```

要查看某个软件包包含哪些文件：

```bash
# rpm -ql rsync
```

要查看某个文件属于哪个软件包：

```bash
# rpm -qf /etc/yum.conf
```

要查看软件包提供的功能：

```bash
# rpm -q --provides rsync
```

要查看软件包所需的依赖：

```bash
# rpm -q --requires rsync
```

要查看谁提供了依赖：

```bash
# rpm -q --whatprovides rsync
```

要查看软件包的签名信息：

```bash
# rpm -q --whatsig rsync
```

要查看软件包的安装脚本：

```bash
# rpm -q --scripts rsync
```

要查看软件包的安装、卸载、升级等脚本列表：

```bash
# rpm -q --changelist rsync
```

要查看软件包的变更日志：

```bash
# rpm -q --changelog rsync
```

## 验证已安装的软件包

在某些情况下，你需要验证系统中安装的软件的行为。例如，当系统被入侵时，攻击者经常会用损坏的二进制文件替换 `ls` 或 `ps` 来掩盖踪迹。将文件系统与 RPM 数据库中存储的信息进行对比变得非常有用。

> 注意 替换关键二进制文件的入侵者也可能篡改你的 RPM 数据库。因此，将此工具作为检查系统有效性的一种方法，但不是唯一方法。

对于每个验证的软件包，`rpm` 会运行多个检查，并在行开头显示一系列字符。点表示检查通过。字母或数字表示检查失败。表 2-3 显示了最实用的检查项目及其失败对应的字符。

### 表 2-3：RPM 软件包验证失败消息

| 表示检查失败的字母 | 描述 |
|---|---|
| S | 文件大小不同 |
| M | 模式不同：包括权限和文件类型 |
| 5 | MD5 校验值不同 |
| U | 用户所有权不同 |
| G | 组所有权不同 |
| T | mTime（最后修改时间）不同 |

使用以下命令验证所有安装的软件包，并过滤出路径中包含 `bin` 的文件：

```
# rpm -Va | grep bin
S.5...T /usr/bin/curl
```

这显示文件系统的 `curl` 二进制文件的大小、MD5 校验值和修改时间与 curl RPM 带的不同。也就是说，该文件已被替换。以下是使用验证选项的几个其他示例：

```bash
# rpm -Vv coreutils               详细检查 coreutils 的文件
# rpm -V -f /usr/bin/pr             验证包含 pr 的软件包
# rpm -V -g Applications/Multimedia  验证所选组的软件包
```

# 第 2 章：安装 Fedora 和添加软件

## 重建你的 RPM 数据库
