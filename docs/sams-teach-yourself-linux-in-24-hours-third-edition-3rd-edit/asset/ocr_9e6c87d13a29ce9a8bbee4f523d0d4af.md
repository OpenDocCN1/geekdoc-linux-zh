![](bbox=[0.18, 0.2, 0.26, 0.32])

Many Linux distributions contain their own special tools for configuring a printer to work with the operating system. Linux-Mandrake uses DrakConf to set up a printer. The printer configuration tool in DrakConf is based on the Red Hat Linux Print System Manager (also known as printtool). TurboLinux uses the TurboPrintCfg utility to set up a printer. You'll find that the information requested by TurboPrintCfg is the same as printtool; only the interface is different.

No matter which printer configuration utility you choose, all of these programs write the information that you supplied to the /etc/printcap file.

![](bbox=[0.18, 0.5, 0.26, 0.62])

If you are unfamiliar with all the technical workings of the Linux printing system, it is recommended that you use one of the printer configuration utilities to set up a printer. Editing the file improperly can cause problems with the other configuration utilities later on. Only experienced users should manually edit the /etc/printcap file to create printing services.

# Task: Setting Up a Local Printer

You can use a variety of distribution-specific tools to set up your printer to work with Linux, but most of them look vaguely similar to the Red Hat Linux Print System Manager tool, or printtool for short. Here's how to use the printtool to write the printer configuration information to the /etc/printcap file:

+   1. Log in to the superuser account.
+   2. Open a terminal emulator and type printtool and press Enter. You may see a series of error messages that inform you of packages that are not installed on the system. Click OK to clear the error messages and to display the main printtool window, as shown in Figure 11.2.
+   3. Click the Add button. This displays the Add a Printer Entry dialog box.
+   4. Select the Local Printer option and click OK. The printtool auto-detects which printer device is in use and displays the detected ports in the Info dialog box. Make a note of the detected device. Make sure it is the same device detected by the dmesg command, and click OK to close the Info dialog box. The Edit Local Printer Entry dialog box appears, as shown in Figure 11.3.