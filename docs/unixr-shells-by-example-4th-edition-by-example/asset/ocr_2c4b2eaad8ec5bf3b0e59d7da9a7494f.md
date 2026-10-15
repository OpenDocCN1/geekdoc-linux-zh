# EXAMPLE 13.4 (CONTINUED)

```
3 ulimit -c 1000000
4 if [ `id -gn` = `id -un` -a `id -u` -gt 14 ]; then
5   umask 002
else
  umask 022
fi
6 USER=`id -un`
7 LOGNAME=$USER
8 MAIL="/var/spool/mail/$USER"
9 HOSTNAME=`/bin/hostname`
10 HISTSIZE=1000
11 HISTFILESIZE=1000
12 export PATH PS1 HOSTNAME HISTSIZE HISTFILESIZE USER LOGNAME MAIL
13 for i in /etc/profile.d/*.sh ; do
14   if [ -x $i ]; then
15     . $i
fi
16 done
17 unset i #
```

# EXPLANATION

+   1 The PATH variable is assigned locations where the shell should search for commands.
+   2 The primary prompt is assigned. It will be displayed in the shell window as the user's name (\u), the @ symbol, the host machine (\W), and a dollar sign.
+   3 The ulimit command (a shell built-in command) is set to limit the maximum size of core files created to 1,000,000 bytes. Core files are memory dumps of programs that have crashed, and they take up a lot of disk space.
+   4 This line reads: If the user's group name is equal to the user's name and the user's ID number is greater than 14 ... (see line 5)
+   5 ... then set the umask to 002. When directories are created they will get 775 permissions and files will get 664 permissions. Otherwise, the umask is set to 022, giving 755 to directories and 644 to files.
+   6 The USER variable is assigned the username (`id -un`).
+   7 The LOGNAME variable is set to the value in $USER.
+   8 The MAIL variable is assigned the path to the mail spooler where the user's mail is saved.
+   9 The HOSTNAME variable is assigned the name of the user's host machine.
+   10 The HISTSIZE variable is set to 1000. HISTSIZE controls the number of history items that are remembered (from the history list stored in the shell's memory) and saved in the history file after the shell exits.