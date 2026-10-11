

## 6. 系统监控与管理
- 监控 CPU 资源
- `uptime` 命令和 `/etc/loadavg` 文件
- `top` 命令
- `atop` 和 `htop` 命令
- `mpstat` 命令
- `sar` 命令
- `iostat` 命令
- 监控内存资源
- `vmstat` 命令
- `top`、`htop` 和 `atop` 命令
- `sar` 命令
- 每个进程的内存使用情况
- 内存不足管理
- 监控磁盘使用情况和可用空间
- `iostat` 命令
- `iotop` 命令
- `atop` 命令
- `smartctl` 命令
- `fio` 和 `hdparm` 命令
- `df` 命令和 LVM 命令
- 监控网络资源
- `ethtool` 命令
- `nmon` 命令
- `traceroute`、`tracpath` 和 `mtr` 命令
- 配额和限制
- 配额
- 限制
- 结论
- 关键事实
- 问题
- 答案

## 7. 网络配置
- 引言
- 结构
- 网络简介
  - 物理层（第 1 层）
  - 数据链路层（第 2 层）
  - 网络层（第 3 层）
  - 传输层（第 4 层）
  - 会话层、表示层和应用层（第 5、6 和 7 层）
- 基本网络配置
  - 基于 Red Hat 系统的网络配置
    - `nmcli` 命令
    - `nmtui` 命令
  - Debian 和 Ubuntu 上的网络配置
- 路由
- 高级网络配置
  - 链路聚合（绑定）
  - 网桥
  - 虚拟局域网（VLAN）
- 结论
- 关键事实
- 问题
- 答案

## 8. 安全性
- 引言
- 结构
- 安全简介
- Linux 上的防火墙配置
  - Firewalld
  - ufw
  - 伪装
- 服务安全
  - 禁用不需要的服务
  - 列出在所有接口上监听的服务
  - 服务日志记录
  - 入侵检测系统
  - 安全模型
- 网络监控
- 结论
- 关键事实
- 问题
- 答案

## 9. 网络服务
- 引言
- 结构
- DHCP 服务和客户端
  - Linux DHCP 服务器和客户端
- DNS 服务和客户端
  - Linux DNS 服务器和客户端
- SSH 服务和 SSH 客户端
  - SSH 公钥和私钥
- 检查可用的网络服务
- 其他流行的网络服务
- 结论
- 关键事实
- 问题
- 答案

## 10. 文件共享
- 引言
- 结构
- NFS 服务和客户端
  - NFS 服务器
  - NFS 客户端
- SMB 简介
- Samba 服务器和客户端
  - Samba 服务器
  - Samba 客户端
- FTP 服务器和客户端
- TFTP 简介
- 结论
- 关键事实
- 问题
- 答案

## 11. 数据库
- 引言
- 结构
- 关系型数据库
- 结构化查询语言 (SQL)
  - CREATE 语句
  - DROP 语句
  - ALTER 语句
  - INSERT 语句
  - SELECT 语句
  - UPDATE 语句
  - DELETE 语句
  - GRANT 语句
  - REVOKE 语句
- MariaDB 服务器
  - MariaDB 客户端和任务
- SQLite
- NoSQL 数据库
- MongoDB 数据库
- MongoDB 客户端和任务
- 结论
- 关键事实
- 问题
- 答案

## 12. 自动化
- 引言
- 结构
- IT 自动化简介
- 使用 shell 脚本进行自动化
- 使用 Python 进行自动化
- 使用 Ansible 进行自动化
  - 清单 (Inventory)
  - AD-HOC 操作
  - YAML
  - Ansible 配置
  - Playbook
  - 变量
  - 变量优先级
  - 处理器 (Handlers)
  - 包含 (Include) 和导入 (Import)
  - 事实 (Facts) 和魔术变量 (Magic variables)
  - 条件语句
  - 循环
  - 注册 (Register)
  - 模板 (Templates)
  - 代码块 (Blocks)
  - 流行模块列表
  - 角色 (Roles)
  - 集合 (Collections)
  - Ansible Galaxy
- 结论
- 关键事实
- 问题
- 答案

## 13. 容器和 CI/CD
- 引言
- 结构
- 容器和镜像简介
- 容器与虚拟化
- 容器内容
- 镜像
- 镜像仓库
- Docker
  - 运行第一个容器
  - 获取客户端和服务器信息
  - 操作容器
    - 暴露容器
    - 容器操作
    - Docker 服务器统计和事件
  - 镜像仓库
