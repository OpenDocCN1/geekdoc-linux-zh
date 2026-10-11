
如果你不需要指定特定的用户可以或不能访问共享，那么 `valid users` 和 `invalid users` 以及 `writable` 是很有用的命令，但如果你命名了特定用户，它们就是没必要的。现在让我们更进一步，开始获取关于特定用户可以读取或写入共享的详细信息。你可以通过 `read list`、`write list`、`valid user` 和 `invalid user` 设置来实现。

`valid user` 看起来像一个由空格分隔的用户名列表，如下例：

```
[pubshare]
path = /publicfiles
guest ok = no
writeable = yes
valid user = jane jim sue
```

在共享中添加这一行会发生很大变化。在此之前，域中的任何人都可以访问此共享——但现在，只有 `jane`、`jim` 和 `sue` 可以访问它。一旦你在共享中有了有效用户列表，那么你最好在该列表中，否则你就无法获得访问。

同样，如果你没有包含 `valid user` 命令，那么每个域用户都是有效的。最后一部分的设置（在没有任何 `valid user` 设置的情况下使用 `writeable = yes`）基本上等同于 NT 含义中的“所有人/完全控制”权限。但一旦你使用了 `valid user` 语句，你就隐式地表示不在该语句中的任何人都无法访问该共享。

如果你想确保某些特定人员无法访问你的共享，可以使用 Samba 团队称为“paranoid”（疑心的）的命令——`invalid user` 命令：

```
invalid user = john paul
```

这是 Samba 对应的 NT 拒绝访问命令——无论用户在 Samba 中可能获得其他权限，在 `invalid user` 列表中意味着完全没有访问权限。你也可以将 `invalid user` 和 `valid user` 命令放入 `smb.conf` 文件的 `[global]` 部分；那么该服务器上的每个共享都将相应地处理有效和无效用户。所以，如果你想确保将某个用户锁定在服务器之外，请将其放入无效用户列表，并将该列表放在 `[global]` 中。

## 指定谁可以读取或写入共享

到目前为止，我们所做的都是通过 `writeable` 和 `valid users` 命令的组合来指定谁可以读取和写入共享。如果你只需要几个人访问共享，并想给他们所有的只读或读写权限，这些就足够了。但让我们更具体地指定谁可以读取和写入共享。两个命令 `read list` 和 `write list` 允许你列出具有只读或读写权限的用户。例如：

```
[pubshare]
path = /publicfiles
guest ok = no
writeable = yes
read list = sam mary phyllis
write list = dawn joe bill
```

在此共享上，`sam`、`mary` 和 `phyllis` 拥有访问权限但只是只读，而 `dawn`、`jane`、`joe` 和 `bill` 具有读写权限。赋予某人 `write list` 权限会覆盖 `writable = no` 设置。没关系，缺少 `valid users` 列表并不是错误——请继续阅读。

`invalid users` 优于 `write list`，因此在 `write list` 列表中优于 `writable = no` 设置；那么在列表中是否能克服进入 `invalid users` 列表呢？换句话说，考虑一下：

```
[pubshare]
path = /publicfiles
guest ok = no
writeable = yes
read list = sam mary phyllis
write list = dawn joe bill
```

在此共享上，`sam`、`mary` 和 `phyllis` 拥有访问权限但只是只读，而 `dawn`、`jane`、`joe` 和 `bill` 具有读写权限。赋予某人 `write list` 权限会覆盖 `writable = no` 设置。没关系，缺少 `valid users` 列表并不是错误——请继续阅读。

`invalid users` 优于 `write list`，因此在 `write list` 列表中优于 `writable = no` 设置；那么在列表中是否能克服进入 `invalid users` 列表呢？换句话说，考虑一下：

```
[pubshare]
path = /publicfiles
guest ok = no
writeable = yes
read list = sam mary phyllis
write list = dawn joe bill
```

在此共享上，`sam`、`mary` 和 `phyllis` 拥有访问权限但只是只读，而 `dawn`、`jane`、`joe` 和 `bill` 具有读写权限。赋予某人 `write list` 权限会覆盖 `writable = no` 设置。没关系，缺少 `valid users` 列表并不是错误——请继续阅读。

### Samba：Linux 网络 453

## 指定 Samba 中的管理员

你可能希望管理员对共享拥有不受的访问权限。你可以通过 `[global]` 中的 `admin users` 命令来实现。如果我想让用户 `pete` 控制控制，我只需在 `smb.conf` 的 `[global]` 部分添加此行：

```
admin users = pete
```

再次，你需要在域和服务器上都需要 `pete` 账户才能执行。

## 在 Samba 中使用组

这些都很好，但谁想一个个列出一堆用户呢？在 NT 和 2000 世界中，我们习惯使用组来处理权限。Samba 允许你命名组，但这是一个两个步骤的过程：你看，你已经看到名为 `bob` 的用户在 Linux 机器上必须有一个名为 `bob` 的账户。但名称不需要匹配——这会让操作变得更简单。如果你的 NT/2000 用户名不匹配，那么你就使用 `smb.conf` 中的 `username map` 命令以及匹配 Linux 映射的文件。

在 `valid users`、`write list`、`read list` 或 `invalid users` 命令中添加组非常简单——只需使用组的名称并加上 `@` 符号即可。要让名为 `engineers` 的组对共享具有写入权限，可以在该共享的部分放置此命令：

```
write list = @engineers
```

再次，这将指向名为 `engineers` 的 Linux 组，请确保已创建该组（`groupadd engineers`）。接下来，让我们将其与实际 NT 或 2000 组连接起来。将此命令放入 `[global]` 部分：

```
username map = /etc/linuxtont
```

`/etc/linuxtont`（顺便说，你可以命名任何名称）是一个简单的文本文件，内容如下：

```
Linux name = NT/2000 name
```

### 设置几个共享：示例

假设你有一个 Samba 服务器，其中有两个你想共享的目录：`/publicstuff` 和 `/privatestuff`。你希望所有人都能以名为 `public` 的共享名称读取 `/publicstuff`，但除了 `gerry` 用户账户外，没人可以向其写入内容。然后，你有一个名为 `/privatestuff` 的共享，你只想让 `managers` 组的成员访问（读和写），使用的共享名为 `private`。

为了简单起见，让我们假设我们仍在旧的 REALM 域示例中工作。这是该域的 `smb.conf` 可能的如下：

```
[global]
wins server = 130.10.20.5
workgroup = REALM
server string = Test Samba Server
netbios name = LINUXBOX
security = domain
password server = *
encrypt passwords = yes
username map = /etc/linixtont
[public]
path = /publicstuff
guest ok = yes
writeable = no
write list = gerry
[private]
path = /privatestuff
guest ok = no
valid users = @managers
write list = @managers
```

`/etc/linixtont` 文件将有一条记录：

```
managers = @managers
```

在第一个共享中，我使用了 `guest ok` 而没有使用 `valid users` 语句，因为我并不在乎谁访问它，但 `writeable = no` 确保了没有人可以修改它——除了 `gerry` 之外。在第二个共享中，禁用访客并显式地仅将 `managers` 组的成员设为 `valid users`，可以将其他人全部排除在外。

## Linux 文件和目录权限 Samba
