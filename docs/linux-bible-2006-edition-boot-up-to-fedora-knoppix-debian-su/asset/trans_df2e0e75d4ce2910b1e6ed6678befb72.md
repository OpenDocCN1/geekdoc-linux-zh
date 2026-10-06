

# 创建用户账户

每个使用你 Linux 系统的人都应该有一个独立的用户账户。拥有用户账户可以为每一个人提供一个安全存储文件的区域，并能够定制其用户界面（GUI、路径、环境变量等），以适应其使用计算机的习惯。

你可以通过多种方式向大多数 Linux 系统中添加用户账户——例如，Red Hat 系统使用 `redhat-config` 工具，而 SUSE 则使用 YaST 中的另一个设置模块。本章描述了如何使用 `useradd` 命令从命令行添加用户账户，因为大多数 Linux 系统都包含该命令。

# 使用 useradd 添加用户

从 shell 创建新用户最直接的方法是使用 `useradd` 命令。在打开具有 root 权限的终端窗口后，只需在命令行提示符下调用 useradd，新账户的详细信息作为参数即可。

唯一要求的参数是用户的登录名，但你可能在此之前包含一些额外信息。每项账户信息之前都有一个带连字符的单字母代码。表 4-2 列出了 `useradd` 可用的选项。

| 选项 | 描述 |
| --- | --- |
| -c comment "comment here" | 为新用户账户提供描述。通常是该者的全名。将 comment 替换为用户账户名（-c jake）。使用引号输入多个单词（-c jake jackson）。 |
| -d home_dir | 为账户设置主目录。默认是以登录名命名并将其放置在 /home 中。将 home_dir 替换为要使用的目录名称（例如，-d /mnt/homes/jake）。 |
| -D | 不创建新账户，而是将所提供的信息保存为任何创建的新账户的默认设置。 |
| -e expire_date | 为账户分配 MM/DD/YYYY 格式的过期日期。将 expire_date 替换为你想使用的日期（-e 05/06/2005）。 |
| -f -1 | 设置密码过期后到账户被永久禁用之间的天数。默认值 -1 表示禁用此选项。将此项设置为 0 则在密码过期后立即禁用账户。将 -1 替换为要使用的数字数。 |
| -g group | 设置新用户所属的主组（如 /etc/group 文件中列出的）。将 group 替换为组名（-g wheel）。 |
| -G grouplist | 将新用户添加到用户逗号分隔的组列表中（-G wheel,sales,tech,lunch）。 |
| -k skel_dir | 设置包含初始配置文件和登录脚本的骨架目录，这些文件将被复制到新用户的目录中。此参数只能与 -m 选项配合使用。将 skel_dir 替换为要使用的目录。（如果没有此选项，将使用 /etc/skel 目录。） |
| -m | 自动创建用户主目录，并将骨架目录 (/etc/skel) 中的文件复制到其中。 |
| -M | 不创建新用户的主目录，即使默认行为是创建它。 |
| -n | 关闭创建与新用户名和 ID 匹配的新组的默认行为。此选项在 Red Hat Linux 系统可用。其他 Linux 系统通常将用户分配到名为 users 的组。 |
| -u uid | 使用 uid 创建一个与其他用户名具有相同 UID 的账户。（这实际上让你拥有两个对同一组文件和目录具有权限的不同用户名）。 |
| -p passwd | 为你正在添加的账户输入密码。这必须是一个加密密码。与其在此处添加加密密码，不如直接使用 `passwd` 用户命令为用户添加密码。 |
| -s shell | 指定此账户使用的命令。将 shell 替换为命令 shell（-s bash）。 |
| -u user_id | 为账户指定用户 ID（-u 474）。如果没有 -u 选项，默认行为是自动分配下一个可用数字。将 user_id 替换为该数字数字（-u）。 |

例如，让我们为新用户 Mary Smith 创建一个登录名为 mary 的账户。首先，以 root 登录，然后输入以下命令：

```bash
# useradd -c "Mary Smith" mary
```

