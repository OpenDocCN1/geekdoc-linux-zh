
基于主机和基于用户的 Samba 系统安全性可通过以下指令增强：invalid users、valid users、hosts allow 和 hosts deny。

重申一下，本节仅关注与 RHCE 目标相关的那些指令。

## Share Settings

要查看 SWAT 可以对 smb.conf 配置文件中的共享设置进行哪些操作，请从 SWAT 基于 Web 的菜单顶部单击 Shares。单击与 Choose Share 关联的下拉文本框，然后单击 Homes。接下来在 Change View To 旁边，单击 Advanced 以显示图 15-3 所示的屏幕。相关选项分为几个类别。

### FIGURE 15-3 SWAT share settings

![](img/9139201cfcaf4292284a0eed074928e5_851_0.png)

此页面上的选项很直接。要创建第二个共享，请在 Create Share 文本框中输入名称，然后单击 Create Share 按钮。然后你可以在其后的文本框中对其进行配置。过程完成后，单击 Commit Changes。出现的许多指令已在全局设置部分解释过，但仅适用于本地共享。这些指令在此未重复。

- **comment** 与共享名称一起包含的信息。
- **path** 要共享的目录的路径。
- **username** 在没有机器用户名时替代用户名；很少使用。
- **force user** 分配给所有连接到共享的用户帐户。
- **force group** 分配给所有连接到共享的组帐户。
- **read only** 如此标记的共享只能读取。
- **guest only** 仅允许访客用户连接。
- **guest ok** 允许访客用户连接；无需密码。

你会注意到大多数这些指令在此未涵盖，事实上很少使用。

## Server Status

要查看系统上 Samba 的当前状态，请从 SWAT 基于 Web 的菜单顶部单击 Server Status。如图 15-4 所示，它支持对 Samba、NetBIOS 和 Winbind 守护进程的控制。如果存在活动连接、活动共享目录和正在使用的文件，它们也会在此视图中列出。

## View Configuration

使用 SWAT 所做的任何更改，一旦保存就会写入 /etc/samba/smb.conf 文件。单击 View。它包含该文件的当前只读视图。

## User Management

你可以使用 SWAT 管理 Samba 用户身份验证数据库。为此，请从 SWAT 基于 Web 的菜单顶部单击 Password。如图 15-5 所示，它支持为当前用户更改密码。此外，你还可以使用所示的屏幕将新用户添加到本地 Samba 身份验证数据库。

### FIGURE 15-4 Default installed Apache home page

![](img/9139201cfcaf4292284a0eed074928e5_853_0.png)

但这些只是 smbpasswd 命令的前端。在任何一种情况下，用户都必须存在于 Linux 身份验证数据库中。例如，以下命令将当前用户 michael 采用并提示输入新密码：

```
# smbpasswd michael
```

或者，以下命令将用户 donna 添加到 Samba 身份验证数据库，并提示输入密码：

```
# smbpasswd -a donna
```

-d、-e 和 -x 选项可分别禁用、启用和从 Samba 身份验证数据库中删除给定用户。

## Test Changes to /etc/samba/smb.conf

对 /etc/samba/smb.conf 进行任何更改后，在投入生产之前应始终测试系统。使用 testparm 实用程序可以对 Samba 配置文件进行简单的语法检查，如图 15-6 所示。这并不会实际检查服务是否正在运行或是否正常运行；它仅检查基本文本语法和命令段。

### FIGURE 15-5 SWAT server password management

![](img/9139201cfcaf4292284a0eed074928e5_854_0.png)

显示的指令是共享段，以及相关的指令。例如，[homes] 共享不是只读的，并且对所有客户端不可浏览。

## Review User- and Host-Based Samba Security

如 RHCE 目标所建议，你需要知道如何为每个服务配置“基于主机的和基于用户的[content]
基于主机和基于用户的 Samba 系统安全性可通过以下指令增强：invalid users、valid users、hosts allow 和 hosts deny。

重申一下，本节仅关注与 RHCE 目标相关的那些指令。

## Share Settings

要查看 SWAT 可以对 smb.conf 配置文件中的共享设置进行哪些操作，请从 SWAT 基于 Web 的菜单顶部单击 Shares。单击与 Choose Share 关联的下拉文本框，然后单击 Homes。接下来在 Change View To 旁边，单击 Advanced 以显示图 15-3 所示的屏幕。相关选项分为几个类别。

### FIGURE 15-3 SWAT share settings

![](img/9139201cfcaf4292284a0eed074928e5_851_0.png)

此页面上的选项很直接。要创建第二个共享，请在 Create Share 文本框中输入名称，然后单击 Create Share 按钮。然后你可以在其后的文本框中对其进行配置。过程完成后，单击 Commit Changes。出现的许多指令已在全局设置部分解释过，但仅适用于本地共享。这些指令在此未重复。

- **comment** 与共享名称一起包含的信息。
- **path** 要共享的目录的路径。
- **username** 在没有机器用户名时替代用户名；很少使用。
- **force user** 分配给所有连接到共享的用户帐户。
- **force group** 分配给所有连接到共享的组帐户。
- **read only** 如此标记的共享只能读取。
- **guest only** 仅允许访客用户连接。
- **guest ok** 允许访客用户连接；无需密码。

你会注意到大多数这些指令在此未涵盖，事实上很少使用。

## Server Status

要查看系统上 Samba 的当前状态，请从 SWAT 基于 Web 的菜单顶部单击 Server Status。如图 15-4 所示，它支持对 Samba、NetBIOS 和 Winbind 守护进程的控制。如果存在活动连接、活动共享目录和正在使用的文件，它们也会在此视图中列出。

## View Configuration

使用 SWAT 所做的任何更改，一旦保存就会写入 /etc/samba/smb.conf 文件。单击 View。它包含该文件的当前只读视图。

## User Management

你可以使用 SWAT 管理 Samba 用户身份验证数据库。为此，请从 SWAT 基于 Web 的菜单顶部单击 Password。如图 15-5 所示，它支持为当前用户更改密码。此外，你还可以使用所示的屏幕将新用户添加到本地 Samba 身份验证数据库。

### FIGURE 15-4 Default installed Apache home page

![](img/9139201cfcaf4292284a0eed074928e5_853_0.png)

但这些只是 smbpasswd 命令的前端。在任何一种情况下，用户都必须存在于 Linux 身份验证数据库中。例如，以下命令将当前用户 michael 采用并提示输入新密码：

```
# smbpasswd michael
```

或者，以下命令将用户 donna 添加到 Samba 身份验证数据库，并提示输入密码：

```
# smbpasswd -a donna
```

-d、-e 和 -x 选项可分别禁用、启用和从 Samba 身份验证数据库中删除给定用户。

## Test Changes to /etc/samba/smb.conf

对 /etc/samba/smb.conf 进行任何更改后，在投入生产之前应始终测试系统。使用 testparm 实用程序可以对 Samba 配置文件进行简单的语法检查，如图 15-6 所示。这并不会实际检查服务是否正在运行或是否正常运行；它仅检查基本文本语法和命令段。

### FIGURE 15-5 SWAT server password management

![](img/9139201cfcaf4292284a0eed074928e5_854_0.png)

显示的指令是共享段，以及相关的指令。例如，[homes] 共享不是只读的，并且对所有客户端不可浏览。

## Review User- and Host-Based Samba Security

如 RHCE 目标所建议，你需要知道如何为每个服务配置“基于主机的和基于用户的[content]
基于主机和基于用户的 Samba 系统安全性可通过以下指令增强：invalid users、valid users、hosts allow 和 hosts deny。

重申一下，本节仅关注与 RHCE 目标相关的那些指令。

## Share Settings

要查看 SWAT 可以对 smb.conf 配置文件中的共享设置进行哪些操作，请从 SWAT 基于 Web 的菜单顶部单击 Shares。单击与 Choose Share 关联的下拉文本框，然后单击 Homes。接下来在 Change View To 旁边，单击 Advanced 以显示图 15-3 所示的屏幕。相关选项分为几个类别。

### FIGURE 15-3 SWAT share settings

![](img/9139201cfcaf4292284a0eed074928e5_851_0.png)

此页面上的选项很直接。要创建第二个共享，请在 Create Share 文本框中输入名称，然后单击 Create Share 按钮。然后你可以在其后的文本框中对其进行配置。过程完成后，单击 Commit Changes。出现的许多指令已在全局设置部分解释过，但仅适用于本地共享。这些指令在此未重复。

- **comment** 与共享名称一起包含的信息。
- **path** 要共享的目录的路径。
- **username** 在没有机器用户名时替代用户名；很少使用。
- **force user** 分配给所有连接到共享的用户帐户。
- **force group** 分配给所有连接到共享的组帐户。
- **read only** 如此标记的共享只能读取。
- **guest only** 仅允许访客用户连接。
- **guest ok** 允许访客用户连接；无需密码。

你会注意到大多数这些指令在此未涵盖，事实上很少使用。

## Server Status

要查看系统上 Samba 的当前状态，请从 SWAT 基于 Web 的菜单顶部单击 Server Status。如图 15-4 所示，它支持对 Samba、NetBIOS 和 Winbind 守护进程的控制。如果存在活动连接、活动共享目录和正在使用的文件，它们也会在此视图中列出。

## View Configuration

使用 SWAT 所做的任何更改，一旦保存就会写入 /etc/samba/smb.conf 文件。单击 View。它包含该文件的当前只读视图。

## User Management

你可以使用 SWAT 管理 Samba 用户身份验证数据库。为此，请从 SWAT 基于 Web 的菜单顶部单击 Password。如图 15-5 所示，它支持为当前用户更改密码。此外，你还可以使用所示的屏幕将新用户添加到本地 Samba 身份验证数据库。

### FIGURE 15-4 Default installed Apache home page

![](img/9139201cfcaf4292284a0eed074928e5_853_0.png)

但这些只是 smbpasswd 命令的前端。在任何一种情况下，用户都必须存在于 Linux 身份验证数据库中。例如，以下命令将当前用户 michael 采用并提示输入新密码：

```
# smbpasswd michael
```

或者，以下命令将用户 donna 添加到 Samba 身份验证数据库，并提示输入密码：

```
# smbpasswd -a donna
```

-d、-e 和 -x 选项可分别禁用、启用和从 Samba 身份验证数据库中删除给定用户。

## Test Changes to /etc/samba/smb.conf

对 /etc/samba/smb.conf 进行任何更改后，在投入生产之前应始终测试系统。使用 testparm 实用程序可以对 Samba 配置文件进行简单的语法检查，如图 15-6 所示。这并不会实际检查服务是否正在运行或是否正常运行；它仅检查基本文本语法和命令段。

### FIGURE 15-5 SWAT server password management

![](img/9139201cfcaf4292284a0eed074928e5_854_0.png)

显示的指令是共享段，以及相关的指令。例如，[homes] 共享不是只读的，并且对所有客户端不可浏览。

## Review User- and Host-Based Samba Security

如 RHCE 目标所建议，你需要知道如何为每个服务配置“基于主机的和基于用户的[content]
基于主机和基于用户的 Samba 系统安全性可通过以下指令增强：invalid users、valid users、hosts allow 和 hosts deny。

重申一下，本节仅关注与 RHCE 目标相关的那些指令。

## Share Settings

要查看 SWAT 可以对 smb.conf 配置文件中的共享设置进行哪些操作，请从 SWAT 基于 Web 的菜单顶部单击 Shares。单击与 Choose Share 关联的下拉文本框，然后单击 Homes。接下来在 Change View To 旁边，单击 Advanced 以显示图 15-3 所示的屏幕。相关选项分为几个类别。

### FIGURE 15-3 SWAT share settings

![](img/9139201cfcaf4292284a0eed074928e5_851_0.png)

此页面上的选项很直接。要创建第二个共享，请在 Create Share 文本框中输入名称，然后单击 Create Share 按钮。然后你可以在其后的文本框中对其进行配置。过程完成后，单击 Commit Changes。出现的许多指令已在全局设置部分解释过，但仅适用于本地共享。这些指令在此未重复。

- **comment** 与共享名称一起包含的信息。
- **path** 要共享的目录的路径。
- **username** 在没有机器用户名时替代用户名；很少使用。
- **force user** 分配给所有连接到共享的用户帐户。
- **force group** 分配给所有连接到共享的组帐户。
- **read only** 如此标记的共享只能读取。
- **guest only** 仅允许访客用户连接。
- **guest ok** 允许访客用户连接；无需密码。

你会注意到大多数这些指令在此未涵盖，事实上很少使用。

## Server Status

要查看系统上 Samba 的当前状态，请从 SWAT 基于 Web 的菜单顶部单击 Server Status。如图 15-4 所示，它支持对 Samba、NetBIOS 和 Winbind 守护进程的控制。如果存在活动连接、活动共享目录和正在使用的文件，它们也会在此视图中列出。

## View Configuration

使用 SWAT 所做的任何更改，一旦保存就会写入 /etc/samba/smb.conf 文件。单击 View。它包含该文件的当前只读视图。

## User Management

你可以使用 SWAT 管理 Samba 用户身份验证数据库。为此，请从 SWAT 基于 Web 的菜单顶部单击 Password。如图 15-5 所示，它支持为当前用户更改密码。此外，你还可以使用所示的屏幕将新用户添加到本地 Samba 身份验证数据库。

### FIGURE 15-4 Default installed Apache home page

![](img/9139201cfcaf4292284a0eed074928e5_853_0.png)

但这些只是 smbpasswd 命令的前端。在任何一种情况下，用户都必须存在于 Linux 身份验证数据库中。例如，以下命令将当前用户 michael 采用并提示输入新密码：

```
# smbpasswd michael
```

或者，以下命令将用户 donna 添加到 Samba 身份验证数据库，并提示输入密码：

```
# smbpasswd -a donna
```

-d、-e 和 -x 选项可分别禁用、启用和从 Samba 身份验证数据库中删除给定用户。

## Test Changes to /etc/samba/smb.conf

对 /etc/samba/smb.conf 进行任何更改后，在投入生产之前应始终测试系统。使用 testparm 实用程序可以对 Samba 配置文件进行简单的语法检查，如图 15-6 所示。这并不会实际检查服务是否正在运行或是否正常运行；它仅检查基本文本语法和命令段。

### FIGURE 15-5 SWAT server password management

![](img/9139201cfcaf4292284a0eed074928e5_854_0.png)

显示的指令是共享段，以及相关的指令。例如，[homes] 共享不是只读的，并且对所有客户端不可浏览。

## Review User- and Host-Based Samba Security

如 RHCE 目标所建议，你需要知道如何为每个服务配置“基于主机的和基于用户的[content]
基于主机和基于用户的 Samba 系统安全性可通过以下指令增强：invalid users、valid users、hosts allow 和 hosts deny。

重申一下，本节仅关注与 RHCE 目标相关的那些指令。

## Share Settings

要查看 SWAT 可以对 smb.conf 配置文件中的共享设置进行哪些操作，请从 SWAT 基于 Web 的菜单顶部单击 Shares。单击与 Choose Share 关联的下拉文本框，然后单击 Homes。接下来在 Change View To 旁边，单击 Advanced 以显示图 15-3 所示的屏幕。相关选项分为几个类别。

### FIGURE 15-3 SWAT share settings

