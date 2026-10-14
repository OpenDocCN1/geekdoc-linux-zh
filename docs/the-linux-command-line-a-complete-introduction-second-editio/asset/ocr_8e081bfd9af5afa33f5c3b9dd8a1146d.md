indicating that this shell has superuser privileges (the trailing # rather than a $), and the current working directory is now the home directory for the superuser (normally /root). Once in the new shell, we can carry out commands as the superuser. When finished, enter exit to return to the previous shell.

```
[root@linuxbox ~]# exit
[me@linuxbox ~]$
```

It is also possible to execute a single command rather than starting a new interactive command by using su this way.

```
su -c 'command'
```

Using this form, a single command line is passed to the new shell for execution. It is important to enclose the command in quotes, as we do not want expansion to occur in our shell but rather in the new shell.

```
[me@linuxbox ~]$ su -c 'ls -l /root/*'
Password:
-rw------ 1 root root 754 2007-08-11 03:19 /root/anaconda-ks.cfg

/root/Mail:
total 0
[me@linuxbox ~]$
```

# sudo: Execute a Command As Another User

The sudo command is like su in many ways but has some important additional capabilities. The administrator can configure sudo to allow an ordinary user to execute commands as a different user (usually the superuser) in a controlled way. In particular, a user may be restricted to one or more specific commands and no others. Another important difference is that the use of sudo does not require access to the superuser's password. Authenticating using sudo requires the user's own password. Let's say, for example, that sudo has been configured to allow us to run a fictitious backup program called backup_script, which requires superuser privileges. With sudo it would be done like this: