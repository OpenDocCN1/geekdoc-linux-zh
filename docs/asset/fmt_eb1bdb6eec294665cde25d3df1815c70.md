
# Linux 内核
- Linux 源码树 420
- 内核类型 421
- 管理模块 422
- 何时重新编译 423
- 内核版本 424
- 获取内核源码 425
- 为内核打补丁 426
- 编译内核 427
- 使用 `xconfig` 配置内核 428
- 创建初始内存磁盘 429
- 出现问题时 430
- 编译过程中的错误 431
- 运行时错误、启动加载器问题 432
- 参考文献 433

## Ubuntu 服务器

## 共享文件与打印机
- 使用网络文件系统 434
- 安装并启动 NFS 435
- NFS 服务器配置 436
- NFS 客户端配置 437

## 目录
- 让 Samba 运行 443
- 通过 `/etc/samba/smb.conf` 配置 Samba 444
- 使用 `test` 命令测试 Samba 447
- 启动、停止和重启 `smbd` 进程 448
- 挂载 Samba 共享 449
- 使用 SWAT 配置 Samba 450
- 使用 Ubuntu 进行网络打印 453
- 创建打印机 454
- 使用通用 UNIX 打印系统 GUI 456
- 避免打印支持问题 458
- 参考文献 460

# 22 Apache 管理 461
- 关于 Apache Web 服务器 461
- 安装 Apache 服务器 462
- 从 Ubuntu 仓库安装 463
- 自从源码编译 464
- 启动和停止 Apache 467
- 手动启动 Apache 服务器 467
- 使用 `/etc/init.d/apache2` 468
- 运行时服务器设置 469
- 运行时配置指令 470
- 编辑 `apache2.conf` 470
- Apache 多进程模块 473
- 使用 `.htaccess` 配置文件 473
- 文件系统身份验证与访问控制 475
- 使用 `allow` 和 `deny` 限制访问 476
- 身份验证 477
- 关于访问控制的结语 479
- Apache 模块 480
- `mod_access` 481
- `mod_alias` 481
- `mod_asis` 481
- `mod_auth` 482
- `mod_auth_dbm` 482
- `mod_auth_digest` 482
- `mod_autoindex` 482
- `mod_cgi` 483
- `mod_dir` and `mod_env` 483
- `mod_expires` 483
- `mod_headers` 483

## 目录 XIX
`mod_include` 484
`mod_info` and `mod_log_config` 484
`mod_mime` and `mod_mime_magic` 484
`mod_negation` 484
`mod_proxy` 484
`mod_rewrite` 484
`mod_setenux` 485
`mod_spelling` 485
`mod_status` 485
`mod_ssl` 485
`mod_unique_id` 485
`mod_userid` 485
`mod_usertrack` 485
`mod_vhost_alias` 486

虚拟主机 486
基于地址的虚拟主机 486
基于名称的虚拟主机 486
日志记录 488
参考文献 490

# 23 其他 HTTP 服务器 491
`Nginx` 491
`lighthttpd` 493
`Yaws` 494
`Cherokee` 494
`Jetty` 495
`thttpd` 495
`Apache Tomcat` 496
参考文献 496

# 24 使用 FTP 进行远程文件传输 497
选择 FTP 服务器 497
选择身份验证服务器或匿名服务器 498
Ubuntu FTP 服务器包 498
其他 FTP 服务器 498
安装 FTP 软件 499
FTP 用户 500
配置非常安全的 FTP 服务器 (`vsftpd`) 502
控制匿名访问 503
其他 `vsftpd` 服务器配置文件 504
使用 `fhosts` 文件允许或拒绝 FTP 服务器连接 505
参考文献 506

# 25 处理邮件 507
邮件如何发送和接收 507
邮件传输代理 (MTA) 508
选择 MTA 510
邮件投递代理 (MDA) 511
邮件用户代理 (MUA) 521
基础 Postfix 的配置与操作 512
配置伪装 (Masquerading) 514
使用智能主机 (Smart Hosts) 515
设置邮件投递间隔 515
邮件中继 516
使用别名转发邮件 516
