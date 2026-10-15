
# SUSE Linux Enterprise Server 管理指南 (课程 3037) (Novell 授权教材)

![](img/667acce1695f6403deb2b60e994760c8_0_0.png)

Dave Garza

Sandy Clark

Stephen Helba

William Pitkin III

Nick Lombardi

Manya Chylinski

Amy Lyon

John Bosco

Brooke Booth

Ed Sawicki

Deborah Yarnell

Dennis Williams

Susan Carroll

Dawn Daugherty

Laura Rickenbach

GEX Publishing Services

www.course.com

前言 XIII

引言 1

前言 XIII

+ 引言 1

课程目标 2

读者群体 2

先决条件 3

SLES 9 5

议程 6

约定 7

# 第一部分

## 管理 SUSE Linux Enterprise Server 9 简介

目标 1 描述 SUSE Linux Enterprise Server 9

SLES 9 10

SLES 9 10

硬件支持 17

目标 2 SLES 9 20

SLES 9 22

目标 3 SLES 9 27

SLES 9 29

硬件信息 32

`/proc/` 33

`/boot/` 35

命令行工具 36

命令行工具 37

界面 41

章节总结 45

本术语 47

7 练习 48

# 第二部分

## 管理用户访问与安全 51

目标 1 描述用户安全 52

用户安全 52

用户组 52

目标 2 管理用户与组 62

使用 YaST 管理用户 62

使用 YaST 管理组 65

用户设置 68

从命令行管理用户任务

使用 sudo 管理用户任务

默认设置

权限 权限

权限设置

从命令行管理权限

使用界面管理权限

PAM 配置

目标 5 配置 PAM

PAM 结构

PAM 示例

目标 6 实现安全策略

安全策略指南

SLES 安全信息

监控登录活动

章节总结

# 第三部分

## 管理 Linux 文件系统 137

目标 1 描述 Linux 文件系统

Linux 文件系统

文件系统格式

文件系统特性

文件系统日志

目标 2 配置文件系统分区

分区类型

Linux 命名

分区设计指南

分区优化

使用 YaST 管理分区

目标 3 使用逻辑卷管理文件系统 (LVM)

LVM 组件

LVM 功能

使用 YaST 配置逻辑卷

目标 4 配置 Linux 系统 179

使用 YaST 配置分区 180

从命令行配置分区 182

挂载文件系统 184

监控并检查文件系统 193

启动、救援或模块磁盘 196

目标 5 设置并配置配额 199

准备文件系统 200

初始化配额系统 201

配置用户和组配额 202

启动并激活配额服务 204

目标 6 备份文件系统 206

数据备份策略 207

使用 YaST 恢复系统 212

数据备份命令行 216

章节总结 221

术语 222

问题 225

# 第四部分

## SUSE Linux 系统管理 229

目标 1 管理 RPM 软件包 230

RPM 组件与功能 230

RPM 基础 231

使用 `rpm` 管理软件包 232

使用 YaST 管理软件包 240

目标 2 验证并更新软件库访问 246

软件库基础 247

查看共享库依赖 (`ldd`) 248

修改软件库配置文件 (`/etc/ld.so.conf`) 248

更新库缓存 (`/etc/ld.so.cache`) 249

目标 3 使用 YaST 在线服务器 (YOU) 管理更新 251

YOU 基础 251

配置本地 YOU 服务器 252

配置和使用 YOU 客户端 255

章节总结 263

术语 264

问题 265

# 第五部分

## 系统初始化 267

目标 1 描述 Linux 加载过程 268

目标 2 管理运行级别 271

运行级别基础 271

在启动时更改运行级别 280

从命令行管理运行级别 280

关机或停止系统 281

使用 YaST 设置运行级别 282

目标 3 管理内核 286

内核模块基础 286

如何查找硬件驱动程序信息 287

如何从命令行管理模块 292

`modprobe` 配置文件 (`/etc/modprobe.conf`) 294

内核模块加载器 (`kmod`) 294

目标 4 管理 GRUB 引导程序 295

什么是启动管理器 296

SUSE Linux 中的启动管理器 296

如何启动 GRUB Shell 298

如何修改 GRUB 配置文件 299

如何使用 YaST 配置 GRUB 300

目标 5 修改系统设置 308

查看并更改系统设置 (`/proc/sys/`) 308

使用 Powertop 修改内核和硬件参数 310

使用 YaST 配置 `/etc/sysconfig/` 313

本章总结 317

关键术语 318

复习题 321

探索练习 323

# 第六章

## 管理 Linux 进程与服务 325

目标 1 管理进程 326

进程定义 326

作业与进程 328

如何管理前台和后台进程 329

如何设置进程优先级 330

如何结束进程 335

进程与服务（守护进程） 338

如何管理守护进程 340

目标 2 描述启动 Shell 脚本与服务 346

启动脚本 346

启动脚本目录结构 347

启动脚本结构 348

目标 3 调度作业 353

仅运行一次作业 (`at`) 355

目标 4 使用系统日志服务 357

Syslog 守护进程 362

重要日志文件 366

如何使用 YaST 查看日志文件 367

如何归档日志文件 (`logrotate`) 368

如何监控硬盘空间 371

本章总结 377

关键术语 378

复习题 380

探索练习 383

## 将 SUSE Linux 企业服务器连接到网络 385

目标 1 配置你的网络连接 386

TCP/IP 基础 386

Linux 中的网络接口 393

网络接口要求 393

如何使用 YaST 配置网卡 394

如何手动修改网卡 400

目标 2 配置和管理路由 406

路由类型 407

如何修改路由配置文件 411

如何激活路由 412

如何使用 `ip` 管理网络接口和路由 412

目标 3 测试网络接口 416

检查主机间的网络连接 (`ping`) 416

检查路由 (`traceroute`) 419

分析网络流量 (`tcpdump` 和 `ethereal`) 421

确定所有网络连接的状态 (`netstat`) 426

检查服务可用性 (`netcat`) 428

本章总结 434

关键术语 434

复习题 437

探索练习 439

## 启用基础服务 441

目标 1 配置和管理网络打印服务 442

打印机与 Linux 支持 442

CUPS 与 SUSE Linux 企业服务器 442

如何配置 SUSE Linux 企业服务器网络打印机 445

如何修改 SUSE Linux 企业服务器网络打印机 452

如何从命令行管理打印 458

如何访问 CUPS Web 管理工具 462

如何排错 CUPS 打印系统 467

目标 2 配置网络文件系统 471

网络文件系统 (NFS) 471

Samba (CIFS) 486

如何监控和测试 Samba 500

目标 3 管理网络资源 504

网络信息服务 (NIS) 504

LDAP 530

本章总结 540

关键术语 542

复习题 545

探索练习 547

目标 1 配置 SUSE Linux 企业服务器时间

SUSE Linux 企业服务器时间概述

如何使用 `hwclock` 和 `date` 同步时间

什么是网络时间协议 (NTP)

如何使用 NTP 同步时间

目标 2 启用 Web 服务器 (Apache)

Web 服务器的工作原理

Apache 与 SUSE Linux

如何使用 YaST 配置 Apache HTTP 服务器

目标 3 启用扩展守护进程 (xinetd)

需要什么

如何使用 YaST 配置 `xinetd`

如何手动管理 `xinetd`

如何配置 TCP Wrapper

目标 4 启用 FTP 服务器

FTP 服务器的作用

FTP 如何工作

PureFTPd 服务器的优势
