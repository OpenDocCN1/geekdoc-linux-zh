

## 将用户或组添加到 ACL

要将用户或组添加到 ACL，再次使用 `setfacl` 命令。例如，要授予用户 “foobar” 对文件 `acltest.txt` 的读取权限，可以使用以下命令：

```bash
setfacl -m u:foobar:r acltest.txt
getfacl acltest.txt
#file:acltest.txt
#owner:0
#group:0
user::rw-
user:foobar:r--
group::r--
mask::r--
other::---
```

如你所见，ACL 列表中已为 foobar 用户添加了一个条目。该用户现在将拥有该文件的读取权限，尽管标准的文件权限通常不会授予其权限。

那么，如果你尝试同时授予该用户写入和读取权限会发生什么？以下命令将授予 foobar 对该文件的读写权限：

```bash
setfacl -m u:foobar:rw acltest.txt
#file:acltest.txt
#owner:0
#group:0
user::rw-
user:foobar:rw-
group::r--
mask::rw-
other::---
```

`getfacl` 的输出显示，foobar 确实被授予了该文件的写入权限。请注意，掩码（mask）也已自动更新，以允许最大的读和写权限。如果此行为不可取（换句话说，你不希望更新掩码），在设置 ACL 时使用 `-n` 选项。例如，以下命令设置了一个 ACL，授予用户 foobar 对该文件的读写访问权限：

```bash
# setfacl -n -m u:foobar:rw acltest.txt
```

然而，此命令不会更新掩码，即使当前掩码不允许写入访问。

> **提示**
> 选项的顺序很重要。`-n` 选项必须位于操作选项之前（在本例中为 `-m`）。如果你颠倒这两个选项的顺序，将会出现以下错误：
> `setfacl: acl_from_text() failed: Invalid argument.`

> **注意**
> 请记住，如果你在不使用 `-n` 选项的情况下设置新 ACL，最大权限掩码将自动更新以允许相应权限。例如，如果掩码当前设置为允许最大只读权限，而你添加了一个允许用户读写权限的 ACL，掩码将自动更新以同时允许读和写权限。如果不想发生这种情况，请始终记得使用 `-n` 选项。

> **提示**
> 当不使用 `-n` 选项且掩码自动更新时，如果添加了一个权限大于当前掩码允许权限的新 ACL，掩码将增加权限。
> 掩码还会自动降低到支持 ACL 中所有条目所需的最小最大权限。例如，如果你删除了一个允许对特定用户进行读写访问的 ACL 条目，并且在删除该条目后，没有剩其他需要写入访问权限的条目，写入访问权限将自动从掩码中移除。正如你可以使用 `-n` 选项来防止掩码自动提升一样，你也可以使用该选项来防止掩码自动降低。

在授予 foobar 对文件的读写访问权限后，你的 ACL 现在应该如下所示：

```bash
#file:acltest.txt
#owner:0
#group:0
user::rw-
user:foobar:rw-
group::r--
mask::rw-
other::--
```

如果你想将掩码改回仅允许最大只读 ACL 权限，请使用以下命令：

```bash
# setfacl -m m::r acltest.txt
```

如果你再次运行 `getfacl` 命令，你将得到以下输出：

```bash
#file:acltest.txt
#owner:0
#group:0
user::rw-
user:fooBar:rw-          # effective: r--
group::r--
mask::r--
other::---
```

请注意，用户 `fooBar` 仍然列出了读和写权限。但是，由于掩码的存在，fooBar 的有效权限是只读。

你还可以通过用逗号分隔多个 ACL 条目，在一条命令中添加多个 ACL。以下是一个示例：

```bash
# setfacl -n -m u:fooBar:rw,g:guest:r,g:visitors:r acltest.txt
```

此命令授予用户 fooBar 读写访问权限，授予用户 guest 读取访问权限，并授予组 visitors 读取访问权限。此外，使用 `-n` 选项可防止更新掩码，即使当前掩码不允许你在此语句中分配的某些权限。

## 使用 ACL 拒绝访问

正如 ACL 可用于允许用户和组访问他们原本无法访问的文件或目录一样，它也可以用于拒绝原本拥有访问权限的用户和组。例如，以下命令为用户 fooBar 创建一个不包含任何权限的 ACL 条目：

