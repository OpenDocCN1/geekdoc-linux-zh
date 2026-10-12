If you **type `cd bash-2.05b`** in `/usr/share/doc`, the current directory changes to `/usr/share/doc/bash - 2.05b`. However, if I type the same command in `/home/naba/naba`, the shell tries to change the current directory to `/home/naba/bash - 2.05b`.

![](bbox=[0.14, 0.2, 0.2, 0.28])

Use the `cd` command without any arguments to change the current directory back to your home directory. No matter where you are, typing **cd** at the shell prompt brings you back home!

![](bbox=[0.14, 0.28, 0.2, 0.36])

By the way, the tilde character (`~`) refers to your home directory. Thus the command `cd -` also changes the current directory to your home directory. You can also refer to another user’s home directory by appending that user’s name to the tilde. Thus, `cd ~superman` changes the current directory to the home directory of superman.

![](bbox=[0.14, 0.36, 0.2, 0.44])

Wait, there’s more. A single dot (`. `) and two dots (`.. `) — often referred to as *dot-dot* — also have special meanings. A single dot (`. `) indicates the current directory, whereas two dots (`.. `) indicate the parent directory. For example, if the current directory is `/usr/share`, you go one level up to `/usr` by typing `cd .. `

```
cd ..
```

# Commands for directory listings and permissions

You can get a directory listing by using the `ls` command. By default, the `ls` command — without any options — displays the contents of the current directory in a compact, multicolumn format. For example, type the next two commands to see the contents of the `/etc/X11` directory:

```
cd /etc/X11
ls
```

The output looks like this (on the console you see some items in different colors):

appink      lxproxy     startx      xdm         xmodmap     xsm
dm          prefinfo    sysconfig   Xftconfig.README-OB SOLETE   xorg.conf
gdm         proxy.mgr   twm         xinit       Xresources
gdm         serverconfig x

*Note: The table in the original image has a different layout, with 'dm' and 'gdm' in the first column, 'prefinfo' and 'proxy.mgr' in the second, 'startx' and 'twm' in the third, 'xdm' and 'xinit' in the fourth, 'xmodmap' and 'Xresources' in the fifth, and 'xsm' in the sixth. The row with 'sysconfig' and 'Xftconfig.README-OB SOLETE' spans across multiple columns. This representation is a simplified version.*

From this listing (without the colors), you cannot tell whether an entry is a file or a directory. To tell the directories and files apart, use the `-F` option with `ls` like this:

```
ls -F
```

![](bbox=[0.88, 0.31, 0.96, 0.37])

![](bbox=[0.88, 0.37, 0.96, 0.49])