# ## Switching Print Systems

To make it easy to switch your print system from LPing to CUPS (or back again), Red Hat provides a tool to manage all the hard work. From the Extras menu, select the System Settings submenu and then select Print System Switcher. Alternatively you can launch `redhat-switch-printer` from the command line or `redhat-switch-printer-nox` if you’re in a nongraphical environment.

![](bbox=[0.28, 0.27, 0.72, 0.49])

After you’ve selected your print system of choice, you’ll still need to actually stop the old print system and start the new one by hand.

```
```bash
[root@scribe /root]# /etc/init.d/lpd stop
[root@scribe /root]# /etc/init.d/cups start
```
```

Don’t forget to check your settings in `redhat-config-services` or the rc directories, as your settings from lpd don’t carry over automatically.

```
```bash
[root@scribe rc3.d]# rm K10cups
[root@scribe rc3.d]# ln -s ../init.d/cups S90cups
```
```

# ## CUPS Server Setup

The preferred method for setting up a CUPS server is to use the web-based administration interface. Unlike GUI tools that were attached as an afterthought by a third party, the CUPS web interface is thoroughly integrated into the CUPS system and is as capable as any other configuration method (although CUPS has its share of third-party GUI tools as well). Command-line tools also exist for CUPS configuration if you’re working in a nongraphical environment. Directly editing the configuration files is rarely ever necessary.