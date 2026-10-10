

# 目录

- 使用 SSH Communications (Windows 图形界面) 创建密钥 142
- 如何将 SSH 客户端密钥对上传到 SSH Communications 的 SSH 服务器 144
- 如何将 SSH 客户端密钥对上传到 OpenSSH 服务器 145
- 如何将 SSH 客户端密钥对上传到 VShell SSH 服务器 147
- 使用 VanDyke SecureCRT 创建密钥 148
- VShell SSH 服务器 149
- OpenSSH 150
- SSH Communications 的 SSH 服务器 151
- SSH 代理 152
- 小结 153

## 第 5 章：SSH 管理 155

- 网络设备 156
- 思科路由器 157
- 思科交换机 160
- 思科 VPN 集中器 160
- 思科 PIX 防火墙 162
- 网络器件过滤器 163
- 安全管理 164
- 管理服务器 165
- 双因素认证 167
- SOCKS 管理 169
- SSH：用户限制 172
  - Chroot 172
  - 用户访问控制 173
  - SSH 用户限制 175
- SSH：网络访问控制 177
  - SSH TCP 包装器 177
  - SSH 连接过滤器 179
- SSH 主机限制 181
- 小结 183

## 第 2 部分：远程访问解决方案 185

### 第 6 章：SSH 端口转发 187

- 客户端端口转发的网络基础 193
- 服务器端口转发的网络基础 200
- SSH 端口转发 201
- SSH 客户端的本地端口转发 205
  - 命令行客户端配置 205
  - SSH Communications 图形界面 SSH 客户端配置 207
  - VanDyke Software 的 Secure CRT 配置 209
  - PuTTY 配置 211
- SSH 客户端的远程端口转发 213
  - OpenSSH 客户端配置 (Unix 和 Windows) 213
  - SSH Communications 命令行客户端配置 (Unix 和 Windows) 214
  - SSH Communications 图形界面 SSH 客户端配置 (Windows) 214
  - VanDyke Software 的 SecureCRT 配置 215
- SSH 服务器的端口转发 217
  - OpenSSH 服务器配置 (Unix 和 Windows) 217
  - SSH Communications SSH 服务器配置 (Unix) 217
  - SSH Communications SSH 服务器配置 (Windows) 220
  - VanDyke Software 的 VShell SSH 服务器配置 222
- SSH 端口转发的优势 225
- 小结 226

## 第 7 章：安全远程访问 229

- 使用 SSH 实现安全电子邮件 230
  - 设置 SSH 服务器 232
  - 设置 SSH 客户端 232
  - 设置电子邮件客户端 234
  - 执行安全电子邮件 237
- 使用 SSH 实现安全文件传输 (SMB 和 NFS) 238
  - 设置 SSH 服务器 241
  - 设置 SSH 客户端 241
  - 设置文件服务器客户端 243
  - 执行安全文件传输 243
    - 使用 SMB 和 SSH 进行安全文件共享 244
    - 使用 NFS 和 SSH 进行安全文件共享 245
- 使用 SSH 实现安全管理 246
  - 设置 SSH 服务器 248
  - 设置 SSH 客户端 249
  - 设置管理客户端 252
  - 执行安全管理 252
    - 使用 Windows 终端服务 (Windows Terminal Services) 和 SSH 进行安全管理 253
    - 使用 VNC 和 SSH 进行安全管理 255
    - 使用 pcAnywhere 和 SSH 进行安全管理 257
- 使用 SSH 实现安全 VPN (PPP over SSH) 259
  - 服务器上的 PPP 守护进程 260
  - VPN 用户和 Sudo 261
  - 客户端脚本 261
- 小结 264

## 第 3 部分：协议替换 267

### 第 8 章：SSH 的多功能性 269

- 终端访问 270
  - 使用远程 Shell (RSH) 破坏系统安全 271
  - 使用远程登录 (Rlogin) 破坏系统安全 272
  - 使用远程执行 (Rexec) 破坏系统安全 273
  - 为什么通过 SSH 访问更好 274
