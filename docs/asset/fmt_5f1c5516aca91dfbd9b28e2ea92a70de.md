
在当今互联的世界中，电子邮件是通信与协作的核心支柱。本章将引导我们如何在 Rocky Linux 9 上配置一个安全、可靠且可扩展的邮件服务器，并对早期版本的兼容性进行说明。通过使用 Postfix，我们将获得管理邮件域、用户和基本配置的实践经验。为了便于理解和故障排除，我们提供了如 `postfix check`、`mailq`、`tail -f /var/log/mailog` 和 `firewall-cmd` 等命令的预期输出。配置注释强调了防火墙规则和虚拟主机等关键领域，而 SSL 证书设置则通过实用的分步指导进行了简化。SPF/DKIM 的实现和 AWS SES 策略与最新的安全标准对齐，以确保邮件身份验证和投递。

除了本地部署外，本章还介绍了使用 AWS 简单邮件服务 (SES) 进行高级云集成，演示了如何构建可扩展且具弹性的电子邮件基础设施。视觉图表说明了 EC2 实例、负载均衡器和自动伸缩组在动态管理流量之间的交互。本章还涉及了 Apache 和 MySQL 的基本性能调优策略。无论作为 Linux 管理员还是开发者，读者都将获得在 Rocky Linux 上构建企业级电子邮件系统的实用见解——既适用于本地环境，也适用于云平台。

## 结构

本章涵盖了以下主题：

字体 邮件服务器的设置、配置以及与 AWS服务的集成

- 安装和配置 Postfix
- 管理邮件域和用户
- 基础邮件服务器安全
- 监控与故障排除
- 集成 AWS SES 实现可扩展的邮件管理

# 邮件服务器的设置、配置以及与 AWS 集成

电子邮件是现代通信的骨干，驱动着从业务信函到自动通知的一切功能。对于系统管理员来说，掌握配置和管理邮件服务器的艺术不仅是技术上的需要，更是确保组织间无缝通信的门户。在本章中，我们将深入探讨在 Rocky Linux 上使用 Postfix 设置和管理邮件服务器的细节，Rocky Linux 是一个强大且多功能的平台，能够精确可靠地处理电子邮件投递。

除了传统的设置外，我们还将探索如何通过与 AWS 简单邮件服务 (SES) 集成来增强邮件服务器的能力。这项强大的云服务允许我们利用 AWS 的扩展性、安全性和成本效益来大规模发送和接收电子邮件。从配置邮件域和管理用户，到实现基本的安全功能和故障排除，本章提供了一个构建安全、可扩展且支持云的电子邮件解决方案的分步指南。

## 实验 1：在 AWS IAM Identity Center 中创建用户和组

先决条件

- 管理员访问：确保我们在 AWS 中拥有管理员权限。
- 已启用 IAM Identity Center：验证我们的 AWS 账户已启用 AWS IAM Identity Center（以前称为 AWS SSO）。

第 1 步：访问 AWS IAM Identity Center

a. 登录 AWS 管理控制台。
b. 导航到 IAM Identity Center。
c. 在 AWS 管理控制台中，在搜索栏中搜索 IAM Identity Center 并选择它。

第 2 步：添加用户

a. 在左侧菜单中，选择“用户 (Users)”。
b. 点击“添加用户 (Add User)”按钮。
c. 填写详细信息：
**名字 (First Name)：输入用户的名字。**
**姓 (Last Name)：输入用户的姓。**
**电子邮件 (Email)：输入用户的邮箱地址（例如，user@example.com）。**
**用户名 (Username)：输入用户名（这可以是邮箱地址或另一个唯一名称）。**
**临时密码 (Temporary Password)：提供一个临时密码（用户将在首次登录时进行重置）。**
（可选）为用户添加标签以便更好地组织。
**点击“添加用户 (Add User)”完成此过程。** 为每个需要的邮箱地址重复此过程。

第 3 步：创建组

a. 在左侧菜单中，选择“组 (Groups)”。
b. 点击“创建组 (Create Group)”按钮。
c. 输入组名称 (Group Name)（例如，Admins, Developers, Finance Team）。
d. （可选）添加描述以解释该组的作用。
e. 点击“创建组 (Create Group)”完成操作。

