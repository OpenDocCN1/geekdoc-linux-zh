![](bbox=[0.13, 0.13, 0.23, 0.23])

By the way, the tilde character (~) refers to your home directory. Thus the command `cd ~` also changes the current directory to your home directory. You can also refer to another user’s home directory by appending that user’s name to the tilde. Thus, `cd ~superman` changes the current directory to the home directory of superman.

![](bbox=[0.13, 0.25, 0.23, 0.33])

Wait, there’s more. A single dot (.) and two dots (..) — often cleverly referred to as *dotdot* — also have special meanings. A single dot (.) indicates the current directory, whereas two dots (..) indicate the parent directory. For example, if the current directory is `/usr/share`, you go one level up to `/usr` by typing

```
```
cd ..
```
```

# ### Commands for directory listings and permissions

You can get a directory listing by using the `ls` command. By default, the `ls` command — without any options — displays the contents of the current directory in a compact, multicolumn format. For example, type the next two commands to see the contents of the `/etc/X11` directory:

```
```
cd /etc/X11
ls
```
```

The output looks like this. (On the console, you see some items in different colors.)

```
```
X                    Xsession.d         cursors         rgb.txt        xkb
XF86Config-4         Xsession.options   default-display-manager  rstart       xserver
Xresources           Xwrapper.config    fonts            sysconfig      xsm
Xsession             app-defaults       gdm              xinit
```
```

From this listing (without the colors), you cannot tell whether an entry is a file or a directory. To tell the directories and files apart, use the `-F` option with `ls` like this:

```
```
ls -F
```
```

This time, the output gives you some more clues about the file types:

```
```
X@                   Xsession.d/        cursors/         rgb.txt        xkb/
XF86Config-4         Xsession.options   default-display-manager  rstart/      xserver/
Xresources/          Xwrapper.config    fonts/           sysconfig/     xsm/
Xsession*            app-defaults/      gdm@             xinit/
```
```

The output from `ls -F` shows the directory names with a slash (/) appended to them. Plain filenames appear as is. The at sign (@) appended to a file’s name (for example, notice the file named *X*) indicates that this file is a link to