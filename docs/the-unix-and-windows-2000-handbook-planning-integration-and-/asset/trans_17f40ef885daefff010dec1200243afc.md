

![](img/415c89a1ede71e11e5040a0038b6916c_520_0.png)

Figure 12.5 WSM users.

## UNIX GROUPS

UNIX 的创始原则之一是能够在用户之间轻松共享文件。如第 11 章所述，UNIX 中的每个文件都能够允许用户、组或其他实体访问。虽然用户级访问只允许一个用户访问文件，但组访问允许组成员拥有该权限。通过使用组权限，文件所有者可以授予给定 UNIX 组中的所有用户子集对任何文件的读、写和/或执行访问权限。以下是标准的 Solaris /etc/group 文件：

```
root::0:root
other::1:
bin::2:root,bin,daemon
sys::3:root,bin,sys,adm
adm::4:root,adm,daemon
uucp::5:root,uucp
mail::6:root
tty::7:root,tty,adm
lp::8:root,lp,adm
```

```
nuucp::9:root,nuucp
staff::10:
daemon::12:root,daemon
sysadmin::14:
nobody::60001:
noaccess::60002:
nogroup::65534:
```

/etc/group 文件中的每一行代表一个不同的组，每个元素在表 12.6 中标识。

一个典型的组条目看起来像这样：

```
math101::150:jsmith,rjones,mbrown,bwhite
```

组 math101 有四个用户，没有密码。该组中的每个用户都可以读取、写入或执行他们可以访问的任何具有组权限的文件。例如：

```
-rw-r---- 1 jsmith math101 810 Aug 18 20:29 answerkey
```

文件 answerkey 虽然由 joeuser 所有，但组 math101 可以读取，但世界不能读取。将权限更改为：

```
-rw-rw---- 1 jsmith math101 810 Aug 18 20:29 answerkey
```

将允许组 math101 中的用户编辑文件，而所有用户都可以读取文件。要为文件分配组所有权，使用 chgrp 程序：

```
chgrp math101 answerkey
```

| Table 12.6 Group Entry Description |  |
|---|---|
| Field (in order) | Description |
| Group Name | An eight-character string consisting of only alphanumeric (numbers or letters) characters. A group must begin with an alphabetic character, and all characters are case-insensitive. |
| Password Field | An empty field represents no password for group use. If a password exists, a user will be prompted for a password to change to that group. |
| Group ID (GID) | Group ID for the group. The range is from 0 to 2147483647, but it is recommended you keep this number below 60000 if you plan to interact with other operating systems. |
| List of Group Members | A comma-separated list of usernames that are members of the group. |

要确定用户的组成员，作为 root 或作为该用户，运行 groups 命令：

```
# groups jsmith
students math101
```

这表明 jsmith 是 groups students 和 math101 的成员。

## Default Group

每个用户都有一个默认组，将分配给他们创建的每个文件。由于用户可以是任意数量的 UNIX 组的成员，因此文件仅创建时分配默认组的所有权。要确定用户的默认组，运行 id 命令：

```
# id -a jsmith
uid=1001(jsmith) gid=14(students) groups=100(students),150(math101)
```

在此示例中，gid 标识用户 jsmith 所属的默认组。登录后，jsmith 只能在组 students 中创建组文件。然而，只要权限正确，jsmith 就可以与任何具有 math101 所有权的文件交互。能够使用适当的组创建文件很方便，特别是如果你要创建许多文件。虽然使用 chgrp 命令是一个选项，但作为用户 jsmith 使用 newgrp 命令：

```
#newgrp math101
```

将为该 shell 实例将 jsmith 设置为默认组的新组：

```
# id -a jsmith
uid=1001(jsmith) gid=150(math101) groups=100(students),150(math101)
```

要返回默认组，输入 newgrp students，或退出当前登录 shell。

groups—Lists the groups of which the supplied user is a member.

![](img/415c89a1ede71e11e5040a0038b6916c_522_0.png)

## USER STARTUP FILES AND THE HOME DIRECTORY

密码文件中指定的 shell 在用户登录时加载。shell（以及一些其他 UNIX 实用程序）可以用与该 shell 或实用程序关联的启动文件进行配置。表 12.7 列出了关联的启动文件

