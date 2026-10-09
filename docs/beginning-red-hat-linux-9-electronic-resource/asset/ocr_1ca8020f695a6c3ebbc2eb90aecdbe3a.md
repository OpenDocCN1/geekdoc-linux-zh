However, to perform certain privileged tasks, such as shutting down the system, you need to assume the identity of an administrator (or root user, in Unix parlance). In these situations, it's rather inconvenient to have to log out of the system and log back in as a root user. For this reason, there is a simpler alternative – you can use the `su` command (with no arguments) and supply the root user's password. This will provide you with a shell that has the privileges of the root user. When you've completed your administrative tasks, you can switch back to the safety of non-admin privileges by exiting the root shell – typing `exit` or `Ctrl-D`.

The `su` command can also be used to switch identities between two non-root users. The `id` command prints the current user ID of the user:

```
$ id
uid=500 (brucewayne) gid=513 (users) groups=513 (users)
$ su
Password:
bash# id
uid=0 (root) gid=0 (root) groups=0 (root), 1 (bin), 2 (daemon)
bash# exit
$ id
uid=500 (brucewayne) gid=513 (users) groups=513 (users)
$ su batman
Password:
$ id
uid=800 (batman) gid=513 (users) groups=513 (users)
```

The `uid` field indicates the user ID of the user, which is a unique number, assigned to each and every user on the system. `gid` is the group ID of the *primary group* that a user belongs to. A group is essentially a collection of users who have some common set of privileges. For instance, all members of the engineering group may have access to say, the blueprints directory on a machine. Each user belongs to at least one group, which is known as the primary group. In addition, they may also belong to other groups as indicated by the `groups` field. Groups like users have a number associated with them; 513 in this case denotes the group ID of the `users` group.

# ### Shutting Down and Rebooting

The `shutdown` command shuts down the system. This command is restricted to `root` users only. Shutdown can be immediate (in which case the `now` argument is passed), or it can be delayed (by `n` seconds by passing the `-t n` option).

If we need to *reboot* rather than *shut down* the system, the `reboot` command comes in handy. It is usually a good idea to run the `sync` command before rebooting or shutting down the system. The `sync` command ensures that file system objects are in a consistent state.

# ### Disk Usage

The `df` command displays a partition-by-partition summary of disk usage. We can supply arguments such as `-k` to indicate to `df` that it should report disk usage in increments of kilobytes, as shown here: