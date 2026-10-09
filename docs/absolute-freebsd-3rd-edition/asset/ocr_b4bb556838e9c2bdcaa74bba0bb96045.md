Instead of exec.start, you could set the persist option. This tells FreeBSD that a jail can exist without any processes running inside it. Including both persist and exec.start means that FreeBSD will start a process for the jail, but when the process stops running, the jail won't shut itself down.

You can tell the jail to run an additional command after it starts with the exec.poststart option. Any command or script listed with exec.poststart gets run in the host once the normal /etc/rc startup process (including any enabled packages) finishes. This lets you write scripts to glue jails together.

Similarly, you can use the exec.prestop option to run a command on the host before stopping the jail. When the sysadmin turns the jail off, the host first runs this command, and then the jail runs the normal shutdown command.

The exec.stop command tells FreeBSD what command to run inside the jail to shut the jail down. If you're simulating a full jail, you'll probably run /bin/sh /etc/rc.shutdown as in our example in the previous section.

# Jail Defaults

You'll find that many of your jails share common settings. You can define those settings in the front of the configuration. All jails will use those settings unless you override them. This doesn't seem to make much sense when using a single jail.

```
exec.start="/bin/sh /etc/rc";
exec.stop="/bin/sh /etc/rc.shutdown";
exec.clean;
mount.devfs;

mariadb {
    host.hostname="mariadb.mwl.io";
    ip4.addr="203.0.113.221";
    path="/jail/mariadb";
}
```

Given this configuration, though, adding another jail becomes five lines including the braces.