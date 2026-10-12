# **Listing 2-1** *Continued*

```
```
pr:12345:powerokwait:/sbin/shutdown -c “Power Restored; \\
Shutdown Cancelled”

# Run getty's in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6

# Run xdm in runlevel 5
x:5:respawn:/etc/X11/prefdm -nodaemon
```
```

This file defines how init behaves during server startup or shutdown events. The following discussion takes a closer look at this file.

The init program ignores all the blank and comment lines (that is, lines that start with a #) in the /etc/initab file. The lines with colon-delimited fields are the init configuration lines. The syntax for such a line is as follows:

```
`id:runlevels:action:process arguments`
```

The first field is a unique label field to identify an entry in the file. An *id* can be 2 to 4 characters long. The second field, *runlevels*, defines which run levels this line applies to. The third field defines what action needs to be taken. The last field (*process*) defines which process needs to be run. Optionally, you can also specify command-line arguments for the process in the fourth field.

As mentioned before, a run level specifies a state of the system. The nine run levels are described in Table 2-1.

# **Table 2-1** *The Run Levels for init*

| Run Level | Description |
| :--- | :--- |
| 0 | Halt – used to halt the system. |
| 1 | Single-user – used to set the system in a minimal configuration suitable for a single user. |
| 2 | Not used. |