# 60 | Master of Linux Commands

+   - ls -lh: Listes sizes more readable (human readable).
- ls -lt: Sort files by modified date (modification).

Now let's talk about the other forms of the ls command use. For example, we want to see only hidden files in the directory not all files and folders which command shold we use? The answer is ls -d. * command.

```
root@kemal:~# ls -ld .*
.bashrc .dbus ICEauthority .profile
.cache .gconf .local .rnd
.bash_history .config .gnome2 .mozilla .wireshark
```

If you do not want "." and ".." directories listed, then you should use ls -d [!] command. To show files beginning only with "b" ls -d b*, to show beginning all others rather than "m" ls -d[!]* must be used. If you want to list the directories above the one you are in, you must use the command as “ls ..”. If you want to see what is in the two directories above you you must use ls ..../ command.

```
root@kemal:/var/log/apache2# ls ../..
backups lib lock mail run tmp WWW
cache local log opt spool unicornscan
root@kemal:/var/log/apache2# -
```

§