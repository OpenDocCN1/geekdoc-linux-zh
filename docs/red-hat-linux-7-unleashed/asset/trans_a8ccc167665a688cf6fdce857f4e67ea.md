

# Apache 服务器

## 本章内容

- 服务器安装 355
- 运行时服务器配置设置 359
- 身份验证和访问控制 366
- Apache 模块 370
- 虚拟主机 378
- 日志记录 381
- 动态内容 382
- 启动和停止服务器 389
- 配置文件清单 393

# 第 12 章

## 配置服务

### 第二部分

本章涵盖了 Apache Web 服务器的安装、配置和管理。

根据 NetCraft 对网站的研究，Apache 是当今互联网上应用最广泛的 Web 服务器。在软件早期开发阶段，“Apache”这个名字出现是因为它是一个“拼凑的”（patchy）服务器，由针对免费提供的 NCSA HTTPd Web 服务器源代码的各种补丁构成。在 NCSA HTTPd 项目终止后的一段时间内，许多人编写了各种各样的补丁来修复代码中的错误或添加他们想要的功能。当时有大量的此类代码流传，人们可以自由分享，但完全缺乏管理。一段时间后，Bob Beheendorf 和 Cliff Skolnick 建立了这些补丁的中心化存储库，Apache 项目由此诞生。该项目仍由一小群核心程序员组成，但欢迎任何人向该小组提交补丁，以便可能被纳入代码中。

在过去几年中，人们对 Apache 项目的兴趣激增，部分原因是开源领域的新兴趣推动。这部分也归功于 IBM 承诺支持并使用 Apache 作为其 Web 产品的基础。他们投入了大量资源，因为使用一个成熟的、经过验证的 Web 服务器比试图自己编写一个更有意义。这种关注的结果是出现了适用于 Windows NT 操作系统的稳定版本以及加快的发布计划。

1999 年年中，Apache 软件基金会成立为一个非营利公司。一个由 ASF 成员每年选举产生的董事会监督该公司。这家公司为几个不同的开源软件开发项目提供了基础——包括 Apache Web 服务器项目。

