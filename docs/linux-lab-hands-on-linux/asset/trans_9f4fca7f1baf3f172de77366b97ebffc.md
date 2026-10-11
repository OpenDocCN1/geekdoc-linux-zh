
## 附录：SELinux 安全策略和上下文

安全增强型 Linux（SELinux）增强功能由美国联邦国家安全局（NSA）开发，自版本 3 的 Fedora Core 和版本 4 的 Red Hat Enterprise Linux 开始包含在内。细粒度访问控制架构在 Linux 内核中得到支持。既支持“类型”强制，也支持基于角色的访问控制（RBAC）。系统进程和文件（包括套接字描述符、IPC、设备）各自被分配一组已知为安全上下文的安全属性。

安全目标：
- 保护系统免受用户侵害
- 保护用户之间互不侵犯
- 保护文件免受脚本/程序侵害

以下 RPM 软件包构成了 SELinux：
- selinux-policy-strict
- selinux-policy-strict-sources：配置文件
- selinux-policy-targeted
- selinux-policy-targeted-sources：配置文件
- libselinux：提供一组接口的库，供具有安全意识的应用程序获取和设置进程和文件的安全上下文。
- selinux-doc

配置文件：`/etc/selinux/config`

```
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#       enforcing - SELinux security policy is enforced.
#       permissive - SELinux prints warnings instead of enforcing.
#       disabled - SELinux is fully disabled.
SELINUX=enforcing
# SELINUXTYPE= type of policy in use. Possible values are:
#       targeted - Only targeted network daemons are protected.
#       strict - Full SELinux protection.
SELINUXTYPE=targeted
```

可以通过设置 `SELINUX=disabled` 来关闭 SELinux 功能。（需要重新启动才能读取新配置。）

直接设置强制执行：
- 强制执行：
    - 使用命令：`setenforce 1`（在内核运行时更改 SELinux 强制执行状态。）
    - 或者
    - `echo 1 > /selinux/enforce`
    - 在 `/etc/grub.conf` 的 "kernel" 命令行中指定：`enforcing=1`（在启动时设置强制执行。）
- 禁用：
    - 使用命令：`setenforce 0`
    - 或者
    - `echo 0 > /selinux/enforce`
    - 或者
    - 在 `/etc/grub.conf` 的 "kernel" 命令行中指定：`selinux=0`

使用命令查看当前设置：`getenforce`

## 安全上下文

- 查看文件/目录上下文：`ls -Z /var/www`
- 设置文件/目录上下文：`chcon -R -h -t httpd_sys_content_t /home/user1/public_html`
    - 选项：
        - `-R`：递归。当前目录及所有子目录中的文件和目录。
        - `-h`：影响符号链接。
        - `-t`：指定安全上下文的类型。
- 查看运行中进程的安全上下文：`ps -eZ`
- 查看用户的安全上下文：`id`

```
uid=500(user1) gid=500(user1) groups=500(user1)
context=user_u:system_r:unconfined_t
```

新文件的安全上下文默认为父目录的安全上下文。

## 附录：YUM 仓库服务器

### 关于 YUM

YUM 或 Yellowdog Updater Modified（修改版 Yellowdog 更新器）是一个交互式自动更新程序，可用于使用 rpm 维护系统。Yum 是 rpm 系统的自动更新器和软件包安装/卸载器。它自动计算依赖关系，并确定安装软件包时应执行哪些操作。Yum 使得维护机器组变得更加容易，无需手动使用 rpm 更新每一台机器。

### 关于仓库

仓库是一组 rpm 列表的集合。它包含有关 rpm 的各种信息，例如其依赖关系等。

### 既然可以使用 rpm 命令安装 RPM，为什么要使用 Yum？

好吧，如果你想要安装 RPM，必须确保其依赖项也已安装。但在 YUM 的情况下并非如此，你可以直接安装软件包及其依赖项。YUM 会处理你所有的安装事务。此外，rpm 安装方式不提供更新功能，但 yum 提供该功能。

### YUM 的关键特性

- 多个仓库
- 简单的配置文件
- 正确的依赖关系计算
- 快速操作
- rpm 一致的行为
- 支持 comps.xml 组，包括多个仓库组
- 简单的接口

### 从 CD/DVD 创建自己的仓库（服务器端配置）

#### 步骤#1：前提条件

