This produces the output shown here:

```
keytable	0:off	1:on	2:on	3:on	4:on	5:on	6:off
atd		0:off	1:off	2:off	3:on	4:on	5:on	6:off
syslog	0:off	1:on	2:on	3:on	4:on	5:on	6:off
gpm		0:off	1:on	2:on	3:on	4:on	5:on	6:off
sendmail	0:off	1:off	2:on	3:on	4:on	5:on	6:off
kudzu		0:off	1:off	2:off	3:on	4:on	5:on	6:off
microcode_ctl	0:off	1:off	2:off	3:off	4:on	5:off	6:off
netfs		0:off	1:off	2:off	3:on	4:on	5:on	6:off
```

As you can see, this is a useful command because it shows you the state of the daemon (on the left) in each of the runlevels. All you have to do is decide whether you want them on or off in various runlevels.

To set a particular service to be on in a set of runlevels, use this command:

```
chkconfig --levels 345 smb on
```

> Be aware that using the `--levels` option affects only the specified runlevels. If you have a daemon configured in runlevel 2, the previous command does not affect it.

This turns on the smb (Samba) daemon in runlevels 3, 4, and 5, which can be verified with this command:

```
chkconfig --list | grep smb
```

This produces the following output:

```
smb			0:off	1:off	2:off	3:on	4:on	5:on	6:off
```

If you want to add a particular daemon to be managed by `chkconfig`, use the `--add` option, like so:

```
chkconfig --add tarfoo
```

This sets the service tarfoo to have either a start or a kill entry in particular runlevels (set in the daemon or service itself and read by `chkconfig`) making it fully configurable by `chkconfig`.

You should note that the last displayed set of daemons are the ones governed by the `inetd` or `xinetd` daemon.

# # Single User Mode

Sometimes going into maintenance or single user mode is necessary, even desirable, for a sysadmin. If you have a disk that needs fsck'ing, you'll most