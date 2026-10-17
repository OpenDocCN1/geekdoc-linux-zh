
$ git clone https://github.com/iknowjason/PurpleCloud

--OMMITTED FOR BREVITY-----

kali@kali: -]

$ cd PurpleCloud/deploy

kali@kali: -~/PurpleCloud/deploy]

$ cp terraform.tfexample terraform.tfvars:

kali@kali: -~/PurpleCloud/deploy]

nano terraform.tfvars

```

![](img/0add480ffb73b6bc89b65d99f7d6b37a_971_0.png)

第一步是克隆 `PurpleCloud` 仓库 1。该仓库本身在 `deploy` 目录下有许多 `Terraform` 脚本 2。一旦进入该目录，你需要将 `terraform.tfexample` 文件移动并重命名为 `terraform.tfvars` 3。接下来，你需要编辑该文件并更改若干设置 4。

以下是你需要在 `tfexample` 文件中更改的相关区域：

```text

armarm_client_id = "REPLACE_WITH_YOUR_VALUES"

arm_client_secret = "REPLACE_WITH_YOUR_VALUES"

subscription_id = "REPLACE_WITH_YOUR_VALUES"

tenant_id = "REPLACE_WITH_YOUR_VALUES"

```

为你提供的图片显示了你如何使用 Azure 端口获取这些值 5。如果你选择 Azure 端口，可以通过选择 Azure Active Directory | 注册应用程序（App Registrations）然后点击你的应用程序（见图 28-2）。

一旦配置文件中填充了这些值，你就可以在文件中找到填充这些项目的值。你需要生成一个客户端密钥（client secret），它可以在应用程序的证书和密钥（Certificates and Secrets）区域找到。你在这个文件中也有编辑 `src_ip` 的选项，以锁定对暴露系统的访问。

运行 `terraform` 命令来构建系统。

```bash

(kali@kali)- -[PurpleCloud/deploy]

$ terraform init apply -var-file=terraform.tfvars

```

通过在 `Terraform` 中指定 `var-file`，你可以进行部署。这将需要几分钟时间。注意我们将使用以下内容。

## 实验 28-2：额外步骤

现在我们已经设置了用户，我们需要为其中一台虚拟机分配系统分配的托管标识（system-assigned managed identity）。以下是需要遵循的步骤：

- 1. 在 Azure 端口中，点击由 `PurpleCloud` 创建的资源组。它命名为 `purplecloud-devops`。
- 2. 一旦列出资源，点击 `rtc-dc1`。在此区域，点击左侧设置区域中的标识（identity）项。

3. 将状态设置为“开启”（On）。您可能需要点击“保存”（Save）以继续。

4. 现在您将看到“Azure 角色分配”（Role Assignments）按钮。点击该按钮添加角色分配。

5. 您可能需要或不需要选择订阅；如果您有多个订阅，则需要从屏幕“范围”（scopes）区域的列表中选择订阅。选择您的订阅，然后选择您的角色为“贡献者”（Contributor）。

注意，这是一个相当高级的访问权限；此时，您应该已经将访问控制列表限制为仅限您的 IP 地址。如果还没有，请确保修改 `terraform.tfvars` 文件，然后重新运行 `Terraform` 以更新配置。

# 实验 28-3：验证访问权限

我们现在应该验证所有的机器都是可以的。为了做到这一点，我们需要使用管理员账户登录到我们的域控制器。本实验将引导您完成该过程，从获取域控制器的 IP 地址开始。

```
(kali)@~/

$ az vm list -o table -do

Name ResourceGroup PowerState Publics Fqdns Location Zones

rtc-dci0 PURPLECLOUD-DEVOPS1 VM running 40.78.2.188 westus

rtc-velhelik0 PURPLECLOUD-DEVOPS1 VM running 13.88.175.91 westus

Win10-Lars PURPLECLOUD-DEVOPS1 VM running 13.88.175.92 westus
```

我们首先使用 `az vm` 工具以表格格式 1 列出所有对象。在环境中，我们看到了三个虚拟机：一个域控制器 2，一个用户工作站 3 以及一个 SOC 服务器/ELK 服务器 4。工作站和域控制器可以通过 RDP 登录，而 SOC 服务器将可以通过 SSH 访问。为了实验的目的，我们将仅集中于 `rtc-dc1`。在示例中，显示的 IP 地址为 40.78.2.188，但您的地址会有所不同。

使用 RDP 访问 `rtc-dc1`，用户名 `rtc.local\rtcadmin`，密码为 `Password123`。如果您可以登录服务器，可以保持 RDP 会话打开或关闭。我们将在本章节稍后返回它。

# Microsoft Azure AD 概述

如您所注意到的，Active Directory 是 Azure 内部机制不可或缺的一部分。理解系统的架构非常重要，以便后续的实验能够清 Azure 与 Azure AD 之间的关系。Azure 是一个身份提供者（IdP）。具体而言，它利用了 OpenID Connect，这是一个构建在 OAuth 之上的框架。“进阶阅读”部分有指向 OAuth 2.0 的链接。

为什么我们看到许多企业运行 Azure？主要原因是 Office 365。许多 Office 365 用户来自本地环境，为了方便用户同步，Azure AD 用于信箱同步。Azure 本身使用一系列范围（scopes）来控制对资源的访问。控制是由范围设置的，而这些范围定义了 Azure 中的权限。正如表 28-1 所示，您将发现不同类型的身份服务之间存在许多差异。

| 特性 | Azure AD | Microsoft AD | 域服务 (Domain Services) |
| :--- | :--- | :--- | :--- |
| 托管类型 | 托管 (SaaS) | 本地，自托管 | 托管 (SaaS) |
| 登录类型 | 基于 Web、OAuth、SAML | LDAP 存储、Kerberos、NTLM | LDAP 存储、Kerberos、NTLM |
| 计算机管理 | N/A，使用 Intune (MDM) | 组策略 | 组策略 |
| 用户管理 | 平平化结构、基于范围 | 文件夹、基于 ACL、树形结构 | 文件夹、基于 ACL、树形结构 |
| 管理员账户/角色 | 全局管理员、计单管理员、贡献者 | 域管理员、企业管理员、备份管理员 | 备份管理员（允许域管理员、企业管理员、架构更改） |
| 组织和多租户 | 租户 (Tenants) | 森林和域 | 无森林、无域 |
| 同步选项 | 本地环境可以同步到 Azure AD | 可以将用户同步到 Azure AD，仅限连接器，仅同步对象 | 无法向外同步，从 Azure 获取输入 |

## Microsoft 身份服务比较

## Azure 权限

现在让我们来看 Azure 中的整体角色。例如，我们可以查看“虚拟机登录”（Virtual Machine Login）角色，这是 Azure 的内置角色。该角色的作用是什么？包含什么？以下是使用 JSON 作为系统输入构建该角色的示例：

```json

{

  "id": "/providers/Microsoft.Authorization/roleDefinitions/fb879df8-f326-4884-b1cf-06fad86be5",

  "properties": {

    "roleName": "Virtual Machine Login",

    "description": "在门户中查看虚拟机并作为普通用户登录。",

    "assignableScopes": [

      "/"

    ],

    "permissions": {

      "actions": [

        "Microsoft.Network/publicIPAddresses/read",

        "Microsoft.Network/virtualNetworks/read",

        "Microsoft.Network/loadBalancers/read",

        "Microsoft.Network/networkInterfaces/read",

        "Microsoft.Compute/virtualMachines/*/read",