![](img/9139201cfcaf4292284a0eed074928e5_851_0.png)

此页面上的选项很直接。要创建第二个共享，请在 Create Share 文本框中输入名称，然后单击 Create Share 按钮。然后你可以在其后的文本框中对其进行配置。过程完成后，单击 Commit Changes。出现的许多指令已在全局设置部分解释过，但仅适用于本地共享。这些指令在此未重复。

- **comment** 与共享名称一起包含的信息。
- **path** 要共享的目录的路径。
- **username** 在没有机器用户名时替代用户名；很少使用。
- **force user** 分配给所有连接到共享的用户帐户。
- **force group** 分配给所有连接到共享的组帐户。
- **read only** 如此标记的共享只能读取。
- **guest only** 仅允许访客用户连接。
- **guest ok** 允许访客用户连接；无需密码。

你会注意到大多数这些指令在此未涵盖，事实上很少使用。

## Server Status

要查看系统上 Samba 的当前状态，请从 SWAT 基于 Web 的菜单顶部单击 Server Status。如图 15-4 所示，它支持对 Samba、NetBIOS 和 Winbind 守护进程的控制。如果存在活动连接、活动共享目录和正在使用的文件，它们也会在此视图中列出。

## View Configuration

使用 SWAT 所做的任何更改，一旦保存就会写入 /etc/samba/smb.conf 文件。单击 View。它包含该文件的当前只读视图。

## User Management

你可以使用 SWAT 管理 Samba 用户身份验证数据库。为此，请从 SWAT 基于 Web 的菜单顶部单击 Password。如图 15-5 所示，它支持为当前用户更改密码。此外，你还可以使用所示的屏幕将新用户添加到本地 Samba 身份验证数据库。

### FIGURE 15-4 Default installed Apache home page

![](img/9139201cfcaf4292284a0eed074928e5_853_0.png)

但这些只是 smbpasswd 命令的前端。在任何一种情况下，用户都必须存在于 Linux 身份验证数据库中。例如，以下命令将当前用户 michael 采用并提示输入新密码：

```
# smbpasswd michael
```

或者，以下命令将用户 donna 添加到 Samba 身份验证数据库，并提示输入密码：

```
# smbpasswd -a donna
```

-d、-e 和 -x 选项可分别禁用、启用和从 Samba 身份验证数据库中删除给定用户。

## Test Changes to /etc/samba/smb.conf

对 /etc/samba/smb.conf 进行任何更改后，在投入生产之前应始终测试系统。使用 testparm 实用程序可以对 Samba 配置文件进行简单的语法检查，如图 15-6 所示。这并不会实际检查服务是否正在运行或是否正常运行；它仅检查基本文本语法和命令段。

### FIGURE 15-5 SWAT server password management

![](img/9139201cfcaf4292284a0eed074928e5_854_0.png)

显示的指令是共享段，以及相关的指令。例如，[homes] 共享不是只读的，并且对所有客户端不可浏览。

## Review User- and Host-Based Samba Security

如 RHCE 目标所建议，你需要知道如何为每个服务配置“基于主机的和基于用户的[content]
基于主机和基于用户的 Samba 系统安全性可通过以下指令增强：invalid users、valid users、hosts allow 和 hosts deny。

重申一下，本节仅关注与 RHCE 目标相关的那些指令。

## Share Settings

要查看 SWAT 可以对 smb.conf 配置文件中的共享设置进行哪些操作，请从 SWAT 基于 Web 的菜单顶部单击 Shares。单击与 Choose Share 关联的下拉文本框，然后单击 Homes。接下来在 Change View To 旁边，单击 Advanced 以显示图 15-3 所示的屏幕。相关选项分为几个类别。

### FIGURE 15-3 SWAT share settings

![](img/9139201cfcaf4292284a0eed074928e5_851_0.png)

此页面上的选项很直接。要创建第二个共享，请在 Create Share 文本框中输入名称，然后单击 Create Share 按钮。然后你可以在其后的文本框中对其进行配置。过程完成后，单击 Commit Changes。出现的许多指令已在全局设置部分解释过，但仅适用于本地共享。这些指令在此未重复。

- **comment** 与共享名称一起包含的信息。
- **path** 要共享的目录的路径。
- **username** 在没有机器用户名时替代用户名；很少使用。
- **force user** 分配给所有连接到共享的用户帐户。
- **force group** 分配给所有连接到共享的组帐户。
- **read only** 如此标记的共享只能读取。
- **guest only** 仅允许访客用户连接。
- **guest ok** 允许访客用户连接；无需密码。

你会注意到大多数这些指令在此未涵盖，事实上很少使用。

## Server Status

要查看系统上 Samba 的当前状态，请从 SWAT 基于 Web 的菜单顶部单击 Server Status。如图 15-4 所示，它支持对 Samba、NetBIOS 和 Winbind 守护进程的控制。如果存在活动连接、活动共享目录和正在使用的文件，它们也会在此视图中列出。

## View Configuration

使用 SWAT 所做的任何更改，一旦保存就会写入 /etc/samba/smb.conf 文件。单击 View。它包含该文件的当前只读视图。

## User Management

