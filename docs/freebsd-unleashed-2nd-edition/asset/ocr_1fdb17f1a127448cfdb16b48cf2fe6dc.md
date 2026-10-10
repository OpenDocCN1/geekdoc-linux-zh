the baton stops twirling for a long period of time, it probably means your system is hanging. If that happens, refer to Appendix C, “Troubleshooting Installation and Boot Problems.” The system will load a few items, and then you should see a message like this:

```
FreeBSD/1386 bootstrap loader, Revision 0.8
(jkh@bento.freebsd.org, Mon Nov 20 11:41:23 GMT 2000)

Hit [Enter] to boot immediately, or any other key for command prompt.
Booting [kernel] in 9 seconds…-
```

Go ahead and press Enter to continue. At some point during this process, you will also be asked to remove the boot floppy and insert the mfsroot floppy. When this happens, simply proceed as instructed and then press Enter so the kernel will finish booting. A flurry of messages will go past your screen as the kernel detects and initializes the hardware in your system. If your system hangs at any point during this period, see Appendix C for help on troubleshooting installation problems.

# # Navigating the Sysinstall Program

After the kernel has finished booting (and assuming you didn’t run into any problems), you will be placed into the FreeBSD Sysinstall program. The first screen you see looks like Figure 2.1.

![](bbox=[0.28, 0.56, 0.71, 0.75])

You can’t use the mouse in Sysinstall, but the program is easy to navigate. Table 2.1 lists the navigation keys you can use in Sysinstall.