了解 Apache 的最佳途径是 Apache 小组的网站 [http://www.apache.org/](http://www.apache.org/) 和 Apache 周刊网站 [http://www.apacheweek.com/](http://www.apacheweek.com/)，在那里你可以订阅通过电子邮件接收 Apache 周刊，以跟上项目最新进展。

**提示**

除了广泛的在线文档外，你还可以在 Apache 服务器的 HTML 目录中找到完整的 Apache 文档。你可以使用系统上包含的一个 Web 浏览器访问你的新 Red Hat 系统上的 `http://localhost/manual/` 来查看这些文档。如果你在这个位置找不到 Apache 的文档，你可能需要自己安装。安装方法如下（版本号可能会有所不同）：

```bash
rpm -Uvh apache-manual-1.3.12-25.1386.rpm
```

Red Hat 附带尽可能最新版本的 Apache，但由于 Apache 快速的发布计划，它很快就会变得过时。你可以在 Red Hat FTP 服务器的 `pub/redhat/current` 区域获取作为 RPM（Red Hat 软件包管理器）安装文件的 Apache，或者你可以从 Apache 网站获取源代码，并本着 Linux 的传统，自行构建。

本章涵盖随 Red Hat 7 发布的版本 1.3.12。

### 服务器安装

你可以从 RPM 安装 Apache，或者自己构建源代码。Apache 源代码几乎可以在任何类 UNIX 操作系统上构建，也可以在 Win32 上构建。

如果你准备安装新版本的 Apache，最好先关闭旧服务器。即使旧服务器不太可能干扰安装过程，关闭它也能确保不会出现问题。如果你不知道如何停止 Apache，请查看本章稍后部分的“启动和停止服务器”章节。

#### 从 RPM 安装

你可以在 Red Hat Linux 安装介质、Red Hat FTP 服务器或其众多镜像站点之一找到 Apache RPM。你应尽可能频繁地检查 `updates.redhat.com` FTP 站点（或其中一个镜像）。在对应于你的 Red Hat 版本的目录中，你时不时会找到 Apache 的更新。这些可能是修复错误或使用安全漏洞的重要更新。当更新版本发布时，为了安全起见，你希望尽快安装它。

**注意**

如果你想要尽可能最新的版本，你可能需要查看 Red Hat 的 Rawhide 发行版，它也可以在他们的 FTP 服务器上获取。此发行版是*实验性的*，并且始终包含所有 RPM 的最新版本。但是，请注意，Apache 包可能依赖于 Rawhide 发行版中其他 RPM 中可用的新功能。因此，你可能需要安装许多新的 RPM 才能使用 Rawhide 中的包。如果你想使用来自 Rawhide 发行版的 Apache 版本，更好的选择可能是下载源代码 RPM（即 SRPM）并自行编译——这样可以避免对其他新包的依赖。

**警告**

你应该警惕安装实验性软件包，特别是在用于“实际生活”的服务器上。务必提前仔细测试软件包！

获取 Apache RPM 后，你可以通过输入以下内容使用命令行 rpm 工具进行安装：

```bash
rpm -Uvh latest_apache.rpm
```

其中 *latest_apache.rpm* 是最新 Apache RPM 的名称。

有关使用 RPM 安装包的信息，请参见第 21 章“Linux 系统管理”。

Apache RPM 在以下目录中安装文件：

- `/etc/httpd/conf`—此目录包含所有 Apache 配置文件，其中包括 *access.conf*、*httpd.conf* 和 *srm.conf*。参见本章稍后关于配置文件的章节。
- `/etc/rc.d/`—此目录下的树状结构包含系统启动脚本。Apache RPM 为 Web 服务器安装了一套完整的脚本。这些脚本可用于从命令行启动和停止服务器，并且当计算机停止、启动或重启时，也会自动启动和停止服务器。有关这些启动脚本的信息，请参见第 9 章“系统启动和关闭”。
- `/var/www`—RPM 在此位置安装默认的服务器图标、CGI 程序和 HTML 文件。如果你想将 Web 内容保存在其他位置，可以通过对服务器配置文件进行适当的更改来实现。
- `/var/www/html/manual/`—如果你安装了 Apache 手册 RPM，你会在这里找到一份 HTML 格式的 Apache 文档副本。你可以通过访问 `http://localhost/manual/` 使用 Web 浏览器访问它。
- `/usr/share/man`—RPM 包含手册页，它们被放置在此目录中。
- `/usr/sbin/`—可执行程序放置在此目录中。这包括服务器可执行文件本身以及各种实用工具。
- `/usr/bin/`—Apache 包中的某些实用程序放置在这里——例如，*htpasswd* 程序，用于生成身份验证密码文件。
- `/var/log/http`—服务器日志文件放置在此目录中。默认情况下，有两个日志文件——access_log 和 error_log——但你可以定义任何数量的自定义日志，其中包含各种信息。参见本章稍后关于日志记录的章节。
- `/usr/src/redhat/SOURCES/`—此目录包含一个 tar 归档文件，其中包含 Apache 的源代码，在某些情况下还包括源代码补丁。必须安装 Apache SRPM 才能创建这些文件。

当 Apache 运行时，它还会在以下目录中创建文件：

- `/var/run/lock`—启动脚本添加一个名为 httpd 的锁文件。
- `/var/run`—Apache 将创建一个包含 Apache 父进程 ID 的文件，名为 httpd.pid。

**注意**

如果你正在升级到 Apache 的新版本，RPM 不会覆盖当前的配置文件。RPM 会将当前文件移动并附加扩展名 .rpmnew。例如，srm.conf 变为 srm.conf.rpmnew。

### 自行构建源代码

获取 Apache 源代码有几种方法。Red Hat 发行版包含含有 Apache 源代码的 SRPM，有时还包括使其与 Red Hat 发行版更好工作的补丁。最新版本可在 ftp://updates.redhat.com 上找到。当你安装这些 SRPM 之一时，一个包含 Apache 源代码的 tar 归档文件将在 /usr/src/redhat/SOURCES/ 中创建。你也可以直接从 http://www.apache.org/ 下载源代码。一旦有了 tar 文件，你需要在一个合适的临时目录（如 /tmp）中解包它。这将创建一个名为 apache_version_number 的目录，其中 version_number 是你下载的版本（例如，apache_1.3.12）。有两种编译源代码的方法——旧的、熟悉的方法（至少对于使用 Apache 多年的我们来说）和新的、简单的方法。

#### 简单方法

要简单地构建 Apache，只需在刚创建的目录中运行 .configure。你可以提供 --prefix 参数以安装到默认目录（/usr/local/apache/）之外的目录。

```bash
.configure --prefix=/preferred/directory/
```