你可以使用 SWAT 管理 Samba 用户身份验证数据库。为此，请从 SWAT 基于 Web 的菜单顶部单击 Password。如图 15-5 所示，它支持为当前用户更改密码。此外，你还可以使用所示的屏幕将新用户添加到本地 Samba 身份验证数据库。

### FIGURE 15-4 Default installed Apache home page

![](img/9139201cfcaf4292284a0eed074928e5_853_0.png)

但这些只是 smbpasswd 命令的前端。在任何一种情况下，用户都必须存在于 Linux 身份验证数据库中。例如，以下命令将当前用户 michael 采用并提示输入新密码：

```
# smbpasswd michael
```

或者，以下命令将用户 donna 添加到 Samba 身份验证数据库，并提示输入密码：

```
# smbpasswd -a donna
```

-d、-e 和 -x 选项可分别禁用、启用和从 Samba 身份验证数据库中删除给定用户。

## Test Changes to /etc/samba/smb.conf

对 /etc/samba/smb.conf 进行任何更改后，在投入生产之前应始终测试系统。使用 testparm 实用程序可以对 Samba 配置文件进行简单的语法检查，如图 15-6 所示。这并不会实际检查服务是否正在运行或是否正常运行；它仅检查基本文本语法和命令段。

### FIGURE 15-5 SWAT server password management

![](img/9139201cfcaf4292284a0eed074928e5_854_0.png)

显示的指令是共享段，以及相关的指令。例如，[homes] 共享不是只读的，并且对所有客户端不可浏览。

## Review User- and Host-Based Samba Security

如 RHCE 目标所建议，你需要知道如何为每个服务配置“基于主机的和基于用户的[content]
基于主机和基于用户的 Samba 系统安全性可通过以下指令增强：invalid users、valid users、hosts allow 和 hosts deny。

重申一下，本节仅关注与 RHCE 目标相关的那些指令。

## Share Settings

要查看 SWAT 对 smb.conf 配置文件中的共享设置能做什么，请从 SWAT Web 菜单顶部单击 Shares。单击与 Choose Share 关联的下拉文本框，然后单击 Homes。接下来在 Change View To 旁单击 Advanced 以显示图 15-3 所示的屏幕。相关选项分为几个类别。

### FIGURE 15-3 SWAT share settings

![](img/9139201cfcaf4292284a0eed074928e5_851_0.png)

此页选项很直接。要创建第二个共享，在 Create Share 文本框输入名称，然后单击 Create Share 按钮。之后可在其后文本框中配置。完成后单击 Commit Changes。出现的许多指令已在全局设置部分解释过，但仅适用于本地共享。此处不重复。

- **comment** 与共享名称一起包含的信息。
- **path** 要共享的目录路径。
- **username** 在没有机器用户名时替代用户名；很少使用。
- **force user** 分配给所有连接共享的用户帐户。
- **force group** 分配给所有连接共享的组帐户。
- **read only** 如此标记的共享只能读取。
- **guest only** 仅允许访客用户连接。
- **guest ok** 允许访客用户连接；无需密码。

你会注意到大多数这些指令在此未涵盖，事实上很少使用。

## Server Status

要查看系统上 Samba 的当前状态，请从 SWAT Web 菜单顶部单击 Server Status。如图 15-4 所示，它支持控制 Samba、NetBIOS 和 Winbind 守护进程。若有活动连接、活动共享目录和正在使用的文件，也会在此视图中列出。

## View Configuration

使用 SWAT 所做的任何更改，保存后会写入 /etc/samba/smb.conf 文件。单击 View。它包含该文件的当前只读视图。

## User Management

可使用 SWAT 管理 Samba 用户身份验证数据库。为此，从 SWAT Web 菜单顶部单击 Password。如图 15-5 所示，它支持为当前用户更改密码。此外，也可使用所示屏幕将新用户添加到本地 Samba 身份验证数据库。

### FIGURE 15-4 Default installed Apache home page

![](img/9139201cfcaf4292284a0eed074928e5_853_0.png)

但这些只是 smbpasswd 命令的前端。在任何情况下，用户都必须存在于 Linux 身份验证数据库中。例如，以下命令将当前用户 michael 采用并提示输入新密码：

```
# smbpasswd michael
```

或者，以下命令将用户 donna 添加到 Samba 身份验证数据库，并提示输入密码：

```
# smbpasswd -a donna
```

-d、-e 和 -x 选项可分别禁用、启用和从 Samba 身份验证数据库中删除给定用户。

## Test Changes to /etc/samba/smb.conf

对 /etc/samba/smb.conf 做任何更改后，投入生产前应始终测试系统。可使用 testparm 实用程序对 Samba 配置文件进行简单语法检查，如图 15-6 所示。这并不会检查服务是否运行或是否正常；它仅检查基本文本语法和命令段。

### FIGURE 15-5 SWAT server password management

![](img/9139201cfcaf4292284a0eed074928e5_854_0.png)

显示的指令是共享段及相关指令。例如，[homes] 共享不是只读的，并且对所有客户端不可浏览。

## Review User- and Host-Based Samba Security

如 RHCE 目标所建议，你需要知道如何为每个服务配置“基于主机的和基于用户的[content]
基于主机和基于用户的 Samba 系统安全性可通过以下指令增强：invalid users、valid users、hosts allow 和 hosts deny。

