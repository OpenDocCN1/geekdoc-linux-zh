the following:” dialog box, check to make sure that the parport, parport_pc, and lp kernel modules have been loaded. You can do this by using the `lsmod` (list modules) command like this:

```
$ /sbin/lsmod

Module           Size  Used by
parport_probe    2960  0 (autoclean)
parport_pc       5620  1 (autoclean)
lip              4476  0 (autoclean)
...
```

If the modules have not been loaded, make sure that your Red Hat (or Mandrake) module configuration file, `/etc/conf.modules`, contains the following line:

```
alias parport_lowlevel parport_pc
```

If Linux still doesn’t recognize an attached printer, go back and make sure that the printer cables are properly attached on both ends and that the printer is turned on. If you use a lomega parallel-port Zip drive, check to make sure the `paride.o` module is unloaded from memory (using the `rmmod` command). After you get your printer working, you can try to use both devices with module support in memory. Next, click the OK button. You’ll see the **Edit Local Printer Entry** dialog box, shown in Figure 14.2.

Note the information returned in this dialog box. The `printtool` command assigns a default name, such as lp, but you can change this to any name you like. Also note the printer device recognized by Linux, such as `/dev/lp0`. When finished, click the Select button to continue. You’ll see the large dialog box shown in Figure 14.3.

![](bbox=[0.18, 0.67, 0.93, 0.88])

**Figure 14.2** Use the `printtool` Edit Local Printer Entry dialog box to name a printer and select additional print-filter options.