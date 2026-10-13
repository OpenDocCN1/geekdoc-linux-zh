Table 27-3: System Runlevels (States)

| State | Description |
|---|---|
| 3 | Full multuser mode with login to command-line interface; allows remote file sharing with other systems on your network. Also referred to as the *text mode state*. |
| 4 | Unused. |
| 5 | Full multuser mode that starts up in an X session, initiating a graphical login; allows remote file sharing with other systems on your network (same as 3, but with graphical login). |
| 6 | Reboots; shuts down and restarts the system (do *not* set the default to this). |

# initab Runlevels

When your system starts up, it uses the default runlevel as specified in the default *init* entry in the */etc/inittab* file. For example, if your default init runlevel is 5 (the graphical login), the default *init* entry in the */etc/inittab* file would be

```
id:5:initdefault:
```

You can change the default runlevel by editing the */etc/inittab* file and changing the *init* default entry. Editing the */etc/inittab* file can be dangerous. You should do this with great care. As an example, if the default runlevel is 3 (command line), the entry for your default runlevel in the */etc/inittab* file should look like the following:

```
id:3:initdefault:
```

You can change the 3 to a 5, to change your default runlevel from the command line interface (3) to the graphical login (5). Change only this number and nothing else.

```
id:5:initdefault:
```