
有时 `sysinstall` 并不足够。例如，如果您需要添加许多用户，您可能更愿意编写一个脚本来完成这项工作，而 `sysinstall` 与脚本的配合并不好。您可能也不愿意在 `sysinstall` 的菜单中摸索。在这种情况下，存在一个更简单但更强大的工具：`adduser`。该程序使用标准输入和输出以相当严格的顺序提示您输入信息，因此，如果您想以半自动化的方式创建账户，可以按照第 5 章所述，使用重定向从脚本中调用它。

第一次运行 `adduser` 时，程序试图访问其配置文件 `/etc/adduser.conf`，但在标准安装中此文件不存在。因此，程序会运行其大部分选项（如稍后所述）以获取默认值。您可以按 ENTER 接受其中大部分的默认值。如果您决定稍后更改它们，您可以编辑 `adduser.conf` 或删除该文件并再次运行 `adduser` 以生成新的默认值。

在生成 `adduser.conf` 之后，或当您运行该程序时，它开始提示您输入信息。第一个信息与用户名和用户身份有关：

```bash
# adduser
Use option '--verbose' if you want to see more warnings and
questions or try to repair bugs.

Enter username [a-z0-9_-]: marie
Enter full name []: Marie Curie
```

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

如果你输入 `n`，`adduser` 将返回以重新收集信息。如果你输入 `y`，`adduser` 将创建账户。然后它会提示你提供有关它向新建账户发送的电子邮件的信息：

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

`adduser` 命令接受各种选项，这些选项会覆盖存储在 `/etc/adduser.conf` 中的默认值。例如，`-home homedir` 将主目录的基础目录（通常是 `/home`）设置为你指定的其他内容。由于这些选项会覆盖你被提示输入的项目，因此很少需要使用它们。一个例外是 `-config_create`，它会创建新的默认配置文件。你可以查阅 `adduser` 的手册页以获取有关这些选项的更多信息。

## 修改用户账户

在一个理想的世界中（从系统管理的角度来看），一旦创建了账户，你就可以不再管它了。不幸的是，情况往往并非如此。你可能需要更改已为某账户输入的一些信息。一种特别常见的变更类型是密码。良好的安全实践是经常更改密码，以最小化密码落入错手时可能造成的损害。（具体频率取决于你的环境。某些高安全环境可能要求使用一次性密码，这些密码在使用后即失效。低安全环境可能每隔几个月更改一次即可。）了解密码的工作原理、如何更改密码以及如何更改其他账户信息，对于账户管理至关重要。

## 理解影子密码

在 UNIX 的早期年份，密码与其他信息一起存储在 `/etc/passwd` 文件中。各种程序需要此文件中的信息——例如，显示系统用户信息的 `finger` 守护进程必须能够从该文件中读取用户的真实姓名。因此，该文件对所有人可读。这种系统曾被视为可接受，因为如前文“账户和组数据结构”部分所述，密码是通过哈希加密的。不幸的是，随着计算机速度和磁盘容量的增长，存储整个字典的哈希并将这些条目与 `/etc/passwd` 文件条目进行比对成为可能。弱密码很容易被这种技术发现。

解决此问题的部分方法是说服用户选择好的密码，但这项任务以困难著称。另一部分解决方案是将密码从 `/etc/passwd` 文件中移出，放入另一个更安全的文件中。在 FreeBSD 中，这是 `/etc/master.passwd` 文件及其关联的数据库格式变体 `/etc/spwd.db`。这些文件包含与其原始对应文件相同的信息，但它们仅可由 `root` 读取。相反于在 `/etc/passwd` 中放入密码，密码字段包含一个星号（`*`），这表明密码存储在安全文件中。

这种密码安全方法被称为*影子密码*。（在其他操作系统中，其实现方式并非总是完全一致，但关键点在于密码存储在仅 `root` 可读的文件中，这是不变的。）普通程序保留对 `/etc/passwd` 的访问权限，这对某些用途是必需的，而只有以 `root` 身份运行的程序才能读取密码。虽然这种方法并不提供完美的安全性；如果破解者甚至能获得有限的 `root` 访问权限，影子密码文件就容易被盗取。不过，影子密码是 FreeBSD 密码安全的重要组成部分。

## 使用 `passwd`
