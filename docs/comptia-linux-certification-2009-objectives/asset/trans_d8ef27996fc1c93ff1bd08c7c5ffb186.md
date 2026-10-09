

## 活动 12-5：配置匿名 vsftpd 服务器

**开始之前：**
- 在 **srvA** 上，你已在 CLI 中以 *root* 身份登录。
- 在命令行中，将目录更改为根目录。
- 输入 `clear` 以清除终端屏幕。

**场景：**
你是一家软件开发公司的网络管理员，该公司在多个国家设有分支机构。各地团队经常通过电子邮件交换大文件。然而，使用电子邮件共享大文件会影响邮件服务器的性能。因此，你希望在服务器上创建一个公共目录，以便用户上传和下载文件。

| **你所做的操作** | **操作方法** |
|:---|:---|
| 1. 安装 FTP。 | a. 在标记为 **srvA** 的服务器上，导航到 */rhelsource/Server* 目录。<br> b. 输入 `rpm -ivh vsftpd-2.0.5-12.el5.i386.rpm` 以安装 *vsftpd* 包。<br> c. 输入 `rpm -qi vsftpd` 以显示已安装的 FTP 版本的信息。<br> d. 清除终端屏幕。 |
| 2. 配置 FTP 以允许匿名访问。 | a. 使用 vi 编辑器打开 /etc/vsftpd/vsftpd.conf 文件。<br> b. 找到内容为 "write_enable=YES" 的行，并验证其未被注释。<br> c. 找到内容为 "#anon_upload_enable=YES" 的行，并取消注释。<br> d. 找到内容为 "#anon_mkdir_write_enable=YES" 的行，并取消注释。<br> e. 保存并关闭该文件。<br> f. 清除终端屏幕。<br> g. 在 /var/ftp 目录中，创建一个名为 upload 的目录，并授予所有用户完全访问权限。<br> h. 启动 vsftpd 服务。<br> i. 输入 `chkconfig vsftpd on` 以便在系统启动时自动启动 vsftpd 服务。<br> j. 清除终端屏幕。 |
| 3. 从网络中的另一台系统访问 FTP 服务器。 | a. 在标记为 srvB 的系统上，确保你处于根目录。输入 `ftp 192.168.0.2` 以连接到 FTP 服务器。<br> b. 以匿名身份登录，无需提供密码。<br> c. 导航到 upload 目录。<br> d. 输入 `put /root/install.log myfile` 以上传 install.log 文件。<br> e. 观察文件是否成功上传。<br> f. 输入 `bye` 以退出 FTP。<br> g. 清除终端屏幕。 |

## 活动 12-6：使用 NFS 导出文件系统

**开始之前：**
- 切换到 srvA。
- 在 srvA 上，你已在 CLI 中以 root 身份登录。
- 显示了第一个终端。
- 输入 `cd /root` 以更改为根目录。
- 输入 `clear` 以清除终端屏幕。

**场景：**
你将要在一些新系统上安装软件应用程序。你创建了一个包含软件的 /rhelsource 目录。你希望将此目录与 192.168.0.0 网络共享，并赋予读或写权限，以便于访问。

| 你所做的操作 | 操作方法 |
| :--- | :--- |
| **1.** 导出 /rhelsource 目录。 | a. 输入 `vi /etc/exports`<br> b. 按 `i` 切换到插入模式。<br> c. 输入 `/rhelsource 192.168.0.* (rw)` 以将 /rhelsource 目录导出到 192.168.0.0 网络。<br> d. 按 `Esc`。<br> e. 保存并关闭该文件。<br> f. 输入 `clear` 以清除终端屏幕。 |
| **2.** 激活 nfs 服务。 | a. 输入 `service nfs start` 以启动 nfs 服务。<br> b. 输入 `exportfs -r` 以激活导出的文件系统。<br> c. 输入 `showmount -e` 以查看导出列表。<br> d. 观察导出的 /rhelsource 目录是否列出。<br> e. 输入 `clear` 以清除终端屏幕。 |

## 活动 12-7：使用 Samba 共享文件系统

**开始之前：**
- 在 srvA 上，你已在 CLI 中以 root 身份登录。
- 显示了第一个终端。
- 输入 `service smb start` 以启动 Samba 服务。
- 输入 `chkconfig smb on` 以自动启动 Samba 服务。
- 输入 `cd /rhelsource/Server` 以更改为 Server 目录。
- 输入 `rpm -ivh system-config-samba-1.2.41-3.el5.noarch.rpm` 以安装 system-config-samba 包。
- 输入 `clear` 以清除终端屏幕。
- 切换到 GUI。以 root 身份登录并显示终端窗口。

**场景：**
你通过 NFS 共享了一个包含所有软件程序的公共目录 /rhelsource。公司中一些使用 Windows 作为操作系统的网络用户发现他们无法访问该公共目录。这些 Windows 用户属于一个名为“mygroup”的工作组。

| 你所做的操作 | 操作方法 |
|:---|:---|
| 1. 指定工作组。 | a. 输入 `system-config-samba` 以修改 samba 配置。<br> b. 在 Samba 服务器配置窗口中，选择 **Preferences→Server Settings**。<br> c. 在 Server Settings 对话框中，在 Workgroup 文本框中，验证工作组名称是否设置为 mygroup。<br> d. 在 Description 文本框中，三击并输入 swprograms。 |
| 2. 指定认证模式。 | a. 选择 Security 选项卡。<br> b. 从 Authentication Mode 下拉列表中，选择 Share 并点击 OK。 |
| 3. 共享 `/rhel/source` 目录。 | a. 选择 **File→Add Share** 以显示 **Create Samba Share** 对话框。<br> b. 在 **Directory** 文本框中，输入 `/rhel/source`。<br> c. 在 **Description** 文本框中，点击并输入 `software programs`。<br> d. 勾选 **Writable** 和 **Visible** 复选框以指定权限级别。 |
| 4. 设置 `/rhel/source` 目录的权限。 | a. 选择 **Access** 选项卡。<br> b. 选择 **Allow access to everyone** 并点击 **OK**。<br> c. 选择 **File→Quit**。<br> d. 输入 `chkconfig smb on` 以便在重启时启动 Samba 服务器。<br> e. 输入 `reboot` 以重启服务器。 |
| 5. 验证用户能否从 Windows 工作站访问 `/rhel/source` 目录。 | a. 重启 `srvB` 并启动 Windows OS。<br> b. 登录到系统。<br> c. 关闭 **Welcome Center** 窗口。<br> d. 选择 **Start→Network**。<br> e. 在 **Network** 窗口中，在地址栏中输入 `//srvA/`。<br> f. 双击 **rhel/source** 文件夹以查看内容。<br> g. 关闭 **rhel/source on srvA** 窗口。 |

# 主题 F

## 配置 NIS

现在，既然你能够配置网络上的跨平台文件共享，你可以开始执行域管理服务了。在本主题中，你将配置网络信息（NIS）。

拥有全球业务组织的必然在世界主要城市设有分支机构。在这种情况下，必须在各办公室的员工之间共享信息。将登录和联系信息存储在集中式系统中，使用户无论身处何地都能访问。网络信息服务（NIS）允许你集中存储用户信息，以便在企业范围内提供服务认证。此外，你可以配置 NIS 在网络上的所有用户中存储组账户信息的数据库。

### 网络信息服务

**定义：**

*网络信息服务（NIS）* 是一种管理网络中所有系统和用户信息的网络服务。它是一个集中式信息管理系统，使网络用户能够维护数据完整性。它允许在整个网络中分发一致的数据。NIS 从数据库向所有主机分发信息，以维护网络中各系统间配置信息的一致性。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_590_0.png)

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_590_1.png)

*图 12-52：* NIS 在网络上管理信息。

### NIS 组件

NIS 由四个主要组件组成。

| 组件 | 描述 |
| :--- | :--- |
| 映射（Maps） | NIS 将用户名、密码和组名等信息存储在数据库文件中；称为 NIS 映射。每个映射由一对文件组成。映射由键值对组成，并存储在数据库管理库格式中。通过在 /var/yp 目录中运行 `make` 可以创建 NIS 映射。 |
| NIS 域 | NIS 域是一组共享相同映射集的主机。域内的主机共享密码、主机和文件信息。映射存储在 /var/yp 目录中具有与域相同名称的子目录中。默认情况下，NIS 域名在 /etc/sysconfig/network 文件中指定。每个域包含单个主 NIS 服务器。客户端只能属于一个域。 |
| NIS 主服务器 | NIS 将在主服务器中存储包含网络信息的数据库。主服务器还包含各种映射的源文件。应在服务器上运行 ypserv 进程以管理 NIS 服务器。主服务器的配置设置存储在 /etc/NIS 目录中的 ypserv.conf 文件中指定。 |
| NIS 从服务器 | NIS 从服务器是平衡主服务器负载的次要服务器。从服务器包含数据库和源文件的副本。对映射或数据库进行的任何更新都会由主服务器使用 yppush 命令更新到从服务器。当主服务器宕机时，从服务器将充当主服务器并解决客户端发送的查询。从服务器的信息在 /var/yp/ypservers 文件中指定。 |

### NIS 映射

NIS 支持许多标准映射。

| 文件 | 映射 | 描述 |
| :--- | :--- | :--- |
| /etc/hosts | hosts.byname, hosts.byaddr | 将 IP 地址映射到相应的主机名。 |
| /etc/networks | networks.byname, networks.byaddr | 将 IP 网络地址映射到网络名称。 |

