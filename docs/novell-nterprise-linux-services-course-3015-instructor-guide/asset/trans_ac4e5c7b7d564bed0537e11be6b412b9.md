
## 默认 NetStorage 访问

NetStorage 网页显示网络文件和文件夹。

以下示例展示了可以从 NetStorage 网页默认访问的文件夹：

**图 6-17**

![](img/d63035f3fce0eaaf97203dde900affb7_106_0.png)

如图 6-17 所示的**共享**（shared）文件夹是 NetStorage 的一个默认位置，所有用户都可以访问该位置以上传或下载文件。用户无需启用 Samba 即可访问此文件夹。

NetStorage 自动配置为允许所有 eDirectory 用户访问 NNLS 服务器上的**共享**（shared）文件夹。该文件夹的路径为：

/var/opt/novell/netstorage/shared

## 额外配置的 NetStorage 访问

您可以创建仅允许特定用户访问的文件夹。通过创建指向 Linux 和 NetWare 服务器上文件夹的存储位置（Storage Location）对象来实现此目的。

用户可能被授予 NNLS 服务器上某些文件夹的 Linux 文件系统权限，但如果未满足以下条件，他们将无法通过 NetStorage 访问这些文件夹：

- 该用户已启用 Samba。
- 对于您专门为 NetStorage 用户创建的文件夹，必须在 smb.conf 文件中将其配置为 Samba 共享。
- 对于用户的主目录，它们默认已配置为 Samba 共享。但如果您想让用户通过 NetStorage 访问主目录，必须以 LUM 用户身份登录来创建该主目录。
- 已创建存储位置（Storage Location）对象，并配置其指向相应的 Samba 共享。
- 用户被分配了存储位置对象的权限。这可以在单个用户级别完成，也可以通过组、容器或其他类似的分配方式完成。

以下示例展示了已配置为可从 NetStorage 网页访问的额外文件夹：

图 6-18

![](img/d63035f3fce0eaaf97203dde900affb7_107_0.png)

## 目标 6    安装和配置 NetStorage

要安装和配置 NetStorage，您需要了解以下内容：

- 安装 NetStorage 的步骤
- 创建存储位置对象和列表
- 配置 NetStorage
- 访问 NetStorage 文件和文件夹

### 安装 NetStorage 的步骤

安装 iFolder 的一般步骤如下：

- 满足 NetStorage 依赖项
- 收集所需信息
- 使用 NNLS 安装功能

#### 满足 NetStorage 依赖项

NetStorage 随 Virtual Office 一起安装。Virtual Office 的依赖项包括：

- 同一 NNLS 服务器上的 Apache 2.0.45
- 同一 NNLS 服务器上的 JVM 1.4.1_02
- 同一 NNLS 服务器上的 Tomcat 4.1.24
- 网络中任意位置的 eDirectory 8.7.1 或更高版本
- 同一 NNLS 服务器上的 iManager 2.0

当您选择 Virtual Office 组件时，NNLS 安装程序将选择所需的组件及其依赖项。它们将在同一过程中全部安装。

有关成功安装尚未安装的 Virtual Office 依赖项所需的信息，请参见表 2-5。

对于大多数网络，您只需在一台服务器上安装 NetStorage；不过，这可能会根据规模和组织的需求而变化。

例如，如果您的公司在地理位置上分散，您可能希望在每个地理区域的一台服务器上安装 NetStorage。

#### 收集所需信息

下表描述了安装 Virtual Office 期间请求的 NetStorage 信息：

表 6-5

| 所需的配置数据 | 描述 |
| :--- | :--- |
| NetStorage 身份验证服务器 | 使用 LDAP 进行 NetStorage 用户身份验证的 eDirectory 服务器的 IP 地址或 DNS 主机名。 |
| NetStorage 代理用户 | 具有执行以下操作权限的用户对象的完全限定名称：<br>• 在指定为 NetStorage 身份验证服务器的 LDAP (eDirectory) 树中搜索 NetStorage 用户<br>• 在 NetStorage 中定义了 iFolder 存储位置的情况下，在用户首次访问存储位置时，在 eDirectory 中存储 iFolder 用户密码短语 |
| NetStorage 代理用户密码 | 指定为 NetStorage 代理用户的用户的密码。 |
| NetStorage 用户上下文 | 要搜索 NetStorage 用户的 NetStorage 身份验证服务器上的上下文。 <br> （所有子上下文也会被搜索。） |
| iFolder 服务器 IP 地址或主机名 | （可选）指定要在 NetStorage 中作为存储位置创建的 iFolder 服务器的 IP 地址或主机名。这使 iFolder 自动对 Virtual Office 用户可用。 |

