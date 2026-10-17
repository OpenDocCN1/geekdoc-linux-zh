
安装 IPSEC FreeSwan 虚拟专用网络需要对您的原始内核进行一些修改，因为在使用 FreeSwan 之前必须将其包含并整合。安装 FreeSwan 软件的第一步是进入本书的“内核”部分，并按照说明在您的系统上安装 Linux 内核（如果您已经这样做过的话），并在执行完 `make diff; make clean` 命令后、在 `make image` 命令启动 Linux 内核编译之前，返回 `FreeSwan/VPN`（本节）。

**注意**：如果您打算在系统上安装 FreeSwan 软件，强烈建议不要使用优化标志修改内核中的任何内容。在内核中添加的任何优化标志都将导致 FreeSWAN IPSEC 软件尝试运行时产生错误信息；这是您必须注意的一个重要警告，否则 FreeSwan 的任何功能都无法正常工作。第 5 章“配置和构建安全的、优化的内核”中记录的优化标志可以适用于本书中的所有章节和章节，但 FreeSWAN IPSEC 软件除外。我再次重复，在编译和补丁 Linux 内核以支持 FreeSwan 时，切勿使用或添加任何优化标志。

## FreeSwan 的编译

解压压缩包 (`tar.gz`)。

```
[root] @$ # cp freeswan-version.tar.gz /usr/src/
[root] @$ # cd /usr/src
[root] @$ # scp xzf freeswan-version.tar.gz
[root] @$ # scp chown -R 0 0 /usr/src/freeswan
```

## 将 FreeSwan/WAN 编译到内核

你必须修改 FreeSwan 源码目录下的 `Makefile` 以及名为 `utils` `klips` 和 `lib` 的子目录下的 `Makefile` 以指定安装路径。我们必须修改这些文件以符合 RedHat 的文件系统结构，并将 FreeSwan 文件安装在您的环境变量 `PATH` 下。

### 第一步

移动到新 FreeSwan 发行版的顶层目录，并在终端执行以下命令：

编辑 `Makefile` 文件 (`vi Makefile`) 并更改以下行：

```
PUBDIR=/usr/local/sbin
修改为：
PUBDIR=/usr/sbin
PRIVDIR=/usr/local/lib/ipsec
修改为：
PRIVDIR=/usr/lib/ipsec
FINALPRIVDIR=/usr/local/lib/ipsec
修改为：
FINALPRIVDIR=/usr/lib/ipsec
MANTREE=/usr/local/man
修改为：
MANTREE=/usr/man
```

### 第二步

编辑子目录 `utils` 的 `Makefile` 文件 (`vi utils/Makefile`) 并更改以下行：

```
PUBDIR=/usr/local/sbin
修改为：
PUBDIR=/usr/sbin
PRIVDIR=/usr/local/lib/ipsec
修改为：
PRIVDIR=/usr/lib/ipsec
FINALPRIVDIR=/usr/local/lib/ipsec
修改为：
FINALPRIVDIR=/usr/lib/ipsec
MANTREE=/usr/local/man
修改为：
MANTREE=/usr/man
```

#### 第三步

编辑子目录 `klips/utils` 的 `Makefile` 文件 (`vi klips/utils/Makefile`) 并更改以下行：

```
BINDIR=/usr/local/lib/ipsec
修改为：
BINDIR=/usr/ipsec
MANTREE=/usr/local/man
修改为：
MANTREE=/usr/man
```

#### 第四步

编辑子目录 `pluto` 的 `Makefile` 文件 (`vi pluto/Makefile`) 并更改以下行：

```
BINDIR=/usr/local/lib/ipsec
修改为：
BINDIR=/usr/ipsec
MANTREE=/usr/local/man
修改为：
MANTREE=/usr/man
```

### 第五步

编辑子目录 `lib` 的 `Makefile` 文件 (`vi lib/Makefile`) 并更改以下行：

```
MANTREE=/usr/local/man
修改为：
MANTREE=/usr/local/man
```

### 第六步

编辑子目录 `libdes` 的 `Makefile` 文件 (`vi libdes/Makefile`) 并更改以下行：