第 4 步：将用户分配到组

a. 导航到“组 (Groups)”部分。
b. 选择我们想要添加用户的某个组。
c. 点击“添加用户 (Add Users)”。
d. 从列表中选择我们之前创建的用户。
e. 点击“添加 (Add)”将他们分配到该组。

第 5 步：为组分配权限

a. 在左侧菜单中，转到“权限集 (Permission Sets)”。
b. 权限集定义了用户和组的访问策略。
c. 创建一个新的权限集或使用现有的：
d. 点击“创建权限集 (Create Permission Set)”并选择预定义的策略（例如，AdministratorAccess, PowerUserAccess）或创建自定义策略。
e. 将权限集分配给组。
f. 导航到“分配 (Assignments)”并点击“分配用户或组 (Assign Users or Groups)”。
g. 选择组和相应的权限集，然后点击“分配 (Assign)”。

第 6 步：验证并共享登录详情

a. 找到 IAM Identity Center 用户门户 URL：
b. 该 URL 可以在“仪表板 (Dashboard)”选项卡下的“用户门户 URL (User portal URL)”下找到。
c. 示例：https://<our-aws-sso-domain>.awsapps.com/start。
d. 与用户共享登录详情：
e. 电子邮件：他们的注册邮箱地址。
f. 临时密码：创建期间提供的密码。
g. 指导用户登录、重置密码并开始使用他们分配的权限。

## 示例邮箱地址

如果我们正在创建 alice@example.com; bob@example.com; charlie@example.com;

a. alice@example.com; bob@example.com; charlie@example.com;
b. 在第 2 步中添加它们。
c. 在第 4 步中分配它们。

## 实验 2：在 IAM Identity Center 中设置和管理用户与组

目标：通过完成此实验，学习如何：

1. 在 IAM Identity Center 中创建用户和组。
2. 将用户分配到组。
3. 为组应用权限。

先决条件

- 具有管理员权限的 AWS 管理控制台访问。
- 账户已启用 IAM Identity Center。

实验步骤

第 1 步：创建用户

a. 登录 AWS 管理控制台。
b. 搜索进入 IAM Identity Center。
c. 点击左侧菜单中的“用户 (Users)”。
d. 点击“添加用户 (Add User)”并填写以下信息（至少两个用户）：
名字：Alice
姓：Smith
电子邮件：alice@example.com
用户名：alice@example.com
临时密码：设置一个 Alice 在首次登录时将更新的密码。
e. 点击“添加用户 (Add User)”保存。
f. 重复步骤创建另一个用户，例如 bob@example.com。

第 2 步：创建组

a. 在 Identity Center 菜单中选择“组 (Groups)”。
b. 点击“创建组 (Create Group)”并命名，例如，Developers。
c. 添加描述，如“开发团队成员的组”。
d. 点击“创建组 (Create Group)”保存。

第 3 步：将用户分配到组

a. 回到“组 (Groups)”并选择 Developers 组。
b. 点击“添加用户 (Add Users)”并选择我们创建的用户（Alice 和 Bob）。
c. 点击“添加 (Add)”确认。

第 4 步：为组分配权限

a. 点击左侧菜单中的“权限集 (Permission Sets)”。
b. 创建一个新的权限集或使用现有的：
i. 点击“创建权限集 (Create Permission Set)”。
ii. 选择策略，如 PowerUserAccess。
iii. 点击“创建 (Create)”完成。
c. 将权限集分配给 Developers 组：
i. 转到“分配 (Assignments)”。
ii. 点击“分配用户或组 (Assign Users or Groups)”。
iii. 选择 Developers 组和权限集，然后点击“分配 (Assign)”。

第 5 步：验证访问

a. 从“仪表板 (Dashboard)”选项卡中找到 IAM Identity Center 用户门户 URL。
b. 与用户共享以下详情：
- 用户门户 URL。
- 他们的邮箱地址和临时密码。
c. 让用户登录门户、重置密码，并验证他们是否可以根据权限访问 AWS 服务。

### 挑战任务（可选）
