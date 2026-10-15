
![](img/f332344337ca8bf6846cb313a66ee0b3_287_0.png)

**注意：** 对于生产服务器，我们强烈建议使用手动磁盘分区选项。

### 3. 网络配置
配置主机名、网关和 DNS。如果有多块网卡，每个设备都有自己的配置屏幕。参见图 9-2。

![](img/f332344337ca8bf6846cb313a66ee0b3_288_0.png)

图 9-2 配置网络

### 4. 防火墙配置
此时，我们可以决定阻止对计算机的访问。我们可以选择“无防火墙”或“启用防火墙”选项。如果勾选了“启用防火墙”，我们可以允许访问某些服务，例如远程登录（SSH）、文件传输（FTP）、邮件服务器（SMTP）和 Web 服务器（HTTP/HTTps）。参见图 9-3。

![](img/f332344337ca8bf6846cb313a66ee0b3_289_0.png)

**注意：** 如果您愿意，可以在系统安装后启用/禁用这些服务。

### 5. 
在后续屏幕中，我们可以选择支持的语言，设置时区和 root 密码，并选择要安装的包。

![](img/f332344337ca8bf6846cb313a66ee0b3_290_0.png)

此后，Linux 将安装完毕并可以使用。

**注意：** 有关在 S/390 架构上详细安装 Linux 的更多信息，可以在 *IBM z/VM and Linux on IBM System z: Virtualization Cookbook for Red Hat Enterprise Linux 4, SG24-7272* 以及以下地址找到：`http://www.ibm.com/ linux`

#### 9.2 收集有关安装过程的信息

**注意：** 本章基于 Red Hat Enterprise Linux 版本 5 编写。当同一主题在 SUSE Linux Enterprise Server 版本 10 中具有不同的文件名或位置时，我们会包含注释。

##### 收集安装期间提供的信息

在安装过程中，所有信息都保存在 `/root/install.log` 文件中，但一旦重启系统，我们就无法访问此文件。在此文件中，我们会遇到关于根据安装选择安装了哪些包及版本的信息。参见示例 9-1。

示例 9-1 `/root/install.log` 的部分内容

```
Installing eel2-devel - 2.16.1-1.el5.s390x

Installing bug-buddy - 1:2.16.0-2.el5.s390x

Installing setroubleshoot - 1.8.11-4.el5.noarch

Installing evolution-data-server-devel - 1.8.0-15.el5.s390

Installing devhelp - 0.12.9-el5.s390

Installing gnome-desktop-devel - 2.16.0-1.fc6.s390

Installing gnome-python2-bonobo - 2.16.0-1.fc6.s390x

Installing sabayon - 2.12.4-3.el5.s390x

Installing eel2-devel - 2.16.1-1.el5.s390

Installing krb5-auth-dialog - 0.7-l.s390x

Installing gtkhtml3 - 3.12.0-1.fc6.s390x

Installing orca - 1.0.0-5.el5.s390x

Installing gnome-python2-gnomevfs - 2.16.0-1.fc6.s390x

Installing gnome-terminal - 2.16.0-3.el5.s390x

Installing libgnome-devel - 2.16.0-6.el5.s390

Installing system-config-date - 1.8.12-1.el5.noarch

Installing nautilus - 2.16.2-6.el5.s390x

Installing alacarte - 0.10.0-1.fc6.noarch

Installing yelp - 2.16.0-13.el5.s390x

Installing eog - 2.16.0.1-6.el5.s390x

Installing gnome-applets - 1:2.16.0-1-19.el5.s390x

Installing ImageMagick - 6.2.8.0-3.el5.4.s390

Installing gnome-system-monitor - 2.16.0-3.el5.s390x

Installing im-chooser - 0.3.3-6.el5.s390x

Installing nautilus-cd-burner - 2.16.0-7.el5.s390x

Installing evince - 0.6.0-8.el5.s390x

Installing nautilus-cd-burner - 2.16.0-7.el5.s390

Installing pirut - 1.2.10-1.el5.noarch

Installing file-roller - 2.16.0-2.fc6.s390x

Installing dogtail - 0.6.1-2.el5.noarch

Installing gnome-power-manager - 2.16.0-7.el5.s390x

Installing gnome-utils - 1:2.16.0-3.el5.s390

Installing gnome-session - 2.16.0-6.el5.s390x
```

###### 收集安装后提供的信息

安装完成后，大多数日志文件位于 `/var/log` 目录中。在此目录下，我们可以找到系统和应用程序的默认日志。应用程序日志的一个示例向我们展示了 `gdm` 和 `cup` 目录，它们分别包含 Gnome Display Manager（Gnome 显示管理器）和 Common UNIX® Printing System（通用 UNIX® 打印系统）的日志。在图 9-5 中，我们可以确认 `/var/log` 目录中还有更多可用的日志。

![](img/f332344337ca8bf6846cb313a66ee0b3_292_0.png)

*图 9-5 /var/log 目录的内容*

关于收集信息，守护进程 `syslogd` 和文件 `syslog.conf` 是理解哪些内容会被打印到 `/var/log/` 文件中的关键。

`Syslogd` 是一个守护进程，它读取消息并将其记录到系统控制台或日志文件中。`syslog.conf` 是该守护进程的配置文件。在 `syslog.conf` 中，我们可以配置要记录什么类型的信息以及这些信息将存储在哪里。

示例 9-2 展示了一个 `syslog.conf` 文件。请注意，所有关于 notice、kern debug 等信息都将被记录在 `/var/log/messages` 中。

*示例 9-2 syslog.conf*
