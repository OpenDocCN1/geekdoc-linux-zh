
```
:Z: /bin/compress -c %s:T_REG|T_ASCII:O_UNCOMPRESS-UNCOMPRESS
: :Z:/bin/compress -c %s:T_REG|T_ASCII:O_COMPRESS
: :gz: /bin/gzip -c %s:T_REG|T_ASCII:O_COMPRESS:GUNZIP
: :gz:/bin/gzip -9 -c %s:T_REG|O_COMPRESS:GZIP
: :tar:/bin/tar -c %s:T_REG|O_COMPRESS:GZIP
: :tar.gz:/bin/tar -cz %s:T_REG|O_COMPRESS:GZIP
: :tar.gz:/bin/tar -xz %s:T_REG|O_COMPRESS:GZIP
: :tar.bz2:/bin/tar -cjf %s:T_REG|O_COMPRESS:BZIP2
: :tar.xz:/bin/tar -c %s:T_REG|O_COMPRESS:GZIP
```

（注：由于原文文本在此处似乎截断或存在异常，此处根据上下文保留了逻辑占位）

如果上述路径不正确，请将其更改为相应的值。

现在编辑完此文件后，将其复制到 `pathnames.h` 中指定的位置。

## ftpusers 文件

首先，查看 `ftpusers` 示例：

```
root
bin
daemon
digital
field
guest
nnbody
operator
ris
sccs
sys
uucp
```

这些是可以登录 FTP 服务器的用户名。你可以根据意愿删除或添加此列表，但请记住默认值是因为可能的安全漏洞而选择的。

完成此文件后，将其复制到 `pathnames.h` 中指定的位置。

## ftpgroups 文件

`ftpgroups` 文件旨在让你创建一个允许 FTP 到你系统的用户组。示例内容如下：

```
test:ENCRYPTED PASSWORD:archive
```

示例中的项目代表：

- `test`: 这是访问名称。
- `ENCRYPTED PASSWORD`: 这是该组的密码，位于 `etc/passwd` 中。
- `archive`: 这是与该条目相关的组名。

> 提示 创建此密码的方法是创建一个虚拟用户，给该用户一个密码，然后直接从 `etc/passwd` 中复制。然后删除该虚拟用户。

用户要利用此功能，他将通过标准程序登录你的 FTP 服务器。然后他将执行 `SITE GROUP` 和 `SITE PASS` 命令获取分配给他的额外权限。

如果你想对用户从何处 FTP 进行控制（允许和禁止的主机），你可以使用 `fthosts` 文件允许或拒绝访问。如果你只想让人们从特定位置 FTP，或者如果你发现有人从特定位置使用你的站点（例如上传你不允许的文件），这将很有用。`fthosts` 文件的内容如下：

```
# 示例主机访问文件
# # ' 之后的内容被视为注释
# 空行被忽略

allow bartm somehost.domain
deny fred otherhost.domain 131.211.32.*
```

注意语法分为列：

- `allow` 或 `deny`
- 你想要允许或限制的账户用户名
- 允许或禁止登录的完整域名或 IP 地址列表，包括特定主机的名称（如果你指的是该站点的所有主机，则使用 `*`）。名称之间只需要空格。

> 注意 如果你使用 `allow`，只有来自你显式列出的主机的人才能以指定的用户名进行 FTP。

一旦完成编辑此文件（如果你想使用话），将其复制到 `pathnames.h` 中指定的目录。

## 设置 Site EXEC 程序

如果你想允许匿名用户在你的 FTP 服务器上运行可执行文件，请将这些程序放入 `pathnames.h` 指定的目录中。

> 注意 要格外小心放入此目录的物品；你不想为自己制造一个安全漏洞！

## 最后安装步骤

安装 FTP 服务器你还需要完成以下最后几项工作：

- 1. 以 `root` 身份登录。
- 2. 进入你存储 FTP 预编译文件的目录。
- 3. 切换 `bin` 目录。
- 4. 运行 `ckconfig` 文件以双检查你是否正确安装了额外文件。此程序将告诉你所有额外配置是否已放置在正确的位置。你可能想将输出重定向到文件（我在这里再次说明），以便捕获任何错误，只需输入：

```
ckconfig > blot
```

## 启动你的 FTP 服务器

现在启动 FTP 服务器变得简单了！只需执行以下操作：

