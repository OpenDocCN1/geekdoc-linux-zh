
```
cd /usr/share/doc
```

然后，要将目录更改为`/usr/share/doc`中的`bash-2.05b`子目录，请键入此命令：

```
cd bash-2.05b
```

现在，如果您使用`pwd`命令，该命令将显示`/usr/share/doc/bash-2.05b`作为当前目录。

这两个示例表明您可以以两种方式引用目录的名称：

- 绝对路径名（例如`/usr/share/doc`），它指定目录树中的确切目录
- 相对目录名（例如`bash-2.05b`，它表示当前目录的`bash-2.05b`子目录，无论当前目录是什么）

如果您在`/usr/share/doc`中键入`cd bash-2.05b`，当前目录将更改为`/usr/share/doc/bash-2.05b`。但是，如果我在`/home/naba`中键入相同的命令，shell将尝试将当前目录更改为`/home/naba/bash-2.05b`。

Use the `cd` command without any arguments to change the current directory back to your home directory. No matter where you are, typing `cd` at the shell prompt brings you back home!

By the way, the tilde character (`~`) refers to your home directory. Thus the command `cd ~` also changes the current directory to your home directory. You can also refer to another user's home directory by appending that user's name to the tilde. Thus, `cd ~superman` changes the current directory to the home directory of `superman`.

Wait, there's more. A single dot (`.`) and two dots (`..`) — often referred to as dot-dot — also have special meanings. A single dot (`.`) indicates the current directory, whereas two dots (`..`) indicate the parent directory. For example, if the current directory is `/usr/share`, you go up one level to `/usr` by typing `cd ..`.

## Commands for directory listings and permissions

You can get a directory listing by using the `ls` command. By default, the `ls` command — without any options — displays the contents of the current directory in a compact, multicolumn format. For example, type the next two commands to see the contents of the `/etc/X11` directory:

```
cd /etc/X11
ls
```

The output looks like this (on the console you'd see some items in different colors):

```
applnk          prefdm          sysconfig       XftConfig.README-OBSOLETE  xserver
desktop-menus   proxymgr        twm             xinit                       xsm
fs              rstart          X               xkb
 gdm             serverconfig    xdm             Xmodmap
lxbproxy        startthere      XF86Config      Xresources
```

From this listing (without the colors), you cannot tell whether an entry is a file or a directory. To tell the directories and files apart, use the `-F` option with `ls` and you'll get more clues:

```
ls -F
applnk/         prefdm*         sysconfig/      XftConfig.README-OBSOLETE  xserver/
desktop-menus/  proxymgr/       twm/            xinit/                      xsm/
fs/             rstart/         X@              xkb@
gdm/            serverconfig/   xdm/            Xmodmap
lxbproxy/       startthere      XF86Config      Xresources
```

The output from `ls -F` shows the directory names with a slash (`/`) appended to them. Plain filenames appear as is. The at sign (`@`) appended to the file named `X` indicates that this file is a link to another file (in other words, this filename simply refers to another file; it's a shortcut). An asterisk (`*`) is appended to executable files (see, for example, the `prefdm` file in the listing). The shell can run any executable file.

You can see even more detailed information about the files and directories with the `-l` option:

```
ls -l
```

For the `/etc/X11` directory, a typical output from `ls -l` looks like the following:
