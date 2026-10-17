
`swat    stream    tcp    nowait.400    root    /usr/bin/swat swat`

- 17. 在修改后强制你的系统重新读取 `inetd.conf`：

`/etc/init.d/netbase reload`

- 18. 最后，重启 Samba 服务：

`/etc/init.d/samba start`

# 从源码安装 Samba

习惯了 Windows 二进制包世界的人最初可能会觉得从源码编译和安装的想法有些令畏。

幸运的是，它实际上并没有初看起来看起来那么困难或复杂。许多源码分发包都打包得非常好，可以以最小的难度进行构建。关键点是确保开发工具（即你的编译器、链接器和 `make` 工具）是最新的且正确安装的。你还需要了解你安装了哪些库，以及你正在安装的包需要哪些库。

Samba 不需要任何非常特殊的库，除非你计划进行带有 SSL 支持或其他功能的级配置。此唯一的例外是 PAM（可插拔认证模块），它经常用于 Linux 变体（特别是 Red Hat 和 Caldera）。对于这一点，你需要获取 PAM 库，这些库通常由操作系统制造商以包的形式提供。

# 有哪些不同的形式？

最常见的 Samba 形式是压缩的 `tar` 文件。对于这种形式，你需要 UNIX `tar`（磁带归档器）工具，它通常随 UNIX 和 Linux 发行版一起。`tar` 工具有多个版本，每个版本的参数也不同。最常见的区别是内置对 `gzip`（GNU Zip）压缩的支持。如果 `tar` 支持 `z` 参数，则内置了 `gzip` 压缩；否则，你需要 `gzip` 工具。如果你没有 `gzip`，可以从 `www.gnu.org` 获取。

Gzipped `tar` 包可以从全球各地的 Samba `http` 和 `ftp` 服务器主机获取。对于离你最近的 Samba 镜像，请检查 `www.samba.org`。

访问 CVS 有两种方法。第一种是通过一个名为 `cvweb` 的工具，它允许通过浏览器访问，并从 Samba CVS 站点连接。第二种是更传统的方法——使用匿名 CVS 客户端。本节将介绍第二种方法。你需要拥有 `cvs` 工具（你应该已经作为系统的标准开发工具安装了它）以及互联网连接。请以 `root` 身份执行以下步骤：

- 1. 创建一个名为 `samba` 的符号链接，指向你拥有的最新 Samba 开发源码的未压缩版本：

```bash
% cd /usr/local/src
% ln -s /samba-2.1/ /samba/
```

- 2. 连接并登录到 CVS 服务器：

```bash
% cvs -d rpserver:cvs@cvs.samba.org:/cvroot login
```

使用你的密码登录。如果登录尝试失败，请确保你处于一个包含名为 `samba` 子目录的目录。

- 3. 执行以下命令：

```bash
% cvs -d rpserver:cvs@cvs.samba.org:/cvroot co samba
```

这将把子目录的内容更新为最新的 `samba` 源码。由于源码不是压缩格式，如果你通过调制解器连接，这可能需要一些时间。

- 4. 退出 CVS 系统：

```bash
% cvs -d rpserver:cvs@cvs.samba.org:/cvroot logout
```

每当你想用最新源码更新内容时，只需执行以下步骤：

- 1. 切换到 CVS 源码目录：

```bash
% cd /usr/local/src/samba
```

- 2. 连接并登录到 CVS 服务器：

```bash
% cvs -d rpserver:cvs@cvs.samba.org:/cvroot login
```

使用你的密码登录。如果登录尝试失败，请确保你处于一个包含名为 `samba` 子目录的目录。

- 3. 执行以下命令：

```bash
% cvs update -P
```

- 4. 退出 CVS 系统：

```bash
% cvs -d :rpserver:cvs@cvs.samba.org:/cvroot logout
```

## 配置并运行源码安装

通过之前描述的任一方法获取源码分发版，并以 `root` 进入你想安装它的目录。在 Linux 系统上这通常是 `/usr/local/src`，但可能会因你的站点而异。