重申一下，本节仅关注与 RHCE 目标相关的那些指令。

## Share Settings

要查看 SWAT 可以对 smb.conf 配置文件中的共享设置进行哪些操作，请从 SWAT 基于 Web 的菜单顶部单击 Shares。单击与 Choose Share 关联的下拉文本框，然后单击 Homes。接下来在 Change View To 旁边，单击 Advanced 以显示图 15-3 所示的屏幕。相关选项分为几个类别。

### FIGURE 15-3 SWAT share settings

![](img/9139201cfcaf4292284a0eed074928e5_851_0.png)

此页面上的选项很直接。要创建第二个共享，请在 Create Share 文本框中输入名称，然后单击 Create Share 按钮。然后你可以在其后的文本框中对其进行配置。过程完成后，单击 Commit Changes。出现的许多指令已在全局设置部分解释过，但仅适用于本地共享。这些指令在此未重复。

- **comment** 与共享名称一起包含的信息。
- **path** 要共享的目录的路径。
- **username** 在没有机器用户名时替代用户名；很少使用。
- **force user** 分配给所有连接到共享的用户帐户。
- **force group** 分配给所有连接到共享的组帐户。
- **read only** 如此标记的共享只能读取。
- **guest only** 仅允许访客用户连接。
- **guest ok** 允许访客用户连接；无需密码。

你会注意到大多数这些指令在此未涵盖，事实上很少使用。

## Server Status

要查看系统上 Samba 的当前状态，请从 SWAT 基于 Web 的菜单顶部单击 Server Status。如图 15-4 所示，它支持对 Samba、NetBIOS 和 Winbind 守护进程的控制。如果存在活动连接、活动共享目录和正在使用的文件，它们也会在此视图中列出。

## View Configuration

使用 SWAT 所做的任何更改，一旦保存就会写入 /etc/samba/smb.conf 文件。单击 View。它包含该文件的当前只读视图。

## User Management

你可以使用 SWAT 管理 Samba 用户身份验证数据库。为此，请从 SWAT 基于 Web 的菜单顶部单击 Password。如图 15-5 所示，它支持为当前用户更改密码。此外，你还可以使用所示的屏幕将新用户添加到本地 Samba 身份验证数据库。

### FIGURE 15-4 Default installed Apache home page

![](img/9139201cfcaf4292284a0eed074928e5_853_0.png)

但这些只是 smbpasswd 命令的前端。在任何一种情况下，用户都必须存在于 Linux 身份验证数据库中。例如，以下命令将当前用户 michael 采用并提示输入新密码：

```
# smbpasswd michael
```

或者，以下命令将用户 donna 添加到 Samba 身份验证数据库，并提示输入密码：

```
# smbpasswd -a donna
```

-d、-e 和 -x 选项可分别禁用、启用和从 Samba 身份验证数据库中删除给定用户。

## Test Changes to /etc/samba/smb.conf

对 /etc/samba/smb.conf 进行任何更改后，在投入生产之前应始终测试系统。使用 testparm 实用程序可以对 Samba 配置文件进行简单的语法检查，如图 15-6 所示。这并不会实际检查服务是否正在运行或是否正常运行；它仅检查基本文本语法和命令段。

### FIGURE 15-5 SWAT server password management

![](img/9139201cfcaf4292284a0eed074928e5_854_0.png)

显示的指令是共享段，以及相关的指令。例如，[homes] 共享不是只读的，并且对所有客户端不可浏览。

## Review User- and Host-Based Samba Security

如 RHCE 目标所建议，你需要知道如何为每个服务配置基于主机的和基于用户的[content]
基于主机和基于用户的 Samba 系统安全性可通过以下指令增强：invalid users、valid users、hosts allow 和 hosts deny。

重申一下，本节仅关注与 RHCE 目标相关的那些指令。

## Share Settings

要查看 SWAT 可以对 smb.conf 配置文件中的共享设置进行哪些操作，请从 SWAT 基于 Web 的菜单顶部单击 Shares。单击与 Choose Share 关联的下拉文本框，然后单击 Homes。接下来在 Change View To 旁边，单击 Advanced 以显示图 15-3 所示的屏幕。相关选项分为几个类别。

### FIGURE 15-3 SWAT share settings

![](img/9139201cfcaf4292284a0eed074928e5_851_0.png)

此页面上的选项很直接。要创建第二个共享，请在 Create Share 文本框中输入名称，然后单击 Create Share 按钮。然后你可以在其后的文本框中对其进行配置。过程完成后，单击 Commit Changes。出现的许多指令已在全局设置部分解释过，但仅适用于本地共享。这些指令在此未重复。

- **comment** 与共享名称一起包含的信息。
- **path** 要共享的目录的路径。
- **username** 在没有机器用户名时替代用户名；很少使用。
- **force user** 分配给所有连接到共享的用户帐户。
- **force group** 分配给所有连接到共享的组帐户。
- **read only** 如此标记的共享只能读取。
- **guest only** 仅允许访客用户连接。
- **guest ok** 允许访客用户连接；无需密码。

你会注意到大多数这些指令在此未涵盖，事实上很少使用。

