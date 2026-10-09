![](bbox=[0.15, 0.09, 0.82, 0.43])

**Figure 12-8. Add A Print Queue SMIT panel**

You can also use the Web-Based System Manager, using the `wsm` command, to configure printers. The main WebSM printer window is shown in Figure 12-9.

# LPD DAEMON

Inbound print requests from a TCP/IP-based network are managed by the `/usr/sbin/lpd` daemon. The `lpd` daemon manages incoming job requests from the network and deposits them into the appropriate queues for subsequent processing by `qdaemon`. Like `qdaemon`, the `lpd` daemon is a subsystem that can be started as part of system boot and shutdown processing by adding it to `/etc/inittab`, or as required from the command line. The `/var/spool/lpd/stat/pid` file contains the PID of the currently running `lpd` daemon.

```
`# startarc -s lpd <----— Start lpd daemon`
`# refresh -s lpd <----— Refresh lpd daemon`
`# stoparc -s lpd <----— Stop lpd daemon`
```