

# Novell® 认证 Linux 工程师 (CLE) 学习指南

Robb H. Tracy

![](img/c7771e8540507f2b00c088c7a411b57b_0_0.png)

## Novell 认证 Linux 工程师 (Novell CLE)：培训/测试路径

![](img/c7771e8540507f2b00c088c7a411b57b_1_0.png)

![](img/c7771e8540507f2b00c088c7a411b57b_1_1.png)

Linux 认证*
Novell CLP、LPI 或同等资质
（非必需，但强烈建议持有）

![](img/c7771e8540507f2b00c088c7a411b57b_1_3.png)

![](img/c7771e8540507f2b00c088c7a411b57b_1_4.png)

![](img/c7771e8540507f2b00c088c7a411b57b_1_5.png)

![](img/c7771e8540507f2b00c088c7a411b57b_1_6.png)

> *参加课程和持有先前的认证并非 Novell CLE 认证的必要条件。
> 通过 Novell 实践考试 (050-685) 是必需的。

## Novell® 认证 Linux 工程师 (Novell CLE) 学习指南

Robb H. Tracy

![](img/c7771e8540507f2b00c088c7a411b57b_2_0.png)

800 East 96th Street, Indianapolis, Indiana 46240 USA

版权所有 © 2005 Novell, Inc.
保留所有权利。未经出版商书面许可，不得以任何形式（电子、机械、影印、录音或其他形式）复制、存储于检索系统或传播本书的任何部分。对于使用本书中包含的信息所产生的任何专利责任，出版商不加以假设。尽管在本书的制备过程中已采取了一切预防措施，但出版商和作者不对错误或遗漏负责。出版商和作者也不对因使用本书中包含的信息而引起的任何损害承担责任。

国际标准书号 (ISBN)：0-7897-3203-3
美国国会图书馆目录卡号：2004101536
美国印刷
首次印刷：2004年10月
07 06 05 04 4 3 2 1

## 商标

书中提到的已知为商标或注册商标的所有术语均已适当大写。Novell Press 无法保证此信息的准确性。本书中对术语的使用不应被视为影响任何商标或注册商标的有效性。

Novell 是注册商标；Novell Press 和 Novell Press 标志是 Novell, Inc. 在美国和其他国家的商标。本书中使用的所有品牌名称和产品名称均为其各自所有者的商品名、服务商标、商标或注册商标。

Linux 是 Linus Torvalds 的注册商标。

## 警告与免责声明

为了使本书尽可能完整和准确，我们已付出所有努力，但不暗示任何保修或适用性。提供的信息是按“原样”基础提供的。对于因使用本书中包含的信息而引起的任何损失或损害，作者和出版商不对任何个人或实体承担任何责任。

## 大宗销售

Pearson Education 在大宗购买或特殊销售时，对本书提供大量折扣。有关更多信息，请联系：

美国企业政府和政府销售
1-800-382-3419
corpsales@pearsontechgroup.com

对于美国以外的销售，请联系：

国际销售
international@pearsoned.com

### 致谢

- **采购编辑**：Jenny Watson
- **开发编辑**：Emmett Dulaney
- **责任编辑**：Charlotte Clapp
- **项目编辑**：Matt Purcell
- **校对编辑**：Bart Reed
- **索引编制**：Chris Barrick
- **校对**：Kathy Bidwell
- **技术编辑**：David Coughanour
- **出版协调**：Vanessa Evans
- **设计师**：Gary Adair
- **页面布局**：Juli Cook

## 内容概览

- 引言 ... 1
- 第 1 章 CLE 实践考试简介 ... 3
- 第 2 章 SUSE Linux 简介 ... 19
- 第 3 章 Linux 管理和配置 ... 67
- 第 4 章 Novell Nterprise Linux 服务 (NNLS) 简介 ... 121
- 第 5 章 NNLS 安装和管理 ... 131
- 第 6 章 使用 eGuide 和 Linux 用户管理进行用户帐户管理 ... 247
- 第 7 章 使用 DirXML 同步用户身份 ... 281
- 第 8 章 使用 iFolder、Samba 和 NetStorage 实现文件服务 ... 331
- 第 9 章 使用 iPrint 实现打印服务 ... 401
- 第 10 章 使用 NetMail 实现邮件服务 ... 437
- 第 11 章 使用 Virtual Office 将所有内容整合在一起 ... 477
- 第 12 章 CLE 练习场景 ... 519
- 索引 ... 537

## 目录

### 引言
1

### 第 1 章
CLE 实践考试简介
3

- CLE 简介
  3
- Novell Nterprise Linux 服务
  4
- 为什么选择 CLE？
  5
- CLE 适合谁？
  7
- CLE 目标
  8
- 如何使用本学习指南
  10
- CLE 测试环境简介
  11
- 为什么要使用实践考试
  11
- CLE 实践考试如何进行
  13
- CLE 实践考试技巧与策略
  15
  - 阅读场景
    16
  - 制定策略
    17
  - 执行计划
    17
  - 测试解决方案
    17
- 摘要
  18

### 第 2 章
SUSE Linux 简介
19

- Linux 概述
  19
  - Linux 历史回顾
    20
  - 关于 GNU
    22
  - Linux 发行版
    22
  - Linux 在计算机系统中的作用
    23
- Linux 用户界面简介
  24
- Linux 文件系统简介
  26
- Linux 用户简介
  33
- 实验练习 2.1：安装新的 SUSE Linux 服务器
  35
- 使用 Linux 命令行
  39
  - Linux Shell
    39
  - 从命令行使用 Linux 命令
    42
  - 常用 Linux 命令
    44
- 实验练习 2.2：使用 Linux 命令行
  47
- 管理 Linux 文件系统
  49
  - 默认 Linux 文件系统结构
    49
  - 命令行文件系统实用程序
    51
  - 使用 mount 命令
    54
  - 管理归档文件
    57
  - 编辑文本文件
    58
- 实验练习 2.3：管理 Linux 文件和目录
  62
- 练习答案
  65
  - 实验练习 2.2
    65
  - 实验练习 2.3
    65
- 摘要
  66

### 第 3 章
Linux 管理和配置
67

- 管理 Linux 用户和组
  67
- Linux 文件系统安全性
  67
- 管理文件所有权和权限
  77
  - 文件所有权
    77
  - 文件权限
    78
- 实验练习 3.1：管理 Linux 安全性
  85
- 管理 Linux 网络配置
  89
  - Linux 网络接口
    89
  - 使用 ifconfig 管理 Linux 网络接口
    91
  - 在 YaST 中配置 Linux 网络接口
    93
- 管理 Linux 应用程序和服务
  98
  - 安装 Linux 软件包
    99
  - 管理 Linux 服务
    102
  - 管理 Linux 进程
    105
- 实验练习 3.2：安装 Linux 产品并管理进程
  107
- 实施和配置 NTP
  111
  - 为什么必须同步时间
    111
- 实验练习 3.3：实施 NTP
  118
- 摘要
  120

### 第 4 章
Novell Nterprise Linux 服务 (NNLS) 简介
121

- NNLS 简介
  121
- 什么是 NNLS？
  122
- NNLS 组件
  124
  - 身份管理
    125
  - 文件管理
    126
  - 打印管理
    127
  - 消息服务
    127
  - 协作服务
    128
  - 版本管理服务
    128
  - 基于 Web 的管理
    128
- Novell 与开源
  129
- 摘要
  130

### 第 5 章
NNLS 安装和管理
131

- 安装 NNLS
  131
- 准备安装 NNLS
  134
- 实验练习 5.1：安装和配置 SLP
  154
- 安装 NNLS
  173
- 实验练习 5.2：准备安装 NNLS
  178
- 实验练习 5.3：安装 NNLS
  183
- 使用 Red Carpet 更新 NNLS
  190
  - 构成 Red Carpet 的组件
    191
  - 配置 Red Carpet
    191
- 实验练习 5.4：使用 rcd 更新 NNLS
  199
- 管理 eDirectory
  201
  - 到底什么是目录？
    201
  - eDirectory 的工作原理
    203
- 实验练习 5.5：管理 eDirectory
  221
- eDirectory 和 LDAP
  227
  - 将 eDirectory 术语与 LDAP 术语对应
    228
  - eDirectory LDAP 集成
    228
  - 将 LDAP 绑定到 eDirectory
    229
  - LDAP 数据交换格式 (LDIF)
    230
- 实验练习 5.6：导入 LDIF 文件
  232

