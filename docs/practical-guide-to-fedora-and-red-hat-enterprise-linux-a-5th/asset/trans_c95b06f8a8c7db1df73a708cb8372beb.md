

## swat 配置说明

在此示例中，请勿点击任何 **Set Default**（设置默认值）按钮。在完成某页上的修改后，但在点击窗口顶部的菜单栏按钮之前，请务必点击每页顶部的 **Commit Changes**（提交更改）。否则，swat 将不会保留您的更改。

首先，点击 Samba/swat 主页顶部的 **GLOBALS**（全局设置）。除以下三项外，请保持所有设置当前状态：**workgroup**（工作组）、**hosts allow**（允许的主机）和 **hosts deny**（禁止的主机）。将 **workgroup** 设置为 Windows 系统使用的工作组。（如果您遵循了前面的 JumpStart 步骤，工作组已经设置好了。）向下滚动至“Security Options”（安全选项）底部，将 **hosts allow** 设置为允许访问本地系统共享资源和打印机的计算机名称或 IP 地址（包括 **localhost** [127.0.0.1]）。使用空格或逗号分隔各项条目。有关设置 **hosts allow** 的各种方式，请参阅第 761 页。将 **hosts deny** 设置为 **ALL**（所有）。完成 **GLOBALS** 页面的操作后，点击 **Commit Changes**（提交更改）（位于页面顶部附近）。

### 提示：如果您无法再使用 swat

如果您无法再使用 swat，可能是因为您错误地更改了 **hosts allow** 设置。在这种情况下，您需要编辑 /etc/samba/smb.conf 并修正包含 **hosts allow** 字样的行：

```
# grep hosts smb.conf
hosts allow = 127.0.0.1, 192.168.0.8
hosts deny = ALL
```

上述条目仅允许来自本地系统和 192.168.0.8 的访问。

接下来，点击页面顶部的 **SHARES**（共享设置）。除了两个 **Change View**（切换视图）按钮外，还会出现三个按钮和两个文本框（图 23-6）。在 **Create Share**（创建共享）按钮旁边的文本框中，输入您想要分配给正在配置的共享的名称。此名称可以是任意内容；它是 Windows 显示且用户在操作共享时选择时使用的名称。点击 **Create Share**。当您想要修改现有共享时，在 **Choose Share**（选择共享）旁边的组合框中显示共享名称，然后点击 **Choose Share**。这两个操作中的任何一个都会展开“Share Parameters”（共享参数）窗口，以显示所选共享的信息。

除 **path**（路径）和可选的 **comment**（注释）外，请保持所有设置为其默认值。**path** 指定了本地 Linux 系统中共享的绝对路径名，而您可以使用 **comment** 来指定该共享所指向的 Linux 系统和目录。**hosts allow** 和 **hosts deny** 的值取自之前设置的全局变量。完成 **SHARES** 页面的操作后，点击 **Commit Changes**（提交更改）。如果您想查看实际上有多少参数，请点击页面顶部附近的 **Advanced**（高级）。

现在，从 Windows 计算机上，您应该能够访问刚刚创建的共享（第 765 页）。

### 提示：更改 smb.conf 时无需重启 Samba

Samba 在每次客户端连接时都会重新读取其配置文件。除非您更改 **security**（安全）参数（第 762 页），否则在更改 **smb.conf** 时不需要重启 Samba。

![](img/f28adb66a7398a382f0505e0ba74a872_799_0.png)

**图 23-6** 共享参数页面

## 手动配置 Samba 服务器

/etc/samba/smb.conf 文件控制 Samba 工作的大部分方面，并分为若干部分。每个部分都以一行以开括号 ([) 开头、包含一些文本并以闭括号 (]) 结尾的行开始。括号内的文本用于标识该部分。典型的章节包括：

- **[globs]** 定义全局参数
- **[printers]** 定义打印机
- **[homes]** 定义 homes 目录中的共享
- **[share name]** 定义一个共享（您可以拥有多个这样的章节）