- Linux 发行版 CD 或 DVD
- 硬盘上的空闲空间（最少 4.0 GB）

> 所需总空间因发行版而异

#### 步骤#2：将光盘复制到硬盘

首先挂载你的 CD/DVD 并将其复制到硬盘

假设 netmon dvd 已插入你的 Linux 系统，请尝试以下建议步骤：

```bash
[root@netmon ~]#mount /dev/dvd /mnt
[root@netmon ~]#cd /mnt/server
[root@netmon Server]#rpm -ivh vsftpd[tab] ([tab] - means hit tab)
[root@netmon Server]#rpm -ivh createrepo[tab] ([tab] - means hit tab)
```

创建仓库可能需要一些时间，完成后请检查 'vsftpd' 服务是否正在运行？如果没有

```bash
[root@netmon Server]#service vsftpd restart
```

使用以下命令确保 vsftpd 服务在启动时开启

```bash
[root@netmon Server]#chkconfig --level 35 vsftpd on
```

要检查 vsftpd 在各种运行级别下的状态，可以尝试此方法

```bash
[root@netmon Server]#chkconfig --list vsftpd
```

> 你会注意到，在成功安装 `vsftpd` 服务后，你的 Linux 系统上会出现 `/var/ftp/pub/` 目录。

```bash
[root@netmon Server]#cp -avr /mnt/* /var/ftp/pub
[root@netmon Server]#pwd
/mnt/server
[root@netmon Server]#cd /var/ftp/pub/Server
[root@netmon Server]#pwd
/var/ftp/pub/Server
```

> 如果你想在你的网络中通过 http 上传安装仓库，应在各自的默认目录 /var/www/html 中为 http 服务器操作。

#### 步骤#3：安装 CreateRepo 软件包

现在进入你复制文件的目录，并查找 createrepo-*.rpm 文件。* 可能因版本和系统架构而异。使用 rpm 命令安装该 rpm，如下所示：

```bash
[root@netmon ]#rpm -ivh --aid createrepo-*.rpm
```

#### 步骤 #4：运行 createrepo

进入你复制文件的目录并运行 createrepo 命令

```bash
[root@netmon Server]#cp repodata/comp*[tab] /tmp
```

```bash
[root@netmon Server]#createrepo -g /tmp/comp[tab] /var/ftp/pub/Server
```

一旦在 /var/ftp/pub/Server 中创建仓库，它会提示你删除现有的 `.oldata`。

```bash
[root@netmon Server]#rm -rf .oldata
```

删除 `.oldata` 后，你必须再次创建仓库

```bash
[root@netmon Server]#createrepo -g /tmp/comp[tab] /var/ftp/pub/Server
```

这需要一些时间，你的仓库将被创建。/var/ftp/pub 还有一个用于 'VT' 的条目，因此也请复制该仓库。

```bash
[root@netmon Server]#cd /var/ftp/pub/VT
[root@netmon VT]# cp repodata/comp[tab] /var/ftp/pub/VT
```

现在，为了让 yum install 正常工作，你必须在目录 `/etc/yum.repos.d/` 中创建 `.repo` 文件。进入此目录，如有必要，将现有的 `.repo` 文件移除/备份到另一个目录

```bash
[root@netmon VT]# cd /etc/yum.repos.d/
```

创建你自己的 '.repo' 文件，类似于

```bash
[root@netmon yum.repos.d]# vi server.repo
```

```ini
[Server]
name=Server
baseurl=http://172.16.100.1/pub/Server (Ip address choice is left to you)
gpgcheck=0
[VT]
name=VT
baseurl=http://172.16.100.1/pub/VT
gpgcheck=0
```

现在检查你的系统上 'wget' 是否正常工作？

```bash
[root@netmon yum.repos.d]#wget ftp://172.16.100.1/pub/Server/createrepo*
```

如果 'wget' 失败，可能性是 vsftpd 服务已停止，或者你需要如下关闭防火墙

```bash
[root@netmon ~]# man ftpd_selinux
```

并在此 ftpd_selinux 文件中搜索 'restart'，即 /restart，并执行这两个命令

```bash
[root@netmon ~]#setsebool -P ftpd_disable_trans 1
[root@netmon ~]#service vsftpd restart
[root@netmon yum.repos.d]#rpm -ivh create*
[root@netmon yum.repos.d]#yum clean all
[root@netmon yum.repos.d]#yum list all
```