![](img/a2d958d7eab32ca5b89b2b8af808aa70_176_0.png)

当你选择用户名时，不要以数字开头（例如 06jsmith）。此外，最好使用所有小写字母，不要控制字符或空格，且最大为 8 个字符。useradd 允许最多 32 个字符，但某些应用程序无法处理那么长的用户名。如果名称太长，ps 等工具会显示 ID 而不是名称。拥有名为 Jsmith 和 jsmith 的用户可能会导致不区分大小写的程序（如 sendmail）产生混乱。

接下来，使用 `passwd` 命令设置 Mary 的初始密码。系统会提示输入密码单词：

```bash
# passwd mary
Changing password for user mary.
New password: *******
Retype password: *******
```

（此示例中的星号代表你输入的密码。输入密码时实际上实际上不会显示任何内容。）

在为 Mary 创建账户时，useradd 命令执行了若干操作：

- 读取 /etc/login.defs 文件以获取创建账户时的默认值。
- 检查命令行参数以确定要覆盖哪些值。
- 根据默认值和命令行参数在 /etc/passwd 和 /etc/shadow 文件中创建新的用户条目。
- 在 /etc/group 文件中创建任何新组条目（Red Hat 使用用户名创建组；Gentoo 将用户添加到 users 组；SUSE 将其添加到你为新用户设置的每个组，如 dialout、audio、video 和其他服务）。
- 根据用户名在 /home 目录下创建一个主目录。
- 将位于 /etc/skel 中的任何文件复制到新的主目录中。这通常包括登录和应用程序脚本。

前面的示例仅使用了部分可用的 useradd 选项。如果你需要，可以显式地设置更多值；这里有一个使用更多选项的示例：

```bash
# useradd -g users -G wheel,sales /bin/tcsh -c "Mary Smith" mary
```

在这种情况下，useradd 被告知将 users 设置为主组 (-g)，并将她加入 wheel 和 sales 组，同时将 tcsh 指定为她的主 shell (-c)。默认在用户名下创建一个主目录 (/home/mary)。该命令会导致在 /etc/passwd 文件中添加类似于下面所示的行：

```text
mary:x:50100:Mary Smith:/home/mary:/bin/tcsh
```

/etc/passwd 文件中的每一行代表一个单一的用户账户记录。每个字段之间用冒号 (:) 字符隔开。字段在序列中的位置决定了它的含义。如你所见，登录名在第一个。再次，密码字段包含一个 x，因为我们使用影子密码文件存储加密密码数据。用户 ID 由 501 选择。组 ID 是 100，对应于 /etc/group 文件中的 users 组。注释字段被正确设置为 Mary Smith，主目录被自动分配为 /home/mary，命令 shell 被分配为 /bin/tcsh，完全按照 useradd 选项中指定的那样。

通过省略许多选项（如我在第一个 useradd 示例中做的那样），在大多数情况下会分配默认值。例如，在 Red Linux 中不使用 -u -G wheel,sales，将创建一个名为 mary 的组并分配给新用户。其他 Linux 系统分配 -s /bin/tcsh 会导致默认将 /bin/bash 分配给组。同样，

/etc/group 文件存储了关于你 Linux 系统上的不同组及其所属用户的信息。组对于允许多个用户共享相同文件而拒绝他人访问非常有用。查看 /etc/group 文件，你发现了类似以下的内容：

```text
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin,adm
adm:x:4:root,adm,daemon
tty:x:5:
disk:x:6:root
lp:x:7:daemon,lp
mem:x:8
kmem:x:9:
wheel:x:10:root,joe.mary

nbody:x:99
users:x:100
chris:x:500
shee:x:501
sales:x:601:bob.jane,jane,mary
```

组文件中的每一行包含组名、与其关联的组 ID 数字以及该组的用户列表。默认情况下，每个用户被添加到其或自己的组中，从 GID 500 开始。注意，mary 被添加到 wheel 和 sales 组，而不是她自己的组。

