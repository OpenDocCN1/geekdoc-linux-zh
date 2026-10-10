
创建 CD-ROM 文件系统后，你需要使用 `mount infocd` 将 CD-ROM 挂载到系统上（假设挂载点是 `/infocd`）。下一步是运行位于基础文档 CD-ROM 上的链接程序。首先，更改目录到 CD-ROM 挂载点——在本例中是 `/infocd`，然后运行 `linkbased` 命令。

```bash
# mount /infocd
# cd /infocd
# ./linkbased
```

`linkbased` 命令将创建指向 CD-ROM 上文档的系统符号链接。在这种情况下，`DocSearch` 和 `man` 页面的基本操作与将文档加载到本地硬盘上时相同。但是，响应时间可能非常差。

当你放弃使用 CD-ROM 并希望将文档安装在服务器磁盘上时，你首先需要移除所有先前创建的符号链接。IBM 考虑到了这一点，并创建了一个取消链接程序。要断开所有链接，请运行 `unlinkbased` 命令并移除 CD-ROM 文件系统。

```bash
# mount /infocd
# cd /infocd
# ./unlinkbased
# umount /infocd
# rmfs [-r] /infocd
```

> 注意 `rmfs` 命令上的 `-r` 开关将移除挂载点或目录。

## 固定磁盘上的 DocSearch

为了获得最佳性能，整个文档搜索服务库应安装在文档服务器本地的固定磁盘上。NFS 安装也能工作，但可用性则取决于 NFS 服务器。额外的复杂性层是不推荐的。你也可以安装 `DocSearch` 核心并让文档 CD-ROM 保持挂载状态，如前一节所述。这种方法可能极慢，具体取决于 CD-ROM 的速度，我们都知道 IBM 以拥有最新最快的 CD-ROM 驱动器而闻名，但服务器确实跑得很热！你还可以通过 NFS 挂载 CD-ROM 以获得更差的性能。接下来，我们将展示如何在 `AIX 4.3.3` 和 `5L` 版本 `5.1` 上安装 `DocSearch`。

## 在 AIX 4.3.3 上安装 DocSearch

如果 `inadm` 用户和组尚不存在，你首先需要在系统中为文档搜索服务定义一个新的用户和组。首先，创建一个名为 `inadm` 的组，然后创建一个名为 `inadm` 的新用户。`inadm` 用户应以其 `inadm` 组作为主组。确保语言环境变量设置为正确的值，对于美国英语为 `en_US`。

```bash
# echo $LANG
```

使用以下 SMIT 快速路径来更改语言变量：

```bash
# smitty chlang
```

接下来，安装以下文件集。在每种情况下，都列出了所在的 CD-ROM 以及具体的文件集。

### AIX 4.3.3 CD-ROM #1

```text
bos.docsearch.rte
bos.docsearch.client.Dt
bos.docsearch.client.com
bos.html.en_US.topnav.navigate
bos.msg.en_US.docsearch.client.Dt
bos.msg.en_US.docsearch.client.com
```

> **注意** 如果你的系统没有运行 CDE，则可以省略 `.Dt` 文件集。

### AIX 4.3.3 CD-ROM #2

```text
IMNSearch.bld.all
IMNSearch.rte.all
```

### AIX 4.3.3 基础文档 CD-ROM

```text
X11.html.en_US.all
bos.html.en_US.all
```

### AIX 4.3.3 附加包 CD-ROM，第 1 卷

```text
Netscape.communicator.com
Netscape.communicator.plugins
```

可选安装包括 `AIX 4.3.3` 扩展文档 CD。`AIX 4.3.3` 的扩展文档 CD-ROM 包含用户和管理员指南、`AIX` 技术参考以及编程指南。如果你需要这些扩展文档，你可以仅安装你需要的单个组件。并不需要 CD-ROM 的全部内容。

基础文档 CD-ROM 的安装可能需要相当长的时间，特别是如果你有一台较旧的 Micro Channel 机器，配备低速的 2X CD-ROM 驱动器；在这种情况下，安装可能需要几个小时才能完成。当所有这些文件集安装完成后，你可以进入下一步，配置 Web 服务器。

在配置 Web 服务器之前，你首先需要停止任何 `httpd` 进程：

```bash
# ps -ef | grep httpd
# kill <httpd 进程 ID>
```

接下来，你需要停止服务器上的 `IMNSearch` 进程：

```bash
# ps -ef | grep -i imm
# immss -stop immhelp
```

此外，如果 `/etc/inittab` 文件中包含 `httpdlite` 条目，请确保使用冒号 (`:`) 将其注释掉。

**注意** `/etc/inittab` 文件使用冒号 (`:`) 而不是井号 (`#`) 来作为注释。

现在你可以使用 SMIT 配置 Web 服务器了。首先，输入

```bash
# smitty web_configure
```

然后按照以下步骤操作：

1. 选择 Change Documentation And Search Server。

2. 按 ENTER。

3. 按 F4 选择 Local。

4. 按 ENTER。

5. 按 F4 选择 IBM HTTP Web Server In Default Location。

6. 按 ENTER。

7. 所有字段应自动填充，如下面的示例所示。

