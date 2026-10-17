
+ 练习 10-2 从命令行管理打印机. . . 10-31

### 目标 2

+ 理解 CUPS 如何工作 . . . . . . . . . . . . . . . . 10-32

+ 打印过程的步骤 . . . . . . . . . . . . . 10-32

+ 打印队列 . . . . . . . . . . . . . . . . . . . 10-34

+ 日志 . . . . . . . . . . . . . . . . . . . 10-37

+ 配置文件 . . . . . . . . . . . 10-41

# 目标 3

+ 配置打印服务器 . . . . . . . . . . . 10-42

+ 向计算机广播打印信息 . . . . . . . . 10-43

+ 限制 . . . . . . . . . . . . . . . . . . 10-47

+ 限制用户和组访问 . . . . . . . . . . 10-50

+ 限制 Web 界面 . . . . . . . . . . 10-52

+ 练习 10-3 限制访问 . . . . . . . . . . 10-54

# 目标 4

+ 使用 Web 界面管理 CUPS 服务器 . . . . 10-55

+ 管理任务 . . . . . . . . . . . . . 10-56

+ 管理类 . . . . . . . . . . . . . . . 10-57

+ 在线帮助 . . . . . . . . . . . . . . . 10-58

+ 管理作业 . . . . . . . . . . . . . . 10-58

+ 管理打印机 . . . . . . . . . . . . . . 10-59

+ 练习 10-4 使用 Web 界面管理 CUPS 服务器 . . . 10-61

# 目标 5

目标 . . . . . . . . . . . . . . . . . . . 11-1

# 目标 1 使用 SSH 提供安全访问 . . . . . . 11-2

+ 加密学基础 . . . . . . . . . . . . . . . 11-3

+ 架构 . . . . . . . . . . . . . . . . . 11-6

+ 配置服务器 . . . . . . . . . . . . . . . . . 11-14

+ 配置客户端 . . . . . . . . . . . . . . . . . 11-15

+ SSH 相关命令 . . . . . . . . . . . . . . . 11-16

## 引言

SUSE Linux Enterprise Server 10 管理（课程 3072）侧重于日常管理。本课程涵盖了系统管理员经常执行的任务，如系统的安装、配置和维护。这些技能与 SUSE Linux Enterprise Server 基础（课程 3071）和 SUSE Linux Enterprise Server 高级管理（课程 3073）中的知识相结合，将帮助你准备 Novell CLP 10 认证。

你的学生包包含以下内容：

- SUSE Linux Enterprise Server 10 手册
- SUSE Linux Enterprise Server 10 练习册
- SUSE Linux Enterprise Server 10 课程 DVD
- SUSE LINUX Enterprise Server 10 产品 DVD
- SUSE LINUX Enterprise Desktop 10 产品 DVD

SUSE Linux Enterprise Server 10 课程 DVD 包含一个 SUSE Linux Enterprise Server 安装镜像，你可以结合 SUSE Linux Enterprise Server 练习册在课堂外进行练习。设置自学环境的说明位于 DVD 上的 `setup` 目录。

## 课程目标

本课程不仅教授理论知识，还通过实际实验对以下 CLP 10 主题进行应用：

- 安装 SUSE Linux Enterprise Server
- 管理 Linux 文件系统
- 管理用户访问和安全
- 手动配置网络
- 管理 Linux 进程和服务程序
- 监控 SUSE Linux Enterprise Server
- 配置系统初始化
- 管理 SUSE Linux Enterprise Server 软件
- 管理备份和恢复
- 管理打印
- 配置远程访问

这些是企业环境中 SUSE Linux 管理员经常需要处理的任务。

以下内容说明了 Novell CLP 10 的培训和测试路径：

![](img/84d12236ddfe17cc29fd21173b9904ac_15_0.png)

有关 Novell 认证计划以及参加 Novell CLP 10 和 CLE 10 实践考试的更多信息，请访问 http://www.novell.com/training/certinfo/，http://www.novell.com/training/certinfo/clp10 以及 http://www.novell.com/training/certinfo/cle10。

在参加此课程之前，您应该参加过以下课程：

- SUSE Linux Enterprise Server 10 Fundamentals (课程 3071)

## SUSE Linux Enterprise Server 10 支持与维护

您在学生包中收到的 SUSE Linux Enterprise Server 10 副本是 SUSE Linux Enterprise Server 10 完整功能副本。

然而，为了获得官方支持和维护更新，您需要执行以下操作之一：

- 注册免费的序列号，该代码将为您提供 30 天的支持和维护。
- 从 Novell（或授权经销商）购买一份 SUSE Linux Enterprise Server 10 副本。

您可以在 http://www.novell.com/products/linuxenterpriseserver/ 获取免费的 30 天支持与维护代码。

您需要拥有或创建一个 Novell 登录账户以访问 30 天评估版。

## Novell 用户中心

Novell Customer Center 是一个直观的基于 Web 的界面，帮助您管理与 Novell 的业务技术交互。Novell Customer Center 整合了对信息、工具和服务的访问，例如：

- 新 SUSE Linux Enterprise 产品的自动注册
- Novell 发出的所有 Linux 产品的补丁和更新
- 所有 Novell 产品、订阅和服务的订单历史
- 新 SUSE Linux Enterprise 产品的权限范围可见性
- Linux 订阅续订状态
- 通过合作伙伴或 Novell 进行订阅续订

例如，一个公司可能有一个需要下载 SUSE Linux Enterprise 软件更新的管理员，一个想要查看订单历史的购买者，以及一个必须核对许可的 IT 经理。通过 Novell Customer Center，公司可以在一个位置满足所有需求，并为每个用户提供与其角色相应的访问权限。

您可以通过 http://www.novell.com/center Novell Customer Center。

## SUSE Linux Enterprise Server 10 在线资源

Novell 提供多种在线资源来帮助您配置和实施 SUSE Linux Enterprise Server 10。

这些包括：

- http://www.novell.com/products/linuxenterpriseserver/

  这是 SUSE Linux Enterprise Server 的 Novell 主页。
- http://www.novell.com/documentation/sles10/index.html

  这是 SLES 10 的 Novell 文档网站。
- http://support.novell.com/linux/

  这是所有 Novell Linux 支持的主页，包含指向知识库、下载和常见问题（FAQs）等支持选项的链接。
- http://www.novell.com/coolsolutions/

  该 Novell 网站提供了 Novell 对各种产品（包括 SUSE Linux）的最新实施指南和建议。

## 议程

以下是此 5 天课程的议程：

表格Intro-1

| 天数 | 章节 | 时长 |
| --- | --- | --- |
| 第 1 天 | 简介 | 00:30 |
| | 节 1：安装 SUSE Linux Enterprise Server 10 | 02:30 |
| | 节 2：管理 Linux 文件系统 | 03:00 |
| 第 2 天 | 节 2：管理 Linux 文件系统（续） | 01:00 |
