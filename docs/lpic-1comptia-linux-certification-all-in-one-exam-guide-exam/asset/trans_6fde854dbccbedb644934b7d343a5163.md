
登录完成后，系统会为你的用户创建唯一的系统环境。如图 9-2 所示，ksanders 用户已登录到本地系统。她的自定义桌面偏好设置已加载，并且她已被授予对 /home/ksanders 中其主目录的访问权限。

如果另一个用户登录到同一系统，则加载的是该用户的偏好设置，而不是 ksanders 的偏好设置。同样，该用户也会被授予访问其主目录的权限。一个需要牢记的重要点是：保存在某用户主目录中的文件受保护，系统上的所有其他用户均无法访问。例如，如果 ksanders 在 /home/ksanders 中保存文件，则该系统上的 tux 用户将无法访问这些文件。

默认情况下，所有用户的主目录都在 /home 目录下创建和维护。例如，在图 9-3 中，Linux 系统上创建了两个用户账户：tux 和 ksanders。

这两个用户都在 /home 中创建了主目录。不过，这一规则有一个例外。请记住，所有 Linux 系统都使用一个名为 root 的超级用户账户。请注意，在图 9-3 中，/home 下并没有为 root 用户账户创建主目录。root 是无家可归的吗？实际上并非如此。root 用户账户也有一个主目录。然而，它并不在 /home 中维护。相反，root 用户的主目录位于

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_376_0.png)

图 9-2 ksanders 的系统环境

/root。如果你仔细查看图 9-3，你会发现文件系统顶部有一个名为 root 的目录。这就是 root 的主目录，当然，只有 root 才能访问它。

你可以使用 shell 提示符下的 `finger username` 命令查看系统中任何用户账户的信息。例如，如果我想查看 Linux 系统上 ksanders 账户的信息，我会输入 `finger ksanders`。执行该命令后，将显示关于 ksanders 账户的有用信息，如下所示：

```
wsl:~/Desktop # finger ksanders
Login: ksanders          Name: Kimberly Sanders
Directory: /home/ksanders     Shell: /bin/bash
Last login Thu Mar 10 16:44 (MST) on :0 from console
No Mail.
No Plan.
```

请注意，`finger` 显示了关于 ksanders 账户的以下信息：

- **Login**：这是用于向系统进行身份验证的用户名。
- **Name**：这是用户的完整姓名。
- **Directory**：这是用户的主目录。
- **Shell**：这是由用户启动的默认 shell。
- **Last Login**：这显示了用户上次登录的时间及来源。

除了被分配主目录和默认 shell 之外，每个用户账户在创建时还会被分配一个唯一的用户 ID (UID) 号。系统中的两个用户账户不会具有相同的 UID。要在 shell 提示符下查看特定用户账户的 UID，可以使用 `id username` 命令。例如，要查看 tux 用户账户的信息，可以在 shell 提示符下输入 `id tux`。该命令的输出如下：

```
wsl:~/Desktop # id tux
uid=1000(tux) gid=100(users) groups=100(users),33(video)
```

请注意，在该系统上，tux 用户账户被分配了 UID 1000。在 SUSE Linux 系统中，系统上创建的第一个常规用户账户总是被分配 UID 1000。下一个用户账户将被分配 UID 1001，依此类推。然而，其他发行版可能使用不同的 UID 编号方案。例如，Fedora 系统中的 UID 从 500 开始，而不是 1000。接下来，你可以看到在该 Fedora 系统上，rtracy 用户的 UID 为 500，因为它是创建的第一个标准用户账户：

```
[root@fs3 ~]# id rtracy
uid=500(rtracy) gid=500(rtracy) groups=500(rtracy)
```

请注意，前面段落中指的是分配给标准用户账户的 UID。那么 root 用户呢？在大多数 Linux 发行版中，root 用户账户总是被分配 UID 0。如下所示：

```
[root@fs3 ~]# id root
uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon),3(sys),4(adm),6(disk),10(wheel)
```

操作系统实际使用的是 UID 来控制对文件系统中文件和目录的访问。我们将在后续章节中更详细地讨论这一点。然而，目前我们需要讨论的是 Linux 用户账户在系统中的存储位置。下面让我们继续探讨这个问题。

## Linux 用户账户的存储位置

Linux 是一个非常灵活的操作系统。其灵活特性之一是系统中用户账户的位置。当你最初安装系统时，你的发行版可能提供了几个选项，让你选择希望将用户账户存储在哪里。例如，图 9-4 显示了 SUSE Linux Enterprise Server 安装程序中的用户身份验证方法选择屏幕。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_377_0.png)

图 9-3 /home 中的用户账户

请注意，此屏幕允许你从以下身份验证方法中进行选择：

- **Local**：此选项将用户账户存储在 /etc/passwd 文件中。这是多年来 Linux 系统使用的默认配置。
- **LDAP**：这是许多 Linux 管理员开始越来越多地采用的一种选项。与将用户账户存储在文件系统中的文件不同，用户账户存储在目录服务中，并通过轻量级目录访问协议 (LDAP) 进行访问。与将账户存储在简单平面文件中的本地身份验证不同，目录服务具有层次结构，允许你按位置、功能或部门对用户账户进行分类和组织。目录数据库还可以在不同的 Linux 系统之间复制，提供容错能力。此选项的关键优势是，它允许你维护一组单一的用户账户，可用于向许多不同的 Linux 系统进行身份验证。
- **NIS**：此选项代表*网络信息服务* (Network Information Service)。当拥有多个需要相同用户账户的系统时，NIS 也旨在提供集中的用户账户管理。为此，NIS 将所有系统配置为使用通用的 passwd 和 shadow 文件。
- **Windows Domain**：如果你的网络中有 Windows 域控制器（或运行 Samba 服务的其他 Linux 服务器），你可以配置 Linux 系统使用域中的用户账户来对本地系统进行身份验证。

> **注意**：本质上，LDAP 选项使 Linux 朝着使用本地身份验证的其他服务器操作系统方向发展，例如 Novell 的 eDirectory 或 Microsoft 的 Active Directory。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_378_0.png)

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_379_0.png)

> **考试提示**：为了参加 LPIC-1/CompTIA Linux+ 考试，你需要关注 Local 选项。所有 Linux 发行版都可以使用 `/etc/passwd` 和 `/etc/shadow` 文件进行身份验证。

这些选项中哪一个最好？这取决于你需要系统做什么。如果系统是一个独立的工作站，Local 选项通常就足够了。你也可以选择使用 LDAP 选项。

如果系统将在一个网络中参与，其中许多不同的用户需要访问该系统，那么你可能需要考虑使用 LDAP、NIS 或 Windows Domain 身份验证。

在此处，我们将关注 Local 选项。此选项在文件系统的以下文件中存储用户和组信息：

- `/etc/passwd`：该文件包含系统的用户账户信息。
- `/etc/shadow`：该文件包含用户账户的密码。
- `/etc/group`：该文件包含系统的组。（我们将在本章后面讨论组。）

让我们先看看 `/etc/passwd` 文件。

337

## /etc/passwd 文件

如果配置为使用本地身份验证，/etc/passwd 文件包含系统的用户账户。系统中的每个用户账户都由文件中的单行表示，如下例所示：

```
ws1:~ # cat /etc/passwd
...
root:x:0:0:root:/root:/bin/bash
sshd:x:100:102:SSH daemon:/var/lib/sshhd:/bin/false
ucup:x:10:14:Unix-to-Unix CoPy system:/etc/ucup:/bin/bash
wwwrun:x:30:8:WWW daemon apache:/var/lib/wwwrun:/bin/false
ksanders:x:1001:100:Kimberly Sanders:/home/ksanders:/bin/bash
tux:x:1000:100:Tux Pengquin:/home/tux:/bin/bash
```

每个账户记录由行中几个不同的字段组成，由冒号 (:) 分隔。它们按以下方式组织：

`Username:Password:UID:GID:Full_Name:Home_Directory:Default_Shell`

例如：

`ksanders:x:1001:100:Kimberly Sanders:/home/ksanders:/bin/bash`

这些字段包含的内容如下：

- **Username**：Username 字段仅标识用户在登录系统时提供的用户名。在此示例中，它是 *ksanders*。
- **Password**：这是一个遗留字段。曾经，用户的密码以加密形式存储在 passwd 文件的该字段中。然而，出于安全原因，密码已从 /etc/passwd 移至 /etc/shadow。（我们稍后会更详细地查看该文件。）因此，该字段中仅显示字符 *x*。
- **UID**：这是用户账户的用户 ID。我们之前在本章中讨论了 UID。在此示例中，*ksanders* 账户的 UID 为 1001。
- **GID**：此字段引用用户默认组的组 ID 号。在此示例中，*ksanders* 账户的 GID 为 100。正如我们将在本章后面看到的那样，这引用的是 users 组。
- **Full_Name**：此字段包含用户的完整姓名。在此示例中，它是 Kimberly Sanders。
- **Home_Directory**：此字段包含用户主目录的路径。在这种情况下，主目录是 /home/ksanders。
- **Default_Shell**：此字段指定默认使用的 shell。对于 *ksanders*，这是 /bin/bash (Bourne-Again Shell)。

实际上，在任何 Linux 系统的 /etc/passwd 文件中都列出了许多用户账户，即使你只创建了一两个账户。所有其他用户账户都是系统用户账户。这里显示了三个系统用户账户的示例：

```
sshd:x:100:102:SSH daemon:/var/lib/sshhd:/bin/false
ucup:x:10:14:Unix-to-Unix CoPy system:/etc/ucup:/bin/bash
wwwrun:x:30:8:WWW daemon apache:/var/lib/wwwrun:/bin/false
```