```text
**IBM HTTP Server Version 1.3.3.2**
DEFAULT_BROWSER = netscape
DOCUMENTATION_SERVER_MACHINE_NAME = yogi
DOCUMENTATION_SERVER_PORT = 80
CGI_DIRECTORY = /usr/ppc/HTTPServer/share/cgi-bin
DOCUMENT_DIRECTORY = /usr/HTTPServer/share/htdocs
```

```text
**IBM HTTP Server Version 1.3.6.0 and Later**
DEFAULT_BROWSER = netscape
DOCUMENTATION_SERVER_MACHINE_NAME = yogi
DOCUMENTATION_SERVER_PORT = 80
CGI_DIRECTORY = /usr/HTTPServer/cgi-bin
DOCUMENT_DIRECTORY = /usr/HTTPServer/htdocs
```

安装已完成。

## 在 AIX 5L 上安装 DocSearch

默认情况下，`DocSearch` 库搜索服务作为 `BOS` 的一部分安装在 `AIX 5L` 上。这对 IBM 来说是新的；在 `AIX 5L` 之前，我们需要四处寻找所需的文件，而且很容易遗漏一两个文件。如果你从以前的 `AIX` 版本或发行版进行了迁移升级，你在让文档搜索服务再次工作时可能会遇到一些问题。对于这些问题的每一个，我发现花一小时卸载并重新安装所有东西最终是节省时间的。

如果你的系统中尚未定义 `inadm` 用户和组，你需要为文档搜索服务在系统中定义一个新的用户和组。首先，创建一个名为 `inadm` 的组，然后创建一个名为 `inadm` 的新用户。`inadm` 用户的主要组应为 `imnadm` 组。确保语言环境变量设置为正确值，美国英语为 `en_US`。

```bash
# echo $LANG
```

使用以下 SMIT 快速路径更改语言变量：

```bash
# smitty clang
```

如果您想知道在 `AIX 5L 5.1` 版本上应安装什么，`DocSearch` 是使用 `5.1` 介质上找到的以下文件集安装的。

### AIX 5.1 CD-ROM Volume 1

- `bos.docsearch.client.Dt`
- `bos.docsearch.client.com`
- `bos.docsearch.rte`
- `bos.msg.en_US.docsearch.client.Dt`
- `bos.msg.en_US.docsearch.client.com`
- `IMNSearch.bld.DBCS`
- `IMNSearch.bld.SBCS`
- `IMNSearch.msg.en_US.rte.com`
- `IMNSearch.rte.DBCS`
- `IMNSearch.rte.SBCS`
- `IMNSearch.rte.client`
- `IMNSearch.rte.com`
- `IMNSearch.rte.server`
- `bos.man.en_US.cmdds`

> **注**：如果您的系统没有运行 CDE，您可以省略所有 `*.Dt` 文件集以节省空间。

### AIX 5.1 Expansion Pack CD-ROM

- `http_server.base.rte`
- `http_server.base.source`
- `Netscape.communicator.com`
- `Netscape.communicator.us`

### AIX 5.1 Base Documentation CD-ROM

- `bos.html.en_US.cmdd.cmdd1`
- `bos.html.en_US.cmdd.cmdd2`
- `bos.html.en_US.cmdd.cmdd3`
- `bos.html.en_US.cmdd.cmdd4`
- `bos.html.en_US.cmdd.cmdd5`
- `bos.html.en_US.cmdd.cmdd6`
- `bos.html.en_US.files.files_ref`
- `bos.html.en_US.manage_gds.install`
- `bos.html.en_US.manage_gds.manage_bos`
- `bos.html.en_US.manage_gds.manage_commo`
- `bos.html.en_US.manage_gds.printers`
- `bos.html.en_US.prog_gds.prog_bos`
- `bos.html.en_US.prog_gds.prog_commo`
- `bos.html.en_US.techref.base`
- `bos.html.en_US.techref.commo`
- `bos.html.en_US.topenav.navigate`
- `bos.html.en_US.user_gds.user_bos`
- `bos.html.en_US.user_gds.user_commo`
- `damit.html.en_US_damitgd`
- `peragent.html.en_US.usergd`

上述文件集列表包括随 `AIX 5L 5.1` 版本提供的所有可用文档。安装所有这些文件集后，您即可开始配置 Web 服务器。

在配置 Web 服务器之前，您首先需要停止任何 `httpd` 进程：

```bash
# ps -ef | grep httpd
# kill <httpd Process ID>
```

接下来，您需要在服务器上停止 `IMNSearch` 进程：

```bash
# ps -ef | grep -i imm
# imnss -stop imnhel p
```

此外，如果 `/etc/inittab` 文件中存在 `httpdlite` 的条目，请确保使用冒号 (`:`) 将其注释掉。

> **注**：`/etc/inittab` 文件使用冒号 (`:`) 而不是井号 (`#`) 进行注释。

要配置 Web 服务器，请运行以下命令：

```bash
# smitty web_configure
```

1. 选择 Change Documentation and Search Server（更改文档和搜索服务器）。

2. 按 ENTER。