- 1. 找到 `inetd` 的进程 ID（PID）。
- 2. 输入 `kill -HUP process ID`（例如 `kill -HUP 345`）来杀死并重启服务器。

## 验证你的 FTP 服务器运行正常

完成这些工作后，能够使用你的 FTP 服务器感觉很棒！让我们向你的 FTP 站点放入一个文件查看，安装一个更好的 FTP 客户端，并测试服务器以确保其运行正常。

## 在你的 FTP 服务器中存储文件

如果你想知道人们登录你的 FTP 服务器时会看到什么，请查看 `"ftp"` 目录。这是他们起始目录。从那里，你可以按照意愿构建服务器的文件系统。按照一般规则，你已经创建的 `"ftp/pub"` 目录是你想要让公众访问的文件存放处。

另一个标准是 `"ftp/incoming"` 目录，人们可以从那里向你的站点上传材料。如果你确实创建了这个目录，请确保设置了权限以便人们可以写入！

## 注意事项

只有当你确定想要人们通过 FTP 将材料上传到你的站点时，才创建 `incoming` 目录。你可能会发现人们利用此目录上传大量非法物品，以便他们的朋友在你看到并删除它们之前将其取走，例如盗版软件和儿童色情。

如果你创建了 `incoming` 目录，务必定期检查它，并检查其中包含的文件，而不仅仅是查看文件名。

如果你非常担心确定哪些类型的文件是非法的，你需要联系当地律师。你也可以联系 EFF（电子自由基金会）。其主页 URL 在第 9 章“安装 UseNet 软件”给出。

此外，检查 `incoming` 目录中出现的所有 MS-DOS 和 Macintosh 文件是否有病毒，特别是如果你不确定是谁上传了它们！

如果你有任何想要提供的文件，尽管开始在你的 FTP 服务器中安排它们吧！确保你的目录和文件的权限符合你的要求。

## 替代 FTP 客户端

尽管你已经有一个 FTP 客户端，但另一个选择是 `NcFTP`。这是一个更灵活且“高级”的客户端，允许你执行额外操作，例如无需下载即可查看文件，以及恢复由于某种原因中断的文件传输。

## 查找并解压客户端

你在这里将安装的 FTP 客户端是 `nctfp-2.1.0`。

定位并解压 FTP：

- 1. 定位文件 `/slackware/n4/tcpip.tgz`
- 2. 将其拷贝到 `/user/src` 或 `/incoming`。
- 3. 输入 `gunzip tcpip.tgz`。
- 4. 输入 `tar -xvf tcpip.tar`。

此包包含 NcFTP 的二进制文件。查看 `README` 文件了解该包的属性。

## 测试你的 FTP 服务器

现在让我们看看一切是否运行正常！有许多访问途径和功能需要测试。

## FTP 连接到你的站点

同时测试在 `ftpsoft` 中匿名 FTP 的能力以及 FTP 到用户账户的连接。

例如，我将匿名 FTP 到 `ftp.renaissoft.com`。从我的个人账户，我只需输入 `ftp.renaissoft.com`。NcFTP 足够智能可以自己识别你的电子邮件地址，所以你不需要将其作为密码输入。然后，我获得了机器的欢迎信息并收到提示（见图 10.1）。

图 10.1

匿名 FTP 到 `ftp.renaissoft.com`。

![](img/df069eac9f46c8d8f72de31230fb3cab_237_0.png)

> 提示

> NcFTP 的一个方便功能是它会记住站点名称。下次我想要匿名访问 `ftp.renaissoft.com` 时，只需输入 `ftp.renaissoft.com` 即可。

正如你所注意到的，你甚至不需要输入 `anonymous` 作为用户 ID。这是因为 NcFTP 默认认为你想执行匿名 FTP。我在这里再举一个非匿名 FTP 的例子。这次，我想访问同一台机器，但使用我自己的账户。我将输入 `ftp -u ftp.renaissoft.com`。然后，我在提示处使用我的用户 ID（`dee`），并在密码提示处使用我的密码。从那里，我直接进入自己主目录的提示符（见图 10.2）。

```
davinci [home/davinci]: ftp -u ftp.renaissoft.com
Login: dee
Password:
User logged in
davinci [home/davinci]: 
```

图 10.2

作为非匿名用户 FTP 连接到机器。

> 提示

> 在某些服务器上，如果你想获取多个文件，可以使用 `mget` 命令。例如，如果你想获取 `file1` 和 `file2`，可以输入 `mget file1 file2`。然而，此命令并不适用于所有服务器。

## 第 10 章—安装 FTP 软件

图 10.5

从 FTP 服务器获取文件。

```
davinci> pub
davinci> get welcome.msg
Receiving file: welcome.msg
100% [####################] 618 bytes ETA 0:00
welcome.msg 618 bytes received in 0.07 seconds. 9.20 K/s
davinci#
```

> 提示

> NcFTP 会记住你上次离开服务器时所在的目录，并在你返回时带你回到那里。

确保人们无法将文件放入 `incoming` 以外的目录。`/incoming` 目录与另一个目录之间权限的一个简单示例，请查看图 10.7 中的两个文件列表。

| | root | vhtml | 1024 Apr 22 1995 | : |

|---|---|---|---|---|

| drwxr-xr-x | root | vhtml | 1024 Dec 19 02:03 | incoming/ |

图 10.7

`/incoming` 目录与任何其他 FTP 目录之间的权限差异。

如果你在这些项目中的一个或多个上遇到问题，请仔细检查所有权权限。

# 特殊配置选项

如果你使用了 `pathnames.h` 文件中的任何特殊项目（例如用户组），请也对它们进行测试。如果你在这些项目上遇到问题且无法解决，请记住你安装了服务器，因此可以访问帮助页（manual pages）。

> 提示

有一个名为 `xftp` 的 X-Windows FTP 客户端。你可以通过 Netscape 进行网络搜索找到它。它在 `sunsite.unc.edu` 及其镜像站点上可用。

# 第 11 章

## 安装 Finger 服务器软件

如果你希望人们能够获取关于用户的特定类型信息，例如他们最后在线的时间，或最后检查邮件的时间（这些信息是可配置的），你将需要安装 Finger 服务器。与其安装默认的 Finger 服务器，你将安装一个更具配置性的服务器，这将让你和你的用户对输出外界的信息有更多控制权。

提供 Finger 服务是一种让人们设置某些内容向世界简单介绍他们自己的简单方法。在某种程度上，Finger 提供了创建一个简单的个人 Web 网页的机会！此外，外部用户可以使用 Finger 查找某人的电子邮件地址。

在本章中，你将学习如何：

- 配置你的 Finger 服务器
- 编译你的 Finger 服务器
- 安装你的 Finger 服务器
- 配置 Finger 输出
- 验证你的 Finger 服务器运行正常

## 配置你的 Finger 服务器

再次强调，这是一个你必须编译的服务器。然而，代码没有比 Finger 服务器更简单了，所以这个编译过程应该是相当省心的。只需只需花些时间，确保在可能进行的少量文件编辑期间不要任何拼写错误。

## 查找并解压服务器源码

你将使用的 Finger 服务器是 `Kfingered-0.04`。这是一个守护进程（daemon），它在后台运行并等待 Finger 请求进入。

要定位并解压 Kfinger，请执行以下步骤：

1. 在 CD-ROM 上找到 `kfingered-0.04.tar.gz` 文件。
2. 将其拷贝到 `/usr/src`。
3. 为你的 Finger 工作创建一个目录，例如 `md finger`。
4. 将 `kfingered-0.04.tar.gz` 移动到你创建的目录中。
5. 输入 `gunzip kfingered-0.04.tar.gz`。
6. 输入 `tar -xvf kfingered-0.04.tar.gz`。

现在，在编译 Finger 服务器之前，你需要进行少量的文件编辑。事实上，如果你不创建虚拟账户（为了让人们可以 Finger 他们并从你的站点获取信息而创建假账号，例如 `info`），你不需要编辑任何内容。

如果你不计划创建虚拟账户，请跳到下一节。如果你不确定，请继续操作并进行少数必要的更改。

要进行你想要的更改，请执行以下操作：

> 注意

此程序中的注释行以 `/*` 开头并以 `*` 结束。

1. `/* #define NO_DUMMY_PROGRAMS */`

你可能想要取消这一行的注释。这将封堵某些入侵者可能知道如何使用的潜在安全漏洞。我将按如下方式取消注释：