- 使用安全文件传输协议 (SFTP) 进行文件传输 276
  - 使用 OpenSSH SFTP 服务器的 SFTP 277
  - 使用 OpenSSH 进行管理目的 277
  - 使用 OpenSSH 进行文件共享 278
  - 使用 OpenSSH 授权用户 279
  - Windows 和 Cygdrive 上的 OpenSSH 280
  - 使用 VanDyke Software VShell 的 SFTP 281
  - 使用 VShell 进行管理目的 281
  - 使用 VShell 进行文件共享 282
  - 使用 VShell 授权用户 287
  - 使用 SSH Communications SSH 服务器的 SFTP 287
  - 使用 SSH Communications SSH 服务器进行管理目的 288
  - 使用 SSH Communications SSH 服务器进行文件共享 289
  - 使用 SSH Communications SSH 服务器授权用户 292
  - 三种 SFTP 解决方案的比较 292
- 安全聊天 293
- 安全备份 297
- 小结 299

## 第 9 章：安全 Web 环境中的代理技术 301

- SSH 和 SOCKS 302
- 动态端口转发和 SOCKS 310
- 使用 SSH 进行安全 Web 浏览 314
- 通过 HTTP 代理使用 SSH 321
- 使用 SSH 保护无线网络 323
- 使用 SSH 和 HTTP 代理保护无线网络安全 324
- 使用 SSH 和动态端口转发保护无线网络安全 325
- 小结 326

## 第 10 章：SSH 案例研究 329

- 案例研究 #1：安全远程访问 330
  - 问题情境 330
  - 业务需求 330
  - 配置 334
    - SSH 客户端配置 334
    - SSH 服务器配置 339
  - 结果检查表 343
- 案例研究 #2：安全无线连接 344
  - 问题 344
  - 业务需求 344
  - 配置 347
    - SSH 客户端配置 347
    - SSH 服务器配置 350
  - 结果检查表 351
- 案例研究 #3：安全文件服务器 353
  - 问题 353
  - 业务需求 353
  - 配置 354
    - SSH 服务器配置 354
    - SSH 客户端配置 356
  - 结果检查表 357
  - 小结 358

尾声 359

索引 361

# 致谢

我想承认并感谢在我职业生涯中帮助过我的几个人。以下人员以多种方式支持了我，使我成为了一名更优秀的专业人士。向这些人，我想说声谢谢：Andy Hubbard, Ronnie Dinfotan, Amy Bergstrom, Tim Gartin, Troy Cardinal, Anthony Barkley, Jason Chan, Kevin Rich, Paul Nash, Nitra Lagrander, Sumit Kakra, Glen Joes, Joel Wallenstrom, Ted Barlow, Allen Dawson, Rob Helt, Larry Harvey, and jum4nj1. 此外，特别感谢 Mike Schifffman, Carol Long, 和 Scott Amerman，他们对这本书的成立起到了至关重要的作用。

# 关于作者

Himanshu Dwivedi 是 @stake 的管理安全架构师，@stake 是数字安全服务的领先提供商。Himanshu 在信息安全方面拥有超过九年的经验，并在 Electronic Data Systems (EDS)、Deloitte and Touche 和 @stake 拥有多年的技术安全经验。他拥有广泛的安全技能，专长于电信行业。此外，他还在美国、欧洲、南美洲和亚洲的主要组织工作过，包括一些主要的软件、制造和基于金融的实体。此外，Himanshu 在多个领域拥有各种技能，包括操作系统 (Microsoft NT/2000, Linux RedHat/Caldera, OpenBSD)；防火墙 (Checkpoint Firewall-1, ipfilter, ipchains)；入侵检测系统 (ISS, Tripwire, Snort 等)；大型机 (OS/3900-RACF)；协议 (SSH, SSL, and IPSEC)；存储区域网络 (EMC, Network Appliance, Brocade, Qlogic)；存储协议 (Fibre Channel, iSCSI, Gigabit IP 等)；网络设备 (Cisco, Nortel, Netscreen 等)；以及各种其他产品和技术。Himanshu 是全美各地提供的几门安全培训课程的主要讲师，包括网络攻击与对策、存储安全和 Windows 2000 安全。

在 @stake，Himanshu 领导存储卓越中心 (CoE)，该中心专注于存储技术的研究和培训，包括网络附加存储 (NAS) 和存储区域网络 (SAN)。他被视为 SAN 安全领域的行业专家，特别是光纤通道安全 (Fibre Channel Security) 方面。他就在 SAN 安全方面进行了大量演示和研讨会，包括 BlackHat 安全会议、SNIA 安全峰会、Storage Networking World、TechTarget 的存储管理大会、StorageWorld、光纤通道大会、SAN-West 和 SAN-East。

