does the work, though it is not directly called. You do not want to remove this script, in the event that you want to enable it again in the future. Going back to the results of the `find` command, you'll see that you got two hits in the `rc3.d` and `rc5.d` directories.

To remove the service, simply `cd` into each of those directories and rename the symlink so that instead of starting with an `S`, it starts with a `K`. By renaming the symlink, you'll be able to come back later and easily enable it without having to try and figure out the correct order that entry should be in (for instance, should it be `$35nfs` or `$45nfs`?).

# Enabling a Service

Enabling a service works just like disabling a service. You find the scripts that actually run at the appropriate runlevels, except instead of changing them from an `S` to a `K`, you'll change them *to* an `S` from a `K`.

If the symlink you are looking for does not exist but the appropriate script in the `init.d` directory does exist, you can simply add a new symlink in the `rc3.d` and `rc5.d` directories. Be sure to use the correct format for the filename (see previous sections for details).

# Starting and Stopping Services

To start or stop a service from the command line, the quick and dirty way to do things is to use the `service` command. Become the root user and run:

```
[root@tedford /root]# `service --status-all`
```

This command shows the currently stopped and running services (complete with process ID numbers for running services). To start a service that isn't running, simply tell that service to start:

```
[root@tedford /root]# `service nfs start`
```

Telling a service to stop works predictably:

```
[root@tedford /root]# `service nfs stop`
```

You can also check the status of a single service (the full list can be overwhelming):

```
[root@tedford /root]# `service nfs status`
```

Other commands supported by the specific service can be used as well, including `restart` to stop and start the service, or `reload` to reread the configuration file (although sometimes these two commands are synonymous, as in the script you'll look at in the next section).