- Podman
- 容器运行时
- Kubernetes
- 持续集成/交付简介
- Jenkins、Gitlab CI/CD 和 Github Actions
  - Jenkins
  - Gitlab CI/CD
  - GitHub Actions
- 结论
- 关键事实
- 问题
- 答案

## 14. 备份与恢复
- 引言
- 结构
- 备份与恢复简介
- 备份存储介质
- 备份类型
- 备份源
- 备份策略
- 备份解决方案功能
- Bacula
  - Bacula 安装
  - Bacula 服务
  - 客户端安装
  - `bconsole` 命令
- Relax-and-Recover (ReaR)
- 结论
- 关键事实
- 问题
- 答案

## 15. 多云管理
- 引言
- 结构
- 云提供商简介
  - 优势
- 云服务
  - 亚马逊网络服务 (AWS)
  - 微软 Azure
  - 谷歌云平台
  - 阿里云
  - OpenStack
- 多云管理
- 基础设施即代码
- Terraform
  - 安装
  - 在 AWS 上运行简单的 Web 服务器
  - 在谷歌云平台上运行简单的 Web 服务器
  - 在微软 Azure 上运行简单的 Web 服务器
  - 使用 Cloudflare 配置 DNS
- 结论
- 关键事实
- 问题
- 答案

## 16. 基础设施即服务
- 引言
- 结构
- 基础设施即服务 (IaaS)
- 私有云
- 混合云
- 作为 IaaS 的 OpenStack
- 在 OpenStack 上运行虚拟机
  - 镜像
  - 规格 (Flavors)
  - 网络架构
  - 虚拟机网络
  - 路由
  - 安全组
  - 公钥
  - 虚拟机
  - 浮动 IP
  - 持久化存储
  - 编排
  - 仪表板
- 结论
- 关键事实
- 问题
- 答案

## 索引

# 第 1 章
## Linux 简介

## 引言
2021 年 8 月 25 日，Linux 庆祝了自 Linus Torvalds 发布关于他设计的新操作系统的消息以来 30 周年。在这三十年中，IT 行业经历了巨大的进步和变化。Linux 成为并巩固了行业中最重要的操作系统地位。

在本章中，我们将描述 Linux 对公司为何至关重要、其最新功能以及使用案例。

## 结构
在本章中，我们将讨论以下主题：
- Linux 的地位
- Linux 在 IT 行业主要部门的应用
  - 软件
  - 设备和基础设施
  - 信息技术和商业服务
  - 新兴技术
  - 电信服务
- Linux 的最新功能
- Linux 与其他操作系统的比较
- Linux 光明的未来

## Linux 的地位
如今，没有连接到互联网的设备（如手机、平板电脑或个人电脑），我们就无法理解我们的日常生活，无论是访问 Web 服务器还是使用应用程序阅读电子邮件、在搜索引擎（如 Google）中查找信息，或购买您需要的产品。

手机和平板电脑最常见的操作系统是 Android，它是 Linux 的一个变体。人们日常使用的流行服务，如邮件服务器或 Web 服务器，几乎都运行在 Linux 发行版系统上。为这些服务提供互联网访问的其他设备通常也运行 Linux。

大量专业开发人员、IT 专业人士和普通用户也将 Linux 作为其主要操作系统。Linux 目前是桌面环境中第三受欢迎的操作系统。

Linux 始于 1991 年 Linus Torvalds 的个人项目。开发工作是在 MINIX（一种类 Unix 操作系统）上完成的。第二年，X 窗口系统被移植到 Linux 上，帮助其获得重要地位。以下是对重要版本发布的简要时间线：
- 第一个稳定版本于 1994 年发布。
- 2.0 版本于 1996 年发布。
- 2.2 版本于 1999 年发布，2.4 版本于 2001 年发布，2.6 版本于 2003 年发布。
- 3.0 版本于 2011 年发布。
- 4.0 版本于 2015 年发布，5.0 版本于 2019 年发布，6.0 版本于 2022 年发布。

历史上其他与 Linux 相关的重要事件如下：
- Debian 始于 1993 年。
- Red Hat Linux 于 1994 年发布。
- Ubuntu 于 2004 年发布。
- Android 1.0 版本于 2008 年发布。
- 自 2017 年起，全球最快 500 台超级计算机名单（Top500）中的所有机器都运行 Linux。

## Linux 在 IT 行业主要部门的应用

