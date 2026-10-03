+   - Manage serial ports. Configure and manage existing serial ports.
- Manage Log Viewer. View application and command-line messages and manage log files.

The console can retrieve toolboxes from the server. These toolboxes are descriptions of organized collections of tools available on a server. After one of these toolboxes is loaded, the console displays it and the tools referenced in it.

The Solaris Management Console can also run in a terminal (non-graphical mode) for use over remote connections or non-interactively from a script.

# Using SMC

The Solaris Management Console is installed when you install the Solaris 8 operating environment version 1/01 or later, and is started at bootup by the /etc/init.d/init.wbem script. At any time, you can check the status of the SMC server by typing the following:

```
/etc/init.d/init.wbem status
```

If SMC is running, you get the following message:

```
SMC server version 2.0.0 running on port 898.
```

# STEP BY STEP

# 19.1 Using SMC

+   1. Start the Solaris Management Console by typing the following:
   `/usr/sbin/smc &`

On a bitmaped display, you see SMC initializing with the screen shown in Figure 19.1.