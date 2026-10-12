

用于网络的硬件设备 457

网络接口卡 457

网络电缆 460

集线器 461

路由器和网桥 461

初始化新的网络硬件 462

使用网络配置工具 464

命令行网络接口配置 465

网络配置文件 469

使用图形化配置工具 472

动态主机配置协议 474

DHCP 的工作原理 475

在安装和启动时激活 DHCP 476

DHCP 软件的安装与配置 477

使用 DHCP 配置网络主机 478

DHCP 的其他用途 480

无线网络 480

Fedora 对无线网络的支持 481

蜂窝网络 482

无线网络的优点 482

从可用的无线协议中进行选择 483

使用补丁/升级来保持网络安全 484

参考 484

通用 484

DHCP 485

无线 485

书籍 485

# 18 互联网连接 487

常见的配置信息 488

奠定基础：localhost 接口 489

检查回环接口的可用性 489

手动配置回环接口 490

配置拨号互联网接入 491

手动配置拨号连接 491

使用 Fedora Core 互联网配置向导 494

配置数字用户线（DSL）接入 497

理解以太网上的点对点协议（PPPoE） 498

手动配置 PPPoE 连接 498

排查连接问题 500

配置拨入式 PPP 服务器 500

参考 503

# 第四部分 Fedora 作为服务器

## 19 Apache Web 服务器管理 509

### 关于 Apache Web 服务器 509

### 安装 Apache 服务器 511

- 从 RPM 安装 511
- 自行编译源代码 513

### 启动和停止 Apache 516

- 手动启动 Apache 服务器 516
- 使用 /etc/rc.d/init.d/httpd 517
- 使用 Red Hat 的 service 命令控制 Apache 519
- 使用 Red Hat 的 chkconfig 命令控制 Apache 519
- 使用 Red Hat 的 system-config-services 客户端控制 Apache 520

### 运行时服务器配置设置 521

- 运行时配置指令 521
- 编辑 httpd.conf 522
- Apache 多部分处理模块 524
- 使用 .htaccess 配置文件 525

### 文件系统认证和访问控制 527

- 使用 allow 和 deny 限制访问 527
- 认证 528
- 关于访问控制的最后说明 531

### Apache 模块 531

- mod_access 532
- mod_alias 532
- mod_asis 532
- mod_auth 533
- mod_auth_anon 533
- mod_auth_dbm 533
- mod_auth_digest 533
- mod_autoindex 534
- mod_cgi 534
- mod_dir 和 mod_env 534
- mod_expires 534
- mod_headers 534
- mod_imap 534
- mod_include 535
- mod_info 和 mod_log_config 535
- mod_mime 和 mod_mime_magic 535
- mod_negotiation 535
- mod_proxy 535
- mod_rewrite 535
- mod_setenvif 536
- mod_speling 536
- mod_status 536
- mod_ssl 536
- mod_unique_id 536
- mod_userdir 536
- mod_usertrack 536
- mod_vhost_alias 536

### 虚拟主机 537

- 基于地址的虚拟主机 537
- 基于名称的虚拟主机 537

### 日志记录 539

### 动态内容 540

### CGI 541

### SSI 542

### 基本 SSI 指令 543

### 流程控制 547

### Apache 的图形界面配置 547

- 配置虚拟主机属性 548
- 配置服务器 549

### 配置 Apache 以达到最佳性能 550

### 用于 Fedora 的其他 Web 服务器 550

- htttpd 550
- Sun ONE Web Server 550
- Stronghold 551
- Zope 551
- Zeus Web Server 551
- TWiki 552

### 参考 552

## 20 数据库服务管理 555

### 数据库基础简述 556

### 关系型数据库如何工作 557

### 理解 SQL 基础 559

- 创建表 560
- 向表中插入数据 561
- 从数据库中检索数据 562

### 选择数据库：MySQL 与 PostgreSQL 564

- 速度 564
- 数据锁定 564
- 事务处理中的 ACID 合规性以保护数据完整性 565
- SQL 子查询 566
- 过程语言和触发器 567

### 配置 MySQL 567

- 为 MySQL 根用户设置密码 568
- 在 MySQL 中创建数据库 569
- 在 MySQL 中授予和回收权限 569

### 配置 PostgreSQL 571

- 初始化 PostgreSQL 的数据目录 571
- 在 PostgreSQL 中创建数据库 573
- 在 PostgreSQL 中创建数据库用户 573
- 在 PostgreSQL 中删除数据库用户 574
- 在 PostgreSQL 中授予和回收权限 575

### 数据库客户端 575

- 通过 SSH 访问数据库 576
- 本地 GUI 客户端访问数据库 577
- Web 访问数据库 577
- MySQL 命令行客户端 578
- PostgreSQL 命令行客户端 580
- 图形化客户端 580

### 参考 581

## 21 文件和打印 583

### 使用网络文件系统 583

- 安装以及启动或停止 NFS 584
- NFS 服务器配置 584
- NFS 客户端配置 586

### 使用 Samba 587

- 使用 /etc/samba/smb.conf 手动配置 Samba 588
- 使用 testparm 命令测试 Samba 591
- 启动 smbd 守护进程 592
- 挂载 Samba 共享 593
- 使用 SWAT 配置 Samba 593

### 使用 Fedora 进行网络和远程打印 598

- 创建网络打印机 598
- 在局域网中启用网络打印 598
- 会话消息块打印 601
- 网络附加打印机配置和打印 601

### 控制台打印控制 603

- 基于控制台的打印机配置 603
- 使用基本打印命令 604
- 管理打印任务 605
- 使用通用 Unix 打印系统（CUPS）图形界面 606
- 创建 CUPS 打印机条目 608
- 避免打印机支持问题 610
- 多功能设备（打印/传真/扫描） 610
- 使用 USB 和旧式打印机 611

### 参考 612

## 22 通过 FTP 进行远程文件服务 613

### 使用 FTP 客户端 613

- FTP 客户端界面 614
- 使用基于文本的 FTP 客户端界面 614
- 使用图形化 FTP 客户端 622

### FTP 服务器 625

- 选择认证服务器或匿名服务器 625
- Fedora FTP 服务器软件包 626
- 其他 FTP 服务器 626
- 安装 FTP 软件 627
- FTP 用户 628
- wu-ftpd 的 xinetd 配置 630
- 为 wu-ftpd 服务器配置 xinetd 630
- 启动非常安全的 FTP 服务器（vsftpd）软件包 631
- 配置非常安全的 FTP 服务器 632
- 控制匿名访问 632
- 其他 vsftpd 服务器配置文件 632

### 配置 Wu-FTPd 服务器 635

- 在 ftpaccess 文件中使用命令配置 wu-ftpd 636
- 配置访问控制 636
- 配置用户信息 639
- 配置系统日志记录 643
- 配置权限控制 644
- 配置针对 ftp.path 的命令 646
- shutdown 文件的结构 647

### 配置 FTP 服务器文件转换操作 647

- 去除前缀 648
- 去除后缀 648
- 添加前缀 648
- 添加后缀 648
- 外部命令 649

