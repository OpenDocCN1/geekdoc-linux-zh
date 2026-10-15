
病毒 599

配置你的防火墙 600

AppArmor 604

制定灾备计划 607

参考文献 608

# 第 21 章 性能调优 610

硬盘 610

使用 BIOS 和内核调优驱动器 611

`hdparm` 命令 612

文件系统调优 613

`tune2fs` 命令 614

`e2fsck` 命令 615

`badblocks` 命令 615

禁用文件访问时间 615

内核 616

Apache 617

MySQL 619

测量键缓冲区使用情况 619

使用查询缓存 621

各种微调 623

查询优化 623

参考文献 624

# 第 22 章 内核与模块管理 625

Linux 内核 626

Linux 源码树 627

内核类型 630

模块管理 631

何时需要重新编译 634

内核版本 635

获取内核源码 636

补丁内核 637

编译内核 640

使用 `xconfig` 配置内核 644

创建初始内存磁盘 (initrd) 镜像 648

出现问题时 648

编译期间的错误 649

内核引导加载器问题 650

参考文献 650

# 第四部分：Ubuntu 作为服务器 652

# 第 23 章 文件与打印机共享 653

使用网络文件系统 (NFS) 654

安装并启动或停止 NFS 654

NFS 服务器配置 654

让 Samba 工作起来 656

手动配置 `/etc/samba/smb.conf` 659

使用 `testpara` 测试 Samba 663

启动、停止和重启 `smbd` 进程 663

挂载 Samba 共享 665

Ubuntu 的网络打印 666

创建网络打印机 666

使用通用 UNIX 打印系统 GUI 668

避免打印机问题 670

参考文献 672

# 第 24 章 Apache 服务器管理 673

关于 Apache Web 服务器 673

安装 Apache 服务器 674

启动和停止 Apache 675

运行时服务器配置设置 677

运行时配置指令 677

编辑 `apache2.conf` 678

Apache 多进程模块 681

使用 `.htaccess` 配置文件 682

文件系统身份验证与访问控制 684

使用 `Require` 限制访问 685

身份验证 685

访问控制的结语 688

# Apache 模块 689

- `mod_access` 690
- `mod_alias` 690
- `mod_asis` 690
- `mod_auth` 691
- `mod_auth_anon` 691
- `mod_auth_dbm` 691
- `mod_auth_digest` 691
- `mod_autoindex` 692
- `mod_cgi` 692
- `mod_dir` and `mod_env` 692
- `mod_expires` 692
- `mod_headers` 692
- `mod_include` 693
- `mod_info` and `mod_log_config` 693
- `mod_mime` and `mod_mime_magic` 693
- `mod_negotiation` 693
- `mod_proxy` 693
- `mod_rewrite` 694
- `mod_setenvif` 694
- `mod_speling` 694
- `mod_status` 694
- `mod_unique_id` 695
- `mod_userdir` 695
- `mod_usertrack` 695
- `mod_vhost_alias` 695

虚拟主机 695

基于地址的虚拟主机 696

基于名称的虚拟主机 696

日志 698

HTTPS 700

参考文献 702

## 第 25 章 Nginx Web 服务器管理 703

关于 Nginx Web 服务器 703

安装 Nginx 服务器 706

从 Ubuntu 存储库安装 706

从源码编译 706

配置 Nginx 服务器 707

虚拟主机 710

设置 PHP 712

添加和配置模块 713

HTTPS 714

参考文献 716

## 第 26 章 其他 HTTP 服务器 717

`lighttpd` 717

`Yaws` 718

`Cherokee` 718

`Jetty` 719

`lighttpd` 720

Apache Tomcat 720

参考文献 720

## 第 27 章 使用 FTP 进行远程文件服务 722

选择 FTP 服务器 722

选择身份验证服务器或匿名服务器 723

Ubuntu FTP 服务器软件包 723

其他 FTP 服务器 724

安装 FTP 软件 725

FTP 用户 725

配置非常安全的 FTP 服务器 (`vsftpd`) 728

控制匿名访问 729

其他 `vsftpd` 服务器配置文件 730

使用 `ifhosts` 文件允许或拒绝 FTP 服务器连接 731

参考文献 733

## 第 28 章 处理邮件 734

邮件是如何发送和接收的 734

邮件传输代理 (MTA) 735

选择 MTA 738

邮件投递代理 (MDA) 738

邮件用户代理 (MUA) 739

基础 Postfix 配置与操作 740

配置伪装 (Masquerading) 743

使用智能主机 (Smart Hosts) 744

设置邮件投递间隔 744

邮件中继 745

使用别名转发邮件 746

使用 Fetchmail 获取邮件 747

安装 Fetchmail 747

配置 Fetchmail 747

选择邮件投递代理 751

Promail 752

Spamassassin 752

| 服务 | 页码 |
| :--- | :--- |
| Squirrelmail | 753 |
| 病毒扫描器 | 753 |
| 自动应答器 | 753 |
| Microsoft Exchange Server 的替代方案 | 753 |
| Microsoft Exchange Server/Outlook 客户端 | 754 |
| CommuniGate Pro | 755 |
| Oracle Beehive | 755 |
| Bynari | 755 |
| Open-Xchange | 755 |
| Horde | 755 |

参考文献 756

## 第 29 章 代理、反向代理和虚拟专用网络 (VPN) 757

* 什么是代理服务器？ | 757
* 安装 Squid | 758
* 配置客户端 | 758
* 访问控制列表 (ACLs) | 759
* 指定客户端 IP 地址 | 765
* 示例配置 | 766
* 虚拟专用网络 (VPN) | 768
* 设置 VPN 客户端 | 770
* 设置 VPN 服务器 | 772

参考文献 774

## 第 30 章 关系型数据库服务的管理 776

* 数据库基础简要回顾 | 778
* 关系型数据库如何工作 | 779
* 理解 SQL 基础 | 782
* 创建表 | 782
* 向表中插入数据 | 784
* 从数据库中检索数据 | 785
* 选择数据库：MySQL 对比 PostgreSQL | 788
* 速度 | 788
* 数据锁定 | 788
* 事务处理中的 ACID 合规性保护 | 789
* 数据完整性 | 789
* SQL 子查询 | 790
* 过程化语言和触发器 | 791
* 配置 MySQL | 791
* 为 MySQL Root 设置密码 | 792
* 在 MySQL 中创建数据库 | 793
* 初始化 PostgreSQL 的数据目录 | 796
* 在 PostgreSQL 中创建数据库 | 797
* 在 PostgreSQL 中创建数据库用户 | 798
* 在 PostgreSQL 中删除数据库用户 | 798
* 在 PostgreSQL 中授予和撤销权限 | 799
* 数据库客户端 | 800
* 通过 SSH 访问数据库 | 801
* 通过本地 GUI 访问数据库 | 803
* 通过 Web 访问数据库 | 803
* MySQL 命令行客户端 | 805
* PostgreSQL 命令行客户端 | 807
* 图形化客户端

## 第 31 章 NoSQL 数据库 809

* 键值存储 | 812
* Cassandra | 813
* Memcached 和 Memcache | 814
* Redis | 815
* Riak | 815
* 文档存储 | 815
* CouchDB | 816
* MongoDB | 817
* BaseX | 818
* 宽列存储 | 819
* BigTable | 819
* 图形存储 | 820
* Neo4j | 820
* OrientDB | 821
* HyperGraphDB | 821
* FlockDB | 821

参考文献 821
