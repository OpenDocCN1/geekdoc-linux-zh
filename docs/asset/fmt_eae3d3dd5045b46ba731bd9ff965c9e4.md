
## 第29章，“Unicode/字符集”

- Jelmer R. Vernooij <jelmer@samba.org>
- John H. Terpstra <jht@samba.org>
- TAKAHASHI Motonobu <monyo@home.monyo.com>（日文字符支持）

## 第30章，“备份技术”

- John H. Terpstra <jht@samba.org>

## 第31章，“高可用性”

- John H. Terpstra <jht@samba.org>
- Jeremy Allison <jra@samba.org>

## 第32章，“处理大型目录”

- Jeremy Allison <jra@samba.org>
- John H. Terpstra <jht@samba.org>

## 第33章，“高级配置技术”

- John H. Terpstra <jht@samba.org>

## 第34章，“从 Samba-2.x 升级到 Samba-3.0.20”

- Jelmer R. Vernooij <jelmer@samba.org>
- John H. Terpstra <jht@samba.org>
- Gerald (Jerry) Carter <jerry@samba.org>

## 第35章，“从 NT4 PDC 迁移到 Samba-3 PDC”

- John H. Terpstra <jht@samba.org>

## 第36章，“SWAT：Samba 网络管理工具”

## 第37章，“Samba 检查表”

- Andrew Tridgell <tridge@samba.org>
- Jelmer R. Vernooij <jelmer@samba.org>
- Dan Shearer <dan@samba.org>

## 第38章，“分析和解决 Samba 问题”

- Gerald (Jerry) Carter <jerry@samba.org>
- Jelmer R. Vernooij <jelmer@samba.org>
- David Bannon <dbannon@samba.org>
- Dan Shearer <dan@samba.org>

## 第39章，“报告 Bug”

- John H. Terpstra <jht@samba.org>
- Jelmer R. Vernooij <jelmer@samba.org>
- Andrew Tridgell <tridge@samba.org>

## 第40章，“如何编译 Samba”

- Jelmer R. Vernooij <jelmer@samba.org>
- John H. Terpstra <jht@samba.org>
- Andrew Tridgell <tridge@samba.org>

## 第41章，“可移植性”

- Jelmer R. Vernooij <jelmer@samba.org>
- John H. Terpstra <jht@samba.org>

## 第42章，“Samba 和其他 CIFS 客户端”

## 第43章，“Samba 性能调优”

- Paul Cochrane <paulc@Dth.scot.nhs.uk>^110
- Jelmer R. Vernooij <jelmer@samba.org>^111
- John H. Terpstra <jht@samba.org>^112

## 第46章，“DNS 和 DHCP 配置指南”

- John H. Terpstra <jht@samba.org>^113

[^106]: <mailto:jelmer@samba.org>
[^107]: <mailto:jht@samba.org>
[^108]: <mailto:dan@samba.org>
[^109]: <mailto:jmcd@us.ibm.com>
[^110]: <mailto:paulc@Dth.scot.nhs.uk>
[^111]: <mailto:jelmer@samba.org>
[^112]: <mailto:jht@samba.org>
[^113]: <mailto:jht@samba.org>

#### 20.8.4 错误消息：“Cannot connect under a different Name”

336

#### 20.8.5 组装驱动程序文件时需谨慎

337

#### 20.8.6 Samba 和打印机端口

340

#### 20.8.7 避免常见的客户端驱动程序错误配置

340

### 20.9 Imprints 工具集

341

#### 20.9.1 什么是 Imprints？

341

#### 20.9.2 创建打印机驱动包

341

#### 20.9.3 Imprints 服务器

341

#### 20.9.4 安装客户端

342

### 20.10 无需用户交互添加网络打印机

342

### 20.11 addprinter 命令

344

### 20.12 将传统打印迁移到 Samba

344

### 20.13 在活动目录或 LDAP 中发布打印机信息

345

### 20.14 常见错误

345

#### 20.14.1 我提供我的根密码但我无法获得访问权限

345

#### 20.14.2 我的打印作业被放入暂存目录，但随后丢失

345

## 第 21 章 CUPS 打印支持

347

### 21.1 简介

347

#### 21.1.1 功能与优势

347

#### 21.1.2 概述

347

### 21.2 基本 CUPS 支持配置

348

#### 21.2.1 链接 smbd 与 libcups.so

348

#### 21.2.2 CUPS 的简单 smb.conf 设置

349

#### 21.2.3 更复杂的 CUPS smb.conf 设置

350

### 21.3 高级配置

351

#### 21.3.1 集中暂存 vs “对等” 打印

351

#### 21.3.2 原始打印服务：Windows 客户端上的厂商驱动程序

351

#### 21.3.3 Windows 客户端驱动程序安装

352

#### 21.3.4 显式启用 application/octet-stream 的 “raw” 打印

352

#### 21.3.5 驱动程序上传方法

353

### 21.4 使用 PostScript 驱动程序下载的高级智能打印

354

#### 21.4.1 Windows 上的 GDI，UNIX 上的 PostScript

354

#### 21.4.2 Windows 驱动程序、GDI 和 EMF

354

#### 21.4.3 UNIX 打印文件转换和 GUI 基础

355

#### 21.4.4 PostScript 和 Ghostscript

356

#### 21.4.5 Ghostscript：非 PostScript 打印机的软件 RIP

357

#### 21.4.6 PostScript 打印机描述 (PPD) 规范

358

#### 21.4.7 使用 Windows 格式的厂商 PPD

359

#### 21.4.8 CUPS 也使用非 PostScript 打印机的 PPD

360

### 21.5 CUPS 过滤架构

361

#### 21.5.1 MIME 类型和 CUPS 过滤器

362

#### 21.5.2 MIME 类型转换规则

362

#### 21.5.3 过滤概述

363

##### 21.5.3.1 过滤器要求

363

#### 21.5.4 预过滤器

363

#### 21.5.5 pstops

364

#### 21.5.6 pstoraster

365

#### 21.5.7 imagetops 和 imageraster

365

#### 21.5.8 rasterto [特定打印机]

366

#### 21.5.9 CUPS 后端

366

#### 21.5.10 cupsomatic/fooomatic 的作用

369

#### 21.5.11 全貌

370

#### 21.5.12 mime.convs

370

#### 21.5.13 “原始” 打印

370

#### 21.5.14 application/octet-stream 打印

371

#### 21.5.15 非 PostScript 打印机的 PostScript 打印机描述

372

#### 21.5.16 cupsomatic/fooomatic-rp 与 CUPS 原生打印

372

#### 21.5.17 过滤链示例

374

#### 21.5.18 CUPS 驱动程序/PPD 的来源

375

#### 21.5.19 使用接口脚本打印

376

### 21.6 网络打印（纯 Windows）

377
