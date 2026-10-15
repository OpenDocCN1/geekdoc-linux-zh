Based on the patterns selected, you might have to accept certain dependencies. If that happens, click OK to return to the installation wizard.

+   5. Click Accept to start the installation. A confirmation window is displayed.
+   6. Click Install. Installation begins, which you can watch as it happens.

# Booting your new Linux system from disk

After the first part of installation completes, your Linux system shuts down. Return to your z/VM 3270 session. IPL the newly installed system from disk to continue the installation.

To boot your new Linux system from disk:

+   1. Observe the following messages as the system powers down:
+   Power down.
+   00: HCPGSP2629I The virtual machine is placed in CP mode due to a SIGP stop from CPU 01.
+   01: HCPGSP2630I The virtual machine is placed in CP mode due to a SIGP stop and store status from CPU 01.

+   2. Boot the new kernel: IPL the disk using the command ipl 100 (where 100 is the disk address of the boot record):

```
==> ipl 100
00: ZIPL v1.6.3 interactive boot menu
00:
00: 0. default (ipl)
00:
00: 1. ipl
00: 2. failsafe
00: 3. ipl
00: 4. failsafe
00:
00: Note: VM users please use '#cp vi vmsg <number> <kernel-parameters>'
00:
00: Please choose (default will boot in 10 seconds):
```

+   3. At this prompt, either wait 10 seconds for the default IPL to proceed or try to type the following command, if you can type quickly enough:

```
#cp vi vmsg 0
```

The installation program brings up an SSH server again, as shown in Figure 4-31 on page 213, so you can begin completing the installation.