```
#define NO_DUMMY_PROGRAMS
```

2. `/* Define NOSUCHUSERPATH and NOSCHUCHUSERFN to enable custom handling */`

/* 对未知用户的 Finger 进行处理。

如果你想设置 Finger 如何处理针对不存在的账户的传入请求，请取消 `dummy.c` 中这部分的注释。

第一个项目 `NOSCHUCHUSERPATH` 定义了 Finger 查找的路径，以查看如何处理对未知用户的信息请求。第二个项目 `NOSCHUCHUSERFN` 定义了 Finger 应在定义的路径中查找的文件。我将保留默认文件名并按如下方式取消注释：

```
#define NOSUCHUSERPATH "/etc/"
#define NOSUCHUSERFNM "badfinger"
```

查看默认的 `finger.c` 看看你是否想保留它；许多系统管理员不会这样做。默认文件对无效用户请求的响应会列出有效用户列表，这可能对你不可接受。你可能想更改 `finger.c`，以便如果你不使用此文件，它将提供自定义的文本响应，对无效用户的响应将是 `finger: username: no user`。

## 编译并安装你的 Finger 服务器

Finger 是一个简单的程序，所以编译所需的时间很短，只需要一点时间。

### 编译 Fingerd

要编译 Kfingerd，请执行以下操作：

1. 以 `root` 身份登录。
2. 进入该目录。
3. 输入 `make`。
4. 编译器给出的信息。

### 安装 Fingerd

安装你的服务器有几个相当简单的步骤。

### 创建 Finger 的家目录

首先，为 Finger 创建一个家目录。要创建此目录，请执行：

1. 以 `root` 身份登录。
2. 进入家目录。
3. 创建目录。
4. 更改权限（`chmod 755`）。

### 移动 Fingerd

将编译后的文件 `Fingerd` 移动到类似 `/usr/sbin` 的地方。

### 将 Fingerd 添加到启动项

要在启动时运行 Fingerd，请执行以下操作：

1. 以 `root` 身份登录。
2. 进入 `/etc` 目录。
3. 编辑 `inetd.conf` 文件。
4. 确保存在以下行：

```
finger      stream      tcp      nowait      root      /usr/sbin/kfingerd
```

> 提示

你会在 `inetd.conf` 中发现此行，但用户是不正确的。你只需要将用户改为 `root`。

5. 保存并退出文件 `inetd`。

重启系统以运行 Fingerd，或者输入 `kill -HUP #`（其中 `#` 是 `inetd` 的进程 ID），然后输入 `inetd` 重新运行。

选择 Kfingerd 而不是标准的、常用的 Finger 的原因之一因为它更具配置性。标准的 Finger 输出的信息并不是每个人希望人们访问的。Kfinger 允许每个用户选择哪些信息对外部 Finger 账户可见，哪些信息不可。

用于单独配置 Finger 输出的文件称为 `.fingerrc`。

### .fingerrc 命令

想要配置 Finger 输出的用户可以使用许多命令（参见 11.1）。

## 第 11 章—安装 Finger 服务软件

| 表 11.1 继续 | |

| :--- | :--- |

| 命令 | planfn | 定义计划文件的名称 |

| | progfn | 定义 Finger 应该调用的程序 |

| subdfnm | 定义存放计划文件的子目录 |

> 注意

> 括号 `[]` 中的条项是可选的。

> 对于最后四项（那些定义要调用或使用的文件的项），如果你不包含文件名，该项将被禁用。例如，如果你只输入了 `proffnm` 而没有文件名，项目文件将被禁用。

你也可以将表 11.2 中的参数添加在表 11.1 中列出的命令之前。

| 表 11.2 附加命令参数 |

| 参数 | 功能 |

| :--- | :--- |

| IP[!] | 除非来自列出的 IP 地址，否则[不要]执行该参数随后的命令 |

| HN[!] | 除非来自列出的主机名，否则[不要]执行该参数随后的命令 |

| HNR | 将主机重映射到其他地方 |

## 示例 .fingerrc 文件

现在，为了感受这些命令是如何协同工作的，让我们创建一个示例 `.fingerrc` 文件。假设我希望某些信息可用而某些不可用：

- 让外部人员查看我的邮件状态。
- 不要提供我的登录位置。
- 不要提供我的闲时间。
- 记录 Finger 请求。