3. 按 F4 选择 Local（本地）。

4. 按 ENTER。

5. 按 F4 选择 IBM HTTP Web Server In Default Location（默认位置的 IBM HTTP Web Server）。

6. 按 ENTER。

所有字段都应自动填充，如下例所示。

### IBM HTTP Web Server Version 1.3.12.2

```bash
DEFAULT_BROWSER = netscape
DOCUMENTATION_SERVER_MACHINE_NAME = yogi
DOCUMENTATION_SERVER_PORT = 80
CGI_DIRECTORY = /usr/HTTPServer/cgi-bin
DOCUMENT_DIRECTORY = /usr/HTTPServer/htdocs
```

作为最后一步，`/etc/inittab` 文件需要有一个条目，以便在系统重启时启动 Web 服务器。要检查 `/etc/inittab` 文件以确保 Web 服务器有条目，请输入以下任一命令：

```bash
# lsitab ih:ishtpd
```

或

```bash
# grep ihshtpd /etc/inittab
```

如果未找到 Web 服务器条目，请插入以下行以在启动时重启服务器：

```bash
# mkitab ihshtpd:2:wait:/usr/HTTPServer/bin/httpd >/dev/console 2>&1 # HTTP Server
```

如果您从 `4.3.3` 迁移到 `5.1.0`，由于产品的 `oslevel` 特定性，您需要遵循此过程才能使 `DocSearch` 正常工作。

安装已完成。

## 使用 DOCSEARCH

`DocSearch` 必须从图形环境（如 X Window System 或 CDE）中执行。访问文档库服务只需将 Web 浏览器指向服务器上的文档目录即可。

在文档服务器上，您可以在 X 环境中输入 `docsearch`，浏览器将打开，并显示列出与文档库服务注册的每本书的可折叠树。对于具有 Web 浏览器的本地用户和远程用户，文档服务器的 URL 应如下所示：

```bash
http://<Server-Hostname>/cgi-bin/ds_form
```

其中 `<Server-Hostname>` 是文档 Web 服务器的主机名或 IP 地址。

如果您没有本地 Web 浏览器，或者您有到远程文档服务器的 telnet 会话，则需要允许远程系统访问您的 X 环境，并将显示导出回您的本地机器：

```bash
# xhost <remote_machine>
```

或

```bash
# xhost +
```

以允许所有机器在本地拥有 X 访问权限。

```bash
# export DISPLAY=<local_hostname_or_IP_address>:0.0
# docsearch &
```

打开的 `DocSearch` 窗口如 `AIX 4.3.3` 的图 2-1 和 `AIX 5L` 的图 2-2 所示。

![](img/82f851021955589d82b22750fb3b1646_39_0.png)

**图 2-1. AIX 4.3.3 DocSearch 主窗口**

![](img/82f851021955589d82b22750fb3b1646_40_0.png)

## Documentation Library

文档库由服务器上所有已注册的文档索引组成。可以搜索库内容，或者在线打开并查看每本单独的书籍。库的所有组件（搜索引擎除外）都是作为基础操作系统的一部分安装的。如果要将系统配置为服务器，则必须手动安装搜索引擎和文档。客户端可以通过 Web 浏览器远程访问文档服务器库。

### 搜索

当您发出 `docsearch` 命令或将 Web 浏览器指向文档服务器时，会看到一个列出可折叠树的浏览器窗口，以及顶部的“Search For”（搜索）字段。顶部还有四个选项卡，分别指向 Books（书籍）、Commands（命令）、Tasks/Topics（任务/主题）和 Other（其他，将显示编程和用户指南）。

要执行搜索，您可以在“Search For”字段中输入感兴趣的关键词并按 ENTER 键。此时，另一个浏览器窗口会打开，显示匹配搜索条件的文章超链接列表。

### 简单搜索

搜索可以是简单的单词或短语匹配，也可以使用 `AND`、`OR` 和 `NOT` 逻辑搜索运算符创建复杂的逻辑搜索。简单搜索如图 2-3 和图 2-4 所示。

简单搜索针对短语或模式有三种选项：

- `PHRASE`，所有单词按顺序
- `ALL of these words`，任意顺序
- `One or MORE of these words`，任意顺序

### 高级搜索

高级搜索使用逻辑运算符 `AND`、`OR` 和 `NOT` 执行，如图 2-5 和图 2-6 所示。

逻辑 `AND` 运算符指定匹配所有单词。逻辑 `OR` 运算符指定匹配任意单词。`NOT` 逻辑运算符指定匹配除 `NOT` 否定的单词以外的所有单词。所有这些逻辑运算符可以混合使用，以实现非常具体的搜索。高级搜索还允许您指定要在单个页面上显示的结果数量。

![](img/82f851021955589d82b22750fb3b1646_41_0.png)

图 2-3. 使用短语进行简单搜索

![](img/82f851021955589d82b22750fb3b1646_42_0.png)

图 2-4. 简单搜索的结果

![](img/82f851021955589d82b22750fb3b1646_42_1.png)

图 2-5. 使用逻辑运算符的高级搜索

![](img/82f851021955589d82b22750fb3b1646_43_0.png)