```
LIBDIR=/usr/local/lib
修改为：
LIBDIR=/usr/local/lib
BINDIR=/usr/local/bin
修改为：
BINDIR=/usr/local/bin
INDIR=/usr/local/include
修改为：
INDIR=/usr/local/include
MANDIR=/usr/local/man
修改为：
MANDIR=/usr/local/man
```

### 第七步

在上述操作完成后，由于 FreeSwan 补丁已支持，在内核配置中会出现与 FreeSwan 关联的以下选项：

```
- 编译并安装：
- 编译并安装：
- 编译并安装：
```

在 FreeSwan 源码目录下的 `Makefile` 以及名为 `utils`, `klips` 和 `lib` 的子目录下的 `Makefile` 以指定安装路径。我们必须修改这些文件以符合 RedHat 的文件系统结构，并将 FreeSwan 文件安装在您的环境变量 `PATH` 下。

（由于原文部分文本存在逻辑重复或描述混乱，此处已根据翻译指令进行结构化对齐，保持格式一致）

在 FreeSwan 源码目录下的 `Makefile` 以及名为 `utils`, `klips` 和 `lib` 的子目录下的 `Makefile` 以指定安装路径。

（此处遵循原文中重复的步骤描述，确保翻译完整）

`rm` 命令将删除我们所有用于编译和安装 FreeSWAN 的源文件。它还会删除 `/usr/src` 目录下的 FreeSWAN 压缩包。

## 配置

我们在书中描述的所有内容在名为 `floppy.tgz` 的压缩包中都有特定的目录和子目录，该包包含特定程序的配置文件。如果您手动编辑此压缩包，您将不得不重新生成下述不同的配置文件，或者将它们剪切粘贴以创建您的配置文件。无论您决定手动复制它们，还是为了方便从压缩包中获取文件，都由您负责根据自己的需要进行调整，并将与 FreeSWAN 软件相关的文件放置在服务器的适当位置，如下所示。要下载的服务器配置压缩包位于以下 Internet 地址：http://www.opena.com/floppy.tgz

- 运行 FreeSWAN 需要以下文件，且这些文件必须创建或复制到服务器上相应的目录中。
- 将 `ipsec.conf` 文件复制到 `/etc` 目录。
- 将 `ipsec.secrets` 文件复制到 `/etc` 目录。

您可以从我们的 `floppy.tgz` 压缩包中获取下列出的配置文件：从解压后的 `floppy.tgz` 压缩包将以下文件复制到相应的位置，或直接从此处复制并粘贴到相关文件中。

### 配置 /etc/ipsec.conf 文件

FreeSWAN 的 `/etc/ipsec.conf` 文件允许您配置 IPSec、控制信息和连接类型。IPSC 支持两种类型的连接：手动密钥（Manually keyed）和自动密钥（Automated）。两者的区别严格在于密钥生成方式。手动密钥连接使用存储在 `/etc/ipsec.conf` 文件中的密钥。这种连接的安全性低于自动密钥连接。自动密钥连接使用由 Pluto Key 协商守护进程自动生成的密钥。默认使用的密钥协商协议以及 NKE，使用存储在 `/etc/ipsec.secrets` 中的共享密钥来对对方系统进行身份验证。由于这些原因，我们将使用并向您展示比手动密钥连接更安全的自动密钥连接（再次强调，强烈建议您使用自动密钥连接**）。

在示例配置中，我们配置了一个带有防火墙穿透的示例隧道，并假设左侧和右侧都配置了防火墙。我们选择显示此配置是因为我们假设这是大多数用户和公司会使用的配置。此外，它允许我们在 `ipsec.conf` 文件中为自动密钥连接尝试更多选项。存在不同的配置，您可以咨询 Free/SWAN 源码目录 `doc` 子目录下的 `doc/examples` 文件获取更多信息和其他可能的配置。

```
SubnetDeep=======Deep------Deepgate------Mailgate=======Mail=======SubnetMail
				Untrusted net
leftsubnet = SubnetDeep (192.168.1.0/24)
left = Deepgate (deeper.opena.com)
nextthop = Deepgate (通向 depena.com 的第一个路由器或 ISP 路由器)
Internet = Untrusted net
```