我通常使用 `/usr/local/sources` 存储归档软件，使用 `/usr/local/src` 存放用于安装的未压缩包。这些是我将在示例中使用的目录。你应该根据你的站点对其进行修改。

### 解压源码

切换到源码安装目录：

```
% cd /usr/local/src
```

使用 `tar` 工具解压存档文件：

```
% tar xvfz /usr/local/sources/samba-2.0.6.tar.gz
```

或者

```bash
% gzip -dc /usr/local/sources/samba-2.0.6.tar.gz | tar xvf -
```

这将在 `/usr/local/src` 下创建一个名为 `samba-2.0.6`（或类似的名称，取决于你使用的版本）的目录。构建 Samba 的源码文件位于源码子目录中。切换到该目录：

```
% cd samba-2.0.6/source
```

### 配置并构建 Samba

现在，你需要为你的系统配置 Samba：

```
% ./configure
```

接下来，编译并安装 Samba：

```
% make
% make install
```

Samba 现在将安装在默认目录：`/usr/local/samba`。有关已安装目录结构的详情，请参考“特定于安装的文件位置”（Installation-Specific File Locations）章节。

## 配置系统以识别 Samba

一旦 Samba 安装在 `/usr/local/samba` 中，你需要更改一些系统配置文件，告诉系统在 Samba 服务随系统启动时以及从 shell 正常执行时去哪里查找二进制文件。此外，你可能还希望将手册页的路径包含在系统的 `MANPATH` 变量中，以便能够找到有关 Samba 二进制文件的信息。

### 配置 PATH 和 MANPATH 变量

你必须修改系统的 `PATH` 和 `MANPATH` 变量，以便能够找到用于执行的二进制文件和手册页。这些通常设置在如 `/etc/profiles`、`/etc/bashrc` 或 `/etc/csh.cshrc` 等文件中，取决于你的系统。

对于基于 `sh` 和 `bash` 的系统，添加以下行：

```
PATH=$PATH:/usr/local/samba/bin
MANPATH=$MANPATH:/usr/local/samba/man
```

并确保在它们之后出现类似下面的行：

```
export PATH MANPATH
```

对于基于 `csh` 和 `tcsh` 的系统，添加以下行：

```
setenv PATH "$(PATH):/usr/local/samba/bin"
setenv MANPATH "$(PATH):/usr/local/samba/man
```

### 配置守护进程

为了保证 Samba 始终运行（即使你重启服务器也是如此），你需要配置系统在启动时自动启动 Samba `smbd` 和 `nmbd` 守护进程服务。通常这些服务启动在如 `/etc/rc`、`/etc/rc.local` 或 `/etc/rc.d/init.d/smbd` 等文件中，取决于你的版本。

- 1. 进入你的编译目录并“解压”新版本；然后进入源子目录：

   % cd /usr/local/src

   % gzip -cd /usr/local/sources/samba-2.1.tar.gz | tar xf -

   % cd samba-2.1/source

- 2. 现在，当你执行配置命令时，你通过传递一个参数来告诉它将其安装到不同的位置：

   % ./configure --prefix=/usr/local/samba-2.1

- 3. 继续编译并安装：

   % make

   % make install

现在你可以使用符号链接指向实际源目录，在不同版本之间进行切换。

- 4. 重命名你自定义的 Samba 安装目录名称：

   % mv /usr/local/samba /usr/local/samba-2.0.6

- 5. 链接到你当前想要使用的版本：

   % ln -s /usr/local/samba-2.1 /usr/local/samba

在你的系统中，配置文件可以保持原样，你只需通过使用以下方法在两个（或更多）安装目录之间切换即可：

```
% rm -f /usr/local/samba
% ln -s /usr/local/samba-2.0.6 /usr/local/samba
```

对于 Samba 守护进程，我建议使用简单的脚本来停止守护进程并交换目录，这是一个示例：