#### 使用 NNLS 安装功能

要从 NNLS 安装 NetStorage（作为 Virtual Office 安装的一部分），请执行以下操作：

1. 执行自定义安装的步骤。
    > 如有必要，请参见第 2 节了解如何进行自定义安装的详细信息。
2. 取消选中*不想*安装的服务，选中**Virtual Office** 服务，然后继续。
    如果之前未安装 eDirectory，请注意，当您选择 Virtual Office 时，eDirectory 默认已选中（连同其他必需组件，如 Apache 和 Tomcat）。
    
    如果之前已安装 eDirectory，安装程序将指示哪些组件已安装。
3. 接受许可协议。
4. **（条件）** 如果提示输入 NICI Foundation Key (NFK) 文件的位置，请插入许可软盘并输入 NFK 文件的路径。
    只有当之前未安装 eDirectory 时，才会提示输入 NICI Foundation Key。
5. 在每次提示处输入所需信息（参见表 6-5）。
6. 查看摘要信息并进行必要的更正。
7. 当所有信息正确时，完成安装。
8. 查看 readme 文件并保存安装设置日志文件。

## 创建存储位置对象和列表

安装 NetStorage 后，您可能只能使用 NetStorage 看到 Linux 服务器上的 iFolder 目录和一个本地共享目录。

访问 Linux 服务器上的文件和目录需要存储位置对象，也可以用于 NetWare 服务器。

用户可能对网络上的某些文件和文件夹具有特定的 eDirectory 权限，但如果未创建存储位置对象，他们将无法使用 NetStorage 访问这些文件和文件夹。

要授予用户文件访问权限，您需要知道如何执行以下操作：

- 创建存储位置对象
- 创建存储位置列表

### 创建存储位置对象

要创建存储位置对象，请执行以下操作：

1. 启动浏览器，输入以下内容以启动 iManager：
    - https://IP_or_DNS/nps/iManager
2. 输入您的*用户名*和*密码*登录。
3. 在左侧的**文件访问 (NetStorage)**下，选择**存储位置：创建**。

将显示以下内容：

![](img/d63035f3fce0eaaf97203dde900affb7_112_0.png)

4. 输入以下内容：
    - **对象名称**：eDirectory 中对象的名称。
    - **显示名称**：在 NetStorage 目录访问列表中显示的名称。
      这是快捷名称，用户可以看到它。如果您为两个不同的存储对象使用相同的显示名称，名称中会添加数字以使每个名称唯一。
    - **目录位置**：目录在文件系统上的位置。该位置是一个 URL，包括文件系统类型、服务器名称、卷和目录路径。
      如果要访问的存储位于 NetWare 服务器上，URL 必须采用以下格式：
      `ncp://server_name/volume/path_to_directory`
      例如：
      `ncp://server1.digitaalair.com/mkgt/reports`
      *或*
      `ncp://111.222.3.4/mkgt/reports`
      如果要访问的存储位于 Linux 服务器上，URL 必须采用以下格式：
      `cifs://server_name/cifs_share_name`
      如果省略文件系统，则假设其为 NCP。
    - **上下文**：存储位置对象所在的目录上下文。
      您可以选择对象选择器图标来浏览并选择上下文。
    - **注释**：仅供管理员使用；不会显示给用户。
5. 完成后，选择**创建**；然后选择**确定**。

### 创建存储位置列表

创建存储位置对象后，必须创建一个存储位置对象列表，该列表可用于指定的用户、组、配置文件或容器对象。

用户下次登录时将看到与该对象关联的目录。创建此列表后，您可以从同一窗口通过向列表分配额外的存储位置对象或从列表中删除存储位置对象来修改该列表。

