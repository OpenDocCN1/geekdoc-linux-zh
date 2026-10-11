![](bbox=[0.93, 0.14, 0.98, 0.19])

After installing the PatchDiag tool, run the script. The script produces a text file that will show you the patches that are not current on the server.

To download a specific patch, go to the SunSolver Online home page (http://sunsolve.sun.com) and click the link Solaris Patches under the Patches section. To find the patches that you need to download, select the operating system and hardware that applies to your server or workstation.

For example, if you chose "Solaris 8.0 (SunOS 5.8) SPARC," the next Web page would show the current patches for the Solaris 8 operating system and the SPARC architecture. You can select an HTTP or FTP download. The Web page also includes a README file that details exactly what the patch fixes. In some cases, you might have no need to update a patch on a server. For example, Patch 110932-01 is a fix for a DHCP agent's use of the CPU when the lease exceeds 48 days. If your network or your server does not use DHCP, there is no need to use this patch.

A recommended Patch Cluster is an accumulation of all released patches for an operating system and hardware architecture. These patches fix operating system problems and the latest security problems. Maintenance Updates are patches that have been tested to work together, whereas the Patch Cluster just includes the latest patches all together. Sometimes the patchdiag tool will report that you need a patch that is newer than one of the patches in a Patch Cluster. It will have to be downloaded and patched by itself because the Patch Clusters are not built regularly.

# Useful Diagnostics Commands

To view detailed system configuration information, give the following command: `prtdiag -v ->`

The main use of this command is to show you what the kernel "sees." For example, if an Ethernet card's device driver is not shown with this command, higher-level functions such as TCP/IP will not be possible.

To view current system information, use the following command (the command is similar to the prtdiag command but not as detailed): `/usr/sbin/prtconf`

Another useful command is the psinfo command, which shows the CPU and clock speed. You can call this command from the shell as follows: `/usr/sbin/psinfo -v`

For TCP/IP troubleshooting, use the arp command. This command shows the Address Resolution Protocal (ARP) table, which in turn shows how the system resolves IP addresses to host names.

Troubleshooting