## Server Status

要查看系统上 Samba 的当前状态，请从 SWAT 基于 Web 的菜单顶部单击 Server Status。如图 15-4 所示，它支持对 Samba、NetBIOS 和 Winbind 守护进程的控制。如果存在活动连接、活动共享目录和正在使用的文件，它们也会在此视图中列出。

## View Configuration

使用 SWAT 所做的任何更改，一旦保存就会写入 /etc/samba/smb.conf 文件。单击 View。它包含该文件的当前只读视图。

## User Management

你可以使用 SWAT 管理 Samba 用户身份验证数据库。为此，请从 SWAT 基于 Web 的菜单顶部单击 Password。如图 15-5 所示，它支持为当前用户更改密码。此外，你还可以使用所示的屏幕将新用户添加到本地 Samba 身份验证数据库。

### FIGURE 15-4 Default installed Apache home page

![](img/9139201cfcaf4292284a0eed074928e5_853_0.png)

但这些只是 smbpasswd 命令的前端。在任何一种情况下，用户都必须存在于 Linux 身份验证数据库中。例如，以下命令将当前用户 michael 采用并提示输入新密码：

```
# smbpasswd michael
```

或者，以下命令将用户 donna 添加到 Samba 身份验证数据库，并提示输入密码：

```
# smbpasswd -a donna
```

-d、-e 和 -x 选项可分别禁用、启用和从 Samba 身份验证数据库中删除给定用户。

## Test Changes to /etc/samba/smb.conf

对 /etc/samba/smb.conf 进行任何更改后，在投入生产之前应始终测试系统。使用 testparm 实用程序可以对 Samba 配置文件进行简单的语法检查，如图 15-6 所示。这并不会实际检查服务是否正在运行或是否正常运行；它仅检查基本文本语法和命令段。

### FIGURE 15-5 SWAT server password management

![](img/9139201cfcaf4292284a0eed074928e5_854_0.png)

显示的指令是共享段，以及相关的指令。例如，[homes] 共享不是只读的，并且对所有客户端不可浏览。

## 回顾基于用户和基于主机的 Samba 安全

如 RHCE 目标所建议，你需要知道如何为每个服务配置基于主机的和基于用户的[content]
基于主机和基于用户的 Samba 系统安全性可通过以下指令增强：invalid users、valid users、hosts allow 和 hosts deny。

重申一下，本节仅关注与 RHCE 目标相关的那些指令。

## Share Settings

要查看 SWAT 对 smb.conf 配置文件中的共享设置能做什么，请从 SWAT Web 菜单顶部单击 Shares。单击与 Choose Share 关联的下拉文本框，然后单击 Homes。接下来在 Change View To 旁单击 Advanced 以显示图 15-3 所示的屏幕。相关选项分为几个类别。

### FIGURE 15-3 SWAT share settings

![](img/9139201cfcaf4292284a0eed074928e5_851_0.png)

此页选项很直接。要创建第二个共享，在 Create Share 文本框输入名称，然后单击 Create Share 按钮。之后可在其后文本框中配置。完成后单击 Commit Changes。出现的许多指令已在全局设置部分解释过，但仅适用于本地共享。此处不重复。

- **comment** 与共享名称一起包含的信息。
- **path** 要共享的目录路径。
- **username** 在没有机器用户名时替代用户名；很少使用。
- **force user** 分配给所有连接共享的用户帐户。
- **force group** 分配给所有连接共享的组帐户。
- **read only** 如此标记的共享只能读取。
- **guest only** 仅允许访客用户连接。
- **guest ok** 允许访客用户连接；无需密码。

你会注意到大多数这些指令在此未涵盖，事实上很少使用。

## Server Status

要查看系统上 Samba 的当前状态，请从 SWAT Web 菜单顶部单击 Server Status。如图 15-4 所示，它支持控制 Samba、NetBIOS 和 Winbind 守护进程。若有活动连接、活动共享目录和正在使用的文件，也会在此视图中列出。

## View Configuration

使用 SWAT 所做的任何更改，保存后会写入 /etc/samba/smb.conf 文件。单击 View。它包含该文件的当前只读视图。

## User Management

可使用 SWAT 管理 Samba 用户身份验证数据库。为此，从 SWAT Web 菜单顶部单击 Password。如图 15-5 所示，它支持为当前用户更改密码。此外，也可使用所示屏幕将新用户添加到本地 Samba 身份验证数据库。

### FIGURE 15-4 Default installed Apache home page

![](img/9139201cfcaf4292284a0eed074928e5_853_0.png)

但这些只是 smbpasswd 命令的前端。在任何情况下，用户都必须存在于 Linux 身份验证数据库中。例如，以下命令将当前用户 michael 采用并提示输入新密码：

```
# smbpasswd michael
```

或者，以下命令将用户 donna 添加到 Samba 身份验证数据库，并提示输入密码：

```
# smbpasswd -a donna
```

-d、-e 和 -x 选项可分别禁用、启用和从 Samba 身份验证数据库中删除给定用户。

## Test Changes to /etc/samba/smb.conf

对 /etc/samba/smb.conf 做任何更改后，投入生产前应始终测试系统。可使用 testparm 实用程序对 Samba 配置文件进行简单语法检查，如图 15-6 所示。这并不会检查服务是否运行或是否正常；它仅检查基本文本语法和命令段。

### FIGURE 15-5 SWAT server password management

![](img/9139201cfcaf4292284a0eed074928e5_854_0.png)

显示的指令是共享段及相关指令。例如，[homes] 共享不是只读的，并且对所有客户端不可浏览。

## 回顾基于用户和基于主机的 Samba 安全

如 RHCE 目标所建议，你需要知道如何为每个服务，包括 Samba，配置主机级和用户级安全。所以虽然本节重复，但很重要。

回顾一下，用户级安全可在主 Samba 配置文件 smb.conf 中配置。该文件中指定的用户配置在单独的数据库中，通常位于 /var/lib/samba 目录，由 smbpasswd 命令管理。

### FIGURE 15-6

使用 testparm 回顾 Samba 配置

```
[root@Maui ~]# testparm
Load smb config files from /etc/samba/smb.conf
rlimit_max: rlimit_max (1024) below minimum Windows limit (16384)
Processing section "[global]"
Processing section "[printers]"
Loaded services file OK.
Server role: ROLE_STANDALONE
Press enter to see a dump of your service definitions

[global]
workgroup = MYGROUP
server string = Samba Server Version %v
log file = /var/log/samba/log.%m
max log size = 50
wins server = 127.0.0.1
cups options = raw

[homes]
comment = Home Directories
read only = No
browseable = No

[printers]
comment = All Printers
path = /var/spool/samba
printable = Yes
browseable = No
[root@Maui ~]#
```

系统通过以下选项启用用户级安全：

```
security = user
```

用户可通过 invalid users 和 valid users 指令指定为允许或拒绝。这些指令可在全局设置部分通用应用，也可在共享目录配置的段中按共享应用。

主机级安全可在 Samba 配置文件和任何相关的 iptables 防火墙中配置。主机可通过 hosts allow 和 hosts deny 等指令允许或拒绝。在某些配置中，你会看到这些指令的同义词，如 allow hosts 和 deny hosts。

例如，以下 hosts allow 指令可将访问限制到指定的网络：

```
hosts allow = 127. 192.168.122. 192.168.100.
```

127. 不是必需的；除非明确包含在 hosts deny 指令中，否则本地主机地址始终允许。

## 回顾基本 Samba 共享

具体到 Samba，RHCE 目标规定你需要“向特定客户端提供网络共享”并“提供适合组协作的网络共享”。

要向一个或多个特定客户端提供网络共享，需要在与共享 Samba 目录关联的段中包含 valid users 和 invalid users 等指令。

要提供适合组协作的网络共享，需要记住以下任务：

- 为要共享的目录设置适当的组和权限。
- 使用 SELinux samba_share_t 文件类型配置共享目录和文件。
- 在 Samba 配置文件中定义单独的共享段，并为 writable、create mask、directory mask 和 write list 设置适当值。

## EXERCISE 15-2

### Configuring Samba with Shares

在本练习中，你将配置 Samba 以共享一个目录。为此，你将直接编辑 /etc/samba/smb.conf 文件。

- 1. 创建 /home/ftp/public 目录。将所有权更改为 ftp 用户和组，权限为两者完全权限 770。
- 2. 确保使用以下命令为目录设置适当的 SELinux 设置：
  此外，为确保更改在 SELinux 重新标记后仍然存在，你希望在 /etc/selinux/targeted/contexts/files 目录中设置 file_contexts.local 文件，使用如下命令：
- 3. 在文本编辑器中打开 /etc/samba/smb.conf 文件。

```
# chcon -R -t samba_share_t /home/ftp
```

```
# semanage fcontext -a -t samba_share_t /home/ftp
```

- 4. 配置 Samba 以只读模式公开共享 /home/ftp/pub 目录树。在 Share Definitions 部分，你可以添加以下命令：
- 5. 允许访客访问所有公共共享。在 smb.conf 中，这意味着在 [pub] 段中添加以下行：
- 6. 要创建访客帐户，你需要在 smb.conf 中添加以下命令：
- 7. 为 pcguest 创建访客帐户，将其与未使用的 UID 和 GID 600 关联。如果已有此 ID 的用户，请替换为未使用的 ID 号。将密码设置为“anonymous”。虽然你可以用第 8 章讨论的 Red Hat 用户管理器来完成，但最快的方法是使用以下命令：
- 8. 为每个连接的计算机主机创建单独的日志文件。这已通过以下命令默认激活：
- 9. 写入并保存 smb.conf 文件的更改。
- 10. 你可以使用 service smb status 命令查看 Samba 是否已在运行。如果已停止，可以使用 service smb start 命令启动。如果正在运行，可以使用以下命令使 Samba 重新读取配置文件：
  此最终选项允许你在不中断用户与 Samba 服务器的连接的情况下更改 Samba 配置。

```
[pub]
    comment = shared FTP directory
    path = /home/ftp/pub
```

```
guest ok = yes
```

```
; guest account = pcguest
```

```
# useradd pcguest -u 600
# passwd pcguest
```

```
log file = /var/log/samba/%m.log
```

```
# service smb reload
```
