
属于 Samba 的旧文件将被删除并安装新文件。旧的 `smb.conf` 文件将保存为 `smb.conf.rpmsave`。

# 验证

`V` 选项可以以许多方式检查软件包。

**表 7–7 验证格式**

| 字符 | 属性 | 说明 |
| :--- | :--- | :--- |
| `5` | MD5 sum | 文件的校验和 |
| `S` | File size | 文件大小 |
| `L` | Symlink | 符号链接 |
| `T` | Mtime | 修改时间 |
| `D` | Device | 指定为设备文件 |
| `U` | User | 文件的用户 ID |
| `G` | Group | 文件的组 ID |
| `M` | Mode | 文件的权限 |

为了实验，尝试更改 `/etc/smb.conf` 的所有者为 `bin`，如下所示：

```bash
/bin/chown bin /etc/smb.conf
```

运行以下 RPM 命令，你会得到以下结果：

`S..U /etc/smb.conf`

`U` 表示 `/etc/smb.conf` 的所有者已更改。别忘了再次改回 `root`！

运行以下 `rpm -V samba` 命令，如果成功则不会返回任何消息。如果你想验证是否生效：

```bash
rpm -q nfs-server-clients-2.2.beta29-2
```

如果软件包已删除：

```bash
package nfs-server-clients-2.2.beta29-2 is not installed
```

使用以下命令重新安装 Samba：

```bash
rpm -ivh /mnt/cdrom/RedHat/RPMS/samba*
```

Samba 包含文件。在这种情况下会给出以下信息：

```bash
rpm -V samba
```

`S5.. /etc/smb.conf`

`S` 表示文件大小已更改，`5` 表示校验和已更改。

## 第 7 章：配置 Linux

要安装存储并分发在 tar 文件中的软件系统，你应该遵循以下指南：

- 1. 归档文件（这通常意味着将单独的文件保存到计算机上的一个或多个目录中）。如果 tar 文件是压缩过的（如果它具有以下后缀之一：`tgz`、`gz` 和 `Z`，则表示它是压缩过的），你可以指定 `tar` 选项来将其解压。
- 2. 大多数软件系统都带有一个 `makefile`，它中包含了编译和安装软件的规则。有时你需要显式地修改 `makefile` 或使用它来创建依赖关系——在这种情况下，输入 `make depend` 命令。更多信息请参阅 `make` 的手册页（`man make`）。
- 3. 编译软件。执行此操作的语法可以是 `make` 或 `make all`。
- 4. 可选地，`makefile` 会为你安装编译好的软件、配置和帮助文件——通常通过运行 `make install` 命令来实现。

就是这样。如果一切顺利，你的系统就安装好了。根据我的经验，大多数 Linux tar 系统在编译和运行时的问题极少。

![](img/29df11d9c5c608cff7b4fa65d0c78e37_298_0.png)

直到我开始写这本书时才意识到，Red Hat 的 CD-ROM 发行版并不包含任何单个 tar 文件。这与传统的 Linux 特尤其是 Slack 发行版相比是哲学上的巨大转变。如果 Red Hat 的哲学成为事实上的标准，互联网社区与商业领域可能会产生巨大的分歧。我设 Linux/GNU 社区的许多人将继续使用 tar 方法，而商业领域将迅速迁移到 RPM。这对于到今为止成功的软件开发周期是否意味着任何负面影响，目前无人能预知，但这可能是一个巨大的转变。

你总会有一些无法使用 RPM 的时候。在第 10 章和第 11 章中，我使用了 RPM 格式不可提供的安全导向型包。它们以 tar 形式提供，你需要手动安装和编译它们。

## 第三部分：一个重要的客户端-服务器网络

### 显示简单的帮助信息
大多数 Linux 命令和实用程序都提供简单快速的帮助系统。输入字符串 `--help` 或 `-h` 作为唯一参数，通常会显示一屏的选项。例如，以下命令显示了列表 7-10 所示的帮助信息：

```bash
/bin/gzip --help |
```

**列表 7-10：命令 `gzip --help` 显示了一个简单的帮助屏幕**

```
gzip 2.2.4 (18 Aug 93)

usage: gzip [-cdfhklNrtvV19] [-S suffix] [file ...]

-c --stdout 向标准输出写入，保持原始文件不变

-d --decompress 解压缩

-f --force 强制覆盖输出文件并压缩文件

-h --help 显示此帮助

-l --list 列出压缩文件内容

-L --license 显示软件许可证

-n --name 不保存或恢复原始名称和时间戳

-N --name 保存或恢复原始名称和时间戳

-q --quiet 抑制所有警告

-r --recursive 对目录进行递归操作

-S .suffix --suffix .suffix 在压缩文件上使用后缀 .suffix

-t --test 测试压缩文件完整性

-v --verbose 冗/详细模式

-V --version 显示版本号

-1 --fast 更快的压缩

-9 --best 更好的压缩

file... 要 (de)压缩的文件。如果没有给出，则使用标准输入。
```
