To see what shell you have been assigned, examine the last field in your passwd file entry. You can do this quickly by using the *finger* command, your login or *username*, and the location and name of the *passwd* file or *pathname*, like this:

```
$ finger kbali /etc/passwd

bbali:x:500:100:William Balli:/home/bballi:/bin/bash
```

In this example, the default shell for the user *bbali* is *bash*. This shell may be used because it is listed in the system-wide list of approved shells, /etc/shells. Look at your system's list of approved shells by using the *cat* command, followed by the pathname to the file like this:

```
$ cat /etc/shells
/bin/ash
/bin/bash
/bin/bash1
/bin/csh
/bin/false
/bin/ksh
/bin/qsh
/bin/tcsh
/bin/true
/usr/bin/csh
/usr/bin/ksh
/usr/bin/passwd
/usr/bin/rbash
/usr/bin/tcsh
/usr/bin/zsh
```

This example, from a SuSE PPC 7.1 system, shows a number of shells (and other applications) that are deemed acceptable shells. Once you know that a shell is acceptable, you can then (as with root) edit your /etc/passwd entry to replace or change the default shell's pathname.

However, a much better (and safer) way to change shells is to use the *chsh* command. Use this command, followed by its *-s* command-line option and the pathname of the desired shell like this:

```
$ chsh -s /usr/bin/ksh
Password:
```

Note that you will be prompted for your password after pressing Enter. Type in your password and then press Enter again. The *chsh* command does have some