

25. 如果你希望此共享仅授予只读访问权限，则将 **read only** 更改为 **yes**。不过，这将违背拥有公共上传空间的初衷。
26. 如果你希望只有经过身份验证的用户才能访问此空间，则将 **public** 更改为 **no**。
27. 请继续操作：

```conf
[public]
	comment = Public Stuff
	path = /home/samba
	public = yes
	writable = yes
	printable = no
	write list = @staff
```

28. 如果你希望利用此定义允许公众查看共享上的信息，但只允许特定用户和/或组对其进行写入，请取消注释，使其看起来像以下内容：

```conf
[public]
	comment = Public Stuff
	path = /home/samba
	public = yes
	writable = yes
	printable = no
	write list = @staff
```

29. 如果你想重命名此共享，请更改括号内的名称。
30. 如果你想将标识符更改为更具描述性的名称，例如 **Staff Policy Documents**，请更改分配给 **comment** 选项的值。
31. 如果你想将这些文档保存在其他位置，请更改 **path** 语句。
32. 如果你不希望任何人通过 Samba 挂载导出进行写入，请将 **writable** 值更改为 **no**。其实 **printable** 选项在此处并不必要，因为你并未定义打印共享。
33. 如果你保留 **writable** 设置为 **yes**，请将 **write list** 值更改为由一组用户和组构成的列表——采用 `@group` 格式——这些用户和组被允许通过 SMB 写入此共享。
34. 参见以下章节，从零开始构建共享定义。

## 构建文件共享语句

要从零开始构建一个文件共享语句，请执行以下操作：

1. 如果你尚未执行此操作，请以 root 身份登录到你要提供分区的主机。
2. 如果你没有正在编辑该文件，请键入 "vi /etc/smb.conf" 以打开 Samba 配置文件。
3. 键入 "G" 以转到文件末尾。
4. 键入 "o" 以在文件末尾打开新的一行，然后进入插入模式。
5. 以共享名称开始。该名称的格式如下：**[sharename]**。名称中不应包含空格或标点符号。除保留共享外，你可以使用任何术语：[global]、[homes] 和 [printers]。
6. 通常，在共享名称后设置的第一个选项是 **comment**。将此行缩进，使其位于共享名称下方，以便一目了然地看出此共享定义的起止位置。注释应具有描述性，但不应向潜在入侵者透露过多信息。例如，到目前为止，你可能拥有以下内容：

```
[ProjectP]
comment = Documents needed by ProjectP staff
```

7. 接下来通常是 **path** 选项。在此，你设置想要共享的文件的文件系统位置。请尽可能隔离此目录，以便人们无法访问他们本不应看到或接触的文件。例如，定义现在可能类似于以下内容：

```
[ProjectP]
comment = Documents needed by ProjectP staff
path = /Projects/P/
```

8. 从这一点开始，"典型"的共享定义不再保持一致性。从这里开始，大多数共享都互不相同，因此你可以稍微自由一些。表 18.6 中列出了你可能想要利用的选项列表。请仔细检查此列表。

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_570_0.png)

表 18.6 在单独的 Samba 共享定义中常用的选项。

| 选项 | 用途 | 值 | 示例 |
| :--- | :--- | :--- | :--- |
| **admin users** | 设置一组用户，这些用户以类似超级用户的权限访问此共享。使用此选项会带来强烈的安全影响，因为不仅允许定义的用户拥有清空共享、更改权限等权力，而且如果入侵者使用其中一个账户获得访问权限，该入侵者可以按照自己的意愿修改文件。 | 空格分隔的用户列表 | **admin users = joe barb** |
| **browseable** | 指定是否允许 Samba 客户端在请求可用共享列表时看到此共享。 | **yes** 或 **no** | **browseable = yes** |
| **case sensitive** | 指定 Samba 是否将文件名处理为区分大小写，或完全忽略大小写。 | **yes** 或 **no** | **case sensitive = no** |
| **copy** | 告诉 Samba 从另一个共享复制所有参数，并覆盖此共享中重复的参数。 | 不带括号的共享名称 | **copy = ProjectB** |
| **default case** | 设置客户端创建的文件名的默认大小写。 | **upper** 或 **lower** | **default case = lower** |
| **dont descend** | 明确拒绝允许 Samba 客户端访问特定的子目录。 | 逗号分隔的子目录列表 | **dont descend = /Projects/ProjectB/needs_approval** |
| **follow symlinks** | 告诉 Samba 是否跟随指向共享外部的符号链接。 | **yes** 或 **no** | **follow symlinks = no** |
| **force group** | 将所有访问此共享的用户设置为属于列出的组。 | 组名，或者如果你希望只有已分配到该组的用户才能以该组名称创建文件，则使用 **+group** | **force group = project_staff** |
| **force user** | 在客户端正确认证后，将所有访问此共享的用户设置为此特定用户名。 | 用户名 | **force user = staff** |
| **guest account** | 设置用于来宾登录的用户账户。 | 账户名称；通常，这应该是一个没有正常 shell 访问权限的账户 | **guest account = smbguest** |
| **guest ok** | 允许未经身份验证的登录，并将所有没有有效登录凭据的客户端分配给来宾账户。 | **yes** 或 **no** | **guest ok = yes** |
| **guest only** | 指定如果 **guest ok** 设置为 **yes**，则访问此共享的所有客户端都将通过来宾账户登录。 | **yes** 或 **no** | **guest only = yes** |
| **hide files** | 设置特定文件可访问，但不会出现在文件列表中。 | 斜杠分隔的文件列表，可用通配符 `*` 和 `?`，以及表 18.3 中列出的替换变量 | **hide files = master_data/master*/temp?*** |
| **hosts allow** | 提供访问控制，使你能够微调谁被允许挂载此共享。如果主机被明确允许，即使列在 **hosts deny** 中，也不会被拒绝。 | 逗号、空格或制表符分隔的主机标识符列表，如第 9 章中 /etc/hosts.allow 的描述 | **hosts allow = .colors.org** |
| **hosts deny** | 提供访问控制，使你能够微调谁被允许挂载此共享。 | 逗号、空格或制表符分隔的主机标识符列表，如第 9 章中 /etc/hosts.deny 的描述 | **hosts deny = ALL** |
| **invalid users** | 指定无法登录此共享的用户。 | **用户名；@group** 用于 NIS netgroups 和标准用户组，**+group** 用于标准用户组，**&group** 用于 NIS netgroups | **invalid users = root, wheel, @admin** |
| **locking** | 启用对客户端正在打开编辑的文件设置锁。 | **yes** 或 **no** | **locking = yes** |
| **mangle case** | 设置是否更改与 **default case** 不匹配的文件名。 | **yes** 或 **no** | **mangle case = no** |
| **mangled map** | 稍微修改 SMB 客户端请求和放置的文件名。 | 要更改的项目，允许使用星号通配符；格式为 **(one other)** | **mangled map = (*.html *.htm)** |
| **mangled names** | 设置是否将非 DOS 格式的文件名转换为 DOS 格式。 | **yes** 或 **no** | **mangled names = no** |
| **max connections** | 设置可以连接到此服务的最大客户端数量。 | 客户端数量，或 0 表示无限 | **max connections = 5** |
| **oplocks** | 启用机会性文件锁的使用，以确保在其他人修改文件时，文件不能被修改。 | **True** 或 **False** | **oplocks = True** |
| **postexec** | 设置当客户端断开与此服务的连接时在服务器上运行的命令或脚本。 | 命令路径，使用表 18.3 中列出的标准替换 | **postexec = /root/bin/leave.scr** |
| **preexec** | 设置当客户端连接到此服务时在服务器上运行的命令或脚本。 | 命令路径，使用表 18.3 中列出的标准替换 | **preexec = /bin/fortune** |

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_572_0.png)

