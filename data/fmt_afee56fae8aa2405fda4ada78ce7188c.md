
# `rpm -Uvh kernel-util-2.4.22-2061.npt1.i386.rpm`

如果您使用 PCMCIA（例如在笔记本电脑上），您还需要安装 `kernel-pcmmia` 包并保留旧版本。如果您使用 `-i` 参数，安装过程可能会返回冲突，因为旧内核需要此包才能支持 PCMCIA 启动。为了绕过这一点，请使用 `--force` 参数，如下例所示：

```
# rpm -ivh --force kernel-pcmcmia-cs-3.1.13-13.i386.rpm
```

如果您使用 ext3 文件系统或 SCSI 控制器，则需要初始内存磁盘（initial RAM disk）。初始内存磁盘的目的是允许模块化内核在内核访问模块通常所在的设备设备之前，能够访问启动所需的模块。

## 578 第四部分：系统维护

初始 RAM 磁盘是通过 `mkinitrd` 命令创建的。然而，Hat 内核 RPM 包已为你执行了这一步。要验证它是否已创建，请使用命令 `ls -l /boot`。你应该能看到文件 `initrd-2.4.22-1.2061-npl1.img`（该版本应与你刚刚安装的内核版本匹配）。

现在你已经安装了新内核，需要配置引导加载程序以启动新内核。请参阅本章末尾的“配置引导加载程序”部分来配置引导程序。

## 从网上安装内核源码

我们优过的升级和自定义内核的方法是使用从互联网各处内核归档站点分发的原始源码进行工作。为什么呢？包括 Red Hat 在内，每个 Linux 发行版都会对内核源码应用补丁，以这些补丁以支持其战略合作伙伴的硬件。这种做法并没有错，因为 Linux 是开源软件，但它确实产生了一个遗憾的副作用，导致 Red Hat 分发的源代码与内核维护者的版本产生分歧。结果就是应用补丁变成了一件碰运气的事（请参见“补丁内核”部分，了解如何以及为什么要使用内核补丁升级源码）。

内核源码的主要站点是 http://www.kernel.org/（见图 24-1）。

![](img/8c5ce181a0f26bec693ad7f04bbfb6fe_611_0.png)

图 24-1：Linux 内核归档首页

## 第 24 章：升级和自定义内核

然而，由于内核负载很大，特别是在新版本发布后，你最好使用我世界各地的许多镜像之一。通常情况下，你可以找到一个适合你的镜像——大多数国家至少有一个镜像，有些国家（如美国和英国）则有很多。事实上，图 24-2 描述的 Linux 内核镜像系统目前包含来自 51 个国家或地区的 138 个站点。另外 74 个国家或地区由位于其他国家的下载站点支持。要找到离你最近镜像，请将你的 Web 浏览器指向 http://www.kernel.org/mirrors/，按字母顺序查看国家列表，并点击你的国家名称以查看所在国家的镜像站点列表。图 24-2 显示了美国 HTTP 镜像站点列表的部分：

![](img/8c5ce181a0f26bec693ad7f04bbfb6fe_612_0.png)

| 名称 | 位置 | 格式 | 链接 |
| :--- | :--- | :--- | :--- |
| Virginia Tech/Technologies | US | 4 | gzip only | download@kernel.org |
| Lynn College Computer Science FTP Server | US | 1.5 | gzip, bzip2 | download@kernel.org |
| InterNAP Network Services | US | 100 | gzip, bzip2 | download@kernel.org |
| pairNetworks, Inc. | US | 1700 | gzip | download@kernel.org |
| NATO Network Services | US | 450 | gzip only | download@kernel.org |
| Semahurst Corporation | US | 300 | gzip only | download@kernel.org |
| HIETS | US | 490 | gzip | download@kernel.org |
| Measurement Communications Mirror Server | US | 622 | gzip | download@kernel.org |
| MIT Communications Materials Modeling Group | US | 1.5 | bzip2 only | download@kernel.org |
| UMass | US | 155 | bzip2 only | download@kernel.org |
| University of Wisconsin - Madison | US | 622 | gzip | download@kernel.org |
| MIT Lab for Computer Science | US | 100 | gzip | download@kernel.org |
| University of Wisconsin Systems Lab | US | 622 | gzip | download@kernel.org |
| University of North Carolina's Metal Lab | US | 45 | gzip only | download@kernel.org |
| Young Moors Burs | US | 100 | bzip2 only | download@kernel.org |
| Jfriere | US | 2048 | gzip | download@kernel.org |
| Telgege | US | 100 | gzip | download@kernel.org |
| Purdue University Computer Society | US | 496 | gzip | download@kernel.org |
| Oregon State University | US | 50 | gzip only | download@kernel.org |

图 24-2：美国的 Linux 内核镜像站点

内核归档镜像系统的设置方式是，对于每个双字母的国家代码，你只需使用主机名 http://www.kernel.org/ 或 ftp.kernel.org 来访问支持该特定国家的镜像。例如，在美国，你将在 Web 浏览器中使用 URL http://www.us.kernel.org/。每个镜像都有 `/pub/linux`（内核源码顶层目录）的完整归档，但可能不会同时提供 gzip 和 bzip2 压缩格式的源码——bzip2 格式的下载时间比 gzip 格式短，但解压时间比 gzip 格式长。

在网络术语中，找到离你最近的归档后，下载所需的文件。随后的指令假设你在终端窗口（如 `xterm`）中使用标准的 FTP 客户端。

## 580 第四部分：系统维护

- 1. 切换目录到你具有写入权限的目录，例如，你的家目录：

```
$ cd ~
```

- 2. 与你选择的归档站点建立 FTP 会话，并使用你的电子邮件地址作为密码以匿名用户身份登录：

```
$ ftp ftp.us.kernel.org

Connected to ftp.us.kernel.org.

220 mirror.services.wisc.edu FTP server ready.

User (ftp.kernel.org:(none)): ftp

331 Anonymous login ok, send your complete email address as your password.

Password:

230 Anonymous access granted, restrictions apply.

ftp>
```

- 3. 切换目录到内核源码目录。该目录的确切位置随镜像而异，因此你可能需要使用 `ls` 命令来定位：

```
ftp> cd /pub/linux/kernel
```

- 4. 切换目录到 v2.4 目录：

```
ftp> v2.4
```

- 5. 执行以下命令以查看 2.4 内核系列的完整源码树列表（列表为了节省空间而进行了截断）：

```
ftp> ls linux-2.4.*
```

```
-rw-r--r-- 1 kernel kernel 22192379 Aug 11 04:13 linux-2.4.8.tar.bz2
-rw-r--r-- 1 kernel kernel 248 Aug 11 04:13 linux-2.4.8.tar.bz2.sign
-rw-r--r-- 1 kernel kernel 27042470 Aug 11 04:13 linux-2.4.8.tar.gz
-rw-r--r-- 1 kernel kernel 248 Aug 11 04:13 linux-2.4.8.tar.gz.sign
```