```bash
# setfacl -m u:fooBar: acltest.txt
```

在这种情况下，用户 fooBar 被拒绝访问文件 `acltest.txt` 的所有权限，即使 fooBar 是拥有该文件的组的成员，且该组对该文件具有访问权限。ACL 压倒标准的文件权限，并拒绝用户访问，即使标准文件权限允许用户访问。

## 删除 ACL 条目

使用 `setfacl` 的 `-x` 选项来删除 ACL 条目。例如，以下命令移除了用户 fooBar 的整个条目：

```bash
# setfacl -x u:fooBar: acltest.txt
```

## 移除所有 ACL 条目

使用 `-b` 选项移除所有 ACL 条目。以下是一个示例：

```bash
# setfacl -b acltest.txt
```

有关 ACL 功能（包括为目录设置默认 ACL 的能力）的更多信息，请参阅 `getfacl` 和 `setfacl` 的 *man* 页面。

# 添加和删除用户

现在，在介绍了权限和所有权之后，我们需要将注意力转向扩展系统的用户基础，以包含更多的用户和组。

使用 `adduser` 脚本将用户添加到系统中。该程序的工作流程与你可能在 Linux 系统上习惯使用的 `adduser` 和 `useradd` 脚本略有不同，但它实现的是相同的目标。你必须是 root 才能运行 `adduser`。

第一次运行 `adduser` 时，脚本会设置一个包含默认值集合的配置文件；下次运行它时，你可以使用 `-s` (silent) 选项来使用这些默认值，脚本将只询问每个用户的基本详细信息。列表 9.2 展示了脚本初始运行的样本。

> **注意**
> 熟悉 FreeBSD 早期版本的用户应注意 `adduser` 脚本的新第一行，它提示你输入新用户名必须匹配的常规表达式。给出的默认常规表达式（将用户名限制为字母数字字符或下划线作为第一个字符，然后其余字符为相同的字符集加上连字符）通常是可取的。然而，这是脚本以前提示输入用户名的地方。不要被骗了！
> 如果你输入自定义的常规表达式，请确保你知道自己在做什么。所有未来的新用户名都必须匹配你在此处输入的模式。如果你意外输入了不可取的值，你可以删除或修改 `/etc/adduser.conf` 以重新开始。
> 常规表达式语法将在第 20 章“Perl 编程入门”中介绍。

## 列表 9.2 `adduser` 会话示例

```text
# adduser
Use option `\`-silent\`` if you don't want to see all warnings and questions.

Check `/etc/shells`
Check `/etc/master.passwd`
Check `/etc/group`
Usernames must match regular expression:
'^ [a-z0-9_] [a-z0-9_- ] * $':
Enter your default shell: bash csh date no sh tcsh [csh]:
Your default shell is: csh -> /bin/csh
Enter your default HOME partition: [/home]:
Copy dotfiles from: /usr/share/skel no [/usr/share/skel]:
Send message from file: /etc/adduser.message no [no]:
Use password-based authentication (y/n) [y]:
Enable account password at creation (y/n) [y]:
Use an empty password (y/n) [n]:

Okay, let's go.
Don't worry about mistakes. I will give you the chance later
to correct any input.
Enter username [ ^ [a-z0-9_] [a-z0-9_- ] * $ ]: joe
Enter full name [ ]: Joe User
Enter shell bash csh date no sh tcsh [csh]:
Enter home directory (full path) [/home/joe]:
Uid [1005]:
Enter login class: default [ ]:
Login group test [joe]:
Login group is `joe'. Invite test into other groups: guest no
[no]:
Use password-based authentication (y/n) [y]:
Use an empty password (y/n) [n]:
Enter password [ ]:
Enter password again [ ]:
Enable account password at creation (y/n) [y]:

Name: joe
Password: ****
Fullname: Joe User
Uid: 1005
Gid: 1005 (joe)
Class:
Groups: joe
HOME: /home/joe
Shell: /bin/csh
OK? (y/n) [y]:
Added user 'joe'
Send message to `joe' and: no root second_mail_address [no]:

Joe User,
```

