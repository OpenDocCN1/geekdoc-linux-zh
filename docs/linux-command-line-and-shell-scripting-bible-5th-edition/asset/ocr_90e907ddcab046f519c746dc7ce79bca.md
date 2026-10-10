# Part I: The Linux Command Line

The **Bash** shell program (*bash*) typically resides in the */usr/bin* directory on modern Linux systems. However, on your Linux system you may find it in the */bin* directory. The **which** *bash* command can help here by providing the directory and filename to use for the Bash shell:

```
```
$ which bash
/usr/bin/bash
$
```
```

A long listing reveals that the *bash* file (the **Bash** shell) is an executable program via the trailing asterisk (*) on the file’s name:

```
```
$ ls -lF /usr/bin/bash
-rwxr-xr-x. 1 root root 1219248 Nov  8 11:30 /usr/bin/bash*
$
```
```

> > **NOTE**
> > Typically on modern Linux systems, the */bin* directory is symbolically linked to the */usr/bin/* directory, which is why the user *christine* has */bin/bash* listed as their default shell program, but the **Bash** shell program actually resides in the */usr/bin/* directory. Symbolic (soft) links are covered in Chapter 3, “Basic Bash Shell Commands.”

On most Linux systems, you’ll find the various installed shells that can be used as the user’s default shell within the */etc/shells* file, as shown here from an Ubuntu 24.04 system:

```
```
$ cat /etc/shells
# /etc/shells: valid login shells
/bin/sh
/usr/bin/sh
/bin/bash
/usr/bin/bash
/bin/rbash
/usr/bin/rbash
/usr/bin/dash
/bin/zsh
/usr/bin/zsh
/usr/bin/zsh
$
```
```

A user can set any of these different shell programs on this system as their shell. However, due to its popularity, it is rare to use any other shell instead of **Bash** as an account’s default interactive shell. The *default interactive shell*, also called a *login shell*, starts whenever a user logs into a *virtual console* terminal or starts a *terminal* emulator in the GUI.

Another shell, *sh*, is the *default system shell*. The **default system shell** is used for system shell scripts, such as those needed at startup.