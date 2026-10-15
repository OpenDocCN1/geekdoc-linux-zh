

useradd -G—此命令设置创建用户主目录、账户过期日期、默认组和命令 shell 的系统默认值。有关具体选项，请参阅 man useradd。 不带任何参数使用时，它会显示系统的默认值。 用户的默认文件集位于 /etc/skel。

### NOTE

用于填充新用户主目录的文件集保存在 /etc/skel 中。这对系统管理员很方便，因为任何需要普遍应用的特殊文件、链接或目录都可以放在 /etc/skel 中，并将为每个新用户自动复制并赋予适当的权限。

```
$ ls -al /etc/skel
total 20
drwxr-xr-x  2 root root 4096 2006-04-27 04:18 .
drwxr-xr-x 110 root root 4096 2006-05-31 21:24 ..
-rw-r--r--  1 root root  220 2006-04-21 23:51 .bash_logout
-rw-r--r--  1 root root  414 2006-04-21 23:51 .bash_profile
-rw-r--r--  1 root root 2227 2006-04-21 23:51 .bashrc
lrwxrwxrwx  1 root root   26 2006-05-07 15:29 Examples -> /usr/share/example-content
```

每一行提供了文件权限、该文件或目录名下包含的文件数、文件所有者、文件组、文件大小、创建日期和文件名。

正如你所见，root 拥有此处的每个文件，但 adduser 命令（指向实际命令 useradd 的符号链接）会将 /etc/skel 中的所有内容复制到新主目录，并将文件所有权和权限重置为新用户。

某些用户文件可能存在，系统管理员不希望用户更改；/home/username 中这些文件的权限可以重置，以便用户可以读取它们但不能写入它们。

userdel—此命令完全删除用户的账户（从而消除该用户的主目录及其包含的所有文件）。

passwd—此命令更新密码管理系统使用的“身份验证令牌”。

### TIP

要锁定用户账户，请使用以下命令：

```
# passwd -l username
```

这会在用户加密密码前加上一个 !（感叹号，也称为 bang）；用于逆转该过程的命令使用 -u 选项。这是解决该问题的更优雅且更受青睐的方案，比传统的 UNIX 手动编辑文件的方式更好。

usermod—此命令更改多个用户属性。最常用的参数是 -s 用于更改 shell 和 -u 用于更改 UID。在用户登录或运行进程时无法进行任何更改。

chsh—此命令更改用户的默认 shell。对于 Ubuntu，默认 shell 是 /bin/bash，被称为 Bash，或 Bourne Again Shell。

## Adding New Users

通过命令行添加此用户的方法实际上相当简单，可以在一行中完成。在此示例中，系统管理员使用 useradd 命令添加新用户 bernice。命令 adduser（在某些 UNIX 系统上找到的变体）是 useradd 的符号链接，因此两个命令的工作方式相同。在此示例中，我们使用 -p 选项设置用户请求的密码；我们使用 -s 设置他的特殊 shell，并使用 -u 选项指定他的 UID。 （如果我们使用默认设置创建用户，则无需使用这些选项。）我们想要完成的所有操作都可以在一行中完成：

```
# useradd bernice -p sTitcher -s /bin/zsh -u 507
```

系统管理员也可以使用 Ubuntu 提供的图形界面，如图 14.2 所示。它可通过管理菜单中的 Users and Groups 项目访问。在此，系统管理员正在向系统添加一个新用户，其中用户 bernice 使用 bash 命令 shell。

以下是我们使用图形 User Manager 界面添加与前面命令中所示相同账户所使用的步骤：

- 1. 通过单击系统设置菜单中的 Users and Groups 菜单项启动 Ubuntu 用户管理器图形界面。
- 2. 单击 Add User 按钮以调出 Add User 对话窗口。
- 3. 填写表单，信息如本节第一段所述。
- 4. 单击 Advanced 选项卡并打开 Shell 下拉菜单以选择 bash shell。
- 5. 使用 UID 对话框中的箭头将 UID 增加到 1413。
- 6. 单击 OK 保存设置。

请注意，用户被手动分配 UID 1413，因为这是她在将要连接到此机器的另一台系统机器上的 UID。因为系统仅将其识别为 1001 而不是 bernice，如果分配了两个不同的 UID，两台机器将无法将 bernice 识别为同一用户。

