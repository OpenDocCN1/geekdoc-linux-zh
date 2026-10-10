

如本章节前面“用户名规则”部分所述，用户名应由小写字母和数字组成。*全名*通常指用户的真实姓名，但如果你愿意，也可以在此处存储其他信息。然后程序会询问与外壳（shells）、主目录（home directories）、用户 ID（UID）以及组归属相关的问题：

```
Enter shell bash csh dash ksh no nosh sh tcsh zsh [sh]: **ksh**
Enter home directory (full path) [/home/marie]:
Uid [1003]:
Enter login class: default []:
Login group marie [marie]:
Login group is ``marie''. Invite marie into other groups: guest no [no]: **users**
```

对于其中大多数选项，你可以按 ENTER 键选择默认值，正如本示例中对大多数响应所做的那样。不过，在这个示例中，*marie* 被赋予了非默认的 *ksh* 外壳，并且除了 *marie* 组之外，还被添加到了 *users* 组中。最后一个选项值得特别说明。默认情况下，*adduser* 会为每个用户创建一个专门的组。创建时，该组仅包含该用户本人，但你也可以将其他用户添加到该组中。这是一种有用的账户安全措施，但并非唯一的方法。本选项以及其他选项将在接下来的章节“确定组策略”中详细描述。如果你不想采用这种方法，可以在 *Login group* 提示处输入一个现有组的名称。

账户创建过程的下一阶段会提示输入若干与密码相关的选项：

```
Use password-based authentication (y/n) [y]:
Use an empty password (y/n) [n]:
Enter password []:
Enter password again []:
Enable account password at creation (y/n) [y]:
```

在本示例中，除了密码部分（在 *Enter password* 和 *Enter password again* 提示处），所有选项都选择了默认值，这是通常的配置方式。尽管本示例中未显示，因为密码不会回显到屏幕上，但相同的密码被输入了两次。输入两次可以降低因拼写错误而导致账户无法使用的风险，从而避免后续需要超级用户干预。输入密码信息后，*adduser* 会要求你验证目前为止输入的信息。

```
Name: marie
Password: ****
Fullname: Marie Curie
Uid: 1003
| Field | Value |
| :--- | :--- |
| Gid: | 1003 (marie) |
| Class: | |
| Groups: | marie users |
| HOME: | /home/marie |
| Shell: | /usr/local/bin/ksh |
| OK? (y/n) [y]: | **y** |
```

如果你输入 `n`，adduser 将返回以重新收集信息。如果你输入 `y`，adduser 将创建账户。然后它会提示你提供有关它向新建账户发送的电子邮件的信息：

```
Added user ``marie''
Send message to ``marie'' and: no root second_mail_address
[no]: charlesd@pangaea.edu

Marie Curie,

your account ``marie'' was created.
Have fun!

See also chpass(1), finger(1), passwd(1)

Add anything to default message (y/n) [n]: n
Send message (y/n) [y]: y
Add another user? (y/n) [y]: n
```

系统会询问你是否要将欢迎邮件的副本发送到其他任何地址。默认响应为“否”，这意味着邮件不会发送给其他人。相反，你可以输入 `root` 将邮件发送到 `root` 账户，或者任何其他电子邮件地址（例如此处显示的 `charlesd@pangaea.edu`）。系统显示消息，其默认内容并不是特别具有信息量——毕竟，任何能阅读该消息的用户可能都知道该账户的存在。此消息存储在 `/etc/adduser.message` 中，因此你可以将其编辑为更有用的内容，例如解释本地策略的消息。你还可以针对每个用户在默认消息中添加信息。如果你愿意，也可以选择不发送该消息。最后，`adduser` 会询问你是否要添加另一个用户。如果你回答 `n`，它退出；如果你回答 `y`，它重新开始该过程。

`adduser` 命令接受各种选项，这些选项会覆盖存储在 `/etc/adduser.conf` 中的默认值。例如，`-home homedir` 将主目录的基础目录（通常是 `/home`）设置为你指定的其他内容。由于这些选项会覆盖你被提示输入的项目，因此很少需要使用它们。一个例外是 `-config_create`，它会创建新的默认配置文件。你可以查阅 adduser 的手册页以获取有关这些选项的更多信息。

## 修改用户账户

