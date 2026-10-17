
在 Windows 上使用 OpenSSH 类似于（甚至等同于）在 Unix 上使用 OpenSSH。Windows 上的 OpenSSH 与 Unix 上的 OpenSSH 遵循相同的一般建议，特别是作为管理目的和授权系统用户目的的强有力解决方案。但在 Windows 上的 OpenSSH 中传输文件不是一个好主意，因为敏感操作系统文件和/或目录存在权限问题。即便如此，我需要提到的一点是将 `cygdrive` 用作 SFTP 根目录。为了指定 SSH 或 SFTP 子系统根目录的默认非目录，需要使用 `cygdrive` 术语。例如，如果在具有 C、D 和 E 驱动器的 Windows 操作系统上希望根目录为 `e:\`，那么您位于 `Program Files\OpenSSH\bin` 中的 `passwd` 文件将如下所示：

```
Administrator::/cygdrive/e:
```

虽然所有 SFTP 用户都被重定向到 `e:\` 卷（这可能是核心 SFTP 目录），但他们并未被限制在 `e:\` 内。这意味着，虽然用户的 SFTP shell 将从 `e:\` 开始，但如果他们通过 SFTP 客户端指定想要访问 `c:\`，只要他们具有相应的 NTFS 权限，他们将允许访问 `c:\`。这也是 OpenSSH 移植到 Windows 的作者强调它仅应用于管理目的的原因之一，因为文件系统安全不是由 OpenSSH SFTP 子系统强制执行的，而是由操作系统上的原生 NTFS 权限强制执行的。

## 使用 VanDyke Software VShell 的 SFTP

VanDyke 的 VShell SSH 服务器在使用 SFTP 子系统时是一个优秀的解决方案。与 OpenSSH 的 SFTP 子系统一样，在 VShell SSH 服务器上启用 SFTP 子系统不需要额外的步骤。与 OpenSSH 不同，VShell 没有用于 SFTP 服务器的直接开/关开关；相反，使用两种方法来启用或禁用它。默认情况下，SFTP 子系统是启用的，并允许所有人无限制访问。为了禁用它，必须配置两个项目：访问控制和 SFTP 选项。您可以在访问控制中为特定用户禁用 SFTP 访问，并可以通过 SFTP 选项限制对 SFTP 文件夹的访问。这两个选项实际上并没有禁用 SFTP 子系统，而是将其限制在特定用户中。这些选项在配置 VShell 的 SFTP 子系统时提供了更多的粒度。为了验证 VShell 的 SFTP 子系统已启用，请完成以下步骤：

1. 前往 Start ↔ Programs ↔ VShell ↔ VShell。
2. 高亮显示 Access Control 部分。
3. 在适当账户的 SFTP 行中选择 Allow 复选框。
4. 选择 Apply。
5. 高亮显示 SFTP 部分。
6. 确保适当的用户被启用以访问适当的账户。默认情况下，允许所有人完全访问所有文件和目录。
7. 选择 Apply。

现在 SFTP 子系统已启用，请从管理、文件传输和授权用户访问的角度审视 VShell。

### 将 VShell 用于管理目的

首先，我将从管理目的的角度讨论 VShell。使用任何 SFTP 客户端（例如 VanDyke Software 的 SecureFX 或 SSH Communications 的 SSH 客户端），您可以连接到 SFTP 服务器以安全地下载文件。例如，如果您想从 IP 地址为 172.16.6.12 的 SFTP 服务器复制名为 `Neeerja.txt` 的文件，您将在 SSH Communications 的 SSH 客户端中完成以下命令：

1. Start ↔ Programs ↔ SSH Communications ↔ Secure File Transfer Client。
2. 选择 Quick Connect。
3. 在 Host Name 中输入 `172.16.6.12`。
4. 在 User Name 字段中输入适当账户的名称。
5. 在 Port Number 字段中指定端口号；默认值为 22。
6. 选择 Password 作为 Authentication Method。
7. 选择 Connect。
8. 当 SFTP 客户端提示时，输入正确的密码。
9. 就这样！现在您可以使用类似 Windows 资源管理器的客户端将文件拖放/复制粘贴到 SFTP 服务器。使用拖放、复制粘贴或菜单栏选项从 SFTP 客户端传输到 SFTP 服务器的所有文件都是加密的。

类似地，要将文件上传到 SSH 服务器，您可以使用拖放、复制粘贴或菜单栏选项。

与 FTP GUI 客户端一样，您可以使用加密会话在本地目录和 SSH 服务器之间传输文件。在这种情况下，VShell 的 SFTP 服务器对于大多数组织的一般管理目的来说是一个非常不错的解决方案。管理员级别的用户可以登录 SSH 服务器进行命令行访问，也可以使用 SFTP 子系统以安全和简便的方式传输重要和敏感的文件及目录。

## 使用 VShell 进行文件共享

接下来，我将从文件共享的角度讨论 VShell。与 OpenSSH 一样，VShell 使用操作系统账户以补充 SSH 的方式提供 SFTP 子系统的使用。在操作系统上拥有账户，即使该账户仅用于 SFTP，也意味着根据 NTFS 权限，该账户可能有权访问、修改或读取操作系统上的敏感文件，例如 `\\winnt\\winnt\\system32` 和 `\\winnt\\repair`。

如果 VShell SFTP 服务器的目的仅是文件共享，由于它们是操作系统账户，所有 VShell 账户仍然对其他部分的操作系统拥有权限。在文件服务器场景中，您可能不希望暴露操作系统目录或整个目录结构以供 SFTP 访问；相反，您可能只想暴露一个根文件夹用于全组织的通用文件共享。例如，您可能不希望所有用户都下载 `\\winnt\\repair\\sam` 的副本；相反，您可能希望他们只下载指定目录（如 `d:\\share`）中的文件。In this

在这种情况下，应使用 V$Shell 的 SFTP 访问控制功能。为了允许系统中所有账户仅访问 `d:\share` 文件夹（该文件夹可以是公司文件服务器上的根目录），请完成以下步骤：

- 1. 前往 **开始 > 程序 > V$Shell > V$Shell**。
- 2. 选中 SFTP 部分。
- 3. 在 SFTP 选项下，选择 **添加**。
- 4. 在 SFTP 根目录字段中，输入 `d:\share` 或 **简单地使用 ... 按钮浏览到该位置**。
- 5. 在别名（Alias）字段中，输入 **CorpFileServer**。
- 6. 在右侧部分选择 **添加**。
- 7. 添加 **Everyone** 组。
- 8. 选择 **确定**。
- 9. 选择 **应用**。

现在，操作系统或域中的所有账户都可以对 `D:\share` 目录进行 SFTP 访问。为了确保拒绝访问操作系统的其余部分，请完成以下步骤：

- 1. 在 SFTP 部分选中 `<Unrestricted>`（无限制）选项，并选择 **编辑**。
- 2. 移除所有账户，包括 **Everyone** 及其他任何存在的账户。
- 3. 输入您希望授予完全 SFTP 访问权限的账户，例如管理员账户。如果需要添加的账户不多，请选择 **确定**。
- 4. 选择 **应用**。

现在，没有账户，或者只有管理员账户，拥有无限制的访问权限。此外，系统或域中的每个其他账户只能访问 `D:\share`，无论该账户拥有何种 NTFS 权限。在使用 SSH 或 SFTP 子系统时，V$Shell 的访问控制列表会覆盖 V$Shell 服务器上的 NTFS 权限。图 8.6 和 8.7 展示了最终结果。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_312_0.png)

**图 8.6 VShell 中 Everyone 组的 SFTP 文件服务器权限。**

![](img/c99d6f526a5f9fa62f2c34daada85ad7_312_1.png)

**图 8.7 VShell 中 Administrators 组的 SFTP 文件服务器权限。**

除了无需任何操作系统访问控制列表（ACLs）即可限制对特定目录的访问外，VShell 还可以允许/限制特定账户访问 SFTP 子系统。例如，如果您希望每个人都只能将 SSH 服务器作为公司文件服务器使用 SFTP 子系统进行访问，而不允许命令行或端口转发访问，那么可以通过执行以下步骤轻松地在 VShell 中设置：

- 1. 选择访问控制部分。
- 2. 单击添加。
- 3. 选择 Everyone 组并选择确定。
- 4. 保持 Everyone 组处于选中状态，并为允许权限选择登录（Logon）和 SFTP。
- 5. 保持 Everyone 组处于选中状态，并选择拒绝权限下的 Shell（Shell）、远程执行（Remote Execution）、端口转发（Port Forwarding）和远程端口转发（Remote Port Forwarding）。
- 6. 选择应用。
