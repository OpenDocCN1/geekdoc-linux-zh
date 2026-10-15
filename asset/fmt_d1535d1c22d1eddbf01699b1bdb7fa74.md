
- Ubuntu 对无线网络的支持 357
- 无线网络的优点 358
- 从可用的无线协议中选择 359

### 15 使用 SSH 和 Telnet 进行远程访问 371
- 设置 Telnet 服务器 371
- Telnet 与 SSH 的比较 372
- 设置 SSH 服务器 372
- SSH 工具 373
- 使用 `scp` 在机器之间复制单个文件 374
- 使用 `sftp` 在机器之间复制多个文件 374
- 使用 `ssh-keygen` 启用基于密钥的登录 375
- 远程 X 377
- XDMCP 377
- VNC 378
- 参考 378

### 第四部分 Ubuntu 作为服务器

### 16 文件和打印 381
- 使用网络文件系统 382
- 安装并启动或停止 NFS 382
- NFS 服务器配置 383
- NFS 客户端配置 384
- 让 Samba 投入使用 385
- 使用 `/etc/samba/smb.conf` 手动配置 Samba 387
- 使用 `testparm` 命令测试 Samba 390

### 17 Apache Web 服务器管理 407
- 避免打印机支持问题 403
- 一体机（打印/传真/扫描）设备 403
- 使用 USB 和旧式打印机 403
- 参考 405
- 关于 Apache Web 服务器 407
- 安装 Apache 服务器 409
- 使用 APT 安装 409
- 自行构建源代码 410
- 启动和停止 Apache 413
- 手动启动 Apache 服务器 413
- 使用 `/etc/init.d/apache2` 414
- 运行时服务器配置设置 416
- 运行时配置指令 416
- 编辑 `apache2.conf` 417
- Apache 多处理模块 419
- 使用 `.htaccess` 配置文件 420
- 文件系统身份验证和访问控制 422
- 使用 `allow` 和 `deny` 限制访问 422
- 身份验证 423
- 关于访问控制的最后说明 425
- Apache 模块 426
- `mod_access` 427
- `mod_alias` 427
- `mod_asis` 427
- `mod_auth` 428
- `mod_spelling` 431
- `mod_status` 431
- `mod_ssl` 431
- `mod_unique_id` 431
- `mod_userdir` 431
- `mod_usertrack` 431
- `mod_vhost_alias` 431
- 虚拟主机 432
- 基于地址的虚拟主机 432
- 基于名称的虚拟主机 432
- 日志记录 434
- 可与 Ubuntu 搭配使用的其他 Web 服务器 435
- Sun ONE Web 服务器 436
- Zope 436
- Zeus Web 服务器 436
- 参考 437

### 18 使用 FTP 进行远程文件服务 439
