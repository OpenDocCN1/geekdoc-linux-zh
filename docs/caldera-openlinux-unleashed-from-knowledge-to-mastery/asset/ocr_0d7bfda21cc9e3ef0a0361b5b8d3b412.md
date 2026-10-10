Message Block). TCP/IP is the protocol used in many non-Microsoft environment (especially UNIX environments) and SMB has been available in Microsoft environments since 1987. Caldera OpenLinux supports both protocols. However, the installation of the SMB environment requires an additional installation of Samba, which is provided on the Caldera OpenLinux media. Both SMB and Samba are covered more fully in Chapter 16.

The steps for adding a remote printer capability to Caldera are very similar to those for setting up a local printer. The remote printer is included in the local */etc/printcap* if you wish to verify any of the parameters.

Although you may use LISA or edit specific files to create a remote printer, COAS may be the simplest method to use.

All of this should be familiar from the section entitled "Using COAS to ‘Administrative' your Printer.'".

+   1. Select Printer and then Add from the screen in Figure 9.5.
+   2. Select Generic Remote Printer from the COAS Select Printer Model dialog box shown in Figure 9.7.

# FIGURE 9.7
The COAS Select Printer Model dialog box.

![](bbox=[0.22, 0.5, 0.82, 0.81])

# **Note**

Be very careful. Generic Remote Printer is near the end of the list and and is followed by Generic PostScript Printer. If you don't select a remote printer, you will set up a local printer, which is not what you are trying to do here.