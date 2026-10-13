
- 2. Type `ls -F` to see the files and directories in your home directory.

- 3. Type `ls -aF` to see everything, including the hidden files.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_197_0.png)

Most Linux commands take single-character options, each with a minus sign as a prefix. When you want to use several options, type a hyphen and concatenate the option letters, one after another. Thus, `ls -al` is equivalent to `ls -a -l` as well as `ls -a -l`.

## Commands for changing permissions and ownerships

You may need to change a file's permission settings to protect it from others. Use the `chmod` command to change the permission settings of a file or a directory.

To use `chmod` effectively, you have to learn how to specify the permission settings. A good way is to concatenate letters from the columns of Table 4-4 in the order shown `Who/Action/Permission`.

Note: You use only the single character from each column — the text in parentheses is for explanation only.

### Table 4-4 Letter Codes for File Permissions

| Who | Action | Permission |
|---|---|---|
| `u` (user) | `+` (add) | `r` (read) |
| `g` (group) | `-` (remove) | `w` (write) |
| `o` (others) | `=` (assign) | `x` (execute) |
| `a` (all) | `s` (set user ID) |  |

For example, to give everyone read access to all files in a directory, pick `a` for all from the first column, `+` for add from the second column, and `r` for read from the third column to come up with the permission setting `a+r`. Then use the whole set of options with `chmod`, like this:

```
chmod a+r *.
```

On the other hand, to permit everyone to execute one specific file, type

```
chmod a+x filename
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_197_1.png)

Suppose you have a file named `mystuff` that you want to protect. You can make it accessible to no one but you if you type the following commands, in this order:

```
chmod a-rwx mystuff
```

```
chmod u+rw mystuff
```

The first command turns off all permissions for everyone, and the second command turns on the read and write permissions for the owner. Type `ls -l` to verify that the change took place `you should see a permission setting of -rw------`. Here's a sample output from `ls -l`:

```
-rw------ 1 naba naba 3 Jun 30 18:45 mystuff
```

Note the third and fourth fields that show `naba naba`. These two fields show the file's user and group ownership. In this case, the name of the user is `naba` and the name of the group is `naba` as well `because Red Hat Linux creates a group for each user`.

Sometimes you have to change a file's user or group ownership for everything to work correctly. For example, suppose you are instructed to create a directory named `cups` and give it the ownership of user ID `lp` and group ID `sys`. How would you do it?

Well, you can log in as root and create the directory with the command `mkdir`:

```
mkdir cups
```

If you check the file's details with the `ls -l` command, you see that the user and group ownership is `root root`.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_198_0.png)

To change the owner, use the `chown` command. For example, to change the ownership of the `cups` directory to user ID `lp` and group ID `sys`, type

```
chown lp.sys cups
```

## Commands for working with files

要从一个目录复制文件到另一个目录，请使用 `cp` 命令。例如，要将文件 `/usr/X11R6/lib/X11/xinit/Xclients` 复制到当前目录 `例如你的主目录` 中的 `Xclients.sample` 文件，请输入以下内容：

```
cp /usr/X11R6/lib/X11/xinit/Xclients Xclients.sample
```

如果要将文件复制到当前目录但保留原始名称，请将句点 `.` 用作 `cp` 命令的第二个参数。因此，以下命令将 `/etc/X11` 目录中的 `XF86Config` 文件复制到当前目录 `用单个句点表示`：

```
cp /etc/X11/XF86Config .
```

`cp` 命令会制作文件的新副本并保留原文件不变。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_199_0.png)

如果要将目录的全部内容 `包括所有子目录及其内容` 复制到另一个目录，请使用命令 `cp -ar sourcedir destdir` `这会将 sourcedir 目录下的所有内容复制到 destdir`。例如，要将 `/etc/X11` 目录中的所有文件复制到当前目录，请输入以下命令：

```
cp -ar /etc/X11 .
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_199_1.png)

要将文件移动到新位置，请使用 `mv` 命令。原始副本将被删除，目标位置会出现新副本。你可以使用 `mv` 重命名文件。如果要将 `today.list` 的名称更改为 `old.list`，请按如下方式使用 `mv` 命令：
