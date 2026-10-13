If the local system is connected to more than one network, you can specify them with the interfaces directive, as shown here. Of course, the devices and network addresses should be changed appropriately.

```
; interfaces = lo eth0 192.168.12.2/24 192.168.13.2/24
```

If you activate the hosts allow directive, that action can limit access to the specified network(s). The following default would limit access to the networks with the 192.168.12.0 and 192.168.13.0 network IP addresses, as well as the local computer (127.):

```
; hosts allow = 127. 192.168.12. 192.168.13.
```

It's possible to configure a hosts deny directive in a similar fashion. With such directives, you can set up host-based security for Samba. In the global section, such security would apply server-wide. You can also use the hosts allow and hosts deny directives in the definitions for individual shared directories, as described later in this chapter.

# Logging Options

The next section sets up logging options, as indicated by the following label:

```
#---------- Logging Options ----------
```

The log file directive as shown sets up separate log files for every machine that connects to this Samba server, based on its machine name (%m). By default, the log file is limited to 50KB. As suggested by the comment, log files that exceed the given size are rotated. If logs exceed that size, you'll still see them in the /var/log/samba directory with the .old extension.

```
# logs split per machine
log file = /var/log/samba/%m.log
# max 50KB per log file, then rotate
max log size = 50
```

# Standalone Server Options

The following section sets up security options, based on configuration as a standalone server:

```
#---------- Standalone Server Options ----------
```