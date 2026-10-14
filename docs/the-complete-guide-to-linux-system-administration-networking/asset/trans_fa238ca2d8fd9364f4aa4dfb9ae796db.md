

## Topic 113 Networking Services

## 1.113.1 Configure and Manage inetd, xinetd, and Related Services

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
| 4 | 考生应能够配置通过 inetd 可用的服务，使用 tcpwrappers 按主机逐一允许或拒绝服务，手动启动、停止和重启 Internet 服务，并配置包括 Telnet 和 FTP 在内的基本网络服务。在 inetd.conf 中将服务设置为以其他用户而非默认用户运行。关键文件、术语和实用程序包括：/etc/inetd.conf、/etc/hosts.allow、/etc/hosts.deny、/etc/services、/etc/xinetd.conf、/etc/xinetd.log。 | Chapter 15, "Using Network Services". |

## 1.113.2 Operate and Perform Basic Configuration of sendmail

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
| 4 | 考生应能够修改 sendmail 配置文件中的简单参数（包括必要时“智能主机”参数），创建邮件别名，管理邮件队列，启动和停止 sendmail，配置邮件转发，并对 sendmail 进行基本故障排除。本目标包括检查并关闭邮件服务器上的开放中继。它不包括 sendmail 的高级自定义配置。关键文件、术语和实用程序包括：/etc/sendmail.cf、/etc/aliases 或 /etc/mail/aliases、/etc/mail/*、~/.forward、mailq、sendmail、newaliases。 | Chapter 15, "Using Network Services". |

## 1.113.3 Operate and Perform Basic Configuration of Apache

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
| 4 | 考生应能够修改 Apache 配置文件中的简单参数，启动、停止和重启 httpd，并在启动时安排 httpd 自动重启。不包括 Apache 的高级自定义配置。关键文件、术语和实用程序包括：apachectl、httpd、httpd.conf。 | Chapter 15, "Using Network Services" |

## 1.113.4 Properly Manage the NFS, smb, and nmb Daemons

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 4 | 考生应知道如何使用 NFS 挂载远程文件系统，配置 NFS 以导出本地文件系统，启动、停止和重启 NFS 服务器。使用包含的 GUI 工具或直接编辑 /etc/smb.conf 文件安装和配置 Samba（注意：这特意排除了高级 NT 域问题，但包括简单地共享主目录和打印机，以及正确将 nmbd 设置为 WINS 客户端。关键文件、术语和实用程序包括：/etc/exports、/etc/fstab、/etc/smb.conf、mount、umount。 | Chapter 15, "Using Network Services" |

## 1.113.5 Set up and Configure Basic DNS Services

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 4 | 考生应能够配置主机名查找并排查仅缓存本地名称服务器的问题的问题。需要理解域名注册和 DNS 翻译过程。需要理解 bind 4 和 bind 8 配置文件的关键差异。关键文件、术语和实用程序包括：/etc/hosts、/etc/resolv.conf、/etc/nsswitch.conf、/etc/named.boot (v.4) 或 /etc/named.conf (v.8)、named。 | Chapter 12, "Configuring Linux Networking" |
|  |  | Chapter 15, "Using Network Services" |

## 1.113.7 Set up Secure Shell (OpenSSH)

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 4 | 考生应能够获取并配置 OpenSSH。本目标包括基本的 OpenSSH 安装和故障排除，以及配置 sshd 在系统启动时启动。关键文件、术语和实用程序包括：/etc/hosts.allow、/etc/hosts.deny、/etc/nologin、/etc/ssh/sshd_config、/etc/ssh/known_hosts、/etc/sshrc、sshd、ssh-keygen。 | Chapter 7, "Remote Login" |
|  |  | Chapter 15, "Using Network Services" |

## Topic 114 Security

## 1.114.1 Perform Security Administration Tasks

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 4 | 考生应知道如何审查系统配置以确保主机安全符合本地安全策略。本目标包括如何配置 TCPWrappers、查找设置了 SUID/SGID 位的文件、验证软件包、设置或更改用户密码和密码 aging 信息，以及根据 CERT、BUGTRAQ 和/或发行版的安全警报更新二进制文件。包括对 ipchains 和 iptable 的基本知识。关键文件、术语和实用程序包括：/proc/net/ip_fwchains、/proc/net/ip_fwname、/proc/net/ip_masquerade、find、ipchains、passwd socket、iptables。 | Chapter 15, "Security Issues" and "Using Network Services" |

## 1.114.2 Set up Host Security

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | 考生应知道如何设置基本的主机安全。任务包括 syslog 配置、影子密码、为 root 邮件设置邮件别名，以及关闭所有未使用的网络服务。关键文件、术语和实用程序包括：/etc/inetd.conf 或 /etc/inet.d/*、/etc/nologin、/etc/passwd、/etc/shadow、/etc/syslog.conf。 | Chapter 11, "Creating and Managing User Accounts" and "User Security Issues" | Chapter 13, "System Logs" | Chapter 15, "Security Issues" |

## 1.114.3 Set up User-level Security

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 1 | 考生应能够配置用户级安全。任务包括对用户登录、进程和内存使用的限制。关键文件、术语和实用程序包括：quota、usermod。 | Chapter 10, "Understanding the File System" | Chapter 11, "Creating and Managing User Accounts" and "User Security Issues" |

## APPENDIX C

## SAIR/GNU CERTIFIED LINUX ADMINISTRATOR (LCA) LEVEL 1 OBJECTIVES

本附录包含 SAIR/GNU Linux 认证管理员（LCA）一级的官方测试目标。这些目标称为能力，可在 www.linuxcertification.org 上在线获取，另有关于 SAIR/GNU LCA 认证计划的附加信息。本认证要求你通过四项考试：安装、管理和网络、安全。本书并未涵盖网络和安全考试的所有要求，但大多数至少已足够涵盖你需要了解的概念。有关这些高级主题的更多详细信息，可在同系列 Course Technology 书籍《Guide to Linux Networking and Security》（ISBN 0-619-00094-5）中找到。

在下面的表格中，通常仅为每个三级标题（例如 1.1.10）提供章节和标题引用。读者应假定更细粒度的标题（例如 1.1.50.1.d）包含在最近提供的三级标题引用中。

![](img/43f64015de86d989e30eff5bb284fb96_821_0.png)

尽管本书已尽最大努力提供及时且相关的信息以确保读者能够通过所有适用的认证考试，请注意，此处提供的能力虽直接取自 SAIR/GNU 网站，但在许多情况下指的是市场上已不再可用的旧技术。熟悉类似的当前技术应能使应试者轻松通过每项考试。

![](img/43f64015de86d989e30eff5bb284fb96_821_1.png)

此处列出的能力编号并非在所有情况下都是连续的。没有能力缺失——SAIR/GNU 网站上出现的编号也不是连续的。

## Course 3X0-101—Linux Installation and Configuration

## 1.1 Theory of Operation

| Competency | Location in This Book (Chapter, Heading) |
|---|---|
| 1.1.10 History of Open Source and Free Software | Chapter 1, "A Brief History" and "Linux in the Market" |
| 1.1.10.1 Describe the historical trends in free software | |
| 1.1.10.2 Define the cost of free software | |
| 1.1.10.3 Describe the advantages and disadvantages of free software | |
| 1.1.20 The GNU General Public License (GPL) | Chapter 1, "A Brief History" and "Linux in the Market" |
| 1.1.20.1 Briefly explain the history of the GNU GPL | |
| 1.1.20.2 Define the use of copyright to enforce copyleft | |
| 1.1.30 Third-party Analysis of open source software | |
| 1.1.30.1 Describe the Microsoft Halloween memos and conclusions | |
| 1.1.40 Living with Free Software | Chapter 1, "Linux in the Market" and "The Work of a System Administrator" |
| 1.1.40.1 Describe the nature of free software development | |
| 1.1.40.2 Explain the business of selling free software | |
| 1.1.40.3 Compare and contrast free software warranty issues with those of proprietary software | |
| 1.1.50 Linux System Concepts | See below |
| 1.1.50.1 Explain the modular structure of Linux | Chapter 1, "A Brief History" |
| 1.1.50.1.a Describe the modular concepts of the Linux kernel | Chapter 13, "Exploring Kernel Components" |
| 1.1.50.1.b Explain the modular nature of the Linux networking subsystem | Chapter 12, "Configuring Linux Networking" |
| 1.1.50.1.c Describe the role of the init process in Linux | Chapter 9, "Init and its Scripts" |