在 Fedora/RHEL 系统中安装时，/etc/samba/smb.conf 示例配置文件包含大量注释和已注释掉的示例。smb.conf 中的注释行可以以井号 (#) 或分号 (;) 开头。示例文件使用井号开始那些旨在保留为注释的行，使用分号开始那些您可能希望模仿或原样使用（通过移除分号）的行。以下 smb.conf 文件片段包含两行真正的注释和七行以分号开头的行，您可能希望取消注释并对其进行修改：

```
# A private directory, usable only by fred. Note that fred requires # write access to the directory.
: [freddir]
:      comment = Fred's Service
:      path = /usr/somewhere/private
:      valid users = fred
:      public = no
:      writable = yes
:      printable = no
```

假设 **smb.conf** 中的全局参数已正确设置，您需要添加一个共享以便 **Windows** 系统能够访问本地 **Linux** 系统上的目录。在 **smb.conf** 文件末尾添加以下简单共享，以便 **Windows** 系统上的用户能够读取和写入本地 `/tmp` 目录：

```
[tmp]  
    comment = temporary directory  
    path = /tmp  
    writable = yes  
    guest ok = yes
```

该共享在 **Windows** 下的名称为 **tmp**；在 **Linux** 下的路径为 `/tmp`。任何能够登录 **Samba** 的 **Windows** 用户（包括 **guest** 来宾）都可以读取和写入此目录，前提是该用户的 **Linux** 权限允许这样做。适用于使用 **Samba** 的 **Windows** 用户的 **Linux** 权限，是适用于该 **Windows** 用户映射到的 **Linux** 用户的权限。

## smb.conf 文件中的参数

`smb.conf` 手册页和 **swat** 的 **Help**（帮助）功能列出了您可以在 `smb.conf` 中设置的所有参数。以下部分介绍了一些您可能想要更改的参数。

### 全局参数

- **interfaces** 一个 **SPACE**（空格）分隔的列表，列出 **Samba** 使用的网络。指定为接口名称（如 `eth0`）或 **IP** 地址/子网掩码对（第 443 页）。
  - 默认：除 127.0.0.1 外的所有活动接口
- **server string** 显示在 **Windows** 机器各个位置的字符串。在字符串中，**Samba** 会将 `%v` 替换为 **Samba** 版本号，将 `%h` 替换为主机名。
  - 默认： **Samba** %v  
  - Fedora/RHEL： **Samba** Server
- **workgroup** 服务器所属的工作组。将其设置为与使用服务器的 **Windows** 客户端相同的工作组。此参数控制当 `security`（第 762 页）设置为 **DOMAIN** 时 **Samba** 使用的域名。
  - 默认： **WORKGROUP**  
  - Fedora/RHEL： **MYGROUP**

### 安全参数

- **encrypt passwords** 设置为 **YES** 时仅接受客户端提供的加密密码。**Windows** 98 和 **Windows** NT 4.0 **Service** Pack 3 及更高版本默认使用加密密码。除非您将 `security` 设置为 **SERVER** 或 **DOMAIN**，否则此参数使用 **smbpasswd** 来验证密码，在这种情况下 **Samba** 使用另一台服务器进行身份验证。
  - 默认： **YES**

如果您未设置 **passwd**（一个密码数据库），Samba 默认将加密密码存储在 **smbpasswd** 文件中。在用户数少于 250 人的服务器上，将密码存储在 **smbpasswd** 文件中是合理的。对于高负载服务器，请查阅 Samba HOWTO 集合中关于配置数据库后端的信息。

- **guest account** 分配给以 **guest** 身份登录或映射为 **guest** 的用户名；仅当 **guest ok**（第 765 页）设置为 YES 时适用。此用户名应存在于 /etc/passwd 中，但不应能够登录系统。通常 **guest account** 被分配值 **nobody**，因为用户 **nobody** 只能访问任何用户都能访问的文件。如果您在 Linux 系统中将 **nobody** 账户用于其他用途，请将此变量设置为除了 **nobody** 以外的其他名称。
  - 默认： **nobody**

- **hosts allow** 类似于 /etc/hosts.allow 文件（第 447 页），此参数指定允许连接到服务器的主机。覆盖在 **hosts deny** 中指定的主机。一个好的策略是在 **hosts deny** 中指定 ALL，并在该文件中指定您希望授予访问权限的主机。以与 **hosts.allow** 相同的方式指定主机。
  - 默认：无（允许所有主机访问）

- **hosts deny** 类似于 /etc/hosts.deny 文件（第 447 页），此参数指定不允许连接到服务器的主机。被在 **hosts allow** 中指定的主机覆盖。如果您在此文件中指定 ALL，请记住在 **hosts allow** 中包含本地系统 (127.0.0.1)。以与 **hosts.deny** 相同的方式指定主机。
  - 默认：无（未排除任何主机）

- **map to guest** 定义何时将失败的登录映射到 **guest account**。仅在 **security** 未设置为 **SHARE** 时有用。
  - Never：仅当用户明确提供 **guest** 作为用户名和密码为空时，才允许 **guest** 登录。
  - Bad User：将任何试图以不存在的用户身份登录的行为视为 **guest** 登录。此参数存在安全风险，因为它允许恶意用户快速获取系统上的用户列表。
  - Bad Password：静默地将输入密码错误的任何用户作为 **guest** 登录。此参数可能会使用户感到困惑，当她们打错密码并无意中作为 **guest** 登录时，因为她们会突然看到比习惯更少的共享。
  - 默认：Never

- **passwd chat** Samba 用于与 **passwd** 程序交互的聊天脚本。如果不遵循此脚本，Samba 不会更改密码。仅在 **unix passwd sync** 设置为 YES 时使用。
  - 默认： `newpassword %n\nnewpassword %n\nchanged`

- **passwd program** Samba 用于设置 Linux 密码的程序。Samba 将 %u 替换为用户名。
  - 默认： `/usr/bin/passwd %u`

