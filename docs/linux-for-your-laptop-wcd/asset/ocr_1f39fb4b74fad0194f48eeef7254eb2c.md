of IP addresses and hostnames specified by wildcards. In this example, the notebook is named zippo.

The corresponding /etc/rsyncd.conf file on the notebook named zippo would look like this:

```
`[ball]`    comment = ball file area    path = /home/bball    read only = no    list = yes    hosts allow = workhorse
```

You (as root) must then run `rsync` in its background (daemon) mode on your remote server and notebook, like this:

```
# rsync --daemon
```

You're now set to transfer files!

# ## Transferring Files

For example, if your notebook is connected to the LAN, and you'd like to synchronize a directory named `work` in your home directory on your notebook with an identical directory on your server named `workhorse`, you can use the `rsync` command, its `-v` options, and the local and remote directories like this:

```
# rsync -vva workhorse:/home/bball/work .
```

The `v` (verbose) option lists the files that are being transferred, and the `a` (archive) option copies files, symbolic links, subdirectories, and contents. The period (`.`) assumes that you are executing this command in your home directory on your notebook. This means that the preceding command could also look like this:

```
# rsync -vva workhorse:/home/bball/work /home/bball
```

# ## Synchronizing the Palm PDA

One of the most useful information appliances to hit the market in recent years (besides your notebook running Linux) is the Palm PDA (Personal Digital Assistant). These ubiquitous devices have captured the hearts and minds of millions of users, and many Linux users are especially fond of the lightweight, easy-to-use