在一个理想的世界中（从系统管理的角度来看），一旦创建了账户，你就可以不再管它了。不幸的是，情况往往并非如此。你可能需要更改已为某账户输入的一些信息。一种特别常见的变更类型是密码。良好的安全实践是经常更改密码，以最小化密码落入错手时可能造成的损害。（具体频率取决于你的环境。某些高安全环境可能要求使用一次性密码，这些密码在使用后即失效。低安全环境可能每隔几个月更改一次即可。）了解密码的工作原理、如何更改密码以及如何更改其他账户信息，对于账户管理至关重要。

## 理解影子密码

在 UNIX 的早期年份，密码与其他信息一起存储在 `/etc/passwd` 文件中。各种程序需要此文件中的信息——例如，显示系统用户信息的 `finger` 守护进程必须能够从该文件中读取用户的真实姓名。因此，该文件对所有人可读。这种系统曾被视为可接受，因为如前文“账户和组数据结构”部分所述，密码是通过哈希加密的。不幸的是，随着计算机速度和磁盘容量的增长，存储整个字典的哈希并将这些条目与 `/etc/passwd` 文件条目进行比对成为可能。弱密码很容易被这种技术发现。

解决此问题的部分方法是说服用户选择好的密码，但这项任务以困难著称。另一部分解决方案是将密码从 `/etc/passwd` 文件中移出，放入另一个更安全的文件中。在 FreeBSD 中，这是 `/etc/master.passwd` 文件及其关联的数据库格式变体 `/etc/spwd.db`。这些文件包含与其原始对应文件相同的信息，但它们仅可由 `root` 读取。相反于在 `/etc/passwd` 中放入密码，密码字段包含一个星号（`*`），这表明密码存储在安全文件中。

这种密码安全方法被称为*影子密码*。（在其他操作系统中，其实现方式并非总是完全一致，但关键点在于密码存储在仅 `root` 可读的文件中，这是不变的。）普通程序保留对 `/etc/passwd` 的访问权限，这对某些用途是必需的，而只有以 `root` 身份运行的程序才能读取密码。虽然这种方法并不提供完美的安全性；如果破解者甚至能获得有限的 `root` 访问权限，影子密码文件就容易被盗取。不过，影子密码是 FreeBSD 密码安全的重要组成部分。

## 使用 `passwd`

当你通过 `sysinstall` 或 `adduser` 创建账户时，系统会提示你为该账户输入密码。不过，有时你或账户所有者必须更改该密码。例如，你可能会鼓励或要求用户定期更改密码，以降低密码被泄露的风险。更改密码的常用工具是 **`passwd`**。该命令的语法相当简单：

```
passwd [-l] [user]
```

通常，FreeBSD 的 **`passwd`** 在本地更改密码，如果系统配置为 Kerberos 领域的一部分，它也会更改 Kerberos 密码。**`-l`** 选项会更改此行为，使得仅更改本地密码。

> **注意**
> Kerberos 是一种分布式身份验证系统，正在托管许多服务器或允许用户登录到多台工作站的网络上变得流行。不过，其特性的讨论超出了本书的范围。如需更多信息，请查阅 Kerberos 网页，http://web.mit.edu/kerberos/www/。

只有 **root** 可以使用 **`user`** 选项，该选项允许超级用户指定要更改密码的用户。因此，在大多数情况下，普通用户可以如下使用 **`passwd`**：

```
$ passwd
Changing local password for marie.
Old password:
New password:
Retype new password:
passwd: updating the database...
passwd: done
```

该程序提示输入旧密码作为一种安全措施，以确保它没有被未授权的人员调用——例如，如果账户所有者离开终端未加看管，而恶棍找到了该终端。然后它提示两次输入新密码并报告其状态。这三个密码都不会回显到屏幕上，以防被路人读取。

当 **root** 使用 **`passwd`** 时，程序不会提示输入旧密码。此功能允许超级用户在不知道旧密码的情况下更改普通用户的密码。此功能在用户忘记密码时非常有用——用户可以去找系统管理员，管理员可以输入新密码。

### 使用 chpass

另一个在调整账户行为时有用的工具是 **`chpass`**。该程序允许你更改账户的各种特性，包括密码、账户过期日期和默认外壳。其语法为：

```
chpass [-a list] [-p encpass] [-e expiretime] [-s newshell] [user]
```

