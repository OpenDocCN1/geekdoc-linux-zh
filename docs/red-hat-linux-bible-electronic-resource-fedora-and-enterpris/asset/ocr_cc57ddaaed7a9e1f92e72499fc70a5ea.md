# Reorganizing or removing run-level scripts

There are several ways to deal with removing programs from the system start-up directories, adding them to particular run levels, or changing when they are executed. From a Terminal window, you can use the *chkconfig* command. From a GUI, use the Service Configuration window.

> CAUTION: You should never remove the run-level file from the */etc/init.d* directory. Because no scripts are run from the */etc/init.d* directory automatically, it is okay to keep them there. Scripts in */etc/init.d* are only accessed as links from the */etc/rcX.d* directories. Keep scripts in the init.d directory so you can add them later by re-linking them to the appropriate run-level directory.

To reorganize or remove run-level scripts from the GUI, use the Service Configuration window. Either click System Settings → Services or log in as root user and type the following from a Terminal window:

```
# *serviceconf* &
```

Figure 12-1 shows an example of the Service Configuration window.

![](bbox=[0.08, 0.42, 0.6, 0.68])

**Figure 12-1:** Reorganize, add, and remove run-level scripts from the Service Configuration window.

The Service Configuration window lets you reconfigure services for run levels 3, 4, and 5. The run levels that you are currently running and currently editing are displayed near the top of the screen. Services that are available for the run level appear in the middle of the frame, with check marks next to the ones configured to start at that level. Here is what you can do from this window:

+   * **Add** — Click the box next to each service you want to start automatically at that run level so that a check mark appears in the box.