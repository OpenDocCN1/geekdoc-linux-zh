use it. For a documentation server, you not only have to install the language locale, but you also must install the documents written for that specific language.

```
`# smit chdoclang`
```

# ## Manage Remote Reboot Facility

You can, if you desire, remotely reboot your systems as shown in the next illustration. I never use this facility because it is a security violation at my shop. However, there is a place for it. If you are doing remote installation and updates that require a reboot, then this facility can save a lot of time. The Remote Reboot Facility is activated by using the SMIT FastPath **sm**it **rrb tty**. Once you activate a port for this purpose, you must not use it for anything else.

```
`# smit rrb tty`
```

![](bbox=[0.08, 0.45, 0.9, 0.58])

# ## Manage System Hang Detection

This is new to AIX 5L. If your system *hangs*, this facility gives you the ability to take some kind of action. By default, it will not do anything. It is up to you to specify what corrective measure you want the machine to take. A shell script can be used to instruct the system how to react to a system hang condition. This is part of IBM's *self-healing* Project eLiza strategy that is an ongoing development effort. Use the SMIT FastPath **smit shd** to set up hang detection, as shown in Figure 8-10.

```
`# smit shd`
```

# ## PTY

The AT&T-style pseudo-TTYs (PTYs) are not allocated automatically under AIX 4 or 5L. The number of PTYs must be specified for both AT&T and BSD-style devices as