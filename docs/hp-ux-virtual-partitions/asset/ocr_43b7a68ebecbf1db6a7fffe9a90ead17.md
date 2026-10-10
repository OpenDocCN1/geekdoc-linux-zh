# Virtual Partition Installation with Ignite-UX

This section contains a step-by-step procedure to set up an Ignite-UX server to install vPars. This procedure was supplied by HP lab engineer Geoff Blaha. Since you’ll be installing many instances of HP-UX 11i and vPars software in a vPars environment, this procedure may save you a lot of time.

In examples in early chapters, we simply specified the name of the Virtual Partition we wanted to boot, such as **vparboot -p cable1**. With this form of **vparboot** we specify a boot kernel on the local system with the *-b* option. The man pages for **vparboot** and the other vPar commands are found in Appendix A.

# Ignite-UX and vPars Cookbook

![](bbox=[0.08, 0.45, 0.16, 0.56])

Use the **vparboot** command from a Virtual Partition to install HP-UX and vPar software to a target vPar. An Ignite-UX server is used as the source depot for this installation process.

The following is an overall vPars installation process (assuming that a new server is being installed)

+   - Install the server and peripherals
+   - Install any required patches for vPars (i.e., Gold Quality Pack, etc.)
+   - Install HP-UX 11i (stand-alone.)
+   - Install vPars software.
+   - Plan for desired vPars.

![](bbox=[0.08, 0.73, 0.16, 0.82])

+   - Create vPars using the **vparcreate** command: this creates the vPars database*/stand/vpdb*.
+   - Shut down HP-UX and place the server into BCH (Boot Console Handler) mode.
+   - Boot from the HP-UX/vPars disk and stop (interact) at the ISL prompt.
+   - Load and run the vPars monitor.

+   - Boot the first vPar (previously installed) with the **vparload** command.
+   - Use the **vparboot** command to install HP-UX and vPars software to all remaining vPars. Use the *Ctrl/A* command to switch the virtual console