+   - **Resolution** — Select the default printing resolution (such as 300, 600, or 1,200 dots per inch). Higher resolutions result in better quality, but take longer to print.
+   - **EconoMode** — Either use the printer’s current setting or choose a mode where you save toner or one where you have the highest possible quality.

> **NOTE:** For a description of other driver options, refer to the CUPS Software User Manual (`/usr/share/doc/cups-* /sum.html`) under the *Standard Printer Options* heading.

Click Apply when you are satisfied with the changes you made to the local printer.

# Configuring remote printers

To use a printer that is available on your network, you must identify that printer to your Fedora or RHEL system. Supported remote printer connections include Networked CUPS (IPP) printers, Networked UNIX (LPD) printers, Networked Windows (SMB) printers, Networked Novell (NCP) printers, and JetDirect printers. (Of course, both CUPS and UNIX print servers can be run from Linux systems, as well as other UNIX systems.)

In each case, you need a network connection from your Fedora or RHEL system that enables you to reach the servers to which those printers are connected. To use a remote printer, of course, requires that someone set up that printer on the remote server computer. See the section “Configuring Print Servers” later in this chapter for information on how to do that in Fedora and RHEL.

You can use the Printer configuration window to configure each of the remote printer types:

+   1. From the GNOME desktop, select **System → Administration → Printing**.
+   2. Click **New Printer**. The **New Printer** window appears.
+   3. Besides the local ports listed (LPT and Serial ports), you can select one of the following types of network printers:
+      - **AppleSocket/HP JetDirect** — For a JetDirect printer.
+      - **Internet Printing Protocol (IPP)** — For a CUPS or other IPP printer.
+      - **LPD/LPR Host or Printer** — For a UNIX printer.
+      - **Windows Printer via SAMBA** — For a Windows system printer.
+   4. Continue following the steps in whichever of the following sections is appropriate.

# Adding a remote CUPS printer

After choosing to add an Internet Printing Protocol (IPP) CUPS printer from the Select Connection window, you must add the following information to the window that appears:

+   - **Hostname** — The host of the computer to which the printer is attached (or otherwise accessible). This can be an IP address or **TCP/IP** hostname for the computer (the **TCP/IP**