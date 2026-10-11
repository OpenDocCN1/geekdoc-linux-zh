# SU: GIVES YOU ANOTHER USER'S PRIVILEGES

The su (substitute user) utility can create a shell or execute a program with the identity and permissions of a specified user. Follow su on the command line with the name of a user; if you are working with root privileges or if you know the user's password, you take on the identity of that user. When you give an su command without an argument, su defaults to Superuser so that you take on the identity of root (you have to know the root password).

To ensure that you are using the system's official version of su (and not one planted on your system by a malicious user), specify su's absolute pathname (/bin/su) when you use it. (Of course, if someone has compromised your system enough that you are running a fake su command, you are in serious trouble anyway—but using an absolute pathname for su is still a good idea.)

When you give an su command to become Superuser, you spawn a new shell, which displays the # prompt. You return to your normal status (and your former shell and prompt) by terminating this shell: Press CONTROL-D or give an exit command. Giving an su command by itself changes your user and group IDs but makes minimal changes to your environment. You still have the same PATH you did when you logged in as yourself. When you run a utility that is normally run by root (the utilities in /sbin and /usr/sbin), you may need to specify an absolute pathname for the utility (such as /sbin/service). When you give the command su – (you can use –l or –login in place of the hyphen), you get a root login shell: It is as though you logged in as root. Not only are your user and group IDs the same as those of root, but your entire environment is that of root. The login shell executes the appropriate startup scripts before displaying a prompt, and your PATH is set to what it would be if you had logged in as root, typically including /sbin and /usr/sbin.

Use the id utility to display the changes in your user and group IDs and in the groups you are associated with. In the following example, the information that starts with context pertains to SELinux:

```
$ id
uid=500(alex) gid=500(alex) groups=500(alex) context=user_u:system_r:unconfined_t
$ su
Password:
# id
uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon),3(sys), ...
```

You can use su with the –c option to run a single command with root privileges, returning to your original shell when the command finishes executing. The following example first shows that a user is not permitted to kill a process. With the use of su –c and the root password, the user is permitted to kill (page 409) the process. The quotation marks are necessary because su –c takes its command in the form of a single argument.

```
$ kill –15 4982
–bash: kill: (4982) – Operation not permitted
$ su –c "kill –15 4982"
Password:
$
```