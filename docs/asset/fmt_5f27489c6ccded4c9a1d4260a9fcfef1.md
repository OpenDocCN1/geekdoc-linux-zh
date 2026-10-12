
- 首先瞄准容易摘取的果实...将任何困难的项目留到以后

- 一些服务可能无法优雅迁移，特别是

    - 如果您并不完全了解当前的服务器/服务

    - 当某些依赖项或服务可能不存在于 Linux 或特定发行版中时。

- 对于某些服务，暂时或永久保留在原处可能是最好的

- 不要试图一口吃成胖子...记住，目标是保留服务和可靠性

### 图 B-19

### 迁移计划概述

- 规划

- 准备

- 实施/迁移

- 迁移后

### 图 B-20

![](img/63e88022bf135307e3eac051ad238b5b_479_0.png)

### 图 B-21

![](img/63e88022bf135307e3eac051ad238b5b_479_1.png)

![](img/63e88022bf135307e3eac051ad238b5b_480_0.png)

![](img/63e88022bf135307e3eac051ad238b5b_480_1.png)

允许硬拷贝 - 禁止分发

### 图 B-24

![](img/63e88022bf135307e3eac051ad238b5b_481_0.png)

### 图 B-25

![](img/63e88022bf135307e3eac051ad238b5b_481_1.png)

### 图 B-26

![](img/63e88022bf135307e3eac051ad238b5b_482_0.png)

### 图 B-27

![](img/63e88022bf135307e3eac051ad238b5b_482_1.png)

### 图 B-28

![](img/63e88022bf135307e3eac051ad238b5b_483_0.png)

### 图 B-29

![](img/63e88022bf135307e3eac051ad238b5b_483_1.png)

![](img/63e88022bf135307e3eac051ad238b5b_484_0.png)

![](img/63e88022bf135307e3eac051ad238b5b_484_1.png)

### 图 B-32

![](img/63e88022bf135307e3eac051ad238b5b_485_0.png)

### 图 B-33

![](img/63e88022bf135307e3eac051ad238b5b_485_1.png)

### 图 B-34

![](img/63e88022bf135307e3eac051ad238b5b_486_0.png)

### 图 B-35

![](img/63e88022bf135307e3eac051ad238b5b_486_1.png)

允许硬拷贝 - 禁止分发

### 图 B-36

![](img/63e88022bf135307e3eac051ad238b5b_487_0.png)

### 图 B-37

![](img/63e88022bf135307e3eac051ad238b5b_487_1.png)

允许硬拷贝 - 禁止分发

### 附录：将服务从 RedHat 迁移到 SUSE Linux Enterprise Server 10

![](img/63e88022bf135307e3eac051ad238b5b_488_0.png)

![](img/63e88022bf135307e3eac051ad238b5b_488_1.png)

允许硬拷贝 - 禁止分发

### 图 B-40

### 打印服务

文件/文件位置：

- **启动脚本** `/etc/init.d/cups`

- **配置文件** `/etc/cups/*`

配置（GUI/CUI）：

- **RH/EL/Fedora:** system-config-printer

- **SLES/SUSE:** `yast (硬件 → 打印机)`

    `yast printer`

备注：

- *两个发行版都使用 cups；如有需要可加载 LPing*

- *较旧版本的 RH 可能正在使用 LPRng*

### 图 B-41

### 电子邮件（postfix/sendmail）

文件/文件位置：

- **启动脚本** `/etc/init.d/postfix`

- **配置文件** `/etc/postfix/*`

- **邮件队列** `/var/spool/postfix`

配置（GUI/CUI）：

- **RH/EL/Fedora:** system-config-mail

- **SLES/SUSE:** `yast (网络服务 → 邮件传输代理)`

    `yast mail`

备注：

- *SUSE 默认运行 postfix；如有需要可加载 sendmail*

- *测试，测试，测试（特别是如果从 sendmail 更改为 postfix）*

## 图 B-42

![](img/63e88022bf135307e3eac051ad238b5b_490_0.png)

## 图 B-43

![](img/63e88022bf135307e3eac051ad238b5b_490_1.png)

## 图 B-44

![](img/63e88022bf135307e3eac051ad238b5b_491_0.png)

## 图 B-45

![](img/63e88022bf135307e3eac051ad238b5b_491_1.png)

# 第 C 部分 附录：Red Hat 用户使用 SUSE Linux Enterprise Server 指南

本指南撰写于 2005 年，重点介绍 SUSE Linux Enterprise Server 9。本指南中的某些信息不适用于 SUSE Linux Enterprise Server 10，但大部分内容仍然有效。

1 允许硬拷贝 - 禁止分发

## 图 C-1

![](img/63e88022bf135307e3eac051ad238b5b_493_0.png)

## 图 C-2

![](img/63e88022bf135307e3eac051ad238b5b_494_0.png)

1 允许硬拷贝 - 禁止分发

## 图 C-3

概览...5  
受众...5  
Red Hat Enterprise Linux...5  
Novell Enterprise Linux...5  
涵盖的主题...6  
安装...6  
自动安装概览...6  
安装模式...9  
引导过程与运行级别...11  
引导加载器差异...11  
Init 脚本...11  
SUSE Linux Enterprise Server 引导过程...12  
Init 和运行级别...13  
SUSE Linux Enterprise Server 引导选项...13  
服务与守护进程...15  
网络配置...18  
用户管理和环境...18  
命令行用户管理...18  
图形化用户管理...19  
用户环境...20  
系统管理...21  
SuSEconfig——规范化工具...21  
YaST：图形界面版本...21  
YaST——文本模式版本...22  
YaST——文本模式版本...23  
比较系统管理工具...23  
服务与支持包 vs. Red Hat 更新...24  
启用 Red Hat Network 支持...25  
启用 SUSE Linux Enterprise Server 支持...25

## 图 C-4

![](img/63e88022bf135307e3eac051ad238b5b_496_0.png)

1 允许硬拷贝 - 禁止分发

## 图 C-5

## 概览

本白皮书旨在协助那些需要用 SUSE™ Linux Enterprise Server 替换其 Red Hat® Enterprise Linux 服务器的 IT 管理员。由 Novell® 分发的 SUSE Linux Enterprise Server 通过提供可扩展、高性能的基础设施，帮助企业利用 IT 和开源技术，实现安全的计算环境。本白皮书涵盖了将 SUSE Linux Enterprise Server 集成到现有 IT 环境中的技术需求，特别强调了用 SUSE Linux Enterprise Server 系统替换遗留的 Red Hat Linux 系统。

Red Hat 和 SUSE Linux 发行版在重点和范围上相似。然而，两者之间存在足够的差异，除非成功建立映射关系，以便系统管理员了解两个发行版将相同的配置文件存储在何处或如何执行相同的任务，否则任何集成或迁移都会令人感到沮丧。

## 受众
