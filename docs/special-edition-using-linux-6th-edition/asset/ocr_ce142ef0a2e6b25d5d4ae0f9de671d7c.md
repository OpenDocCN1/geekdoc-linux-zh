> > **Note** Passwords in NetWare are not case sensitive, unlike in Linux.

# NETWARE CLIENT MESSAGE OPTIONS

The NetWare client for OpenLinux enables you to specify whether you want to receive broadcast messages sent by users, administrators, or system messages (from servers). Client message options are set for each server to which you are attached. The following syntax is used (Table 28.10 shows the possible command-line options for the nwmsg utility):

```
nwmsg [OPTIONS] none|system|all
```

**Table 28.10 — Command-Line Options for nwmsg**

| Options | Description |
|---|---|
| `-h` | Displays command help |
| `-a` | Modifies message options for all connections |
| `-s <SERVER>` | Modifies message options for specified server only |

Setting your NetWare client to receive messages from all sources can be accomplished by issuing the following command:

```
nwmsg -a all
```

To receive messages from the system administrator only for the OpenLinux NetWare server, you can issue the following command:

```
nwmsg -s OPENLINUX system
```

The previous command only modifies the message option for the OpenLinux server. All other connections remain unchanged. The nwwhoami utility displays the message options set for each server to which you are connected.

You can configure your NetWare client to not receive any messages from any system to which you are attached. If you want to do so, issue the following command:

```
nwmsg -a none
```

# ADMINISTRATION UTILITIES FOR NDS

Most Linux implementations do not include any NetWare administration utilities. However, Caldera OpenLinux eDesktop 2.4 ships with several utilities that enable you to administer a NetWare NDS tree. This section reviews each of these utilities. Table 28.11 contains a brief overview of each utility.