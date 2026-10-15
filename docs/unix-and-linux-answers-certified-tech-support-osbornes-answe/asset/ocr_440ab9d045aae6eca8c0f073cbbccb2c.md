![](bbox=[0.307, 0.095, 0.838, 0.397])

**Figure 11-6** You’ll need to add an LPR Port to your Windows NT printing system to connect to a remote lpr printer

UNIX machines. However, if you’re using one of the SMB products, many will allow you to add a Windows or Windows NT shared printer into the native UNIX print spooler. These printers will use a simple passthrough interface script that sends the entire job, unmanipulated, to the Windows NT spooling system to manage.

Alternatively, the NFS servers available for Windows NT generally include support for NFS printers, and there are other third-party and freeware lpd solutions available as well. But the best bet is to let UNIX manage the printers—it

![](bbox=[0.278, 0.742, 0.875, 0.85])

**Figure 11-7** Type in the machine name or IP address and the printer name to complete the addition of a remote lp printer to Windows NT