```bash
#!/bin/sh
/etc/rc.d/init.d/smbd stop
rm -f /usr/local/samba
ln -s /usr/local/samba-2.0.6 /usr/local/samba
/etc/rc.d/init.d/smbd start
```

# 安装特定文件位置

众所周知，每个专有的 UNIX 版本都有自己的目录结构安排和系统配置方法。这曾是 UNIX 的噩梦，也是它在 20 世纪 80 年代失去许多声誉的原因。因为每种 UNIX 都是特定的（不仅考虑 System V 和 BSD 之间的差异），每个变体都需要特定的知识。因此，微软在 UNIX 上取得了了大量进展。

## Samba 简介

第一部分

遗憾的是，尽管程度较轻，Linux 也面临着类似的困境。尽管 Linux 的本质意味着许多内容在各种发行版中都是标准且通，但每个发行版为各种文件选择了略不同的位置，系统配置文件的组织方式略有不同。幸运的是，对于 Linux 来说，这些差异不大，任何一个发行版的经验管理员都应该快速适应另一个发行版。

# Samba 的默认文件位置

由于没有取决于站的配置选项，Samba 将自身安装到目录 `/usr/local/samba` 中。表 5.3 显示了 Samba 的默认目录结构。

表 5.3 Samba 默认目录结构

| 目录 | 描述 |

|---|---|

| bin/ | 二进制文件（包括管理二进制文件和守护进程） |

| lib/ | 存储 `smb.conf` 和 `smusers` 配置文件的位置 |

| lib/codpages/ | 存储国际语言支持的 codpages 的位置 |

| man/ | 手册页 |

| swat/ | Samba Web 管理工具 (SWAT) |

| var/ | 存储状态信息（如日志和锁文件）的目录 |

| private/ | Samba 存储 `smpasswd` 文件和 ID 文件的位置 |

有几个关键的配置文件与 Samba 相关联，如表 5.4 所示。

表 5.4 Samba 配置文件

| 文件 | 描述 |

|---|---|

| smb.conf | Windows INI 格式的 Samba 主配置文件 |

| smpasswd | Samba 密码列表，类似于 `/etc/passwd` |

| smbusers | Windows 到 UNIX 用户名的映射（例如 Administrator 映射到 root） |

# Linux 发行版上的示例文件和目录位置

表 5.5 显示了本章涵盖的三个 Linux 发行版的关键 Samba 目录和资源的默认位置。

# 表 5.5 Samba 文件在 Linux发行版上的位置

| 文件类型 | Red Hat Linux | Caldera OpenLinux | Debian GNU/Linux |

|---|---|---|---|

| smb.conf | /etc | /etc/samba.d | /etc |

| smpasswd | /etc | /etc/samba.d | /var/samba |

| 锁文件 | /var/lock/samba | /var/lock/samba.d | /var/lock |

| 日志文件 | /var/log/samba | /var/log/samba.d | /var/log |

| 客户端二进制文件 | /usr/bin | /usr/bin | /usr/bin |

| Samba 守护进程和管理二进制 | /usr/sbin | /usr/sbin | /usr/sbin |

| SWAT | /usr/share/swat | /usr/share/swat | 未安装 |

# 测试你的安装

在将 Samba 服务器安装到生产环境之前，你应该认真考虑测试配置及其与网络上其他 CIFS 客户端的交互。此举优点有两点。首先，它将帮助你更清楚地理解 CIFS 和 Samba 是与客户端交互的。它甚至可以帮助你更好地理解 Windows 客户端使用 CIFS 的方式。其次，它将帮助你上线做好准备。通过确保完全理解发生的情况，你能够减少对用户的影响并维护你的声誉。本节将帮助你测试并诊断 Samba 安装中的问题。

# 设置测试环境

你应该准备以下最小配置：

- 在继续之前，对于 Linux 准备好以下最小配置：- 尽管 Linux 的本质意味着许多内容在各种发行版中都是标准且通用的，但每个发行版为各种文件选择了略不同的位置，系统配置文件的组织方式略有不同。幸运的是，对于 Linux 来说，这些差异不大，任何一个发行版的经验管理员都应该快速适应另一个发行版。

# 只是一个简单的配置示例

```ini
[global]
workgroup = MYGROUP
[homes]
read only = No
[public]
guest ok = Yes
```

# 测试你的安装

在将 Samba 服务器安装到生产环境之前，你应该认真考虑测试配置及其与网络上其他 CIFS 客户端的交互。此举优点有两点。首先，它将帮助你更清楚地理解 CIFS 和 Samba 是与客户端交互的。它甚至可以帮助你更好地理解 Windows 客户端使用 CIFS 的方式。其次，它将帮助你上线做好准备。通过确保完全理解发生的情况，你能够减少对用户的影响并维护你的声誉。本节将帮助你测试并诊断 Samba 安装中的问题。

# 设置测试环境

你应该准备以下最小配置：

- 在继续之前，对于 Linux 准备好以下最小配置：- 尽管 Linux 的本质意味着许多内容在各种发行版中都是标准且通用的，但每个发行版为各种文件选择了略不同的位置，系统配置文件的组织方式略有不同。幸运的是，对于 Linux 来说，这些差异不大...

## Samba 简介

第一部分

如果你有与此处所示类似的体验，这意味着你已经有一个可以工作的 Samba 配置，并且你的服务器已成功共享并连接到 CIFS 服务。下一步要在 Windows 机器上进行检查。

## 使用 Samba 和 Windows 客户端进行测试

一旦你已经在你的 Samba 服务器上进行了本地测试，并确定一切运行正常，就是时候尝试测试 Windows 机器与 Samba 服务器之间的连接了。最简单的配置是使用一个 Samba 服务器和一个 Windows 9x 客户端。

## 使用 smbClient 命令测试 Windows 文件共享

在你的 Windows 机器上，创建一个简单的文件共享。示例例如：

- 1. 打开“我的电脑”。

- 2. 右键点击 C 盘图标（如果 C 盘不存在，则点击其他），并从弹出菜单中选择“共享”。

- 3. 如图 5.4 所示，选择“共享为”，并点击确定。

![](img/3a3dd42091ecc215c9b779bbd31cd990_189_0.png)

现在，在 Samba 服务器上以任何用户身份登录 shell，使用 `smbclient` 命令连接你刚刚创建的 Windows 9x 共享。

## 使用 Windows 9x 或 NT4 工作站客户端测试 Samba 共享

当你的 Samba 机器连接到同一个局域网，且 Samba 运行之前的之前的配置文件运行时，打开你 Windows 机器上的“资源管理器”或“网络邻域”。你应该能够像图 5.5 所示看到文件共享。（Windows 9x 客户端有时需要一段时间来刷新其浏览器。）你应该能够通过以下方法直接访问 Samba 服务器：

- 1. 点击“开始”

- 2. 选择“运行”。

- 3. 在命令框中输入 `MACHINENAME` 并点击确定。

将出现一个 Explorer 样式的窗口，显示两个文件共享：一个用于公共（public），另一个用于你的用户（用户名）。图 5.5 显示了 Windows 98 上的 Explorer 5.0 显示的基本文件共享。

图 5.5

使用 Windows 98 查看 Samba 共享。

![](img/3a3dd42091ecc215c9b779bbd31cd990_190_0.png)

## 故障排除提示

如果你在使用 Samba 时遇到问题，请先查看本节后部分的常见问题列表，看看它是否包含在内。

Samba 提供了大量的文档，在需要更多细节和进行故障排除时应始终参考这些文档。文档通常位于预装系统的 `/usr/doc` 下，也可以在 Samba 源码的 `docs` 目录下找到。

你还可以参考互联网上的许多资源。

## 如果某些不起不起去哪里寻找

Samba 网站包含关于 Samba 的最新信息和丰富的资源。主站可以在 `www.samba.org` 找到，它在全球范围内都有镜像。
